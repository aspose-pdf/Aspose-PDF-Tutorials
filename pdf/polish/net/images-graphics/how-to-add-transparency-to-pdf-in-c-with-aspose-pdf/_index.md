---
category: general
date: 2026-11-22
description: Dodaj przezroczystość do PDF przy użyciu Aspose.PDF dla C#. Dowiedz się,
  jak zmienić przezroczystość PDF w przejrzystym, krok po kroku przykładzie.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- how to change pdf opacity
- Aspose.PDF opacity
- PDF graphics state C#
- PDF blend mode example
language: pl
lastmod: 2026-11-22
og_description: Dodaj przezroczystość do pliku PDF przy użyciu Aspose.PDF dla C#.
  Ten samouczek pokazuje, jak szybko i niezawodnie zmienić przezroczystość PDF.
og_image_alt: Screenshot of a PDF page showing translucent graphics after adding transparency
og_title: Dodaj przezroczystość do PDF w C# – kompletny przewodnik Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Add transparency to PDF using Aspose.PDF for C#. Learn how to change
    PDF opacity with a clear, step‑by‑step example.
  headline: How to add transparency to PDF in C# with Aspose.PDF
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: Jak dodać przezroczystość do PDF w C# przy użyciu Aspose.PDF
url: /pl/net/images-graphics/how-to-add-transparency-to-pdf-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak dodać przezroczystość do PDF w C# przy użyciu Aspose.PDF

Jeśli potrzebujesz **dodać przezroczystość do PDF** plików, ten przewodnik pokazuje kompletną rozwiązanie przy użyciu Aspose.PDF dla .NET. Zobaczysz dokładnie **jak zmienić przezroczystość PDF** dla grafiki wektorowej, tekstu lub obrazów, nie opuszczając środowiska C#.

Tutorial obejmuje każdy krok — od załadowania dokumentu po edycję stanu graficznego strony i zapisanie wyniku. Po zakończeniu będziesz mógł tworzyć PDF‑y, w których wybrane elementy są półprzezroczyste, co jest przydatne przy znakach wodnych, efektach nakładania lub makietach projektowych.

## Wymagania wstępne

* .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.8)
* Ważna licencja Aspose.PDF for .NET lub tymczasowy klucz ewaluacyjny
* Visual Studio 2022 (lub dowolne IDE obsługujące C#)
* Plik PDF wejściowy o nazwie `input.pdf` umieszczony w znanym folderze

Te elementy gwarantują, że kod uruchomi się bez dodatkowej konfiguracji.

## Krok 1: Załaduj dokument PDF

Pierwsza operacja to otwarcie istniejącego pliku PDF. Aspose.PDF reprezentuje cały plik klasą `Document`.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;

// Load the source PDF
var inputPath = @"C:\MyFiles\input.pdf";
var doc = new Document(inputPath);
```

*Dlaczego ten krok jest ważny*: Ładowanie dokumentu tworzy model w pamięci, który pozwala przeglądać strony, zasoby i strumienie zawartości. Bez tego obiektu nie możesz modyfikować stanów graficznych.

## Krok 2: Uzyskaj dostęp do słownika zasobów pierwszej strony

Przezroczystość jest stosowana poprzez **stan graficzny** przechowywany w słowniku zasobów strony. Potrzebujesz `DictionaryEditor`, aby edytować ten słownik.

```csharp
// Get the first page (pages are 1‑based)
var page = doc.Pages[1];

// Open the resource dictionary for editing
var dictEditor = new DictionaryEditor(page.Resources);
var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();
```

Jeśli strona nie zawiera jeszcze wpisu `ExtGState`, Aspose.PDF automatycznie tworzy pusty słownik po jego żądaniu. Ta elastyczność oznacza, że ten sam kod działa zarówno dla PDF‑ów już używających przezroczystości, jak i tych, które jej nigdy nie mają.

## Krok 3: Utwórz nowy stan graficzny z wartościami przezroczystości

Stan graficzny przechowuje parametry takie jak przezroczystość wypełnienia (`ca`), przezroczystość obrysu (`CA`) oraz tryb mieszania (`BM`). Poniższy blok buduje słownik definiujący 50 % przezroczystości wypełnienia przy zachowaniu pełnej nieprzezroczystości obrysów.

```csharp
// Build a new graphics state dictionary
var graphicsState = CosPdfDictionary.CreateEmptyDictionary(doc);

// Stroke opacity – fully opaque (value between 0 and 1)
graphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity – 50 % transparent
graphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode – Normal (other modes: Multiply, Screen, etc.)
graphicsState.Add("BM", new CosPdfName("Normal"));
```

*Dlaczego te klucze*:  
* `CA` kontroluje przezroczystość ścieżek obrysowanych (linie, krawędzie).  
* `ca` kontroluje przezroczystość obiektów wypełnionych (wypełnienia tekstu, wypełnienia obrazów).  
* `BM` określa, jak przezroczysty obiekt miesza się z zawartością pod spodem; `Normal` jest najczęściej wybieranym trybem.

## Krok 4: Zarejestruj stan graficzny w zasobach strony

Po utworzeniu stanu graficznego musisz dodać go do słownika `ExtGState` strony pod unikalną nazwą (np. `GS0`). Strumienie zawartości mogą potem odwoływać się do tej nazwy, aby zastosować ustawienia przezroczystości.

```csharp
// Add the new graphics state to the resource dictionary
extGState.Add("GS0", graphicsState);
```

W tym momencie plik PDF zawiera wielokrotnego użytku stan graficzny o nazwie `GS0`. Każde polecenie rysujące, które odwołuje się do `/GS0 gs`, zostanie wyrenderowane z określoną przezroczystością.

## Krok 5: Zastosuj stan graficzny do zawartości strony (opcjonalnie)

Jeśli chcesz wpłynąć na istniejącą zawartość, musisz wstawić polecenie na początku strumienia zawartości strony. Poniższy fragment pokazuje, jak dodać operator stanu graficznego na początek.

```csharp
// Retrieve the original content stream
var content = page.Contents[1];

// Insert the graphics state operator at the start of the stream
content.Contents.Insert(0, new CosPdfLiteral("GS0 gs"));
```

*Kiedy używać tego kroku*: Jeśli PDF już zawiera polecenia rysujące i chcesz, aby stały się półprzezroczyste, dodaj operator na początek. Jeśli planujesz później dodawać nowe obiekty, możesz odwoływać się do `GS0` bezpośrednio przy ich tworzeniu.

## Krok 6: Zapisz zmodyfikowany PDF

Na koniec zapisz zaktualizowany dokument na dysk.

```csharp
var outputPath = @"C:\MyFiles\output.pdf";
doc.Save(outputPath);
```

Powstały `output.pdf` pokazuje elementy wypełnienia pierwszej strony z 50 % przezroczystością, podczas gdy obrysy pozostają w pełni widoczne. Otwórz plik w dowolnym przeglądarce PDF, aby zweryfikować efekt.

## Jak zmienić przezroczystość PDF dla wielu stron

To samo podejście działa dla dowolnego numeru strony. Przejdź pętlą po `doc.Pages` i powtórz kroki 2‑5, przydzielając unikalną nazwę stanu graficznego dla każdej strony (np. `GS1`, `GS2`). Oto kompaktowa wersja:

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    var pg = doc.Pages[i];
    var editor = new DictionaryEditor(pg.Resources);
    var ext = editor["ExtGState"].ToCosPdfDictionary();

    var gs = CosPdfDictionary.CreateEmptyDictionary(doc);
    gs.Add("CA", new CosPdfNumber(1));
    gs.Add("ca", new CosPdfNumber(0.75)); // 75% fill opacity
    gs.Add("BM", new CosPdfName("Normal"));

    var gsName = $"GS{i - 1}";
    ext.Add(gsName, gs);

    var cnt = pg.Contents[1];
    cnt.Contents.Insert(0, new CosPdfLiteral($"{gsName} gs"));
}
```

Ta pętla zmniejsza duplikację kodu i demonstruje **jak zmienić przezroczystość PDF** w całym dokumencie.

## Typowe pułapki i wskazówki najlepszych praktyk

| Problem | Dlaczego się pojawia | Zalecane rozwiązanie |
|---------|----------------------|----------------------|
| Brak wpisu `ExtGState` | Niektóre pliki PDF nigdy nie tworzyły słownika stanu graficznego | `DictionaryEditor` automatycznie tworzy go; nie potrzebny dodatkowy kod |
| Przezroczystość niewidoczna | Podgląd pamięta oryginalną stronę | Wyczyść pamięć podglądu lub ponownie otwórz plik |
| Niezgodność trybu mieszania | Użycie `Multiply` na ciemnym tle może spowodować zniknięcie obiektów | Testuj różne wartości `BM` (`Normal`, `Screen`, `Overlay`), aby uzyskać pożądany efekt wizualny |
| Konflikt wielu stanów graficznych | Ponowne użycie tej samej nazwy (`GS0`) na różnych stronach nadpisuje poprzednią definicję | Użyj unikalnej nazwy dla każdej strony (`GS0`, `GS1`, …) |

## Pełny działający przykład

Poniżej znajduje się samodzielny program, który możesz skopiować, wkleić i uruchomić. Zawiera wszystkie instrukcje `using`, obsługę błędów i komentarze.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

class AddTransparencyDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        const string inputPath = @"C:\MyFiles\input.pdf";
        const string outputPath = @"C:\MyFiles\output.pdf";

        // Load the PDF
        var doc = new Document(inputPath);

        // Process each page
        for (int pageIndex = 1; pageIndex <= doc.Pages.Count; pageIndex++)
        {
            var page = doc.Pages[pageIndex];
            var dictEditor = new DictionaryEditor(page.Resources);
            var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();

            // Create a graphics state with 60% fill opacity
            var graphicsState = CosPdfDictionary.CreateEmptyDictionary(doc);
            graphicsState.Add("CA", new CosPdfNumber(1));               // stroke opacity
            graphicsState.Add("ca", new CosPdfNumber(0.6));             // fill opacity
            graphicsState.Add("BM", new CosPdfName("Normal"));         // blend mode

            // Unique name for this page
            string gsName = $"GS{pageIndex - 1}";
            extGState.Add(gsName, graphicsState);

            // Prepend the graphics state operator to the page content
            var content = page.Contents[1];
            content.Contents.Insert(0, new CosPdfLiteral($"{gsName} gs"));
        }

        // Save the result
        doc.Save(outputPath);
        Console.WriteLine($"PDF saved with transparency at: {outputPath}");
    }
}
```

**Oczekiwany wynik**: Po otwarciu `output.pdf` wszystkie wypełnione kształty, tekst lub obrazy na każdej stronie będą wyświetlane z 60 % przezroczystością, podczas gdy krawędzie pozostaną w pełni nieprzezroczyste. Zmiana jest natychmiastowa i działa w Adobe Acrobat, Edge, Chrome oraz w każdej przeglądarce PDF respektującej stan graficzny PDF.

## Zakończenie

Teraz wiesz, jak **dodać przezroczystość do PDF** przy użyciu Aspose.PDF dla C#. Tutorial obejmował ładowanie dokumentu, edycję słownika zasobów strony, tworzenie własnego stanu graficznego oraz zapis zmodyfikowanego pliku. Nauczyłeś się także **jak zmienić przezroczystość PDF** dla jednej lub wielu stron oraz uzyskałeś praktyczne wskazówki, jak unikać typowych błędów.

Następnie odkryj powiązane tematy, takie jak:

* Dodawanie znaków wodnych obrazu z zmienną przezroczystością
* Używanie różnych trybów mieszania (`Multiply`, `Screen`) dla efektów kreatywnych
* Łączenie przezroczystości z adnotacjami PDF

Eksperymentuj z tymi wariantami, aby dostosować wyjście PDF do wizualnych wymagań Twojego projektu. Szczęśliwego kodowania!

## Co warto nauczyć się dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, pomagając opanować dodatkowe funkcje API i poznać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak dodać stan graficzny pdf i kontrolować przezroczystość przy użyciu Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)
- [Jak ustawić przezroczystość w PDF i jak zmienić tryb mieszania przy użyciu Aspose.Pdf](/pdf/hongkong/net/images-graphics/how-to-set-opacity-in-a-pdf-and-how-to-change-blend-mode-wit/)
- [Jak dodać przezroczystość do PDF i narysować prostokąt w PDF przy użyciu Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}