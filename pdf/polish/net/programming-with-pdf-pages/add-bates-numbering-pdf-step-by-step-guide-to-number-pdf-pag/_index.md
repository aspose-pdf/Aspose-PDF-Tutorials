---
category: general
date: 2026-03-03
description: Szybko dodaj numerację Batesa do PDF i dowiedz się, jak numerować strony
  PDF lub dodać kolejno numerowane strony PDF przy użyciu Aspose.Pdf w C#.
draft: false
keywords:
- add bates numbering pdf
- number pdf pages
- add sequential pdf numbers
- pdf bates numbering tutorial
- aspnet pdf automation
language: pl
og_description: Dodaj numerację Bates w PDF w C#, aby numerować strony PDF i dodać
  kolejno numery PDF. Pełny kod, wyjaśnienia i najlepsze praktyki.
og_title: Dodaj numerację Bates do PDF – Kompletny samouczek C#
tags:
- PDF
- C#
- Aspose.Pdf
- Document Automation
title: Dodaj numerację Bates w PDF – Przewodnik krok po kroku, jak numerować strony
  PDF
url: /pl/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodawanie numeracji Bates w PDF – Kompletny samouczek C#

Kiedykolwiek potrzebowałeś **add bates numbering pdf** plików, ale nie wiedziałeś, od czego zacząć? Nie jesteś jedyny — zespoły prawne, audytorzy i archiwiści borykają się z tym samym problemem. Dobra wiadomość? Kilka linijek C# i biblioteka Aspose.Pdf pozwalają automatycznie **number pdf pages**, a dodatkowo zyskujesz elastyczność **add sequential pdf numbers** z własnymi prefiksami, sufiksami i położeniem.

W tym przewodniku przeprowadzimy Cię przez rzeczywisty przykład, wyjaśnimy, dlaczego każde ustawienie ma znaczenie, oraz pokażemy, jak dostosować kod do przypadków brzegowych, takich jak różne rozmiary stron czy niestandardowa liczba cyfr. Po zakończeniu będziesz mieć gotowy do uruchomienia fragment kodu, który dodaje numery Bates do dowolnego PDF, oraz zrozumiesz „dlaczego” stojące za każdą opcją.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.6+)
- Ważna licencja Aspose.Pdf for .NET (lub darmowy klucz ewaluacyjny)
- Visual Studio 2022 (lub dowolny edytor C#, którego używasz)
- Źródłowy PDF o nazwie `source.pdf` w folderze, do którego możesz odwołać się

To wszystko — nie potrzebujesz dodatkowych pakietów NuGet poza Aspose.Pdf.

## Krok 1 – Otwórz źródłowy dokument PDF

Pierwszą rzeczą, którą musisz zrobić, jest załadowanie PDF, który chcesz otoczyć znacznikiem. Użycie bloku `using` zapewnia prawidłowe zwolnienie uchwytu pliku, co zapobiega problemom z blokowaniem później.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the original PDF
using (var pdfDocument = new Document(@"C:\MyDocs\source.pdf"))
{
    // The rest of the steps will go inside this block.
}
```

> **Dlaczego to ważne:** Otwieranie dokumentu wewnątrz instrukcji `using` zapewnia deterministyczne zwolnienie zasobów. Jeśli to pominiesz, plik może pozostać zablokowany, a kolejne próby zapisania lub usunięcia PDF‑a zakończą się niepowodzeniem — co widziałem, że powoduje problemy w środowiskach produkcyjnych.

## Krok 2 – Skonfiguruj opcje numeracji Bates

Teraz informujemy Aspose, jak mają wyglądać numery Bates. Każda właściwość mapuje się bezpośrednio na element wizualny na stronie.

```csharp
// Step 2: Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    Prefix = "2025-",               // Text before the number
    Suffix = "-A",                  // Text after the number
    Start = 5000,                   // First number in the sequence
    NumberOfDigits = 5,             // Pads with leading zeros (e.g., 05000)
    Placement = BatesNumberPlacement.BottomRight // Where the number appears
};
```

### Szybkie wskazówki dotyczące opcji

| Property | What it does | When to change it |
|----------|--------------|-------------------|
| **Prefix / Suffix** | Dodaje stały tekst przed/po części numerycznej. | Użyj identyfikatora sprawy, kodu projektu lub „CONF‑” dla dokumentów poufnych. |
| **Start** | Pierwszy numer w serii. | Jeśli kontynuujesz schemat numeracji z poprzedniej partii, ustaw odpowiednio tę wartość. |
| **NumberOfDigits** | Kontroluje wypełnianie zerami. | W dokumentach prawnych często potrzebne jest dokładnie 6 cyfr; ustaw na `6`. |
| **Placement** | BottomRight, BottomLeft, TopRight, TopLeft, Center. | Wybierz w zależności od układu dokumentu; BottomRight jest najczęściej używany dla numerów Bates. |

> **Pro tip:** Jeśli potrzebujesz **number pdf pages** w kilku kolumnach, możesz wywołać `pdfDocument.AddBatesNumbering` dwa razy z różnymi wartościami `Placement` i odrębnymi ciągami `Prefix`.

## Krok 3 – Zastosuj numerację Bates do dokumentu

Gdy opcje są gotowe, faktyczne nanoszenie numeracji odbywa się jednym wywołaniem metody. Aspose wewnętrznie obsługuje paginację, rotację i obliczenia marginesów.

```csharp
// Step 3: Apply the numbering to every page
pdfDocument.AddBatesNumbering(batesOptions);
```

> **Dlaczego jedno wywołanie działa:** W tle Aspose iteruje po `pdfDocument.Pages`, tworzy `TextFragment` dla każdej strony i pozycjonuje go zgodnie z wybranym `Placement`. Ta abstrakcja oszczędza Ci pisania ręcznej pętli i radzenia sobie z przekształceniami współrzędnych.

## Krok 4 – Zapisz zaktualizowany PDF

Na koniec zapisz zmodyfikowany plik na dysku. Możesz nadpisać oryginał lub utworzyć nowy plik; poniższy przykład tworzy świeżą kopię.

```csharp
// Step 4: Persist the changes
pdfDocument.Save(@"C:\MyDocs\bates_numbered.pdf");
```

Jeśli potrzebujesz **add sequential pdf numbers** do strumienia (np. przy wysyłaniu pliku przez API), zamień ścieżkę pliku na `MemoryStream`:

```csharp
using var output = new MemoryStream();
pdfDocument.Save(output);
output.Position = 0; // Reset for downstream consumption
```

## Pełny działający przykład

Łącząc wszystko razem, oto kompletny, gotowy do uruchomienia program:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Open the source PDF
        using (var pdfDocument = new Document(@"C:\MyDocs\source.pdf"))
        {
            // Configure Bates numbering
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "2025-",
                Suffix = "-A",
                Start = 5000,
                NumberOfDigits = 5,
                Placement = BatesNumberPlacement.BottomRight
            };

            // Apply the numbering
            pdfDocument.AddBatesNumbering(batesOptions);

            // Save the result
            pdfDocument.Save(@"C:\MyDocs\bates_numbered.pdf");
        }

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

### Oczekiwany wynik

- Nowy plik `bates_numbered.pdf` pojawia się w `C:\MyDocs`.
- Każda strona wyświetla coś w stylu `2025-05000-A`, `2025-05001-A`, … w prawym dolnym rogu.
- Liczby są wypełnione zerami do pięciu cyfr, zgodnie z ustawieniem `NumberOfDigits`.

## Obsługa typowych wariantów

### 1. Różne rozmiary stron

Jeśli Twój PDF zawiera zarówno strony w orientacji pionowej, jak i poziome, możesz zauważyć, że numer jest obcięty po szerszej stronie. Aby to naprawić, włącz właściwość `AutoFit`:

```csharp
batesOptions.AutoFit = true; // Adjusts font size to fit within page margins
```

### 2. Niestandardowa czcionka lub kolor

Domyślnie numery Bates są czarne, 12‑pt Times New Roman. Zmień wygląd, uzyskując dostęp do `TextState`:

```csharp
batesOptions.TextState = new TextState
{
    FontSize = 10,
    Font = FontRepository.FindFont("Courier New"),
    ForegroundColor = Color.GetBlue()
};
```

### 3. Pomijanie stron

Załóżmy, że chcesz **number pdf pages**, ale pominąć stronę tytułową. Użyj zakresu stron:

```csharp
pdfDocument.AddBatesNumbering(batesOptions, new PageNumbering { Start = 2 });
```

### 4. Dodawanie wielu schematów numeracji

Zespoły prawne czasami wymagają zarówno numeru Bates, jak i poufnego znaku wodnego. Uruchom dwa oddzielne wywołania `AddBatesNumbering` z różnymi wartościami `Placement`:

```csharp
// First scheme – bottom right
pdfDocument.AddBatesNumbering(batesOptions);

// Second scheme – top left, different prefix
var confidentialOptions = new BatesNumberingOptions
{
    Prefix = "CONF-",
    Start = 1,
    NumberOfDigits = 4,
    Placement = BatesNumberPlacement.TopLeft,
    TextState = new TextState { FontSize = 8, ForegroundColor = Color.GetRed() }
};
pdfDocument.AddBatesNumbering(confidentialOptions);
```

## Najczęściej zadawane pytania

**Q: Czy to działa z PDF‑ami, które już zawierają istniejący tekst?**  
A: Tak. Aspose dodaje numer Bates jako osobną warstwę, więc istniejąca treść pozostaje nienaruszona. Jeśli potrzebujesz, aby numery pojawiały się *za* istniejącym tekstem (rzadko), musiałbyś ręcznie manipulować strumieniami zawartości strony.

**Q: Co zrobić, jeśli PDF jest chroniony hasłem?**  
A: Najpierw załaduj go z hasłem: `new Document(path, new LoadOptions { Password = "secret" })`. Po naniesieniu numeracji możesz ponownie zastosować szyfrowanie za pomocą `pdfDocument.Encrypt(...)`.

**Q: Czy mogę używać tego w aplikacji konsolowej .NET Core?**  
A: Oczywiście. Ten sam kod działa w .NET Core, .NET 5+ i .NET Framework. Wystarczy odwołać się do odpowiedniego pakietu NuGet Aspose.Pdf.

## Podsumowanie

Właśnie omówiliśmy, jak **add bates numbering pdf** pliki, jak **number pdf pages**, oraz jak **add sequential pdf numbers** z pełną kontrolą nad formatowaniem, położeniem i obsługą przypadków brzegowych. Krótki fragment kodu powyżej wykonuje najcięższą pracę, a dodatkowe opcje pozwalają dostosować rozwiązanie do dowolnego przepływu pracy prawnego, archiwizacyjnego lub zgodnościowego.

Gotowy na kolejny krok? Spróbuj połączyć to podejście z:

- **Batch processing** – iteruj po folderze PDF‑ów i zastosuj ten sam schemat numeracji.
- **Dynamic prefixes** – pobieraj identyfikatory spraw z bazy danych i wstawiaj je do każdego dokumentu.
- **PDF/A compliance** – po numeracji wywołaj `pdfDocument.Convert(..., PdfFormat.PdfA2b)`, aby zapewnić długoterminową archiwizację.

Śmiało eksperymentuj, podziel się swoimi odkryciami lub zadawaj pytania w komentarzach. Szczęśliwego kodowania i niech Twoje PDF‑y zawsze będą idealnie zindeksowane! 

![Screenshot of a PDF page with Bates numbers in the bottom‑right corner](https://example.com/images/bates-numbered.png "add bates numbering pdf example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}