---
category: general
date: 2026-07-20
description: Jak přeskočit export obrázků při převodu PDF na HTML pomocí Aspose.PDF
  pro .NET – naučte se převést PDF na HTML bez obrázků během pouhých tří kroků.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to skip image export in pdf to html
- convert pdf to html without images
- aspose pdf html conversion
- disable raster images
- pdf to html conversion c#
language: cs
lastmod: 2026-07-20
og_description: Jak přeskočit export obrázků při převodu PDF do HTML pomocí Aspose.PDF
  pro .NET. Tento průvodce vám ukáže, jak efektivně převést PDF do HTML bez obrázků.
og_image_alt: C# code screenshot converting PDF to HTML without images using Aspose.PDF
og_title: Jak vynechat export obrázků z PDF do HTML – Rychlý C# tutoriál
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: How to skip image export in PDF to HTML using Aspose.PDF for .NET –
    learn to convert PDF to HTML without images in just three steps.
  headline: How to Skip Image Export in PDF to HTML – Complete C# Guide
  type: TechArticle
- description: How to skip image export in PDF to HTML using Aspose.PDF for .NET –
    learn to convert PDF to HTML without images in just three steps.
  name: How to Skip Image Export in PDF to HTML – Complete C# Guide
  steps:
  - name: Why `RasterImages = false` Does the Trick
    text: '- **Raster images** are the bitmap pictures embedded in the PDF (JPEG,
      PNG, etc.). When you set `RasterImages` to `false`, Aspose simply omits the
      step that extracts and writes those bitmaps to the HTML folder. - The rest of
      the PDF—fonts, vector shapes, tables, and layout information—still gets tra'
  - name: 1️⃣ Load Your PDF Document
    text: We use the `Document` class, which parses the PDF structure in memory. No
      extra configuration is needed unless you’re dealing with encrypted files.
  - name: 2️⃣ Tweak the Save Options
    text: '`HtmlSaveOptions` is a flexible container. Besides `RasterImages`, you
      could also tweak `SplitIntoPages`, `EmbedFonts`, or `CssStyleSheetType`. For
      our purpose, the single line `RasterImages = false` does all the heavy lifting.'
  - name: 3️⃣ Write Out the HTML
    text: The `Save` method writes a single HTML file (plus a folder for any auxiliary
      resources like CSS). Because we disabled raster images, the resources folder
      will be empty or contain only CSS files.
  - name: Expected Result
    text: 'Open `NoImages.html` in a browser. You should see:'
  type: HowTo
tags:
- pdf
- html
- csharp
- aspose
- conversion
title: Jak přeskočit export obrázků při převodu PDF do HTML – Kompletní průvodce C#
url: /cs/net/conversion-export/how-to-skip-image-export-in-pdf-to-html-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak přeskočit export obrázků při převodu PDF do HTML – Kompletní průvodce v C#

Už jste se někdy zamysleli **jak přeskočit export obrázků při převodu PDF do HTML**, když potřebujete jen textové rozvržení? Možná vytváříte odlehčený webový náhled a těžké rastrové obrázky jsou jen zbytečnou zátěží. Dobrou zprávou je, že nemusíte vynalézat kolo—Aspose.PDF pro .NET vám poskytuje praktický přepínač pro **převod PDF do HTML bez obrázků** během okamžiku.

V tomto tutoriálu projdeme přesné kroky, vysvětlíme, proč volba funguje, a ukážeme vám připravený příklad. Na konci budete mít čistý HTML soubor, který odráží strukturu původního PDF, ale vynechá všechny rastrové obrázky.

## Požadavky

Než se pustíme dál, ujistěte se, že máte:

- .NET 6 nebo novější (kód také funguje s .NET Framework 4.7+)
- Visual Studio 2022 (nebo jakýkoli editor, který preferujete)
- Licencovanou kopii **Aspose.PDF for .NET** (zdarma zkušební verze stačí pro testování)
- PDF soubor, který chcete převést—ideálně s několika těžkými obrázky, abyste viděli rozdíl

To je vše. Žádné další NuGet balíčky kromě Aspose.PDF.

## Jak přeskočit export obrázků při převodu PDF do HTML – Nastavení a kód

Níže je kompletní, samostatný program. Vložte jej do nového konzolového projektu, nahraďte zástupné cesty a stiskněte **F5**.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.HtmlSaveOptions;

namespace PdfToHtmlNoImages
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF. Adjust the path to point at your file.
            string sourcePdf = @"C:\Docs\HeavyImages.pdf";
            Document pdfDocument = new Document(sourcePdf);

            // 2️⃣ Configure HTML save options.
            //    Setting RasterImages = false tells Aspose to skip raster image export.
            HtmlSaveOptions htmlOptions = new HtmlSaveOptions
            {
                RasterImages = false // <-- This is the key line for skipping images
            };

            // 3️⃣ Save the PDF as HTML. The output will contain text and vector graphics only.
            string outputHtml = @"C:\Docs\NoImages.html";
            pdfDocument.Save(outputHtml, htmlOptions);

            Console.WriteLine("Conversion complete! HTML saved to: " + outputHtml);
        }
    }
}
```

### Proč `RasterImages = false` funguje

- **Raster images** jsou bitmapové obrázky vložené do PDF (JPEG, PNG atd.). Když nastavíte `RasterImages` na `false`, Aspose jednoduše vynechá krok, který tyto bitmapy extrahuje a zapisuje do složky HTML.
- Zbytek PDF — písma, vektorové tvary, tabulky a informace o rozvržení — se stále převede do HTML/CSS, takže stránka vypadá *téměř* identicky, jen je lehčí.
- Tato volba je zvláště užitečná pro scénáře **convert pdf to html without images**, jako jsou SEO‑přátelské náhledy, úryvky e‑mailů nebo mobilně‑první návrhy, kde je šířka pásma důležitá.

## Krok za krokem: Převod PDF do HTML bez obrázků

### 1️⃣ Načtěte svůj PDF dokument

Používáme třídu `Document`, která v paměti analyzuje strukturu PDF. Žádná další konfigurace není potřeba, pokud nepracujete s šifrovanými soubory.

### 2️⃣ Upravit možnosti uložení

`HtmlSaveOptions` je flexibilní kontejner. Kromě `RasterImages` můžete také upravit `SplitIntoPages`, `EmbedFonts` nebo `CssStyleSheetType`. Pro náš účel stačí jediný řádek `RasterImages = false`, který udělá veškerou těžkou práci.

### 3️⃣ Zapsat HTML

Metoda `Save` zapíše jeden HTML soubor (plus složku pro případné pomocné zdroje, jako je CSS). Protože jsme zakázali rastrové obrázky, složka se zdroji bude prázdná nebo bude obsahovat jen soubory CSS.

### Očekávaný výsledek

Otevřete `NoImages.html` v prohlížeči. Měli byste vidět:

- Všechna nadpisy, odstavce a tabulky zachovány.
- Žádné značky `<img>` odkazující na soubory JPEG/PNG.
- Mnohem menší velikost souboru — často **70‑90 % úspora** oproti exportu s obrázky.

Pokud stránku porovnáte bok po boku s HTML verzí, která obsahuje obrázky, rozvržení bude prakticky identické, jen chybí vizuální obsah.

## Časté problémy a tipy pro profesionály

- **Chybějící písma?** Pokud PDF používá vlastní písma, nastavte `htmlOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll`, aby se text vykresloval správně.
- **Vektorová grafika stále viditelná:** Aspose převádí vektorová kresby na SVG. Pokud opravdu potřebujete výstup *pouze s textem*, můžete také nastavit `htmlOptions.VectorGraphics = false`.
- **Velké PDF:** U masivních dokumentů zvažte streamování PDF (`Document.Load(stream)`), abyste se vyhnuli načítání celého souboru do paměti.
- **Cesty k souborům:** Používejte `Path.Combine` pro bezpečnost napříč platformami, zejména pokud později cílíte na Linux kontejnery.

## Kompletní funkční příklad – shrnutí

Zde je celý program znovu, tentokrát s malým ošetřením chyb pro větší robustnost:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.HtmlSaveOptions;

namespace PdfToHtmlNoImages
{
    class Program
    {
        static void Main()
        {
            try
            {
                string sourcePdf = Path.Combine(Environment.CurrentDirectory, "HeavyImages.pdf");
                string outputHtml = Path.Combine(Environment.CurrentDirectory, "NoImages.html");

                Document pdfDocument = new Document(sourcePdf);

                HtmlSaveOptions htmlOptions = new HtmlSaveOptions
                {
                    RasterImages = false,
                    // Optional: keep vector graphics if you need them
                    // VectorGraphics = false
                };

                pdfDocument.Save(outputHtml, htmlOptions);
                Console.WriteLine($"✅ Success! HTML saved to {outputHtml}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Conversion failed: {ex.Message}");
            }
        }
    }
}
```

Spusťte jej, otevřete vzniklé HTML a okamžitě uvidíte výhodu **přeskočení exportu obrázků**.

## Co dál? Rozšíření pracovního postupu

Nyní, když umíte **převést PDF do HTML bez obrázků**, můžete chtít:

- **Post‑process HTML** a vložit lazy‑loaded zástupce tam, kde byly obrázky odstraněny.
- **Kombinovat s headless prohlížečem** (např. Puppeteer) a z HTML znovu generovat PDF — užitečné pro vytvoření „pouze‑textové“ verze originálu.
- **Integrovat do webového API**, aby uživatelé mohli nahrávat PDF a okamžitě získávat odlehčené HTML náhledy.

Všechny tyto scénáře staví na stejném základním principu: ovládejte `HtmlSaveOptions`, abyste výstup přizpůsobili svým potřebám.

---

*Šťastné programování! Pokud narazíte na potíže, zanechte komentář níže a společně je vyřešíme.*

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vlastních projektech.

- [Převod PDF do HTML v .NET pomocí Aspose.PDF bez ukládání obrázků](/pdf/english/net/conversion-export/convert-pdf-html-net-asposepdf-no-images/)
- [Konverze PDF do HTML pomocí Aspose.PDF .NET: Uložit obrázky jako externí PNG](/pdf/english/net/conversion-export/pdf-to-html-conversion-external-png-aspose-pdf-net/)
- [Převod PDF do HTML v .NET s vlastními cestami k obrázkům pomocí Aspose.PDF](/pdf/english/net/conversion-export/convert-pdf-html-custom-image-paths-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}