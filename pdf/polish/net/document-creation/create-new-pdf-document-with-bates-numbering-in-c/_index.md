---
category: general
date: 2026-08-04
description: Utwórz nowy dokument PDF w C# i szybko dodaj numerację Bates przy użyciu
  Aspose.Pdf – dowiedz się, jak dodać pustą stronę PDF i niestandardowe numery stron.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new pdf document
- add bates numbering pdf
- how to add bates
- add blank page pdf
- add custom page numbers
language: pl
lastmod: 2026-08-04
og_description: Utwórz nowy dokument PDF w C# i automatycznie dodaj numerację Bates
  do PDF w zarządzaniu sprawami prawnymi – pełny przykład kodu w zestawie.
og_image_alt: Screenshot of a C# program creating a PDF document with Bates numbers
  applied
og_title: Utwórz nowy dokument PDF z numeracją Bates w C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create new PDF document in C# and add Bates numbering pdf quickly using
    Aspose.Pdf – learn to add blank page pdf and custom page numbers.
  headline: Create new PDF document with Bates numbering in C#
  type: TechArticle
tags:
- C#
- PDF
- Aspose.Pdf
- Bates numbering
title: Utwórz nowy dokument PDF z numeracją Batesa w C#
url: /pl/net/document-creation/create-new-pdf-document-with-bates-numbering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz nowy dokument PDF z numeracją Bates w C#

Jeśli potrzebujesz **utworzyć nowy dokument PDF** w C#, ten przewodnik pokaże Ci, jak **dodać numerację Bates do PDF** przy użyciu Aspose.Pdf. Nauczysz się **dodać pustą stronę PDF**, skonfigurować **dodawanie własnych numerów stron** i zapisać ostateczny plik.

Samouczek obejmuje każdy krok, od instalacji biblioteki po generowanie PDF spełniającego standardy dokumentacji prawnej. Po zakończeniu będziesz w stanie wygenerować PDF, wstawić pustą stronę, zastosować numery Bates oraz dostosować format numeracji — wszystko w jednym, uruchamialnym programie.

## Wymagania wstępne

Zanim zaczniesz, upewnij się, że masz:

* .NET 6.0 SDK lub nowszy zainstalowany  
* Visual Studio 2022 (lub dowolne IDE C#)  
* Aktywna licencja Aspose.Pdf dla .NET lub darmowy klucz ewaluacyjny  

Nie potrzebujesz żadnych dodatkowych pakietów NuGet; samouczek instaluje wszystko automatycznie.

## Krok 1: Zainstaluj Aspose.Pdf przez NuGet

Otwórz terminal w folderze projektu i uruchom:

```bash
dotnet add package Aspose.Pdf
```

Polecenie dodaje najnowszą stabilną wersję Aspose.Pdf do Twojego projektu, udostępniając klasy `Document`, `BatesNumbering` i inne klasy do manipulacji PDF, których będziesz używać.

## Krok 2: Utwórz nowy dokument PDF – wstępna konfiguracja

Tworzenie pliku PDF jest podstawą każdej późniejszej operacji. Klasa `Document` reprezentuje cały kontener PDF.

```csharp
using Aspose.Pdf;

// Step 2: Create a new PDF document
using var doc = new Document();
```

*Dlaczego to ważne*: Tworzenie instancji `Document` alokuje wewnętrzne struktury potrzebne dla stron, czcionek i grafiki. Użycie `using var` zapewnia prawidłowe zwolnienie zasobów pliku po zapisaniu.

## Krok 3: Dodaj pustą stronę PDF

PDF musi zawierać co najmniej jedną stronę, zanim będziesz mógł umieścić na niej treść. Dodanie pustej strony zapewnia czyste płótno dla numeracji Bates.

```csharp
// Step 3: Add a blank page to the document
Page page = doc.Pages.Add();
```

`Metoda Pages.Add()` dodaje nową, pustą stronę na końcu kolekcji stron dokumentu. Możesz powtórzyć to wywołanie, aby dodać więcej stron, jeśli później będziesz potrzebował **dodać własne numery stron** na wielu stronach.

## Krok 4: Skonfiguruj numerację Bates – jak dodać Bates

Numeracja Bates to kolejny identyfikator powszechnie używany w dokumentach prawnych. Konfigurujesz go za pomocą klasy `BatesNumbering`.

```csharp
// Step 4: Set up Bates numbering options
var bates = new BatesNumbering
{
    StartNumber = 1000,      // Starting number for the sequence
    Prefix = "CaseA-",       // Text to prepend to each number
    Increment = 1,           // Increment between consecutive numbers
    // Optional: Set the location, font size, etc.
};
```

*Dlaczego to ważne*: `StartNumber` określa pierwszą liczbę, `Prefix` dodaje czytelną etykietę, a `Increment` kontroluje wielkość kroku. Możesz także dostosować `HorizontalAlignment`, `VerticalAlignment`, `FontSize` i `Margins`, aby kontrolować wygląd numeru na każdej stronie.

## Krok 5: Zastosuj numerację Bates do strony PDF

Gdy opcje numeracji są gotowe, zastosuj je do strony (lub do całego dokumentu).

```csharp
// Step 5: Apply the Bates numbering to the page
bates.Apply(page);
```

Wywołanie `Apply` wstawia sformatowany numer domyślnie do stopki strony. Jeśli potrzebujesz numeru w innym miejscu, ustaw `bates.Position` przed wywołaniem `Apply`.

## Krok 6: Zapisz PDF z zastosowaną numeracją Bates

Na koniec zapisz dokument w pamięci do dysku.

```csharp
// Step 6: Save the PDF with Bates numbers applied
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumbered.pdf");

doc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

Zapisany plik zawiera teraz jedną stronę z numerem Bates **CaseA-1000** wyświetlonym na dole. Otwórz PDF w dowolnym przeglądarce, aby zweryfikować numerację.

## Oczekiwany wynik

Po otwarciu `BatesNumbered.pdf` powinieneś zobaczyć:

* Jedną pustą stronę (lub więcej, jeśli dodałeś dodatkowe strony)  
* Tekst **CaseA-1000** umieszczony na dole strony (domyślna lokalizacja)  

Jeśli dodasz więcej stron i ponownie użyjesz tej samej instancji `BatesNumbering`, numery będą automatycznie zwiększane (CaseA-1001, CaseA-1002, …).

## Porada: Dodawanie własnych numerów stron oprócz numeracji Bates

Czasami potrzebujesz zarówno numeracji Bates, jak i tradycyjnych numerów stron. Możesz je połączyć, dodając `TextFragment` po zastosowaniu numeracji Bates:

```csharp
// Add a traditional page number in the header
var pageNumber = new TextFragment($"Page {page.Number}")
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Top,
    FontSize = 12,
    Font = FontRepository.FindFont("Arial")
};
page.Paragraphs.Add(pageNumber);
```

Ten fragment kodu demonstruje **dodawanie własnych numerów stron** przy zachowaniu etykiety Bates.

## Przypadek brzegowy: Zastosowanie numeracji Bates do wielu stron

Jeśli Twój dokument zawiera kilka stron, możesz zastosować tę samą instancję `BatesNumbering` do każdej strony w pętli:

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    bates.Apply(doc.Pages[i]);
}
```

Pętla zapewnia, że każda strona otrzymuje kolejny numer na podstawie zdefiniowanego `StartNumber` i `Increment`.

## Częste pułapki i jak ich unikać

| Problem | Dlaczego się pojawia | Rozwiązanie |
|-------|----------------|-----|
| Numery pojawiają się nieśrodkowo | Domyślne wyrównanie może nie pasować do Twojego układu | Ustaw `bates.HorizontalAlignment` i `bates.VerticalAlignment` explicite |
| Numery nakładają się na istniejącą treść | Nie zdefiniowano marginesu | Dostosuj `bates.Margin` lub użyj `bates.Position`, aby przesunąć numer |
| Wyjątek licencyjny w czasie wykonywania | Wersja ewaluacyjna ogranicza wyjście | Zastosuj ważną licencję Aspose.Pdf przed utworzeniem dokumentu (`License license = new License(); license.SetLicense("Aspose.Pdf.lic");`) |

## Pełny działający przykład

Poniżej znajduje się samodzielny program, który możesz skopiować, wkleić i uruchomić.

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1. Create a new PDF document
        using var doc = new Document();

        // 2. Add a blank page pdf
        Page page = doc.Pages.Add();

        // 3. Configure Bates numbering – how to add bates
        var bates = new BatesNumbering
        {
            StartNumber = 1000,
            Prefix = "CaseA-",
            Increment = 1,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(20, 20, 20, 20),
            FontSize =


## Co powinieneś się nauczyć dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak dodać i dostosować numery stron w PDF przy użyciu Aspose.PDF dla .NET | Przewodnik po manipulacji dokumentami](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF .NET: Dodaj numery stron do PDF przy użyciu FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Utwórz dokument PDF przy użyciu Aspose.PDF – Dodaj stronę, kształt i zapisz](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}