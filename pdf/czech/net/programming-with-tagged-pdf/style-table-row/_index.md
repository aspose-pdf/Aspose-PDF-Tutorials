---
"description": "Naučte se, jak upravovat styly řádků tabulky v PDF pomocí Aspose.PDF pro .NET s podrobným návodem, jak snadno vylepšit formátování dokumentu."
"linktitle": "Řádek tabulky stylů"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Řádek tabulky stylů"
"url": "/cs/net/programming-with-tagged-pdf/style-table-row/"
"weight": 180
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Řádek tabulky stylů

## Zavedení

Pokud jde o vytváření dobře strukturovaných a krásně formátovaných dokumentů PDF, Aspose.PDF pro .NET je ideálním řešením. Ať už automatizujete reporty, faktury nebo vytváříte dynamické tabulky, formátování tabulek s různými styly je klíčem k vytříbenému dokumentu. V tomto tutoriálu se podrobně ponoříme do stylování řádků tabulky pomocí Aspose.PDF pro .NET. A nebojte se, provedu vás krok za krokem, stejně jako dobrý rozhovor u kávy!

## Předpoklady

Než se pustíme do detailů, ujistěme se, že máte vše připravené. Budete potřebovat:

1. Aspose.PDF pro knihovnu .NET  
   Pokud ho ještě nemáte, můžete si ho stáhnout z [zde](https://releases.aspose.com/pdf/net/)Můžete také získat [bezplatná zkušební verze](https://releases.aspose.com/) začít.
2. Vývojové prostředí  
   Nastavte si Visual Studio nebo jakékoli C# IDE dle vašeho výběru. Budete také potřebovat nainstalované rozhraní .NET, ale předpokládám, že s tím už jste obeznámeni.
3. Základní znalost C# a .NET  
   Dobrá znalost C# vám tento tutoriál usnadní. Ale nebojte se, každý krok vám podrobně vysvětlím!

## Importovat balíčky

Než začneme pracovat s Aspose.PDF, musíme importovat potřebné jmenné prostory. Ve vašem projektu v C# nezapomeňte zahrnout následující:

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Tyto prvky jsou nezbytné pro vytvoření a stylování tabulky a samozřejmě pro práci s tagovaným obsahem za účelem dodržování předpisů.

Nyní si úkol rozebereme krok za krokem, abyste mohli stylovat řádky tabulky jako profesionál!

## Krok 1: Vytvořte nový dokument PDF

Nejdříve to nejdůležitější: vytvořme si zcela nový PDF dokument. Tento dokument bude obsahovat všechny stylizované řádky tabulky.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Vytvořit dokument
Document document = new Document();
```

Zde jednoduše inicializujeme nový `Document` objekt, který bude reprezentovat náš PDF soubor. Nezapomeňte nastavit cestu k adresáři, kam budete ukládat výstupní soubory.

## Krok 2: Práce s označeným obsahem

Pro strukturování PDF z hlediska přístupnosti budeme pracovat s tagovaným obsahem. To pomáhá vytvářet strukturované prvky, jako jsou tabulky, a zajišťuje jejich soulad se standardy přístupnosti, jako je PDF/UA.

```csharp
ITaggedContent taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example table row style");
taggedContent.SetLanguage("en-US");
```

Zde nastavujeme název a jazyk pro tagovaný obsah PDF. Je to, jako byste dali PDF souboru název a řekli mu, v jakém jazyce má mluvit!

## Krok 3: Definování struktury tabulky

Dále si definujme strukturu tabulky, kterou se chystáme vytvořit. Každá tabulka potřebuje záhlaví, tělo a zápatí – podobně jako dobře organizovaný blogový příspěvek!

```csharp
// Získat prvek kořenové struktury
StructureElement rootElement = taggedContent.RootElement;

// Vytvořit prvek struktury tabulky
TableElement tableElement = taggedContent.CreateTableElement();
rootElement.AppendChild(tableElement);
TableTHeadElement tableTHeadElement = tableElement.CreateTHead();
TableTBodyElement tableTBodyElement = tableElement.CreateTBody();
TableTFootElement tableTFootElement = tableElement.CreateTFoot();
```

Zde vytváříme tabulku se záhlavím (`THead`), tělo (`TBody`) a zápatí (`TFoot`). Tyto prvky budou držet naše řádky.

## Krok 4: Přidání řádku záhlaví tabulky

Tabulky bez záhlaví jsou jako knihy bez názvů. Nejprve si vytvořme řádek záhlaví, který poskytne kontext pro data.

```csharp
TableTRElement headTrElement = tableTHeadElement.CreateTR();
headTrElement.AlternativeText = "Head Row";
for (int colIndex = 0; colIndex < 3; colIndex++)
{
    TableTHElement thElement = headTrElement.CreateTH();
    thElement.SetText(String.Format("Head {0}", colIndex));
}
```

Zde projdeme smyčkou a přidáme tři buňky záhlaví (`TableTHElement`) a každému z nich připsat popisný text. Jednoduché, že?

## Krok 5: Přidání stylizovaných řádků těla

A teď přichází ta zábavná část – stylování řádků! Vytvořme sedm řádků s vlastními styly. Nastavíme barvy pozadí, ohraničení, odsazení a zarovnání textu.

```csharp
for (int rowIndex = 0; rowIndex < 7; rowIndex++)
{
    TableTRElement trElement = tableTBodyElement.CreateTR();
    trElement.AlternativeText = String.Format("Row {0}", rowIndex);
    trElement.BackgroundColor = Color.LightGoldenrodYellow;
    trElement.Border = new BorderInfo(BorderSide.All, 0.75F, Color.DarkGray);
    trElement.DefaultCellBorder = new BorderInfo(BorderSide.All, 0.50F, Color.Blue);
    trElement.MinRowHeight = 100.0;
    trElement.FixedRowHeight = 120.0;
    trElement.IsInNewPage = (rowIndex % 3 == 1);
    trElement.IsRowBroken = true;

    for (int colIndex = 0; colIndex < 3; colIndex++)
    {
        TableTDElement tdElement = trElement.CreateTD();
        tdElement.SetText(String.Format("Cell [{0}, {1}]", rowIndex, colIndex));
    }
}
```

- Barva pozadí: Pro profesionální, ale zároveň hřejivý nádech jsme použili světle žlutou od zlatobýlu.
- Ohraničení: Každý řádek má tmavě šedý vnější okraj a modré okraje buněk pro ostrý vzhled.
- Výška a odsazení: Nastaví se výška řádků a pro čistší vzhled se přidá odsazení.
- Zalomení stránek: Aby byla tabulka čitelnější, každý druhý řádek začíná na nové stránce.

## Krok 6: Přidání řádku zápatí

Stejně jako záhlaví i zápatí ukotvuje tabulku. Pojďme si jedno vytvořit.

```csharp
TableTRElement footTrElement = tableTFootElement.CreateTR();
footTrElement.AlternativeText = "Foot Row";
for (int colIndex = 0; colIndex < 3; colIndex++)
{
    TableTDElement tdElement = footTrElement.CreateTD();
    tdElement.SetText(String.Format("Foot {0}", colIndex));
}
```

Jednoduše projdeme třemi buňkami zápatí a přidáme trochu textu. Alternativním textem pro zápatí je „Řádek pro nohy“, aby bylo přístupné.

## Krok 7: Uložení dokumentu PDF

Teď, když je stůl připravený, je čas uložit vaše mistrovské dílo!

```csharp
document.Save(dataDir + "StyleTableRow.pdf");
```

A tak se váš PDF uloží se všemi krásnými řádky tabulky, které jsme právě stylizovali.

## Krok 8: Ověření shody s PDF/UA

Abychom zajistili, že náš PDF soubor splňuje standardy přístupnosti, ověříme jeho shodu s PDF/UA.

```csharp
document = new Document(dataDir + "StyleTableRow.pdf");
bool isPdfUaCompliance = document.Validate(dataDir + "StyleTableRow.xml", PdfFormat.PDF_UA_1);
Console.WriteLine(String.Format("PDF/UA compliance: {0}", isPdfUaCompliance));
```

Díky tomu bude váš PDF soubor splňovat standard PDF/UA, takže bude přístupný všem. Přístupnost je klíčová!

## Závěr

A je to! S pouhými několika řádky kódu jste vytvořili plně stylizovanou tabulku v PDF pomocí Aspose.PDF pro .NET. Od záhlaví po zápatí jsme stylizovali každý řádek, přidali prvky přístupnosti a dokonce jsme ověřili shodu dokumentu s předpisy. Ať už pracujete na firemních zprávách, prezentacích, nebo si jen užíváte PDF, tento průvodce vám pomůže. A teď se pusťte do stylování svých tabulek jako profesionál!

## Často kladené otázky

### Mohu také změnit styl písma tabulky?  
Ano! Styl písma můžete upravit pomocí `TextState` objekt pro každou buňku, což umožňuje plné přizpůsobení.

### Jak mohu do tabulky přidat další sloupce?  
Stačí upravit `colCount` proměnnou a přidat do smyček další buňky pro záhlaví, tělo a zápatí.

### Co se stane, když nenastavím výšku řádku?  
Pokud nenastavíte výšku řádku, tabulka se automaticky upraví na základě obsahu.

### Mohu to použít pro dynamický počet řádků?  
Rozhodně! Můžete načítat data z databáze nebo jakéhokoli jiného zdroje a dynamicky upravovat počet řádků a sloupců.

### Je Aspose.PDF pro .NET zdarma k použití?  
Aspose.PDF pro .NET je licencovaný produkt, ale můžete si ho vyzkoušet s [bezplatná zkušební verze](https://releases.aspose.com/) nebo si pořiďte [dočasná licence](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}