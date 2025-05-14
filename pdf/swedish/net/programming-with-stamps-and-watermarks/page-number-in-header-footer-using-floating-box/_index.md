---
"description": "Lägg enkelt till sidnummer i ditt PDF-sidhuvud och -sidfot med hjälp av en flytande ruta med Aspose.PDF för .NET i den här steg-för-steg-handledningen."
"linktitle": "Sidnummer i sidhuvudsfot med flytande ruta"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Sidnummer i sidhuvudsfot med flytande ruta"
"url": "/sv/net/programming-with-stamps-and-watermarks/page-number-in-header-footer-using-floating-box/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Sidnummer i sidhuvudsfot med flytande ruta

## Introduktion

När det gäller att hantera PDF-dokument programmatiskt utmärker sig Aspose.PDF för .NET som ett exceptionellt verktyg. Det förenklar hur vi skapar, redigerar och manipulerar PDF-filer i .NET-applikationer. Oavsett om du genererar fakturor, rapporter eller någon annan dokumenttyp kan elegant sidnummer förbättra professionalismen och organisationen i dina PDF-filer. I den här handledningen går vi in på hur du lägger till sidnummer i sidhuvudet och sidfoten i din PDF med hjälp av en flytande ruta. Redo att komma igång? Nu kör vi!

## Förkunskapskrav

Innan vi börjar denna spännande resa in i PDF-manipulationens värld, finns det några saker du behöver ha:

### Installation av .NET-miljö
Se till att du har en .NET-utvecklingsmiljö. Du kan använda Visual Studio, vilket är ett populärt val bland utvecklare för .NET-applikationer.

### Aspose.PDF-bibliotek
Installera Aspose.PDF-biblioteket. Du kan enkelt ladda ner det från webbplatsen:

- [Ladda ner Aspose.PDF för .NET](https://releases.aspose.com/pdf/net/)

### Grundläggande kunskaper i C#-programmering
En grundläggande förståelse för C# hjälper dig att förstå koncepten och kodavsnitten som presenteras i den här handledningen.

### Tillgång till dokumentationen
Det är alltid fördelaktigt att ha [Aspose.PDF-dokumentation](https://reference.aspose.com/pdf/net/) praktisk för referens och djupare utforskning av eventuella ytterligare funktioner.

## Importera paket

För att komma igång måste du importera de nödvändiga paketen i ditt projekt. Detta säkerställer att Aspose.PDF-assemblingen är tillgänglig för användning i din kod. Så här gör du:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Nu ska vi dela upp processen för att lägga till sidnummer med hjälp av en flytande ruta i hanterbara steg. Följ med när vi går igenom.

## Steg 1: Konfigurera din dokumentmiljö

Låt oss börja med att ange katalogen där ditt PDF-dokument ska lagras. Detta är avgörande eftersom det avgör var din utdatafil sparas.

```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Ersätta `YOUR DOCUMENT DIRECTORY` med den sökväg du väljer där du vill spara PDF-filen.

## Steg 2: Instansiera dokumentet

Nästa steg är att skapa ett nytt PDF-dokument. Detta innebär att använda `Document` klassen från Aspose.PDF-biblioteket.

```csharp
// Instansiera dokumentinstans
Aspose.Pdf.Document pdf = new Aspose.Pdf.Document();
```
Här skapar vi en ny instans av `Document` klass, som fungerar som vår duk för manipulation.

## Steg 3: Lägg till en ny sida

Nu ska vi lägga till en sida i vårt PDF-dokument. Varje PDF behöver minst en sida, eller hur?

```csharp
// Lägg till en sida i PDF-dokumentet
Aspose.Pdf.Page page = pdf.Pages.Add();
```
Det här kodavsnittet lägger till en ny sida i vårt dokument, vilket gör det redo att ta emot innehåll, inklusive vår flytande ruta med sidnummer.

## Steg 4: Skapa en flytande låda

Nu är det dags att skapa vår flytande ruta som ska innehålla sidnumret. `FloatingBox` klassen låter oss placera innehåll fritt på sidan.

```csharp
// Initierar en ny instans av FloatingBox-klassen
Aspose.Pdf.FloatingBox box1 = new Aspose.Pdf.FloatingBox(140, 80);
```
Här är parametrarna `(140, 80)` Ange bredden och höjden på den flytande rutan. Du kan justera dessa värden baserat på dina layoutpreferenser.

## Steg 5: Placering av den flytande lådan

Positionering är nyckeln! Du vill bestämma var sidnumret ska visas på sidan. Du kommer att arbeta med `Left` och `Top` egenskaper för att ange positionen.

```csharp
// Flyttal som anger styckets vänstra position
box1.Left = 2;
// Flyttal som anger styckets översta position
box1.Top = 10;
```
Dessa värden avgör placeringen av den flytande rutan på sidan. Experimentera gärna med dem för att se vad som ser bäst ut för ditt dokument.

## Steg 6: Lägg till text med sidnummermakrot

Nu ska vi lägga till en sträng som dynamiskt visar sidnumret. Det är här magin händer!

```csharp
// Lägg till makrona i styckesamlingen i FloatingBox
box1.Paragraphs.Add(new Aspose.Pdf.Text.TextFragment("Page: ($p/ $P )"));
```
I det här fallet, `($p/ $P)` är ett makro som visar det aktuella sidnumret (`$p`) och det totala antalet sidor (`$P`). Som ett resultat formateras texten till att läsas något i stil med "Sida: 1/5".

## Steg 7: Lägg till den flytande rutan på sidan

Det är dags att lägga till den flytande rutan, tillsammans med sidnummertexten, på vår nyskapade sida.

```csharp
// Lägg till en flytande ruta på sidan
page.Paragraphs.Add(box1);
```
Den här raden bäddar i huvudsak in din flytande ruta på sidan, vilket gör den till en del av dokumentets layout. 

## Steg 8: Spara ditt dokument

Slutligen, glöm inte att spara ditt arbete! Det sista steget är att spara ditt PDF-dokument med ett korrekt filnamn.

```csharp
// Spara dokumentet
pdf.Save(dataDir + "PageNumberinHeaderFooterUsingFloatingBox_out.pdf");
```
Se till att den angivna sökvägen innehåller önskat filnamn. Nu är din fantastiska PDF med sidnummer skapad! 

## Slutsats

Och där har ni det, gott folk! Att lägga till sidnummer i sidhuvudet och sidfoten på er PDF med Aspose.PDF för .NET är så enkelt. Med bara några få rader kod har ni påbörjat en resa för att bemästra dokumenthantering i era applikationer. Tveka inte att experimentera med olika layouter och formateringar – kreativiteten känner trots allt inga gränser! Redo att generera det där professionella dokumentet? Ta er kodningshatt och börja experimentera.

## Vanliga frågor

### Kan jag anpassa utseendet på sidnumreringstexten?  
Ja, du kan anpassa textegenskaper, som teckenstorlek, färg och stil, genom att justera `TextFragment` egenskaper.

### Är Aspose.PDF gratis att använda?  
Även om Aspose.PDF erbjuder en gratis provperiod är det en betald produkt för produktionsbruk. [köp den här](https://purchase.aspose.com/buy).

### Var kan jag hitta mer detaljerad dokumentation?  
Du kan hitta omfattande dokumentation om [Aspose.PDF-dokumentationswebbplats](https://reference.aspose.com/pdf/net/).

### Hur använder jag sidhuvuden och sidfot på flera sidor?  
Du kan loopa igenom alla sidor i ditt dokument och tillämpa den flytande rutan på var och en på liknande sätt.

### Vad händer om jag behöver support för ytterligare funktioner?  
För ytterligare frågor eller support kan du besöka [Aspose-forumet](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}