---
"description": "Lär dig hur du skapar en fylld rektangel i en PDF med Aspose.PDF för .NET med den här steg-för-steg-handledningen. Perfekt för utvecklare på alla nivåer."
"linktitle": "Skapa fylld rektangel"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Skapa fylld rektangel"
"url": "/sv/net/programming-with-graphs/create-filled-rectangle/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Skapa fylld rektangel

## Introduktion

Har du någonsin velat skapa visuellt tilltalande PDF-filer programmatiskt? I så fall har du kommit rätt! I den här handledningen dyker vi ner i Aspose.PDF för .NET, ett kraftfullt bibliotek som låter dig enkelt manipulera PDF-dokument. Idag fokuserar vi på att skapa en fylld rektangel i en PDF-fil. Oavsett om du är en erfaren utvecklare eller precis har börjat, kommer den här guiden att guida dig genom varje steg på ett vänligt och engagerande sätt. Så ta din kodningshatt och låt oss sätta igång!

## Förkunskapskrav

Innan vi går in i koden finns det några saker du behöver ha på plats:

1. Visual Studio: Se till att du har Visual Studio installerat på din dator. Det är ett fantastiskt IDE för .NET-utveckling.
2. Aspose.PDF för .NET: Du måste ladda ner och installera Aspose.PDF-biblioteket. Du hittar det [här](https://releases.aspose.com/pdf/net/).
3. Grundläggande kunskaper i C#: Lite förtrogenhet med C#-programmering hjälper dig att förstå kodavsnitten bättre.

## Importera paket

För att komma igång behöver du importera de nödvändiga paketen i ditt C#-projekt. Så här gör du:

### Skapa ett nytt projekt

Öppna Visual Studio och skapa ett nytt C#-projekt. Du kan välja en konsolapplikation för enkelhetens skull.

### Lägg till Aspose.PDF-referens

1. Högerklicka på ditt projekt i lösningsutforskaren.
2. Välj "Hantera NuGet-paket".
3. Sök efter "Aspose.PDF" och installera den senaste versionen.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Nu när vi har allt klart, låt oss dyka in i koden!

## Steg 1: Konfigurera din dokumentkatalog

Först och främst måste du ange sökvägen där din PDF ska sparas. Detta är avgörande eftersom det talar om för programmet var filen ska skapas.

```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Ersätta `"YOUR DOCUMENT DIRECTORY"` med den faktiska sökvägen på din dator där du vill spara PDF-filen.

## Steg 2: Skapa en dokumentinstans

Nästa steg är att skapa en instans av `Document` klass. Den här klassen representerar PDF-dokumentet du kommer att arbeta med.

```csharp
// Skapa dokumentinstans
Document doc = new Document();
```

Den här raden initierar ett nytt PDF-dokument som vi kan manipulera.

## Steg 3: Lägg till en sida i dokumentet

Nu ska vi lägga till en sida i vårt dokument. Varje PDF behöver minst en sida, eller hur?

```csharp
// Lägg till sida till sidsamling i PDF-filen
Page page = doc.Pages.Add();
```

Den här koden lägger till en ny sida i dokumentet, vilket gör att vi kan rita former på den.

## Steg 4: Skapa en grafinstans

För att rita former behöver vi skapa en `Graph` exempel. Tänk på ett diagram som en duk där du kan rita olika former.

```csharp
// Skapa Graph-instans
Aspose.Pdf.Drawing.Graph graph = new Aspose.Pdf.Drawing.Graph(100.0, 400.0);
```

Här skapar vi en graf med en bredd på 100 och en höjd på 400.

## Steg 5: Lägg till grafen på sidan

Nu när vi har vår graf, låt oss lägga till den på sidan vi skapade tidigare.

```csharp
// Lägg till grafobjekt till styckesamlingen för sidans instans
page.Paragraphs.Add(graph);
```

Denna linje fäster grafen vid sidan, vilket gör den redo för ritning.

## Steg 6: Skapa en rektangelinstans

Sedan skapar vi en rektangel som vi vill fylla med färg.

```csharp
// Skapa Rectangle-instans
Aspose.Pdf.Drawing.Rectangle rect = new Aspose.Pdf.Drawing.Rectangle(100, 100, 200, 120);
```

I den här koden definierar vi rektangelns position och storlek. Parametrarna representerar x- och y-koordinaterna, bredden och höjden.

## Steg 7: Ange fyllningsfärgen

Nu ska vi välja en färg för vår rektangel. Vi fyller den med rött i det här exemplet.

```csharp
// Ange fyllningsfärg för Graph-objekt
rect.GraphInfo.FillColor = Aspose.Pdf.Color.Red;
```

Den här linjen ställer in rektangelns fyllningsfärg till röd. Du kan välja vilken färg du vill!

## Steg 8: Lägg till rektangeln i grafen

Med vår rektangel klar är det dags att lägga till den i grafen.

```csharp
// Lägg till rektangelobjekt till grafobjektets formsamling
graph.Shapes.Add(rect);
```

Den här koden lägger till rektangeln i grafen, vilket gör den till en del av vår ritning.

## Steg 9: Spara PDF-dokumentet

Slutligen måste vi spara vårt dokument i den angivna katalogen.

```csharp
dataDir = dataDir + "CreateFilledRectangle_out.pdf";
// Spara PDF-fil
doc.Save(dataDir);
```

Den här koden sparar PDF-filen med namnet `CreateFilledRectangle_out.pdf` i katalogen du angav tidigare.

## Steg 10: Bekräftelsemeddelande

För att informera oss om att allt gick smidigt kan vi skriva ut ett bekräftelsemeddelande.

```csharp
Console.WriteLine("\nFilled rectangle object created successfully.\nFile saved at " + dataDir);
```

Den här raden visar ett meddelande i konsolen som bekräftar att den fyllda rektangeln har skapats.

## Slutsats

Och där har du det! Du har lyckats skapa en fylld rektangel i ett PDF-dokument med Aspose.PDF för .NET. Detta kraftfulla bibliotek öppnar upp en värld av möjligheter för PDF-manipulation, vilket gör att du kan skapa fantastiska dokument programmatiskt. Oavsett om du genererar rapporter, fakturor eller någon annan typ av PDF, har Aspose.PDF det du behöver.

## Vanliga frågor

### Vad är Aspose.PDF för .NET?
Aspose.PDF för .NET är ett bibliotek som låter utvecklare skapa, manipulera och konvertera PDF-dokument programmatiskt.

### Kan jag använda Aspose.PDF gratis?
Ja, Aspose erbjuder en gratis testversion som du kan använda för att utforska bibliotekets funktioner. Du kan ladda ner den. [här](https://releases.aspose.com/).

### Finns det något sätt att få support för Aspose.PDF?
Absolut! Du kan få support via Aspose-forumet. [här](https://forum.aspose.com/c/pdf/10).

### Hur kan jag köpa Aspose.PDF?
Du kan köpa Aspose.PDF genom att besöka köpsidan [här](https://purchase.aspose.com/buy).

### Vilka typer av former kan jag skapa med Aspose.PDF?
Du kan skapa olika former, inklusive rektanglar, cirklar, linjer och mer, med hjälp av Aspose.PDF-biblioteket.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}