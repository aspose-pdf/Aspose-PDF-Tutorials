---
category: general
date: 2026-09-27
description: Přidejte Batesovo číslování do PDF pomocí Aspose.PDF v C#. Naučte se,
  jak načíst PDF dokument, nastavit možnosti Batesova číslování a uložit aktualizovaný
  soubor.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- load pdf document
- how to add bates numbering
- Aspose.PDF C#
- PDF Bates numbering example
language: cs
lastmod: 2026-09-27
og_description: Přidejte Batesovo číslování do PDF pomocí Aspose.PDF v C#. Tento tutoriál
  vám ukáže, jak načíst PDF dokument, nakonfigurovat Batesovo číslování a uložit výsledek.
og_image_alt: Screenshot of a PDF page displaying Bates numbers in the footer
og_title: Přidejte číslování Bates do PDF pomocí Aspose.PDF – průvodce pro C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Add bates numbering to PDF using Aspose.PDF in C#. Learn how to load
    a PDF document, set Bates numbering options, and save the updated file.
  headline: Add bates numbering to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF processing
title: Přidat Batesovo číslování do PDF pomocí Aspose.PDF v C#
url: /cs/net/programming-with-text/add-bates-numbering-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidání Bates číslování do PDF pomocí Aspose.PDF v C#

Pokud potřebujete **přidat Bates číslování** do PDF souboru, tento návod vám ukáže kompletní, připravené řešení. Uvidíte, jak **načíst PDF dokument**, nakonfigurovat možnosti Bates číslování a zapsat očíslovaný soubor zpět na disk — vše pomocí Aspose.PDF pro .NET.

Používání Bates čísel je běžné v právních, policejních a archivních pracovních postupech. Na konci tohoto tutoriálu budete schopni vložit sekvenční identifikátor na každou stránku, přizpůsobit předponu a začít číslování od libovolného čísla.

## Co se naučíte

* Jak **načíst obsah PDF dokumentu** do objektu `Aspose.Pdf.Document`.  
* Přesné kroky **jak přidat Bates číslování** pomocí `BatesNumberingOptions`.  
* Jak uložit upravený soubor při zachování původního rozložení a kvality.  

Nejsou vyžadovány žádné externí nástroje — stačí balíček Aspose.PDF NuGet a .NET vývojové prostředí (Visual Studio, VS Code nebo Rider).  

---

## Krok 1: Instalace Aspose.PDF pro .NET

Otevřete složku projektu v terminálu a spusťte:

```bash
dotnet add package Aspose.PDF
```

Balíček obsahuje obor názvů `Aspose.Pdf`, který poskytuje všechny třídy použité v tomto tutoriálu. Po instalaci znovu načtěte projekt, aby IDE načetlo novou referenci.

## Krok 2: Načtení PDF dokumentu

Načtení zdrojového souboru je první operací, protože motor Bates číslování pracuje s existující instancí `Document`.

```csharp
using Aspose.Pdf;

// ...

// Replace with the path to your input PDF
string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Load the PDF document into memory
Document doc = new Document(inputPath);
```

**Proč je to důležité:** Třída `Document` parsuje strukturu PDF, poskytuje vám přístup ke stránkám, anotacím a metadatům. Bez předchozího načtení souboru nemůžete aplikovat žádné číslování.

## Krok 3: Konfigurace možností Bates číslování

Vytvořte objekt `BatesNumberingOptions` a nastavte požadovanou předponu, počáteční číslo a volitelné parametry formátování.

```csharp
using Aspose.Pdf;

// ...

BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Text that appears before the numeric part
    Prefix = "CASE01",

    // First number to use (1 means the first page gets CASE01-1)
    StartNumber = 1,

    // Optional: customize the appearance
    // The default places the number in the footer, centered.
    // You can change Font, FontSize, Color, and Position if needed.
    // Example:
    // Font = FontRepository.FindFont("Arial"),
    // FontSize = 10,
    // Color = Color.Black,
    // Margin = new Margin(0, 0, 0, 20)
};
```

**Proč je to důležité:** `BatesNumberingOptions` říká Aspose.PDF, jak generovat štítek pro každou stránku. `Prefix` vám pomáhá seskupit související případy, zatímco `StartNumber` vám umožní pokračovat v sekvenci z předchozí dávky.

## Krok 4: Uložení PDF s aplikovaným Bates číslováním

Předávejte objekt s možnostmi metodě `Save`. Aspose.PDF zapisuje čísla přímo na každou stránku.

```csharp
// Replace with the desired output path
string outputPath = @"YOUR_DIRECTORY\output.pdf";

// Save the document, applying the Bates numbering
doc.Save(outputPath, batesOptions);
```

**Proč je to důležité:** Přetížení `Save(string, BatesNumberingOptions)` kombinuje krok renderování s procesem číslování, což zajišťuje, že výstupní soubor obsahuje viditelné identifikátory.

## Kompletní příklad – vše dohromady

Níže je jednorázový, samostatný program, který můžete zkopírovat, vložit a spustit. Ukazuje **jak přidat Bates číslování** od začátku až do konce.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the PDF document
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Set up Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                Prefix = "CASE01",
                StartNumber = 1,
                // Optional appearance tweaks:
                // Font = FontRepository.FindFont("Times New Roman"),
                // FontSize = 9,
                // Color = Color.DarkBlue,
                // Margin = new Margin(0, 0, 0, 15)
            };

            // 3️⃣ Save the document with Bates numbers
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath, batesOptions);

            Console.WriteLine($"Bates numbering added. Output saved to: {outputPath}");
        }
    }
}
```

### Očekávaný výstup

Spuštěním programu vznikne `output.pdf`, kde každá stránka zobrazí štítek podobný:

```
CASE01-1
CASE01-2
CASE01-3
...
```

Čísla se ve výchozím nastavení zobrazují v patičce, ale můžete je přesunout úpravou vlastnosti `Margin` v `BatesNumberingOptions`.

## Okrajové případy a běžné varianty

| Situace | Co upravit |
|-----------|----------------|
| **Různá předpona pro každou dávku** | Změňte `Prefix` před voláním `Save`. Můžete iterovat přes více dokumentů s odlišnými předponami. |
| **Pokračovat v číslování z předchozího souboru** | Nastavte `StartNumber` na poslední použité číslo + 1. |
| **Umístit čísla do hlavičky** | Použijte `batesOptions.Margin = new Margin(20, 0, 0, 0);` (horní okraj) nebo přizpůsobte `batesOptions.Position`. |
| **Vlastní font nebo barva** | Přiřaďte vlastnosti `Font`, `FontSize` a `Color` podle ukázky v komentované sekci. |
| **Velké PDF (1000+ stránek)** | Operace je paměťově úsporná; nicméně můžete před uložením povolit `doc.OptimizeResources()`, aby se snížila velikost souboru. |

**Tip:** Pokud váš pracovní postup vyžaduje různé schémata číslování pro každý dokument, zabalte logiku do pomocné metody:

```csharp
static void ApplyBatesNumbering(string src, string dst, string prefix, int start)
{
    var doc = new Document(src);
    var opts = new BatesNumberingOptions { Prefix = prefix, StartNumber = start };
    doc.Save(dst, opts);
}
```

## Závěr

Nyní víte **jak přidat Bates číslování** do libovolného PDF pomocí Aspose.PDF v C#. Tutoriál pokryl načtení PDF dokumentu, konfiguraci možností číslování a uložení finálního souboru — vše v jednom spustitelném programu.

Odtud můžete zkoumat související témata, jako je **přidávání vodoznaků**, **sloučení více PDF** nebo **extrakce textu** pomocí Aspose.PDF. Experimentujte s různými fonty, barvami a pozicemi, aby odpovídaly formátovacím standardům vaší organizace.

Jste připraveni automatizovat svůj právní dokumentační workflow? Přidejte kód do vašeho build pipeline, spusťte jej na dávkách souborů a nechte Aspose.PDF udělat těžkou práci. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Vytvoření PDF dokumentu C# – Přidání Bates číslování](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/)
- [Přidání Bates číslování PDF – Průvodce krok za krokem číslování PDF stránek](/pdf/english/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/)
- [Aspose PDF tutoriál – Vložení prázdné stránky a aktualizace Bates číslování](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}