---
"description": "Lär dig hur du anpassar sidnummer när du lägger till en innehållsförteckning i dina PDF-dokument med Aspose.PDF för .NET i den här omfattande handledningen."
"linktitle": "Anpassa sidnummer när du lägger till innehållsförteckning"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Anpassa sidnummer när du lägger till innehållsförteckning"
"url": "/sv/net/programming-with-document/customizepagenumbeswhileaddingtoc/"
"weight": 100
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Anpassa sidnummer när du lägger till innehållsförteckning

## Introduktion

dokumenthanteringens värld regerar PDF-filer suveränt. De är det självklara formatet för att dela och bevara dokument på olika plattformar. Men vad händer när du vill förbättra dina PDF-dokument med funktioner som en innehållsförteckning (TOC)? Det är där Aspose.PDF för .NET kommer in i bilden! Detta kraftfulla bibliotek låter utvecklare enkelt manipulera PDF-filer, vilket gör att de kan lägga till, ändra och anpassa innehåll utan ansträngning. I den här handledningen kommer vi att dyka in i hur du anpassar sidnummer samtidigt som du lägger till en innehållsförteckning i dina PDF-dokument med Aspose.PDF för .NET. Så ta din kodningshatt och låt oss sätta igång!

## Förkunskapskrav

Innan vi går in i koden finns det några saker du behöver ha på plats:

1. Visual Studio: Se till att du har Visual Studio installerat på din dator. Detta kommer att vara vår utvecklingsmiljö.
2. Aspose.PDF för .NET: Du behöver ladda ner och installera Aspose.PDF-biblioteket. Du hittar det [här](https://releases.aspose.com/pdf/net/).
3. Grundläggande kunskaper i C#: Bekantskap med C#-programmering hjälper dig att förstå kodavsnitten bättre.
4. En exempel-PDF-fil: Ha en exempel-PDF-fil redo som vi kan arbeta med. Du kan skapa en enkel eller ladda ner en befintlig PDF.

## Importera paket

För att komma igång behöver vi importera de nödvändiga paketen. Öppna ditt Visual Studio-projekt och lägg till en referens till Aspose.PDF-biblioteket. Du kan göra detta med hjälp av NuGet Package Manager:

1. Högerklicka på ditt projekt i lösningsutforskaren.
2. Välj "Hantera NuGet-paket".
3. Sök efter "Aspose.PDF" och installera det.

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

När du har installerat biblioteket kan du börja koda!

## Steg 1: Konfigurera din dokumentkatalog

Först och främst måste vi konfigurera vår dokumentkatalog. Det är här vi lagrar våra PDF-filer för in- och utdata. 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string inFile = dataDir + "42824.pdf";
string outFile = dataDir + "42824_out.pdf";
```

I det här utdraget, ersätt `YOUR DOCUMENT DIRECTORY` med den faktiska sökvägen dit dina PDF-filer finns. Detta hjälper oss att ladda den befintliga PDF-filen och spara den ändrade versionen.

## Steg 2: Ladda den befintliga PDF-filen

Nu när vi har konfigurerat vår dokumentkatalog, låt oss ladda den befintliga PDF-filen. 

```csharp
Document doc = new Document(inFile);
```

Här skapar vi ett nytt `Document` objektet genom att skicka inmatningsfilens sökväg. Detta gör att vi kan manipulera PDF-innehållet programmatiskt.

## Steg 3: Infoga en ny sida för innehållsförteckningen

Nästa steg är att skapa en ny sida i PDF-filen där innehållsförteckningen ska finnas.

```csharp
Aspose.Pdf.Page tocPage = doc.Pages.Insert(1);
```

Den här raden infogar en ny sida i början av dokumentet. Innehållsförteckningen visas på den här sidan.

## Steg 4: Skapa innehållsförteckning

Nu ska vi skapa ett objekt som representerar innehållsförteckningen.

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocInfo.PageNumbersPrefix = "P";
tocPage.TocInfo = tocInfo;
```

I det här steget skapar vi en `TocInfo` objektet och ställ in dess titel på "Innehållsförteckning". Vi anpassar även teckenstorlek och stil. `PageNumbersPrefix` är satt till "P", vilket kommer att prefixa sidnumren i innehållsförteckningen.

## Steg 5: Lägg till rubriker i innehållsförteckningen

Nu kommer det roliga! Vi ska gå igenom dokumentets sidor och lägga till rubriker i vår innehållsförteckning.

```csharp
for (int i = 1; i < doc.Pages.Count; i++)
{
    Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
    TextSegment segment2 = new TextSegment();
    heading2.TocPage = tocPage;
    heading2.Segments.Add(segment2);
    heading2.DestinationPage = doc.Pages[i + 1];
    heading2.Top = doc.Pages[i + 1].Rect.Height;
    segment2.Text = "Page " + i.ToString();
    tocPage.Paragraphs.Add(heading2);
}
```

I den här loopen skapar vi en ny `Heading` objekt för varje sida. Vi ställer in målsidan för varje rubrik och anger texten som ska visas, vilket är "Sida X" där X är sidnumret. Slutligen lägger vi till rubriken på innehållsförteckningssidan.

## Steg 6: Spara det uppdaterade dokumentet

Efter att ha lagt till alla nödvändiga rubriker är det dags att spara vårt uppdaterade dokument.

```csharp
doc.Save(outFile);
```

Den här raden sparar den modifierade PDF-filen med innehållsförteckningen inkluderad. Du kan nu öppna utdatafilen och se din anpassade innehållsförteckning!

## Slutsats

Och där har du det! Du har framgångsrikt anpassat sidnummer samtidigt som du lagt till en innehållsförteckning i ditt PDF-dokument med hjälp av Aspose.PDF för .NET. Detta kraftfulla bibliotek gör det enkelt att manipulera PDF-filer, och med bara några få rader kod kan du förbättra dina dokument avsevärt. Oavsett om du skapar rapporter, e-böcker eller någon annan typ av PDF kan en innehållsförteckning avsevärt förbättra navigeringen för dina läsare. Så vad väntar du på? Dyk ner i Aspose.PDF och börja skapa fantastiska PDF-filer idag!

## Vanliga frågor

### Vad är Aspose.PDF för .NET?
Aspose.PDF för .NET är ett bibliotek som låter utvecklare skapa, manipulera och konvertera PDF-dokument programmatiskt.

### Kan jag använda Aspose.PDF gratis?
Ja, Aspose erbjuder en gratis testversion som du kan använda för att utforska bibliotekets funktioner. Du kan ladda ner den. [här](https://releases.aspose.com/).

### Hur får jag support för Aspose.PDF?
Du kan få support genom att besöka Aspose-forumet [här](https://forum.aspose.com/c/pdf/10).

### Finns det en tillfällig licens tillgänglig?
Ja, du kan begära en tillfällig licens för Aspose.PDF [här](https://purchase.aspose.com/temporary-license/).

### Var kan jag köpa Aspose.PDF för .NET?
Du kan köpa Aspose.PDF för .NET [här](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}