---
category: general
date: 2026-08-14
description: Jak nastavit možnosti Batesova číslování v C# pomocí GroupDocs. Postupujte
  podle tohoto krok‑za‑krokem tutoriálu a přidejte vlastní předpony a počáteční čísla
  při převodu Wordu do PDF.
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
language: cs
lastmod: 2026-08-14
og_description: Jak rychle nastavit možnosti Batesova číslování v C#. Tento průvodce
  vám ukáže, jak přidat vlastní předpony a počáteční čísla při převodu Wordu do PDF.
og_image_alt: Screenshot of C# code applying Bates numbering to a PDF
og_title: Jak nastavit možnosti Bates číslování v C# – krok za krokem tutoriál
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
title: Jak nastavit možnosti Batesova číslování v C# – kompletní průvodce
url: /cs/net/programming-with-stamps-and-watermarks/how-to-set-bates-numbering-options-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak nastavit možnosti Bates číslování v C# – kompletní průvodce

Pokud potřebujete **jak nastavit možnosti Bates číslování** v C#, tento průvodce vás provede přesnými kroky. Naučíte se, jak nastavit počáteční číslo, přidat předponu a aplikovat číslování při převodu dokumentu Word do PDF pomocí GroupDocs API.

Zpracování dokumentů často vyžaduje jedinečné identifikátory na každé stránce pro právní nebo archivní účely. Na konci tohoto tutoriálu budete mít znovupoužitelný úryvek, který můžete vložit do libovolného .NET projektu, ať už vytváříte nástroj pro podporu soudních řízení nebo automatizovaný generátor zpráv. Nejsou potřeba žádné externí nástroje – stačí knihovna GroupDocs.Conversion a několik řádků C#.

## Co budete potřebovat

* .NET 6.0 SDK nebo novější nainstalované  
* Visual Studio 2022 (nebo jakékoli IDE podporující .NET)  
* Platná licence GroupDocs.Conversion (bezplatná zkušební verze funguje pro testování)  
* Ukázkový dokument Word (`input.docx`), který chcete očíslovat  

Tyto předpoklady zajišťují, že kód poběží bez další konfigurace.

## Přehled nastavení možností Bates číslování

Jádro **nastavení možností Bates číslování** spočívá ve třech objektech:

1. `Document` – načte zdrojový soubor.  
2. `BatesNumberingOptions` – obsahuje počáteční číslo, předponu a další podrobnosti formátování.  
3. `AddBatesNumbering` – metoda, která vloží číslování na každou stránku.  

Pochopení, proč každá část existuje, vám pomůže přizpůsobit řešení složitějším scénářům, jako jsou vlastní fonty nebo vícejazyčné číslování.

## Krok 1: Instalace NuGet balíčku GroupDocs.Conversion

Otevřete terminál ve složce řešení a spusťte:

```bash
dotnet add package GroupDocs.Conversion
```

**GroupDocs API** poskytuje třídu `Document` a rozšiřující metodu `AddBatesNumbering`, která je použita později v tutoriálu.

## Krok 2: Načtení zdrojového dokumentu

```csharp
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;

// Step 2: Load the source Word document
Document document = new Document(@"C:\Docs\input.docx");
```

*Proč tento krok?*  
Načtení souboru vytvoří v paměti reprezentaci, kterou může převodový engine manipulovat. Bez instance `Document` nemůžete aplikovat Bates číslování ani žádnou jinou transformaci.

## Krok 3: Vytvoření možností Bates číslování

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

*Proč tento krok?*  
`BatesNumberingOptions` zapouzdřuje všechna nastavení, která můžete potřebovat při **nastavování možností Bates číslování**. Úprava `StartNumber` a `Prefix` vám umožní sladit výstup s vaším systémem správy případů. Vlastnost `Position` řídí vizuální umístění, což je často požadavek na shodu.

## Krok 4: Aplikace Bates číslování na dokument

```csharp
// Step 4: Apply the numbering to every page
document.AddBatesNumbering(batesOptions);
```

Metoda `AddBatesNumbering` prochází každou stránku načteného `Document` a vloží nakonfigurovaný řetězec. Protože metoda pracuje s paměťovou reprezentací, můžete před uložením řetězit další kroky zpracování (např. vodoznak).

## Krok 5: Převod a uložení výsledku jako PDF

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

*Proč tento krok?*  
Ukládání jako PDF je běžný finální formát pro právní dokumenty. Objekt `PdfConvertOptions` vám umožní jemně doladit výstup, ale není vyžadován pro základní číslování. Volání `Save` zapíše plně očíslované PDF na disk.

## Kompletní, spustitelný příklad

Spojením všech částí získáte samostatnou konzolovou aplikaci, kterou můžete zkompilovat a spustit:

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

**Očekávaný výstup**

Spuštěním programu se vytvoří `output.pdf`, kde každá stránka zobrazuje štítek jako `CASE-1000`, `CASE-1001` atd., umístěný v pravém zápatí. Otevřete PDF v libovolném prohlížeči a ověřte, že čísla jsou zobrazená podle očekávání.

## Časté úskalí a osvědčené postupy

| Issue | Why it happens | How to avoid it |
|-------|----------------|-----------------|
| **Relativní cesty způsobují `FileNotFoundException`** | Pracovní adresář konzolové aplikace se může lišit od toho ve Visual Studiu. | Používejte absolutní cesty nebo `Path.Combine(AppContext.BaseDirectory, "input.docx")`. |
| **Číslování překrývá existující zápatí** | Pokud má zdrojový dokument již obsah v zvoleném prostoru zápatí, může být nové číslo skryté. | Zvolte jinou `Position` (např. `HeaderLeft`) nebo upravte šablonu zdroje. |
| **Velké dokumenty jsou pomalé** | Bates číslování prochází každou stránku; spotřeba paměti roste s velikostí souboru. | Zpracovávejte dokument po částech pomocí `Document.Split`, pokud překročíte 500 stránek. |
| **Vypršení licence** | Bezplatná zkušební verze GroupDocs vyprší po 30 dnech, což způsobí výjimku při `AddBatesNumbering`. | Použijte platný licenční klíč před načtením dokumentu: `License license = new License(); license.SetLicense("license.lic");`. |

**Tip:** Pokud potřebujete pro každý případ jiný formát čísla (např. `2023-CASE-001`), vytvořte předponu dynamicky před vytvořením `BatesNumberingOptions`.

## Rozšíření řešení

Stejný přístup **Bates číslování C#** funguje s dalšími zdrojovými formáty, jako jsou `.txt`, `.html` nebo dokonce obrázky. Stačí změnit příponu souboru při vytváření objektu `Document` a převodový engine se postará o zbytek.

Můžete také kombinovat **konverzi dokumentů C#** s OCR pro naskenovaná PDF:

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

## Závěr

Nyní víte **jak nastavit možnosti Bates číslování** v C# od začátku až do konce. Vytvořením objektu `BatesNumberingOptions`, jeho aplikací pomocí `AddBatesNumbering` a uložením výsledku jako PDF můžete automatizovat tvorbu právně vyhovujících, jedinečně identifikovaných dokumentů.

Odtud můžete zkoumat související témata, jako je **generování PDF v C#**, **konverze dokumentů C#**, nebo pokročilé funkce **GroupDocs API**, jako jsou vodoznaky a digitální podpisy. Experimentujte s různými předponami, pozicemi a formáty čísel, aby vyhovovaly vašemu workflow.

Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Přidání Bates číslování PDF v C# – Kompletní průvodce](/pdf/english/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/)
- [Jak přidat a přizpůsobit číslování stránek v PDF pomocí Aspose.PDF pro .NET | Průvodce manipulací s dokumenty](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Jak přidat textový razítkový zápatí v PDF pomocí Aspose.PDF pro .NET&#58; Průvodce krok za krokem](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}