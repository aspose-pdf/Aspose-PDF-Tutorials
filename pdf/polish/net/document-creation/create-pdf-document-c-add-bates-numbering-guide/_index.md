---
category: general
date: 2026-02-28
description: Utwórz dokument PDF w C# z numeracją Batesa. Dowiedz się, jak dodać numerację
  Batesa do PDF, ustawić prefiksy i wygenerować kolejno numery PDF w jednym przewodniku.
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add document identification numbers
- add sequential pdf numbers
language: pl
og_description: Utwórz dokument PDF w C# z numeracją Batesa. Ten samouczek pokazuje,
  jak dodać numerację Batesa do PDF, ustawić własne prefiksy i generować kolejno numerowane
  pliki PDF.
og_title: Tworzenie dokumentu PDF w C# – Dodaj numerację Batesa
tags:
- Aspose.PDF
- C#
- PDF automation
title: Tworzenie dokumentu PDF w C# – Przewodnik dodawania numeracji Batesa
url: /pl/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie dokumentu PDF C# – Przewodnik po dodawaniu numeracji Batesa

Zastanawiałeś się kiedyś, jak **tworzyć dokument PDF w C#**, który już posiada unikalny identyfikator na każdej stronie? To powszechny problem, gdy trzeba śledzić pliki prawne, dokumenty sądowe lub dowolną partię PDF‑ów, które muszą być przeszukiwalne po numerze. Dobra wiadomość? Dzięki Aspose.PDF możesz dodać numery Batesa w kilku linijkach kodu — bez ręcznej edycji.

W tym przewodniku przeprowadzimy Cię przez cały proces: wczytanie istniejącego PDF, skonfigurowanie **add bates numbering pdf**, zastosowanie numerów i ostateczne zapisanie wyniku. Po zakończeniu będziesz w stanie **add document identification numbers** i nawet **add sequential PDF numbers** automatycznie, wszystko w C#.

## Wymagania wstępne

- .NET 6.0 lub nowszy (API działa również z .NET Framework 4.5+)
- Licencjonowana kopia **Aspose.PDF for .NET** (bezpłatna wersja próbna działa do testów)
- Plik PDF wejściowy, który chcesz ponumerować (nazwijmy go `input.pdf`)
- Visual Studio 2022 (lub dowolne preferowane IDE)

Nie są potrzebne dodatkowe pakiety NuGet poza Aspose.PDF.

![Utwórz dokument PDF C# z numeracją Batesa](https://example.com/image.png "Przykład tworzenia dokumentu PDF C#")

## Krok 1: Wczytaj źródłowy dokument PDF

Zanim będziesz mógł **add bates numbering pdf**, potrzebujesz obiektu `Document`, który reprezentuje plik na dysku.

```csharp
using Aspose.Pdf;

// Load the source PDF document
var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*Dlaczego to ważne*: Klasa `Document` jest punktem wejścia dla każdej operacji w Aspose.PDF. Abstrahuje system plików, dzięki czemu możesz pracować ze stronami, adnotacjami i metadanymi, nie dotykając surowych bajtów.

> **Wskazówka:** Jeśli przetwarzasz wiele plików w pętli, ponownie używaj tej samej instancji `Document` tylko wtedy, gdy źródło jest identyczne; w przeciwnym razie twórz nowy obiekt dla każdego pliku, aby uniknąć wycieków pamięci.

## Krok 2: Zdefiniuj opcje numeracji Batesa

Tutaj część **how to add bates** staje się konkretna. Konfigurujesz obiekt `BatesNumberingOptions`, aby powiedzieć Aspose, jaki ma być prefiks, od którego numeru rozpocząć i jak duża ma być czcionka.

```csharp
// Define Bates numbering options (prefix, start number, font size)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",   // You can change this to any string you need
    Start = 1000,      // Starting number – useful for continuous numbering across batches
    FontSize = 9       // Small enough to fit in the margin but still readable
};
```

*Dlaczego to ważne*: `Prefix` pozwala wstawić identyfikator sprawy (np. „ABC-”). Właściwość `Start` jest niezbędna, gdy **adding sequential PDF numbers** w wielu dokumentach — po prostu zwiększaj ją. A `FontSize` zapewnia, że liczby nie zasłaniają istniejącej treści.

## Krok 3: Zastosuj numerację Batesa do całego dokumentu

Teraz faktycznie nanosimy numery na każdą stronę. Klasa `BatesNumbering` wykonuje całą ciężką pracę.

```csharp
// Apply Bates numbering to the entire document
var bates = new BatesNumbering();
bates.AddBatesNumbering(pdfDocument, batesOptions);
```

*Dlaczego to ważne*: „Pod maską” Aspose przechodzi przez każdą stronę, oblicza odpowiedni numer (Prefiks + (Start + indeksStrony)) i rysuje go domyślnie w prawym dolnym rogu. Pozycję można później dostosować, ale domyślne ustawienie działa w większości dokumentów w stylu prawniczym.

> **Częste pytanie:** *Co zrobić, jeśli muszę ponumerować tylko podzbiór stron?*  
> Użyj przeciążenia `AddBatesNumbering(Document, BatesNumberingOptions, int startPage, int endPage)`, aby ograniczyć zakres.

## Krok 4: Zapisz PDF z zastosowaną numeracją Batesa

Ostatni krok to zapisanie zmodyfikowanego dokumentu z powrotem na dysk.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*Dlaczego to ważne*: Metoda `Save` zachowuje oryginalny format pliku, więc otrzymujesz standardowy PDF, który może otworzyć każdy przeglądarka — wraz z **add document identification numbers** na każdej stronie.

## Pełny działający przykład

Łącząc wszystko razem, oto samodzielny program, który możesz wkleić do nowej aplikacji konsolowej i od razu uruchomić.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF document
            var inputPath = @"YOUR_DIRECTORY/input.pdf";
            var pdfDocument = new Document(inputPath);

            // 2️⃣ Define Bates numbering options (prefix, start number, font size)
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                FontSize = 9
            };

            // 3️⃣ Apply Bates numbering to the entire document
            var bates = new BatesNumbering();
            bates.AddBatesNumbering(pdfDocument, batesOptions);

            // 4️⃣ Save the PDF with Bates numbers applied
            var outputPath = @"YOUR_DIRECTORY/output.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbering added successfully. Output saved to {outputPath}");
        }
    }
}
```

**Oczekiwany rezultat:** Otwórz `output.pdf` w dowolnym podglądzie; zobaczysz „ABC‑1000”, „ABC‑1001”, … wydrukowane w prawym dolnym rogu każdej strony. Liczby są tekstem zaznaczalnym, więc są przeszukiwalne i można je kopiować — dokładnie to, czego oczekujesz od prawidłowej implementacji **add sequential PDF numbers**.

## Przypadki brzegowe i warianty

### Niestandardowe pozycjonowanie

Jeśli domyślny róg koliduje z istniejącymi stopkami, możesz przesunąć położenie:

```csharp
batesOptions.Position = new Position(10, 10); // X, Y from the bottom‑left
```

### Różne formaty numerów

Chcesz liczby wypełnione zerami (np. 001000)? Użyj `NumberFormat`:

```csharp
batesOptions.NumberFormat = "D6"; // Pads to 6 digits
```

### Wiele plików w partii

Podczas przetwarzania wielu PDF‑ów utrzymuj licznik bieżący:

```csharp
int globalStart = 5000;
foreach (var file in Directory.GetFiles(@"YOUR_DIRECTORY\Batch", "*.pdf"))
{
    var doc = new Document(file);
    var opts = new BatesNumberingOptions
    {
        Prefix = "BATCH-",
        Start = globalStart,
        FontSize = 9
    };
    new BatesNumbering().AddBatesNumbering(doc, opts);
    doc.Save(Path.ChangeExtension(file, ".bated.pdf"));
    globalStart += doc.Pages.Count; // Increment for the next file
}
```

### Obsługa PDF‑ów zabezpieczonych hasłem

Jeśli źródłowy PDF jest zaszyfrowany, przekaż hasło przy tworzeniu obiektu `Document`:

```csharp
var pdfDocument = new Document("protected.pdf", new LoadOptions { Password = "mySecret" });
```

## Najczęściej zadawane pytania

| Pytanie | Odpowiedź |
|----------|--------|
| **Czy mogę użyć innej biblioteki?** | Tak, biblioteki takie jak iTextSharp lub PdfSharp również obsługują wstawianie tekstu na poziomie strony, ale Aspose.PDF oferuje najprostsze API do numeracji Batesa. |
| **Czy to wpływa na rozmiar pliku?** | Dodanie kilku bajtów tekstu na stronę jest nieznaczne; rozmiar wyjściowy zazwyczaj rośnie o mniej niż 1 KB na stronę. |
| **Czy numeracja jest przeszukiwalna?** | Zdecydowanie. Aspose zapisuje numery jako obiekty tekstowe, a nie jako obrazy, więc są indeksowane przez czytniki PDF. |
| **Co zrobić, jeśli potrzebuję innej czcionki?** | Ustaw `batesOptions.Font` na obiekt `Font` (np. `FontRepository.FindFont("Arial")`). |

## Zakończenie

Właśnie pokazaliśmy, jak **create PDF document C#** i natychmiast **add bates numbering pdf** przy użyciu Aspose.PDF. Proces jest prosty, niezawodny i w pełni programowalny — idealny dla kancelarii prawnych, agencji rządowych lub każdej organizacji, która musi **add document identification numbers** i **add sequential PDF numbers** do dużych partii plików.

Weź tę bazę i eksperymentuj: wypróbuj różne prefiksy dla różnych działów, łańcuchuj numerację przez wiele plików lub osadzaj kody QR obok numerów Batesa dla dodatkowej identyfikowalności. Nie ma granic, gdy masz już opanowany podstawowy przepływ pracy.

Jeśli ten poradnik okazał się przydatny, udostępnij go, zostaw komentarz lub zapoznaj się z innymi naszymi przewodnikami o manipulacji PDF w C#. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}