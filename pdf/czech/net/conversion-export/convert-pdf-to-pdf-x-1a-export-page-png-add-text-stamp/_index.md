---
category: general
date: 2026-03-29
description: převést PDF na PDF/X‑1a a exportovat stránku PDF jako PNG v jednom toku
  – také se naučte, jak přidat textové razítko do PDF pomocí Aspose.Pdf (C#).
draft: false
keywords:
- convert pdf to pdf/x-1a
- export pdf page png
- add text stamp pdf
- Aspose.Pdf conversion
- PDF/X‑1a workflow
language: cs
og_description: převod PDF na PDF/X‑1a a export stránky PDF do PNG při přidání textové
  razítka PDF – kompletní průvodce C# s Aspose.Pdf.
og_title: převést PDF na PDF/X-1a, exportovat stránku jako PNG a přidat textové razítko
tags:
- Aspose.Pdf
- C#
- PDF processing
title: převést PDF na PDF/X‑1a, exportovat stránku jako PNG a přidat textové razítko
url: /cs/net/conversion-export/convert-pdf-to-pdf-x-1a-export-page-png-add-text-stamp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# převod pdf na pdf/x-1a, export stránky png a přidání textového razítka – Kompletní C# průvodce

Už jste někdy potřebovali **convert pdf to pdf/x-1a**, ale také chtěli rychlý PNG náhled první stránky a vlastní textové razítko ve stejném dokumentu? Nejste v tom sami. V mnoha výrobních řetězcích—například při předkontrole tiskových souborů nebo automatickém generování reportů—často narazíte na tuto přesnou kombinaci požadavků.

V tomto tutoriálu projdeme jedním souvislým pracovním postupem, který provádí tři věci po sobě: **convert pdf to pdf/x-1a**, **export pdf page png** a **add text stamp pdf**. Kód používá knihovnu Aspose.Pdf pro .NET, takže získáte profesionální řešení, aniž byste se museli zabývat nízkoúrovňovými interními částmi PDF. Na konci budete mít spustitelný program v C#, který můžete vložit do libovolné konzolové aplikace, Azure Function nebo CI kroku.

> **Co získáte** – kompletní zdrojový soubor, podrobné vysvětlení krok za krokem, tipy na běžné úskalí a rychlý způsob, jak ověřit výstup.

## Požadavky

- .NET 6.0 nebo novější (API funguje také s .NET Framework 4.x).  
- NuGet balíček Aspose.Pdf pro .NET (`Aspose.Pdf`) – verze 23.10 je aktuální v době psaní.  
- Vstupní PDF (`input.pdf`) a soubor ICC profilu (`Coated_Fogra39L_VIGC_300.icc`) umístěné ve složce, kterou ovládáte.  
- Základní znalost C# a Visual Studio (nebo vašeho oblíbeného IDE).

Pokud vám některý z těchto pojmů není známý, jednoduše nainstalujte NuGet balíček pomocí:

```bash
dotnet add package Aspose.Pdf --version 23.10.0
```

Pojďme se ponořit dál.

## Krok 1: Načtení zdrojového PDF dokumentu

První věc, kterou uděláme, je otevřít PDF, na kterém chceme pracovat. Třída `Document` z Aspose.Pdf představuje celý soubor a načítá obsah líně, takže neplatíte výkonový trest, dokud se skutečně nedotknete stránek.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Devices;
using Aspose.Pdf.Text;
using Aspose.Pdf.Conversion;

// Adjust these paths to match your environment
string baseDir = @"C:\MyProjects\PdfDemo\";
string inputPath = Path.Combine(baseDir, "input.pdf");

// Load the PDF – this is where any file‑not‑found errors will surface
Document pdfDoc = new Document(inputPath);
```

*Proč je to důležité*: Včasné načtení dokumentu nám poskytuje jediný objekt, který můžeme předávat pro konverzi, renderování a razítkování. Pokud přeskočíte explicitní načtení a pokusíte se pracovat s neexistujícím souborem, později obdržíte nejasnou výjimku `FileNotFoundException`.

## Krok 2: Převod dokumentu na PDF/X‑1a pomocí vlastního ICC profilu

PDF/X‑1a je de‑facto standard pro tiskové PDF. Krok konverze vám také umožňuje vložit **Output Intent** (ICC profil), aby downstream RIPy přesně věděly, jak mají být barvy interpretovány.

```csharp
// Prepare conversion options – we ask Aspose to delete any objects that would break PDF/X‑1a compliance
PdfFormatConversionOptions conversionOptions = new PdfFormatConversionOptions(
    PdfFormat.PDF_X_1A,               // Target format
    ConvertErrorAction.Delete)       // Drop non‑compliant objects automatically
{
    IccProfileFileName = Path.Combine(baseDir, "Coated_Fogra39L_VIGC_300.icc"),
    OutputIntent = new OutputIntent("FOGRA39") // Human‑readable name for the intent
};

// Perform the conversion in‑place
pdfDoc.Convert(conversionOptions);
```

*Tip*: Pokud potřebujete přísnější zpracování chyb, nahraďte `ConvertErrorAction.Delete` za `ConvertErrorAction.Throw`. Tím se konverze přeruší při první nekompatibilitě, což je užitečné pro automatizované QA pipeline.

## Krok 3: Export první stránky jako PNG při analýze fontů

PNG náhled je často vyžadován pro rychlé vizuální kontroly nebo generování miniatur. Povolením `AnalyzeFonts` zajistí Aspose, že všechny vložené fonty jsou správně rasterizovány, čímž se vyhnete překvapením s chybějícími glyfy.

```csharp
// Configure the PNG device – you can tweak resolution, color depth, etc.
PngDevice pngDevice = new PngDevice
{
    RenderingOptions = new RenderingOptions
    {
        AnalyzeFonts = true,          // Guarantees faithful text rendering
        Resolution = 300              // 300 DPI is a good trade‑off for quality vs. size
    }
};

// Export the first page (index is 1‑based)
string pngPath = Path.Combine(baseDir, "page1.png");
pngDevice.Process(pdfDoc.Pages[1], pngPath);
```

Po spuštění najdete `page1.png` vedle vašich zdrojových souborů. Otevřete jej v libovolném prohlížeči obrázků a ověřte, že konverze vypadá správně.

## Krok 4: Přidání textového razítka, které automaticky upravuje velikost písma

**Textové razítko** je praktický způsob, jak vodoznakovat nebo anotovat PDF, aniž byste měnili podkladové content streamy. Nastavením `AutoAdjustFontSizeToFitStampRectangle` zajistíte, že knihovna zmenší nebo zvětší text tak, aby nikdy nepřetekl definovaný obdélník.

```csharp
// Create a stamp with the desired text
TextStamp autoSizeStamp = new TextStamp("Auto‑size")
{
    AutoAdjustFontSizeToFitStampRectangle = true,
    Width = 400,        // Width of the stamp rectangle (points)
    Height = 200,       // Height of the stamp rectangle (points)
    // Optional: position the stamp – here we center it on the page
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Center,
    // Optional: give it a semi‑transparent background for readability
    Background = new BackgroundInfo(Color.FromRgb(255, 255, 0), 0.3f)
};

// Attach the stamp to the first page (you could loop over all pages if needed)
pdfDoc.Pages[1].AddStamp(autoSizeStamp);
```

*Proč automatická velikost?* Pokud později změníte text razítka na delší (např. dynamický časový údaj), nebudete muset ručně přepočítávat velikosti písma – razítko se přizpůsobí za běhu.

## Krok 5: Uložení aktualizovaného PDF dokumentu

Nakonec vše zapíšete zpět na disk. Můžete buď přepsat původní soubor, nebo vytvořit zcela nový; níže uvedený příklad vytváří `output.pdf`.

```csharp
string outputPath = Path.Combine(baseDir, "output.pdf");
pdfDoc.Save(outputPath);
```

Když se uložení dokončí, máte:

1. Soubor **PDF/X‑1a** kompatibilní (`output.pdf`).  
2. PNG **náhled** první stránky (`page1.png`).  
3. **Textové razítko**, které přesně zapadá do svého obdélníku.

### Rychlý kontrolní seznam ověření

| ✅ Kontrola | Jak ověřit |
|------------|------------|
| Soulad s PDF/X‑1a | Otevřete `output.pdf` v Adobe Acrobat → *Print Production* → *Preflight* a vyberte “PDF/X‑1a:2001”. |
| PNG vypadá správně | Otevřete `page1.png` ve Windows Photo Viewer nebo v libovolném editoru obrázků. |
| Razítko se zobrazuje | Projděte `output.pdf` – text “Auto‑size” by měl být vycentrován na stránce 1. |

![náhled převodu pdf na pdf/x-1a s automaticky velikostním textovým razítkem](image.png "náhled převodu pdf na pdf/x-1a zobrazující razítko")

*Alt text obrázku*: **náhled převodu pdf na pdf/x-1a s automaticky velikostním textovým razítkem** – ukazuje finální PDF po všech krocích.

## Běžné varianty a okrajové případy

- **Více stránek** – Pokud potřebujete razítkovat každou stránku, projděte `pdfDoc.Pages` v cyklu a zavolejte `AddStamp` uvnitř smyčky.  
- **Jiný výstupní formát** – Změňte `PdfFormat.PDF_X_1A` na `PdfFormat.PDF_A_1B` pro archivní PDF.  
- **Vyšší rozlišení PNG** – Nastavte `Resolution = 600` v `RenderingOptions` pro miniatury v tiskové kvalitě.  
- **Vlastní font pro razítko** – Přiřaďte `autoSizeStamp.Font = FontRepository.FindFont("Arial")` před přidáním razítka.  
- **Zpracování chyb** – Obalte každý hlavní krok do `try/catch` a logujte `ConversionException` nebo `FileNotFoundException` pro snadnější ladění.

## Kompletní funkční příklad (připravený ke kopírování a vložení)

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Devices;
using Aspose.Pdf.Text;
using Aspose.Pdf.Conversion;
using Aspose.Pdf.Color; // For BackgroundInfo color

class PdfX1aWorkflow
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Setup paths
        // -----------------------------------------------------------------
        string baseDir = @"C:\MyProjects\PdfDemo\";
        string inputPdf = Path.Combine(baseDir, "input.pdf");
        string iccProfile = Path.Combine(baseDir, "Coated_Fogra39L_VIGC_300.icc");
        string pngOutput = Path.Combine(baseDir, "page1.png");
        string finalPdf = Path.Combine(baseDir, "output.pdf");

        // -----------------------------------------------------------------
        // 2️⃣ Load the source document
        // -----------------------------------------------------------------
        Document pdfDoc = new Document(inputPdf);

        // -----------------------------------------------------------------
        // 3️⃣ Convert to PDF/X‑1a (print‑ready)
        // -----------------------------------------------------------------
        PdfFormatConversionOptions convOpts = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_1A,
            ConvertErrorAction.Delete)
        {
            IccProfileFileName = iccProfile,
            OutputIntent = new OutputIntent("FOGRA39")
        };
        pdfDoc.Convert(convOpts);

        // -----------------------------------------------------------------
        // 4️⃣ Export first page as PNG (export pdf page png)
        // -----------------------------------------------------------------
        PngDevice pngDevice = new PngDevice
        {
            RenderingOptions = new RenderingOptions
            {
                AnalyzeFonts = true,
                Resolution = 300
            }
        };
        pngDevice.Process(pdfDoc.Pages[1], pngOutput);

        // -----------------------------------------------------------------
        // 5️⃣ Add auto‑sizing text stamp (add text stamp pdf)
        // -----------------------------------------------------------------
        TextStamp stamp = new TextStamp("Auto‑size")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Width = 400,
            Height = 200,
            HorizontalAlignment = HorizontalAlignment.Center,
            VerticalAlignment = VerticalAlignment.Center,
            Background = new BackgroundInfo(Color.From

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}