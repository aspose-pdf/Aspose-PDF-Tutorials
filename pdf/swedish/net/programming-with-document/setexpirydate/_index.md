---
"description": "Lär dig hur du anger ett utgångsdatum i PDF-filer med Aspose.PDF för .NET. Förbättra dokumentsäkerheten med den här steg-för-steg-guiden."
"linktitle": "Ange utgångsdatum i PDF-filen"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Ange utgångsdatum i PDF-filen"
"url": "/sv/net/programming-with-document/setexpirydate/"
"weight": 300
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ange utgångsdatum i PDF-filen

## Introduktion

I dagens digitala tidsålder är det viktigare än någonsin att hantera och säkra dokument. Tänk dig att skicka ut en PDF som automatiskt blir otillgänglig efter ett visst datum. Låter som magi, eller hur? Med Aspose.PDF för .NET kan du enkelt ställa in ett utgångsdatum för dina PDF-filer. Den här funktionen är särskilt användbar för känsliga dokument som behöver begränsas efter en viss period. I den här handledningen guidar vi dig genom processen att ställa in ett utgångsdatum i en PDF-fil steg för steg. Så ta din kodningshatt och låt oss dyka in!

## Förkunskapskrav

Innan vi börjar finns det några saker du behöver ha på plats:

1. Utvecklingsmiljö: Se till att du har en .NET-utvecklingsmiljö konfigurerad. Detta kan vara Visual Studio eller någon annan IDE som stöder .NET.
2. Aspose.PDF för .NET: Du måste ha Aspose.PDF-biblioteket installerat. Om du inte har gjort det än kan du ladda ner det från [här](https://releases.aspose.com/pdf/net/).
3. Grundläggande kunskaper i C#: Den här handledningen förutsätter att du har grundläggande förståelse för C#-programmering. Om du är nybörjare på C#, oroa dig inte! Vi kommer att hålla det enkelt och okomplicerat.

## Importera paket

För att komma igång med Aspose.PDF behöver du importera de nödvändiga namnrymderna i ditt C#-projekt. Så här gör du:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
```

Dessa namnrymder ger dig tillgång till de kärnfunktioner som krävs för att arbeta med PDF-dokument i Aspose.PDF.

## Steg 1: Konfigurera din dokumentkatalog

Först och främst måste du ange sökvägen till din dokumentkatalog. Det är här din PDF-fil kommer att sparas. 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Ersätta `"YOUR DOCUMENT DIRECTORY"` med den faktiska sökvägen dit du vill spara din PDF-fil. Det är som att säga till ditt program: "Hörru, det är här jag sparar mina filer!"

## Steg 2: Instansiera dokumentobjektet

Nästa steg är att skapa en ny instans av `Document` klass. Detta är din arbetsyta där du skapar din PDF.

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

Tänk på `Document` objektet som ett tomt pappersark. Du kan lägga till innehåll på det hur du vill!

## Steg 3: Lägg till en sida i PDF-filen

Nu när du har konfigurerat ditt dokument är det dags att lägga till en sida i det. Det är här ditt innehåll kommer att placeras.

```csharp
doc.Pages.Add();
```

Du har precis skapat en ny sida i din PDF. Det är som att lägga till en ny sida i din anteckningsbok där du kan anteckna dina tankar.

## Steg 4: Lägg till text på sidan

Låt oss göra den här sidan lite mer intressant genom att lägga till lite text. Vi lägger till ett enkelt "Hej världen"-meddelande.

```csharp
doc.Pages[1].Paragraphs.Add(new TextFragment("Hello World..."));
```

Den här kodraden lägger till ett textfragment på den första sidan i din PDF. Det är som att skriva en titel högst upp på sidan!

## Steg 5: Skapa JavaScript för utgångsdatum

Nu kommer det roliga! Du ska skapa en JavaScript-åtgärd som kontrollerar PDF-filens utgångsdatum. Om det aktuella datumet överskrider utgångsdatumet kommer ett meddelande att varna användaren.

```csharp
JavascriptAction javaScript = new JavascriptAction(
"var year=2017;"
+ "var month=5;"
+ "today = new Date(); today = new Date(today.getFullYear(), today.getMonth());"
+ "expiry = new Date(year, month);"
+ "if (today.getTime() > expiry.getTime())"
+ "app.alert('The file is expired. You need a new one.');");
```

Här är vad som händer:
- Du anger utgångsår och utgångsmånad.
- Du får dagens datum.
- Du jämför dagens datum med utgångsdatumet.
- Om dagens datum har passerat utgångsdatumet dyker ett meddelande upp!

## Steg 6: Ställ in JavaScript som PDF-öppningsåtgärd

Nu behöver du ställa in JavaScript-åtgärden som öppningsåtgärd för ditt PDF-dokument. Det betyder att JavaScript-kommandot körs så snart PDF-filen öppnas.

```csharp
doc.OpenAction = javaScript;
```

Den här raden anger att PDF-filen ska köra JavaScript-koden när någon öppnar den. Det är som att ställa in en påminnelse som går igång så fort du öppnar din kalender!

## Steg 7: Spara PDF-dokumentet

Äntligen är det dags att spara ditt PDF-dokument med funktionen för utgångsdatum. 

```csharp
dataDir = dataDir + "SetExpiryDate_out.pdf";
doc.Save(dataDir);
```

Den här raden sparar din PDF till den angivna katalogen med namnet "SetExpiryDate_out.pdf". Det är som att sätta ditt färdiga konstverk i en ram!

## Slutsats

Och där har du det! Du har skapat en PDF-fil med ett utgångsdatum med Aspose.PDF för .NET. Den här funktionen förbättrar inte bara säkerheten utan säkerställer också att känslig information hålls under kontroll. Oavsett om du skickar ut kontrakt, rapporter eller andra viktiga dokument kan det vara revolutionerande att sätta ett utgångsdatum.

## Vanliga frågor

### Vad är Aspose.PDF för .NET?
Aspose.PDF för .NET är ett kraftfullt bibliotek som låter utvecklare skapa, manipulera och konvertera PDF-dokument i .NET-applikationer.

### Kan jag använda Aspose.PDF gratis?
Ja, du kan använda en gratis testversion av Aspose.PDF. Du kan ladda ner den. [här](https://releases.aspose.com/).

### Hur köper jag Aspose.PDF?
Du kan köpa Aspose.PDF genom att besöka [köpsida](https://purchase.aspose.com/buy).

### Vad händer om jag behöver stöd?
Om du har några frågor eller behöver hjälp kan du besöka [Aspose supportforum](https://forum.aspose.com/c/pdf/10).

### Kan jag få en tillfällig licens för Aspose.PDF?
Ja, du kan ansöka om ett tillfälligt körkort [här](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}