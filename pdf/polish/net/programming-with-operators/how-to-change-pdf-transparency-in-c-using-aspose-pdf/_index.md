---
category: general
date: 2026-09-24
description: Dowiedz się, jak zmienić przezroczystość PDF w C# przy użyciu Aspose.Pdf.
  Ten przewodnik krok po kroku obejmuje przezroczystość PDF, tryb mieszania oraz edycję
  stanu graficznego.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.Pdf graphics state
- PDF opacity
- C# PDF manipulation
- blend mode PDF
- modify PDF resources
language: pl
lastmod: 2026-09-24
og_description: Zmieniaj przezroczystość PDF w C# przy użyciu Aspose.Pdf. Postępuj
  zgodnie z tym przewodnikiem, aby edytować krycie PDF, tryb mieszania i stan graficzny,
  uzyskując profesjonalny efekt dokumentu.
og_image_alt: Screenshot showing C# code that changes PDF transparency
og_title: Zmiana przezroczystości PDF w C# – kompletny przewodnik Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Learn how to change PDF transparency in C# with Aspose.Pdf. This step‑by‑step
    guide covers PDF opacity, blend mode and graphics state editing.
  headline: How to change PDF transparency in C# using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- C#
- Aspose.Pdf
- Transparency
title: Jak zmienić przezroczystość PDF w C# przy użyciu Aspose.Pdf
url: /pl/net/programming-with-operators/how-to-change-pdf-transparency-in-c-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zmienić przezroczystość PDF w C# przy użyciu Aspose.Pdf

Jeśli potrzebujesz **zmienić przezroczystość PDF** w projekcie .NET, ten przewodnik pokaże Ci dokładnie, jak to zrobić przy użyciu Aspose.Pdf. Zobaczysz kompletny, gotowy do uruchomienia przykład, który modyfikuje nieprzezroczystość PDF, ustawia tryb mieszania i aktualizuje słownik stanu graficznego strony.

Zmiana przezroczystości PDF jest częstym wymogiem, gdy chcesz dodać znaki wodne, nakładać grafiki lub uzyskać własne efekty wizualne. W tym tutorialu nauczysz się edytować **stan graficzny Aspose.Pdf**, dostosowywać **nieprzezroczystość PDF** oraz pracować z ustawieniami **blend mode PDF** — wszystko przy użyciu czystego kodu C#.

## Wymagania wstępne

Przed rozpoczęciem upewnij się, że masz:

* .NET 6.0 lub nowszy zainstalowany  
* Licencję Aspose.Pdf for .NET (lub tymczasowy klucz ewaluacyjny)  
* Plik PDF o nazwie `input.pdf` w folderze, który możesz odwołać jako `YOUR_DIRECTORY`  
* Podstawową znajomość C# i Visual Studio (dowolne IDE działa)

Nie są wymagane dodatkowe pakiety NuGet poza `Aspose.Pdf`. Kod działa na Windows, Linux i macOS, ponieważ Aspose.Pdf jest wieloplatformowy.

## Zmiana przezroczystości PDF – krok 1: otwarcie dokumentu PDF

Pierwszą operacją jest załadowanie źródłowego pliku PDF. Użycie bloku `using` zapewnia automatyczne zwolnienie uchwytu pliku.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System.Collections.Generic;

string inputPath  = @"YOUR_DIRECTORY\input.pdf";
string outputPath = @"YOUR_DIRECTORY\output.pdf";

using (var document = new Document(inputPath))
{
    // The document is now ready for manipulation.
```

Otwieranie dokumentu jest podstawą każdego zadania **manipulacji PDF w C#**. Jeśli plik nie zostanie znaleziony, Aspose.Pdf zgłasza `FileNotFoundException`, więc sprawdź ścieżkę przed uruchomieniem kodu.

## Dostęp do zasobów strony przy użyciu stanu graficznego Aspose.Pdf

Następnie pobieramy pierwszą stronę i jej słownik zasobów. Słownik zasobów przechowuje obiekty takie jak czcionki, obrazy oraz wpisy **ExtGState**, które kontrolują parametry graficzne.

```csharp
    // Step 2: Get the first page of the document
    var page = document.Pages[1];

    // Step 3: Access the page's resource dictionary for editing
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

Klasa `DictionaryEditor` zapewnia wygodny wrapper do odczytu i zapisu słowników PDF. Skupiamy się tutaj na słowniku **ExtGState**, ponieważ przechowuje on ustawienia przezroczystości.

## Utworzenie i skonfigurowanie nowego stanu graficznego dla nieprzezroczystości PDF

Teraz budujemy nowy słownik stanu graficznego. Ten słownik będzie zawierał parametry definiujące nieprzezroczystość obrysów (`CA`), nieprzezroczystość wypełnień (`ca`) oraz tryb mieszania (`BM`).

```csharp
    // Step 4: Retrieve the existing ExtGState dictionary (graphics states)
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

    // Step 5: Create a new empty graphics state dictionary
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

    // Step 6: Define graphics state parameters (stroke opacity, fill opacity, blend mode)
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),            // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),          // Fill opacity (50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))       // Blend mode PDF (standard normal blending)
    };

    // Step 7: Add each parameter to the new graphics state dictionary
    foreach (var param in parameters)
        newGraphicsState.Add(param);
```

* **`CA`** kontroluje nieprzezroczystość operacji kreskowych (linie, obramowania).  
* **`ca`** kontroluje nieprzezroczystość operacji wypełniania (wypełnione kształty, tekst).  
* **`BM`** wybiera tryb mieszania; domyślnie jest to `"Normal"`, ale możesz użyć `"Multiply"` lub `"Screen"` dla efektów artystycznych.

Te ustawienia są rdzeniem manipulacji **nieprzezroczystością PDF**. Dostosuj wartości liczbowe do swojego projektu wizualnego — `0` oznacza całkowitą przezroczystość, `1` pełną nieprzezroczystość.

## Wstawienie stanu graficznego i zapisanie dokumentu

Po skonstruowaniu nowego stanu dodajemy go do istniejącego słownika **ExtGState** pod unikalną nazwą (`GS0`). Na koniec zapisujemy zmodyfikowany plik PDF.

```csharp
    // Step 8: Insert the new graphics state into the ExtGState dictionary with a name
    extGState.Add("GS0", newGraphicsState);

    // Step 9: Save the modified PDF document
    document.Save(outputPath);
}
```

Gdy PDF zostanie otwarty w przeglądarce, każdy element odwołujący się do `GS0` zostanie wyrenderowany z określoną przezroczystością. Później możesz zastosować ten stan graficzny do wybranych obiektów, używając właściwości `GraphicsState` poleceń rysujących (np. `page.Contents.Add(new TextFragment(...){ GraphicsState = "GS0" })`).

## Zweryfikuj wynik

Otwórz `output.pdf` w Adobe Acrobat Reader, Foxit lub dowolnym przeglądarce PDF obsługującej przezroczystość. Powinieneś zobaczyć elementy wypełnienia pierwszej strony renderowane z 50 % nieprzezroczystością, podczas gdy obrysy pozostają w pełni nieprzezroczyste. Jeśli nie zauważysz zmiany, upewnij się, że strona faktycznie używa nowego stanu graficznego — w przeciwnym razie możesz jawnie przypisać `GS0` do obiektów, które chcesz zmodyfikować.

![Przykład kodu C# zmieniającego przezroczystość PDF](path/to/image.png){: .img-responsive alt="Przykład kodu C# zmieniającego przezroczystość PDF"}

*Powyższy obraz przedstawia kompletny kod C#, który zmienia przezroczystość PDF.*

## Typowe warianty i przypadki brzegowe

| Sytuacja | Jak dostosować kod |
|-----------|-----------------------|
| **Wiele stron** | Iteruj po `document.Pages` i powtórz kroki 2‑8 dla każdej strony. |
| **Inny tryb mieszania** | Zastąp `"Normal"` przez `"Multiply"`, `"Screen"` lub dowolną nazwę trybu mieszania zgodną ze standardem PDF. |
| **Wyższa nieprzezroczystość wypełnienia** | Zmień `new CosPdfNumber(0.5)` na wartość pomiędzy `0` a `1`. |
| **Brak istniejącego ExtGState** | Jeśli `resourcesEditor["ExtGState"]` zwraca `null`, utwórz nowy słownik: `var extGState = CosPdfDictionary.CreateEmptyDictionary(document); resourcesEditor["ExtGState"] = extGState;` |

Te warianty pokazują elastyczność **modyfikacji zasobów PDF** przy użyciu Aspose.Pdf. Dostosowując parametry, możesz tworzyć znaki wodne, półprzezroczyste nakładki lub własne elementy UI wewnątrz pliku PDF.

## Pełny, gotowy do uruchomienia przykład

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do nowego projektu aplikacji konsolowej. Zawiera wszystkie niezbędne dyrektywy `using`, obsługę błędów oraz komentarze.



## Co powinieneś się nauczyć dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z krok po kroku wyjaśnieniami, pomagając opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Zmienianie nieprzezroczystości PDF przy użyciu Aspose.PDF – Kompletny przewodnik C#](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Zmienianie nieprzezroczystości PDF w C# – Kompletny przewodnik Aspose](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-in-c-complete-aspose-guide/)
- [Dodawanie przezroczystości do PDF przy użyciu Aspose – Kompletny przewodnik C#](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}