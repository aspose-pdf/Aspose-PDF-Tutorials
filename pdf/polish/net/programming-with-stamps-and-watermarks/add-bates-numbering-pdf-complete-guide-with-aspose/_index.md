---
category: general
date: 2026-06-08
description: Dodaj numerację Batesa w pliku PDF przy użyciu Aspose.Pdf w C#. Dowiedz
  się, jak dodać numerację Batesa, dodać numery stron w PDF, dodać numery sekwencyjne
  w PDF oraz zobacz przykład numeru Batesa w PDF.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add page numbers pdf
- add sequential numbers pdf
- bates number pdf example
language: pl
og_description: Dodaj numerację Bates w PDF w C#. Ten poradnik pokazuje, jak dodać
  numerację Bates, dodać numery stron w PDF oraz dodać kolejne numery w PDF, wraz
  z pełnym przykładem numeracji Bates w PDF.
og_title: Dodaj numerację Bates w PDF – Kompletny przewodnik z Aspose
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. Learn how to add bates,
    add page numbers pdf, add sequential numbers pdf, and see a bates number pdf example.
  headline: Add Bates Numbering PDF – Complete Guide with Aspose
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. Learn how to add bates,
    add page numbers pdf, add sequential numbers pdf, and see a bates number pdf example.
  name: Add Bates Numbering PDF – Complete Guide with Aspose
  steps:
  - name: Install the Aspose.Pdf NuGet Package
    text: 'First, add the library to your project. Open the Package Manager Console
      and run:'
  - name: Open the Source PDF Document
    text: Now we load the PDF we want to stamp. The `using` statement ensures the
      file is closed properly even if an exception occurs.
  - name: Create a Bates Numbering Facade
    text: 'The *facade* pattern hides the complexity of the underlying PDF structure.
      Here’s how we instantiate it:'
  - name: Configure the Starting Number and Prefix
    text: Bates numbers often include a case‑specific prefix. You can also control
      the number of digits, the separator, and the placement on the page.
  - name: Apply the Bates Numbering to the Document
    text: 'With the facade configured, we now stamp every page:'
  - name: Save the Modified PDF
    text: 'Finally, write the output to disk:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF processing
title: Dodaj numerację Bates w PDF – Kompletny przewodnik z Aspose
url: /pl/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-guide-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodaj numerację Bates w PDF – Kompletny przewodnik programistyczny

Kiedykolwiek potrzebowałeś **add bates numbering pdf**, ale nie wiedziałeś od czego zacząć? Jeśli kiedykolwiek zastanawiałeś się *jak dodać bates* do dokumentu prawnego, jesteś we właściwym miejscu. W tym samouczku przeprowadzimy Cię przez praktyczny, kompleksowy przykład, który nie tylko dodaje numery Bates, ale także pokazuje, jak **add page numbers pdf**, **add sequential numbers pdf**, a nawet dostarcza gotowy do uruchomienia **bates number pdf example**.

Użyjemy biblioteki Aspose.Pdf dla .NET, ponieważ ukrywa ona niskopoziomowe szczegóły PDF, jednocześnie dając precyzyjną kontrolę. Po zakończeniu tego przewodnika będziesz miał ponownie używalny fragment kodu, który możesz wkleić do dowolnego projektu C#, i zrozumiesz, dlaczego każda linijka ma znaczenie.

## Czego będziesz potrzebować

- **.NET 6.0** lub nowszy (kod działa również na .NET Framework 4.6+).  
- **Licencja** na Aspose.Pdf lub darmowy tymczasowy klucz ewaluacyjny.  
- Przykładowy PDF o nazwie `input.pdf` umieszczony w folderze, do którego możesz odwołać się w kodzie.  
- Visual Studio, Rider lub dowolny edytor C#, którego używasz.

To wszystko — żadnych dodatkowych narzędzi, żadnych skomplikowanych poleceń w wierszu. Gotowy? Zanurzmy się.

## Dodaj numerację Bates w PDF – Implementacja krok po kroku

Poniżej dzielimy proces na sześć logicznych kroków. Każdy krok zawiera krótki fragment kodu, wyjaśnienie *dlaczego* to robimy oraz wskazówkę, która może się przydać.

### Krok 1: Zainstaluj pakiet NuGet Aspose.Pdf

Najpierw dodaj bibliotekę do swojego projektu. Otwórz konsolę Package Manager i uruchom:

```powershell
Install-Package Aspose.Pdf
```

> **Porada:** Jeśli pracujesz na .NET Core, możesz także użyć `dotnet add package Aspose.Pdf`.

Instalacja pakietu daje dostęp do klasy `Aspose.Pdf.Facades.BatesNumbering`, która jest sercem **add bates numbering pdf**.

### Krok 2: Otwórz źródłowy dokument PDF

Teraz wczytujemy PDF, który chcemy otoczyć pieczątką. Instrukcja `using` zapewnia, że plik zostanie zamknięty prawidłowo, nawet w przypadku wystąpienia wyjątku.

```csharp
using (var doc = new Aspose.Pdf.Document(@"C:\MyPdfs\input.pdf"))
{
    // All further steps happen inside this block.
}
```

Dlaczego używamy `Aspose.Pdf.Document`? Reprezentuje on cały PDF w pamięci, umożliwiając manipulację stronami, czcionkami i metadanymi bez modyfikacji oryginalnego pliku na dysku.

### Krok 3: Utwórz fasadę Bates Numbering

Wzorzec *fasady* ukrywa złożoność wewnętrznej struktury PDF. Oto jak ją tworzymy:

```csharp
var bates = new Aspose.Pdf.Facades.BatesNumbering();
```

Ten obiekt zostanie później skonfigurowany z prefiksem, numerem początkowym i opcjami formatowania. Traktuj go jako „silnik”, który **add page numbers pdf** w sposób zgodny z Bates.

### Krok 4: Skonfiguruj numer początkowy i prefiks

Numery Bates często zawierają specyficzny dla sprawy prefiks. Możesz także kontrolować liczbę cyfr, separator oraz położenie na stronie.

```csharp
bates.StartNumber = 1000;          // First number in the sequence
bates.Prefix = "CASE-";            // Prefix that appears before each number
bates.NumberOfDigits = 5;          // Pads numbers with leading zeros (e.g., 01000)
bates.Separator = "-";             // Optional separator between prefix and number
bates.Location = new Aspose.Pdf.Rectangle(0, 0, 200, 20); // Bottom‑left corner
bates.FontSize = 12;
bates.FontColor = System.Drawing.Color.Blue;
```

**Dlaczego te ustawienia?**  
- `StartNumber` pozwala kontynuować poprzednią serię.  
- `NumberOfDigits` zapewnia jednolitą długość, co jest kluczowe przy indeksacji prawnej.  
- `Location` definiuje, gdzie pojawi się **add sequential numbers pdf**; możesz przenieść go w prawy górny róg, jeśli wolisz.

### Krok 5: Zastosuj numerację Bates do dokumentu

Po skonfigurowaniu fasady, nakładamy pieczątkę na każdą stronę:

```csharp
bates.AddBatesNumbering(doc);
```

W tle Aspose iteruje po każdej stronie, rysuje tekst w określonym miejscu i respektuje istniejącą zawartość. Ta pojedyncza linijka to właśnie to, co **add bates numbering pdf** w Twoim pliku.

### Krok 6: Zapisz zmodyfikowany PDF

Na koniec zapisujemy wynik na dysku:

```csharp
doc.Save(@"C:\MyPdfs\output.pdf");
```

Masz teraz PDF, w którym każda strona posiada unikalny identyfikator Bates, gotowy do przeglądu lub złożenia w sądzie.

#### Pełny działający przykład (Przykład numeracji Bates w PDF)

Łącząc wszystko razem, oto kompletny, samodzielny program, który możesz skompilować i uruchomić:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using (var doc = new Document(@"C:\MyPdfs\input.pdf"))
        {
            // 2️⃣ Create the Bates numbering facade
            var bates = new BatesNumbering();

            // 3️⃣ Configure prefix, start number, and formatting
            bates.StartNumber = 1000;
            bates.Prefix = "CASE-";
            bates.NumberOfDigits = 5;
            bates.Separator = "-";
            bates.Location = new Rectangle(0, 0, 200, 20); // Bottom‑left
            bates.FontSize = 12;
            bates.FontColor = Color.Blue;

            // 4️⃣ Apply the numbering to every page
            bates.AddBatesNumbering(doc);

            // 5️⃣ Save the result
            doc.Save(@"C:\MyPdfs\output.pdf");
        }

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

> **Oczekiwany wynik:** Otwórz `output.pdf`, a zobaczysz „CASE‑01000”, „CASE‑01001”, … w lewym dolnym rogu każdej strony.

![Screenshot of a PDF page with Bates numbers at the bottom-left corner – add bates numbering pdf example](https://example.com/bates-numbering-screenshot.png "add bates numbering pdf example")

*(Tekst alternatywny obrazu: *add bates numbering pdf example* – pokazuje zastosowane numery Bates w przykładowym PDF.)*

## Jak dodać Bates – Zrozumienie fasady

Możesz się zastanawiać, **how to add bates** bez fasady Aspose. Alternatywą jest ręczne rysowanie tekstu na każdej stronie przy użyciu niskopoziomowych operatorów PDF, ale takie podejście jest podatne na błędy i wymaga dogłębnej znajomości specyfikacji PDF. Fasada ukrywa te szczegóły, pozwalając skupić się na *co* chcesz (prefiks, numer początkowy), a nie na *jak* to renderować.

Jeśli kiedykolwiek będziesz musiał **add page numbers pdf** w stylu innym niż Bates (np. „Strona 3 z 12”), możesz ponownie użyć klasy `BatesNumbering` — po prostu ustaw `Prefix` na pusty ciąg i dostosuj `Location`. Silnik pod spodem jest ten sam, co oznacza spójne renderowanie w obu przypadkach.

## Dodaj numery stron w PDF – Dostosowanie położenia i stylu

Zespoły prawne często żądają numeru strony w nagłówku, podczas gdy personel wsparcia litigiacyjnego woli go w stopce. Oto szybka modyfikacja:

```csharp
bates.Location = new Rectangle(0, doc.Pages[1].PageInfo.Height - 20, 200, 20); // Top‑right
bates.Prefix = "";               // No prefix for plain page numbers
bates.StartNumber = 1;           // Start from 1
bates.NumberOfDigits = 0;        // No padding
bates.FontColor = Color.Black;
```

To samo wywołanie `AddBatesNumbering` teraz **add page numbers pdf** na górze każdej strony. Ponieważ fasada działa na obiekcie dokumentu, możesz przełączać się między numeracją Bates a zwykłą numeracją stron za pomocą kilku zmian właściwości — bez potrzeby przepisywania pętli.

## Dodaj numery sekwencyjne w PDF – Zaawansowane formatowanie

Załóżmy, że potrzebujesz formatu takiego jak `2023-CASE-00123`. Możesz połączyć prefiks daty z istniejącymi ustawieniami:

```csharp
bates.Prefix = $"{DateTime.Now:yyyy}-CASE-";
bates.NumberOfDigits = 5;
bates.Separator = "-";
```

Teraz każda strona będzie wyświetlać `2023-CASE-00123`, `2023-CASE-00124`, itd. To pokazuje, jak łatwo możesz **add sequential numbers pdf**, spełniając skomplikowane konwencje nazewnictwa.

## Przypadki brzegowe i typowe pułapki

| Sytuacja | Na co zwrócić uwagę | Sugerowane rozwiązanie |
|-----------|----------------------|---------------|
| **Bardzo duże pliki PDF ( > 500 MB )** | Zużycie pamięci może gwałtownie wzrosnąć, ponieważ cały dokument jest ładowany do RAM. | Użyj `Document` z ustawieniami `MemoryManagement` lub przetwarzaj plik w częściach przy pomocy `PdfFileEditor`. |
| **Existing page numbers** |  |  |

## Co powinieneś nauczyć się dalej?

Kolejne samouczki dotyczą ściśle powiązanych tematów, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne przykłady kodu oraz wyjaśnienia krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Jak dodać i dostosować numery stron w PDF przy użyciu Aspose.PDF dla .NET | Przewodnik po manipulacji dokumentami](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Jak dodać pieczątki numerów stron w PDF przy użyciu Aspose.PDF dla .NET | Znaki wodne i tła](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [Aspose.PDF .NET: Dodaj numery stron do PDF przy użyciu FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}