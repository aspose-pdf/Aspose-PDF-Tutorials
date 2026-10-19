---
category: general
date: 2026-10-01
description: Dodaj niestandardowy ExtGState PDF przy użyciu Aspose.PDF, aby szybko
  ustawić przezroczystość w PDF. Postępuj zgodnie z tym przewodnikiem, aby dowiedzieć
  się, jak ustawić przezroczystość w PDF przy użyciu niestandardowego stanu graficznego.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom extgstate pdf
- how to set transparency pdf
- Aspose.PDF graphics state
- PDF opacity settings
- PDF blend mode tutorial
language: pl
lastmod: 2026-10-01
og_description: Dodaj własny ExtGState do PDF i dowiedz się, jak ustawić przezroczystość
  w PDF w kilku linijkach C#. Ten przewodnik obejmuje każdy krok, od wczytania pliku
  po zapisanie wyniku.
og_image_alt: Screenshot of a PDF page showing transparent graphics after adding a
  custom ExtGState
og_title: Dodaj niestandardowy ExtGState PDF – pełny samouczek Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Add custom ExtGState PDF using Aspose.PDF to set transparency PDF quickly.
    Follow this guide to learn how to set transparency PDF with a custom graphics
    state.
  headline: Add custom ExtGState PDF with Aspose.PDF – step‑by‑step guide
  type: TechArticle
tags:
- PDF
- Aspose.PDF
- C#
- GraphicsState
title: Dodaj własny ExtGState PDF przy użyciu Aspose.PDF – przewodnik krok po kroku
url: /pl/net/images-graphics/add-custom-extgstate-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj niestandardowy ExtGState PDF przy użyciu Aspose.PDF – przewodnik krok po kroku

Jeśli potrzebujesz **dodać niestandardowy ExtGState PDF**, aby kontrolować krycie i tryby mieszania, ten poradnik pokaże Ci dokładnie, jak to zrobić. Zobaczysz kompletny, działający przykład, który demonstruje **jak ustawić przezroczystość PDF** przy użyciu Aspose.PDF dla .NET.

W kolejnych sekcjach omówimy wymagany pakiet NuGet, szczegółowy podział kodu oraz wskazówki dotyczące obsługi przypadków brzegowych, takich jak wiele stron czy niestandardowe tryby mieszania. Po zakończeniu będziesz w stanie modyfikować dowolny istniejący PDF i zastosować przezroczysty stan graficzny bez opuszczania IDE.

## Prerequisites

- .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.7+)
- Visual Studio 2022 (lub dowolny edytor C#, którego preferujesz)
- Pakiet NuGet **Aspose.PDF for .NET** (wersja 23.12 lub nowsza)
- Przykładowy plik PDF o nazwie `input.pdf` umieszczony w folderze, do którego możesz odwołać się w projekcie

> **Porada:** Użyj dedykowanego folderu „Resources” w swoim rozwiązaniu, aby przechowywać razem pliki PDF wejściowe i wyjściowe. To zapobiega błędom związanym ze ścieżkami podczas uruchamiania kodu.

## Install Aspose.PDF

Otwórz konsolę NuGet Package Manager i uruchom:

```bash
dotnet add package Aspose.PDF
```

Pakiet dostarcza klasy `Aspose.Pdf.Document`, `CosPdfDictionary` oraz powiązane klasy używane w przykładzie kodu.

## Step 1 – Load the PDF document

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;

// Load the source PDF
using var pdfDocument = new Document("Resources/input.pdf");
```

**Dlaczego ten krok jest ważny:**  
`Document` reprezentuje cały plik PDF w pamięci. Otwieranie go w bloku `using` zapewnia zwolnienie wszystkich niezarządzanych zasobów po zakończeniu przetwarzania.

## Step 2 – Access the first page’s resource dictionary

```csharp
// Get the first page (pages are 1‑based in Aspose.PDF)
Page firstPage = pdfDocument.Pages[1];

// The resource dictionary holds objects like fonts, XObjects, and ExtGState entries
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

**Wyjaśnienie:**  
Każda strona PDF posiada słownik *Resources*, który grupuje obiekty wielokrotnego użytku. Edytując ten słownik możemy wstrzyknąć nowy stan graficzny, do którego strona będzie mogła odwołać się później.

## Step 3 – Retrieve (or create) the ExtGState dictionary

```csharp
// Try to get the existing ExtGState dictionary; create one if it does not exist
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    extGStateDict = new CosPdfDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", extGStateDict);
}
```

**Dlaczego najpierw sprawdzamy:**  
Niektóre pliki PDF już definiują wpis `ExtGState`. Dodanie duplikatu nadpisałoby istniejące stany i mogłoby zepsuć inną zawartość. Ten kod obronny zachowuje oryginalne wpisy.

## Step 4 – Build a custom graphics state

```csharp
// Create an empty dictionary that will become our custom graphics state
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the graphics state entries
var graphicsStateEntries = new[]
{
    // CA – stroke opacity (range 0‑1)
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),
    // ca – fill opacity (range 0‑1)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // BM – blend mode (Normal, Multiply, Screen, etc.)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

// Add each entry to the dictionary
foreach (var entry in graphicsStateEntries)
{
    newGraphicsState.Add(entry);
}
```

**Co robi każdy klucz:**

| Klucz | Znaczenie | Typowe wartości |
|-------|-----------|-----------------|
| `CA` | Krycie linii | `0.0` (całkowicie przezroczyste) → `1.0` (nieprzezroczyste) |
| `ca` | Krycie wypełnienia | Ten sam zakres co `CA` |
| `BM` | Tryb mieszania | `Normal`, `Multiply`, `Screen`, `Overlay` itd. |

Ustawiając `ca` na `0.5` sprawiamy, że wypełnione kształty są w 50 % przezroczyste, podczas gdy `CA` pozostaje w pełni nieprzezroczyste dla linii. Zmiana `BM` pozwala eksperymentować z efektami mieszania podobnymi do Photoshopa.

## Step 5 – Register the custom graphics state under a unique name

```csharp
// Choose a unique name for the new state, e.g., "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

**Konwencja nazewnictwa:**  
Specyfikacje PDF zalecają krótkie, wielkie identyfikatory. Użycie `GS0` (Graphics State 0) ułatwia odwoływanie się do nazwy w strumieniach zawartości.

## Step 6 – Apply the custom graphics state in a content stream (optional)

Jeśli chcesz narysować przezroczysty prostokąt na pierwszej stronie, możesz dodać następujące operatory na początku:

```csharp
// Build the content stream that uses the new graphics state
var content = new Operator[]
{
    new Operator("q"),                 // Save graphics state
    new Operator("GS0", "gs"),         // Set our custom ExtGState
    new Operator("0.5 0.5 1 rg"),      // Set fill color (light blue)
    new Operator("100 500 200 100 re"),// Rectangle (x, y, width, height)
    new Operator("f"),                 // Fill the rectangle using the fill opacity
    new Operator("Q")                  // Restore graphics state
};

// Add the operators to the page's content
firstPage.Contents.Add(content);
```

**Dlaczego ten krok jest opcjonalny:**  
Poprzednie kroki jedynie *definiują* stan graficzny. Aby zobaczyć efekt, musisz odwołać się do niego w strumieniu zawartości strony. Powyższy fragment pokazuje praktyczne zastosowanie, ale możesz także zastosować stan do istniejących poleceń rysowania w swoim PDF.

## Step 7 – Save the modified PDF

```csharp
// Persist the changes to a new file
pdfDocument.Save("Resources/output.pdf");
```

Gdy otworzysz `output.pdf`, zauważysz, że prostokąt jest renderowany z 50 % kryciem wypełnienia, podczas gdy jego obramowanie pozostaje w pełni nieprzezroczyste — dokładnie taki rezultat **jak ustawić przezroczystość PDF** przy użyciu niestandardowego ExtGState.

## Handling Multiple Pages

Jeśli potrzebujesz tego samego efektu przezroczystości na każdej stronie, przeiteruj `pdfDocument.Pages` i powtórz **Krok 2**‑**Krok 5** dla zasobów każdej strony. Uważaj, aby dodać stan graficzny tylko raz na stronę; ponowne użycie tego samego słownika na wielu stronach nie jest dozwolone przez specyfikację PDF.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    var editor = new DictionaryEditor(page.Resources);
    // Ensure ExtGState exists, then add GS0 as shown earlier
    // (code omitted for brevity)
}
```

## Common pitfalls and how to avoid them

| Objaw | Przyczyna | Rozwiązanie |
|-------|-----------|-------------|
| Brak zmiany krycia | `ca` lub `CA` poza zakresem 0‑1 | Użyj wartości dziesiętnych między `0.0` a `1.0`. |
| Zawartość znika | Stan graficzny nie został zastosowany (brak operatora `gs`) | Wstaw `GS0 gs` przed poleceniami rysowania. |
| PDF nie otwiera się | Zduplikowany klucz w słowniku `ExtGState` | Sprawdź `extGStateDict.ContainsKey("GS0")` przed dodaniem. |
| Tryb mieszania ignorowany | Przeglądarka nie obsługuje określonego trybu | Trzymaj się standardowych trybów, takich jak `Normal`, `Multiply`. |

## Full runnable example

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Load the PDF
        using var pdfDocument = new Document("Resources/input.pdf");

        // Work with the first page
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        CosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        else
        {
            extGStateDict = new CosPdfDictionary(pdfDocument);
            resourcesEditor.Add("ExtGState", extGStateDict);
        }

        // Create custom graphics state
        CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var entries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var e in entries) newGraphicsState.Add(e);

        // Register under a unique name
        extGStateDict.Add("GS0", newGraphicsState);

        // Optional: draw a transparent rectangle
        var ops = new Operator[]
        {
            new Operator("q"),
            new Operator("GS0", "gs"),
            new Operator("0.5 0.5 1 rg"),
            new Operator("100 500 200 100 re"),
            new Operator("f"),
            new Operator("Q")
        };
        firstPage.Contents.Add(ops);

        // Save result
        pdfDocument.Save("Resources/output.pdf");
    }
}
```

**Oczekiwany wynik:**  
Po otwarciu `output.pdf` widoczny jest jasno‑niebieski prostokąt w współrzędnych (100, 500) z 50 % kryciem wypełnienia. Obramowanie prostokąta pozostaje w pełni nieprzezroczyste, ponieważ `CA` jest ustawione na `1.0`.

## Conclusion

Teraz wiesz, jak **dodać niestandardowe obiekty ExtGState PDF** przy użyciu Aspose.PDF i precyzyjnie kontrolować krycie oraz tryby mieszania — odpowiadając na częste pytanie **jak ustawić przezroczystość PDF**. Poradnik obejmował ładowanie dokumentu, edycję słownika zasobów, definiowanie stanu graficznego, jego zastosowanie oraz zapisanie wyniku.

Następnie możesz zbadać:

- Używanie różnych trybów mieszania (`Multiply`, `Screen`) dla kreatywnych efektów.
- Zastosowanie tego samego ExtGState do obiektów XObject obrazów dla półprzezroczystych logo.
- Automatyzacja procesu masowych modyfikacji PDF w usłudze w tle.

Śmiało eksperymentuj z wartościami, zmieniaj nazwę stanu graficznego lub

## What Should You Learn Next?

Poniższe poradniki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Dodaj przezroczystość do PDF przy użyciu Aspose – Kompletny przewodnik C#](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [Jak dodać znak wodny strony do PDF przy użyciu Aspose.PDF dla Java (poradnik 2023)](/pdf/english/java/watermarks-backgrounds/add-page-stamp-aspose-pdf-java/)
- [Jak dodać znak wodny tekstowy do PDF przy użyciu Aspose.PDF dla Java: Kompletny przewodnik](/pdf/english/java/document-manipulation/aspose-pdf-java-add-text-stamp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}