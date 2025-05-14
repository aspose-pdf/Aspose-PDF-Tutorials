---
"description": "Lär dig hur du konverterar HTML till PDF med Aspose.PDF för .NET med den här steg-för-steg-guiden. Perfekt för utvecklare som vill effektivisera dokumentgenerering."
"linktitle": "Ange autentiseringsuppgifter under HTML till PDF"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Ange autentiseringsuppgifter under HTML till PDF"
"url": "/sv/net/document-conversion/provide-credentials-during-html-to-pdf/"
"weight": 240
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ange autentiseringsuppgifter under HTML till PDF

## Introduktion

mjukvaruutvecklingens värld är det vanligt att konvertera HTML till PDF. Oavsett om du genererar rapporter, fakturor eller andra dokument kan ett pålitligt bibliotek för att hantera denna uppgift spara dig mycket tid och ansträngning. Använd Aspose.PDF för .NET, ett kraftfullt bibliotek som låter utvecklare enkelt skapa, manipulera och konvertera PDF-dokument. I den här handledningen guidar vi dig genom processen att använda Aspose.PDF för att konvertera HTML till PDF samtidigt som vi tillhandahåller autentiseringsuppgifter för säker åtkomst. Så ta din kodningshatt och låt oss dyka in!

## Förkunskapskrav

Innan vi börjar finns det några saker du behöver ha på plats:

1. Visual Studio: Se till att du har Visual Studio installerat på din dator. Detta kommer att vara vår utvecklingsmiljö.
2. Aspose.PDF för .NET: Du kan ladda ner biblioteket från [webbplats](https://releases.aspose.com/pdf/net/)Om du vill prova det först kan du också skaffa en [gratis provperiod](https://releases.aspose.com/).
3. Grundläggande kunskaper i C#: Bekantskap med C#-programmering hjälper dig att förstå exemplen bättre.
4. Internetåtkomst: Eftersom vi hämtar HTML-innehåll från en URL, se till att du har en aktiv internetanslutning.

## Importera paket

För att komma igång med Aspose.PDF behöver du importera de nödvändiga paketen till ditt projekt. Så här gör du:

1. Öppna ditt Visual Studio-projekt.
2. Högerklicka på ditt projekt i Solution Explorer och välj "Hantera NuGet-paket".
3. Sök efter "Aspose.PDF" och installera den senaste versionen.

```csharp
using System.IO;
using Aspose.Pdf;
using System;
using System.Net;
```
Nu när vi har allt konfigurerat, låt oss dela upp processen att konvertera HTML till PDF med inloggningsuppgifter i hanterbara steg.

## Steg 1: Konfigurera din dokumentkatalog

Innan vi kan konvertera HTML till PDF måste vi ange var vår PDF-fil ska sparas. Detta görs genom att definiera en sökväg till dokumentkatalogen.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Ersätta `"YOUR DOCUMENT DIRECTORY"` med den faktiska sökvägen dit du vill spara din PDF-fil. Detta kan vara en mapp på skrivbordet eller någon annan plats på ditt system.

## Steg 2: Skapa en webbförfrågan

Nästa steg är att skapa en begäran för att hämta HTML-innehållet från en specifik URL. Det är här vi kommer att använda `WebRequest` klass.

```csharp
WebRequest request = WebRequest.Create("http://My.signchart.com/Report/PrintBook.asp?ProjectGuid=6FB9DBB0-");
```

Här skapar vi en förfrågan till URL:en som innehåller HTML-koden vi vill konvertera. Se till att ersätta URL:en med den du tänker använda.

## Steg 3: Ange inloggningsuppgifter (om det behövs)

Om servern kräver inloggningsuppgifter för att komma åt innehållet måste vi ställa in dem. Detta görs med hjälp av `CredentialCache.DefaultCredentials`.

```csharp
request.Credentials = CredentialCache.DefaultCredentials;
```

Den här raden säkerställer att begäran använder standardinloggningsuppgifterna för den aktuella användaren. Om du behöver ange specifika inloggningsuppgifter kan du skapa en ny. `NetworkCredential` objekt.

## Steg 4: Få svaret

Nu när vi har konfigurerat vår förfrågan är det dags att få svaret från servern.

```csharp
HttpWebResponse response = (HttpWebResponse)request.GetResponse();
```

Den här raden skickar begäran och väntar på att servern ska svara. Om allt går bra får vi det HTML-innehåll vi behöver.

## Steg 5: Läs svarsflödet

När vi har fått svaret behöver vi läsa innehållet som returneras av servern. Detta görs med hjälp av en `StreamReader`.

```csharp
Stream dataStream = response.GetResponseStream();
StreamReader reader = new StreamReader(dataStream);
string responseFromServer = reader.ReadToEnd();
reader.Close();
dataStream.Close();
response.Close();
```

Här läser vi hela innehållet i svarsströmmen in i en strängvariabel som heter `responseFromServer`Glöm inte att stänga läsaren och strömmen för att frigöra resurser.

## Steg 6: Konvertera HTML till PDF

Nu kommer den spännande delen! Vi ska konvertera HTML-innehållet till ett PDF-dokument med hjälp av Aspose.PDF.

```csharp
MemoryStream stream = new MemoryStream(System.Text.Encoding.UTF8.GetBytes(responseFromServer));
HtmlLoadOptions options = new HtmlLoadOptions("http://My.signchart.com/");
options.ExternalResourcesCredentials = CredentialCache.DefaultCredentials;

Document pdfDocument = new Document(stream, options);
```

I det här steget skapar vi en `MemoryStream` från HTML-innehållet och konfigurationen `HtmlLoadOptions`Detta gör att vi kan ange bas-URL:en för alla externa resurser (som bilder eller stilmallar) som HTML-koden kan referera till.

## Steg 7: Spara PDF-dokumentet

Slutligen måste vi spara det genererade PDF-dokumentet i den angivna katalogen.

```csharp
pdfDocument.Save(dataDir + "ProvideCredentialsDuringHTMLToPDF_out.pdf");
```

Den här raden sparar PDF-filen med namnet `ProvideCredentialsDuringHTMLToPDF_out.pdf` katalogen vi angav tidigare.

## Slutsats

Och där har du det! Du har framgångsrikt konverterat HTML till PDF med Aspose.PDF för .NET samtidigt som du tillhandahåller autentiseringsuppgifter för säker åtkomst. Detta kraftfulla bibliotek gör det enkelt att hantera PDF-dokument, och med bara några få rader kod kan du generera professionellt utseende PDF-filer från HTML-innehåll. 

## Vanliga frågor

### Vad är Aspose.PDF för .NET?
Aspose.PDF för .NET är ett bibliotek som låter utvecklare skapa, manipulera och konvertera PDF-dokument i .NET-applikationer.

### Hur installerar jag Aspose.PDF?
Du kan installera Aspose.PDF via NuGet Package Manager i Visual Studio eller ladda ner det från [webbplats](https://releases.aspose.com/pdf/net/).

### Kan jag använda Aspose.PDF gratis?
Ja, Aspose erbjuder en gratis testversion som du kan använda för att utvärdera biblioteket innan du köper.

### Vilka typer av dokument kan jag skapa med Aspose.PDF?
Du kan skapa en mängd olika dokument, inklusive rapporter, fakturor och blanketter, med Aspose.PDF.

### Var kan jag hitta stöd för Aspose.PDF?
Du kan hitta stöd och ställa frågor på [Aspose supportforum](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}