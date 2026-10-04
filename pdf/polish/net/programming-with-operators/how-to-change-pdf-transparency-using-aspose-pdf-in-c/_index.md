---
category: general
date: 2026-10-04
description: Dowiedz się, jak zmienić przezroczystość PDF za pomocą Aspose.Pdf w C#.
  Ten przewodnik krok po kroku dodaje niestandardowy stan graficzny, aby dostosować
  krycie i tryb mieszania.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.Pdf graphics state
- PDF opacity C#
- ExtGState dictionary
- blend mode PDF
language: pl
lastmod: 2026-10-04
og_description: Zmieniaj przezroczystość PDF w C# przy użyciu Aspose.Pdf. Skorzystaj
  z tego zwięzłego samouczka, aby modyfikować krycie, tryb mieszania i stan graficzny
  w swoich plikach PDF.
og_image_alt: Screenshot of a PDF page before and after changing transparency with
  Aspose.Pdf
og_title: Zmieniaj przezroczystość PDF przy użyciu Aspose.Pdf – kompletny przewodnik
  C#
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to change PDF transparency with Aspose.Pdf in C#. This step‑by‑step
    guide adds a custom graphics state to adjust opacity and blend mode.
  headline: How to change PDF transparency using Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- graphics state
title: Jak zmienić przezroczystość PDF przy użyciu Aspose.Pdf w C#
url: /pl/net/programming-with-operators/how-to-change-pdf-transparency-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zmienić przezroczystość PDF przy użyciu Aspose.Pdf w C#

Jeśli potrzebujesz **zmienić przezroczystość PDF** w projekcie .NET, ten przewodnik pokaże Ci dokładnie, jak to zrobić przy użyciu Aspose.Pdf. Po zakończeniu tutorialu będziesz mieć PDF, w którym wybrane obiekty używają niestandardowej nieprzezroczystości i trybu mieszania, bez konieczności używania dodatkowych narzędzi.

Praca z nieprzezroczystością PDF jest częstym wymogiem przy znakach wodnych, nakładkach graficznych lub subtelnych efektach wizualnych. Poniższe kroki obejmują wszystko, czego potrzebujesz — od wczytania dokumentu po edycję **słownika ExtGState**, stworzenie nowego stanu graficznego i zapisanie wyniku.

## Prerequisites

Zanim rozpoczniesz, upewnij się, że masz:

* **Aspose.Pdf for .NET** (wersja 23.12 lub nowsza). Możesz zainstalować go przez NuGet:

```bash
dotnet add package Aspose.Pdf
```

* Środowisko programistyczne .NET (Visual Studio, VS Code lub `dotnet` CLI).
* Plik PDF wejściowy znajdujący się w znanym katalogu (przykład używa `input.pdf`).

Nie są wymagane dodatkowe biblioteki.

## Krok 1: Załaduj dokument PDF

Pierwsza operacja to otwarcie istniejącego PDF. Użycie bloku `using` zapewnia automatyczne zwolnienie uchwytu pliku.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Tools;

// ...

using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

*Dlaczego to ważne*: Ładowanie dokumentu tworzy reprezentację w pamięci, którą możesz modyfikować. Klasa `Document` daje również dostęp do niskopoziomowych obiektów COS, co jest niezbędne do zmiany przezroczystości PDF.

## Krok 2: Uzyskaj dostęp do zasobów pierwszej strony

Stany graficzne są przechowywane w słowniku zasobów strony. Pobieramy pierwszą stronę i opakowujemy jej zasoby w `DictionaryEditor`, aby móc je wygodnie edytować.

```csharp
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Wyjaśnienie*: `DictionaryEditor` abstrahuje obsługę słownika COS, umożliwiając odczyt i zapis wpisów takich jak `ExtGState` bez konieczności pracy z surową składnią PDF.

## Krok 3: Pobierz (lub utwórz) słownik ExtGState

**Słownik ExtGState** przechowuje nazwane obiekty stanu graficznego. Jeśli już istnieje, używamy go ponownie; w przeciwnym razie tworzymy nowy.

```csharp
CosPdfDictionary extGStateDict;

// Try to fetch an existing ExtGState entry
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a fresh ExtGState dictionary and add it to the resources
    extGStateDict = new CosPdfDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*Dlaczego ten krok*: Bez wpisu `ExtGState` silnik PDF nie ma gdzie odczytać niestandardowych ustawień nieprzezroczystości. Dodanie słownika sprawia, że strona jest świadoma nowych stanów graficznych, które definiujesz.

## Krok 4: Zdefiniuj nowy stan graficzny z nieprzezroczystością i trybem mieszania

Stan graficzny to zestaw parametrów renderowania PDF. Tutaj ustawiamy:

* **CA** – nieprzezroczystość konturu (1 = w pełni nieprzezroczysty)
* **ca** – nieprzezroczystość wypełnienia (0.5 = 50 % przezroczyste)
* **BM** – tryb mieszania (`Normal` jest domyślny, ale możesz eksperymentować z `Multiply`, `Screen` itp.)

```csharp
// Create an empty dictionary that will become the new graphics state
var graphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Prepare the entries
var graphicsStateEntries = new KeyValuePair<string, ICosPdfPrimitive>[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // blend mode
};

// Populate the dictionary
foreach (var entry in graphicsStateEntries)
{
    graphicsState.Add(entry);
}
```

*Wgląd*: Wartości `CosPdfNumber` są liczbami zmiennoprzecinkowymi od 0 do 1. Zmiana ich pozwala precyzyjnie dostroić, jak wyglądają przezroczyste kontury i wypełnienia. Tryb mieszania określa, jak przezroczysta zawartość współdziała z grafiką pod spodem.

## Krok 5: Zarejestruj stan graficzny w ExtGState

Nadajemy nowemu stanowi nazwę (`GS0`). Później, przy rysowaniu obiektów, odwołujesz się do tej nazwy w strumieniu zawartości.

```csharp
extGStateDict.Add("GS0", graphicsState); // "GS0" becomes the identifier you’ll use later
```

*Najlepsza praktyka*: Używaj przejrzystej konwencji nazewnictwa (`GS0`, `GS_Watermark` itp.), aby móc zarządzać wieloma stanami bez zamieszania.

## Krok 6: Zastosuj stan graficzny do zawartości strony (opcjonalnie)

Jeśli chcesz zastosować nową nieprzezroczystość do istniejących elementów strony, musisz zmodyfikować strumień zawartości strony. Poniżej prosty przykład, który dodaje półprzezroczysty prostokąt na górze strony.

```csharp
// Build a content stream that sets the graphics state and draws a rectangle
var contentBuilder = new Aspose.Pdf.Operators.ContentBuilder(pdfDocument);
contentBuilder.SetGraphicsState("GS0");
contentBuilder.SetFillColor(Color.FromRgb(255, 0, 0)); // red fill
contentBuilder.Rectangle(100, 500, 200, 100); // x, y, width, height
contentBuilder.FillPath();

firstPage.Contents.Add(contentBuilder);
```

*Dlaczego to działa*: Operator `SetGraphicsState` informuje interpreter PDF, aby używał parametrów zdefiniowanych w `GS0` dla wszystkich kolejnych poleceń rysowania. Prostokąt pojawia się więc z 50 % nieprzezroczystością wypełnienia, zachowując pełną nieprzezroczystość konturu.

## Krok 7: Zapisz zmodyfikowany PDF

Na koniec zapisz zmiany na dysk.

```csharp
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

Wynikowy `output.pdf` zawiera nowy stan graficzny, a każda zawartość odwołująca się do `GS0` zostanie wyrenderowana z określoną przezroczystością.

![Diagram showing PDF transparency change](/images/pdf-transparency-before-after.png "PDF page before and after applying custom graphics state")
*Image alt text (for SEO and accessibility):* **przykład zmiany przezroczystości PDF – oryginalna vs. zmodyfikowana strona**

## Pełny działający przykład

Łącząc wszystko razem, oto pojedynczy, uruchamialny program, który zmienia przezroczystość PDF i dodaje półprzezroczysty prostokąt.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Tools;
using System.Collections.Generic;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Drawing;

class ChangePdfTransparency
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            CosPdfDictionary extGStateDict;
            if (resourcesEditor.ContainsKey("ExtGState"))
                extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
            else
            {
                extGStateDict = new CosPdfDictionary(pdfDocument);
                resourcesEditor["ExtGState"] = extGStateDict;
            }

            // Create a new graphics state (opacity + blend mode)
            var graphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var e in entries) graphicsState.Add(e);

            // Register the graphics state as GS0
            extGStateDict.Add("GS0", graphicsState);

            // OPTIONAL: draw a semi‑transparent rectangle using GS0
            var builder = new ContentBuilder(pdfDocument);
            builder.SetGraphicsState("GS0");
            builder.SetFillColor(Color.FromRgb(255, 0, 0)); // red
            builder.Rectangle(100, 500, 200, 100);
            builder.FillPath();
            firstPage.Contents.Add(builder);

            // Save the result
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF transparency changed and saved to output.pdf");
    }
}
```

### Oczekiwany wynik

* Plik `output.pdf` zostaje utworzony w określonym folderze.
* Po otwarciu PDF zobaczysz czerwony prostokąt, którego wypełnienie jest w 50 % przezroczyste, a obramowanie pozostaje w pełni nieprzezroczyste.
* Wszystkie inne obiekty odwołujące się do `GS0` (np. znaki wodne) odziedziczą tę samą nieprzezroczystość i tryb mieszania.

## Częste pytania i obsługa przypadków brzegowych

| Question | Answer |
|----------|--------|
| **Czy mogę zmienić tylko nieprzezroczystość konturu?** | Ustaw `CA` na pożądaną wartość i pozostaw `ca` na `1`. |
| **Jakie tryby mieszania są obsługiwane?** | Wszystkie standardowe tryby mieszania PDF (`Normal`, `Multiply`, `Screen`, `Overlay` itp.) są akceptowane poprzez wpis `BM`. |
| **Czy muszę czyścić słownik po użyciu?** | Nie. Obiekty `CosPdfDictionary` są zarządzane przez Aspose.Pdf i zapisywane do pliku po wywołaniu `Save`. |
| **Jak to działa z zaszyfrowanymi PDF‑ami?** | Załaduj dokument z odpowiednim hasłem (`new Document(path, password)`). Manipulacja stanem graficznym działa tak samo po odszyfrowaniu dokumentu w pamięci. |
| **Czy można zastosować ten sam stan graficzny do wielu stron?** | Tak. Dodaj wpis `GS0` do słownika `ExtGState` każdej strony lub utwórz jeden współdzielony słownik w zasobach globalnych dokumentu i odwołuj się do niego z każdej strony. |

## Wskazówki i najlepsze praktyki

* **Pro tip:** Trzymaj nazwy stanów graficznych krótkie, ale opisowe (`GS_Watermark`, `GS_Overlay`). To zapobiega kolizjom nazw i ułatwia debugowanie.
* **Watch out for:** Przypadkowe nadpisanie istniejącego wpisu `ExtGState`. Zawsze sprawdzaj `resourcesEditor.ContainsKey("ExtGState")` przed utworzeniem nowego słownika.
* **Performance note:** Modyfikowanie niskopoziomowych obiektów COS jest szybkie, ale jeśli musisz przetworzyć tysiące stron, rozważ grupowanie zmian, aby zmniejszyć obciążenie pamięci.

## Kolejne kroki

Teraz, gdy wiesz, jak **zmienić przezroczystość PDF**, możesz zgłębiać pokrewne tematy, takie jak:

* Dodawanie **znaków wodnych** z niestandardową nieprzezroczystością (`PDF opacity C#`).
* Używanie **różnych trybów mieszania** w celu uzyskania artystycznych efektów (`blend mode PDF`).
* Tworzenie wielokrotnego użytku **bibliotek stanów graficznych** dla masowej generacji dokumentów (`Aspose.Pdf graphics state`).

Eksperymentuj ze zmianą wartości `ca` i `CA`, lub zamień czerwony prostokąt na obraz lub nakładkę tekstową. Te same zasady mają zastosowanie — po prostu odwołaj się do stanu graficznego `GS0` przed rysowaniem nowej zawartości.

*Nauczyłeś się, jak zmienić przezroczystość PDF przy użyciu Aspose.Pdf w C#. Zastosuj te techniki, aby ulepszyć raporty, faktury lub każdy wynik oparty na PDF, gdzie liczy się subtelna kontrola wizualna.*

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu wraz z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Zmiana nieprzezroczystości PDF przy użyciu Aspose.PDF – Kompletny przewodnik C#](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Zmiana nieprzezroczystości PDF w C# – Kompletny przewodnik Aspose](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-in-c-complete-aspose-guide/)
- [Dodawanie przezroczystości do PDF przy użyciu Aspose – Kompletny przewodnik C#](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}