---
category: general
date: 2026-08-08
description: Ustaw przezroczystość PDF w C# przy użyciu Aspose.PDF – dowiedz się,
  jak dostosować przezroczystość obrysu i wypełnienia kilkoma liniami kodu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set pdf opacity
- Aspose.PDF for .NET
- C# graphics state
- PDF resource dictionary
- blend mode
- PDF transparency
language: pl
lastmod: 2026-08-08
og_description: Ustaw przezroczystość PDF w C# szybko. Ten przewodnik pokazuje, jak
  modyfikować przezroczystość obrysu i wypełnienia przy użyciu API stanu graficznego
  Aspose.PDF.
og_image_alt: Screenshot of C# code that sets PDF opacity with Aspose.PDF
og_title: Ustaw przezroczystość PDF w C# z Aspose.PDF – samouczek krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Set PDF opacity in C# using Aspose.PDF – learn how to adjust stroke
    and fill transparency with a few lines of code.
  headline: Set PDF opacity in C# with Aspose.PDF – complete guide
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Ustaw przezroczystość PDF w C# z Aspose.PDF – kompletny przewodnik
url: /pl/net/images-graphics/set-pdf-opacity-in-c-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ustaw przezroczystość PDF w C# przy użyciu Aspose.PDF – kompletny przewodnik

Jeśli potrzebujesz **ustawić przezroczystość PDF** dla konkretnych operacji rysowania, ten tutorial pokaże Ci dokładnie, jak to zrobić przy użyciu Aspose.PDF for .NET. Niezależnie od tego, czy tworzysz znaki wodne, półprzezroczyste nakładki, czy własne grafiki, poznasz zwięzłe, gotowe do produkcji podejście.

W kolejnych sekcjach omówimy wszystko, od ładowania pliku PDF po edycję jego stanu graficznego, dodanie nowej definicji przezroczystości i zapisanie wyniku. Nie jest wymagana żadna zewnętrzna dokumentacja — wystarczy poniższy kod oraz krótkie wyjaśnienie każdego kroku.

## Wymagania wstępne

Przed rozpoczęciem upewnij się, że masz:

* .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.7+)
* Ważną licencję Aspose.PDF for .NET (bezpłatna wersja próbna wystarczy do oceny)
* Plik PDF wejściowy (`input.pdf`) znajdujący się w folderze, do którego masz uprawnienia odczytu/zapisu
* Visual Studio 2022 lub dowolne inne IDE obsługujące C#

## Krok 1 – Załaduj dokument PDF (Aspose.PDF for .NET)

Pierwszym zadaniem jest otwarcie istniejącego pliku PDF. Aspose.PDF reprezentuje plik PDF klasą `Document`, która daje pełny dostęp do stron, zasobów i obiektów niskiego poziomu.

```csharp
// Load the PDF document from disk
string inputPath = @"C:\MyFolder\input.pdf";
using var doc = new Aspose.Pdf.Document(inputPath);
```

*Dlaczego to jest ważne*: Ładowanie dokumentu tworzy model w pamięci, który możesz bezpiecznie modyfikować. Instrukcja `using` zapewnia automatyczne zwolnienie uchwytu pliku po zakończeniu pracy.

## Krok 2 – Pobierz pierwszą stronę, którą chcesz edytować

Przezroczystość jest definiowana na poziomie strony poprzez słownik zasobów strony. Tutaj celujemy w pierwszą stronę, ale możesz przejść przez `doc.Pages` w pętli, aby wykonać operację wsadową.

```csharp
// Access the first page (pages are 1‑based in Aspose.PDF)
var page = doc.Pages[1];
```

*Dlaczego to jest ważne*: Każda strona ma własną kolekcję `Resources`, w której przechowywane są stany graficzne, czcionki, obrazy itp. Modyfikacja właściwej strony zapewnia, że efekt przezroczystości pojawi się tam, gdzie tego oczekujesz.

## Krok 3 – Otwórz słownik zasobów strony do edycji

Aspose.PDF udostępnia pomocnika `DictionaryEditor`, który umożliwia manipulację słownikami PDF niskiego poziomu bez uszkadzania struktury pliku.

```csharp
// Prepare a dictionary editor for the page's resources
var dictEditor = new Aspose.Pdf.DictionaryEditor(page.Resources);
```

*Dlaczego to jest ważne*: Bezpośrednia edycja słowników COS (Content Object System) jest jedynym sposobem na wstrzyknięcie własnego stanu graficznego. Edytor ukrywa niskopoziomową składnię, jednocześnie utrzymując poprawność PDF.

## Krok 4 – Pobierz istniejący słownik ExtGState

Słownik **ExtGState** (external graphics state) przechowuje informacje o przezroczystości, trybie mieszania, grubości linii itp. Jeśli nie istnieje, Aspose.PDF utworzy go automatycznie po dodaniu nowego wpisu.

```csharp
// Get the ExtGState dictionary; create it if missing
var extGState = dictEditor["ExtGState"]?.ToCosPdfDictionary()
                ?? new Aspose.Pdf.Cos.CosPdfDictionary(doc);
```

*Dlaczego to jest ważne*: Bez wpisu `ExtGState` nie będziesz mógł odwołać się do własnej przezroczystości później w strumieniu zawartości strony. Ten krok zapewnia, że kontener jest obecny.

## Krok 5 – Utwórz nowy stan graficzny z żądaną przezroczystością

Stan graficzny to zbiór parametrów. Dla przezroczystości ustawiamy `CA` (stroke opacity) oraz `ca` (fill opacity). Dodatkowo definiujemy tryb mieszania (`BM`), aby kontrolować, jak przezroczyste piksele współdziałają z zawartością pod spodem.

```csharp
// Build a new graphics state dictionary
var newGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(doc);
newGs.Add("CA", new Aspose.Pdf.Cos.CosPdfNumber(0.8)); // 80 % stroke opacity
newGs.Add("ca", new Aspose.Pdf.Cos.CosPdfNumber(0.4)); // 40 % fill opacity
newGs.Add("BM", new Aspose.Pdf.Cos.CosPdfName("Normal")); // standard blend mode
```

*Dlaczego to jest ważne*: `CA` i `ca` przyjmują wartości od 0 (całkowicie przezroczyste) do 1 (całkowicie nieprzezroczyste). Dostosuj te liczby, aby uzyskać pożądany efekt wizualny. Tryb mieszania `"Normal"` jest najczęściej używany, ale możesz eksperymentować z `"Multiply"` lub `"Screen"` dla artystycznych efektów.

## Krok 6 – Zarejestruj nowy stan graficzny w kolekcji ExtGState

Każdy stan graficzny musi mieć unikalną nazwę (np. `GS0`). Dodajemy nasz słownik do kolekcji `ExtGState`, a następnie aktualizujemy zasoby strony.

```csharp
// Add the new graphics state under the name "GS0"
extGState.Add("GS0", newGs);

// Ensure the ExtGState entry is stored back in the page resources
dictEditor["ExtGState"] = extGState;
```

*Dlaczego to jest ważne*: Dzięki nazwie stanu (`GS0`) możesz odwołać się do niego później w strumieniu zawartości strony przy użyciu operatora `gs`. Jeśli potrzebujesz kilku poziomów przezroczystości, utwórz dodatkowe wpisy (`GS1`, `GS2`, …).

## Krok 7 – Zastosuj stan graficzny do poleceń rysowania (opcjonalnie)

Jeśli chcesz natychmiast zastosować przezroczystość do istniejącej zawartości, musisz edytować strumień zawartości strony. Poniżej prosty przykład rysujący półprzezroczysty prostokąt przy użyciu nowo utworzonego stanu.

```csharp
// Build a content stream that uses the graphics state GS0
var content = new Aspose.Pdf.Operator.GSave();
content.Operators.Add(new Aspose.Pdf.Operator.SetGraphicsState("GS0"));
content.Operators.Add(new Aspose.Pdf.Operator.SetFillColorRgb(1, 0, 0)); // red fill
content.Operators.Add(new Aspose.Pdf.Operator.Rectangle(100, 500, 200, 100));
content.Operators.Add(new Aspose.Pdf.Operator.FillPath());
content.Operators.Add(new Aspose.Pdf.Operator.GRestore());

page.Contents.Add(content);
```

*Dlaczego to jest ważne*: Operator `gs` (`SetGraphicsState`) instruuje renderer PDF, aby użył wartości przezroczystości zdefiniowanych w `GS0` dla wszystkich kolejnych poleceń rysowania. Para `gsave`/`grestore` zapewnia, że pozostałe elementy strony pozostają niezmienione.

## Krok 8 – Zapisz zmodyfikowany PDF

Na koniec zapisz zaktualizowany dokument na dysku.

```csharp
// Save the PDF with the new opacity settings
string outputPath = @"C:\MyFolder\output.pdf";
doc.Save(outputPath);
```

*Dlaczego to jest ważne*: Zapis finalizuje wszystkie zmiany, osadza nowy stan graficzny i tworzy plik PDF, który każdy przeglądarka (Adobe Acrobat, Chrome itp.) wyświetli z zamierzoną przezroczystością.

### Oczekiwany rezultat

Otwórz `output.pdf` w przeglądarce PDF. Powinieneś zobaczyć czerwony prostokąt, którego obrys ma 80 % nieprzezroczystości, a wypełnienie 40 % nieprzezroczystości, płynnie łącząc się z tłem. Reszta strony pozostaje niezmieniona.

## Typowe warianty i przypadki brzegowe

| Sytuacja | Co zmienić | Powód |
|-----------|----------------|--------|
| **Multiple opacity levels** | Utwórz dodatkowe stany graficzne (`GS1`, `GS2`, …) z różnymi wartościami `CA`/`ca` i odwołuj się do nich w potrzebnych miejscach | Umożliwia precyzyjną kontrolę nad różnymi elementami |
| **Different blend modes** | Użyj `"Multiply"`, `"Screen"`, `"Overlay"` itp., zamiast `"Normal"` w wpisie `BM` | Tworzy artystyczne efekty mieszania |
| **Applying to an existing content stream** | Wstaw `SetGraphicsState` przed konkretnymi operatorami rysowania, które chcesz zmodyfikować | Zapobiega niepożądanej przezroczystości w niepowiązanych obiektach |
| **Large PDFs** | Przetwarzaj strony w pętli `foreach (Page p in doc.Pages)`, aby nie ładować całego pliku do pamięci jednocześnie | Poprawia wydajność i zmniejsza obciążenie pamięci |
| **No existing ExtGState** | Kod w Kroku 4 już tworzy słownik, jeśli go brak, więc nie wymaga dodatkowej obsługi | Gwarantuje, że słownik jest obecny |

### Wskazówka profesjonalisty

Gdy dodajesz wiele własnych stanów graficznych, zachowaj spójną konwencję nazewnictwa (`GS0`, `GS1`, …) i udokumentuj przeznaczenie każdego w bloku komentarzy. Ułatwi to przyszłą konserwację, szczególnie w projektach zespołowych.

## Pełny, gotowy do uruchomienia przykład

Poniżej znajduje się kompletny program, który możesz skopiować, wkleić i uruchomić. Zawiera wszystkie kroki, niezbędne dyrektywy `using` oraz komentarze.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

namespace PdfOpacityDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the PDF
            string inputPath = @"C:\MyFolder\input.pdf";
            using var doc = new Document(inputPath);

            // 2. Get the first page (adjust index for other pages)
            var page = doc.Pages[1];

            // 3. Open the page's resource dictionary
            var dictEditor = new DictionaryEditor(page.Resources);

            // 4. Retrieve or create the ExtGState dictionary
            var extGState = dictEditor["ExtGState"]?.ToCosPdfDictionary()
                            ?? new CosPdfDictionary(doc);

            // 5. Create a new graphics state with desired opacity
            var newGs = CosPdfDictionary.CreateEmptyDictionary(doc);
            newGs.Add("CA", new CosPdfNumber(0.8));          // stroke opacity (80%)
            newGs.Add("ca", new CosPdfNumber(0.4));          // fill opacity (40%)
            newGs.Add("BM", new CosPdfName("Normal"));      // blend mode

            // 6. Register the graphics state as "GS0"
            extGState.Add("GS0", newGs);
            dictEditor["ExtGState"] = extGState; // write back to resources

            // 7. (Optional) Draw a rectangle using the new opacity
            var content = new Operator.GSave();
            content.Operators.Add(new Operator.SetGraphicsState("GS0"));
            content.Operators.Add(new Operator.SetFillColorRgb(1, 0, 0)); // red
            content.Operators.Add(new Operator.Rectangle(100, 500, 200, 100));
            content.Operators.Add(new Operator.FillPath());
            content.Operators.Add(new Operator.GRestore());

            page.Contents.Add(content);

            // 8. Save the modified PDF
            string outputPath = @"C:\MyFolder\output.pdf";
            doc.Save(outputPath);

            Console.WriteLine("PDF saved with new opacity settings at: " + outputPath);
        }
    }
}
```

Uruchom program,

## Co warto się nauczyć dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i poznać alternatywne podejścia w własnych projektach.

- [Ustaw tła obrazów w PDF przy użyciu Aspose.PDF for .NET: Kompletny przewodnik](/pdf/english/net/images-graphics/aspose-pdf-net-set-image-backgrounds/)
- [Jak tworzyć przerywane linie w PDF przy użyciu Aspose.PDF for .NET: Przewodnik krok po kroku](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Jak dostosować PDF przy użyciu Aspose.PDF for .NET: Ustaw marginesy strony i rysuj linie](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}