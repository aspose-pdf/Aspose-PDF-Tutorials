---
"description": "Naučte se, jak stylovat buňky tabulky v PDF pomocí Aspose.PDF pro .NET v tomto podrobném návodu. Postupujte podle pokynů k vytvoření a formátování krásných tabulek v PDF."
"linktitle": "Buňka tabulky stylů"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Buňka tabulky stylů"
"url": "/cs/net/programming-with-tagged-pdf/style-table-cell/"
"weight": 160
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Buňka tabulky stylů

## Zavedení

Vytváření profesionálně vypadajících tabulek v PDF může být složité, ale s Aspose.PDF pro .NET je to překvapivě jednoduché! Ať už stylujete záhlaví, zápatí nebo konkrétní buňky tabulky, tato výkonná knihovna vám poskytne všechny nástroje, které potřebujete k vytváření krásně formátovaných dokumentů PDF. V tomto tutoriálu si ukážeme, jak stylovat buňky tabulky v dokumentu PDF pomocí Aspose.PDF pro .NET. Nebojte se – vše rozdělíme do snadno sledovatelných kroků.

## Předpoklady

Než se ponoříte do kódu, ujistěte se, že máte následující předpoklady:

1. Aspose.PDF pro .NET: Stáhněte a nainstalujte nejnovější verzi souboru Aspose.PDF z [zde](https://releases.aspose.com/pdf/net/).
2. IDE (jako Visual Studio): Nastavení vývojového prostředí .NET.
3. Základní znalost programování v C#: Je vyžadována určitá znalost jazyka C#.
4. Licence Aspose.PDF: Získejte dočasnou nebo plnou licenci pro odemknutí všech funkcí knihovny. Můžete získat bezplatnou zkušební verzi. [zde](https://purchase.aspose.com/temporary-license/).

## Importovat balíčky

Než začnete, nezapomeňte importovat potřebné jmenné prostory. Ve svém projektu budete potřebovat následující:

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Nyní, když je vše nastaveno, pojďme se pustit do podrobného návodu!

Vytvoříme tabulku v dokumentu PDF a upravíme její buňky. Každý krok bude podrobně vysvětlen.

## Krok 1: Vytvořte nový dokument PDF

Prvním krokem je vytvoření nového PDF dokumentu. V souboru Aspose.PDF můžete inicializovat nový `Document` objekt, který představuje váš PDF soubor.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Vytvořte nový PDF dokument
Document document = new Document();
ITaggedContent taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example table cell style");
taggedContent.SetLanguage("en-US");
```

Zde inicializujeme PDF dokument a nastavíme jeho název a jazyk. Tím dosáhnete správné struktury dokumentu, která je nezbytná pro shodu s PDF/UA.

## Krok 2: Nastavení struktury tabulky

Tabulky v PDF souborech jsou definovány v rámci strukturních prvků. Vytvořme tabulku a definujme její řádky a sloupce.

```csharp
// Získejte prvek kořenové struktury
StructureElement rootElement = taggedContent.RootElement;

// Vytvoření prvku struktury tabulky
TableElement tableElement = taggedContent.CreateTableElement();
rootElement.AppendChild(tableElement);
TableTHeadElement tableTHeadElement = tableElement.CreateTHead();
TableTBodyElement tableTBodyElement = tableElement.CreateTBody();
TableTFootElement tableTFootElement = tableElement.CreateTFoot();
```

Nyní jsme definovali záhlaví tabulky (`TableTHeadElement`), tělo (`TableTBodyElement`) a noha (`TableTFootElement`) sekce. Můžete si je představit jako kostru vaší tabulky.

## Krok 3: Stylizace buněk záhlaví

Stylizace buněk záhlaví je zvýrazní. Zde použijeme barvy pozadí, ohraničení a zarovnání textu.

```csharp
int colCount = 4;
TableTRElement headTrElement = tableTHeadElement.CreateTR();
headTrElement.AlternativeText = "Head Row";

for (int colIndex = 0; colIndex < colCount; colIndex++)
{
    TableTHElement thElement = headTrElement.CreateTH();
    thElement.SetText($"Head {colIndex}");
    thElement.BackgroundColor = Color.GreenYellow;
    thElement.Border = new BorderInfo(BorderSide.All, 4.0F, Color.Gray);
    thElement.IsNoBorder = true;
    thElement.Margin = new MarginInfo(16.0, 2.0, 8.0, 2.0);
    thElement.Alignment = HorizontalAlignment.Right;
}
```

V tomto kroku projdeme každou buňku záhlaví a přiřadíme jí zelenožluté pozadí, šedý okraj a text zarovnaný vpravo. Tyto vlastnosti můžete upravit tak, aby odpovídaly požadovanému designu.

## Krok 4: Naplnění a stylování těla tabulky

Tělo tabulky obsahuje skutečná data. Zde je návod, jak můžete každou buňku stylovat pomocí specifických okrajů, ohraničení a nastavení textu.

```csharp
int rowCount = 4;

for (int rowIndex = 0; rowIndex < rowCount; rowIndex++)
{
    TableTRElement trElement = tableTBodyElement.CreateTR();
    trElement.AlternativeText = $"Row {rowIndex}";

    for (int colIndex = 0; colIndex < colCount; colIndex++)
    {
        TableTDElement tdElement = trElement.CreateTD();
        tdElement.SetText($"Cell [{rowIndex}, {colIndex}]");
        tdElement.BackgroundColor = Color.Yellow;
        tdElement.Border = new BorderInfo(BorderSide.All, 4.0F, Color.Gray);
        tdElement.Margin = new MarginInfo(8.0, 2.0, 8.0, 2.0);
        tdElement.Alignment = HorizontalAlignment.Center;
        
        TextState cellTextState = new TextState();
        cellTextState.ForegroundColor = Color.DarkBlue;
        cellTextState.FontSize = 7.5F;
        cellTextState.FontStyle = FontStyles.Bold;
        cellTextState.Font = FontRepository.FindFont("Arial");
        tdElement.DefaultCellTextState = cellTextState;
    }
}
```

V tomto kroku vyplníme tělo tabulky čtyřmi řádky a každou buňku upravíme žlutým pozadím a vycentrovaným tučným modrým textem. Použijeme také `MarginInfo` třída pro definování odsazení kolem textu.

## Krok 5: Styl zápatí

Abychom tabulce dodali úplnou strukturu, přidáme a upravíme styl buněk zápatí, stejně jako jsme to udělali u záhlaví.

```csharp
TableTRElement footTrElement = tableTFootElement.CreateTR();
footTrElement.AlternativeText = "Foot Row";

for (int colIndex = 0; colIndex < colCount; colIndex++)
{
    TableTDElement tdElement = footTrElement.CreateTD();
    tdElement.SetText($"Foot {colIndex}");
}
```

Zápatí je stylizováno podobně jako záhlaví, což čtenářům usnadňuje sledování struktury tabulky.

## Krok 6: Uložení a ověření dokumentu PDF

Nakonec uložíme PDF dokument a zkontrolujeme, zda je kompatibilní s PDF/UA.

```csharp
// Uložení tagovaného dokumentu PDF
document.Save(dataDir + "StyleTableCell.pdf");

// Kontrola shody s PDF/UA
document = new Document(dataDir + "StyleTableCell.pdf");
bool isPdfUaCompliance = document.Validate(dataDir + "StyleTableCell.xml", PdfFormat.PDF_UA_1);
Console.WriteLine($"PDF/UA compliance: {isPdfUaCompliance}");
```

Uložíme PDF a použijeme `Validate` metodu, která zajistí, že splňuje standardy přístupnosti (soulad s PDF/UA).

## Závěr

Stylizace tabulek v PDF pomocí Aspose.PDF pro .NET je výkonná i flexibilní. S několika řádky kódu můžete vytvořit vlastní návrhy tabulek, díky nimž vaše PDF dokumenty vyniknou. Od úpravy okrajů buněk a pozadí až po zajištění shody s pravidly přístupnosti, Aspose.PDF usnadňuje vytváření propracovaných PDF souborů.

## Často kladené otázky

### Mohu na jednotlivé buňky tabulky použít různé styly?  
Ano, můžete upravovat styl jednotlivých buněk přizpůsobením `TableTDElement` vlastnosti.

### Jak mohu sloučit buňky tabulky?  
Můžete použít `ColSpan` a `RowSpan` vlastnosti pro sloučení buněk v tabulce.

### Je možné vytvořit tabulku kompatibilní s PDF/UA?  
Ano, jak je ukázáno v této příručce, můžete zajistit soulad s PDF/UA ověřením dokumentu pomocí `Validate` metoda.

### Mohu v buňkách tabulky použít různá písma?  
Rozhodně! Můžete zadat různá písma pomocí `TextState` objekt pro každou buňku.

### Jak si stáhnu soubor Aspose.PDF pro .NET?  
Můžete si ho stáhnout z [stránka s vydáními](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}