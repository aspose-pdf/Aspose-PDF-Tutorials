---
"description": "Naučte se, jak vytvořit a stylovat prvek tabulky v Aspose.PDF pro .NET s podrobnými pokyny, vlastním stylováním a kompatibilitou s PDF/UA."
"linktitle": "Prvek tabulky stylů"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Prvek tabulky stylů"
"url": "/cs/net/programming-with-tagged-pdf/style-table-element/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Prvek tabulky stylů

## Zavedení

tomto článku se ponoříme do toho, jak vytvořit a stylovat prvek tabulky pomocí Aspose.PDF pro .NET. Naučíte se, jak strukturovat tabulku, používat vlastní styly a ověřit shodu dokumentu s PDF/UA. Po absolvování tohoto tutoriálu budete schopni snadno vytvářet profesionálně vypadající tabulky ve svých PDF souborech!

## Předpoklady

Než se pustíte do tutoriálu, musíte se ujistit, že máte následující:

1. Visual Studio nebo podobné IDE nainstalované na vašem počítači.
2. .NET Framework nebo .NET Core SDK pro spuštění aplikace.
3. Knihovna Aspose.PDF pro .NET byla stažena a uvedena ve vašem projektu. Nejnovější verzi si můžete stáhnout z [zde](https://releases.aspose.com/pdf/net/).
4. Platná licence Aspose nebo [dočasná licence](https://purchase.aspose.com/temporary-license/) odemknout plnou funkčnost knihovny.

## Importovat balíčky

Pro začátek importujte potřebné jmenné prostory do projektu:

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Tyto jmenné prostory pokrývají základní operace s PDF, tagovaný obsah, tabulky a formátování textu.

Nyní si rozebereme proces vytváření a stylování tabulky v Aspose.PDF. Projdeme si každou část podrobně, abyste mohli lépe sledovat.

## Krok 1: Vytvořte nový dokument PDF a nastavte označený obsah

V tomto prvním kroku vytvoříme prázdný dokument PDF a nastavíme jeho označený obsah.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Vytvořte nový PDF dokument
Document document = new Document();

// Nastavení tagovaného obsahu
ITaggedContent taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example table style");
taggedContent.SetLanguage("en-US");
```

Začneme vytvořením nového `Document` objekt, který představuje náš PDF. `TaggedContent` Objekt se používá ke správě struktury dokumentu a zajišťuje soulad se standardy přístupnosti. Nastavujeme název a jazyk dokumentu pro správné tagování.

## Krok 2: Definování kořenového prvku

Dále vytvoříme kořenový strukturní element, který bude sloužit jako kontejner pro veškerý obsah v našem PDF.

```csharp
// Získejte prvek kořenové struktury
StructureElement rootElement = taggedContent.RootElement;
```

Ten/Ta/To `RootElement` slouží jako základní kontejner pro všechny strukturované prvky, včetně naší tabulky. Pomáhá udržovat strukturální hierarchii dokumentu, což je důležité jak pro organizaci, tak pro přístupnost.

## Krok 3: Vytvořte a upravte styl prvku tabulky

Nyní, když je kořenový element nastaven, vytvoříme `TableElement` a aplikovat styly, jako je barva pozadí, ohraničení a zarovnání.

```csharp
// Vytvořit prvek struktury tabulky
TableElement tableElement = taggedContent.CreateTableElement();
rootElement.AppendChild(tableElement);

// Stylizace stolu
tableElement.BackgroundColor = Color.Beige;
tableElement.Border = new BorderInfo(BorderSide.All, 0.80F, Color.Gray);
tableElement.Alignment = HorizontalAlignment.Center;
tableElement.Broken = TableBroken.Vertical;
tableElement.ColumnAdjustment = ColumnAdjustment.AutoFitToWindow;
```

Vytvoříme `TableElement`, který definuje strukturu naší tabulky. `BackgroundColor`, `Border`a `Alignment` Vlastnosti nám umožňují přizpůsobit vzhled tabulky. `Broken` Vlastnost zajišťuje, že pokud se tabulka zalomí napříč stránkami, zalomí se svisle.

## Krok 4: Nastavení rozměrů tabulky a stylů buněk

V tomto kroku definujeme počet sloupců, odsazení buněk a další důležité vlastnosti tabulky.

```csharp
tableElement.ColumnWidths = "80 80 80 80 80";
tableElement.DefaultCellBorder = new BorderInfo(BorderSide.All, 0.50F, Color.DarkBlue);
tableElement.DefaultCellPadding = new MarginInfo(16.0, 2.0, 8.0, 2.0);
tableElement.DefaultCellTextState.ForegroundColor = Color.DarkCyan;
tableElement.DefaultCellTextState.FontSize = 8F;
```

Šířku sloupců určujeme tak, aby všechny sloupce v tabulce byly rovnoměrně rozmístěny. `DefaultCellBorder`, `DefaultCellPadding`a `DefaultCellTextState` definujte výchozí styly pro buňky, včetně ohraničení, odsazení, barvy textu a velikosti písma.

## Krok 5: Přidání opakujících se řádků a vlastních stylů

Můžeme také definovat styly pro opakující se řádky a další specifické prvky tabulky, jako jsou záhlaví a zápatí.

```csharp
tableElement.RepeatingRowsCount = 3;
TextState rowStyle = new TextState();
rowStyle.BackgroundColor = Color.LightCoral;
tableElement.RepeatingRowsStyle = rowStyle;
```

Ten/Ta/To `RepeatingRowsCount` zajišťuje, že se první tři řádky opakují, pokud tabulka zabírá více stránek. Nastavíme `RepeatingRowsStyle` použít na tyto řádky vlastní barvu pozadí.

## Krok 6: Přidání prvků záhlaví, těla a nohou stolu

Nyní si vytvořme záhlaví, tělo a zápatí tabulky a naplníme je obsahem.

```csharp
TableTHeadElement tableTHeadElement = tableElement.CreateTHead();
TableTBodyElement tableTBodyElement = tableElement.CreateTBody();
TableTFootElement tableTFootElement = tableElement.CreateTFoot();

// Vytvořit řádek záhlaví
TableTRElement headTrElement = tableTHeadElement.CreateTR();
headTrElement.AlternativeText = "Head Row";
for (int colIndex = 0; colIndex < 5; colIndex++)
{
    TableTHElement thElement = headTrElement.CreateTH();
    thElement.SetText($"Head {colIndex}");
}

// Naplnění těla tabulky
for (int rowIndex = 0; rowIndex < 10; rowIndex++)
{
    TableTRElement trElement = tableTBodyElement.CreateTR();
    for (int colIndex = 0; colIndex < 5; colIndex++)
    {
        TableTDElement tdElement = trElement.CreateTD();
        tdElement.SetText($"Cell [{rowIndex}, {colIndex}]");
    }
}
```

Tabulka je rozdělena na tři části: záhlaví, tělo a patu. Nejprve vytvoříme záhlaví pomocí `TableTHElement` a přidáme záhlaví sloupců. Poté naplníme tělo tabulky `TableTDElement`a vyplní každou buňku popiskem, který obsahuje její pozici.

## Krok 7: Uložte dokument

Nakonec uložíme PDF dokument do zadaného adresáře.

```csharp
// Uložení tagovaného dokumentu PDF
document.Save(dataDir + "StyleTableElement.pdf");
```

Tento krok dokončí proces vytváření dokumentu uložením souboru PDF se stylizovanou tabulkou.

## Krok 8: Ověření shody s PDF/UA

Po uložení dokumentu je nezbytné zajistit, aby splňoval standardy PDF/UA (Universal Accessibility).

```csharp
// Zkontrolujte shodu s PDF/UA
document = new Document(dataDir + "StyleTableElement.pdf");
bool isPdfUaCompliance = document.Validate(dataDir + "StyleTableElement.xml", PdfFormat.PDF_UA_1);
Console.WriteLine($"PDF/UA compliance: {isPdfUaCompliance}");
```

Zde dokument znovu načteme a ověříme ho podle standardů PDF/UA. Soulad s předpisy zajišťuje, že váš PDF soubor splňuje požadavky na přístupnost, takže je vhodný pro širokou škálu uživatelů.

## Závěr

S Aspose.PDF pro .NET je vytváření a stylování tabulek ve vašich PDF dokumentech jednoduché a intuitivní. Dodržováním kroků uvedených v tomto tutoriálu můžete vytvářet tabulky s přizpůsobenými styly a zajistit, aby vaše PDF soubory splňovaly standardy přístupnosti. Ať už generujete sestavy nebo vytváříte strukturované dokumenty, tabulky jsou mocným nástrojem pro přehlednou prezentaci dat.

## Často kladené otázky

### Mohu vkládat obrázky do buněk tabulky?
Ano, obrázky můžete vkládat do buněk tabulky pomocí `Image` živel.

### Jak mohu dynamicky upravit šířku sloupců?
Můžete nastavit `ColumnAdjustment` majetek `AutoFitToWindow` automaticky upravovat šířku sloupců na základě obsahu.

### Je shoda s PDF/UA povinná pro všechny dokumenty?
I když to není povinné, doporučuje se to pro dokumenty, které vyžadují vysoké standardy přístupnosti.

### Mohu na konkrétní řádky použít různé styly?
Ano, jednotlivé řádky nebo buňky si můžete přizpůsobit úpravou jejich `TextState` nebo `BackgroundColor`.

### Jaká je výhoda používání tagovaného obsahu?
Označený obsah zlepšuje přístupnost dokumentů a pomáhá zajistit soulad se standardy, jako je PDF/UA.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}