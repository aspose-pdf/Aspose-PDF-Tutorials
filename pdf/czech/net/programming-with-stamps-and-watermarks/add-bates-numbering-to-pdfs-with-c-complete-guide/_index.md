---
category: general
date: 2026-04-10
description: Přidejte Batesovo číslování do PDF pomocí C# během několika minut. Naučte
  se, jak přidat vlastní čísla stránek, jak číslovat PDF soubory a jak efektivně použít
  Batesovo číslování.
draft: false
keywords:
- add bates numbering
- add custom page numbers
- how to number pdf
- how to add bates
- apply bates numbering
language: cs
og_description: Přidejte Batesovo číslování do PDF pomocí C# během několika minut.
  Tento návod ukazuje, jak přidat vlastní čísla stránek, jak číslovat PDF soubory
  a jak krok za krokem aplikovat Batesovo číslování.
og_title: Přidejte Batesovo číslování do PDF pomocí C# – Kompletní průvodce
tags:
- PDF
- C#
- Bates numbering
title: Přidejte Batesovo číslování do PDF pomocí C# – Kompletní průvodce
url: /cs/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Přidání Bates Numbering do PDF pomocí C# – Kompletní průvodce

Už jste někdy potřebovali **add bates numbering** do PDF, ale nevedeli jste, kde začít? Nejste sami – právní týmy, auditoři a všichni, kteří pracují s velkými sadami dokumentů, tuto překážku potkávají pravidelně. Dobrá zpráva? Několika řádky C# můžete automaticky razítkovat každou stránku vlastním identifikátorem a také se naučíte **how to add custom page numbers**.

V tomto tutoriálu projdeme vše, co potřebujete: požadovaný NuGet balíček, nastavení možností číslování, aplikaci čísel a ověření výsledku. Na konci budete vědět **how to number PDF** soubory programově a budete připraveni upravit prefix, suffix, velikost písma nebo dokonce cílit na konkrétní stránky.

## Prerequisites

- .NET 6.0 nebo novější (kód funguje také s .NET Framework 4.7+)
- Visual Studio 2022 (nebo jakékoli IDE, které preferujete)
- Knihovna **Aspose.PDF for .NET** (bezplatná zkušební verze stačí pro učení)
- Vzorek PDF pojmenovaný `source.pdf` umístěný ve složce, kterou ovládáte

Pokud máte tyto položky zaškrtnuté, pojďme se ponořit dál.

## Step 1: Install and Reference Aspose.PDF

Nejprve přidejte balíček Aspose.PDF do svého projektu:

```bash
dotnet add package Aspose.PDF
```

Nebo použijte UI NuGet Package Manager. Po instalaci zahrňte jmenný prostor na začátek souboru:

```csharp
using Aspose.Pdf;
```

> **Tip:** Udržujte své balíčky aktuální; nejnovější verze (k dubnu 2026) přidává několik výkonových vylepšení pro velké dokumenty.

## Step 2: Open the Source PDF Document

Otevření souboru je jednoduché. Použijeme blok `using`, aby se souborový handle uvolnil automaticky.

```csharp
// Step 2: Open the source PDF document
using (var sourceDocument = new Document("YOUR_DIRECTORY/source.pdf"))
{
    // The rest of the workflow lives inside this block.
}
```

Třída `Document` představuje celý PDF, poskytuje nám přístup ke stránkám, anotacím a samozřejmě k Bates numbering.

## Step 3: Define Bates Numbering Settings

Nyní přichází jádro záležitosti – konfigurace možností **add bates numbering**. Můžete nastavit počáteční číslo, prefix, suffix, velikost písma, okraj a dokonce určit, které stránky obdrží razítko.

```csharp
// Step 3: Define Bates numbering settings
var batesOptions = new BatesNumberingOptions
{
    StartNumber = 1,                 // First number in the sequence
    Prefix = "ABC-",                 // Text before the number
    Suffix = "-2024",                // Text after the number
    FontSize = 12,                   // Size of the numbering font
    Margin = 10,                     // Distance from the page edge (points)
    PageNumbers = new[] { 1, 2, 3 }  // Pages to which numbering is applied
};
```

### Why These Settings Matter

- **StartNumber** vám umožní pokračovat v sekvenci z předchozí dávky.
- **Prefix/Suffix** jsou užitečné pro identifikátory případů nebo roční razítka.
- **FontSize** a **Margin** ovlivňují čitelnost; příliš malé písmo může být v tisku přehlédnuto.
- **PageNumbers** je místo, kde **apply bates numbering** selektivně. Vynechte toto pole, pokud chcete číslovat každou stránku.

Pokud potřebujete **add custom page numbers**, které nejsou sekvenční, můžete vytvořit seznam jako `{5, 10, 15}` a předat jej zde.

## Step 4: Apply the Bates Numbering to the Selected Pages

S připravenými možnostmi knihovna udělá těžkou práci. Metoda `AddBatesNumbering` vloží razítko na každou cílovou stránku.

```csharp
// Step 4: Apply the Bates numbering to the selected pages
sourceDocument.AddBatesNumbering(batesOptions);
```

Za scénou Aspose.PDF vytvoří textový fragment pro každou stránku, umístí jej podle okraje a respektuje zvolenou velikost písma. To zajišťuje, že čísla se objeví přesně tam, kde očekáváte, ať už PDF zobrazujete na obrazovce nebo jej tisknete.

## Step 5: Save the Modified Document

Nakonec uložte změny do nového souboru, aby originál zůstal nedotčený.

```csharp
// Step 5: Save the modified document with Bates numbers
sourceDocument.Save("YOUR_DIRECTORY/bates.pdf");
```

Nyní máte `bates.pdf` obsahující označené stránky. Otevřete jej v libovolném PDF prohlížeči a uvidíte něco jako:

```
ABC-1-2024   (on page 1, top‑right)
ABC-2-2024   (on page 2, top‑right)
ABC-3-2024   (on page 3, top‑right)
```

### Verifying the Result

Rychlá kontrola je programově přečíst text první stránky:

```csharp
using (var doc = new Document("YOUR_DIRECTORY/bates.pdf"))
{
    var text = doc.Pages[1].ExtractText();
    Console.WriteLine(text.Contains("ABC-1-2024") ? "Bates number applied!" : "Oops, something went wrong.");
}
```

Pokud konzole vypíše *Bates number applied!*, máte vše v pořádku.

## Edge Cases & Common Variations

| Situace | Co změnit | Důvod |
|-----------|----------------|--------|
| **Number every page** | Omit `PageNumbers` or set it to `null` | API ve výchozím nastavení čísluje všechny stránky, pokud pole není poskytnuto. |
| **Different margin per side** | Use `Margin = new MarginInfo { Top = 15, Right = 10 }` (requires Aspose > 23.3) | Poskytuje jemné řízení umístění. |
| **Large documents (> 500 pages)** | Enable `batesOptions.StartNumber` at a higher value and consider `batesOptions.FontSize = 10` to avoid overlap | Udržuje razítko čitelné bez překrývání stránky. |
| **Need a different font** | Set `batesOptions.Font = FontRepository.FindFont("Arial")` | Některé právní firmy vyžadují konkrétní typ písma. |

> **Pozor:** Pokud zadáte číslo stránky, které neexistuje (např. `PageNumbers = new[] { 999 }`), Aspose.PDF jej tiše přeskočí. Vždy ověřujte rozsah, pokud seznam vytváříte dynamicky.

## Full Working Example

Níže je kompletní, připravený k spuštění program. Vložte jej do konzolové aplikace, upravte cesty a stiskněte **F5**.

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // Adjust these paths to match your environment
        string sourcePath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        // Open the source PDF
        using (var sourceDocument = new Document(sourcePath))
        {
            // Configure Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1,
                Prefix = "ABC-",
                Suffix = "-2024",
                FontSize = 12,
                Margin = 10,
                PageNumbers = new[] { 1, 2, 3 } // Change or remove to number all pages
            };

            // Apply the numbering
            sourceDocument.AddBatesNumbering(batesOptions);

            // Save the new PDF
            sourceDocument.Save(outputPath);
        }

        // Verify the first page contains the expected stamp
        using (var doc = new Document(outputPath))
        {
            string extracted = doc.Pages[1].ExtractText();
            bool success = extracted.Contains("ABC-1-2024");
            Console.WriteLine(success
                ? "Bates numbering added successfully!"
                : "Numbering failed – check your options.");
        }
    }
}
```

Spuštěním tohoto kódu vytvoříte `bates.pdf` se třemi označenými stránkami zobrazenými dříve. Otevřete soubor a uvidíte čísla zarovnaná vpravo, 10 bodů od okraje, v 12‑bodovém písmu.

## Visual Preview

![add bates numbering preview](/images/bates-numbering-sample.png)

*Snímek obrazovky výše ukazuje, jak vypadá výstup **add bates numbering** po spuštění skriptu.*

## Conclusion

Právě jsme prošli, jak **add bates numbering** do PDF pomocí C#. Konfigurací `BatesNumberingOptions`, aplikací razítka a uložením dokumentu máte nyní opakovatelný řešení, které může také **add custom page numbers**, **how to number pdf** soubory a **apply bates numbering** v jakémkoli projektu.

Další kroky? Zkuste kombinovat toto s dávkovým procesorem, který prochází složku PDF, nebo experimentujte s různými prefixy pro každý typ případu. Můžete také prozkoumat sloučení více PDF po jejich číslování – užitečné pro tvorbu komplexních balíčků případů.

Máte otázky ohledně okrajových případů, nebo chcete vidět, jak vložit čísla do zápatí místo záhlaví? Zanechte komentář a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}