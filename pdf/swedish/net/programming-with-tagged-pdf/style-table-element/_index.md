---
"description": "Lär dig hur du skapar och formaterar ett tabellelement i Aspose.PDF för .NET med steg-för-steg-instruktioner, anpassad formatering och PDF/UA-kompatibilitet."
"linktitle": "Stiltabellelement"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Stiltabellelement"
"url": "/sv/net/programming-with-tagged-pdf/style-table-element/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Stiltabellelement

## Introduktion

den här artikeln går vi in på hur man skapar och formaterar ett tabellelement med Aspose.PDF för .NET. Du lär dig hur du strukturerar en tabell, tillämpar anpassade format och validerar PDF/UA-kompatibiliteten i ditt dokument. I slutet av den här handledningen kommer du enkelt att kunna skapa professionella tabeller i dina PDF-filer!

## Förkunskapskrav

Innan du börjar med handledningen måste du se till att du har följande:

1. Visual Studio eller en liknande IDE installerad på din dator.
2. .NET Framework eller .NET Core SDK för att köra programmet.
3. Aspose.PDF för .NET-biblioteket har laddats ner och refererats till i ditt projekt. Du kan hämta den senaste versionen från [här](https://releases.aspose.com/pdf/net/).
4. En giltig Aspose-licens eller en [tillfällig licens](https://purchase.aspose.com/temporary-license/) för att låsa upp bibliotekets fulla funktionalitet.

## Importera paket

För att börja, importera de nödvändiga namnrymderna till ditt projekt:

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Dessa namnrymder täcker centrala PDF-åtgärder, taggat innehåll, tabeller och textformatering.

Nu ska vi gå igenom processen för att skapa och formatera en tabell i Aspose.PDF. Vi går igenom varje avsnitt i detalj så att du kan följa med.

## Steg 1: Skapa ett nytt PDF-dokument och konfigurera taggat innehåll

I det här första steget skapar vi ett tomt PDF-dokument och konfigurerar dess taggade innehåll.

```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Skapa ett nytt PDF-dokument
Document document = new Document();

// Konfigurera taggat innehåll
ITaggedContent taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example table style");
taggedContent.SetLanguage("en-US");
```

Vi börjar med att skapa ett nytt `Document` objekt, som representerar vår PDF. Den `TaggedContent` objektet används för att hantera dokumentets struktur och säkerställa att tillgänglighetsstandarder följs. Vi anger dokumentets titel och språk för korrekt taggning.

## Steg 2: Definiera rotelementet

Nästa steg är att skapa rotstrukturelementet, som fungerar som behållare för allt innehåll i vår PDF-fil.

```csharp
// Hämta rotstrukturelementet
StructureElement rootElement = taggedContent.RootElement;
```

De `RootElement` fungerar som basbehållare för alla strukturerade element, inklusive vår tabell. Den hjälper till att upprätthålla dokumentets strukturella hierarki, vilket är viktigt för både organisation och tillgänglighet.

## Steg 3: Skapa och formatera tabellelementet

Nu när rotelementet är konfigurerat skapar vi ett `TableElement` och tillämpa stilar som bakgrundsfärg, kantlinjer och justering.

```csharp
// Skapa tabellstrukturelement
TableElement tableElement = taggedContent.CreateTableElement();
rootElement.AppendChild(tableElement);

// Styla bordet
tableElement.BackgroundColor = Color.Beige;
tableElement.Border = new BorderInfo(BorderSide.All, 0.80F, Color.Gray);
tableElement.Alignment = HorizontalAlignment.Center;
tableElement.Broken = TableBroken.Vertical;
tableElement.ColumnAdjustment = ColumnAdjustment.AutoFitToWindow;
```

Vi skapar en `TableElement`, vilket definierar vår tabellstruktur. Den `BackgroundColor`, `Border`och `Alignment` egenskaperna låter oss anpassa tabellens utseende. `Broken` Egenskapen säkerställer att om tabellen bryts över flera sidor, så bryts den vertikalt.

## Steg 4: Ange tabelldimensioner och cellformat

I det här steget definierar vi antalet kolumner, cellfyllning och andra viktiga tabellegenskaper.

```csharp
tableElement.ColumnWidths = "80 80 80 80 80";
tableElement.DefaultCellBorder = new BorderInfo(BorderSide.All, 0.50F, Color.DarkBlue);
tableElement.DefaultCellPadding = new MarginInfo(16.0, 2.0, 8.0, 2.0);
tableElement.DefaultCellTextState.ForegroundColor = Color.DarkCyan;
tableElement.DefaultCellTextState.FontSize = 8F;
```

Vi anger kolumnbredderna för att säkerställa att varje kolumn i tabellen är jämnt fördelad. `DefaultCellBorder`, `DefaultCellPadding`och `DefaultCellTextState` definiera standardstilarna för cellerna, inklusive kantlinjer, utfyllnad, textfärg och teckenstorlek.

## Steg 5: Lägg till upprepade rader och anpassade stilar

Vi kan också definiera stilar för upprepade rader och andra specifika tabellelement som sidhuvuden och sidfot.

```csharp
tableElement.RepeatingRowsCount = 3;
TextState rowStyle = new TextState();
rowStyle.BackgroundColor = Color.LightCoral;
tableElement.RepeatingRowsStyle = rowStyle;
```

De `RepeatingRowsCount` säkerställer att de tre första raderna upprepas om tabellen sträcker sig över flera sidor. Vi ställer in `RepeatingRowsStyle` för att tillämpa en anpassad bakgrundsfärg på dessa rader.

## Steg 6: Lägg till bordets huvud-, stomme- och fotelement

Nu ska vi skapa tabellens sidhuvud, brödtext och sidfot och fylla dem med innehåll.

```csharp
TableTHeadElement tableTHeadElement = tableElement.CreateTHead();
TableTBodyElement tableTBodyElement = tableElement.CreateTBody();
TableTFootElement tableTFootElement = tableElement.CreateTFoot();

// Skapa rubrikrad
TableTRElement headTrElement = tableTHeadElement.CreateTR();
headTrElement.AlternativeText = "Head Row";
for (int colIndex = 0; colIndex < 5; colIndex++)
{
    TableTHElement thElement = headTrElement.CreateTH();
    thElement.SetText($"Head {colIndex}");
}

// Fyll i tabellens brödtext
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

Tabellen är indelad i tre delar: huvud, kropp och fot. Vi skapar först rubrikraden med hjälp av `TableTHElement` och lägger till kolumnrubriker. Sedan fyller vi tabellens brödtext med `TableTDElement`, och fyller varje cell med en etikett som anger dess position.

## Steg 7: Spara dokumentet

Slutligen sparar vi PDF-dokumentet i den angivna katalogen.

```csharp
// Spara det taggade PDF-dokumentet
document.Save(dataDir + "StyleTableElement.pdf");
```

Det här steget avslutar dokumentskapandet genom att spara PDF-filen med den formaterade tabellen.

## Steg 8: Validera PDF/UA-efterlevnad

Efter att du har sparat dokumentet är det viktigt att säkerställa att det uppfyller PDF/UA-standarderna (Universal Accessibility).

```csharp
// Kontrollera PDF/UA-efterlevnad
document = new Document(dataDir + "StyleTableElement.pdf");
bool isPdfUaCompliance = document.Validate(dataDir + "StyleTableElement.xml", PdfFormat.PDF_UA_1);
Console.WriteLine($"PDF/UA compliance: {isPdfUaCompliance}");
```

Här laddar vi om dokumentet och validerar det mot PDF/UA-standarder. Efterlevnad säkerställer att din PDF uppfyller tillgänglighetskraven, vilket gör den lämplig för en mängd olika användare.

## Slutsats

Med Aspose.PDF för .NET är det enkelt och intuitivt att skapa och formatera tabeller i dina PDF-dokument. Genom att följa stegen som beskrivs i den här handledningen kan du skapa tabeller med anpassade format och säkerställa att dina PDF-filer uppfyller tillgänglighetsstandarder. Oavsett om du genererar rapporter eller skapar strukturerade dokument är tabeller ett kraftfullt verktyg för att presentera data tydligt.

## Vanliga frågor

### Kan jag lägga till bilder inuti tabellceller?
Ja, du kan infoga bilder i tabellceller med hjälp av `Image` element.

### Hur justerar jag kolumnbredder dynamiskt?
Du kan ställa in `ColumnAdjustment` egendom till `AutoFitToWindow` för att justera kolumnbredder automatiskt baserat på innehåll.

### Är PDF/UA-efterlevnad obligatorisk för alla dokument?
Även om det inte är obligatoriskt rekommenderas det för dokument som kräver höga tillgänglighetsstandarder.

### Kan jag tillämpa olika stilar på specifika rader?
Ja, du kan anpassa enskilda rader eller celler genom att justera deras `TextState` eller `BackgroundColor`.

### Vad är fördelen med att använda taggat innehåll?
Taggat innehåll förbättrar dokumenttillgängligheten och hjälper till att säkerställa efterlevnad av standarder som PDF/UA.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}