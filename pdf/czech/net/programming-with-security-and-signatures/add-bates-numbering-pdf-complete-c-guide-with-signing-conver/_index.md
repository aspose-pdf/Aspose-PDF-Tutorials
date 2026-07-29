---
category: general
date: 2026-06-21
description: Přidejte Batesovo číslování do PDF a naučte se, jak přidávat Batesova
  čísla, převádět PDF na PDF/X‑4, převádět PDF na PDF/A‑4 a digitálně podepisovat
  PDF v C# v jednom průvodci.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbers
- digitally sign pdf c#
- convert pdf to pdf/x-4
- convert pdf to pdfa-4
language: cs
og_description: Přidejte Batesovo číslování do PDF, zjistěte, jak přidat Batesova
  čísla, převést PDF na PDF/X-4, převést PDF na PDF/A-4 a digitálně podepsat PDF v
  C# pomocí Aspose.Pdf.
og_title: Přidání Batesova číslování do PDF – krok za krokem C# tutoriál
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
title: Přidání Batesova číslování do PDF – Kompletní C# průvodce s podepisováním a
  konverzí
url: /cs/net/programming-with-security-and-signatures/add-bates-numbering-pdf-complete-c-guide-with-signing-conver/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidání Batesova číslování PDF – Kompletní průvodce v C# s podepisováním a konverzí

Už jste se někdy zamýšleli nad **add bates numbering pdf** bez toho, abyste si trhali vlasy? Nejste jediní. Právní týmy, auditoři a všichni, kdo potřebují sledovatelné dokumenty, se neustále ptají *jak přidat Batesova čísla* do PDF a zároveň potřebují, aby soubor splňoval standardy PDF/X‑4 nebo PDF/A‑4 a byl digitálně podepsán.  

V tomto tutoriálu projdeme přesně to – pomocí Aspose.Pdf pro .NET **add bates numbering pdf**, ukážeme **jak přidat Batesova čísla**, **convert pdf to pdf/x-4**, **convert pdf to pdfa-4** a nakonec **digitally sign pdf c#**. Na konci budete mít připravený program, který vytvoří tři vyladěné PDF: verzi PDF/X‑4, verzi s Batesovým číslováním a digitálně podepsanou verzi.

![add bates numbering pdf example](image-placeholder.png "Screenshot showing add bates numbering pdf in action")

## Co budete potřebovat

- **.NET 6+** (nebo .NET Framework 4.6+). Aspose.Pdf podporuje oba.
- **Platná licence Aspose.Pdf pro .NET** (nebo můžete pracovat s evaluační verzí, ale objeví se vodoznaky).
- **Soubor certifikátu PKCS#7** (`.pfx`) a jeho heslo pro podepisování.
- **Ukázkový PDF**, který chcete transformovat (umístěte jej do složky, kterou ovládáte).
- Visual Studio, Rider nebo jakékoli IDE pro C#, které máte rádi.

To je vše – žádné další NuGet balíčky kromě `Aspose.Pdf`. Pokud knihovnu ještě nepřidali, spusťte:

```bash
dotnet add package Aspose.Pdf
```

Pojďme se ponořit do kódu.

## Krok 1: Načtení zdrojového PDF dokumentu

Nejprve musíme načíst originální soubor do paměti. To je základ pro všechny následující operace.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

// Load the source PDF – adjust the path to your environment
var document = new Document("YOUR_DIRECTORY/sample.pdf");
```

> **Proč je to důležité:** Načtení PDF vytvoří objekt `Document`, který představuje celý soubor a poskytuje přístup k API pro konverzi, formulářová pole a zabezpečení.

## Krok 2: Konverze PDF na PDF/X‑4 (shoda s PDF/A‑4)

Pokud váš workflow vyžaduje archivní kvalitu, PDF/X‑4 (podmnožina PDF/A‑4) je správná cesta. Zde je návod, jak **convert pdf to pdf/x-4** pomocí Aspose.

```csharp
// Set conversion options – PDF/X‑4 is the target format
var conversionOptions = new PdfFormatConversionOptions(PdfFormat.PDF_X_4, ConvertErrorAction.Delete);

// Perform the conversion
document.Convert(conversionOptions);
```

> **Tip:** Příznak `ConvertErrorAction.Delete` odstraní veškerý obsah, který by porušil shodu, a zajistí čistý výstup PDF/X‑4.

## Krok 3: Uložení verze PDF/X‑4

Jakmile dokument splňuje PDF/X‑4, uložíme jej na disk.

```csharp
document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");
```

Nyní máte soubor kompatibilní s **convert pdf to pdfa-4** (PDF/X‑4 je členem rodiny PDF/A‑4). Klidně jej otevřete v Acrobat a ověřte štítek shody.

## Krok 4: Přidání Batesova číslování – jádro „Add Bates Numbering PDF“

Batesovo číslování je sekvenční identifikátor umístěný na každé stránce. Toto je přesná odpověď na otázku *jak přidat Batesova čísla* programově.

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

> **Proč to funguje:** `AddBatesNumbering` prochází každou stránku a razítkuje číslo na výchozí pozici (vpravo dole). Později můžete pozici upravit pomocí `BatesNumberingOptions`, pokud budete potřebovat.

## Krok 5: Uložení PDF s Batesovým číslováním

Po **add bates numbering pdf** potřebujeme samostatný soubor, který si zachová čísla.

```csharp
document.Save("YOUR_DIRECTORY/sample_bates.pdf");
```

Otevřete soubor; měli byste vidět „CASE‑5000“, „CASE‑5001“ a tak dále ve spodní části každé stránky.

## Krok 6: Digitální podepsání PDF – „Digitally Sign PDF C#“ v praxi

Digitální podpis zaručuje pravost a integritu. Níže **digitally sign pdf c#** pomocí hash algoritmu SHA‑384.

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

> **Pro tip:** `Rectangle` určuje, kde se zobrazí viditelný podpis. Pokud vizuální indikátor nepotřebujete, nastavte `signatureAppearance` na `false`.

## Krok 7: Uložení digitálně podepsaného PDF

Nakonec zapíšeme podepsaný dokument na disk.

```csharp
signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
```

Nyní máte soubor **digitally sign pdf c#**, který lze ověřit v libovolném PDF čtečce podporující digitální podpisy.

## Kompletní zdrojový kód – vše v jednom řešení

Níže je kompletní, připravený program, který spojuje všechny kroky. Zkopírujte, upravte cesty a stiskněte **F5**.

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

### Očekávaný výstup

| Soubor | Účel | Klíčová vlastnost |
|--------|------|-------------------|
| `sample_pdfx4.pdf` | Verze PDF/X‑4 | Splňuje shodu PDF/A‑4 |
| `sample_bates.pdf` | PDF s Batesovým číslováním | Aplikováno **add bates numbering pdf** |
| `sample_signed.pdf` | Digitálně podepsané PDF | **digitally sign pdf c#** s SHA‑384 |

Otevřete kterýkoli ze tří souborů v Adobe Acrobat Reader; u druhého souboru uvidíte Batesova čísla a u třetího pole s podpisem.

## Často kladené otázky (FAQ)

**Q: Můžu změnit pozici Batesových čísel?**  
A: Ano. Použijte vlastnosti `BatesNumberingOptions`, jako jsou `Location` a `FontSize`, pro doladění umístění.

**Q: Co když potřebuji PDF/A‑4 místo PDF/X‑4?**  
A: V konverzních možnostech změňte `PdfFormat.PDF_X_4` na `PdfFormat.PDFA_4`. Tím splníte požadavek **convert pdf to pdfa-4**.

**Q: Můj certifikát používá jiný hash algoritmus – mohu použít SHA‑256?**  
A: Samozřejmě. Nahraďte `DigestHashAlgorithm.Sha384` za `DigestHashAlgorithm.Sha256` (nebo jakýkoli podporovaný algoritmus).

**Q: Musím volat `document.Save` po každém kroku?**  
A: Není to nutné. V tomto postupu ukládáme po konverzi a po přidání Batesova číslování, abychom vám poskytli mezilehlé soubory. Ukládání můžete odložit až na konec, pokud chcete provést jediný zápis.

## Závěr

Právě jsme předvedli praktické, end‑to‑end řešení, které **add bates numbering pdf**, vysvětluje **jak přidat Batesova čísla**, ukazuje **convert pdf to pdf/x-4**, a pokrývá

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným krok‑za‑krokem vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vlastních projektech.

- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/german/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/french/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/japanese/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}