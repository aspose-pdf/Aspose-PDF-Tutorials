---
category: general
date: 2026-10-10
description: Naučte se, jak uložit PDF jako HTML pomocí Aspose.PDF, vynecháním rastrových
  obrázků. Tento průvodce pokrývá převod PDF do HTML a efektivní uložení dokumentu
  jako HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save pdf as html
- convert pdf to html
- aspose pdf to html
- save pdf without images
- save document as html
language: cs
lastmod: 2026-10-10
og_description: Uložte PDF jako HTML pomocí Aspose.PDF a vynechejte rastrové obrázky.
  Sledujte tento kompletní návod, jak převést PDF na HTML a uložit dokument jako HTML.
og_image_alt: Screenshot showing PDF saved as HTML without images using Aspose.PDF
og_title: Uložte PDF jako HTML bez obrázků – průvodce krok za krokem Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to save PDF as HTML with Aspose.PDF, skipping raster images.
    This guide covers convert PDF to HTML and save document as HTML efficiently.
  headline: How to save PDF as HTML without images using Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- HTML conversion
title: Jak uložit PDF jako HTML bez obrázků pomocí Aspose.PDF
url: /cs/net/document-conversion/how-to-save-pdf-as-html-without-images-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak uložit PDF jako HTML bez obrázků pomocí Aspose.PDF

Pokud potřebujete **uložit PDF jako HTML** a vynechat všechny rastrové grafiky, tento tutoriál vám přesně ukáže, jak na to. Nastavením `HtmlSaveOptions` můžete PDF převést na HTML efektivně a udržet výstup lehký – ideální pro web‑přátelskou dokumentaci nebo SEO‑optimalizované stránky.

Kromě odstraňování obrázků průvodce také ukazuje širší workflow **convert PDF to HTML**, takže získáte čistý HTML soubor, který zachovává text, vektorové grafiky a rozvržení. Žádné externí nástroje nejsou potřeba; vše běží uvnitř standardního .NET projektu.

## Požadavky

* .NET 6.0 nebo novější (kód také funguje s .NET Framework 4.6+)
* Platná licence Aspose.PDF for .NET (nebo bezplatný evaluační klíč)
* Vstupní PDF soubor umístěný v známém adresáři
* Visual Studio 2022 (nebo jakékoli C# IDE)

Tyto položky jsou dostačující pro zkompilování a spuštění ukázkového kódu uvedeného níže.

## Krok 1: Nainstalujte NuGet balíček Aspose.PDF

Prvním krokem je přidat knihovnu Aspose.PDF do vašeho projektu:

```bash
dotnet add package Aspose.PDF
```

Spuštěním tohoto příkazu se obnoví nejnovější stabilní verze Aspose.PDF, která obsahuje třídu `HtmlSaveOptions` potřebnou pro konverzi.

## Krok 2: Načtěte zdrojový PDF dokument

Načtení PDF je jednoduché pomocí třídy `Document`. Tato třída představuje celý PDF soubor v paměti.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Saving;

// Step 2: Load the source PDF document
Document doc = new Document(@"C:\MyFiles\input.pdf");
```

*Proč je tento krok důležitý:*  
`Document` analyzuje strukturu PDF, poskytuje vám přístup k stránkám, fontům a zdrojům. Bez načtení souboru nejprve nemůžete použít žádné možnosti ukládání.

## Krok 3: Nakonfigurujte HTML možnosti ukládání tak, aby přeskočily rastrové obrázky

Objekt `HtmlSaveOptions` vám umožňuje jemně doladit výstup HTML. Nastavením `SkipRasterImages` na `true` řeknete Aspose.PDF, aby během konverze ignoroval všechny bitmapové obrázky (JPEG, PNG, GIF).

```csharp
// Step 3: Configure HTML save options to skip raster images
HtmlSaveOptions htmlOpts = new HtmlSaveOptions
{
    // Exclude all raster (bitmap) images from the output HTML
    SkipRasterImages = true,

    // Optional: embed fonts as Base64 to avoid external font files
    EmbedFonts = true,

    // Optional: preserve the original layout as closely as possible
    FixedLayout = true
};
```

*Proč je tento krok důležitý:*  
Rastrové obrázky často dominují velikosti souboru. Jejich vynecháním vytvoříte štíhlejší HTML soubor, který se načítá rychleji a je snazší jej indexovat vyhledávači. Další možnosti (`EmbedFonts`, `FixedLayout`) jsou uvedeny pro úplnost; nejsou nutné pro odstranění obrázků.

## Krok 4: Uložte dokument jako HTML bez obrázků

Nyní můžete zapsat převedený obsah na disk. Přetížení `Save` přijímá cílovou cestu, požadovaný `SaveFormat` a dříve nakonfigurované možnosti.

```csharp
// Step 4: Save the document as HTML without raster images
doc.Save(@"C:\MyFiles\no_images.html", SaveFormat.Html, htmlOpts);
```

Po dokončení volání obsahuje `no_images.html` textový obsah, vektorové tvary a CSS, které rekonstruují původní rozvržení PDF – bez bitmapových obrázků.

### Očekávaný výstup

Otevřete `no_images.html` v prohlížeči. Měli byste vidět:

* Všechny nadpisy, odstavce a tabulky z původního PDF.
* Vektorové grafiky (např. SVG tvary) vykreslené správně.
* Žádné `<img>` značky odkazující na rastrové soubory; tyto značky jsou zcela vynechány.

Pokud prozkoumáte HTML zdroj, všimnete si absence elementů `<img src="...">`, což potvrzuje, že `SkipRasterImages` fungovalo podle očekávání.

## Kompletní, spustitelný příklad

Níže je samostatná konzolová aplikace, která spojuje všechny kroky dohromady. Zkopírujte kód do nového .NET konzolového projektu a spusťte jej.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Saving;

namespace PdfToHtmlNoImages
{
    class Program
    {
        static void Main(string[] args)
        {
            // Input and output paths – adjust to your environment
            string inputPath = @"C:\MyFiles\input.pdf";
            string outputPath = @"C:\MyFiles\no_images.html";

            // 1. Load the PDF document
            Document doc = new Document(inputPath);
            Console.WriteLine($"Loaded PDF: {inputPath}");

            // 2. Set up HTML save options to omit raster images
            HtmlSaveOptions htmlOpts = new HtmlSaveOptions
            {
                SkipRasterImages = true,
                EmbedFonts = true,
                FixedLayout = true
            };
            Console.WriteLine("Configured HtmlSaveOptions to skip raster images.");

            // 3. Save as HTML
            doc.Save(outputPath, SaveFormat.Html, htmlOpts);
            Console.WriteLine($"PDF saved as HTML without images at: {outputPath}");
        }
    }
}
```

**Spuštění programu** vypíše průběžné zprávy do konzole a vytvoří `no_images.html`. Ověřte soubor jeho otevřením v libovolném moderním prohlížeči.

## Běžné varianty a okrajové případy

| Situace | Jak upravit kód |
|-----------|-----------------------|
| **Ponechat rastrové obrázky** | Set `SkipRasterImages = false` (or omit the property). |
| **Převést pouze rozsah stránek** | Use `doc.Pages.Delete(pageNumber)` to remove unwanted pages before saving, or set `htmlOpts.PageIndex` and `htmlOpts.PageCount`. |
| **Uložit každou stránku PDF jako samostatný HTML soubor** | Set `htmlOpts.SplitIntoPages = true`; the library will generate `output_page1.html`, `output_page2.html`, etc. |
| **Komprimovat výsledné HTML** | After saving, run a minifier on the file or set `htmlOpts.Compress = true` (available in newer Aspose versions). |
| **Zpracovat PDF chráněné heslem** | Pass the password to the `Document` constructor: `new Document(inputPath, new LoadOptions { Password = "secret" })`. |

Tyto varianty vám umožní přizpůsobit konverzi **aspose pdf to html** mnoha reálným scénářům.

## Profesionální tipy

* **Licencujte včas** – Zaregistrujte svou licenci Aspose.PDF před načtením dokumentu, aby se předešlo vodoznakům z evaluační verze.
* **Výkon** – Pro velké PDF soubory znovu použijte jedinou instanci `HtmlSaveOptions` a zvažte povolení `htmlOpts.UseZOrder = true`, což urychlí vykreslování překrývajících se elementů.
* **Testování** – Porovnejte velikost HTML souboru s obrázky a bez nich, abyste kvantifikovali výhodu `SkipRasterImages`.

## Závěr

Nyní víte, jak **uložit PDF jako HTML** a zároveň odstranit rastrové grafiky pomocí Aspose.PDF pro .NET. Kompletní postup – načíst PDF, nakonfigurovat `HtmlSaveOptions` s `SkipRasterImages` a uložit výsledek – pokrývá základní případ použití **convert PDF to HTML** a lze jej rozšířit o konverzi rozsahu stránek, výstup po stránkách nebo další optimalizace.

Dále můžete prozkoumat **save document as HTML** s vloženým CSS, nebo experimentovat s třídou `SvgSaveOptions` pro generování škálovatelných vektorových grafik místo HTML. Oba přístupy dále snižují velikost souboru a zlepšují responzivitu moderních webových aplikací. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Převést PDF na HTML v .NET pomocí Aspose.PDF bez ukládání obrázků](/pdf/english/net/conversion-export/convert-pdf-html-net-asposepdf-no-images/)
- [Konverze PDF na HTML pomocí Aspose.PDF .NET: Uložit obrázky jako externí PNG](/pdf/english/net/conversion-export/pdf-to-html-conversion-external-png-aspose-pdf-net/)
- [Uložit PDF jako HTML s Aspose.PDF – Rychlý C# průvodce](/pdf/english/net/conversion-export/save-pdf-as-html-with-aspose-pdf-quick-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}