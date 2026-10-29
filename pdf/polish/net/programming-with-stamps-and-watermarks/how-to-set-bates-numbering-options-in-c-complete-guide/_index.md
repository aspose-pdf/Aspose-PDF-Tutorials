---
category: general
date: 2026-08-14
description: Jak ustawić opcje numeracji Batesa w C# przy użyciu GroupDocs. Postępuj
  zgodnie z tym samouczkiem krok po kroku, aby dodać własne prefiksy i numery początkowe
  podczas konwersji Worda do PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set bates numbering options
- Bates numbering C#
- GroupDocs API
- document conversion C#
- AddBatesNumbering method
- C# PDF generation
language: pl
lastmod: 2026-08-14
og_description: Jak szybko ustawić opcje numeracji Bates w C#. Ten przewodnik pokazuje,
  jak dodać własne prefiksy i numery początkowe przy konwertowaniu Worda na PDF.
og_image_alt: Screenshot of C# code applying Bates numbering to a PDF
og_title: Jak ustawić opcje numeracji Bates w C# – samouczek krok po kroku
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  headline: How to set bates numbering options in C# – complete guide
  type: TechArticle
- description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  name: How to set bates numbering options in C# – complete guide
  steps:
  - name: '`Document` – loads the source file.'
    text: '`Document` – loads the source file.'
  - name: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
    text: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
  - name: '`AddBatesNumbering` – the method that injects the numbering into each page.'
    text: '`AddBatesNumbering` – the method that injects the numbering into each page.'
  type: HowTo
tags:
- Bates numbering
- C#
- .NET
- GroupDocs
- PDF conversion
title: Jak ustawić opcje numeracji Bates w C# – kompletny przewodnik
url: /pl/net/programming-with-stamps-and-watermarks/how-to-set-bates-numbering-options-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak ustawić opcje numeracji Bates w C# – kompletny przewodnik

Jeśli potrzebujesz **jak ustawić opcje numeracji Bates** w C#, ten przewodnik poprowadzi Cię krok po kroku. Dowiesz się, jak skonfigurować numer początkowy, dodać prefiks i zastosować numerację podczas konwertowania dokumentu Word na PDF przy użyciu GroupDocs API.

Przetwarzanie dokumentów często wymaga unikalnych identyfikatorów na każdej stronie w celach prawnych lub archiwalnych. Po zakończeniu tego samouczka będziesz mieć fragment kodu, który możesz wstawić do dowolnego projektu .NET, niezależnie od tego, czy tworzysz narzędzie wsparcia procesowego, czy automatyczny generator raportów. Nie są potrzebne żadne zewnętrzne narzędzia – wystarczy biblioteka GroupDocs.Conversion i kilka linii C#.

## Czego będziesz potrzebować

* .NET 6.0 SDK lub nowszy zainstalowany  
* Visual Studio 2022 (lub dowolne IDE obsługujące .NET)  
* Ważna licencja GroupDocs.Conversion (bezpłatna wersja próbna działa do testów)  
* Przykładowy dokument Word (`input.docx`), który chcesz ponumerować  

Te wymagania wstępne zapewniają, że kod uruchomi się bez dodatkowej konfiguracji.

## Jak ustawić opcje numeracji Bates – przegląd

Podstawą **jak ustawić opcje numeracji Bates** są trzy obiekty:

1. `Document` – ładuje plik źródłowy.  
2. `BatesNumberingOptions` – przechowuje numer początkowy, prefiks i inne szczegóły formatowania.  
3. `AddBatesNumbering` – metoda, która wstawia numerację na każdej stronie.  

Zrozumienie, dlaczego każdy element istnieje, pomaga dostosować rozwiązanie do bardziej złożonych scenariuszy, takich jak własne czcionki czy numeracja wielojęzyczna.

## Krok 1: Zainstaluj pakiet NuGet GroupDocs.Conversion

Otwórz terminal w folderze rozwiązania i uruchom:

```bash
dotnet add package GroupDocs.Conversion
```

**GroupDocs API** udostępnia klasę `Document` oraz metodę rozszerzającą `AddBatesNumbering` używaną później w samouczku.

## Krok 2: Załaduj dokument źródłowy

```csharp
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;

// Step 2: Load the source Word document
Document document = new Document(@"C:\Docs\input.docx");
```

*Dlaczego ten krok?*  
Ładowanie pliku tworzy reprezentację w pamięci, którą silnik konwersji może manipulować. Bez instancji `Document` nie możesz zastosować numeracji Bates ani żadnej innej transformacji.

## Krok 3: Utwórz opcje numeracji Bates

```csharp
// Step 3: Configure Bates numbering
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // The first page will be numbered 1000
    StartNumber = 1000,
    // Each page will be prefixed with "CASE-"
    Prefix = "CASE-",
    // Optional: set the number format (e.g., 4 digits)
    NumberFormat = "#0000",
    // Optional: choose where the number appears (header/footer)
    Position = BatesNumberingPosition.FooterRight
};
```

*Dlaczego ten krok?*  
`BatesNumberingOptions` kapsułkuje wszystkie ustawienia, które mogą być potrzebne przy **ustawianiu opcji numeracji Bates**. Dostosowanie `StartNumber` i `Prefix` pozwala dopasować wynik do systemu zarządzania sprawami. Właściwość `Position` kontroluje położenie wizualne, co często jest wymogiem zgodności.

## Krok 4: Zastosuj numerację Bates w dokumencie

```csharp
// Step 4: Apply the numbering to every page
document.AddBatesNumbering(batesOptions);
```

Metoda `AddBatesNumbering` przechodzi przez każdą stronę załadowanego `Document` i wstawia skonfigurowany ciąg znaków. Ponieważ metoda działa na reprezentacji w pamięci, możesz łańcuchowo dodawać kolejne kroki przetwarzania (np. znak wodny) przed zapisaniem.

## Krok 5: Konwertuj i zapisz wynik jako PDF

```csharp
// Step 5: Define PDF conversion options (optional)
PdfConvertOptions pdfOptions = new PdfConvertOptions
{
    // Preserve original layout
    EmbedStandardFonts = true
};

// Save the numbered document as PDF
document.Save(@"C:\Docs\output.pdf", pdfOptions);
```

*Dlaczego ten krok?*  
Zapisywanie jako PDF jest powszechnym formatem końcowym dla dokumentów prawnych. Obiekt `PdfConvertOptions` pozwala precyzyjnie dostroić wyjście, ale nie jest wymagany do podstawowej numeracji. Wywołanie `Save` zapisuje w pełni ponumerowany PDF na dysku.

## Pełny, działający przykład

Łącząc wszystko razem, oto samodzielna aplikacja konsolowa, którą możesz skompilować i uruchomić:

```csharp
using System;
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;
using GroupDocs.Conversion.Options.Convert.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the source Word document
            Document document = new Document(@"C:\Docs\input.docx");

            // Configure Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1000,
                Prefix = "CASE-",
                NumberFormat = "#0000",
                Position = BatesNumberingPosition.FooterRight
            };

            // Apply numbering to each page
            document.AddBatesNumbering(batesOptions);

            // Optional: set PDF conversion preferences
            PdfConvertOptions pdfOptions = new PdfConvertOptions
            {
                EmbedStandardFonts = true
            };

            // Save the numbered PDF
            document.Save(@"C:\Docs\output.pdf", pdfOptions);

            Console.WriteLine("Bates numbering applied successfully. Output saved to output.pdf");
        }
    }
}
```

**Oczekiwany wynik**

Uruchomienie programu tworzy `output.pdf`, w którym każda strona wyświetla etykietę taką jak `CASE-1000`, `CASE-1001` itd., umieszczoną w prawym stopce. Otwórz PDF w dowolnym przeglądarce, aby zweryfikować, że liczby pojawiają się zgodnie z zamierzeniami.

## Częste pułapki i najlepsze praktyki

| Problem | Dlaczego się pojawia | Jak tego uniknąć |
|-------|----------------|-----------------|
| **Ścieżki względne powodują `FileNotFoundException`** | Katalog roboczy aplikacji konsolowej może różnić się od tego w Visual Studio. | Używaj ścieżek bezwzględnych lub `Path.Combine(AppContext.BaseDirectory, "input.docx")`. |
| **Numeracja zachodzi na istniejące stopki** | Jeśli dokument źródłowy już zawiera treść w wybranym obszarze stopki, nowy numer może być ukryty. | Wybierz inną `Position` (np. `HeaderLeft`) lub dostosuj szablon źródłowy. |
| **Duże dokumenty działają wolno** | Numeracja Bates iteruje po każdej stronie; zużycie pamięci rośnie wraz z rozmiarem pliku. | Przetwarzaj dokument w partiach używając `Document.Split`, jeśli przekraczasz 500 stron. |
| **Wygaśnięcie licencji** | Bezpłatna wersja próbna GroupDocs wygasa po 30 dniach, powodując wyjątek przy `AddBatesNumbering`. | Zastosuj ważny klucz licencyjny przed załadowaniem dokumentu: `License license = new License(); license.SetLicense("license.lic");`. |

**Wskazówka:** Jeśli potrzebujesz innego formatu numeru dla każdej sprawy (np. `2023-CASE-001`), zbuduj prefiks dynamicznie przed utworzeniem `BatesNumberingOptions`.

## Rozszerzanie rozwiązania

To samo **Bates numbering C#** podejście działa z innymi formatami źródłowymi, takimi jak `.txt`, `.html` czy nawet obrazy. Wystarczy zmienić rozszerzenie pliku przy konstruowaniu obiektu `Document`, a silnik konwersji zajmie się resztą.

Możesz także połączyć **document conversion C#** z OCR dla zeskanowanych PDF‑ów:

```csharp
// Example: add OCR before numbering (requires GroupDocs.Viewer)
using GroupDocs.Viewer;
using GroupDocs.Viewer.Options;

Document scannedPdf = new Document(@"C:\Docs\scanned.pdf");
var viewer = new Viewer(scannedPdf);
var viewOptions = new HtmlViewOptions();
viewer.View(viewOptions); // OCR step
// Then apply Bates numbering as shown earlier
```

## Zakończenie

Teraz wiesz **jak ustawić opcje numeracji Bates** w C# od początku do końca. Tworząc obiekt `BatesNumberingOptions`, stosując go za pomocą `AddBatesNumbering` i zapisując wynik jako PDF, możesz zautomatyzować produkcję dokumentów spełniających wymogi prawne i posiadających unikalne identyfikatory.  

Od tego momentu możesz zgłębiać powiązane tematy, takie jak **C# PDF generation**, **document conversion C#**, czy zaawansowane funkcje **GroupDocs API**, np. znakowanie wodne i podpisy cyfrowe. Eksperymentuj z różnymi prefiksami, pozycjami i formatami numerów, aby dopasować je do swojego przepływu pracy.

Miłego kodowania!

## Co warto się nauczyć dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu oraz wyjaśnienia krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Dodaj numerację Bates PDF w C# – kompletny przewodnik](/pdf/english/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/)
- [Jak dodać i dostosować numery stron w PDF‑ach przy użyciu Aspose.PDF dla .NET | Przewodnik po manipulacji dokumentami](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Jak dodać stopkę z tekstowym znakiem wodnym w PDF‑ach przy użyciu Aspose.PDF dla .NET: przewodnik krok po kroku](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}