---
category: general
date: 2026-02-09
description: Uložte PDF jako PNG v C# pomocí Aspose PDF, poté exportujte PDF do HTML,
  přidejte vodoznakové razítko PDF a naučte se, jak převést PDFX‑1a pro konverzi PDF
  v ASP.NET.
draft: false
keywords:
- save pdf as png
- export pdf to html
- add watermark stamp pdf
- how to convert pdfx-1a
- asp.net pdf conversion
language: cs
og_description: Uložte PDF jako PNG v C# s Aspose PDF, poté exportujte PDF do HTML,
  přidejte vodoznakové razítko PDF a zjistěte, jak převést PDFX‑1a pro konverzi PDF
  v ASP.NET.
og_title: Uložit PDF jako PNG a převést na PDF/X‑1a pomocí Aspose PDF
tags:
- aspnet
- pdf
- csharp
title: Uložte PDF jako PNG a převést na PDF/X‑1a pomocí Aspose PDF
url: /cs/net/conversion-export/save-pdf-as-png-and-convert-to-pdf-x-1a-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uložte PDF jako PNG a převěďte na PDF/X‑1a pomocí Aspose PDF

Už jste se někdy zamysleli, jak **save PDF as PNG** bez toho, aby vám to vytrhlo vlasy? Nejste jediní — vývojáři neustále požadují rychlý způsob, jak rasterizovat stránku a zároveň zachovat původní PDF beze změny. V tomto průvodci vás provedeme právě tím, a také vám ukážeme, jak **export PDF to HTML**, přidat **watermark stamp PDF**, a dokonce **convert PDFX‑1a** pro robustní **ASP.NET PDF conversion** pipeline.

Co získáte z tohoto tutoriálu, je jednorázový, připravený k kopírování C# program, který načte PDF, převede jej na soubor kompatibilní s PDF/X‑1a, vykreslí první stránku jako PNG, přidá dynamický textový razítko a nakonec vygeneruje HTML verzi, která respektuje kódování fontů. Žádné vágní odkazy, jen konkrétní kód a „proč“ za každým řádkem.

## Požadavky

- .NET 6.0 nebo novější (kód funguje také na .NET Framework 4.7+)
- NuGet balíček Aspose.Pdf pro .NET (`Install-Package Aspose.Pdf`)
- Soubor ICC profilu (`profile.icc`), pokud potřebujete shodu s PDF/X‑1a
- Vstupní PDF (`input.pdf`), které chcete transformovat

To je vše — žádné další knihovny, žádné skryté kroky. Pokud to máte, můžete začít.

## Krok 1: Načtěte zdrojový PDF dokument

Než budeme moci cokoli udělat, musíme PDF načíst do paměti.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Devices;

// Load the PDF you’ll be working with
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

**Proč je to důležité:** `Document` je hlavní objekt; poskytuje přístup ke stránkám, fontům a metadatům. Načtení jednou udržuje zbytek pipeline rychlý.

## Krok 2: Převod na PDF/X‑1a (Jak převést PDFX‑1a)

PDF/X‑1a je standardem pro soubory připravené k tisku. Převod zajišťuje, že všechny fonty jsou vloženy a barvy definovány.

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

**Tip:** Pokud vynecháte ICC profil, Aspose vloží výchozí, ale použití přesného profilu, který vaše tiskárna očekává, zabraňuje nepříjemným posunům barev.

## Krok 3: Uložte soubor kompatibilní s PDF/X‑1a

Nyní, když dokument splňuje specifikaci PDF/X‑1a, zapíšeme jej.

```csharp
pdfDocument.Save("YOUR_DIRECTORY/pdfx1a.pdf");
```

Všimnete si, že velikost souboru může vzrůst — jsou vkládány další zdroje, což je přesně to, co chcete pro spolehlivý tisk.

## Krok 4: Vykreslete první stránku do PNG (Uložte PDF jako PNG)

Zde se ukáže hlavní klíčové slovo: **save PDF as PNG** pro náhledové miniatury nebo webové zobrazení.

```csharp
// Configure PNG device with font analysis (helps with text extraction later)
PngDevice pngDevice = new PngDevice
{
    RenderingOptions = new RenderingOptions { AnalyzeFonts = true }
};

// Render only the first page
pngDevice.Process(pdfDocument.Pages[1], "YOUR_DIRECTORY/page1.png");
```

![Příklad uložení PDF jako PNG](https://example.com/images/save-pdf-as-png.png "Příklad PDF stránky uložené jako PNG")

Příznak `AnalyzeFonts` říká Aspose, aby vložil informace o fontu do metadat PNG, což je užitečný trik, pokud později potřebujete mapovat zpět na původní text.

## Krok 5: Přidejte vodotiskový razítko PDF

Přidání **watermark stamp PDF** je s `TextStamp` od Aspose triviální. Razítko automaticky přizpůsobíme tak, aby se vešlo do obdélníku.

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

**Proč automatické přizpůsobení?** Různé stránky mají různé hustoty; nechat API vypočítat optimální velikost fontu zaručuje, že text nikdy nepřeteče obdélník.

## Krok 6: Uložte PDF s razítkem

Po přidání razítka změny uložíme.

```csharp
pdfDocument.Save("YOUR_DIRECTORY/stamped.pdf");
```

Otevřete `stamped.pdf` v libovolném prohlížeči a uvidíte pole „Important notice“ pěkně vycentrované — žádné ruční úpravy nejsou potřeba.

## Krok 7: Export PDF do HTML (Export PDF to HTML)

Nakonec **export PDF to HTML** s preferencí CMap pro kódování fontů. To zajišťuje, že vygenerované HTML používá Unicode, kdekoliv je to možné, a text zůstane prohledávatelný.

```csharp
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    FontEncodingStrategy = HtmlSaveOptions.FontEncodingRules.DecreaseToUnicodePriorityLevel
};

// Save the HTML representation
pdfDocument.Save("YOUR_DIRECTORY/cmap.html", htmlOptions);
```

Výsledný `cmap.html` obsahuje elementy `<canvas>` pro složité grafiky a správné `<span>` tagy pro text, což ho připravuje na SEO‑přátelské webové stránky.

## Kompletní funkční příklad

Níže je kompletní program, který můžete vložit do konzolové aplikace. Stačí nahradit placeholder cesty a jste připraveni.

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

**Očekávaný výstup**

- `pdfx1a.pdf` — tiskový PDF/X‑1a soubor
- `page1.png` — rastrový obrázek první stránky (ideální pro miniatury)
- `stamped.pdf` — originální PDF s škálovatelným vodotiskem „Important notice“
- `cmap.html` — web‑přátelská HTML verze s Unicode fonty

## Časté otázky a okrajové případy

- **Co když má zdrojové PDF šifrované stránky?**  
  Načtěte jej s heslem: `new Document("input.pdf", new LoadOptions { Password = "secret" })`.

- **Potřebuji ICC profil pro každý převod?**  
  Ne nutně — Aspose použije generický profil, ale pro striktní shodu s PDF/X‑1a byste měli poskytnout přesně ten, který používá vaše tiskárna.

- **Mohu vykreslit více než jednu stránku do PNG?**  
  Samozřejmě. Procházejte `pdfDocument.Pages` a zavolejte `pngDevice.Process(page, $"page{page.Number}.png")`.

- **Je výstupní HTML vhodné pro mobily?**  
  Vygenerované HTML používá responzivní elementy `<canvas>`. Pokud potřebujete čistě CSS‑založený text, nastavte `htmlOptions.SplitIntoPages = false` a upravte `htmlOptions.PartsEmbeddingMode`.

## Tipy pro ASP.NET PDF konverzi

Když integrujete tento kód do ASP.NET Core controlleru, pamatujte na:

1. **Streamujte výsledek** místo zápisu na disk — použijte `MemoryStream` a vraťte `FileResult`.
2. **Uvolněte** `Document` a objekty zařízení pomocí `using

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}