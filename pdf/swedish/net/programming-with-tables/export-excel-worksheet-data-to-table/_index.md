---
"description": "Lär dig hur du exporterar Excel-kalkylbladsdata till en PDF-tabell med Aspose.PDF för .NET. Steg-för-steg-handledning med kodexempel, förkunskapskrav och användbara tips."
"linktitle": "Exportera Excel-kalkylbladsdata till tabell"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Exportera Excel-kalkylbladsdata till tabell"
"url": "/sv/net/programming-with-tables/export-excel-worksheet-data-to-table/"
"weight": 70
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Exportera Excel-kalkylbladsdata till tabell

## Introduktion

Har du någonsin behövt exportera data från ett Excel-kalkylblad till en PDF-fil, prydligt ordnade i ett tabellformat? Tänk dig att ha en massa data i Excel, men behöva dela den som en professionell PDF. Det kan låta komplicerat, eller hur? Men med Aspose.PDF för .NET kan du göra den här uppgiften till en barnlek. I den här handledningen guidar vi dig genom processen att exportera Excel-kalkylbladsdata till en tabell i ett PDF-dokument med hjälp av Aspose.PDF för .NET. Vi tar dig steg för steg och bryter ner allt så att även om du är nybörjare på detta kommer du att känna dig som ett proffs i slutet.

## Förkunskapskrav

Innan vi går in i kodningen, låt oss få några saker konfigurerade:

1. Aspose.PDF för .NET-biblioteket – Se till att du har den senaste versionen installerad. Du kan [ladda ner den här](https://releases.aspose.com/pdf/net/).
2. Aspose.Cells för .NET-biblioteket – Du behöver detta för att hantera Excel-operationer. Ladda ner det från [här](https://releases.aspose.com/cells/net/).
3. .NET-utvecklingsmiljö – Ett verktyg som Visual Studio fungerar perfekt för kodning.
4. Excel-fil – Ha en Excel-fil med den data du vill exportera redo.

Om du inte har biblioteken Aspose.PDF och Aspose.Cells kan du börja med en [gratis provperiod](https://releases.aspose.com/).

## Importera paket

Till att börja med, se till att du har installerat både Aspose.PDF- och Aspose.Cells-biblioteken i ditt projekt. Du kan installera dem med hjälp av NuGet Package Manager i Visual Studio.

Så här importerar du nödvändiga paket i din C#-kod:

```csharp
using System.Data;
using System.IO;
using System.Linq;
```

Nu när förutsättningarna är ställda, låt oss gå igenom processen för att exportera data från ett Excel-ark till en tabell i ett PDF-dokument.

## Steg 1: Läs in Excel-arbetsboken

För att börja behöver du ladda din Excel-arbetsbok i programmet. I det här steget använder vi Aspose.Cells för att öppna Excel-filen.

```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Läs in Excel-arbetsboken
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(new FileStream(dataDir + "newBook1.xlsx", FileMode.Open));
```

Förklaring: Här anger vi sökvägen till katalogen där vår Excel-fil finns och laddar arbetsboken med hjälp av `Aspose.Cells.Workbook`Se till att justera `"YOUR DOCUMENT DIRECTORY"` för att peka på din fils plats.

## Steg 2: Öppna det första arbetsbladet

Efter att vi har laddat arbetsboken behöver vi komma åt det första kalkylbladet där våra data lagras.

```csharp
// Åtkomst till det första kalkylbladet i Excel-filen
Aspose.Cells.Worksheet worksheet = workbook.Worksheets[0];
```

Förklaring: Det här steget är enkelt – vi hämtar det första kalkylbladet från arbetsboken, som innehåller de data som ska exporteras.

## Steg 3: Exportera data till datatabellen

Nu ska vi exportera data från Excel-arket till ett DataTable-objekt, som fungerar som en mellanhand för att överföra data till PDF-filen.

```csharp
// Exportera innehållet i 7 rader och 2 kolumner med början från den första cellen till DataTable
DataTable dataTable = worksheet.Cells.ExportDataTable(0, 0, worksheet.Cells.MaxRow + 1, worksheet.Cells.MaxColumn + 1, true);
```

Förklaring: Den `ExportDataTable` Metoden extraherar data från den första cellen i kalkylbladet och sträcker sig över alla rader och kolumner. Dessa data lagras sedan i en `DataTable` för vidare användning.

## Steg 4: Skapa ett nytt PDF-dokument

Sedan måste vi skapa ett nytt PDF-dokument med Aspose.PDF.

```csharp
// Instansiera en dokumentinstans
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document();

// Skapa en sida i dokumentinstansen
Aspose.Pdf.Page page = pdfDocument.Pages.Add();
```

Förklaring: Här initierar vi en ny `Aspose.Pdf.Document` och lägg till en sida på den. Den här sidan kommer senare att innehålla tabellen vi skapar från Excel-data.

## Steg 5: Skapa ett tabellobjekt i PDF

Låt oss gå vidare till att skapa en tabell inuti PDF-dokumentet.

```csharp
// Skapa ett tabellobjekt
Aspose.Pdf.Table table = new Aspose.Pdf.Table();

// Lägg till Table-objektet i sidans styckensamling
page.Paragraphs.Add(table);
```

Förklaring: Vi skapar en `Aspose.Pdf.Table` objektet och lägg till det i sidans stycken samling, vilket säkerställer att tabellen visas på sidan.

## Steg 6: Ställ in kolumnbredder och kantlinjer

Tabeller i PDF behöver definierade kolumnbredder. Vi kommer också att lägga till ramar för att göra tabellen mer läsbar.

```csharp
// Ange kolumnbredder för tabellen
table.ColumnWidths = "40 100 100";

// Ange standardcellkantlinje
table.DefaultCellBorder = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 0.1F);
```

Förklaring: Vi ställer in bredden på de tre kolumnerna och ger alla celler en standardkantlinje med en tjocklek på `0.1F`.

## Steg 7: Importera data från datatabellen till PDF-tabellen

Nu är det dags att importera data från datatabellen till vår PDF-tabell.

```csharp
// Importera data till tabellobjektet från datatabellen
table.ImportDataTable(dataTable, true, 0, 0, dataTable.Rows.Count + 1, dataTable.Columns.Count);
```

Förklaring: Den `ImportDataTable` Metoden överför all data från `DataTable` till PDF-tabellen. Detta fyller tabellen med data från ditt Excel-ark.

## Steg 8: Stilisera rubrikraden

Nu ska vi formatera tabellens rubrikrad genom att ändra bakgrundsfärg, teckensnitt och justering.

```csharp
// Hämta den första raden från tabellen
Aspose.Pdf.Row headerRow = table.Rows[0];

// Ange formatering för rubrikraden
foreach (Aspose.Pdf.Cell cell in headerRow.Cells)
{
    cell.BackgroundColor = Color.Blue;
    cell.DefaultCellTextState.Font = Aspose.Pdf.Text.FontRepository.FindFont("Helvetica-Oblique");
    cell.DefaultCellTextState.ForegroundColor = Color.Yellow;
    cell.DefaultCellTextState.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center;
}
```

Förklaring: Vi loopar igenom alla celler i den första raden (rubriken) och ställer in deras bakgrundsfärg till blå, textfärgen till gul och justerar texten till mitten.

## Steg 9: Stilisera de återstående raderna

För att skilja mellan rubriken och resten av raderna, låt oss lägga till en annan stil för de återstående raderna.

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

Förklaring: För alla rader utom rubriken anger vi en grå bakgrund och vit textfärg.

## Steg 10: Spara PDF-dokumentet

Spara slutligen PDF-dokumentet med tabellen.

```csharp
// Spara PDF-filen
pdfDocument.Save(dataDir + "Exceldata_toPdf_table.pdf");
```

Förklaring: Vi sparar PDF-filen i den angivna katalogen. Voilà! Dina Excel-data finns nu i en vackert formaterad PDF-tabell.

## Slutsats

Och där har du det! Med bara några få steg har du exporterat data från ett Excel-kalkylblad till en tabell i en PDF-fil med hjälp av Aspose.PDF för .NET. Genom att bryta ner processen och utforma den längs vägen kan du anpassa din utdata och se till att dina data ser rena och professionella ut. Så nästa gång någon ger dig en Excel-fil och ber om en PDF-rapport vet du exakt vad du ska göra.

## Vanliga frågor

### Kan jag anpassa tabellen mer?
Absolut! Du kan ändra färger, teckensnitt, justering och till och med lägga till ramar runt specifika celler.

### Är Aspose.PDF för .NET gratis?
Den erbjuder en gratis provperiod, men för längre tids användning behöver du en licens. Du kan [köp den här](https://purchase.aspose.com/buy).

### Kan jag bara exportera specifika rader och kolumner?
Ja, du kan ändra parametrarna i `ExportDataTable` metod för att exportera specifika intervall.

### Fungerar detta med stora Excel-filer?
Ja, Aspose.Cells är utformat för att hantera stora Excel-filer effektivt.

### Hur kan jag lägga till fler sidor i PDF-filen?
Du kan använda `pdfDocument.Pages.Add()` för att lägga till så många sidor som du behöver.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}