---
category: general
date: 2026-10-17
description: Dodaj przezroczystość do PDF przy użyciu Aspose.PDF dla .NET, edytuj
  zasoby PDF i zapisz zmodyfikowane pliki PDF w jednym, uruchamialnym przykładzie.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- save modified pdf
- edit pdf resources
- Aspose.PDF transparency
- C# PDF manipulation
language: pl
lastmod: 2026-10-17
og_description: Dodaj przezroczystość do PDF przy użyciu Aspose.PDF dla .NET, edytuj
  zasoby PDF i zapisz zmodyfikowane pliki PDF z pełnym przykładem w C#.
og_image_alt: Screenshot showing a PDF with added transparency using Aspose.PDF in
  C#
og_title: Dodaj przezroczystość do PDF za pomocą Aspose.PDF – przewodnik
schemas:
- author: Aspose
  dateModified: '2026-10-17'
  description: Add transparency to PDF with Aspose.PDF for .NET, edit PDF resources,
    and save modified PDF files in a single, runnable example.
  headline: How to add transparency to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- pdf
- aspnet
- csharp
title: Jak dodać przezroczystość do PDF przy użyciu Aspose.PDF w C#
url: /pl/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak dodać przezroczystość do PDF przy użyciu Aspose.PDF w C#

Jeśli potrzebujesz **dodać przezroczystość do PDF** programowo, ten przewodnik pokazuje jasne, kompleksowe rozwiązanie z Aspose.PDF dla .NET. Nauczysz się **edytować zasoby PDF**, tworzyć niestandardowy stan graficzny oraz **zapisać zmodyfikowany PDF** bez opuszczania projektu C#.

Praca z przezroczystością PDF często wydaje się ukryta za niskopoziomowymi operatorami PDF. Po zakończeniu tego samouczka będziesz mieć w pełni działający przykład, który możesz skopiować‑wkleić, uruchomić i dostosować do wielu stron lub różnych trybów mieszania.

## Wymagania wstępne

- .NET 6.0 (lub dowolna nowsza wersja .NET)  
- Pakiet NuGet Aspose.PDF for .NET (`Aspose.Pdf`)  
- Podstawowa znajomość C#  
- Plik PDF wejściowy (`input.pdf`) umieszczony w folderze, do którego możesz odwołać się

> **Wskazówka:** Zainstaluj pakiet przy użyciu `dotnet add package Aspose.Pdf` przed rozpoczęciem.

## Krok 1: Załaduj dokument PDF

Pierwszą operacją jest otwarcie źródłowego PDF. Aspose.PDF reprezentuje PDF jako obiekt `Document`, który daje dostęp do stron, zasobów i niskopoziomowych słowników.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Collections;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;   // for graphics‑state objects

// Path to the original PDF
string pdfPath = @"YOUR_DIRECTORY\input.pdf";

// Open the document in a using block so it disposes automatically
using (var document = new Document(pdfPath))
{
    // The rest of the steps are inside this block
```

*Dlaczego to ważne:* Otwieranie dokumentu w ten sposób zapewnia zwolnienie uchwytu pliku po zakończeniu edycji, zapobiegając problemom z blokadą pliku, gdy później **zapiszesz zmodyfikowany PDF**.

## Krok 2: Uzyskaj dostęp do pierwszej strony i jej słownika zasobów

Strony PDF przechowują obiekty graficzne (czcionki, obrazy, wpisy ExtGState) w *słowniku zasobów*. Aby zmienić krycie, musimy pracować z pod‑słownikiem `ExtGState`.

```csharp
    // Get the first page (pages are 1‑based in Aspose.PDF)
    Page page = document.Pages[1];

    // Obtain a mutable editor for the page's resources
    var resourcesEditor = new DictionaryEditor(page.Resources);

    // Retrieve the ExtGState dictionary; create it if missing
    var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                         ?? new CosPdfDictionary(document);
```

*Dlaczego to ważne:* Jeśli oryginalny PDF już zawiera słownik `ExtGState`, rozszerzamy go; w przeciwnym razie tworzymy nowy, aby móc bezpiecznie **edytować zasoby PDF**.

## Krok 3: Zbuduj nowy stan graficzny z przezroczystością

Stan graficzny (`ExtGState`) zawiera parametry takie jak krycie linii (`CA`), krycie wypełnienia (`ca`) oraz tryb mieszania (`BM`). Tworzymy pusty słownik i wypełniamy go żądanymi wartościami.

```csharp
    // Create an empty ExtGState dictionary for the new entry
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

    // Define the transparency entries
    var entries = new[]
    {
        // CA – stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA",
            new CosPdfNumber(1)),

        // ca – fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca",
            new CosPdfNumber(0.5)),

        // BM – blend mode (Normal is the default)
        new KeyValuePair<string, ICosPdfPrimitive>("BM",
            new CosPdfName("Normal"))
    };

    // Add each entry to the new ExtGState dictionary
    foreach (var entry in entries)
        newGraphicsState.Add(entry);
```

*Dlaczego to ważne:* Wpis `ca` jest kluczem do **dodania przezroczystości do PDF** w treści używającej tego stanu graficznego. Możesz dostosować wartość liczbową (0 – 1), aby kontrolować stopień przejrzystości obiektu.

## Krok 4: Wstaw stan graficzny do zasobów strony

Musimy nadać nowemu stanowi graficznemu nazwę (np. `"GS0"`). Ta nazwa może później być odwoływana przez strumienie treści w celu zastosowania przezroczystości.

```csharp
    // Add the new ExtGState under the name "GS0"
    extGStateDict.Add("GS0", newGraphicsState);

    // Ensure the modified ExtGState dictionary is written back to the page
    resourcesEditor["ExtGState"] = extGStateDict;
```

*Dlaczego to ważne:* Dodając `"GS0"` do słownika `ExtGState`, każda operacja rysowania, która wybierze ten stan, zostanie wyrenderowana z określonym kryciem. To jest sedno **edycji zasobów PDF** pod kątem przezroczystości.

## Krok 5: Zastosuj stan graficzny do treści strony (opcjonalnie)

Jeśli chcesz, aby istniejąca treść strony automatycznie używała nowej przezroczystości, musisz dodać na początek operator stanu graficznego do strumienia treści strony. Poniższy fragment pokazuje, jak otoczyć istniejącą treść operatorami `gs` (ustaw stan graficzny) i `Q` (przywróć stan graficzny).

```csharp
    // Get the current content stream
    var content = page.Contents[1]; // assume a single content stream

    // Build a new stream that sets the graphics state, draws the original content, then restores
    string gsOperator = "/GS0 gs\n"; // select the graphics state we created
    string restoreOperator = "Q\n";   // restore graphics state after drawing

    // Prepend the gs operator and append the restore operator
    string newStream = gsOperator + content.Stream.ToString() + restoreOperator;

    // Replace the original stream with the modified one
    content.Stream = new CosPdfStream(document);
    content.Stream.SetData(newStream);
```

*Dlaczego to ważne:* Bez tego kroku stan graficzny istnieje, ale nie jest używany. Dodanie operatora `gs` informuje renderer PDF, aby zastosował przezroczystość do wszystkiego, co następuje dalej.

## Krok 6: **Zapisz zmodyfikowany PDF** na dysku

Na koniec zapisz zmodyfikowany dokument do nowego pliku. Metoda `Save` automatycznie obsługuje wszystkie niskopoziomowe aktualizacje.

```csharp
    // Path for the output PDF
    string outputPath = @"YOUR_DIRECTORY\output.pdf";

    // Persist the changes
    document.Save(outputPath);
}
```

*Dlaczego to ważne:* Wywołanie `document.Save` zapewnia, że zaktualizowany **zapisany zmodyfikowany pdf** zawiera nowy wpis `ExtGState` oraz strumień treści, który się do niego odwołuje. Powstały plik wyświetli półprzezroczyste wypełnienie na pierwszej stronie.

## Oczekiwany rezultat

Otwórz `output.pdf` w dowolnej przeglądarce PDF (Adobe Reader, Chrome itp.) i powinieneś zobaczyć grafikę pierwszej strony wyrenderowaną z 50 % kryciem wypełnienia. Jeśli przeanalizujesz PDF przy pomocy narzędzia takiego jak **PDF‑Tron** lub **iText**, znajdziesz wpis słownika `ExtGState` o nazwie `GS0` z wartością `ca` ustawioną na `0.5`.

## Przypadki brzegowe i warianty

| Sytuacja | Co zmienić |
|-----------|----------------|
| **Wiele stron** | Iteruj przez `document.Pages` i powtórz kroki 2‑5 dla każdej strony, używając unikalnej nazwy takiej jak `GS1`, `GS2`, … |
| **Istniejący konflikt nazw ExtGState** | Sprawdź `extGStateDict.ContainsKey("GS0")` przed dodaniem; jeśli istnieje, wygeneruj nowy klucz (`"GS" + Guid.NewGuid().ToString("N")`) |
| **Różne tryby mieszania** | Zastąp `"Normal"` przez `"Multiply"`, `"Screen"` itp., zmieniając wpis `BM` |
| **Potrzebne tylko krycie linii** | Pomiń wpis `ca` lub ustaw go na `1` i zamiast tego dostosuj `CA` |

## Pełny, gotowy do uruchomienia przykład

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Collections;
using Aspose.Pdf.Generator;

class AddTransparencyExample
{
    static void Main()
    {
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath


## Co powinieneś się nauczyć dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Dodaj przezroczystość do PDF przy użyciu Aspose.PDF – Kompletny przewodnik C#](/pdf/english/net/programming-with-stamps-and-watermarks/add-transparency-to-pdf-with-aspose-pdf-complete-c-guide/)
- [Jak dodać pieczątki stron w PDF przy użyciu Aspose.PDF dla .NET: Kompletny przewodnik](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Jak dodać obrazy do PDF przy użyciu Aspose.PDF dla .NET: Kompletny przewodnik](/pdf/english/net/images-graphics/add-images-to-pdfs-using-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}