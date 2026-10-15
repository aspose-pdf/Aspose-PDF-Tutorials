---
title: Přizpůsobte pozadí, okraje a odsazení buněk tabulky v PDF pomocí Aspose.Pdf pro .NET
weight: 101
limit:
description: Naučte se, jak vytvořit PDF s dvousloupcovou tabulkou a aplikovat vlastní barvy pozadí, okraje a odsazení na každou buňku pomocí Aspose.Pdf pro .NET.
keywords: [Aspose.Pdf for .NET, style table cells pdf, pdf table cell background, pdf table cell border, pdf cell padding, Aspose PDF table styling]
url: /net/tables-lists/style-table-cells/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Naučte se, jak vytvořit PDF s dvousloupcovou tabulkou a aplikovat vlastní
    barvy pozadí, okraje a odsazení na každou buňku pomocí Aspose.Pdf pro .NET.
  headline: Přizpůsobte pozadí, okraje a odsazení buněk tabulky v PDF pomocí Aspose.Pdf
    pro .NET
  type: TechArticle
- description: Naučte se, jak vytvořit PDF s dvousloupcovou tabulkou a aplikovat vlastní
    barvy pozadí, okraje a odsazení na každou buňku pomocí Aspose.Pdf pro .NET.
  name: Přizpůsobte pozadí, okraje a odsazení buněk tabulky v PDF pomocí Aspose.Pdf
    pro .NET
  steps:
  - name: Vytvořte nový prázdný PDF dokument uvnitř bloku using.
    text: Vytvořte nový prázdný PDF dokument uvnitř bloku using.
  - name: Přidejte prázdnou stránku do PDF dokumentu.
    text: Přidejte prázdnou stránku do PDF dokumentu.
  - name: Vytvořte instanci objektu Table se dvěma sloupci o šířce 200 bodů, tenkým
      černým vnějším okrajem a výchozím odsazením buňky 5 bodů.
    text: Vytvořte instanci objektu Table se dvěma sloupci o šířce 200 bodů, tenkým
      černým vnějším okrajem a výchozím odsazením buňky 5 bodů.
  - name: Přidejte první řádek do tabulky.
    text: Přidejte první řádek do tabulky.
  - name: Vytvořte první buňku, vložte text "First cell", nastavte světle žluté pozadí,
      červený okraj o tloušťce 2 body a okraj (margin) 4 body.
    text: Vytvořte první buňku, vložte text "First cell", nastavte světle žluté pozadí,
      červený okraj o tloušťce 2 body a okraj (margin) 4 body.
  - name: Vytvořte druhou buňku, přidejte text "Second cell", nastavte světle zelené
      pozadí, modrý okraj o tloušťce 2 body a okraj 4 body.
    text: Vytvořte druhou buňku, přidejte text "Second cell", nastavte světle zelené
      pozadí, modrý okraj o tloušťce 2 body a okraj 4 body.
  - name: Přidejte druhý řádek do tabulky.
    text: Přidejte druhý řádek do tabulky.
  - name: Vytvořte třetí buňku, vložte "Third cell", nastavte světle azurové pozadí,
      tmavě šedý okraj o tloušťce 2 body a okraj 4 body.
    text: Vytvořte třetí buňku, vložte "Third cell", nastavte světle azurové pozadí,
      tmavě šedý okraj o tloušťce 2 body a okraj 4 body.
  - name: Vytvořte čtvrtou buňku, přidejte "Fourth cell", nastavte světle růžové pozadí,
      fialový okraj o tloušťce 2 body a okraj 4 body.
    text: Vytvořte čtvrtou buňku, přidejte "Fourth cell", nastavte světle růžové pozadí,
      fialový okraj o tloušťce 2 body a okraj 4 body.
  - name: Přidejte plně stylovanou tabulku na stránku, aby byla v PDF viditelná.
    text: Přidejte plně stylovanou tabulku na stránku, aby byla v PDF viditelná.
  - name: Uložte PDF dokument do souboru a uzavřete blok using.
    text: Uložte PDF dokument do souboru a uzavřete blok using.
  - name: Vytiskněte potvrzovací zprávu do konzole.
    text: Vytiskněte potvrzovací zprávu do konzole.
  type: HowTo
- questions:
  - answer: '`DefaultCellPadding` poskytuje základní odsazení pro každou buňku, ale
      pokud přiřadíte `Margin` (např. `cellA1.Margin = new MarginInfo(...)`), hodnoty
      marginu přepíšou výchozí odsazení pro danou buňku.'
    question: Ovlivňuje `DefaultCellPadding` nastavený na `Table` buňky, které mají
      také definovaný `Margin`?
  - answer: Bez `Table.Border` se vynechá vnější obdélník kolem celé tabulky; budou
      viditelné pouze jednotlivé okraje buněk, které nastavíte (např. `cellA2.Border`).
    question: Jak bude PDF vypadat, pokud odstraním vlastnost `Border` z objektu `Table`?
  - answer: Ano, vytvořte `BorderInfo` s konkrétním `BorderSide` (např. `new BorderInfo(BorderSide.Left,
      3, Aspose.Pdf.Color.Black)`) a přiřaďte jej k vlastnosti `Border` buňky.
    question: Mohu nastavit buňce různou šířku okraje na každé straně?
  - answer: Vytvořte novou instanci `Row` pomocí `Row newRow = dataTable.Rows.Add();`
      a poté přidejte buňky do `newRow.Cells` stejně jako u předchozích řádků.
    question: Jak mohu po zobrazeném kódu přidat třetí řádek do tabulky?
  type: FAQPage
images:
- /net/tables-lists/style-table-cells/og-image.png
og_title: Styling buněk PDF tabulky – pozadí, okraj, odsazení
og_description: Rychle formátujte buňky tabulky v PDF pomocí vlastních barev, okrajů a rozestupů s Aspose.Pdf pro .NET.
og_image_alt: Příručka ukazující, jak stylovat barvu pozadí, okraj a odsazení buněk tabulky v PDF pomocí Aspose.Pdf pro .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přizpůsobte pozadí, okraje a odsazení buněk tabulky v PDF pomocí Aspose.Pdf pro .NET
Cílem tohoto tutoriálu je ukázat, jak vytvořit PDF dokument, přidat dvousloupcovou tabulku a přesně řídit vzhled každé buňky. Nastavením barev pozadí, definováním okrajů a úpravou odsazení můžete zvýraznit data v tabulce a dosáhnout profesionálního vzhledu. Příklad používá třídy Aspose.Pdf Document a Table k demonstraci jednotlivých možností stylování.

---

{{< tutorial-widget sourcePath="pdf/net/tables-lists/style-table-cells" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: Ovlivňuje `DefaultCellPadding` nastavený na `Table` buňky, které mají také definovaný `Margin`?**  
A: `DefaultCellPadding` poskytuje základní odsazení pro každou buňku, ale pokud přiřadíte `Margin` (např. `cellA1.Margin = new MarginInfo(...)`), hodnoty marginu přepíšou výchozí odsazení pro danou buňku.

**Q: Jak bude PDF vypadat, pokud odstraním vlastnost `Border` z objektu `Table`?**  
A: Bez `Table.Border` se vynechá vnější obdélník kolem celé tabulky; budou viditelné pouze jednotlivé okraje buněk, které nastavíte (např. `cellA2.Border`).

**Q: Mohu nastavit buňce různou šířku okraje na každé straně?**  
A: Ano, vytvořte `BorderInfo` s konkrétním `BorderSide` (např. `new BorderInfo(BorderSide.Left, 3, Aspose.Pdf.Color.Black)`) a přiřaďte jej k vlastnosti `Border` buňky.

**Q: Jak mohu po zobrazeném kódu přidat třetí řádek do tabulky?**  
A: Vytvořte novou instanci `Row` pomocí `Row newRow = dataTable.Rows.Add();` a poté přidejte buňky do `newRow.Cells` stejně jako u předchozích řádků.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}