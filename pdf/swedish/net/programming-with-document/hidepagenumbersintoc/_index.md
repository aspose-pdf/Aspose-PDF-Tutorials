---
"description": "Lär dig hur du döljer sidnummer i innehållsförteckningen med Aspose.PDF för .NET. Följ den här detaljerade guiden med kodexempel för att skapa professionella PDF-filer."
"linktitle": "Dölj sidnummer i innehållsförteckningen"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Dölj sidnummer i innehållsförteckningen"
"url": "/sv/net/programming-with-document/hidepagenumbersintoc/"
"weight": 220
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Dölj sidnummer i innehållsförteckningen

## Introduktion

När du arbetar med PDF-filer kanske du ibland vill skapa en innehållsförteckning (TOC) men hålla det snyggt genom att dölja sidnumren. Kanske flyter dokumentet bättre utan dem, eller kanske är det ett estetiskt val. Oavsett anledning, om du arbetar med Aspose.PDF för .NET, kommer den här handledningen att visa dig exakt hur du döljer sidnummer i din innehållsförteckning.

## Förkunskapskrav

Innan vi börjar finns det några saker du behöver ha på plats. Här är en snabb checklista:

- Visual Studio installerat: Du behöver en fungerande version av Visual Studio för att kunna koda.
- Aspose.PDF för .NET-bibliotek: Se till att du har installerat Aspose.PDF för .NET-biblioteket.
  - Nedladdningslänk: [Aspose.PDF för .NET](https://releases.aspose.com/pdf/net/)
- Tillfällig licens: Om du testar funktionerna är det bra att ha en tillfällig licens.
  - Tillfällig licens: [Hämta det här](https://purchase.aspose.com/temporary-license/)

## Importera paket

Innan du börjar med koden, se till att du importerar följande namnrymder i ditt C#-projekt. Dessa kommer att tillhandahålla de nödvändiga klasser och metoderna för att arbeta med PDF-dokument och skapa din innehållsförteckning (TOC).

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

Nu när din miljö är redo och paketen har importerats, låt oss bryta ner varje steg i processen. Vi kommer att gå igenom varje del av koden för att säkerställa tydlighet, så att du enkelt kan följa med.

## Steg 1: Initiera ditt PDF-dokument

Det första vi behöver göra är att skapa ett nytt PDF-dokument och lägga till en sida för innehållsförteckningen (TOC).


```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "HiddenPageNumbers_out.pdf";
Document doc = new Document();
Page tocPage = doc.Pages.Add();
```

- dataDir: Det här är katalogen där din utdatafil kommer att sparas.
- Document(): Initierar ett nytt PDF-dokument.
- Pages.Add(): Lägger till en ny tom sida i dokumentet, som senare kommer att innehålla din innehållsförteckning.

## Steg 2: Konfigurera innehållsförteckning och titel

Nästa steg är att definiera innehållsförteckningen, inklusive att ange titeln som ska visas högst upp i innehållsförteckningen.

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocPage.TocInfo = tocInfo;
```

- TocInfo: Det här objektet innehåller all information om innehållsförteckningen.
- Textfragment: Representerar texten i innehållsförteckningen, här anger vi den som "Innehållsförteckning".
- Teckensnitt: Vi formaterar innehållsförteckningens titel genom att ställa in dess storlek till 20 och göra den fetstilad.
- tocPage.TocInfo: Vi tilldelar innehållsförteckningsinformationen till sidan som ska visa innehållsförteckningen.

## Steg 3: Dölj sidnummer i innehållsförteckningen

Nu till det roliga! Här konfigurerar vi innehållsförteckningen för att dölja sidnumren.

```csharp
tocInfo.IsShowPageNumbers = false;
tocInfo.FormatArrayLength = 4;
```

- IsShowPageNumbers: Detta är den magiska knappen som döljer sidnumren. Ställ in den på `false`och sidnumren kommer inte att visas i innehållsförteckningen.
- FormatArrayLength: Vi ställer in detta till 4, vilket indikerar att vi vill definiera formatering för fyra nivåer av innehållsförteckningsrubriker.

## Steg 4: Anpassa innehållsförteckningens formatering

För att ge din innehållsförteckning mer stil ska vi nu definiera formatering för olika rubriknivåer.

```csharp
tocInfo.FormatArray[0].Margin.Right = 0;
tocInfo.FormatArray[0].TextState.FontStyle = FontStyles.Bold | FontStyles.Italic;
tocInfo.FormatArray[1].Margin.Left = 30;
tocInfo.FormatArray[1].TextState.Underline = true;
tocInfo.FormatArray[1].TextState.FontSize = 10;
tocInfo.FormatArray[2].TextState.FontStyle = FontStyles.Bold;
tocInfo.FormatArray[3].TextState.FontStyle = FontStyles.Bold;
```

- FormatArray: Denna array styr formateringen av innehållsförteckningsposter. Varje index representerar en annan rubriknivå.
- Marginal och textstil: Vi ställer in marginaler och använder teckensnitt som fetstil, kursiv stil och understrykning för varje rubriknivå.

## Steg 5: Lägg till rubriker i dokumentet

Slutligen, låt oss lägga till de faktiska rubrikerna som kommer att ingå i innehållsförteckningen.

```csharp
Page page = doc.Pages.Add();
for (int Level = 1; Level != 5; Level++)
{ 
    Heading heading2 = new Heading(Level); 
    TextSegment segment2 = new TextSegment(); 
    heading2.TocPage = tocPage; 
    heading2.Segments.Add(segment2); 
    heading2.IsAutoSequence = true; 
    segment2.Text = "this is heading of level " + Level; 
    heading2.IsInList = true; 
    page.Paragraphs.Add(heading2); 
}
```

- Rubrik och textsegment: Dessa representerar rubrikerna som kommer att visas i din innehållsförteckning. Varje nivå får sin egen rubrik.
- IsAutoSequence: Numrerar rubrikerna automatiskt.
- IsInList: Säkerställer att varje rubrik visas i innehållsförteckningen.

## Steg 6: Spara dokumentet

När allt är inställt sparar du PDF-dokumentet till din angivna utdatafil.

```csharp
doc.Save(outFile);
```

Och det var allt! Du har skapat en PDF med en innehållsförteckning, och sidnumren är dolda!

## Slutsats

Att skapa en innehållsförteckning i en PDF och dölja sidnummer kan verka knepigt, men med Aspose.PDF för .NET är det jätteenkelt. Genom att följa den här steg-för-steg-guiden har du lärt dig hur du anpassar innehållsförteckningsformatet, döljer sidnummer och använder olika stilar på dina rubriker. Nu kan du skapa professionella PDF-filer skräddarsydda efter dina exakta behov.

## Vanliga frågor

### Kan jag visa sidnummer för specifika rubriker i innehållsförteckningen?
Nej, Aspose.PDF döljer eller visar sidnummer för hela innehållsförteckningen. Du kan inte selektivt dölja dem för specifika poster.

### Är det möjligt att lägga till fler nivåer i innehållsförteckningen?
Ja, du kan öka `FormatArrayLength` för att definiera fler nivåer av innehållsförteckningsrubriker.

### Hur kan jag ändra teckensnittet för alla innehållsförteckningsposter?
Du kan ändra teckensnittet genom att modifiera `TextState.Font` egenskap för varje nivå i `FormatArray`.

### Kan jag infoga hyperlänkar i innehållsförteckningen?
Ja, du kan länka varje innehållsförteckning till ett specifikt avsnitt i dokumentet med hjälp av `Heading.TocPage` egendom.

### Behöver jag en licens för Aspose.PDF?
Ja, en giltig licens krävs för produktionsanvändning. Du kan få en tillfällig licens. [här](https://purchase.aspose.com/temporary-license/) för att testa funktionerna.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}