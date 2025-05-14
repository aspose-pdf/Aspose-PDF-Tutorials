---
"description": "Naučte se, jak používat vyměnitelné symboly v záhlaví a zápatí dokumentu PDF pomocí Aspose.PDF pro .NET."
"linktitle": "Vyměnitelné symboly v záhlaví a zápatí"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Vyměnitelné symboly v záhlaví a zápatí"
"url": "/cs/net/programming-with-text/replaceable-symbols-in-header-footer/"
"weight": 320
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Vyměnitelné symboly v záhlaví a zápatí

## Zavedení

Při práci se soubory PDF se někdy objeví situace, kdy je potřeba přizpůsobit záhlaví a zápatí dynamickým obsahem, jako jsou čísla stránek, názvy sestav nebo data generování. Naštěstí Aspose.PDF pro .NET tento proces zjednodušuje a umožňuje vám vytvářet PDF soubory s automaticky aktualizovanými symboly v záhlavích a zápatích, jako jsou čísla stránek nebo podrobnosti o generování sestav. Tento článek vás provede podrobným procesem nahrazování symbolů v záhlavích a zápatích pomocí Aspose.PDF pro .NET způsobem, který je nejen jednoduchý, ale také neuvěřitelně efektivní.

## Předpoklady

Než se ponoříte do podrobného návodu, ujistěte se, že máte následující:

- Aspose.PDF pro knihovnu .NET – [Stáhnout](https://releases.aspose.com/pdf/net/) nebo si pořiďte [bezplatná zkušební verze](https://releases.aspose.com/).
- Visual Studio nebo jakékoli C# IDE nainstalované ve vašem systému.
- Základní znalost vývoje v C# a .NET.
- Platný [licence](https://purchase.aspose.com/temporary-license/) pro Aspose.PDF, nebo můžete použít zkušební verzi.

## Importovat balíčky

Pro začátek je potřeba importovat potřebné jmenné prostory, které umožní funkčnost souboru Aspose.PDF pro .NET. Níže je uveden potřebný import:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

Tyto funkce jsou nezbytné pro vytváření PDF, manipulaci s textem a správu záhlaví a zápatí.

Rozdělme si ukázkový kód na snadno srozumitelné kroky.

## Krok 1: Nastavení dokumentu a stránky

Nejprve musíme inicializovat dokument a přidat do něj stránku. Tím se vytvoří základ pro přidání záhlaví a zápatí.

```csharp
// Nastavení adresáře dokumentů
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Inicializovat objekt dokumentu
Document doc = new Document();

// Přidat stránku do dokumentu
Page page = doc.Pages.Add();
```

Zde nastavujeme PDF dokument pomocí `Document` třída a přidání stránky s `doc.Pages.Add()`Tato stránka bude obsahovat záhlaví, zápatí a další obsah.

## Krok 2: Konfigurace okrajů stránky

Dále definujeme okraje stránky, abychom zajistili, že náš obsah nebude sahat až k okraji.

```csharp
// Konfigurace okrajů
MarginInfo marginInfo = new MarginInfo();
marginInfo.Top = 90;
marginInfo.Bottom = 50;
marginInfo.Left = 50;
marginInfo.Right = 50;
page.PageInfo.Margin = marginInfo;
```

Zde jsme definovali horní, dolní, levý a pravý okraj pomocí `MarginInfo` třídu a aplikoval ji na stránku pomocí `page.PageInfo.Margin`.

## Krok 3: Vytvořte a nakonfigurujte záhlaví

Nyní si vytvořme záhlaví a přidejme ho na stránku. Záhlaví bude obsahovat název a název sestavy.

```csharp
// Vytvořit záhlaví
HeaderFooter hfFirst = new HeaderFooter();
page.Header = hfFirst;

// Nastavení okrajů záhlaví
hfFirst.Margin.Left = 50;
hfFirst.Margin.Right = 50;

// Přidat název do záhlaví
TextFragment t1 = new TextFragment("report title");
t1.TextState.Font = FontRepository.FindFont("Arial");
t1.TextState.FontSize = 16;
t1.TextState.ForegroundColor = Aspose.Pdf.Color.Black;
t1.TextState.FontStyle = FontStyles.Bold;
t1.TextState.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center;
hfFirst.Paragraphs.Add(t1);

// Přidat název sestavy do záhlaví
TextFragment t2 = new TextFragment("Report_Name");
t2.TextState.Font = FontRepository.FindFont("Arial");
t2.TextState.FontSize = 12;
t2.TextState.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center;
hfFirst.Paragraphs.Add(t2);
```

Přidali jsme dva `TextFragment` objekty do záhlaví: jeden pro název sestavy a druhý pro název sestavy. Text je stylizován pomocí `TextState` vlastnosti jako písmo, velikost a zarovnání.

## Krok 4: Vytvořte a nakonfigurujte zápatí

Nyní je čas nastavit zápatí, které bude obsahovat dynamický obsah, jako jsou čísla stránek a datum generování.

```csharp
// Vytvořit zápatí
HeaderFooter hfFoot = new HeaderFooter();
page.Footer = hfFoot;

// Nastavení okrajů zápatí
hfFoot.Margin.Left = 50;
hfFoot.Margin.Right = 50;

// Přidat obsah zápatí
TextFragment t3 = new TextFragment("Generated on test date");
TextFragment t4 = new TextFragment("Report Name");
TextFragment t5 = new TextFragment("Page $p of $P");
```

zápatí uvádíme fragmenty pro datum generování, název sestavy a dynamická čísla stránek (`$p` a `$P` představují aktuální číslo stránky a celkový počet stránek).

## Krok 5: Vytvořte tabulku v zápatí

Do zápatí můžete také přidat složitější prvky, jako jsou tabulky, pro lepší uspořádání dat.

```csharp
// Vytvořit tabulku pro zápatí
Table tab2 = new Table();
hfFoot.Paragraphs.Add(tab2);
tab2.ColumnWidths = "165 172 165";

// Vytvořte řádky a buňky pro tabulku
Row row3 = tab2.Rows.Add();
row3.Cells.Add();
row3.Cells.Add();
row3.Cells.Add();

// Nastavení zarovnání pro každou buňku
row3.Cells[0].Alignment = Aspose.Pdf.HorizontalAlignment.Left;
row3.Cells[1].Alignment = Aspose.Pdf.HorizontalAlignment.Center;
row3.Cells[2].Alignment = Aspose.Pdf.HorizontalAlignment.Right;

// Přidání obsahu do buněk tabulky
row3.Cells[0].Paragraphs.Add(t3);
row3.Cells[1].Paragraphs.Add(t4);
row3.Cells[2].Paragraphs.Add(t5);
```

Tento blok kódu vytvoří v zápatí tabulku se třemi sloupci, přičemž každý sloupec obsahuje různé informace, jako je datum generování, název sestavy a čísla stránek.

## Krok 6: Přidání obsahu na stránku

Kromě záhlaví a zápatí můžete do těla stránky PDF přidat obsah. Zde přidáme tabulku se zástupným textem.

```csharp
Table table = new Table();
table.ColumnWidths = "33% 33% 34%";
page.Paragraphs.Add(table);

// Přidat obsah tabulky
for (int i = 0; i <= 10; i++)
{
    Row row = table.Rows.Add();
    for (int c = 0; c <= 2; c++)
    {
        Cell cell = row.Cells.Add("Content " + c);
        cell.Margin = new MarginInfo { Left = 30, Top = 10, Bottom = 10 };
    }
}
```

Tento kód přidá na stránku jednoduchou tabulku se třemi sloupci. Můžete ji upravit podle svých specifických potřeb.

## Krok 7: Uložte PDF

Jakmile je vše nastaveno, posledním krokem je uložení PDF dokumentu na požadované místo.

```csharp
dataDir = dataDir + "ReplaceableSymbolsInHeaderFooter_out.pdf";
doc.Save(dataDir);
Console.WriteLine("Symbols replaced successfully in header and footer. File saved at " + dataDir);
```

Zadáte cestu k souboru a uložíte dokument pomocí `doc.Save()`Hotovo! Úspěšně jste vytvořili PDF s přizpůsobenými záhlavími a zápatími.

## Závěr

Nahrazení symbolů v záhlavích a zápatích pomocí Aspose.PDF pro .NET je nejen jednoduché, ale i efektivní. Dodržováním výše uvedeného podrobného návodu si můžete snadno přizpůsobit své PDF soubory dynamickým obsahem, jako jsou čísla stránek, názvy sestav a data. Tato metoda je vysoce flexibilní a umožňuje vám vkládat tabulky, upravovat formátování a ovládat rozvržení tak, aby vyhovovalo vašim specifickým požadavkům.

## Často kladené otázky

### Mohu si přizpůsobit písma pro záhlaví a zápatí?  
Ano, písma, velikosti, barvy a styly textu v záhlavích a zápatích si můžete plně přizpůsobit.

### Jak přidám obrázky do záhlaví a zápatí?  
Můžete použít `ImageStamp` vkládat obrázky do záhlaví a zápatí.

### Je možné přidat hypertextové odkazy do záhlaví nebo zápatí?  
Ano, můžete použít `TextFragment` s hypertextovým odkazem nastavením `Hyperlink` vlastnictví.

### Mohu použít různé záhlaví pro liché a sudé stránky?  
Ano, Aspose.PDF umožňuje zadat různé záhlaví a zápatí pro liché a sudé stránky.

### Jak upravím pozice záhlaví a zápatí?  
Okraje a vlastnosti zarovnání můžete upravit pro kontrolu polohy záhlaví a zápatí.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}