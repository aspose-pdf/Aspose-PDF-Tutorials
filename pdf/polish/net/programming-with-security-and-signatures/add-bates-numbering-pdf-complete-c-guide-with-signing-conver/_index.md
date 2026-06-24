---
category: general
date: 2026-06-21
description: Dodaj numerację Bates do PDF i dowiedz się, jak dodać numery Bates, konwertować
  PDF do PDF/X‑4, konwertować PDF do PDF/A‑4 oraz cyfrowo podpisać PDF w C# w jednym
  przewodniku.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbers
- digitally sign pdf c#
- convert pdf to pdf/x-4
- convert pdf to pdfa-4
language: pl
og_description: Dodaj numerację Bates do PDF, zobacz, jak dodać numery Bates, konwertuj
  PDF do PDF/X-4, konwertuj PDF do PDF/A-4 i cyfrowo podpisz PDF w C# przy użyciu
  Aspose.Pdf.
og_title: Dodaj numerację Bates do PDF – Samouczek C# krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add bates numbering pdf and learn how to add bates numbers, convert
    pdf to pdf/x-4, convert pdf to pdfa-4, and digitally sign pdf c# in a single walkthrough.
  headline: Add Bates Numbering PDF – Complete C# Guide with Signing & Conversion
  type: TechArticle
- questions:
  - answer: Yes. Use `BatesNumberingOptions` properties such as `Location` and `FontSize`
      to fine‑tune placement.
    question: Can I change the position of the Bates numbers?
  - answer: Switch `PdfFormat.PDF_X_4` to `PdfFormat.PDFA_4` in the conversion options.
      That satisfies the **convert pdf to pdfa-4** requirement.
    question: What if I need PDF/A‑4 instead of PDF/X‑4?
  - answer: Absolutely. Replace `DigestHashAlgorithm.Sha384` with `DigestHashAlgorithm.Sha256`
      (or any supported algorithm).
    question: My certificate uses a different hash algorithm—can I use SHA‑256?
  - answer: 'Not strictly. In this flow we save after conversion and after Bates numbering
      to give you intermediate files. You could defer saving until the end if you
      prefer a single write operation. ## Wrap‑Up We’ve just demonstrated a practical,
      end‑to‑end solution that **add bates numbering pdf**, explains **'
    question: Do I need to call `document.Save` after each step?
  type: FAQPage
tags:
- Aspose.Pdf
- C#
- PDF processing
- Bates numbering
title: Dodaj numerację Bates do PDF – Kompletny przewodnik C# z podpisywaniem i konwersją
url: /pl/net/programming-with-security-and-signatures/add-bates-numbering-pdf-complete-c-guide-with-signing-conver/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dodawanie numeracji Bates do PDF – Kompletny przewodnik C# z podpisywaniem i konwersją

Zastanawiałeś się kiedyś, **jak dodać numerację Bates do PDF**, nie tracąc przy tym włosów? Nie jesteś sam. Zespoły prawne, audytorzy i wszyscy, którzy potrzebują dokumentów z możliwością śledzenia, nieustannie pytają *jak dodać numerację Bates* do PDF, a potem wymagają, aby plik spełniał standardy PDF/X‑4 lub PDF/A‑4 oraz był cyfrowo podpisany.  

W tym tutorialu przejdziemy krok po kroku przez to właśnie – używając Aspose.Pdf dla .NET **dodamy numerację Bates do PDF**, pokażemy **jak dodać numerację Bates**, **przekonwertujemy PDF na PDF/X‑4**, **przekonwertujemy PDF na PDF/A‑4**, a na końcu **cyfrowo podpiszemy PDF w C#**. Po zakończeniu będziesz mieć gotowy program, który generuje trzy dopracowane pliki PDF: wersję PDF/X‑4, wersję z numeracją Bates oraz wersję cyfrowo podpisaną.

![przykład dodawania numeracji bates do pdf](image-placeholder.png "Zrzut ekranu pokazujący dodawanie numeracji bates do pdf w praktyce")

## Co będzie potrzebne

- **.NET 6+** (lub .NET Framework 4.6+). Aspose.Pdf obsługuje oba.
- **Ważna licencja Aspose.Pdf dla .NET** (lub wersja ewaluacyjna – wówczas pojawią się znaki wodne).
- **Plik certyfikatu PKCS#7** (`.pfx`) oraz jego hasło do podpisywania.
- **Przykładowy PDF**, który chcesz przetworzyć (umieść go w folderze, do którego masz dostęp).
- Visual Studio, Rider lub dowolne IDE dla C#.

To wszystko – nie potrzebujesz dodatkowych pakietów NuGet poza `Aspose.Pdf`. Jeśli jeszcze nie dodałeś biblioteki, uruchom:

```bash
dotnet add package Aspose.Pdf
```

Teraz przejdźmy do kodu.

## Krok 1: Załaduj źródłowy dokument PDF

Najpierw musimy wczytać oryginalny plik do pamięci. To podstawa dla wszystkich kolejnych operacji.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

// Load the source PDF – adjust the path to your environment
var document = new Document("YOUR_DIRECTORY/sample.pdf");
```

> **Dlaczego to ważne:** Ładowanie PDF tworzy obiekt `Document`, który reprezentuje cały plik i daje dostęp do API konwersji, pól formularzy oraz zabezpieczeń.

## Krok 2: Konwersja PDF do PDF/X‑4 (zgodność z PDF/A‑4)

Jeśli Twój proces wymaga jakości archiwalnej, PDF/X‑4 (podzbiór PDF/A‑4) jest właściwym wyborem. Oto jak **przekonwertować pdf na pdf/x-4** przy użyciu Aspose.

```csharp
// Set conversion options – PDF/X‑4 is the target format
var conversionOptions = new PdfFormatConversionOptions(PdfFormat.PDF_X_4, ConvertErrorAction.Delete);

// Perform the conversion
document.Convert(conversionOptions);
```

> **Wskazówka:** Flaga `ConvertErrorAction.Delete` usuwa wszelką zawartość, która mogłaby naruszyć zgodność, zapewniając czysty wynik PDF/X‑4.

## Krok 3: Zapisz wersję PDF/X‑4

Po zapewnieniu zgodności z PDF/X‑4 zapisujemy dokument na dysku.

```csharp
document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");
```

Masz teraz plik kompatybilny z **konwersją pdf na pdfa-4** (PDF/X‑4 jest członkiem rodziny PDF/A‑4). Możesz otworzyć go w Acrobat, aby zweryfikować znacznik zgodności.

## Krok 4: Dodaj numerację Bates – sedno „Dodawania numeracji Bates do PDF”

Numeracja Bates to kolejny identyfikator umieszczany na każdej stronie. To dokładna odpowiedź na pytanie *jak dodać numerację Bates* programowo.

```csharp
// Configure Bates numbering options
var batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",   // Optional prefix
    Start = 5000        // Starting number
};

// Apply Bates numbering to the document
document.AddBatesNumbering(batesOptions);
```

> **Dlaczego to działa:** `AddBatesNumbering` przechodzi przez każdą stronę i nakłada numer w domyślnej lokalizacji (prawy dolny róg). Po potrzebie możesz zmienić pozycję za pomocą `BatesNumberingOptions`.

## Krok 5: Zapisz PDF z numeracją Bates

Po **dodaniu numeracji bates do pdf** potrzebujemy osobnego pliku, który zachowa numery.

```csharp
document.Save("YOUR_DIRECTORY/sample_bates.pdf");
```

Otwórz plik; powinieneś zobaczyć „CASE‑5000”, „CASE‑5001” i tak dalej na dole każdej strony.

## Krok 6: Cyfrowe podpisanie PDF – „Cyfrowe podpisanie PDF C#” w praktyce

Podpis cyfrowy zapewnia autentyczność i integralność. Poniżej **cyfrowo podpiszemy pdf w c#** używając skrótu SHA‑384.

```csharp
// Prepare the signature handler
var signature = new PdfFileSignature(document);

// Load the PKCS#7 certificate (adjust password)
var pkcs7 = new PKCS7Detached(
    "YOUR_DIRECTORY/mycert.pfx", // Path to .pfx
    "pwd",                       // Certificate password
    DigestHashAlgorithm.Sha384   // Strong hashing algorithm
);

// Sign page 1, place signature rectangle at (100,100)-(200,150)
signature.Sign(
    pageNumber: 1,
    signatureAppearance: true,
    rectangle: new Rectangle(100, 100, 200, 150),
    pkcs7: pkcs7
);
```

> **Pro tip:** `Rectangle` definiuje, gdzie pojawi się widoczny podpis. Jeśli nie potrzebujesz wizualnego wskaźnika, ustaw `signatureAppearance` na `false`.

## Krok 7: Zapisz cyfrowo podpisany PDF

Na koniec zapisujemy podpisany dokument na dysku.

```csharp
signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
```

Masz teraz plik **cyfrowo podpisany pdf c#**, który może być zweryfikowany w dowolnym czytniku PDF obsługującym podpisy cyfrowe.

## Pełny kod źródłowy – rozwiązanie „wszystko w jednym”

Poniżej kompletny, gotowy do uruchomienia program, który łączy wszystkie kroki. Skopiuj, dostosuj ścieżki i naciśnij **F5**.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source PDF document
        // -------------------------------------------------
        var document = new Document("YOUR_DIRECTORY/sample.pdf");

        // -------------------------------------------------
        // Step 2: Convert the document to PDF/X‑4 format
        // (PDF/A‑4 compliance)
        // -------------------------------------------------
        var conversionOptions = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_4,
            ConvertErrorAction.Delete);
        document.Convert(conversionOptions);

        // -------------------------------------------------
        // Step 3: Save the PDF/X‑4 version
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");

        // -------------------------------------------------
        // Step 4: Add Bates numbering – how to add bates numbers
        // -------------------------------------------------
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 5000
        };
        document.AddBatesNumbering(batesOptions);

        // -------------------------------------------------
        // Step 5: Save the Bates‑numbered PDF
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_bates.pdf");

        // -------------------------------------------------
        // Step 6: Sign the document using SHA‑384 hashing
        // -------------------------------------------------
        var signature = new PdfFileSignature(document);
        var pkcs7 = new PKCS7Detached(
            "YOUR_DIRECTORY/mycert.pfx",
            "pwd",
            DigestHashAlgorithm.Sha384);
        signature.Sign(
            pageNumber: 1,
            signatureAppearance: true,
            rectangle: new Rectangle(100, 100, 200, 150),
            pkcs7: pkcs7);

        // -------------------------------------------------
        // Step 7: Save the digitally signed PDF
        // -------------------------------------------------
        signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
    }
}
```

### Oczekiwany wynik

| Plik | Cel | Kluczowa funkcja |
|------|-----|-------------------|
| `sample_pdfx4.pdf` | Wersja PDF/X‑4 | Spełnia zgodność PDF/A‑4 |
| `sample_bates.pdf` | PDF z numeracją Bates | Zastosowano **add bates numbering pdf** |
| `sample_signed.pdf` | Cyfrowo podpisany PDF | **digitally sign pdf c#** z SHA‑384 |

Otwórz dowolny z trzech plików w Adobe Acrobat Reader; zobaczysz numerację Bates w drugim pliku oraz pole podpisu w trzecim.

## Najczęściej zadawane pytania (FAQ)

**Q: Czy mogę zmienić położenie numerów Bates?**  
A: Tak. Użyj właściwości `BatesNumberingOptions`, takich jak `Location` i `FontSize`, aby precyzyjnie ustawić pozycję.

**Q: Co zrobić, jeśli potrzebuję PDF/A‑4 zamiast PDF/X‑4?**  
A: Zamień `PdfFormat.PDF_X_4` na `PdfFormat.PDFA_4` w opcjach konwersji. To spełni wymaganie **convert pdf to pdfa-4**.

**Q: Mój certyfikat używa innego algorytmu skrótu – czy mogę użyć SHA‑256?**  
A: Oczywiście. Zastąp `DigestHashAlgorithm.Sha384` przez `DigestHashAlgorithm.Sha256` (lub inny obsługiwany algorytm).

**Q: Czy muszę wywoływać `document.Save` po każdym kroku?**  
A: Niekoniecznie. W tym przepływie zapisujemy po konwersji i po numeracji Bates, aby uzyskać pliki pośrednie. Możesz odłożyć zapis do końca, jeśli wolisz jednorazową operację zapisu.

## Podsumowanie

Właśnie pokazaliśmy praktyczne, kompleksowe rozwiązanie, które **add bates numbering pdf**, wyjaśnia **how to add bates numbers**, prezentuje **convert pdf to pdf/x-4**, oraz obejmuje ...

## Co warto nauczyć się dalej?

Poniższe tutoriale dotyczą ściśle powiązanych tematów, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne przykłady kodu oraz szczegółowe wyjaśnienia, pomagające opanować dodatkowe funkcje API i eksplorować alternatywne podejścia w własnych projektach.

- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/german/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/french/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/japanese/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}