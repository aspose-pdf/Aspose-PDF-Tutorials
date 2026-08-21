---
category: general
date: 2026-08-20
description: Utwórz niestandardowy stan graficzny w PDF przy użyciu Aspose.Pdf. Dowiedz
  się, jak edytować zasoby PDF i dodać przezroczystość w PDF w kilku prostych krokach.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom graphics state
- edit pdf resources
- add transparency pdf
- Aspose.Pdf graphics state
- PDF resource dictionary
language: pl
lastmod: 2026-08-20
og_description: Utwórz niestandardowy stan graficzny w PDF przy użyciu Aspose.Pdf.
  Ten samouczek pokazuje, jak szybko edytować zasoby PDF i dodać przezroczystość do
  PDF.
og_image_alt: Screenshot of C# code that creates a custom graphics state in a PDF
og_title: Utwórz niestandardowy stan graficzny w PDF – przewodnik Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create custom graphics state in PDF with Aspose.Pdf. Learn how to edit
    PDF resources and add transparency PDF in just a few steps.
  headline: Create custom graphics state in PDF using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- Aspose.Pdf
- C#
- Graphics state
title: Utwórz niestandardowy stan graficzny w PDF przy użyciu Aspose.Pdf
url: /pl/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie niestandardowego stanu graficznego w PDF przy użyciu Aspose.Pdf

Jeśli potrzebujesz **utworzyć niestandardowy stan graficzny** w pliku PDF, ten przewodnik pokaże Ci dokładnie, jak to zrobić przy pomocy Aspose.Pdf dla .NET. Po zakończeniu tutorialu będziesz w stanie **edytować zasoby PDF**, wstrzyknąć nowy słownik stanu graficznego oraz **dodać zawartość PDF z przezroczystością** bez opuszczania projektu C#.

Zobaczysz kompletny, gotowy do uruchomienia przykład, wyjaśnienie, dlaczego każda linia ma znaczenie, oraz wskazówki dotyczące obsługi dokumentów wielostronicowych lub różnych trybów mieszania. Nie są wymagane żadne zewnętrzne narzędzia — wystarczy biblioteka Aspose.Pdf oraz podstawowe środowisko .NET.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

* .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.7+)
* Licencjonowaną kopię **Aspose.Pdf for .NET** (darmowa wersja próbna wystarczy do testów)
* Plik PDF wejściowy o nazwie `input.pdf` umieszczony w folderze, do którego możesz odwołać się w kodzie
* Visual Studio 2022 lub dowolne IDE obsługujące rozwój w C#

Tutorial zakłada, że znasz podstawową składnię C# oraz pojęcie stron PDF.

## Krok 1: Załaduj źródłowy PDF i uzyskaj dostęp do pierwszej strony

Pierwszą operacją jest otwarcie pliku PDF i pobranie strony, której zasoby chcesz zmodyfikować. Aspose.Pdf reprezentuje każdą stronę jako obiekt `Page`, a każda strona zawiera **słownik zasobów**, w którym przechowywane są stany graficzne, czcionki, XObjecty i inne elementy.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

// Load the PDF you want to edit
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Get the first page (pages are 1‑based in Aspose.Pdf)
    Page firstPage = pdfDocument.Pages[1];
```

*Dlaczego to ważne:* Klasa `Document` ładuje plik do pamięci, a `Pages[1]` daje bezpośredni dostęp do słownika zasobów pierwszej strony, czyli miejsca, w którym znajduje się stan graficzny.

## Krok 2: Otwórz słownik zasobów do edycji

Aspose.Pdf udostępnia pomocnika `DictionaryEditor`, który pozwala traktować słownik zasobów jak zwykły .NET‑owy `Dictionary`. Dzięki temu łatwo można odczytywać, dodawać lub zamieniać wpisy, takie jak `ExtGState`.

```csharp
    // Create an editor for the page’s resources
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Dlaczego to ważne:* `DictionaryEditor` abstrahuje niskopoziomowe obiekty COS, umożliwiając pracę z znanymi parami klucz/wartość, jednocześnie zachowując zgodność z PDF.

## Krok 3: Pobierz (lub utwórz) słownik ExtGState

Wpis **ExtGState** przechowuje wszystkie zewnętrzne obiekty stanu graficznego dla strony. Jeśli słownik nie istnieje, Aspose.Pdf utworzy dla Ciebie pusty.

```csharp
    // Ensure the ExtGState dictionary exists
    var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
        ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
        : new CosPdfDictionary(pdfDocument);
```

*Dlaczego to ważne:* Brak wpisu `ExtGState` spowodowałby później `KeyNotFoundException`. Ten warunek pozwala kodowi działać na PDF‑ach, które nigdy wcześniej nie definiowały niestandardowego stanu graficznego — kluczowy element odporności **edytowania zasobów PDF**.

## Krok 4: Zbuduj niestandardowy słownik stanu graficznego

Stan graficzny opisuje, jak renderowane są operacje rysowania. Aby **dodać przezroczystość PDF**, musisz ustawić wpisy `ca` (przezroczystość wypełnienia) i `CA` (przezroczystość obrysu), a opcjonalnie tryb mieszania (`BM`). Poniższy kod tworzy nowy słownik z tymi parametrami.

```csharp
    // Create an empty dictionary that will become the new graphics state
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Define the parameters you want for the custom state
    var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
    {
        // Stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        // Fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        // Blend mode – "Normal" is the default, but you can use "Multiply", "Screen", etc.
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };

    // Populate the dictionary with the parameters
    foreach (var param in graphicsStateParams)
        newGraphicsState.Add(param);
```

*Dlaczego to ważne:* Wpisy `ca` i `CA` kontrolują przezroczystość odpowiednio dla operacji wypełnienia i obrysu. Ustawienie `BM` pozwala eksperymentować z różnymi efektami kompozycji, co jest przydatne, gdy później **dodajesz zawartość PDF z przezroczystością**, taką jak półprzezroczyste kształty lub obrazy.

## Krok 5: Zarejestruj nowy stan graficzny pod unikalną nazwą

Każdy stan graficzny w słowniku `ExtGState` musi mieć unikalną nazwę (np. `GS0`, `GS1`). Możesz wybrać dowolną nazwę, która nie koliduje z istniejącymi wpisami.

```csharp
    // Choose a name that is unlikely to collide with existing states
    const string graphicsStateName = "GS0";

    // Add the new graphics state to the ExtGState dictionary
    extGStateDict.Add(graphicsStateName, newGraphicsState);

    // If the ExtGState entry was missing, attach it back to the page resources
    if (!resourcesEditor.ContainsKey("ExtGState"))
        resourcesEditor["ExtGState"] = extGStateDict;
```

*Dlaczego to ważne:* Wstawiając nowy słownik pod nazwą `GS0`, udostępniasz stan do odwołań w strumieniach zawartości strony. Warunkowy blok zapewnia, że wpis `ExtGState` jest obecny nawet w PDF‑ach, które początkowo go nie posiadały — kolejny **środek zabezpieczający edytowanie zasobów PDF**.

## Krok 6: Użyj niestandardowego stanu graficznego w zawartości strony (opcjonalnie)

Poprzednie kroki jedynie *definiują* stan graficzny. Aby zobaczyć efekt, musisz odwołać się do niego w strumieniu zawartości strony. Poniżej szybki przykład rysujący półprzezroczysty prostokąt przy użyciu właśnie utworzonego stanu.

```csharp
    // Get the page’s content stream (or create a new one if empty)
    var content = firstPage.Contents[1];
    var graphics = new ContentWriter(content);

    // Save current graphics state
    graphics.WriteOperator(OperatorName.SaveState);
    // Set the custom graphics state we just defined
    graphics.WriteOperand($"/{graphicsStateName}");
    graphics.WriteOperator(OperatorName.SetExtGState);
    // Draw a rectangle (coordinates are in points)
    graphics.WriteOperand(100);   // lower‑left x
    graphics.WriteOperand(500);   // lower‑left y
    graphics.WriteOperand(200);   // width
    graphics.WriteOperand(100);   // height
    graphics.WriteOperator(OperatorName.Rectangle);
    // Fill the rectangle using the current fill opacity (ca = 0.5)
    graphics.WriteOperator(OperatorName.Fill);
    // Restore the previous graphics state
    graphics.WriteOperator(OperatorName.RestoreState);
```

*Dlaczego to ważne:* Operator `SetExtGState` (`gs`) instruuje renderer PDF, aby zastosował parametry zdefiniowane w `GS0`. Prostokąt pojawi się z 50 % przezroczystością wypełnienia, podczas gdy jego obrys pozostanie w pełni nieprzezroczysty.

## Krok 7: Zapisz zmodyfikowany PDF

Na koniec zapisz zmiany na dysku. Możesz nadpisać oryginalny plik lub utworzyć nowy.

```csharp
    // Save the updated PDF
    pdfDocument.Save("YOUR_DIRECTORY/output_with_custom_gs.pdf");
}
```

Po otwarciu `output_with_custom_gs.pdf` w przeglądarce PDF powinieneś zobaczyć półprzezroczysty prostokąt na pierwszej stronie. Potwierdza to, że pomyślnie **utworzyłeś niestandardowy stan graficzny**, **edytowałeś zasoby PDF** i **dodałeś zawartość PDF z przezroczystością**.

## Typowe warianty i przypadki brzegowe

| Sytuacja | Co dostosować |
|-----------|----------------|
| **Wiele stron wymaga tego samego stanu** | Zarejestruj stan graficzny raz (kroki 1‑5) i odwołuj się do `GS0` w strumieniach zawartości dowolnej strony. |
| **Różna przezroczystość dla poszczególnych elementów** | Zdefiniuj dodatkowe stany (`GS1`, `GS2`, …) z innymi wartościami `ca`/`CA` i przełączaj je przy pomocy `SetExtGState`. |
| **Tryb mieszania inny niż Normal** | Zamień `"Normal"` na `"Multiply"`, `"Screen"` lub dowolny standardowy tryb mieszania PDF w wpisie `BM`. |
| **Kolizja nazw** | Przed dodaniem sprawdź `extGStateDict.ContainsKey(yourName)` i wybierz unikalny sufiks, jeśli to konieczne. |
| **PDF już zawiera słownik ExtGState** | Kod w Kroku 3 już ponownie wykorzystuje istniejący słownik, więc nie jest wymagana dodatkowa obsługa. |

**Wskazówka:** Pracując z dużymi plikami PDF, umieść użycie `Document` w bloku `using` (jak pokazano), aby szybko zwolnić zasoby natywne. Rozważ także włączenie właściwości `PdfCompliance` Aspose.Pdf, jeśli musisz zagwarantować zgodność z PDF/A lub PDF/X po edycji zasobów.

## Pełny działający przykład

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Load the PDF you want to edit
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 1: Get the first page
            Page firstPage = pdfDocument.Pages[1];

            // Step 2: Open the page resources for editing
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 3: Retrieve or create the ExtGState dictionary
            var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
                ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
                : new CosPdfDictionary(pdfDocument);

            // Step 4: Build a custom graphics state (50 % fill opacity, 100 % stroke opacity)
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var param in graphicsStateParams)
                newGraphicsState.Add(param);

            // Step 5: Register the graphics state under the name GS0
            const string graphicsStateName = "GS0";
            extGStateDict.Add(graphicsStateName, newGraphics


## Co powinieneś nauczyć się dalej?


Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz wyjaśnienia krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i poznać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Create PDF with Aspose – Add Form Field and Pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [How to Create Custom Tables in PDFs Using Aspose.PDF .NET](/pdf/english/net/tables-lists/create-custom-tables-in-pdfs-aspose-pdf-dot-net/)
- [Create Custom Pdf Stamps Aspose Pdf Net](/pdf/hongkong/net/images-graphics/create-custom-pdf-stamps-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}