---
"description": "Lär dig hur du lägger till upprepade kolumner i PDF-dokument med Aspose.PDF för .NET. Steg-för-steg-guide med exempel och kod. Perfekt för utvecklare."
"linktitle": "Lägg till upprepande kolumn i PDF-dokument"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Lägg till upprepande kolumn i PDF-dokument"
"url": "/sv/net/programming-with-tables/add-repeating-column/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till upprepande kolumn i PDF-dokument

## Introduktion

Om du arbetar med PDF-dokument och behöver lägga till upprepade kolumner har du kommit rätt! Med Aspose.PDF för .NET kan du enkelt hantera tabeller och innehåll i en PDF. Oavsett om du skapar dynamiska rapporter, fakturor eller andra strukturerade dokument kan upprepade kolumner vara banbrytande när det gäller att organisera data. Låt oss dyka ner i en steg-för-steg-guide om hur du lägger till upprepade kolumner i ett PDF-dokument.

## Förkunskapskrav

Innan vi går in i koden, låt oss se till att du har allt konfigurerat:

- Aspose.PDF för .NET: Du måste ha Aspose.PDF för .NET-biblioteket installerat i ditt projekt.
- [Ladda ner Aspose.PDF för .NET](https://releases.aspose.com/pdf/net/)
- [Gratis provperiod](https://releases.aspose.com/)
- Utvecklingsmiljö: Se till att du har en .NET-kompatibel IDE, till exempel Visual Studio, installerad.
- Grundläggande förståelse för C#: Vi kommer att gå igenom allting, men en grundläggande förståelse för C# hjälper dig att följa med smidigt.
  
Om du inte har Aspose.PDF för .NET ännu kan du skaffa en [tillfällig licens](https://purchase.aspose.com/temporary-license/) för att börja utforska dess funktioner.

## Importera paket

För att börja måste du importera de nödvändiga namnrymderna från Aspose.PDF för .NET. Så här gör du:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

Dessa paket tillhandahåller de grundläggande klasser och metoder som krävs för att arbeta med PDF-dokument och manipulera tabeller.

Nu ska vi dela upp processen i flera steg för att lägga till upprepade kolumner i ett PDF-dokument. Följ med!

## Steg 1: Ange sökvägen till din dokumentkatalog

Innan vi skapar eller manipulerar några filer måste vi definiera sökvägen dit den genererade PDF-filen ska sparas. I ditt C#-projekt, ange katalogsökvägen till där dina filer ska finnas:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "AddRepeatingColumn_out.pdf";
```

Den här sökvägen pekar till katalogen där den utgående PDF-filen kommer att sparas. Ersätt `"YOUR DOCUMENT DIRECTORY"` med den faktiska sökvägen på din maskin.

## Steg 2: Skapa ett nytt PDF-dokument

Till att börja med, instansiera en ny `Document` objekt. Detta kommer att fungera som behållare för alla sidor och innehåll i PDF-filen.

```csharp
Document doc = new Document();
Aspose.Pdf.Page page = doc.Pages.Add();
```

Här har vi skapat ett nytt PDF-dokument och lagt till en tom sida i det. `doc.Pages.Add()` Metoden infogar en ny sida i dokumentet.

## Steg 3: Instansiera den yttre tabellen

Nästa steg är att skapa en yttre tabell. Tabellen kommer att täcka hela sidans bredd och fungera som en behållare för andra tabeller, inklusive den som kommer att innehålla de upprepade kolumnerna.

```csharp
Aspose.Pdf.Table outerTable = new Aspose.Pdf.Table();
outerTable.ColumnWidths = "100%";
outerTable.HorizontalAlignment = HorizontalAlignment.Left;
```

Vi har satt `ColumnWidths` egenskapen till "100%", vilket innebär att tabellen kommer att sträckas över hela sidbredden.

## Steg 4: Skapa den inre tabellen

Nu ska vi skapa den inre tabellen, som kommer att ha upprepade kolumner. De viktigaste egenskaperna här är `Broken`, vilket gör att tabellen kan fortsätta över samma sida, och `ColumnAdjustment`, som automatiskt justerar kolumnbredden så att den passar innehållet.

```csharp
Aspose.Pdf.Table mytable = new Aspose.Pdf.Table();
mytable.Broken = TableBroken.VerticalInSamePage;
mytable.ColumnAdjustment = ColumnAdjustment.AutoFitToContent;
```

Den här inre tabellen kommer att kapslas in i den yttre tabellen.

## Steg 5: Lägg till tabeller på sidan

Nu när vi har både den yttre och den inre tabellen redo, låt oss lägga till dem på sidan. Detta steg säkerställer att tabellerna inkluderas i dokumentets struktur.

```csharp
page.Paragraphs.Add(outerTable);
var bodyRow = outerTable.Rows.Add();
var bodyCell = bodyRow.Cells.Add();
bodyCell.Paragraphs.Add(mytable);
mytable.RepeatingColumnsCount = 5;
```

Här lade vi till `outerTable` till sidan, och sedan inom den yttre tabellen kapslade vi `mytable`Dessutom satte vi `RepeatingColumnsCount` till 5, som anger hur många kolumner som ska upprepas när data läggs till.

## Steg 6: Lägg till rubrikrad

Nu är det dags att lägga till rubrikerna i tabellen. Rubrikraden ger sammanhang till informationen och hjälper till att strukturera kolumnerna. 

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

Det här kodavsnittet lägger till den första raden (som vi kommer att använda som rubriker) och fyller den med celler som innehåller text som "rubrik 1", "rubrik 2" och så vidare.

## Steg 7: Lägg till datarader

Slutligen kan vi lägga till lite data i tabellen. Denna loop skapar dynamiskt rader och fyller cellerna med innehåll:

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

Loopen itererar sex gånger, lägger till rader och fyller varje cell med motsvarande kolumndata (t.ex. "kolumn 1, 1", "kolumn 2, 2", etc.).

## Steg 8: Spara dokumentet

När alla rader och kolumner har lagts till är det sista steget att spara dokumentet till den angivna sökvägen.

```csharp
doc.Save(outFile);
```

Ditt dokument är nu sparat med upprepade kolumner!

## Slutsats

Där har du det! Med dessa enkla steg kan du skapa ett PDF-dokument med upprepade kolumner med Aspose.PDF för .NET. Genom att utnyttja flexibiliteten hos kapslade tabeller kan du uppnå komplexa layouter som gör att dina PDF-filer ser professionella och organiserade ut. Testa detta för ditt nästa projekt och utforska Aspose.PDFs fulla potential för att hantera dina PDF-genereringsbehov.

## Vanliga frågor

### Vad är Aspose.PDF för .NET?
Aspose.PDF för .NET är ett kraftfullt bibliotek som låter utvecklare skapa, redigera och hantera PDF-dokument programmatiskt.

### Kan jag justera antalet upprepade kolumner dynamiskt?
Ja, du kan ändra antalet upprepade kolumner genom att modifiera `RepeatingColumnsCount` egendom.

### Hur kan jag ansöka om en licens till Aspose.PDF för .NET?
Du kan tillämpa en licens från en fil eller ström genom att följa anvisningarna [dokumentation](https://reference.aspose.com/pdf/net/).

### Är det möjligt att lägga till bilder i tabellcellerna?
Ja, Aspose.PDF för .NET stöder att lägga till olika typer av innehåll, inklusive bilder, i tabellceller.

### Kan jag anpassa tabelllayouten ytterligare?
Absolut! Aspose.PDF erbjuder omfattande funktioner för att anpassa tabellstilar, inklusive kantlinjer, utfyllnad, justering och mer.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}