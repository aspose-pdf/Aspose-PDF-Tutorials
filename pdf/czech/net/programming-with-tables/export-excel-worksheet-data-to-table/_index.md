---
"description": "Naučte se, jak exportovat data z listu aplikace Excel do tabulky PDF pomocí nástroje Aspose.PDF pro .NET. Podrobný návod s příklady kódu, předpoklady a užitečnými tipy."
"linktitle": "Export dat z excelovského listu do tabulky"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Export dat z excelovského listu do tabulky"
"url": "/cs/net/programming-with-tables/export-excel-worksheet-data-to-table/"
"weight": 70
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Export dat z excelovského listu do tabulky

## Zavedení

Potřebovali jste někdy exportovat data z excelového listu do PDF souboru, úhledně uspořádaného do tabulkového formátu? Představte si, že máte v Excelu spoustu dat, ale potřebujete je sdílet jako profesionálně vypadající PDF. Může to znít složitě, že? Ale s Aspose.PDF pro .NET můžete tento úkol proměnit v hračku. V tomto tutoriálu vás provedeme procesem exportu dat z excelového listu do tabulky v PDF dokumentu pomocí Aspose.PDF pro .NET. Provedeme vás krok za krokem a vše rozebereme tak, abyste se i když s tímto tématem začínáte, na konci cítili jako profesionál.

## Předpoklady

Než se pustíme do kódování, pojďme si nastavit pár věcí:

1. Aspose.PDF pro knihovnu .NET – Ujistěte se, že máte nainstalovanou nejnovější verzi. Můžete [stáhněte si to zde](https://releases.aspose.com/pdf/net/).
2. Knihovna Aspose.Cells pro .NET – Budete ji potřebovat pro zpracování operací v Excelu. Stáhněte si ji z [zde](https://releases.aspose.com/cells/net/).
3. Vývojové prostředí .NET – Pro kódování bude perfektně fungovat nástroj jako Visual Studio.
4. Soubor Excel – Mějte připravený soubor Excel s daty, která chcete exportovat.

Pokud nemáte knihovny Aspose.PDF a Aspose.Cells, můžete začít s [bezplatná zkušební verze](https://releases.aspose.com/).

## Importovat balíčky

Nejprve se ujistěte, že máte ve svém projektu nainstalovány knihovny Aspose.PDF a Aspose.Cells. Můžete je nainstalovat pomocí Správce balíčků NuGet ve Visual Studiu.

Zde je návod, jak importovat potřebné balíčky do kódu C#:

```csharp
using System.Data;
using System.IO;
using System.Linq;
```

Nyní, když jsou nastaveny předpoklady, pojďme si projít proces exportu dat z excelového listu do tabulky v dokumentu PDF.

## Krok 1: Načtení sešitu aplikace Excel

Nejprve je třeba do programu načíst sešit aplikace Excel. V tomto kroku použijeme Aspose.Cells k otevření souboru aplikace Excel.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Načtení sešitu aplikace Excel
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(new FileStream(dataDir + "newBook1.xlsx", FileMode.Open));
```

Vysvětlení: Zde zadáme cestu k adresáři, kde se nachází náš soubor Excel, a načteme sešit pomocí `Aspose.Cells.Workbook`Nezapomeňte upravit `"YOUR DOCUMENT DIRECTORY"` aby ukazoval na umístění vašeho souboru.

## Krok 2: Přístup k prvnímu pracovnímu listu

Po načtení sešitu potřebujeme přistupovat k prvnímu listu, kde jsou uložena naše data.

```csharp
// Přístup k prvnímu listu v souboru aplikace Excel
Aspose.Cells.Worksheet worksheet = workbook.Worksheets[0];
```

Vysvětlení: Tento krok je jednoduchý – z sešitu si vezmeme první list, který obsahuje data k exportu.

## Krok 3: Export dat do DataTable

Nyní exportujme data z excelovského listu do objektu DataTable, který bude sloužit jako prostředník pro přenos dat do PDF.

```csharp
// Export obsahu 7 řádků a 2 sloupců počínaje 1. buňkou do DataTable
DataTable dataTable = worksheet.Cells.ExportDataTable(0, 0, worksheet.Cells.MaxRow + 1, worksheet.Cells.MaxColumn + 1, true);
```

Vysvětlení: `ExportDataTable` Metoda extrahuje data počínaje první buňkou listu a zahrnuje všechny řádky a sloupce. Tato data jsou poté uložena v `DataTable` pro další použití.

## Krok 4: Vytvořte nový dokument PDF

Dále musíme vytvořit nový PDF dokument pomocí Aspose.PDF.

```csharp
// Vytvoření instance dokumentu
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document();

// Vytvořte stránku v instanci dokumentu
Aspose.Pdf.Page page = pdfDocument.Pages.Add();
```

Vysvětlení: Zde inicializujeme nový `Aspose.Pdf.Document` a přidejte k ní stránku. Tato stránka bude později obsahovat tabulku, kterou vytváříme z dat z Excelu.

## Krok 5: Vytvořte objekt tabulky v PDF

Pojďme k vytvoření tabulky uvnitř dokumentu PDF.

```csharp
// Vytvoření objektu Table
Aspose.Pdf.Table table = new Aspose.Pdf.Table();

// Přidejte objekt Table do kolekce odstavců stránky.
page.Paragraphs.Add(table);
```

Vysvětlení: Vytvoříme `Aspose.Pdf.Table` objekt a přidejte ho do kolekce paragraphs stránky, což zajistí, že se tabulka na stránce zobrazí.

## Krok 6: Nastavení šířky a ohraničení sloupců

Tabulky v PDF potřebují definovanou šířku sloupců. Také přidáme ohraničení, aby byla tabulka čitelnější.

```csharp
// Nastavení šířky sloupců tabulky
table.ColumnWidths = "40 100 100";

// Nastavení výchozího ohraničení buňky
table.DefaultCellBorder = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 0.1F);
```

Vysvětlení: Nastavíme šířku tří sloupců a všem buňkám dáme výchozí ohraničení o tloušťce `0.1F`.

## Krok 7: Import dat z DataTable do PDF tabulky

Nyní je čas importovat data z DataTable do naší tabulky PDF.

```csharp
// Import dat do objektu Table z DataTable
table.ImportDataTable(dataTable, true, 0, 0, dataTable.Rows.Count + 1, dataTable.Columns.Count);
```

Vysvětlení: `ImportDataTable` metoda přenáší všechna data z `DataTable` do tabulky PDF. Tím se tabulka naplní daty z vašeho excelového listu.

## Krok 8: Stylizace řádku záhlaví

Upravme styl záhlaví tabulky změnou barvy pozadí, písma a zarovnání.

```csharp
// Získejte první řádek z tabulky
Aspose.Pdf.Row headerRow = table.Rows[0];

// Nastavení stylu pro řádek záhlaví
foreach (Aspose.Pdf.Cell cell in headerRow.Cells)
{
    cell.BackgroundColor = Color.Blue;
    cell.DefaultCellTextState.Font = Aspose.Pdf.Text.FontRepository.FindFont("Helvetica-Oblique");
    cell.DefaultCellTextState.ForegroundColor = Color.Yellow;
    cell.DefaultCellTextState.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center;
}
```

Vysvětlení: Projdeme všechny buňky v prvním řádku (záhlaví) a nastavíme jim barvu pozadí na modrou, barvu textu na žlutou a zarovnáme text na střed.

## Krok 9: Stylizace zbývajících řádků

Abychom rozlišili mezi záhlavím a zbytkem řádků, přidejme pro zbývající řádky jiný styl.

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++)
{
    foreach (Aspose.Pdf.Cell cell in table.Rows[i].Cells)
    {
        cell.BackgroundColor = Color.Gray;
        cell.DefaultCellTextState.ForegroundColor = Color.White;
    }
}
```

Vysvětlení: Pro všechny řádky kromě záhlaví jsme nastavili šedé pozadí a bílou barvu textu.

## Krok 10: Uložení dokumentu PDF

Nakonec uložte dokument PDF s tabulkou.

```csharp
// Uložit PDF
pdfDocument.Save(dataDir + "Exceldata_toPdf_table.pdf");
```

Vysvětlení: Uložíme PDF do zadaného adresáře. Voilà! Vaše data z Excelu jsou nyní uvnitř krásně naformátované tabulky PDF.

## Závěr

A je to! V několika krocích jste exportovali data z excelového listu do tabulky v PDF pomocí Aspose.PDF pro .NET. Rozdělením procesu a jeho úpravou si můžete přizpůsobit výstup a zajistit, aby vaše data vypadala čistě a profesionálně. Takže až vám příště někdo podá excelový soubor a požádá o PDF zprávu, budete přesně vědět, co dělat.

## Často kladené otázky

### Mohu si stůl více přizpůsobit?
Rozhodně! Můžete upravovat barvy, písma, zarovnání a dokonce i přidávat ohraničení k určitým buňkám.

### Je Aspose.PDF pro .NET zdarma?
Nabízí bezplatnou zkušební verzi, ale pro delší používání budete potřebovat licenci. Můžete [kupte si to zde](https://purchase.aspose.com/buy).

### Mohu exportovat pouze určité řádky a sloupce?
Ano, parametry můžete upravit v `ExportDataTable` metoda pro export specifických rozsahů.

### Funguje to s velkými soubory Excelu?
Ano, Aspose.Cells je navržen pro efektivní zpracování velkých souborů aplikace Excel.

### Jak mohu do PDF přidat další stránky?
Můžete použít `pdfDocument.Pages.Add()` přidat tolik stránek, kolik potřebujete.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}