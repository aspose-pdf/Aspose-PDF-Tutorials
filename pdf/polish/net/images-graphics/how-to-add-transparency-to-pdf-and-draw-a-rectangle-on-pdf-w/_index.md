---
category: general
date: 2026-09-12
description: Dowiedz się, jak dodać przezroczystość do pliku PDF, narysować prostokąt
  w PDF oraz zapisać PDF z przezroczystością przy użyciu Aspose.PDF w C# – przewodnik
  krok po kroku.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- draw rectangle on pdf
- save pdf with transparency
language: pl
lastmod: 2026-09-12
og_description: Dodaj przezroczystość do PDF, narysuj prostokąt w PDF i zapisz PDF
  z przezroczystością przy użyciu Aspose.PDF w C#. Skorzystaj z tego pełnego samouczka.
og_image_alt: Screenshot of a PDF page showing a semi‑transparent rectangle drawn
  with Aspose.PDF
og_title: Dodaj przezroczystość do PDF i narysuj prostokąt w PDF – kompletny przewodnik
  C#
schemas:
- author: Aspose
  dateModified: '2026-09-12'
  description: Learn how to add transparency to PDF, draw a rectangle on PDF, and
    save PDF with transparency using Aspose.PDF in C# – step‑by‑step guide.
  headline: How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Jak dodać przezroczystość do PDF i narysować prostokąt w PDF przy użyciu Aspose.PDF
url: /pl/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak dodać przezroczystość do PDF i narysować prostokąt w PDF przy użyciu Aspose.PDF

Jeśli potrzebujesz **dodać przezroczystość do PDF** plików, ten przewodnik pokaże Ci dokładnie, jak to zrobić w C#. Dowiesz się także, jak **narysować prostokąt w PDF** i w końcu **zapisać PDF z przezroczystością**, aby wynik mógł być ponownie użyty w raportach, fakturach lub dowolnym procesie automatyzacji dokumentów.

Podczas tego samouczka wykonasz:

* Załadujesz istniejący dokument PDF.
* Utworzysz niestandardowy stan graficzny definiujący krycie linii i wypełnienia.
* Zastosujesz ten stan graficzny na płótnie i narysujesz prostokąt.
* Zapiszesz zmodyfikowany plik, zachowując ustawienia przezroczystości.

Nie są wymagane żadne zewnętrzne narzędzia poza biblioteką Aspose.PDF for .NET, a każda linia kodu jest wyjaśniona, abyś rozumiał *dlaczego* każdy krok ma znaczenie.

## Wymagania wstępne

* .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.7+).
* Licencjonowana lub ewaluacyjna kopia **Aspose.PDF for .NET**. Zainstaluj ją przez NuGet:

```bash
dotnet add package Aspose.Pdf
```

* Plik PDF wejściowy (`input.pdf`) umieszczony w folderze, do którego możesz odwołać się w swoim projekcie.

## Krok 1: Załaduj dokument PDF

Pierwszą operacją jest otwarcie pliku źródłowego. Użycie instrukcji `using` zapewnia prawidłowe zwolnienie zasobów dokumentu, co zapobiega problemom z blokowaniem pliku przy późniejszym zapisie.

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";
using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

*Dlaczego to ważne*: Załadowanie dokumentu daje dostęp do kolekcji stron, słowników zasobów i obiektów płótna niezbędnych do rysowania.

## Krok 2: Uzyskaj dostęp do słownika zasobów pierwszej strony

Każda strona PDF posiada **słownik zasobów**, w którym przechowywane są obiekty takie jak czcionki, obrazy i stany graficzne. Aby wprowadzić nowe ustawienie przezroczystości, musimy edytować wpis `ExtGState`.

```csharp
// Step 2: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

*Dlaczego to ważne*: `DictionaryEditor` umożliwia odczyt i modyfikację niskopoziomowych obiektów PDF bez naruszania struktury dokumentu.

## Krok 3: Utwórz niestandardowy stan graficzny z wartościami przezroczystości

Stan graficzny (`ExtGState`) kontroluje sposób renderowania operacji rysowania. Definiujemy dwa parametry krycia:

* **CA** – krycie linii (obrys kształtów).
* **ca** – krycie wypełnienia (wnętrze kształtów).

Ustawiamy także tryb mieszania (`BM`) na „Normal”, który jest najczęściej używanym działaniem kompozycji.

```csharp
// Step 3: Create a custom graphics state (ExtGState) with transparency settings
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
var customGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "CA", new Aspose.Pdf.Cos.CosPdfNumber(1)),          // stroke opacity = 100 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),        // fill opacity = 50 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))      // normal blend mode
};

foreach (var p in parameters)
    customGs.Add(p);

// Register the new graphics state under the name "GS0"
extGStateDict.Add("GS0", customGs);
```

*Dlaczego to ważne*: Dodając `GS0` do słownika `ExtGState` tworzymy odwołanie, które płótno może aktywować przed rysowaniem. Krycie wypełnienia `0.5` sprawia, że prostokąt jest półprzezroczysty, co realizuje cel **dodania przezroczystości do PDF**.

## Krok 4: Zastosuj stan graficzny i narysuj prostokąt

Teraz instruujemy płótno strony, aby użyło właśnie utworzonego stanu graficznego, a następnie rysujemy prostokąt. Współrzędne są zgodne z systemem współrzędnych PDF (początek w lewym dolnym rogu).

```csharp
// Step 4: Apply the custom graphics state and draw a rectangle
var canvas = firstPage.Canvas;

// Activate the transparency graphics state
canvas.SetGraphicsState("GS0");

// Draw a rectangle from (100, 500) to (200, 600)
canvas.Rectangle(100, 500, 200, 600);

// Render the rectangle outline using the current graphics state
canvas.Stroke();
```

*Dlaczego to ważne*: `SetGraphicsState("GS0")` przełącza kontekst rysowania na wcześniej zdefiniowane ustawienia przezroczystości. Metoda `Rectangle` definiuje kształt, a `Stroke` rysuje obrys z określonym kryciem. Jeśli chcesz także wypełniony prostokąt, zamień `Stroke()` na `FillAndStroke()`.

## Krok 5: Zapisz zmodyfikowany PDF zachowując przezroczystość

Na koniec zapisujemy dokument z powrotem na dysk. Plik wyjściowy zawiera nowy stan graficzny, narysowany prostokąt oraz informacje o przezroczystości.

```csharp
// Step 5: Save the modified PDF
string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
pdfDocument.Save(outputPath);
```

*Dlaczego to ważne*: Zapisanie dokumentu finalizuje wszystkie zmiany. Powstały plik może być otwarty w dowolnym przeglądarce PDF, a prostokąt będzie wyświetlany z 50 % kryciem wypełnienia.

### Oczekiwany rezultat

Po otwarciu `output_with_extgstate.pdf` powinieneś zobaczyć prostokąt, którego obramowanie jest w pełni nieprzezroczyste, a wnętrze półprzezroczyste, co pozwala na prześwitywanie zawartości znajdującej się pod spodem.

## Przypadki brzegowe i praktyczne wskazówki

| Sytuacja | Zalecana korekta |
|-----------|------------------------|
| **Wiele stron** | Iteruj po `pdfDocument.Pages` i powtórz kroki 2‑4 dla każdej docelowej strony. |
| **Różne wartości krycia** | Zmień wartości `CosPdfNumber` dla `CA` (krycie linii) i `ca` (krycie wypełnienia) na dowolną liczbę pomiędzy `0` (całkowicie przezroczyste) a `1` (całkowicie nieprzezroczyste). |
| **Niestandardowe tryby mieszania** | Zastąp `"Normal"` przez `"Multiply"`, `"Screen"` lub dowolny standardowy tryb mieszania PDF obsługiwany przez twoją przeglądarkę. |
| **Wypełniony prostokąt** | Użyj `canvas.FillAndStroke()` zamiast `canvas.Stroke()`, aby zastosować zarówno wypełnienie, jak i obrys. |
| **Ponowne użycie tego samego stanu graficznego** | Możesz wywołać `canvas.SetGraphicsState("GS0")` przed rysowaniem dowolnej liczby kształtów na tej samej stronie. |

**Wskazówka:** Zawsze sprawdzaj słownik zasobów po dodaniu nowego `ExtGState`. Jeśli słownik nie istnieje, najpierw go utwórz:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
    resourcesEditor.Add("ExtGState", new Aspose.Pdf.Cos.CosPdfDictionary(pdfDocument));
```

## Pełny, gotowy do uruchomienia przykład

Poniżej znajduje się samodzielny program, który możesz skopiować do aplikacji konsolowej i uruchomić od razu (zamień `YOUR_DIRECTORY` na rzeczywistą ścieżkę).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF document
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Access the first page’s resources
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        if (!resourcesEditor.ContainsKey("ExtGState"))
            resourcesEditor.Add("ExtGState", new CosPdfDictionary(pdfDocument));

        // 3️⃣ Create a custom graphics state with transparency
        var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        var customGs = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };

        foreach (var p in parameters)
            customGs.Add(p);

        extGStateDict.Add("GS0", customGs);

        // 4️⃣ Apply the graphics state and draw a rectangle
        var canvas = firstPage.Canvas;
        canvas.SetGraphicsState("GS0");
        canvas.Rectangle(100, 500, 200, 600);
        canvas.Stroke(); // use FillAndStroke() for a filled shape

        // 5️⃣ Save the PDF with transparency
        string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine("PDF saved with a transparent rectangle at: " + outputPath);
    }
}
```

Uruchomienie programu generuje `output_with_extgstate.pdf`, który demonstruje **dodanie przezroczystości do PDF**, **rysowanie prostokąta w PDF** oraz **zapis PDF z przezroczystością** w jednym przebiegu.

## Zakończenie

Teraz wiesz, jak **dodać przezroczystość do plików PDF**, **narysować prostokąt w PDF** i **zapisać PDF z przezroczystością** przy użyciu Aspose.PDF for .NET. Proces opiera się na tworzeniu niestandardowego `ExtGState`, zastosowaniu go na płótnie i zachowaniu zmian. Dzięki tym elementom możesz rozszerzyć technikę na inne kształty, wiele stron lub dynamiczne wartości krycia.

**Kolejne kroki**

* Zbadaj inne prymitywy rysowania, takie jak `canvas.Ellipse`, `canvas.Path` lub `canvas.TextFragment`, ponownie używając tego samego stanu graficznego.
* Połącz przezroczystość z nakładkami obrazów, aby tworzyć znaki wodne (`canvas.Image` + niestandardowy `ExtGState`).
* Przejrzyj dokumentację Aspose.PDF dotyczącą **parametrów stanu graficznego** w celu uzyskania zaawansowanych efektów kompozycji.

Miłego kodowania i ciesz się wizualną elastycznością, jaką przezroczystość wprowadza do Twoich przepływów pracy z PDF!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak utworzyć PDF w C# – Dodaj stronę, narysuj prostokąt i zapisz](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [Jak dodać obiekt linii w PDF przy użyciu Aspose.PDF for .NET: Przewodnik krok po kroku](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Jak dodać znaczniki obrazu do PDF przy użyciu Aspose.PDF for .NET: Przewodnik krok po kroku](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}