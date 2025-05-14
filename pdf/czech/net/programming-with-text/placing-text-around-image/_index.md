---
"description": "Naučte se, jak umístit text kolem obrázků v PDF souborech pomocí Aspose.PDF pro .NET. Postupujte podle našeho podrobného návodu a vytvořte profesionální PDF soubory s obrázky a textem vedle sebe."
"linktitle": "Umístění textu kolem obrázku v souboru PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Umístění textu kolem obrázku v souboru PDF"
"url": "/cs/net/programming-with-text/placing-text-around-image/"
"weight": 260
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Umístění textu kolem obrázku v souboru PDF

## Zavedení

Už jste někdy zkoušeli umístit text kolem obrázku v souboru PDF, ale shledali jste to náročným? Pokud ano, jste na správném místě! Aspose.PDF pro .NET tento proces zjednodušuje a umožňuje vám umístit text vedle obrázků pomocí několika řádků kódu. Ať už vytváříte zprávy, dokumenty nebo prezentace, tato funkce je fantastickým způsobem, jak vylepšit rozvržení obsahu a učinit ho vizuálně atraktivnějším. Dnes si ukážeme, jak pomocí Aspose.PDF pro .NET umístit text kolem obrázků v dokumentu PDF.

## Předpoklady

Než se pustíme do kódu, ujistěme se, že máme vše nastavené. Zde je to, co budete potřebovat:

- Aspose.PDF pro .NET: Můžete si jej stáhnout z [zde](https://releases.aspose.com/pdf/net/).
- Visual Studio: Pro bezproblémový chod se ujistěte, že máte nainstalovanou nejnovější verzi.
- .NET Framework: Tento příklad používá .NET, proto se ujistěte, že je vaše prostředí nastaveno pro vývoj v .NET.
- Dočasná licence: Můžete požádat o dočasnou licenci [zde](https://purchase.aspose.com/temporary-license/) pokud hodnotíte produkt.

Pokud jste ještě nenastavili Aspose.PDF pro .NET, postupujte podle pokynů k instalaci v [dokumentace](https://reference.aspose.com/pdf/net/).

## Importovat jmenné prostory

Než začneme s kódováním, musíme importovat potřebné jmenné prostory. Zde je úryvek kódu, který to udělá:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Tyto jmenné prostory jsou nezbytné, protože poskytují přístup ke třídám jako `Document`, `Page`, `Image`a `HtmlFragment`, který použijeme k vytvoření a manipulaci s PDF.

Nyní, když jsme si připravili půdu, pojďme si rozebrat, jak umístit text kolem obrázku v souboru PDF pomocí Aspose.PDF pro .NET. Provedeme vás tím krok za krokem.

## Krok 1: Vytvoření instance objektu Document

Nejprve je třeba vytvořit dokument PDF. V Aspose.PDF se to provádí vytvořením instance `Document` objekt. Tento objekt bude sloužit jako základ pro veškerý obsah, který budeme přidávat.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

Zde jsme vytvořili prázdný PDF dokument. Zatím nemá žádné stránky, ale nebojte se, v dalším kroku jednu přidáme.

## Krok 2: Přidání stránky do dokumentu

Teď, když máme dokument, je čas přidat stránku. Představte si to jako vytvoření prázdného listu papíru, kam přidáte svůj obsah.

```csharp
Aspose.Pdf.Page page = doc.Pages.Add();
```

Tento kód přidá do dokumentu novou stránku. Ve výchozím nastavení je stránka prázdná, ale to se chystáme změnit.

## Krok 3: Vytvořte tabulku pro uspořádání obsahu

Abychom zachovali správné zarovnání obrázku a textu, použijeme tabulku. Tabulky v PDF souborech mohou pomoci strukturovat rozvržení, podobně jako v dokumentech Word nebo HTML.

```csharp
Aspose.Pdf.Table table1 = new Aspose.Pdf.Table();
page.Paragraphs.Add(table1);
```

Tento úryvek kódu vytvoří tabulku a přidá ji na stránku. Představte si tabulku jako rámec pro zarovnání obrázku a textu.

## Krok 4: Nastavení šířky sloupců pro tabulku

Nyní, když jsme přidali tabulku, musíme definovat, jak široké by měly být sloupce. Tím zajistíme, že obrázek a text budou na stránce mít vhodnou velikost.

```csharp
table1.ColumnWidths = "120 270";
```

Tento řádek nastavuje šířku dvou sloupců – jednoho pro obrázek a druhého pro text. Upravte tyto hodnoty, pokud váš obrázek nebo text potřebuje více či méně místa.

## Krok 5: Definování okrajů a odsazení

Aby vše vypadalo úhledně, přidejme k tabulce okraje a odsazení.

```csharp
Aspose.Pdf.MarginInfo margin = new Aspose.Pdf.MarginInfo();
margin.Top = 5f;
margin.Left = 5f;
margin.Right = 5f;
margin.Bottom = 5f;
table1.DefaultCellPadding = margin;
```

Tato nastavení zajišťují, že tabulka má konzistentní rozestupy, díky čemuž je obsah vizuálně atraktivní.

## Krok 6: Vložení obrázku do tabulky

A teď se pustíme do té zábavné části – přidání obrázku. V tomto případě přidáme logo Aspose, ale klidně můžete použít jakýkoli obrázek, který se vám líbí.

```csharp
Aspose.Pdf.Row row1 = table1.Rows.Add();
Aspose.Pdf.Image logo = new Aspose.Pdf.Image();
logo.File = dataDir + "aspose-logo.jpg";
logo.FixHeight = 120;
logo.FixWidth = 110;
row1.Cells.Add();
row1.Cells[0].Paragraphs.Add(logo);
```

Zde se dozvíte, co se děje:
- Načteme obrázek z vámi zadaného adresáře.
- Nastavíme výšku a šířku obrázku.
- Nakonec přidáme obrázek do první buňky v tabulce.

## Krok 7: Přidání textu vedle obrázku

Nyní, když je obrázek na místě, přidejme vedle něj nějaký text. V tomto příkladu použijeme text ve formátu HTML k úpravě stylu obsahu.

```csharp
string TitleString = "<font face=\"Arial\" size=6 color=\"#101090\"><b> Aspose.Pdf for .NET</b></font>";
string BodyString1 = "<font face=\"Arial\" size=2><br/>Aspose.Pdf for .NET is a non-graphical PDF document reporting component that enables .NET applications to <b>create PDF documents from scratch</b> without utilizing Adobe Acrobat.</font>";

Aspose.Pdf.HtmlFragment TitleText = new Aspose.Pdf.HtmlFragment(TitleString + BodyString1);
row1.Cells.Add();
row1.Cells[1].Paragraphs.Add(TitleText);
```

Tento blok přidá stylizovaný název a popis do buňky vedle obrázku. Text můžete formátovat pomocí HTML tagů pro větší přizpůsobení.

## Krok 8: Úprava svislého zarovnání

Ve výchozím nastavení se obsah v buňkách tabulky nemusí zarovnat požadovaným způsobem. V tomto případě se chceme ujistit, že je text zarovnán k hornímu okraji buňky.

```csharp
row1.Cells[1].VerticalAlignment = Aspose.Pdf.VerticalAlignment.Top;
```

Díky tomu bude text umístěn v horní části buňky, což zachovává čisté a profesionální rozvržení.

## Krok 9: Přidejte další text pod obrázek a popis

Možná budete chtít pod obrázek a text vložit další obsah. Pro tento účel přidejme do tabulky další řádek.

```csharp
Aspose.Pdf.Row SecondRow = table1.Rows.Add();
SecondRow.Cells.Add();
SecondRow.Cells[0].ColSpan = 2;
SecondRow.Cells[0].VerticalAlignment = Aspose.Pdf.VerticalAlignment.Top;

string SecondRowString = "<font face=\"Arial\" size=2>Aspose.Pdf for .NET supports the creation of PDF files through API and XML or XSL-FO templates.</font>";
Aspose.Pdf.HtmlFragment SecondRowText = new Aspose.Pdf.HtmlFragment(SecondRowString);
SecondRow.Cells[0].Paragraphs.Add(SecondRowText);
```

Zde jsme přidali další řádek s dalším textem, který se rozprostírá přes oba sloupce, aby byla zachována rovnováha v rozvržení.

## Krok 10: Uložení dokumentu PDF

Nakonec musíme dokument uložit, abyste si mohli prohlédnout změny.

```csharp
doc.Save(dataDir + "PlacingTextAroundImage_out.pdf");
```

Tím se uloží PDF s obrázkem a textem formátovaným přesně tak, jak chceme.

## Závěr

Umístění textu kolem obrázků v PDF se může zdát jako náročný úkol, ale Aspose.PDF pro .NET tento proces zjednodušuje. Využitím tabulek, obrázků a stylizovaného textu můžete s minimálním úsilím vytvářet profesionálně vypadající PDF soubory. S pouhými několika řádky kódu můžete umístit obsah přesně tam, kam chcete, a dodat tak svým dokumentům elegantní a dobře organizovaný vzhled.

## Často kladené otázky

### Mohu tuto metodu použít k umístění více obrázků s textem?
Ano, jednoduše přidejte do tabulky další řádky a buňky, abyste mohli zahrnout další obrázky a text.

### Mohu změnit zarovnání obrázku?
Rozhodně! Zarovnání obrázku můžete upravit úpravou vlastností zarovnání buňky.

### Jak mohu text dále stylizovat?
Můžete použít HTML tagy v rámci `HtmlFragment` objekt pro použití různých stylů, jako je tučné písmo, kurzíva nebo jiná písma.

### Mohu ovládat mezery mezi textem a obrázkem?
Ano, s použitím `MarginInfo` Objekt umožňuje ovládat odsazení a okraje mezi prvky.

### Je možné do textu přidat odkazy?
Rozhodně! Hypertextové odkazy můžete vkládat do textu ve formátu HTML pomocí `<a>` štítek.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}