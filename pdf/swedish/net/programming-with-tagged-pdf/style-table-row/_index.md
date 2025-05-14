---
"description": "Lär dig hur du formaterar tabellrader i en PDF med Aspose.PDF för .NET med en steg-för-steg-guide för att enkelt förbättra dokumentformateringen."
"linktitle": "Stiltabellrad"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Stiltabellrad"
"url": "/sv/net/programming-with-tagged-pdf/style-table-row/"
"weight": 180
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Stiltabellrad

## Introduktion

När det gäller att skapa välstrukturerade och vackert formaterade PDF-dokument är Aspose.PDF för .NET en självklar lösning. Oavsett om du automatiserar rapporter, fakturor eller skapar dynamiska tabeller är formatering av tabeller med olika stilar nyckeln till ett polerat dokument. I den här handledningen går vi djupare in i hur man utformar en tabellrad med Aspose.PDF för .NET. Och oroa dig inte, jag guidar dig steg för steg, precis som ett bra samtal över en kopp kaffe!

## Förkunskapskrav

Innan vi går in på detaljerna, låt oss se till att du har allt på plats. Du behöver:

1. Aspose.PDF för .NET-bibliotek  
   Om du inte redan har den kan du hämta den från [här](https://releases.aspose.com/pdf/net/)Du kan också få en [gratis provperiod](https://releases.aspose.com/) att komma igång.
2. Utvecklingsmiljö  
   Installera Visual Studio eller valfri C# IDE. Du behöver också .NET installerat, men jag antar att du redan är bekant med det.
3. Grundläggande kunskaper i C# och .NET  
   Goda kunskaper i C# gör den här handledningen enkel. Men oroa dig inte, jag kommer att förklara varje steg i detalj!

## Importera paket

Innan vi kan börja arbeta med Aspose.PDF måste vi importera de nödvändiga namnrymderna. Se till att du inkluderar följande i ditt C#-projekt:

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Dessa är viktiga för att skapa och formatera tabellen, och naturligtvis för att arbeta med taggat innehåll för att säkerställa efterlevnad.

Nu ska vi gå igenom uppgiften steg för steg, så att du kan utforma dina tabellrader som ett proffs!

## Steg 1: Skapa ett nytt PDF-dokument

Först och främst: låt oss skapa ett helt nytt PDF-dokument. Det här dokumentet kommer att innehålla alla formaterade tabellrader.

```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Skapa dokument
Document document = new Document();
```

Här initierar vi helt enkelt en ny `Document` objektet som ska representera vår PDF-fil. Se till att ange sökvägen till katalogen där du ska spara dina utdatafiler.

## Steg 2: Arbeta med taggat innehåll

För att strukturera din PDF för tillgänglighet arbetar vi med taggat innehåll. Detta hjälper till att skapa strukturerade element som tabeller och säkerställer att de följer tillgänglighetsstandarder som PDF/UA.

```csharp
ITaggedContent taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example table row style");
taggedContent.SetLanguage("en-US");
```

Här ställer vi in titel och språk för PDF-filens taggade innehåll. Det är som att ge din PDF ett namn och ange vilket språk den ska tala!

## Steg 3: Definiera tabellstrukturen

Nu ska vi definiera strukturen för tabellen vi ska skapa. Varje tabell behöver en sidhuvud, brödtext och sidfot – ungefär som ett välorganiserat blogginlägg!

```csharp
// Hämta rotstrukturelement
StructureElement rootElement = taggedContent.RootElement;

// Skapa tabellstrukturelement
TableElement tableElement = taggedContent.CreateTableElement();
rootElement.AppendChild(tableElement);
TableTHeadElement tableTHeadElement = tableElement.CreateTHead();
TableTBodyElement tableTBodyElement = tableElement.CreateTBody();
TableTFootElement tableTFootElement = tableElement.CreateTFoot();
```

Det vi gör här är att skapa en tabell med en rubrik (`THead`), kropp (`TBody`), och sidfot (`TFoot`). Dessa element kommer att hålla våra rader.

## Steg 4: Lägg till tabellrubrikraden

Tabeller utan rubriker är som böcker utan titlar. Låt oss först skapa rubrikraden för att ge sammanhang för informationen.

```csharp
TableTRElement headTrElement = tableTHeadElement.CreateTR();
headTrElement.AlternativeText = "Head Row";
for (int colIndex = 0; colIndex < 3; colIndex++)
{
    TableTHElement thElement = headTrElement.CreateTH();
    thElement.SetText(String.Format("Head {0}", colIndex));
}
```

Här loopar vi igenom och lägger till tre rubrikceller (`TableTHElement`), vilket ger var och en en beskrivande text. Enkelt, eller hur?

## Steg 5: Lägg till stiliserade brödtextrader

Nu kommer den roliga delen – att utforma raderna! Nu skapar vi sju rader med anpassade stilar. Vi anger bakgrundsfärger, ramar, utfyllnad och textjustering.

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

- Bakgrundsfärg: Vi använde en ljus gullrisgul för en professionell men ändå varm touch.
- Kantlinjer: Varje rad får en mörkgrå yttre kantlinje och blå cellkantlinjer för ett skarpt utseende.
- Höjd och utfyllnad: Radhöjderna är inställda och utfyllnad läggs till för ett rent utseende.
- Sidbrytningar: För att göra tabellen mer läsbar börjar varannan rad på en ny sida.

## Steg 6: Lägg till sidfotsraden

Precis som sidhuvudet förankrar sidfoten tabellen. Nu skapar vi en.

```csharp
TableTRElement footTrElement = tableTFootElement.CreateTR();
footTrElement.AlternativeText = "Foot Row";
for (int colIndex = 0; colIndex < 3; colIndex++)
{
    TableTDElement tdElement = footTrElement.CreateTD();
    tdElement.SetText(String.Format("Foot {0}", colIndex));
}
```

Vi loopar helt enkelt igenom tre sidfotsceller och lägger till lite text. Alternativtexten för sidfoten är "Fotrad" för att göra den tillgänglig.

## Steg 7: Spara PDF-dokumentet

Nu när bordet är uppställt är det dags att spara ditt mästerverk!

```csharp
document.Save(dataDir + "StyleTableRow.pdf");
```

Precis så sparas din PDF med alla de vackra tabellrader vi just har formaterat.

## Steg 8: Validera PDF/UA-efterlevnad

För att säkerställa att vår PDF följer tillgänglighetsstandarder validerar vi den för PDF/UA-kompatibilitet.

```csharp
document = new Document(dataDir + "StyleTableRow.pdf");
bool isPdfUaCompliance = document.Validate(dataDir + "StyleTableRow.xml", PdfFormat.PDF_UA_1);
Console.WriteLine(String.Format("PDF/UA compliance: {0}", isPdfUaCompliance));
```

Detta säkerställer att din PDF uppfyller PDF/UA-standarden, vilket gör den tillgänglig för alla. Tillgänglighet är nyckelordet!

## Slutsats

Och där har du det! Med bara några få rader kod har du skapat en helt formaterad tabell i en PDF med Aspose.PDF för .NET. Från sidhuvuden till sidfot har vi formaterat varje rad, lagt till tillgänglighetselement och till och med validerat dokumentet för efterlevnad. Oavsett om du arbetar med företagsrapporter, presentationer eller bara har kul med PDF-filer, har den här guiden allt du behöver. Nu kan du börja formatera dina tabeller som ett proffs!

## Vanliga frågor

### Kan jag även ändra tabellens teckensnitt?  
Ja! Du kan ändra teckensnittet med hjälp av `TextState` objekt för varje cell, vilket möjliggör fullständig anpassning.

### Hur lägger jag till fler kolumner i min tabell?  
Justera bara `colCount` variabel och lägg till fler celler i looparna för sidhuvud, brödtext och sidfot.

### Vad händer om jag inte anger radhöjden?  
Om du inte anger radhöjden justeras tabellen automatiskt baserat på innehållet.

### Kan jag använda detta för ett dynamiskt antal rader?  
Absolut! Du kan hämta data från en databas eller någon annan källa och dynamiskt justera rad- och kolumnantalet.

### Är Aspose.PDF för .NET gratis att använda?  
Aspose.PDF för .NET är en licensierad produkt, men du kan prova den med en [gratis provperiod](https://releases.aspose.com/) eller få en [tillfällig licens](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}