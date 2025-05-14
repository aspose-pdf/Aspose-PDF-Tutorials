---
"description": "Naučte se, jak přidat opakující se sloupce do PDF dokumentů pomocí Aspose.PDF pro .NET. Podrobný návod s příklady a kódem. Ideální pro vývojáře."
"linktitle": "Přidat opakující se sloupec do dokumentu PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Přidat opakující se sloupec do dokumentu PDF"
"url": "/cs/net/programming-with-tables/add-repeating-column/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidat opakující se sloupec do dokumentu PDF

## Zavedení

Pokud pracujete s dokumenty PDF a potřebujete přidat opakující se sloupce, jste na správném místě! Pomocí Aspose.PDF pro .NET můžete snadno spravovat tabulky a obsah v PDF. Ať už vytváříte dynamické sestavy, faktury nebo jakýkoli jiný strukturovaný dokument, opakující se sloupce mohou být v organizaci dat zásadní. Pojďme se ponořit do podrobného návodu, jak do dokumentu PDF přidat opakující se sloupce.

## Předpoklady

Než se pustíme do kódu, ujistěme se, že máte vše nastavené:

- Aspose.PDF pro .NET: V projektu musíte mít nainstalovanou knihovnu Aspose.PDF pro .NET.
- [Stáhnout Aspose.PDF pro .NET](https://releases.aspose.com/pdf/net/)
- [Bezplatná zkušební verze](https://releases.aspose.com/)
- Vývojové prostředí: Ujistěte se, že máte nainstalované IDE kompatibilní s .NET, například Visual Studio.
- Základní znalost C#: I když si vše rozebereme, základní znalost C# vám pomůže plynule se v textu orientovat.
  
Pokud ještě nemáte Aspose.PDF pro .NET, můžete si ho stáhnout [dočasná licence](https://purchase.aspose.com/temporary-license/) abyste mohli začít prozkoumávat jeho funkce.

## Importovat balíčky

Pro začátek je potřeba importovat potřebné jmenné prostory z Aspose.PDF pro .NET. Postupujte takto:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

Tyto balíčky poskytují základní třídy a metody potřebné pro práci s PDF dokumenty a manipulaci s tabulkami.

Nyní si rozdělme proces do několika kroků, abychom do dokumentu PDF přidali opakující se sloupce. Sledujte to!

## Krok 1: Nastavení cesty k adresáři dokumentů

Než začneme vytvářet nebo manipulovat s jakýmikoli soubory, musíme definovat cestu, kam bude vygenerovaný PDF uložen. Ve vašem projektu C# nastavte cestu k adresáři, kde budou vaše soubory umístěny:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "AddRepeatingColumn_out.pdf";
```

Tato cesta ukazuje na adresář, kam bude uložen výstupní PDF. Nahraďte `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou na vašem počítači.

## Krok 2: Vytvořte nový dokument PDF

Pro začátek vytvořte novou instanci `Document` objekt. Ten bude sloužit jako kontejner pro všechny stránky a obsah v PDF.

```csharp
Document doc = new Document();
Aspose.Pdf.Page page = doc.Pages.Add();
```

Zde jsme vytvořili nový dokument PDF a přidali do něj prázdnou stránku. `doc.Pages.Add()` Metoda vloží do dokumentu novou stránku.

## Krok 3: Vytvoření instance vnější tabulky

Dále vytvoříme vnější tabulku. Tato tabulka bude zabírat celou šířku stránky a bude sloužit jako kontejner pro další tabulky, včetně té, která bude obsahovat opakující se sloupce.

```csharp
Aspose.Pdf.Table outerTable = new Aspose.Pdf.Table();
outerTable.ColumnWidths = "100%";
outerTable.HorizontalAlignment = HorizontalAlignment.Left;
```

Nastavili jsme `ColumnWidths` vlastnost na „100 %“, což znamená, že se tabulka roztáhne přes celou šířku stránky.

## Krok 4: Vytvořte vnitřní tabulku

Nyní si vytvořme vnitřní tabulku, která bude mít opakující se sloupce. Klíčové vlastnosti jsou zde `Broken`, což umožňuje, aby tabulka pokračovala na stejné stránce, a `ColumnAdjustment`, který automaticky upraví šířku sloupců tak, aby odpovídala obsahu.

```csharp
Aspose.Pdf.Table mytable = new Aspose.Pdf.Table();
mytable.Broken = TableBroken.VerticalInSamePage;
mytable.ColumnAdjustment = ColumnAdjustment.AutoFitToContent;
```

Tato vnitřní tabulka bude vnořena do vnější tabulky.

## Krok 5: Přidání tabulek na stránku

Nyní, když máme připravené vnější i vnitřní tabulky, přidejme je na stránku. Tento krok zajistí, že tabulky budou zahrnuty do struktury dokumentu.

```csharp
page.Paragraphs.Add(outerTable);
var bodyRow = outerTable.Rows.Add();
var bodyCell = bodyRow.Cells.Add();
bodyCell.Paragraphs.Add(mytable);
mytable.RepeatingColumnsCount = 5;
```

Zde jsme přidali `outerTable` na stránku a poté jsme do vnější tabulky vnořili `mytable`Dále jsme nastavili `RepeatingColumnsCount` na 5, čímž se určí, kolik sloupců se má opakovat při přidávání dat.

## Krok 6: Přidání řádku záhlaví

Nyní je čas přidat do tabulky záhlaví. Řádek záhlaví poskytuje kontext datům a pomáhá strukturovat sloupce. 

```csharp
Aspose.Pdf.Row row = mytable.Rows.Add();
row.Cells.Add("header 1");
row.Cells.Add("header 2");
row.Cells.Add("header 3");
row.Cells.Add("header 4");
row.Cells.Add("header 5");
row.Cells.Add("header 6");
row.Cells.Add("header 7");
row.Cells.Add("header 11");
row.Cells.Add("header 12");
row.Cells.Add("header 13");
row.Cells.Add("header 14");
row.Cells.Add("header 15");
row.Cells.Add("header 16");
row.Cells.Add("header 17");
```

Tento úryvek kódu přidá první řádek (který použijeme jako záhlaví) a naplní jej buňkami obsahujícími text jako „záhlaví 1“, „záhlaví 2“ atd.

## Krok 7: Přidání datových řádků

Nakonec můžeme do tabulky přidat nějaká data. Tato smyčka dynamicky vytváří řádky a buňky naplňuje obsahem:

```csharp
for (int RowCounter = 0; RowCounter <= 5; RowCounter++)
{
    Aspose.Pdf.Row row1 = mytable.Rows.Add();
    row1.Cells.Add("col " + RowCounter.ToString() + ", 1");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 2");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 3");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 4");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 5");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 6");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 7");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 11");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 12");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 13");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 14");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 15");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 16");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 17");
}
```

Smyčka se opakuje šestkrát, přidává řádky a každou buňku vyplňuje odpovídajícími daty ze sloupců (např. „sloupec 1, 1“, „sloupec 2, 2“ atd.).

## Krok 8: Uložte dokument

Jakmile jsou přidány všechny řádky a sloupce, posledním krokem je uložení dokumentu do zadané cesty k souboru.

```csharp
doc.Save(outFile);
```

Váš dokument je nyní uložen s opakujícími se sloupci!

## Závěr

A máte to! Pomocí těchto jednoduchých kroků můžete vytvořit PDF dokument s opakujícími se sloupci pomocí Aspose.PDF pro .NET. Využitím flexibility vnořených tabulek můžete dosáhnout složitých rozvržení, díky nimž budou vaše PDF dokumenty vypadat profesionálně a uspořádaně. Vyzkoušejte to pro svůj další projekt a prozkoumejte plný potenciál Aspose.PDF pro vaše potřeby generování PDF.

## Často kladené otázky

### Co je Aspose.PDF pro .NET?
Aspose.PDF pro .NET je výkonná knihovna, která umožňuje vývojářům programově vytvářet, upravovat a spravovat PDF dokumenty.

### Mohu dynamicky upravit počet opakujících se sloupců?
Ano, počet opakujících se sloupců můžete změnit úpravou `RepeatingColumnsCount` vlastnictví.

### Jak mohu použít licenci k souboru Aspose.PDF pro .NET?
Licenci můžete použít ze souboru nebo streamu podle pokynů [dokumentace](https://reference.aspose.com/pdf/net/).

### Je možné přidat obrázky do buněk tabulky?
Ano, Aspose.PDF pro .NET podporuje přidávání různých typů obsahu, včetně obrázků, do buněk tabulky.

### Mohu si rozvržení tabulky dále přizpůsobit?
Rozhodně! Aspose.PDF nabízí rozsáhlé funkce pro úpravu stylů tabulek, včetně ohraničení, odsazení, zarovnání a dalších.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}