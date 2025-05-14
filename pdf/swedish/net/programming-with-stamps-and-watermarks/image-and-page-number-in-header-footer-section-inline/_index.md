---
"description": "Lär dig hur du lägger till en bild och ett sidnummer infogat i sidhuvudet i en PDF med hjälp av Aspose.PDF för .NET med den här steg-för-steg-guiden."
"linktitle": "Bild och sidnummer i sidhuvuds- och sidfotsavsnittet infogat"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Bild och sidnummer i sidhuvuds- och sidfotsavsnittet infogat"
"url": "/sv/net/programming-with-stamps-and-watermarks/image-and-page-number-in-header-footer-section-inline/"
"weight": 120
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Bild och sidnummer i sidhuvuds- och sidfotsavsnittet infogat

## Introduktion

Aspose.PDF för .NET är ett kraftfullt verktyg som ger omfattande möjligheter för att manipulera och generera PDF-filer. Oavsett om du behöver lägga till bilder, anpassa sidhuvuden och sidfoten eller hantera text, har Aspose.PDF det du behöver. I den här handledningen utforskar vi hur man lägger till en bild och ett sidnummer infogat i sidhuvudet eller sidfoten i ett PDF-dokument. Låt oss dyka in och bryta ner processen steg för steg.

## Förkunskapskrav

Innan vi går in i koden, låt oss se till att du har allt på plats för att följa med:

- Aspose.PDF för .NET: Ladda ner den senaste versionen från [Aspose PDF-nedladdningssida](https://releases.aspose.com/pdf/net/).
- Utvecklingsmiljö: Du behöver en C# IDE, till exempel Visual Studio.
- Körkort: Om du inte redan har körkort kan du skaffa det. [tillfällig licens här](https://purchase.aspose.com/temporary-license/) eller köp en komplett från [Aspose-butik](https://purchase.aspose.com/buy).

Nu när du har förkunskapskraven redo är det dags att börja.

## Importera paket

Innan du börjar koda, se till att importera nödvändiga namnrymder:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Dessa paket låter dig arbeta med PDF-filer och textmanipulera.

## Steg 1: Konfigurera dokumentkatalogen

Det första vi behöver göra är att definiera sökvägen till katalogen där vår PDF-fil ska sparas. Denna sökväg kan anpassas till projektets mapp eller valfri plats på din dator.

```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Denna variabel innehåller platsen där ditt dokument kommer att lagras. Ersätt `"YOUR DOCUMENT DIRECTORY"` med den faktiska vägen.

## Steg 2: Instansiera PDF-dokumentet

I det här steget skapar vi en ny instans av `Aspose.Pdf.Document` objekt. Detta objekt kommer att fungera som ryggraden i din PDF-fil.

```csharp
// Instansiera ett Document-objekt genom att anropa dess tomma konstruktor
Aspose.Pdf.Document pdf1 = new Aspose.Pdf.Document();
```

Här skapar vi en tom PDF-fil som vi senare kan fylla med innehåll.

## Steg 3: Lägg till en sida i PDF-filen

Din PDF behöver minst en sida där du kan lägga till sidhuvuden, sidfot och innehåll. Nu lägger vi till en tom sida i vårt dokument.

```csharp
// Skapa en sida i PDF-objektet
Aspose.Pdf.Page page = pdf1.Pages.Add();
```

Genom att ringa `pdf1.Pages.Add()`, en ny sida läggs till i dokumentet, redo för anpassning av sidhuvud och sidfot.

## Steg 4: Skapa och ange rubriken

Nu är det dags att skapa dokumentets rubrik. Det är här vi lägger till text, bild och sidnummer.

```csharp
// Skapa dokumentets rubriksektion
Aspose.Pdf.HeaderFooter header = new Aspose.Pdf.HeaderFooter();
// Ange sidhuvudet för PDF-filen
page.Header = header;
```

Vi skapar en `HeaderFooter` objektet och tilldela det till `Header` sidans egenskap, vilket säkerställer att allt vi lägger till i sidhuvudet visas högst upp på sidan.

## Steg 5: Lägg till inbäddad text i rubriken

Att lägga till text är lika enkelt som att skapa en `TextFragment` och anger dess egenskaper. Låt oss lägga till lite färgad text i vår rubrik.

```csharp
// Skapa ett textobjekt
Aspose.Pdf.Text.TextFragment txt1 = new Aspose.Pdf.Text.TextFragment("Aspose.Pdf is a Robust component by");
// Ange färgen
txt1.TextState.ForegroundColor = Color.Blue;
txt1.IsInLineParagraph = true;
```

I det här steget skapar vi en `TextFragment` med innehållet "Aspose.Pdf är en Robust-komponent av" och ställ in dess färg på blå. `IsInLineParagraph` Egenskapen säkerställer att texten är inbäddad, vilket innebär att den kommer att visas på samma rad som de andra elementen (som bilden och ytterligare text).

## Steg 6: Infoga en inbäddad bild i sidhuvudet

För att göra din rubrik visuellt tilltalande kan du lägga till en bild inbäddad i texten. Det kan vara din företagslogotyp eller annan grafik.

```csharp
// Skapa ett bildobjekt i sektionen
Aspose.Pdf.Image image1 = new Aspose.Pdf.Image();
// Ange sökvägen till bildfilen
image1.File = dataDir + "aspose-logo.jpg";
// Ställ in bildbreddinformationen
image1.FixWidth = 50;
image1.FixHeight = 20;
// Anger att seg1:s InlineParagraph är en bild.
image1.IsInLineParagraph = true;
```

Här lägger vi till en bild i rubriken genom att skapa en `Image` objektet, ställa in dess bana och justera bredd och höjd. `IsInLineParagraph` säkerställer att bilden är i linje med texten.

## Steg 7: Lägg till ytterligare inbäddad text för att slutföra rubriken

Låt oss lägga till lite mer text för att komplettera den inbyggda rubriken.

```csharp
Aspose.Pdf.Text.TextFragment txt2 = new Aspose.Pdf.Text.TextFragment(" Pty Ltd.");
txt2.IsInLineParagraph = true;
txt2.TextState.ForegroundColor = Color.Maroon;
header.Paragraphs.Add(txt1);
header.Paragraphs.Add(image1);
header.Paragraphs.Add(txt2);
```

I den här delen skapar vi ytterligare en `TextFragment` med innehållet "Pty Ltd." och sätt dess färg till rödbrun. Både textfragment och bilden läggs till i rubriken.

## Steg 8: Spara PDF-filen

När du har konfigurerat rubriken är det dags att spara PDF-filen.

```csharp
// Spara PDF-filen
pdf1.Save(dataDir + "ImageAndPageNumberInHeaderFooter_UsingInlineParagraph_out.pdf");
```

De `Save` Metoden skriver den slutliga PDF-filen till den angivna platsen.

## Slutsats

Grattis! Du har lagt till en bild och text i sidhuvudet på ett PDF-dokument med Aspose.PDF för .NET. Den här handledningen guidade dig genom de viktigaste stegen, inklusive att skapa ett dokument, lägga till sidor, infoga sidhuvuden och placera inbäddat innehåll som text och bilder. Aspose.PDF ger dig otrolig flexibilitet att hantera dina PDF-filer, oavsett om det handlar om att manipulera sidhuvuden, sidfot eller komplext innehåll. 

## Vanliga frågor

### Kan jag lägga till ett sidnummer i rubriken också?
Ja! Du kan enkelt lägga till ett sidnummer genom att använda `TextFragment` klassen och formatera den efter behov. Infoga den bara i rubriksektionen som inbäddat innehåll.

### Hur ställer jag in en bakgrundsbild i headern?
Du kan använda `BackgroundImage` egendomen tillhörande `HeaderFooter` klassen för att ange en bakgrundsbild. Detta är dock inte inbäddat innehåll, och det kommer att täcka hela rubrikområdet.

### Är det möjligt att använda andra bildformat än JPEG?
Absolut! Aspose.PDF stöder olika bildformat som PNG, BMP och GIF.

### Kan jag anpassa teckensnittet på texten i sidhuvudet?
Ja, du kan använda `TextState` objekt för att ändra textens teckensnitt, storlek och stil.

### Behöver jag en licens för att använda Aspose.PDF för .NET?
Ja, Aspose.PDF kräver en licens för produktionsanvändning, men du kan börja med en [gratis provperiod här](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}