---
category: general
date: 2026-09-08
description: Dodaj przezroczystość do pliku PDF za pomocą Aspose.PDF dla .NET – dowiedz
  się, jak ustawić przezroczystość obrysu i wypełnienia, tryb mieszania oraz zapisać
  wynik w kilka minut.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- aspose.pdf transparency
- pdf graphics state
- extgstate dictionary
- pdf opacity settings
language: pl
lastmod: 2026-09-08
og_description: Dodaj przezroczystość do pliku PDF przy użyciu Aspose.PDF dla .NET.
  Ten samouczek pokazuje, jak zmodyfikować słownik ExtGState, ustawić krycie i tryb
  mieszania oraz zapisać zaktualizowany plik.
og_image_alt: Screenshot of a PDF page showing semi‑transparent shapes created with
  Aspose.PDF
og_title: Dodaj przezroczystość do PDF za pomocą Aspose.PDF – przewodnik krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Add transparency to PDF with Aspose.PDF for .NET – learn to set stroke
    and fill opacity, blend mode, and save the result in minutes.
  headline: How to add transparency to PDF files using Aspose.PDF for .NET
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: How to add transparency to PDF files using Aspose.PDF for .NET
url: /pl/net/images-graphics/how-to-add-transparency-to-pdf-files-using-aspose-pdf-for-ne/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak dodać przezroczystość do plików PDF przy użyciu Aspose.PDF dla .NET

Jeśli potrzebujesz **dodać przezroczystość do PDF** dokumentów, ten przewodnik pokazuje dokładnie, jak zmodyfikować stan graficzny przy użyciu Aspose.PDF dla .NET. Nauczysz się ustawiać przezroczystość obrysu, wypełnienia oraz tryb mieszania na jednej stronie, a następnie zapisać wynik jako nowy plik.

Przezroczystość jest częstym wymogiem przy znakach wodnych, nakładkach graficznych lub efektach wizualnych w raportach. W tym samouczku zobaczysz kompletny, działający kod, zrozumiesz, dlaczego każde wywołanie API ma znaczenie, oraz otrzymasz wskazówki dotyczące obsługi przypadków brzegowych, takich jak brakujące wpisy zasobów.

## Czego będziesz potrzebować

* .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.6+)
* Ważna licencja Aspose.PDF dla .NET (bezpłatna wersja próbna działa do testów)
* Plik PDF wejściowy o nazwie `input.pdf` umieszczony w folderze, do którego możesz odwołać się w kodzie
* Środowisko programistyczne C# (Visual Studio, Rider lub VS Code)

Nie są wymagane dodatkowe pakiety NuGet poza `Aspose.Pdf`.

## Przegląd stanu graficznego PDF

Stan graficzny PDF jest przechowywany w **słowniku ExtGState** wewnątrz słownika zasobów strony. Każdy wpis definiuje parametry renderowania, takie jak grubość linii, przezroczystość i tryb mieszania. Tworząc nowy obiekt stanu graficznego i dodając go do słownika `ExtGState`, możesz ponownie używać tych samych ustawień przezroczystości w wielu poleceniach rysowania.

Zrozumienie tej struktury pomaga unikać typowych pułapek, takich jak próba ustawienia przezroczystości bezpośrednio na obiekcie `Page` (co nie jest obsługiwane przez API). Zamiast tego pracujesz z niskopoziomowymi obiektami COS, które odwzorowują się jeden‑do‑jeden ze specyfikacją PDF.

## Krok 1: Załaduj dokument PDF

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Cos;

// Load the source PDF
var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");
```

*Dlaczego ten krok?*  
`Document` jest punktem wejścia dla wszelkiej manipulacji PDF. Załadowanie pliku tworzy reprezentację w pamięci, którą możesz edytować bez modyfikacji oryginalnego pliku na dysku.

## Krok 2: Pobierz pierwszą stronę i jej edytor słownika zasobów

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor provides convenient access to the page’s resources
var resourceEditor = new DictionaryEditor(page.Resources);
```

*Dlaczego ten krok?*  
Wszystkie wpisy stanu graficznego znajdują się wewnątrz zasobów strony. `DictionaryEditor` abstrahuje obsługę niskopoziomowego słownika COS, umożliwiając odczyt lub tworzenie wpisów takich jak `ExtGState`.

## Krok 3: Pobierz słownik ExtGState z zasobów strony

```csharp
// The ExtGState entry may already exist; if not, create it
CosPdfDictionary extGStateDict;
if (resourceEditor.ContainsKey("ExtGState"))
{
    extGStateDict = (CosPdfDictionary)resourceEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a new ExtGState dictionary and attach it to the page resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);
    resourceEditor.Add("ExtGState", extGStateDict);
}
```

*Dlaczego ten krok?*  
PDF może całkowicie pominąć słownik `ExtGState`. Powyższy kod bezpiecznie obsługuje zarówno istniejące, jak i brakujące przypadki, zapewniając, że samouczek działa z dowolnym plikiem PDF wejściowym.

## Krok 4: Utwórz nowy słownik stanu graficznego i zdefiniuj jego wpisy

```csharp
// Create an empty dictionary that will hold our transparency settings
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Define the entries:
//   CA – stroke opacity (0 = fully transparent, 1 = opaque)
//   ca – fill opacity
//   BM – blend mode (Normal, Multiply, etc.)
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity = 100%
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // Fill opacity = 50%
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Standard blend mode
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*Dlaczego ten krok?*  
`CA` i `ca` są operatorami PDF kontrolującymi przezroczystość dla operacji obrysu i wypełnienia (non‑stroking). Ustawienie `BM` na `Normal` zachowuje domyślne zachowanie kompozycji, ale możesz eksperymentować z `Multiply` lub `Screen` dla efektów artystycznych.

## Krok 5: Dodaj nowy stan graficzny do słownika ExtGState

```csharp
// Choose a unique name for the graphics state (e.g., GS0)
extGStateDict.Add("GS0", newGraphicsState);
```

*Dlaczego ten krok?*  
Nazwa `GS0` staje się odwołaniem, które możesz użyć później w strumieniach zawartości (`/GS0 gs`). Dodanie jej do `ExtGState` sprawia, że PDF jest świadomy nowych parametrów przezroczystości.

## Krok 6: Zastosuj stan graficzny w strumieniu zawartości (opcjonalnie)

Jeśli chcesz zobaczyć efekt od razu, możesz dodać na początek proste polecenie rysowania, które używa nowego stanu:

```csharp
// Build a content stream that draws a semi‑transparent rectangle
var content = new PageContent();
content.Operators.Add(new Operator("q"));                     // Save graphics state
content.Operators.Add(new Operator("GS0", "gs"));            // Set our custom graphics state
content.Operators.Add(new Operator("0.2", "0.2", "0.8", "rg")); // Set fill color (light blue)
content.Operators.Add(new Operator("100", "500", "200", "100", "re")); // Rectangle
content.Operators.Add(new Operator("f"));                    // Fill
content.Operators.Add(new Operator("Q"));                     // Restore graphics state

// Insert the new content at the beginning of the page
page.Contents.Insert(0, content);
```

*Dlaczego ten krok?*  
Opcjonalny fragment pokazuje, jak dodany stan graficzny (`GS0`) jest faktycznie używany. Prostokąt pojawi się z 50 % przezroczystością wypełnienia, podczas gdy jego obrys pozostanie w pełni nieprzezroczysty.

## Krok 7: Zapisz zmodyfikowany dokument PDF

```csharp
pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
```

Powstały plik, `output.pdf`, zawiera nowy wpis `ExtGState` oraz, jeśli dodałeś opcjonalną zawartość, półprzezroczystą nakładkę prostokąta.

### Oczekiwany wynik

Gdy otworzysz `output.pdf` w Adobe Acrobat Reader lub dowolnym przeglądarce PDF, powinieneś zobaczyć:

* Oryginalną zawartość strony bez zmian.
* Jeśli uruchomiłeś opcjonalny kod rysujący, jasnoniebieski prostokąt, którego wypełnienie jest w 50 % przezroczyste, pozwalając na prześwitowanie podkładu strony.

## Pełny listing źródłowy

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Operators;
using System.Collections.Generic;

class AddTransparencyExample
{
    static void Main()
    {
        // 1. Load the PDF
        var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2. Get the first page and its resources
        var page = pdfDoc.Pages[1];
        var resourceEditor = new DictionaryEditor(page.Resources);

        // 3. Retrieve or create ExtGState dictionary
        CosPdfDictionary extGStateDict;
        if (resourceEditor.ContainsKey("ExtGState"))
            extGStateDict = (CosPdfDictionary)resourceEditor["ExtGState"].ToCosPdfDictionary();
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);
            resourceEditor.Add("ExtGState", extGStateDict);
        }

        // 4. Create new graphics state with transparency settings
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);
        var graphicsStateEntries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // Fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
        };
        foreach (var entry in graphicsStateEntries)
            newGraphicsState.Add(entry);

        // 5. Add the graphics state to ExtGState with a unique name
        extGStateDict.Add("GS0", newGraphicsState);

        // 6. (Optional) Draw a rectangle using the new state
        var content = new PageContent();
        content.Operators.Add(new Operator("q"));
        content.Operators.Add(new Operator("GS0", "gs"));
        content.Operators.Add(new Operator("0.2", "0.2", "0.8", "rg"));
        content.Operators.Add(new Operator("100", "500", "200", "100", "re"));
        content.Operators.Add(new Operator("f"));
        content.Operators.Add(new Operator("Q"));
        page.Contents.Insert(0, content);

        // 7. Save the updated PDF
        pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

Skopiuj kod do aplikacji konsolowej, zamień `YOUR_DIRECTORY` na rzeczywistą ścieżkę folderu i uruchom ją. Program wygeneruje `output.pdf` z dodanymi ustawieniami przezroczystości.

## Typowe pułapki i jak ich uniknąć

| Objaw | Przyczyna | Rozwiązanie |
|-------|-----------|-------------|
| `KeyNotFoundException` on `"ExtGState"` | Strona nie ma wpisu `ExtGState`. | Samouczek już tworzy słownik, gdy brak; upewnij się, że używasz dostarczonego warunku warunkowego. |
| Transparency not visible in the viewer | Polecenia rysujące nigdy nie odwołują się do `GS0`. | Dodaj operator `gs` (`"GS0 gs"`) przed dowolnym poleceniem obrysu/wypełnienia, jak pokazano w opcjonalnym fragmencie. |
| PDF ulega uszkodzeniu po zapisaniu | Nieprawidłowe mieszanie wysokopoziomowych API `Page` z niskopoziomowymi obiektami COS. | Trzymaj się wzorca pobierania `CosPdfDictionary` przez `DictionaryEditor` i unikaj modyfikacji tego samego słownika dwukrotnie. |
| Blend mode has no effect | Przeglądarka nie obsługuje wybranego trybu mieszania. | Użyj `Normal` dla szerokiej kompatybilności; eksperymentuj z `Multiply` tylko w przeglądarkach, które zgłaszają wsparcie. |

## Kolejne kroki

Teraz, gdy wiesz, jak **dodać przezroczystość do PDF** plików, możesz:

* Zastosować ten sam stan graficzny do wielu stron, iterując po `pdfDoc.Pages`.
* Połączyć przezroczystość ze ścieżkami przycinania w celu zaawansowanego znakowania wodnego.
* Zbadać inne wpisy ExtGState, takie jak `SM` (regulacja obrysu) lub `CA`

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak dodać i wyrównać znaczniki tekstowe w PDF przy użyciu Aspose.PDF dla .NET \| Znaki wodne i tła](/pdf/english/net/watermarks-backgrounds/add-text-stamp-aspose-pdf-dotnet/)
- [Jak dodać obracający się znak wodny obrazu do PDF przy użyciu Aspose.PDF dla .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)
- [Jak dodać znaczniki stron w PDF przy użyciu Aspose.PDF dla .NET: Kompletny przewodnik](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}