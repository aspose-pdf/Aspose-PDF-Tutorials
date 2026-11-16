---
category: general
date: 2026-11-16
description: Dowiedz się, jak utworzyć stan graficzny PDF w C# przy użyciu Aspose.Pdf.
  Ten przewodnik obejmuje przezroczystość, tryb mieszania oraz pełny przykład kodu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf graphics state
- Aspose.Pdf ExtGState
- PDF opacity
- C# PDF manipulation
- PDF blend mode
- Aspose.Pdf graphics state
language: pl
lastmod: 2026-11-16
og_description: Utwórz stan graficzny PDF w C# przy użyciu Aspose.Pdf. Skorzystaj
  z tego pełnego samouczka, aby programowo ustawić przezroczystość i tryb mieszania.
og_image_alt: Illustration of how to create PDF graphics state with Aspose.Pdf in
  C#
og_title: Tworzenie stanu graficznego PDF w C# – krok po kroku przewodnik Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to create PDF graphics state in C# using Aspose.Pdf. This
    guide covers opacity, blend mode, and full code example.
  headline: How to create PDF graphics state in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF
title: Jak utworzyć stan graficzny PDF w C# przy użyciu Aspose.Pdf
url: /pl/net/images-graphics/how-to-create-pdf-graphics-state-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak utworzyć stan graficzny PDF w C# z Aspose.Pdf

Jeśli potrzebujesz **utworzyć stan graficzny PDF** w projekcie .NET, ten tutorial pokazuje dokładnie, jak to zrobić przy użyciu Aspose.Pdf. Niezależnie od tego, czy chcesz kontrolować przezroczystość, zmienić tryb mieszania, czy ponownie wykorzystać niestandardowy stan graficzny na wielu stronach, poniższe kroki dostarczają kompletną, gotową do uruchomienia rozwiązanie.

W tym przewodniku nauczysz się, jak uzyskać dostęp do zasobów strony, dodać wpis **ExtGState** i zachować zmiany w nowym pliku. Przykład działa z Aspose.Pdf 23.12 (lub nowszym) i jest przeznaczony dla .NET 6+, ale koncepcje mają zastosowanie również do wcześniejszych wersji.

## Wymagania wstępne

* Visual Studio 2022 (lub dowolne IDE C#) z zainstalowanym .NET 6 SDK.  
* Licencja Aspose.Pdf for .NET lub tymczasowy klucz ewaluacyjny.  
* Plik PDF o nazwie `input.pdf` umieszczony w folderze, do którego możesz odwołać się z kodu.  

Nie są wymagane dodatkowe pakiety NuGet poza `Aspose.Pdf`.

## Co obejmuje tutorial

* Ładowanie istniejącego dokumentu PDF.  
* Nawigacja do słownika zasobów pierwszej strony.  
* Tworzenie nowego słownika stanu graficznego, definiującego przezroczystość obrysu (`CA`), przezroczystość wypełnienia (`ca`) oraz tryb mieszania (`BM`).  
* Dodanie nowego stanu graficznego do kolekcji **ExtGState** pod niestandardową nazwą (`GS0`).  
* Zapis zaktualizowanego PDF, aby kolejne polecenia rysowania mogły odwoływać się do nowego stanu.

Po zakończeniu tutorialu będziesz w stanie programowo **tworzyć obiekty stanu graficznego PDF** i ponownie wykorzystywać je w dowolnej operacji rysowania.

## Krok 1: Konfiguracja projektu i importowanie przestrzeni nazw

Utwórz nową aplikację konsolową (lub zintegrować kod w istniejącym projekcie). Dodaj odwołanie do Aspose.Pdf i dołącz wymagane przestrzenie nazw:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Generator;
```

> **Pro tip:** Jeśli używasz darmowej wersji ewaluacyjnej, dodaj `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` przed załadowaniem dokumentu, aby uniknąć komunikatów o znakach wodnych.

## Krok 2: Załaduj dokument PDF

Otwieranie pliku jest proste. Klasa `Document` reprezentuje cały PDF i zapewnia dostęp do jego stron oraz zasobów.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";

using (var document = new Document(inputPath))
{
    // All subsequent steps run inside this using block
```

Umieszczenie kodu wewnątrz bloku `using` zapewnia zwolnienie uchwytu pliku po zakończeniu operacji, co jest niezbędne przy **manipulacji PDF w C#** w usługach produkcyjnych.

## Krok 3: Pobierz słownik zasobów pierwszej strony

Każda strona PDF posiada słownik *Resources*, który przechowuje czcionki, obrazy i stany graficzne. Potrzebujemy `DictionaryEditor`, aby edytować tę strukturę.

```csharp
    // Step 3: Get the first page and its resources dictionary
    var page = document.Pages[1];
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

Jeśli PDF już zawiera wpis `ExtGState`, `resourcesEditor["ExtGState"]` zwróci go; w przeciwnym razie Aspose.Pdf utworzy pusty słownik, gdy dodamy pierwszy wpis.

## Krok 4: Uzyskaj dostęp lub utwórz słownik ExtGState

Słownik **ExtGState** przechowuje nazwane obiekty stanu graficznego. Pobieramy istniejący lub tworzymy nowy kontener.

```csharp
    // Step 4: Access (or create) the ExtGState dictionary within the resources
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

Gdy `ExtGState` nie istnieje, `resourcesEditor["ExtGState"]` automatycznie zwraca nowy pusty słownik, co zapewnia działanie kodu dla dowolnego PDF.

## Krok 5: Zbuduj nowy słownik stanu graficznego

Stan graficzny to `CosPdfDictionary` z określonymi kluczami:

* `CA` – przezroczystość obrysu (0‑1)  
* `ca` – przezroczystość wypełnienia (0‑1)  
* `BM` – tryb mieszania (`Normal`, `Multiply`, itp.)

Tworzymy pusty słownik, wypełniamy go, a następnie dodajemy do `ExtGState`.

```csharp
    // Step 5: Create a new graphics state dictionary with desired parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (50% transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };

    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

Możesz zmienić `0.5` na dowolną wartość pomiędzy `0` a `1`, aby dostosować przezroczystość wypełnienia, lub zamienić `"Normal"` na `"Multiply"` dla innego **trybu mieszania PDF**. Ta elastyczność jest powodem, dla którego tworzenie niestandardowego stanu graficznego jest potężną techniką w obsłudze **stanu graficznego Aspose.Pdf**.

## Krok 6: Zarejestruj stan graficzny pod nazwą

Strumienie zawartości PDF odwołują się do stanów graficznych po nazwie. Tutaj używamy `GS0`, ale dowolna unikalna nazwa zadziała.

```csharp
    // Step 6: Add the new graphics state to the ExtGState dictionary with a name (e.g., GS0)
    extGState.Add("GS0", newGraphicsState);
```

Jeśli potrzebujesz wielu stanów, powtórz krok tworzenia z różnymi parametrami i dodaj je jako `GS1`, `GS2` itd. Ten wzorzec dobrze skalowuje się w przypadku złożonych dokumentów, które wymagają różnych ustawień przezroczystości lub trybu mieszania na różnych warstwach.

## Krok 7: Zapisz zmodyfikowany PDF

Na koniec zapisz zaktualizowany dokument do nowego pliku. Zachowanie oryginału niezmienionego ułatwia debugowanie.

```csharp
    // Step 7: Save the updated PDF document
    string outputPath = @"YOUR_DIRECTORY\output.pdf";
    document.Save(outputPath);
}
```

Po wykonaniu, `output.pdf` zawiera wpis `ExtGState` o nazwie `GS0`. Każdy kolejny operator rysowania może odwołać się do niego za pomocą operatora `gs` (np. `GS0 gs` w strumieniu zawartości).

> **Dlaczego to ważne:** Tworząc wielokrotnie używany stan graficzny, unikasz powtarzania ustawień przezroczystości i trybu mieszania dla każdego polecenia rysowania, co poprawia zarówno wydajność, jak i utrzymanie kodu.

## Użycie nowego stanu graficznego w strumieniu zawartości (opcjonalnie)

Jeśli chcesz od razu zobaczyć efekt, możesz dodać prostokąt, który używa właśnie utworzonego stanu:

```csharp
using (var document = new Document(outputPath))
{
    var page = document.Pages[1];
    var content = page.Contents[1]; // Get the first content stream

    // Insert graphics state selection and a semi‑transparent rectangle
    var operators = new List<Operator>
    {
        new Operator("GS0", "gs"),                     // Select our custom graphics state
        new Operator("0.5", "w"),                      // Set line width (optional)
        new Operator("100", "100", "200", "150", "re"), // Rectangle (x, y, width, height)
        new Operator("B")                              // Stroke the rectangle
    };

    foreach (var op in operators)
        content.Operators.Add(op);

    document.Save(@"YOUR_DIRECTORY\final_output.pdf");
}
```

Prostokąt zostanie narysowany z 50 % przezroczystością wypełnienia, podczas gdy obrys pozostanie w pełni nieprzezroczysty, dokładnie tak jak zdefiniowano w słowniku **create PDF graphics state**.

## Typowe pułapki i jak ich unikać

| Problem | Dlaczego się pojawia | Rozwiązanie |
|-------|----------------|-----|
| `ExtGState` entry not found | Niektóre pliki PDF pomijają ten słownik całkowicie. | `DictionaryEditor` automatycznie tworzy go, gdy dodasz pierwszy wpis, więc dodatkowe sprawdzanie nie jest potrzebne. |
| Opacity values > 1 or < 0 | Specyfikacja PDF ogranicza przezroczystość do zakresu `[0,1]`. | Ogranicz wartości przed utworzeniem `CosPdfNumber`. |
| Blend mode typo | Nazwy trybów mieszania w PDF są wrażliwe na wielkość liter. | Używaj dokładnych nazw, takich jak `"Normal"`, `"Multiply"`, `"Screen"`. |
| License watermark | Wersja ewaluacyjna dodaje znak wodny na pierwszej stronie. | Zastosuj prawidłowy plik licencji przed otwarciem dokumentu. |

## Pełny, gotowy do uruchomienia przykład

Poniżej znajduje się samodzielny program, który możesz skopiować, wkleić i uruchomić. Zamień `YOUR_DIRECTORY` na rzeczywistą ścieżkę folderu na swoim komputerze.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;

class Program
{
    static void Main()
    {
        // Optional: apply license to remove evaluation watermark
        // var license = new Aspose.Pdf.License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        using (var document = new Document(inputPath))
        {
            // 1️⃣ Get first page and its resources
            var page = document.Pages[1];
            var resourcesEditor = new DictionaryEditor(page.Resources);

            // 2️⃣ Access (or create) ExtGState dictionary
            var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // 3️⃣ Build new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // 4️⃣ Register the state with a name (GS0)
            extGState.Add("


## Co warto nauczyć się dalej?


Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu wraz z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Utwórz niestandardowy stan graficzny w PDF przy użyciu Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Dodaj stan graficzny do PDF przy użyciu Aspose.PDF dla .NET (C#)](/pdf/english/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/)
- [Jak utworzyć pusty stan graficzny w PDF przy użyciu C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}