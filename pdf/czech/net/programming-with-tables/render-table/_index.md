---
"description": "Vytvářejte profesionální PDF soubory snadno vykreslením tabulek pomocí Aspose.PDF pro .NET. Postupujte podle našeho podrobného návodu, jak zvládnout generování dokumentů."
"linktitle": "Vykreslení tabulky v dokumentu PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Vykreslení tabulky v dokumentu PDF"
"url": "/cs/net/programming-with-tables/render-table/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vykreslení tabulky v dokumentu PDF

## Zavedení

Vytváření profesionálně vypadajících PDF souborů programově se může zdát jako náročný úkol, ale s Aspose.PDF pro .NET se to stává hračkou. Ať už generujete zprávy, faktury nebo jakýkoli jiný typ dokumentu, který vyžaduje tabulková data, Aspose.PDF nabízí nástroje, které potřebujete. V tomto tutoriálu se krok za krokem podíváme na to, jak vykreslit tabulky v dokumentu PDF. Na konci budete mít důkladné znalosti o tom, jak manipulovat s tabulkami, spravovat vlastnosti stránek a snadno ukládat soubory PDF.

## Předpoklady

Než se ponoříme do kódu, potřebujeme následující:

- Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio. Můžete si ho stáhnout [zde](https://visualstudio.microsoft.com/downloads/).
- Aspose.PDF pro .NET: Knihovnu Aspose.PDF si můžete snadno stáhnout z [Stránka s vydáním Aspose](https://releases.aspose.com/pdf/net/).
- Základní znalost C#: Pochopení základů C# vám pomůže lépe se orientovat.
- .NET Framework: V ideálním případě se ujistěte, že pracujete v kompatibilním prostředí .NET.

Jakmile máte tyto předpoklady nastavené, můžete začít vytvářet dokumenty PDF!

## Importovat balíčky

Na začátku vašeho C# souboru budete muset importovat potřebné jmenné prostory Aspose.PDF. To vám umožní využívat funkce knihovny v našem projektu.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

Ujistěte se, že jste do projektu přidali potřebné odkazy na knihovnu Aspose.PDF. Pokud používáte NuGet, můžete ji snadno přidat vyhledáním `Aspose.PDF`.

Nyní, když máme vše nastavené, pojďme si rozdělit proces vykreslení tabulky v dokumentu PDF na zvládnutelné kroky. Nebojte se, provedu vás každým krokem s jasnými pokyny!

## Krok 1: Nastavení informací o dokumentu a stránce

Nejdříve musíme vytvořit nový dokument a nakonfigurovat jeho nastavení stránky. Zde je návod, jak to udělat:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document();
PageInfo pageInfo = doc.PageInfo;
Aspose.Pdf.MarginInfo marginInfo = pageInfo.Margin;

marginInfo.Left = 37;
marginInfo.Right = 37;
marginInfo.Top = 37;
marginInfo.Bottom = 37;

pageInfo.IsLandscape = true;
```

Vysvětlení: 
- Začneme definováním místa, kam bude náš dokument uložen (`dataDir`). 
- Pak vytvoříme novou instanci `Document` třída. 
- Okraje stránky upravíme tak, abychom kolem tabulky vytvořili volný prostor.
- Nakonec nastavíme orientaci dokumentu na šířku, což pomáhá při zobrazování širších tabulek.

## Krok 2: Vytvořte první tabulku

Dále si vytvořme naši první tabulku a naplňme ji vzorovými daty:

```csharp
Aspose.Pdf.Table table = new Aspose.Pdf.Table();
table.ColumnWidths = "50 100"; // Definování šířky sloupců
```

Vysvětlení: Zde vytváříme instanci `Table` třídu a nastavte šířku sloupců. První sloupec bude mít šířku 50 jednotek a druhý sloupec bude mít šířku 100 jednotek.

## Krok 3: Naplnění tabulky řádky

Nyní si do tabulky v cyklu přidáme řádky:

```csharp
Page curPage = doc.Pages.Add(); // Přidání nové stránky
for (int i = 1; i <= 120; i++)
{
    Aspose.Pdf.Row row = table.Rows.Add();
    row.FixedRowHeight = 15; // Nastavení pevné výšky řádků
    
    Aspose.Pdf.Cell cell1 = row.Cells.Add();
    cell1.Paragraphs.Add(new TextFragment("Content 1"));
    
    Aspose.Pdf.Cell cell2 = row.Cells.Add();
    cell2.Paragraphs.Add(new TextFragment("HHHHH"));
}
```

Vysvětlení: 
- Zde vytvoříme novou stránku pro přidání naší tabulky.
- Používáme `for` cyklus pro přidání 120 řádků do naší tabulky. Každý řádek má pevnou výšku 15 jednotek.
- Uvnitř každého řádku přidáme dvě buňky a naplníme je textem.

## Krok 4: Přidání první tabulky na stránku

Jakmile naplníme tabulku, přidáme ji na aktuální stránku:

```csharp
Aspose.Pdf.Paragraphs paragraphs = curPage.Paragraphs;
paragraphs.Add(table);
```

Vysvětlení: Tento krok jednoduše přidá tabulku, kterou jsme vytvořili, do odstavců aktuální stránky, čímž se tabulka zobrazí v dokumentu PDF.

## Krok 5: Vytvořte druhou tabulku

Nyní si vytvořme druhou tabulku s jiným obsahem a přidejme ji na novou stránku:

```csharp
Aspose.Pdf.Table table1 = new Aspose.Pdf.Table();
table1.ColumnWidths = "100 100";
for (int i = 1; i <= 10; i++)
{
    Aspose.Pdf.Row row = table1.Rows.Add();
    Aspose.Pdf.Cell cell1 = row.Cells.Add();
    cell1.Paragraphs.Add(new TextFragment("LAAAAAAA"));
    
    Aspose.Pdf.Cell cell2 = row.Cells.Add();
    cell2.Paragraphs.Add(new TextFragment("LAAGGGGGG"));
}
table1.IsInNewPage = true; // Nastavení zobrazení druhé tabulky na nové stránce
paragraphs.Add(table1);
```

Vysvětlení: 
- Tento úryvek kódu vytvoří novou tabulku se dvěma sloupci, oba o šířce 100 jednotek.
- A `for` Smyčka přidá 10 řádků s ukázkovým obsahem.
- Nastavením `table1.IsInNewPage` Pokud je nastaveno na hodnotu true, zajistíme, aby se tato tabulka zobrazovala na nové stránce, čímž se zachová přehlednost a přehlednost.

## Krok 6: Uložte dokument

Nyní, když jsou naše tabulky připravené, uložme si náš dokument:

```csharp
dataDir = dataDir + "IsNewPageProperty_Test_out.pdf";
doc.Save(dataDir);
```

Vysvětlení: Zadáme název souboru a uložíme dokument do definovaného adresáře. Po spuštění tohoto kódu se vytvoří soubor PDF s názvem `IsNewPageProperty_Test_out.pdf` bude vytvořen ve vámi zadaném místě.

## Krok 7: Potvrzovací zpráva

Nakonec, abychom uživatele informovali, že vše proběhlo hladce, můžeme přidat přátelskou konzolovou zprávu:

```csharp
Console.WriteLine("\nTable rendered successfully on a page.\nFile saved at " + dataDir);
```

Vysvětlení: Toto je jednoduchý způsob, jak potvrdit, že operace proběhla úspěšně, a zjistit, kde uživatel najde svůj nový soubor PDF.

## Závěr

A tady to máte! Úspěšně jste vykreslili tabulky v PDF dokumentu pomocí Aspose.PDF pro .NET. S pouhými několika řádky kódu můžete zpracovávat a prezentovat velké množství dat v uspořádaném formátu, díky čemuž budou vaše dokumenty informativní i vizuálně přitažlivé. Ať už pracujete na inventárních seznamech, finančních zprávách nebo vzdělávacích dokumentech, tabulky jsou vynikajícím způsobem, jak na první pohled sdělit složité informace.

## Často kladené otázky

### Mohu si přizpůsobit vzhled tabulek v souboru Aspose.PDF?  
Rozhodně! Můžete upravit barvy, ohraničení, styly písma a další vlastnosti pro vylepšení vzhledu tabulek.

### Je Aspose.PDF zdarma k použití?  
Aspose.PDF nabízí bezplatnou zkušební verzi, ale pro komerční použití je nutný nákup. Ceny si můžete prohlédnout [zde](https://purchase.aspose.com/buy).

### Jak mohu získat podporu pro problémy s Aspose.PDF?  
Pomoc můžete vyhledat na fóru podpory Aspose. [zde](https://forum.aspose.com/c/pdf/10).

### Existují nějaká omezení pro bezplatnou zkušební verzi?  
Ano, zkušební verze může mít určitá omezení, například vodoznaky na generovaných dokumentech. Pro plnou funkčnost zvažte pořízení dočasné licence. [zde](https://purchase.aspose.com/temporary-license/).

### Kde najdu více informací o funkcích Aspose.PDF?  
Můžete si prohlédnout dostupnou komplexní dokumentaci [zde](https://reference.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}