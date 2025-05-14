---
"description": "Lär dig hur du anger en sida som ska visas i en PDF med Aspose.PDF för .NET. Förbättra användarnavigeringen med den här enkla guiden."
"linktitle": "Ange sida vid visning"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Ange sida vid visning"
"url": "/sv/net/programming-with-links-and-actions/specify-page-when-viewing/"
"weight": 110
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ange sida vid visning

## Introduktion

Vill du förbättra dina PDF-applikationer genom att dirigera användare till specifika sidor när de öppnar ett dokument? Då har du kommit till rätt ställe! I den här guiden går vi in på detaljerna kring att använda Aspose.PDF för .NET för att ange vilken sida som ska visas när en PDF öppnas. Den här funktionen kan avsevärt förbättra användarupplevelsen, särskilt när du behöver uppmärksamma viktiga delar av ditt dokument.

## Förkunskapskrav

Innan vi börjar programmera, se till att du har allt du behöver för att komma igång. Här är vad du behöver:

1. Grundläggande kunskaper om .NET: Bekantskap med .NET-ramverket är viktigt. Om du är bekväm med C# och har en grundläggande förståelse för objektorienterad programmering är du redo!

2. Aspose.PDF för .NET: Du måste ha Aspose.PDF-biblioteket installerat i ditt projekt. Om du inte har installerat det än kan du ladda ner det. [här](https://releases.aspose.com/pdf/net/).

3. Visual Studio: Den här handledningen förutsätter att du använder Visual Studio som din IDE. Se till att du har det installerat på din dator.

4. En PDF-fil: Du behöver en befintlig PDF-fil som du kommer att arbeta med. Om du inte har någon kan du skapa ett exempeldokument eller använda valfri PDF-fil.

När ni har dessa förutsättningar på plats kan vi kavla upp ärmarna och börja koda!

## Importera paket

Nu när vi är klara, låt oss importera de nödvändiga paketen till vårt projekt. Följ dessa steg:

### Starta Visual Studio

Öppna Visual Studio och skapa antingen ett nytt projekt eller ladda ett befintligt där du vill implementera funktionen för visning av PDF-sidorna.

### Referens Aspose.PDF

För att använda Aspose.PDF-biblioteket måste du lägga till en referens till det:

1. Högerklicka på ditt projekt i lösningsutforskaren.
2. Välj "Hantera NuGet-paket".
3. Leta efter `Aspose.PDF` och installera paketet.

### Importera namnrymder

Lägg till följande using-direktiv högst upp i din kodfil:

```csharp
using System;
using System.IO;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
```

Nu är du redo att börja bygga din PDF-sidas navigeringslogik!

Låt oss dela upp vår uppgift i hanterbara steg. Vi skriver kod som öppnar ett PDF-dokument, anger en specifik sida som ska visas vid visning och sparar det uppdaterade dokumentet. 

## Steg 1: Ställ in dokumentkatalogen

Först måste du ange sökvägen till dina dokument:

```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Ersätt med din katalog
```

Den här raden är i huvudsak din färdplan. Du anger för din kod var PDF-filen finns. Se till att ersätta den. `YOUR DOCUMENT DIRECTORY` med den faktiska sökvägen på din maskin.

## Steg 2: Ladda PDF-filen

Sedan laddar du PDF-filen i ditt program:

```csharp
// Ladda PDF-filen
Document doc = new Document(dataDir + "SpecifyPageWhenViewing.pdf");
```

Det som händer här är att du skapar en ny instans av en `Document` objektet medan du anger sökvägen till din PDF-fil. Du kan tänka på det som att öppna boken du just har lagt på bordet.

## Steg 3: Gå till önskad sida

Nu ska vi öppna sidan som du vill visa när dokumentet öppnas:

```csharp
// Hämta instansen av dokumentets andra sida
Page page2 = doc.Pages[2]; // Kom ihåg att indexering börjar vid 1
```

Här öppnar vi den andra sidan i ditt dokument. Det är värt att notera att sidnumreringen börjar på 1 i detta sammanhang, så om du tänker på sida 2 måste du använda ett index på 2.

## Steg 4: Ställ in zoomfaktorn

Du kan justera zoomnivån för sidan som visas:

```csharp
// Skapa variabeln för att ställa in zoomfaktorn för målsidan
double zoom = 1; // 1 betyder 100 % zoom
```

Att ställa in en zoomfaktor hjälper till att avgöra hur mycket av sidan användaren ser direkt efter öppning. Värdet 1 innebär att sidan visas med 100 % zoom, vilket generellt är en bra standard.

## Steg 5: Skapa GoToAction-instansen

Låt oss sätta navigeringsfunktionerna igång:

```csharp
// Skapa GoToAction-instans
GoToAction action = new GoToAction(doc.Pages[2]); 
```

I det här steget skapar du en instans av `GoToAction` som i huvudsak representerar handlingen att navigera till en specifik punkt i PDF-filen – i det här fallet den andra sidan.

## Steg 6: Definiera destinationen

Nu behöver du definiera vart åtgärden ska leda:

```csharp
// Gå till sida 2
action.Destination = new XYZExplicitDestination(page2, 0, page2.Rect.Height, zoom);
```

Den här raden är som att ange en GPS-destination för GåTillAktionen. Du anger att den ska gå till sida 2 högst upp på sidan (höjd) och med den angivna zoomnivån.

## Steg 7: Ställ in öppningsåtgärden

Låt oss se till att den här åtgärden utförs när dokumentet öppnas:

```csharp
// Ställ in dokumentöppningsåtgärden
doc.OpenAction = action;
```

Med detta har du deklarerat att när din PDF öppnas aktiveras den navigeringsåtgärd vi just definierade. Det är som om du har placerat välkomstmattan vid dokumentets ytterdörr.

## Steg 8: Spara det uppdaterade dokumentet

Slutligen, låt oss spara dokumentet med de gjorda ändringarna:

```csharp
// Spara uppdaterat dokument
doc.Save(dataDir + "goto2page_out.pdf");
```

Det här steget slutför ditt arbete! Du kommer att ha en ny PDF-fil med namnet `goto2page_out.pdf` som öppnas direkt till den sida du angav.

Med det är kodningsdelen klar! Du har framgångsrikt programmerat Aspose.PDF för att visa en specifik sida när en PDF öppnas. 

## Slutsats

I den här guiden har vi steg för steg gått igenom hur man anger en sida i en PDF-fil med Aspose.PDF för .NET. Den här funktionen förbättrar inte bara navigeringen för dina användare utan effektiviserar även deras interaktion med viktigt innehåll i dina dokument. Genom att använda sådana funktioner skapar du en mer användarvänlig upplevelse som kan särskilja dina PDF-applikationer.

## Vanliga frågor

### Vad är Aspose.PDF för .NET?
Aspose.PDF för .NET är ett bibliotek som gör det möjligt för utvecklare att skapa, modifiera och hantera PDF-dokument i .NET-applikationer.

### Kan jag ange flera sidor som ska visas?
Nej, du kan bara ställa in dokumentet så att det öppnas på en viss sida. Du kan däremot skapa olika dokument för olika startsidor.

### Vad händer om jag vill visa en sida med en annan zoomnivå?
Du kan ändra zoomnivån genom att justera `zoom` variabeln innan dokumentet sparas.

### Var kan jag hitta fler exempel på hur man använder Aspose.PDF?
Du kan kontrollera [dokumentation](https://reference.aspose.com/pdf/net/) för fler exempel och funktioner.

### Finns det en gratis testversion av Aspose.PDF för .NET?
Ja! Du kan ladda ner en gratis testversion av Aspose.PDF [här](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}