---
category: general
date: 2026-10-13
description: Dowiedz się, jak ustawić przezroczystość w pliku PDF przy użyciu Aspose.Pdf
  dla C#. Zobacz także, jak zapisać zmodyfikowany PDF i zmienić alfa wypełnienia.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set transparency
- save modified pdf
- change fill alpha
- set fill opacity
- edit pdf resources
language: pl
lastmod: 2026-10-13
og_description: Jak ustawić przezroczystość w pliku PDF przy użyciu Aspose.Pdf dla
  C#. Postępuj zgodnie z tym przewodnikiem, aby edytować zasoby PDF, zmienić alfa
  wypełnienia i zapisać zmodyfikowane pliki PDF.
og_image_alt: Screenshot of a PDF page showing transparent graphics applied with Aspose.Pdf
  in C#
og_title: Jak ustawić przezroczystość w pliku PDF przy użyciu Aspose.Pdf C# – przewodnik
  krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  headline: How to set transparency in a PDF with Aspose.Pdf C#
  type: TechArticle
- description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  name: How to set transparency in a PDF with Aspose.Pdf C#
  steps:
  - name: Load the PDF document
    text: '```csharp using Aspose.Pdf; using System.Collections.Generic;'
  - name: Edit PDF resources to add a graphics state
    text: '```csharp // Get the first page (pages are 1‑based) Page firstPage = pdfDocument.Pages[1];'
  - name: Change fill alpha and set fill opacity
    text: '```csharp // Create an empty graphics state dictionary CosPdfDictionary
      newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);'
  - name: Add the new graphics state to the ExtGState dictionary
    text: '```csharp // Register the new state under the name "GS0" extGStateDict.Add("GS0",
      newGraphicsState); ```'
  - name: (Optional) Apply the graphics state in a content stream
    text: 'If you want to draw a rectangle using the new fill opacity, add the following
      after the previous steps:'
  - name: Save modified PDF
    text: '```csharp // Persist the changes to a new file pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
      ```'
  - name: Next steps
    text: '* Explore other blend modes (`Multiply`, `Screen`, etc.) by changing the
      `BM` entry. * Adjust stroke alpha (`CA`) to create semi‑transparent outlines.
      * Combine multiple graphics states to build a library of reusable visual effects.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- Transparency
title: Jak ustawić przezroczystość w PDF przy użyciu Aspose.Pdf C#
url: /pl/net/images-graphics/how-to-set-transparency-in-a-pdf-with-aspose-pdf-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak ustawić przezroczystość w pliku PDF przy użyciu Aspose.Pdf C#

Jeśli potrzebujesz ustawić przezroczystość w pliku PDF przy użyciu C#, ten samouczek pokazuje dokładne kroki. Dowiesz się także, jak zapisać zmodyfikowane pliki PDF i zmienić alfa wypełnienia bez opuszczania środowiska Aspose.Pdf.

Poradnik prowadzi przez ładowanie dokumentu, edycję zasobów PDF, tworzenie stanu graficznego definiującego przezroczystość wypełnienia oraz zachowanie zmian. Nie są wymagane żadne zewnętrzne narzędzia; wszystko działa w standardowym projekcie .NET.

## Wymagania wstępne

* .NET 6.0 lub nowszy zainstalowany  
* Ważna licencja Aspose.Pdf for .NET (lub darmowy klucz ewaluacyjny)  
* Plik PDF wejściowy znajdujący się w znanym katalogu  

Możesz dodać pakiet Aspose.Pdf za pomocą NuGet:

```bash
dotnet add package Aspose.Pdf
```

## Jak ustawić przezroczystość w pliku PDF

Ta sekcja zawiera podstawową implementację. Każdy krok wyjaśnia **dlaczego** kod jest potrzebny, a nie tylko **co** robi.

### Krok 1: Załaduj dokument PDF

```csharp
using Aspose.Pdf;
using System.Collections.Generic;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*Dlaczego ten krok?*  
`Document` reprezentuje cały plik PDF w pamięci. Otwieranie pliku daje dostęp do stron, zasobów i obiektów niskiego poziomu, które będziesz modyfikować.

### Krok 2: Edytuj zasoby PDF, aby dodać stan graficzny

```csharp
// Get the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];

// Create an editor for the page's resource dictionary
DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);

// Retrieve the ExtGState dictionary; it holds graphics state objects
CosPdfDictionary extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
```

*Dlaczego ten krok?*  
Strony PDF przechowują wielokrotnie używane obiekty — czcionki, obrazy i stany graficzne — w słowniku zasobów. Wpis `ExtGState` zawiera ustawienia przezroczystości. Edytując ten słownik, możesz wprowadzić nowy stan, do którego strona może odwoływać się.

### Krok 3: Zmień alfa wypełnienia i ustaw przezroczystość wypełnienia

```csharp
// Create an empty graphics state dictionary
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the graphics state entries
var graphicsStateEntries = new[]
{
    // Stroke alpha (CA) – fully opaque
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    // Fill alpha (ca) – 50 % transparent
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // Blend mode (BM) – normal composition
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

// Populate the new graphics state
foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*Dlaczego ten krok?*  
`ca` kontroluje **przezroczystość wypełnienia**, natomiast `CA` kontroluje **przezroczystość konturu**. Ustawienie `ca` na `0.5` sprawia, że wypełnione kształty są w 50 % przezroczyste. Wpis `BM` wybiera tryb mieszania; `"Normal"` jest najczęściej wybieranym trybem dla standardowej przezroczystości.

### Krok 4: Dodaj nowy stan graficzny do słownika ExtGState

```csharp
// Register the new state under the name "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

*Dlaczego ten krok?*  
Nazwanie stanu graficznego (`"GS0"`) pozwala strumieniom zawartości na stronie odwoływać się do niego za pomocą operatora `gs`. Po tej rejestracji strona może zastosować właśnie zdefiniowaną przezroczystość.

### Krok 5: (Opcjonalnie) Zastosuj stan graficzny w strumieniu zawartości

Jeśli chcesz narysować prostokąt używając nowej przezroczystości wypełnienia, dodaj poniższy kod po poprzednich krokach:

```csharp
// Create a content stream that uses the new graphics state
string cs = @"
q               % Save graphics state
/GS0 gs         % Apply the graphics state defined earlier
0 0 200 100 re  % Define a rectangle (x, y, width, height)
0.2 0.6 0.8 rg  % Set fill color (RGB)
f               % Fill the rectangle using the current graphics state
Q               % Restore graphics state
";

firstPage.Contents.Add(new Aspose.Pdf.Operator.GsContent(cs));
```

*Dlaczego ten krok?*  
Operatory `q`/`Q` zapisują i przywracają stan graficzny, zapewniając, że przezroczystość wpływa tylko na zamierzone polecenia rysowania. Operator `gs` przełącza na stan graficzny o nazwie `"GS0"`.

### Krok 6: Zapisz zmodyfikowany PDF

```csharp
// Persist the changes to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*Dlaczego ten krok?*  
Zapis zapisuje zaktualizowany słownik zasobów oraz wszelkie nowe strumienie zawartości na dysk. Powstały plik (`output.pdf`) zawiera przezroczysty prostokąt zdefiniowany w poprzednim kroku.

## Pełny przykład gotowy do uruchomienia

Łącząc wszystkie elementy, oto kompletny program, który możesz skompilować i uruchomić:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using System.Collections.Generic;

class SetTransparencyDemo
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Access the first page and its resources
        Page firstPage = pdfDocument.Pages[1];
        var resourceEditor = new DictionaryEditor(firstPage.Resources);
        var extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();

        // Create a new graphics state with 50 % fill opacity
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var graphicsStateEntries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke alpha
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill alpha
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var entry in graphicsStateEntries)
            newGraphicsState.Add(entry);

        // Register the graphics state as "GS0"
        extGStateDict.Add("GS0", newGraphicsState);

        // Optional: draw a rectangle using the new transparency
        string cs = @"
q
/GS0 gs
0 0 200 100 re
0.2 0.6 0.8 rg
f
Q
";
        firstPage.Contents.Add(new GsContent(cs));

        // Save the modified PDF
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

**Oczekiwany wynik** – `output.pdf` pokazuje prostokąt wypełniony jasnym fioletowym kolorem, który jest w 50 % przezroczysty, umożliwiając częściowe widzenie dowolnej zawartości w tle.

## Częste pytania i przypadki brzegowe

* **Czy mogę zmienić przezroczystość konturu zamiast przezroczystości wypełnienia?**  
  Ustaw wartość `CA` (wielkie litery) na liczbę pomiędzy `0` (całkowicie przezroczyste) a `1` (całkowicie nieprzezroczyste). Przykład już ustawia `CA` na `1`, co oznacza, że kontury pozostają nieprzezroczyste.

* **Co jeśli strona nie ma jeszcze słownika ExtGState?**  
  `resourceEditor["ExtGState"]` automatycznie utworzy pusty słownik. Dodanie `"GS0"` działa w ten sam sposób.

* **Czy stan graficzny można ponownie używać na wielu stronach?**  
  Tak. Po dodaniu wpisu do słownika zasobów dokumentu, każda strona odwołująca się do `"GS0"` odziedziczy te same ustawienia przezroczystości.

* **Jak to podejście różni się od użycia wysokopoziomowego API `Graphics`?**  
  Edycja niskopoziomowego słownika zasobów daje precyzyjną kontrolę nad wewnętrzną strukturą PDF i generuje mniejsze pliki, ponieważ unika osadzania dodatkowych obiektów.

## Podsumowanie

Teraz wiesz **jak ustawić przezroczystość w pliku PDF** przy użyciu Aspose.Pdf dla C#. Samouczek obejmował edycję zasobów PDF, zmianę alfa wypełnienia, ustawienie przezroczystości wypełnienia oraz zapis zmodyfikowanego PDF. Dzięki tej podstawie możesz eksperymentować z różnymi trybami mieszania, stosować przezroczystość do tekstu lub tworzyć wielokrotnego użytku stany graficzne dla złożonych dokumentów.

### Kolejne kroki

* Zbadaj inne tryby mieszania (`Multiply`, `Screen` itp.) zmieniając wpis `BM`.  
* Dostosuj alfa konturu (`CA`), aby tworzyć półprzezroczyste obramowania.  
* Połącz wiele stanów graficznych, aby zbudować bibliotekę wielokrotnego użytku efektów wizualnych.

Śmiało podziel się swoimi wynikami lub zadaj pytania w komentarzach. Szczęśliwego kodowania!

## Co powinieneś się nauczyć dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak dostosować pliki PDF przy użyciu Aspose.PDF dla .NET&#58; Ustaw marginesy stron i rysuj linie](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [Jak ustawić rozmiar obrazu w pliku PDF przy użyciu Aspose-PDF dla .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [Jak ustawić uprawnienia PDF przy użyciu Aspose.PDF dla .NET&#58; Kompletny przewodnik](/pdf/english/net/security-permissions/set-pdf-privileges-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}