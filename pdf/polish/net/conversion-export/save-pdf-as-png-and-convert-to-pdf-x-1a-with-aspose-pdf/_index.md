---
category: general
date: 2026-02-09
description: Zapisz PDF jako PNG w C# przy użyciu Aspose PDF, następnie wyeksportuj
  PDF do HTML, dodaj znak wodny w postaci stempla PDF i dowiedz się, jak konwertować
  PDFX‑1a dla konwersji PDF w ASP.NET.
draft: false
keywords:
- save pdf as png
- export pdf to html
- add watermark stamp pdf
- how to convert pdfx-1a
- asp.net pdf conversion
language: pl
og_description: Zapisz PDF jako PNG w C# przy użyciu Aspose PDF, następnie wyeksportuj
  PDF do HTML, dodaj znak wodny (stempel) PDF i dowiedz się, jak konwertować PDFX‑1a
  dla konwersji PDF w ASP.NET.
og_title: Zapisz PDF jako PNG i konwertuj do PDF/X‑1a za pomocą Aspose PDF
tags:
- aspnet
- pdf
- csharp
title: Zapisz PDF jako PNG i konwertuj do PDF/X‑1a za pomocą Aspose PDF
url: /pl/net/conversion-export/save-pdf-as-png-and-convert-to-pdf-x-1a-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zapisz PDF jako PNG i konwertuj do PDF/X‑1a przy użyciu Aspose PDF

Zastanawiałeś się kiedyś, jak **save PDF as PNG** bez utraty włosów? Nie jesteś jedyny — programiści ciągle pytają o szybki sposób na rasteryzację strony przy jednoczesnym zachowaniu oryginalnego PDF. W tym przewodniku przejdziemy dokładnie przez to, a także pokażemy, jak **export PDF to HTML**, dodać **watermark stamp PDF**, i nawet **convert PDFX‑1a** dla solidnego **ASP.NET PDF conversion** pipeline.

Co otrzymasz po przeczytaniu tego tutorialu, to jednoplikowy program w C#, gotowy do kopiowania i wklejania, który wczytuje PDF, konwertuje go do pliku zgodnego z PDF/X‑1a, renderuje pierwszą stronę jako PNG, dodaje dynamiczny znak tekstowy i na końcu generuje wersję HTML zachowującą kodowanie czcionek. Bez niejasnych odniesień, tylko konkretny kod i „dlaczego” za każdą linijką.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również na .NET Framework 4.7+)
- Pakiet NuGet Aspose.Pdf for .NET (`Install-Package Aspose.Pdf`)
- Plik profilu ICC (`profile.icc`), jeśli potrzebna jest zgodność z PDF/X‑1a
- Źródłowy PDF (`input.pdf`), który chcesz przekształcić

To wszystko — żadnych dodatkowych bibliotek, żadnych ukrytych kroków. Jeśli masz te elementy, możesz zaczynać.

## Krok 1: Wczytaj źródłowy dokument PDF

Zanim będziemy mogli cokolwiek zrobić, musimy wczytać PDF do pamięci.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Devices;

// Load the PDF you’ll be working with
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

**Dlaczego to ważne:** `Document` jest podstawowym obiektem; daje dostęp do stron, czcionek i metadanych. Wczytanie go raz sprawia, że reszta pipeline’u jest szybka.

## Krok 2: Konwertuj do PDF/X‑1a (Jak konwertować PDFX‑1a)

PDF/X‑1a jest standardem de‑facto dla plików gotowych do druku. Konwersja zapewnia, że wszystkie czcionki są osadzone, a kolory zdefiniowane.

```csharp
// Set up conversion options for PDF/X‑1a
PdfFormatConversionOptions conversionOptions = new PdfFormatConversionOptions(
    PdfFormat.PDF_X_1A,               // Target format
    ConvertErrorAction.Delete)       // What to do on errors
{
    IccProfileFileName = "YOUR_DIRECTORY/profile.icc", // External ICC profile
    OutputIntent = new OutputIntent("FOGRA39")        // Output intent for printing
};

// Perform the conversion
pdfDocument.Convert(conversionOptions);
```

**Pro tip:** Jeśli pominiesz profil ICC, Aspose osadzi domyślny, ale użycie dokładnego profilu, którego oczekuje drukarnia, zapobiega nieprzyjemnym przesunięciom kolorów.

## Krok 3: Zapisz plik zgodny z PDF/X‑1a

Teraz, gdy dokument spełnia specyfikację PDF/X‑1a, zapisujemy go.

```csharp
pdfDocument.Save("YOUR_DIRECTORY/pdfx1a.pdf");
```

Zauważysz, że rozmiar pliku może wzrosnąć — dodatkowe zasoby są osadzane, co jest dokładnie tym, czego potrzebujesz dla niezawodnego wydruku.

## Krok 4: Renderuj pierwszą stronę do PNG (Zapisz PDF jako PNG)

Tutaj główne słowo kluczowe błyszczy: **save PDF as PNG** dla miniatur lub wyświetlania w sieci.

```csharp
// Configure PNG device with font analysis (helps with text extraction later)
PngDevice pngDevice = new PngDevice
{
    RenderingOptions = new RenderingOptions { AnalyzeFonts = true }
};

// Render only the first page
pngDevice.Process(pdfDocument.Pages[1], "YOUR_DIRECTORY/page1.png");
```

![Przykład zapisu PDF jako PNG](https://example.com/images/save-pdf-as-png.png "Przykład strony PDF zapisanej jako PNG")

Flaga `AnalyzeFonts` instruuje Aspose, aby osadził informacje o czcionkach w metadanych PNG, przydatny trik, jeśli później potrzebujesz odnieść się do oryginalnego tekstu.

## Krok 5: Dodaj znak wodny Watermark Stamp PDF

Dodanie **watermark stamp PDF** jest trywialne przy użyciu `TextStamp` Aspose. Sprawimy, że znak będzie automatycznie dopasowywany do prostokąta.

```csharp
// Create a text stamp that auto‑adjusts its font size
TextStamp textStamp = new TextStamp("Important notice")
{
    AutoAdjustFontSizeToFitStampRectangle = true,
    AutoAdjustFontSizePrecision = 0.01f,
    Width = 400,               // Width of the stamp rectangle
    Height = 200,              // Height of the stamp rectangle
    WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords
};

// Place the stamp on the first page
pdfDocument.Pages[1].AddStamp(textStamp);
```

**Dlaczego auto‑adjust?** Różne strony mają różną gęstość; pozwolenie API na obliczenie optymalnego rozmiaru czcionki gwarantuje, że tekst nigdy nie wyjdzie poza prostokąt.

## Krok 6: Zapisz oznaczony PDF

Po dodaniu znaku zapisujemy zmiany.

```csharp
pdfDocument.Save("YOUR_DIRECTORY/stamped.pdf");
```

Otwórz `stamped.pdf` w dowolnym przeglądarce i zobaczysz pole „Important notice” ładnie wyśrodkowane — bez ręcznej ingerencji.

## Krok 7: Eksportuj PDF do HTML (Export PDF to HTML)

Na koniec **export PDF to HTML** z preferowaniem CMap dla kodowania czcionek. To zapewnia, że generowany HTML używa Unicode wszędzie tam, gdzie to możliwe, utrzymując tekst przeszukiwalny.

```csharp
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    FontEncodingStrategy = HtmlSaveOptions.FontEncodingRules.DecreaseToUnicodePriorityLevel
};

// Save the HTML representation
pdfDocument.Save("YOUR_DIRECTORY/cmap.html", htmlOptions);
```

Wynikowy `cmap.html` zawiera elementy `<canvas>` dla złożonej grafiki oraz odpowiednie znaczniki `<span>` dla tekstu, co czyni go gotowym do SEO‑przyjaznych stron internetowych.

## Pełny działający przykład

Poniżej pełny program, który możesz wkleić do aplikacji konsolowej. Wystarczy podmienić ścieżki zastępcze i gotowe.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Devices;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Convert to PDF/X‑1a (how to convert pdfx‑1a)
        PdfFormatConversionOptions conversionOptions = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_1A,
            ConvertErrorAction.Delete)
        {
            IccProfileFileName = "YOUR_DIRECTORY/profile.icc",
            OutputIntent = new OutputIntent("FOGRA39")
        };
        pdfDocument.Convert(conversionOptions);

        // 3️⃣ Save the PDF/X‑1a file
        pdfDocument.Save("YOUR_DIRECTORY/pdfx1a.pdf");

        // 4️⃣ Render first page as PNG (save pdf as png)
        PngDevice pngDevice = new PngDevice
        {
            RenderingOptions = new RenderingOptions { AnalyzeFonts = true }
        };
        pngDevice.Process(pdfDocument.Pages[1], "YOUR_DIRECTORY/page1.png");

        // 5️⃣ Add a dynamic watermark stamp (add watermark stamp pdf)
        TextStamp textStamp = new TextStamp("Important notice")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            AutoAdjustFontSizePrecision = 0.01f,
            Width = 400,
            Height = 200,
            WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords
        };
        pdfDocument.Pages[1].AddStamp(textStamp);

        // 6️⃣ Save the stamped PDF
        pdfDocument.Save("YOUR_DIRECTORY/stamped.pdf");

        // 7️⃣ Export to HTML (export pdf to html)
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            FontEncodingStrategy = HtmlSaveOptions.FontEncodingRules.DecreaseToUnicodePriorityLevel
        };
        pdfDocument.Save("YOUR_DIRECTORY/cmap.html", htmlOptions);

        Console.WriteLine("All operations completed successfully.");
    }
}
```

**Oczekiwany wynik**

- `pdfx1a.pdf` – plik gotowy do druku PDF/X‑1a
- `page1.png` – rasterowy obraz pierwszej strony (idealny do miniatur)
- `stamped.pdf` – oryginalny PDF z skalowalnym znakiem wodnym „Important notice”
- `cmap.html` – przyjazna dla sieci wersja HTML z czcionkami Unicode

## Częste pytania i przypadki brzegowe

- **Co jeśli źródłowy PDF ma zaszyfrowane strony?**  
  Wczytaj go z hasłem: `new Document("input.pdf", new LoadOptions { Password = "secret" })`.

- **Czy potrzebuję profilu ICC przy każdej konwersji?**  
  Niekoniecznie — Aspose użyje domyślnego profilu, ale dla ścisłej zgodności z PDF/X‑1a powinieneś dostarczyć dokładny profil używany przez drukarnię.

- **Czy mogę renderować więcej niż jedną stronę do PNG?**  
  Oczywiście. Przejdź pętlą po `pdfDocument.Pages` i wywołaj `pngDevice.Process(page, $"page{page.Number}.png")`.

- **Czy wyjściowy HTML jest przyjazny dla urządzeń mobilnych?**  
  Generowany HTML używa responsywnych elementów `<canvas>`. Jeśli potrzebujesz czystego tekstu opartego na CSS, ustaw `htmlOptions.SplitIntoPages = false` i dostosuj `htmlOptions.PartsEmbeddingMode`.

## Wskazówki dla konwersji PDF w ASP.NET

Gdy integrujesz ten kod w kontrolerze ASP.NET Core, pamiętaj o:

1. **Strumieniuj wynik** zamiast zapisywać na dysk — użyj `MemoryStream` i zwróć `FileResult`.
2. **Zwalniaj** (`Dispose`) obiekty `Document` i urządzenia przy pomocy `using

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}