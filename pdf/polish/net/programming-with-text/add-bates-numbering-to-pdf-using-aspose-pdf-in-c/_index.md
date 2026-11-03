---
category: general
date: 2026-09-27
description: Dodaj numerację Bates do pliku PDF przy użyciu Aspose.PDF w C#. Dowiedz
  się, jak wczytać dokument PDF, ustawić opcje numeracji Bates i zapisać zaktualizowany
  plik.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- load pdf document
- how to add bates numbering
- Aspose.PDF C#
- PDF Bates numbering example
language: pl
lastmod: 2026-09-27
og_description: Dodaj numerację Bates do pliku PDF przy użyciu Aspose.PDF w C#. Ten
  samouczek pokazuje, jak wczytać dokument PDF, skonfigurować numerację Bates i zapisać
  wynik.
og_image_alt: Screenshot of a PDF page displaying Bates numbers in the footer
og_title: Dodaj numerację Bates do PDF za pomocą Aspose.PDF – przewodnik C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Add bates numbering to PDF using Aspose.PDF in C#. Learn how to load
    a PDF document, set Bates numbering options, and save the updated file.
  headline: Add bates numbering to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF processing
title: Dodaj numerację Batesa do PDF przy użyciu Aspose.PDF w C#
url: /pl/net/programming-with-text/add-bates-numbering-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj numerację Bates do PDF przy użyciu Aspose.PDF w C#

Jeśli potrzebujesz **dodać numerację Bates** do pliku PDF, ten przewodnik pokaże Ci kompletną, gotową do uruchomienia rozwiązanie. Zobaczysz, jak **wczytać dokument PDF**, skonfigurować opcje numeracji Bates oraz zapisać ponumerowany plik na dysku — wszystko przy użyciu Aspose.PDF dla .NET.

Stosowanie numerów Bates jest powszechne w procesach prawnych, organach ścigania i archiwizacji. Po zakończeniu tego tutorialu będziesz mógł osadzić kolejny identyfikator na każdej stronie, dostosować prefiks i rozpocząć numerację od dowolnej liczby.

## Czego się nauczysz

* Jak **wczytać zawartość dokumentu PDF** do obiektu `Aspose.Pdf.Document`.  
* Dokładne kroki **jak dodać numerację Bates** przy użyciu `BatesNumberingOptions`.  
* Jak zapisać zmodyfikowany plik, zachowując pierwotny układ i jakość.  

Nie są wymagane żadne zewnętrzne narzędzia — jedynie pakiet NuGet Aspose.PDF oraz środowisko programistyczne .NET (Visual Studio, VS Code lub Rider).  

---

## Krok 1: Zainstaluj Aspose.PDF dla .NET

Otwórz folder projektu w terminalu i uruchom:

```bash
dotnet add package Aspose.PDF
```

Pakiet zawiera przestrzeń nazw `Aspose.Pdf`, która dostarcza wszystkie klasy użyte w tym tutorialu. Po instalacji odśwież projekt, aby IDE wykryło nową referencję.

## Krok 2: Wczytaj dokument PDF

Wczytanie pliku źródłowego jest pierwszą operacją, ponieważ silnik numeracji Bates działa na istniejącej instancji `Document`.

```csharp
using Aspose.Pdf;

// ...

// Replace with the path to your input PDF
string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Load the PDF document into memory
Document doc = new Document(inputPath);
```

**Dlaczego to ważne:** Klasa `Document` analizuje strukturę PDF, dając dostęp do stron, adnotacji i metadanych. Bez wczytania pliku nie możesz zastosować żadnej numeracji.

## Krok 3: Skonfiguruj opcje numeracji Bates

Utwórz obiekt `BatesNumberingOptions` i ustaw żądany prefiks, numer początkowy oraz opcjonalne parametry formatowania.

```csharp
using Aspose.Pdf;

// ...

BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Text that appears before the numeric part
    Prefix = "CASE01",

    // First number to use (1 means the first page gets CASE01-1)
    StartNumber = 1,

    // Optional: customize the appearance
    // The default places the number in the footer, centered.
    // You can change Font, FontSize, Color, and Position if needed.
    // Example:
    // Font = FontRepository.FindFont("Arial"),
    // FontSize = 10,
    // Color = Color.Black,
    // Margin = new Margin(0, 0, 0, 20)
};
```

**Dlaczego to ważne:** `BatesNumberingOptions` informuje Aspose.PDF, jak generować etykietę dla każdej strony. `Prefix` pomaga grupować powiązane sprawy, a `StartNumber` umożliwia kontynuację sekwencji z poprzedniej partii.

## Krok 4: Zapisz PDF z zastosowaną numeracją Bates

Przekaż obiekt opcji do metody `Save`. Aspose.PDF zapisuje numery bezpośrednio na każdej stronie.

```csharp
// Replace with the desired output path
string outputPath = @"YOUR_DIRECTORY\output.pdf";

// Save the document, applying the Bates numbering
doc.Save(outputPath, batesOptions);
```

**Dlaczego to ważne:** Przeciążenie `Save(string, BatesNumberingOptions)` łączy krok renderowania z procesem numeracji, zapewniając, że plik wyjściowy zawiera widoczne identyfikatory.

## Pełny przykład – wszystko razem

Poniżej znajduje się pojedynczy, samodzielny program, który możesz skopiować, wkleić i uruchomić. Demonstracja **jak dodać numerację Bates** od początku do końca.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the PDF document
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Set up Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                Prefix = "CASE01",
                StartNumber = 1,
                // Optional appearance tweaks:
                // Font = FontRepository.FindFont("Times New Roman"),
                // FontSize = 9,
                // Color = Color.DarkBlue,
                // Margin = new Margin(0, 0, 0, 15)
            };

            // 3️⃣ Save the document with Bates numbers
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath, batesOptions);

            Console.WriteLine($"Bates numbering added. Output saved to: {outputPath}");
        }
    }
}
```

### Oczekiwany wynik

Uruchomienie programu tworzy plik `output.pdf`, w którym każda strona wyświetla etykietę podobną do:

```
CASE01-1
CASE01-2
CASE01-3
...
```

Numery pojawiają się domyślnie w stopce, ale możesz je przenieść, dostosowując właściwość `Margin` w `BatesNumberingOptions`.

## Przypadki brzegowe i typowe wariacje

| Sytuacja | Co należy dostosować |
|-----------|----------------------|
| **Inny prefiks dla każdej partii** | Zmieniaj `Prefix` przed wywołaniem `Save`. Możesz iterować po wielu dokumentach z różnymi prefiksami. |
| **Kontynuacja numeracji z poprzedniego pliku** | Ustaw `StartNumber` na ostatnio użyty numer + 1. |
| **Umieszczenie numerów w nagłówku** | Użyj `batesOptions.Margin = new Margin(20, 0, 0, 0);` (margines górny) lub dostosuj `batesOptions.Position`. |
| **Niestandardowa czcionka lub kolor** | Przypisz właściwości `Font`, `FontSize` i `Color`, jak pokazano w sekcji komentarzy. |
| **Duże PDF‑y (1000+ stron)** | Operacja jest pamięcio‑oszczędna; jednak możesz wywołać `doc.OptimizeResources()` przed zapisem, aby zmniejszyć rozmiar pliku. |

**Porada:** Jeśli Twój przepływ pracy wymaga różnych schematów numeracji dla poszczególnych dokumentów, wydziel logikę do metody pomocniczej:

```csharp
static void ApplyBatesNumbering(string src, string dst, string prefix, int start)
{
    var doc = new Document(src);
    var opts = new BatesNumberingOptions { Prefix = prefix, StartNumber = start };
    doc.Save(dst, opts);
}
```

## Podsumowanie

Teraz wiesz **jak dodać numerację Bates** do dowolnego PDF przy użyciu Aspose.PDF w C#. Tutorial obejmował wczytywanie dokumentu PDF, konfigurowanie opcji numeracji oraz zapisywanie finalnego pliku — wszystko w jednym, wykonywalnym programie.  

Od tego momentu możesz zgłębiać tematy pokrewne, takie jak **dodawanie znaków wodnych**, **scalanie wielu PDF‑ów** czy **wyodrębnianie tekstu** przy pomocy Aspose.PDF. Eksperymentuj z różnymi czcionkami, kolorami i pozycjami, aby dopasować formatowanie do standardów Twojej organizacji.

Gotowy, aby zautomatyzować przepływ pracy dokumentów prawnych? Dodaj kod do swojego pipeline’u budowania, uruchom go na partiach plików i pozwól Aspose.PDF wykonać ciężką pracę. Powodzenia w kodowaniu!


## Co powinieneś nauczyć się dalej?


Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne przykłady kodu oraz wyjaśnienia krok po kroku, pomagające opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Create PDF Document C# – Add Bates Numbering](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/)
- [Add Bates Numbering PDF – Step‑by‑Step Guide to Number PDF Pages](/pdf/english/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/)
- [Aspose PDF Tutorial – Insert a Blank Page and Update Bates Numbering](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}