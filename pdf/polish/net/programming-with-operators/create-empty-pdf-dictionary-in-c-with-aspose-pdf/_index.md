---
category: general
date: 2026-08-14
description: Utwórz pusty słownik PDF w C# przy użyciu Aspose.Pdf – dowiedz się, jak
  dodać stan graficzny do kolekcji ExtGState i modyfikować pliki PDF programowo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.Pdf Document
- PDF graphics state
- ExtGState dictionary
- CosPdfDictionary usage
language: pl
lastmod: 2026-08-14
og_description: Utwórz pusty słownik PDF w C# przy użyciu Aspose.Pdf. Skorzystaj z
  tego kompletnego przewodnika, aby dodać niestandardowy stan graficzny do kolekcji
  ExtGState w pliku PDF.
og_image_alt: Screenshot showing C# code that creates an empty PDF dictionary with
  Aspose.Pdf
og_title: Utwórz pusty słownik PDF w C# – przewodnik krok po kroku Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  headline: Create empty PDF dictionary in C# with Aspose.Pdf
  type: TechArticle
- description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  name: Create empty PDF dictionary in C# with Aspose.Pdf
  steps:
  - name: Create a new **Console App** project in Visual Studio.
    text: Create a new **Console App** project in Visual Studio.
  - name: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
    text: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
  - name: 'Add the following `using` directives at the top of `Program.cs`:'
    text: 'Add the following `using` directives at the top of `Program.cs`:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Utwórz pusty słownik PDF w C# przy użyciu Aspose.Pdf
url: /pl/net/programming-with-operators/create-empty-pdf-dictionary-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie pustego słownika PDF w C# z Aspose.Pdf

Jeśli potrzebujesz **tworzyć puste słowniki PDF** podczas pracy z plikami PDF, ten przewodnik pokaże Ci dokładnie, jak to zrobić w C# przy użyciu biblioteki Aspose.Pdf. Niezależnie od tego, czy budujesz własny stan graficzny, dodajesz nowy zasób, czy przygotowujesz szablon do późniejszego użycia, poniższe kroki dostarczają kompletną, gotową do uruchomienia rozwiązanie.

Nauczysz się, jak wczytać PDF, uzyskać dostęp do słownika zasobów pierwszej strony, zbudować zupełnie nowy `CosPdfDictionary` i wstawić go do kolekcji `ExtGState`. Po zakończeniu tutorialu będziesz mieć działający plik `output.pdf`, który zawiera nowo utworzony słownik.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

- .NET 6.0 lub nowszy (kod działa także z .NET Framework 4.6+)
- Visual Studio 2022 lub dowolne inne IDE dla C#
- Licencję Aspose.Pdf for .NET (lub tymczasowy klucz ewaluacyjny)
- Przykładowy plik PDF o nazwie **input.pdf** umieszczony w folderze, do którego masz dostęp (ścieżka do folderu będzie użyta jako `dataDir`)

Nie są wymagane dodatkowe pakiety NuGet poza `Aspose.Pdf`.

## Krok 1: Konfiguracja projektu i odwołanie do Aspose.Pdf

1. Utwórz nowy projekt **Console App** w Visual Studio.  
2. Otwórz **NuGet Package Manager** i zainstaluj `Aspose.Pdf`:

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. Dodaj następujące dyrektywy `using` na początku pliku `Program.cs`:

   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Text;
   using Aspose.Pdf.Operators;
   using Aspose.Pdf.Facades;
   using Aspose.Pdf.InteractiveFeatures;
   using Aspose.Pdf.Xmp;
   using Aspose.Pdf.Operators.Filters;
   using Aspose.Pdf.Operators.Gfx;
   ```

   *Dlaczego te przestrzenie nazw?* `Aspose.Pdf` zawiera podstawową klasę `Document`, natomiast `Aspose.Pdf.Operators.Gfx` udostępnia `CosPdfDictionary`, `CosPdfNumber` i powiązane niskopoziomowe obiekty PDF potrzebne do **tworzenia pustych słowników PDF**.

## Krok 2: Wczytanie źródłowego PDF

Pierwszym działaniem jest wczytanie istniejącego pliku PDF do instancji `Document`. Dzięki temu uzyskasz dostęp do wszystkich stron, zasobów i niskopoziomowych słowników.

```csharp
// Step 2: Load the PDF document
string dataDir = @"C:\MyPdfFolder\";               // Change to your folder
using var pdfDocument = new Document(dataDir + "input.pdf");
```

*Wyjaśnienie*: `Document` odczytuje plik do pamięci i przygotowuje wewnętrzne struktury. Instrukcja `using` zapewnia zwolnienie uchwytu pliku po zakończeniu przetwarzania.

## Krok 3: Dostęp do słownika zasobów pierwszej strony

Każda strona PDF posiada słownik **Resources**, który grupuje czcionki, obrazy, obiekty ExtGState i inne współdzielone zasoby. Aby wstawić nowy stan graficzny, musimy edytować ten słownik.

```csharp
// Step 3: Get the first page and its Resources dictionary
Page firstPage = pdfDocument.Pages[1];                     // PDF pages are 1‑based
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` to klasa pomocnicza, która pozwala traktować słownik PDF jak `Dictionary<string, object>` w C#.

## Krok 4: Pobranie (lub utworzenie) kolekcji ExtGState

`ExtGState` przechowuje obiekty stanu graficznego, takie jak przezroczystość, tryb mieszania i grubość linii. Jeśli źródłowy PDF już zawiera wpis `ExtGState`, używamy go; w przeciwnym razie tworzymy nowy pusty słownik.

```csharp
// Step 4: Ensure an ExtGState dictionary exists
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a brand‑new ExtGState dictionary and add it to Resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*Dlaczego to sprawdzenie?* Niektóre pliki PDF nie posiadają wcale wpisu `ExtGState`. Obsługa obu przypadków sprawia, że tutorial jest odporny na różne pliki wejściowe.

## Krok 5: **Tworzenie pustego słownika PDF** dla nowego stanu graficznego

Teraz faktycznie **tworzymy puste słowniki PDF**, które definiują parametry stanu graficznego. Słownik zaczyna się pusty, a my dodajemy wymagane klucze:

```csharp
// Step 5: Build a new graphics state dictionary (empty PDF dictionary + entries)
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Stroke opacity (CA) – 1 means fully opaque strokes
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes semi‑transparent fills
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default compositing mode
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

### Co robi każdy wpis

| Klucz | Typ | Znaczenie |
|-------|-----|-----------|
| **CA** | `CosPdfNumber` | Przezroczystość obrysu (zakres 0‑1). |
| **ca** | `CosPdfNumber` | Przezroczystość wypełnienia (zakres 0‑1). |
| **BM** | `CosPdfName`   | Tryb mieszania; najczęściej używany to `"Normal"`. |

Ponieważ zaczęliśmy od **pustego słownika PDF**, mamy pełną kontrolę nad tym, które wpisy zostaną dodane. W razie potrzeby możesz rozszerzyć słownik o dodatkowe parametry stanu graficznego, takie jak `LW` (grubość linii) czy `LC` (kapitalizacja linii).

## Krok 6: Wstawienie nowego stanu graficznego do ExtGState

Słownik `ExtGState` działa jak mapa, w której każdy wpis jest identyfikowany nazwą (np. `GS0`, `GS1`). Dodajemy nasz świeżo zbudowany słownik pod unikalnym kluczem.

```csharp
// Step 6: Add the graphics state to the ExtGState collection
extGStateDict.Add("GS0", newGraphicsState);
```

Jeśli planujesz dodać wiele stanów, zwiększaj sufiks (`GS1`, `GS2`, …), aby uniknąć kolizji nazw.

## Krok 7: Zapis zmodyfikowanego PDF

Na koniec zapisujemy zmiany na dysku. Metoda `Save` automatycznie serializuje zaktualizowane słowniki.

```csharp
// Step 7: Persist the changes
pdfDocument.Save(dataDir + "output.pdf");
```

Otwórz `output.pdf` w dowolnym przeglądarce PDF i sprawdź wpis **Resources → ExtGState** (większość przeglądarek ukrywa to, ale narzędzia takie jak Adobe Acrobat Preflight czy PDF‑Tron mogą to pokazać). Powinien tam być wpis `GS0` zawierający wartości przezroczystości i trybu mieszania, które zdefiniowałeś.

## Kompletny działający przykład

Łącząc wszystkie elementy, oto pełny program, który możesz skopiować do `Program.cs` i uruchomić:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators.Gfx;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string dataDir = @"C:\MyPdfFolder\"; // <-- change to your folder
        using var pdfDocument = new Document(dataDir + "input.pdf");

        // -----------------------------------------------------------------
        // 2️⃣ Access the first page’s Resources dictionary
        // -----------------------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // -----------------------------------------------------------------
        // 3️⃣ Retrieve or create the ExtGState dictionary
        // -----------------------------------------------------------------
        CosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourcesEditor["ExtGState"] = extGStateDict;
        }

        // -----------------------------------------------------------------
        // 4️⃣ **Create empty PDF dictionary** for a new graphics state
        // -----------------------------------------------------------------
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode

        // -----------------------------------------------------------------
        // 5️⃣ Add the graphics state to ExtGState
        // -----------------------------------------------------------------
        extGStateDict.Add("GS0", newGraphicsState);

        // -----------------------------------------------------------------
        // 6️⃣ Save the modified PDF
        // -----------------------------------------------------------------
        pdfDocument.Save(dataDir + "output.pdf");

        Console.WriteLine("PDF saved with new empty dictionary at: " + dataDir + "output.pdf");
    }
}
```

**Oczekiwany wynik** – Konsola wyświetli linię potwierdzającą, a `output.pdf` będzie zawierał nowy wpis `GS0` w `ExtGState`. Gdy wyrenderujesz stronę odwołującą się do `GS0` (np. za pomocą operatora strumienia treści `gs`), obrysy będą w pełni nieprzezroczyste, a wypełnienia w 50 % przezroczyste.

## Częste pytania i obsługa przypadków brzegowych

| Pytanie | Odpowiedź |
|---------|-----------|
| *Co jeśli PDF ma wiele stron?* | Przykład dotyczy pierwszej strony (`Pages[1]`). Aby wpłynąć na wszystkie strony, przeiteruj `pdfDocument.Pages` i powtórz kroki 3‑5 dla zasobów każdej strony. |
| *Czy mogę dodać słownik do strony, która już ma wpis ExtGState o nazwie „GS0”?* | Tak, ale musisz użyć innego klucza (`GS1`, `GS2`, …), aby nie nadpisać istniejącego wpisu. |
| *Czy modyfikowanie słownika po zapisaniu jest bezpieczne?* | Po wywołaniu `Save` reprezentacja w pamięci jest odłączona od pliku. Możesz dalej edytować obiekt `Document` i ponownie wywołać `Save`, jeśli zajdzie taka potrzeba. |
| *Czy potrzebna jest licencja na Aspose.Pdf, aby używać ` |  

## Co warto poznać dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne przykłady kodu oraz szczegółowe wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [How to Remove Graphics from PDFs Using Aspose.PDF .NET&#58; A Complete Guide](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [How to Create Multi-Layer PDFs Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/advanced-features/create-multi-layer-pdfs-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}