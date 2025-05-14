---
"description": "Steg-för-steg-guide för att ändra sidorientering i en PDF med Aspose.PDF för .NET. Lätt att följa och implementera i dina projekt."
"linktitle": "Ändra orientering"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Ändra orientering"
"url": "/sv/net/programming-with-pdf-pages/change-orientation/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ändra orientering

## Introduktion

Har du någonsin haft problem med en PDF-fil där sidorienteringen är helt... fel? Kanske har du ett dokument som har skannats eller skapats felaktigt, och sidorna behöver roteras för att bli begripliga. Som tur är för oss erbjuder Aspose.PDF för .NET ett enkelt och kraftfullt sätt att manipulera PDF-filer på nästan alla tänkbara sätt – inklusive att ändra sidorienteringen. Oavsett om du vill växla från stående till liggande eller vice versa, kommer den här guiden att guida dig genom processen steg för steg.

Så om du är redo att dyka in och rotera PDF-sidorna med lätthet, låt oss sätta igång!

## Förkunskapskrav

Innan vi går in på detaljerna kring att ändra sidorientering i din PDF, låt oss snabbt gå igenom vad du behöver ha på plats:

- Aspose.PDF för .NET: Se till att du har installerat Aspose.PDF-biblioteket för .NET. Om du inte har det kan du [ladda ner den här](https://releases.aspose.com/pdf/net/).
- En .NET-utvecklingsmiljö: Du kan använda Visual Studio, JetBrains Rider eller valfri IDE för att arbeta med .NET.
- Grundläggande kunskaper i C#: Även om den här guiden är enkel, kommer lite grundläggande förståelse för C# att göra den ännu enklare att följa.
- En PDF-fil: Exemplet nedan förutsätter att du har en PDF-fil med flera sidor. Om du inte har en till hands kan du skapa eller ladda ner en exempel-PDF att arbeta med.

Om du precis har börjat kan du också prova Aspose.PDF med en [gratis tillfällig licens](https://purchase.aspose.com/temporary-license/) innan man bestämmer sig för att [köp den fullständiga versionen](https://purchase.aspose.com/buy).

## Importera namnrymder

Innan du kan manipulera sidorienteringen i din PDF måste du importera nödvändiga namnrymder i ditt C#-projekt. Se till att du har följande:

```csharp
using System.IO;
using Aspose.Pdf;
```

Med detta importerat, låt oss hoppa över till huvuddelen av handledningen.

## Steg 1: Ladda PDF-dokumentet

Det första vi behöver göra är att ladda PDF-filen du vill ändra. Du kan använda `Document` klassen från namnrymden Aspose.PDF för att öppna din PDF.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document(dataDir + "input.pdf");
```

Den här raden laddar PDF-filen från din angivna katalog. Se till att ersätta den. `"YOUR DOCUMENT DIRECTORY"` med den faktiska sökvägen till din fil. Den `"input.pdf"` är den PDF-fil du vill ändra orienteringen på.

## Steg 2: Loopa igenom varje sida

Nu när vi har laddat dokumentet, låt oss loopa igenom varje sida i PDF-filen. Vi använder en `foreach` loop för att gå igenom varje sida, vilket gör att vi kan tillämpa orienteringsändringen på dem alla.

```csharp
foreach (Page page in doc.Pages)
{
    // Manipulera varje sida
}
```

Denna loop itererar genom alla sidor i dokumentet.

## Steg 3: Hämta sidans MediaBox

Varje sida i en PDF har en `MediaBox` som definierar sidans gränser. Vi behöver komma åt detta för att bestämma den aktuella orienteringen och ändra den.

```csharp
Aspose.Pdf.Rectangle r = page.MediaBox;
```

De `MediaBox` ger oss sidans dimensioner, såsom dess bredd, höjd och positionering.

## Steg 4: Byt bredd och höjd

För att ändra sidorienteringen från stående till liggande eller liggande till stående, byter vi helt enkelt bredd- och höjdvärdena. I det här steget justeras sidans dimensioner.

```csharp
double newHeight = r.Width;
double newWidth = r.Height;
double newLLX = r.LLX;
double newLLY = r.LLY + (r.Height - newHeight);
```

Den här koden byter höjd och bredd och flyttar det nedre vänstra hörnet (`LLY`) så att innehållet får plats snyggt efter rotationen.

## Steg 5: Uppdatera MediaBox och CropBox

Nu när vi har den nya höjden och bredden, låt oss tillämpa ändringarna på sidans `MediaBox` och `CropBox`Den `CropBox` är viktigt om originaldokumentet hade en uppsättning, att säkerställa att hela sidan visas korrekt.

```csharp
page.MediaBox = new Aspose.Pdf.Rectangle(newLLX, newLLY, newLLX + newWidth, newLLY + newHeight);
page.CropBox = new Aspose.Pdf.Rectangle(newLLX, newLLY, newLLX + newWidth, newLLY + newHeight);
```

Det här steget ändrar storleken på sidan baserat på de nya dimensioner vi just beräknat.

## Steg 6: Rotera sidan

Slutligen ställer vi in sidans rotationsvinkel. Aspose.PDF gör detta superenkelt. Vi kan rotera sidan 90 grader för att växla från stående till liggande format eller tvärtom.

```csharp
page.Rotate = Rotation.on90;
```

Denna kod roterar sidan 90 grader och vänder den till önskad orientering.

## Steg 7: Spara utdata-PDF-filen

Efter att ha tillämpat ändringarna av orienteringen på alla sidor sparar vi det ändrade dokumentet till en ny fil. 

```csharp
dataDir = dataDir + "ChangeOrientation_out.pdf";
doc.Save(dataDir);
System.Console.WriteLine("\nPage orientation changed successfully.\nFile saved at " + dataDir);
```

Se till att du anger ett nytt filnamn (i det här fallet `ChangeOrientation_out.pdf`) för att spara utdata. På så sätt skriver du inte över din ursprungliga fil.

### Slutsats

Och där har du det! Att ändra sidorienteringen på en PDF-fil med Aspose.PDF för .NET är lika enkelt som att ladda dokumentet, loopa igenom sidorna, justera MediaBox och spara den uppdaterade filen. Oavsett om du har ett dåligt skannat dokument eller behöver rotera sidor för att matcha dina formateringsbehov, bör den här steg-för-steg-guiden hjälpa dig.

## Vanliga frågor

### Kan jag rotera specifika sidor istället för alla sidor i PDF-filen?  
Ja, du kan modifiera loopen för att rikta in dig på specifika sidor med hjälp av deras index istället för att loopa igenom alla sidor.

### Vad är `MediaBox`?  
De `MediaBox` definierar sidans storlek och form i en PDF-fil. Det är där sidans innehåll placeras.

### Fungerar Aspose.PDF för .NET med andra filformat?  
Ja, Aspose.PDF kan hantera en mängd olika filformat som HTML, XML, XPS och mer.

### Finns det en gratisversion av Aspose.PDF för .NET?  
Ja, du kan börja med en [gratis provperiod](https://releases.aspose.com/) eller begära en [tillfällig licens](https://purchase.aspose.com/temporary-license/).

### Kan jag ångra ändringarna när de har sparats?  
När du har sparat dokumentet är ändringarna permanenta. Se till att arbeta med en kopia eller spara en säkerhetskopia av originalfilen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}