---
"description": "Naučte se, jak pomocí tohoto podrobného návodu použít různé styly číslování (římské číslice, abecední) na nadpisy v PDF pomocí Aspose.PDF pro .NET."
"linktitle": "Použít styl čísla v souboru PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Použít styl čísla v souboru PDF"
"url": "/cs/net/programming-with-headings/apply-number-style/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Použít styl čísla v souboru PDF

## Zavedení

Už jste někdy zjistili, že potřebujete do svých PDF dokumentů přidat krásně číslované seznamy? Ať už formátujete právní dokumenty, zprávy nebo prezentace, správné styly číslování jsou nezbytné pro organizaci informací. S Aspose.PDF pro .NET můžete na nadpisy PDF souborů použít různé styly číslování a vytvořit tak dobře strukturované a profesionální dokumenty. 

## Předpoklady

Než se pustíme do kódování, pojďme si projít, co budete potřebovat:

1. Aspose.PDF pro .NET: Stáhněte si nejnovější verzi souboru Aspose.PDF z [zde](https://releases.aspose.com/pdf/net/).
2. Vývojové prostředí: Ujistěte se, že máte Visual Studio nebo jakékoli jiné IDE kompatibilní s .NET.
3. .NET Framework: Ujistěte se, že máte nainstalovaný .NET Framework 4.0 nebo vyšší.
4. Licence: Můžete použít dočasnou licenci od [zde](https://purchase.aspose.com/temporary-license/) nebo prozkoumejte [bezplatná zkušební verze](https://releases.aspose.com/) možnosti.

## Importovat balíčky

Chcete-li začít, ujistěte se, že máte v projektu importovány následující jmenné prostory:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

## Krok 1: Nastavení dokumentu

Začněme vytvořením nového PDF dokumentu a konfigurací jeho nastavení stránek. Nastavíme velikost stránky a okraje pro řízení rozvržení našeho obsahu.

Vysvětlení: V tomto kroku nastavujeme základní strukturu PDF, která zahrnuje definování velikosti stránky, výšky a okrajů pro konzistentní formátování.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document pdfDoc = new Document();

// Nastavení rozměrů a okrajů stránky
pdfDoc.PageInfo.Width = 612.0;
pdfDoc.PageInfo.Height = 792.0;
pdfDoc.PageInfo.Margin = new Aspose.Pdf.MarginInfo();
pdfDoc.PageInfo.Margin.Left = 72;
pdfDoc.PageInfo.Margin.Right = 72;
pdfDoc.PageInfo.Margin.Top = 72;
pdfDoc.PageInfo.Margin.Bottom = 72;
```

Tímto způsobem bude mít váš dokument standardní velikost stránky, ekvivalentní stránce o rozměrech 8,5 x 11 palců, a okraj 72 bodů (nebo 1 palec) na všech stranách.

## Krok 2: Přidání stránky do PDF

Dále přidáme do dokumentu PDF novou stránku, na kterou později použijeme styly číslování.

Vysvětlení: Každý PDF soubor vyžaduje stránky! Tento krok přidá do PDF prázdnou stránku a nastaví její okraje tak, aby odpovídaly nastavení na úrovni dokumentu.

```csharp
// Přidání nové stránky do dokumentu PDF
Aspose.Pdf.Page pdfPage = pdfDoc.Pages.Add();
pdfPage.PageInfo.Width = 612.0;
pdfPage.PageInfo.Height = 792.0;
pdfPage.PageInfo.Margin = new Aspose.Pdf.MarginInfo();
pdfPage.PageInfo.Margin.Left = 72;
pdfPage.PageInfo.Margin.Right = 72;
pdfPage.PageInfo.Margin.Top = 72;
pdfPage.PageInfo.Margin.Bottom = 72;
```

## Krok 3: Vytvořte plovoucí rámeček

Plovoucí pole (FloatingBox) umožňuje umístit obsah (například text nebo nadpisy) do rámečku, který se chová nezávisle na toku stránky. To je užitečné, když chcete mít úplnou kontrolu nad rozvržením obsahu.

Vysvětlení: Zde nastavujeme FloatingBox, který bude obsahovat nadpisy, na které budou použity styly čísel.

```csharp
// Vytvořte FloatingBox pro strukturovaný obsah
Aspose.Pdf.FloatingBox floatBox = new Aspose.Pdf.FloatingBox();
floatBox.Margin = pdfPage.PageInfo.Margin;
pdfPage.Paragraphs.Add(floatBox);
```

## Krok 4: Přidejte první nadpis s římskými číslicemi

A teď přichází ta vzrušující část! Přidejme první nadpis s malými římskými číslicemi.

Vysvětlení: Na nadpis aplikujeme styl NumberingStyle.NumeralsRomanLowercase, který bude zobrazovat číslování římskými číslicemi (i, ii, iii atd.).

```csharp
// Vytvořte první nadpis pomocí římských číslic
Aspose.Pdf.Heading heading = new Aspose.Pdf.Heading(1);
heading.IsInList = true;
heading.StartNumber = 1;
heading.Text = "List 1";
heading.Style = NumberingStyle.NumeralsRomanLowercase;
heading.IsAutoSequence = true;
floatBox.Paragraphs.Add(heading);
```

## Krok 5: Přidejte druhý nadpis s římskými číslicemi

Pro demonstrační účely přidejme druhý nadpis s římskými číslicemi, ale tentokrát začneme od 13.

Vysvětlení: Vlastnost StartNumber umožňuje začít číslování od vlastního čísla – v tomto případě začínáme od 13.

```csharp
// Vytvořte druhý nadpis začínající římskou číslicí 13
Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
heading2.IsInList = true;
heading2.StartNumber = 13;
heading2.Text = "List 2";
heading2.Style = NumberingStyle.NumeralsRomanLowercase;
heading2.IsAutoSequence = true;
floatBox.Paragraphs.Add(heading2);
```

## Krok 6: Přidání nadpisu s abecedním číslováním

Pro zpestření přidejme třetí nadpis, ale tentokrát použijeme abecední číslování malými písmeny (a, b, c atd.).

Vysvětlení: Změna stylu číslování na LettersLowercase nám umožňuje použít abecední číslování pro naše nadpisy.

```csharp
// Vytvořte nadpis s abecedním číslováním
Aspose.Pdf.Heading heading3 = new Aspose.Pdf.Heading(2);
heading3.IsInList = true;
heading3.StartNumber = 1;
heading3.Text = "the value, as of the effective date of the plan, of property to be distributed under the plan on account of each allowed";
heading3.Style = NumberingStyle.LettersLowercase;
heading3.IsAutoSequence = true;
floatBox.Paragraphs.Add(heading3);
```

## Krok 7: Uložení PDF souboru

Nakonec, po použití všech stylů nadpisů a číslování, uložme soubor PDF do požadovaného adresáře.

Vysvětlení: Tento krok uloží soubor PDF obsahující všechny formátované nadpisy s použitými styly číslování.

```csharp
// Uložit dokument PDF
dataDir = dataDir + "ApplyNumberStyle_out.pdf";
pdfDoc.Save(dataDir);
Console.WriteLine("\nNumber style applied successfully in headings.\nFile saved at " + dataDir);
```

## Závěr

A tady to máte! Úspěšně jste aplikovali styly číslování – římské číslice a abecední – na nadpisy v souboru PDF pomocí Aspose.PDF pro .NET. Flexibilita, kterou Aspose.PDF nabízí pro ovládání rozvržení stránky, stylů číslování a umístění obsahu, vám poskytuje výkonnou sadu nástrojů pro vytváření dobře organizovaných a profesionálních dokumentů PDF.

## Často kladené otázky

### Mohu na stejný dokument PDF použít různé styly číslování?  
Ano, Aspose.PDF pro .NET umožňuje kombinovat různé styly číslování, jako jsou římské číslice, arabské číslice a abecední číslování v rámci jednoho dokumentu.

### Jak mohu přizpůsobit počáteční číslování pro nadpisy?  
Počáteční číslo pro libovolný nadpis můžete nastavit pomocí `StartNumber` vlastnictví.

### Existuje způsob, jak resetovat pořadí číslování?  
Ano, číslování můžete resetovat úpravou `StartNumber` vlastnost pro každý nadpis.

### Mohu kromě číslování použít na nadpisy tučné písmo nebo kurzívu?  
Rozhodně! Styly nadpisů si můžete přizpůsobit úpravou vlastností, jako je písmo, velikost, tučné písmo a kurzíva, pomocí `TextState` objekt.

### Jak získám dočasnou licenci pro Aspose.PDF?  
Dočasné povolení můžete získat od [zde](https://purchase.aspose.com/temporary-license/) otestovat Aspose.PDF bez omezení.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}