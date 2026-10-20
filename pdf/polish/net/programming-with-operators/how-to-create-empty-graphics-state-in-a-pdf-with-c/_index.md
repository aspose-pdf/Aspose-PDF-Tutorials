---
category: general
date: 2026-08-17
description: Utwórz pusty stan graficzny w pliku PDF przy użyciu C# i Aspose.Pdf.
  Postępuj zgodnie z tym przewodnikiem krok po kroku, aby bezpiecznie edytować zasoby
  ExtGState.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty graphics state
- Aspose PDF graphics state
- C# modify PDF resources
- add ExtGState dictionary
- PDF page resources editing
language: pl
lastmod: 2026-08-17
og_description: Utwórz pusty stan graficzny w pliku PDF przy użyciu C#. Ten samouczek
  pokazuje, jak edytować zasoby ExtGState przy użyciu Aspose.Pdf, aby uzyskać niezawodne
  modyfikacje PDF.
og_image_alt: Screenshot of C# code that adds an empty graphics state to a PDF document
og_title: Utwórz pusty stan graficzny w PDF przy użyciu C# – przewodnik krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Create empty graphics state in a PDF using C# and Aspose.Pdf. Follow
    this step‑by‑step guide to edit ExtGState resources safely.
  headline: How to create empty graphics state in a PDF with C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Jak utworzyć pusty stan graficzny w PDF przy użyciu C#
url: /pl/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak utworzyć pusty stan graficzny w PDF przy użyciu C#

Jeśli potrzebujesz **utworzyć pusty stan graficzny** w PDF, ten przewodnik pokaże Ci dokładnie, jak to zrobić w C# i Aspose.Pdf. Zobaczysz kompletny, działający przykład, który dodaje nowy wpis do słownika ExtGState strony, nie wpływając na istniejącą zawartość.

Praca ze stanami graficznymi PDF jest powszechnym wymogiem, gdy chcesz kontrolować przezroczystość, tryby mieszania lub inne parametry renderowania na poziomie pojedynczego obiektu. Poniższy kod demonstruje zalecaną metodę, wyjaśnia, dlaczego każdy krok ma znaczenie, i opisuje typowe warianty, które możesz napotkać.

## Prerequisites

Zanim rozpoczniesz, upewnij się, że masz:

* .NET 6.0 lub nowszy (przykład kompiluje się także z .NET Core).
* Licencję Aspose.Pdf for .NET (lub tymczasowy klucz ewaluacyjny).
* Folder zawierający plik `input.pdf`, który chcesz zmodyfikować.
* Podstawową znajomość składni C# oraz koncepcji PDF, takich jak słowniki zasobów.

## Step 1: Set up the project and import namespaces

Utwórz nową aplikację konsolową lub włącz kod do istniejącego projektu. Dodaj pakiet NuGet Aspose.Pdf:

```bash
dotnet add package Aspose.Pdf
```

Następnie zaimportuj wymagane przestrzenie nazw:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
```

Te importy dają dostęp do klas `Document`, `DictionaryEditor` oraz prymitywów PDF potrzebnych do **utworzenia pustego stanu graficznego**.

## Step 2: Define the folder that holds the PDF files

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfSamples\";
```

Zastąp ścieżkę lokalizacją własnych plików PDF. Przechowywanie katalogu w zmiennej sprawia, że kod jest wielokrotnego użytku i łatwiejszy do testowania.

## Step 3: Load the source PDF document

```csharp
// Step 2: Load the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // All subsequent operations happen inside this using block
```

Otwieranie dokumentu wewnątrz instrukcji `using` zapewnia automatyczne zwolnienie uchwytu pliku po zapisaniu zmian.

## Step 4: Access the first page and its Resources dictionary

```csharp
    // Step 3: Get the first page and its Resources dictionary
    var firstPage = pdfDocument.Pages[1];
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
    var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

* `Pages[1]` pobiera pierwszą stronę (numery stron PDF zaczynają się od 1).
* `DictionaryEditor` zapewnia wygodny sposób odczytu i modyfikacji słowników PDF.
* Wpis `ExtGState` przechowuje wszystkie obiekty stanu graficznego dla strony. Jeśli klucz nie istnieje, Aspose.Pdf automatycznie tworzy pusty słownik.

## Step 5: Build a new empty graphics‑state dictionary

Stan graficzny, który dodajesz, może być pusty lub wstępnie wypełniony parametrami, takimi jak przezroczystość (`CA`, `ca`) czy tryb mieszania (`BM`). W tym tutorialu tworzymy **pusty stan graficzny**, a następnie ustawiamy kilka typowych wartości, aby zilustrować działanie słownika.

```csharp
    // Step 4: Create a new empty graphics‑state dictionary and set its parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // Stroke opacity
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };
    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

* `CosPdfDictionary.CreateEmptyDictionary` tworzy czysty kontener, który możesz wypełnić dowolnymi kluczami stanu graficznego.
* Dodanie `CA`, `ca` i `BM` jest opcjonalne; możesz je pominąć, jeśli naprawdę potrzebujesz pustego stanu. Kod pokazuje, jak dodać wpisy, gdy później zdecydujesz się kontrolować renderowanie.

## Step 6: Insert the new graphics state into the ExtGState dictionary

```csharp
    // Step 5: Add the new graphics state to the page's ExtGState dictionary (e.g., name it "GS0")
    extGStateDict.Add("GS0", newGraphicsState);
```

Nazwanie wpisu `"GS0"` podąża za powszechną konwencją prefiksowania nazw stanów graficznych „GS”. Możesz wybrać dowolną prawidłową nazwę PDF, która nie koliduje z istniejącymi kluczami.

## Step 7: Save the modified PDF document

```csharp
    // Step 6: Save the modified PDF document
    pdfDocument.Save(dataDir + "output.pdf");
}
```

Wywołanie `Save` zapisuje zaktualizowany plik jako `output.pdf`. Otworzenie tego pliku w przeglądarce PDF potwierdzi, że nowy stan graficzny istnieje; możesz odwołać się do niego później operatorem `gs` w strumieniach zawartości.

### Full source listing

Łącząc wszystkie elementy, pełny program wygląda następująco:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;

class Program
{
    static void Main()
    {
        // Define the folder that contains the PDF files
        string dataDir = @"C:\PdfSamples\";

        // Load the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Get the first page and its Resources dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create a new empty graphics‑state dictionary and set its parameters
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters)
                newGraphicsState.Add(p);

            // Add the new graphics state to the page's ExtGState dictionary (name it "GS0")
            extGStateDict.Add("GS0", newGraphicsState);

            // Save the modified PDF document
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("Empty graphics state created and saved to output.pdf");
    }
}
```

Uruchomienie programu wypisuje linię potwierdzającą i tworzy `output.pdf` z nowo dodanym stanem graficznym.

## Why this approach works best

* **Direct dictionary editing** – Użycie `DictionaryEditor` eliminuje konieczność parsowania całego strumienia zawartości. Modyfikujesz tylko te zasoby, które Cię interesują.
* **Typed PDF primitives** – `CosPdfNumber`, `CosPdfName` i `CosPdfDictionary` gwarantują, że wygenerowany PDF jest zgodny ze specyfikacją PDF 1.7.
* **Safety** – Blok `using` zwalnia obiekt `Document`, zapobiegając blokadom plików, które mogłyby uszkodzić kolejne kompilacje.
* **Extensibility** – Gdy pusty stan graficzny istnieje, możesz odwołać się do niego z dowolnego operatora zawartości (`gs`), aby zmienić przezroczystość, tryb mieszania lub inne parametry wybranych poleceń rysowania.

## Common variations and edge cases

| Situation | Recommended tweak |
|-----------|-------------------|
| **Multiple pages** | Pętla po `pdfDocument.Pages` i powtórzenie wstawiania słownika dla każdej strony, którą chcesz zmodyfikować. |
| **No existing ExtGState entry** | `resourcesEditor["ExtGState"]` automatycznie tworzy pusty słownik, jeśli nie istnieje. Nie wymaga dodatkowego kodu. |
| **Different graphics‑state name** | Zastąp `"GS0"` nazwą pasującą do Twojej konwencji, np. `"MyTransparentState"`. |
| **Adding only an empty state** | Pomiń tablicę `parameters` oraz pętlę `foreach`; słownik pozostanie pusty. |
| **Working with encrypted PDFs** | Podaj hasło przy tworzeniu `new Document(path, password)` przed edycją zasobów. |

## Verifying the result

Możesz zweryfikować, że stan graficzny został dodany, przeglądając PDF w narzędziu niskopoziomowym, takim jak **PDF‑Tron** lub **iText Sharp**. Poszukaj wpisu podobnego do:

```
/ExtGState << /GS0 << /CA 1 /ca 0.5 /BM /Normal >> >>
```

Jeśli wpis się pojawi, operacja **utworzenia pustego stanu graficznego** zakończyła się sukcesem.

## Conclusion

Teraz wiesz, jak **utworzyć pusty stan graficzny** w PDF przy użyciu C# i Aspose.Pdf. Tutorial omówił każdy krok – od załadowania dokumentu, przez edycję słownika `ExtGState`, po zapis wyniku – wyjaśniając przy tym uzasadnienie każdej czynności.  

Od tego momentu możesz:

* Używać nowego stanu graficznego w strumieniach zawartości (`gs /GS0`).
* Eksperymentować z dodatkowymi kluczami, takimi jak `/SM` (korekta pędzla) lub `/OPM` (tryb nadruku).
* Zastosować tę samą technikę do innych typów zasobów, np. `/XObject` lub `/ColorSpace`.

Miłego hakowania PDF‑ów i zachęcamy do eksploracji innych scenariuszy **Aspose PDF graphics state**, takich jak dynamiczne zmiany przezroczystości czy własne tryby mieszania!

## What Should You Learn Next?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz szczegółowe wyjaśnienia, pomagające opanować dodatkowe funkcje API i poznać alternatywne podejścia w własnych projektach.

- [Jak utworzyć linie przerywane w PDF przy użyciu Aspose.PDF dla .NET&#58; przewodnik krok po kroku](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Jak usunąć grafikę z PDF przy użyciu Aspose.PDF .NET&#58; kompletny przewodnik](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Tworzenie i wypełnianie prostokątów w PDF przy użyciu Aspose.PDF dla .NET&#58; przewodnik krok po kroku](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}