---
"description": "Lär dig hur du ställer in ett standardteckensnittsnamn när du renderar PDF-filer till bilder med Aspose.PDF för .NET. Den här guiden beskriver förutsättningar, steg-för-steg-instruktioner och vanliga frågor."
"linktitle": "Ange standardnamn för teckensnitt"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Ange standardnamn för teckensnitt"
"url": "/sv/net/document-conversion/set-default-font-name/"
"weight": 270
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ange standardnamn för teckensnitt

## Introduktion

Har du någonsin försökt rendera ett PDF-dokument till en bild men märkt att teckensnitten helt enkelt inte ser rätt ut? Kanske ser texten förvrängd ut, eller så kanske det ursprungliga teckensnittet inte stöds. Det är här som att ställa in ett standardteckensnitt kan rädda dagen! Med Aspose.PDF för .NET kan du enkelt ställa in ett standardteckensnitt för din PDF-rendering, vilket säkerställer att ditt dokument ser skarpt och professionellt ut. I den här handledningen kommer vi att guida dig genom hur du ställer in standardteckensnittsnamnet när du renderar en PDF till en bild. I slutet av den här guiden kommer du att ha kunskaperna för att ta itu med alla PDF-renderingsutmaningar som kommer i din väg. Redo? Nu dyker vi in!

## Förkunskapskrav

Innan vi går in i koden finns det några saker du behöver ha på plats:

- Aspose.PDF för .NET: Det här kraftfulla biblioteket är vad vi kommer att använda för att manipulera vårt PDF-dokument. Du kan ladda ner det från [Aspose webbplats](https://releases.aspose.com/pdf/net/).
- Visual Studio: Se till att du har Visual Studio installerat på din dator. Detta kommer att vara vår utvecklingsmiljö.
- .NET Framework: Se till att du har .NET Framework installerat. Aspose.PDF för .NET stöder olika versioner, så kontrollera dokumentationen för att se om den uppfyller dina behov.
- Ett PDF-dokument: Du behöver ett exempel på ett PDF-dokument att arbeta med. Om du inte har ett kan du skapa en enkel PDF eller ladda ner ett exempel online.

När du har ställt in allt är vi redo att börja koda!

## Importera paket

Innan vi går in i koden är det viktigt att importera de nödvändiga paketen. Detta säkerställer att vi har tillgång till alla klasser och metoder vi behöver för vårt projekt.

```csharp
using Aspose.Pdf.Devices;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
```

Dessa importer är viktiga eftersom de tar med de namnrymder som krävs för att hantera PDF-manipulation, bildrendering och filströmningsoperationer.

## Steg 1: Konfigurera ditt projekt och din dokumentsökväg

Först och främst, låt oss ställa in sökvägen till katalogen där ditt PDF-dokument finns. Detta blir din utgångspunkt för att manipulera PDF-filen.

```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```
Här, `dataDir` är katalogen där ditt PDF-dokument finns. Se till att ersätta `"YOUR DOCUMENT DIRECTORY"` med den faktiska sökvägen till ditt dokument. Detta är viktigt eftersom koden behöver veta var PDF-filen ska hämtas ifrån.

## Steg 2: Ladda PDF-dokumentet

Nu när vi har dokumentsökvägen är nästa steg att ladda PDF-dokumentet i minnet så att vi kan börja arbeta med det.

```csharp
using (Document pdfDocument = new Document(dataDir + "input.pdf"))
```
Vi använder `Document` klassen från Aspose.PDF-biblioteket för att ladda vår PDF-fil. Den här klassen tillhandahåller olika metoder och egenskaper för att arbeta med PDF-dokumentet. `"input.pdf"` bör ersättas med det faktiska filnamnet på din PDF. Den här filen kommer att användas som indata för rendering.

## Steg 3: Skapa en bildström för utdata

När dokumentet har laddats behöver vi konfigurera en ström för att spara den renderade bilden. Det är här utdatabilden kommer att lagras.

```csharp
using (FileStream imageStream = new FileStream(dataDir + "SetDefaultFontName.png", FileMode.Create))
```
De `FileStream` klassen används för att skapa en ny fil där den renderade bilden ska sparas. I det här exemplet sparar vi bilden som `"SetDefaultFontName.png"`Den `FileMode.Create` säkerställer att en ny fil skapas, eller att en befintlig fil skrivs över.

## Steg 4: Ställ in upplösningen för bilden

Innan PDF-filen renderas till en bild är det viktigt att ställa in upplösningen. Detta avgör kvaliteten och skärpan på den utgående bilden.

```csharp
Resolution resolution = new Resolution(300);
```
De `Resolution` Klassen anger upplösningen för utdatabilden. Här har vi valt en upplösning på 300 DPI (punkter per tum), vilket är standard för högkvalitativa bilder. Detta säkerställer att text och grafik i din PDF återges tydligt utan att detaljer förloras.

## Steg 5: Konfigurera PNG-enheten

Sedan måste vi konfigurera enheten som hanterar renderingen av PDF-filen till en PNG-bild.

```csharp
PngDevice pngDevice = new PngDevice(resolution);
```
De `PngDevice` klassen ansvarar för att rendera PDF-dokumentet till en PNG-bild. Genom att skicka `resolution` invända mot det, ser vi till att bilden skapas med den angivna DPI:n.

## Steg 6: Ange standardtypsnittsnamn

Här är den viktiga delen – att ställa in standardtypsnittet. Detta blir reservtypsnittet om det ursprungliga typsnittet i PDF-filen inte är tillgängligt.

```csharp
RenderingOptions ro = new RenderingOptions();
ro.DefaultFontName = "Arial";
pngDevice.RenderingOptions = ro;
```
Vi skapar en instans av `RenderingOptions` och ställ in dess `DefaultFontName` egendom till `"Arial"`Det betyder att om det ursprungliga teckensnittet i PDF-filen inte kan hittas, kommer Arial att användas istället. Detta steg är avgörande för att bibehålla läsbarheten och utseendet på texten i den renderade bilden.

## Steg 7: Rendera PDF-sidan till en bild

Slutligen, med allt konfigurerat, kan vi nu rendera den första sidan av PDF-dokumentet till en bild och spara den med hjälp av filströmmen vi skapade tidigare.

```csharp
pngDevice.Process(pdfDocument.Pages[1], imageStream);
```
De `Process` metod för `PngDevice` klassen används för att rendera den angivna PDF-sidan (i det här fallet den första sidan) till en bild. Utdata sparas sedan till `imageStream`Det här steget konverterar PDF-sidan till en PNG-bild med den angivna upplösningen och standardteckensnittet.

## Steg 8: Stäng filströmmen och PDF-dokumentet

Efter att bilden har renderats är det viktigt att stänga filströmmen och PDF-dokumentet för att frigöra resurser.

```csharp
imageStream.Close();
pdfDocument.Dispose();
```
Stänger `imageStream` säkerställer att filen sparas korrekt och att ingen data går förlorad. Kassera `pdfDocument` frigör minne och resurser, vilket förhindrar potentiella minnesläckor.

## Slutsats

Och där har du det! Med bara några få rader kod har du lärt dig hur du ställer in ett standardteckensnitt när du renderar en PDF till en bild med Aspose.PDF för .NET. Denna färdighet är otroligt praktisk, särskilt när du hanterar PDF-filer som kan innehålla teckensnitt som inte stöds. Genom att ställa in ett standardteckensnitt säkerställer du att dina renderade bilder bibehåller sin läsbarhet och professionella utseende.

## Vanliga frågor

### Vad händer om det angivna standardteckensnittet inte är installerat på systemet?
Om standardteckensnittet som anges i `RenderingOptions` inte är installerat på systemet kommer Aspose.PDF att använda ett systemdefinierat reservteckensnitt.

### Kan jag använda andra teckensnitt än Arial som standardteckensnitt?
Absolut! Du kan ställa in vilket teckensnitt som helst som är installerat på ditt system som standardteckensnitt.

### Är det möjligt att rendera flera sidor av en PDF till bilder samtidigt?
Ja, du kan loopa igenom sidorna i din PDF och rendera varje sida individuellt med samma process.

### Påverkar inställningen av hög upplösning prestandan för PDF-rendering?
Ja, högre upplösningar kommer att resultera i större bildfiler och kan öka renderingstiden, men de kommer också att producera tydligare bilder.

### Kan jag rendera PDF-filen till andra bildformat än PNG?
Ja, Aspose.PDF stöder rendering till olika bildformat som JPEG, BMP och TIFF.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}