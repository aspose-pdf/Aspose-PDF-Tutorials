---
"description": "Lär dig hur du ställer in callout-egenskapen i en PDF-fil med Aspose.PDF för .NET i den här detaljerade steg-för-steg-handledningen."
"linktitle": "Ange callout-egenskap i PDF-fil"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Ange callout-egenskap i PDF-fil"
"url": "/sv/net/annotations/setcalloutproperty/"
"weight": 130
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ange callout-egenskap i PDF-fil

## Introduktion

Att skapa professionella och visuellt tilltalande PDF-dokument kräver ofta att man lägger till anteckningar som drar uppmärksamhet till specifikt innehåll. En sådan anteckning är callout, som liknar de där pratbubblor man ser i serier. De hjälper till att förtydliga eller betona text i din PDF. Aspose.PDF för .NET gör det otroligt enkelt att lägga till sådana anteckningar i dina dokument, och i den här handledningen går vi igenom hur man ställer in callout-egenskapen i en PDF-fil med hjälp av detta kraftfulla bibliotek. Oavsett om du är en erfaren utvecklare eller precis har börjat, kommer du i slutet av den här guiden att ha en tydlig förståelse för hur man arbetar med callouts i PDF-filer.

## Förkunskapskrav

Innan vi dyker in i koden, låt oss gå igenom det viktigaste du behöver för att komma igång.

1. Aspose.PDF för .NET: Se till att du har biblioteket Aspose.PDF för .NET installerat. Du kan ladda ner det från [här](https://releases.aspose.com/pdf/net/).
2. IDE: En utvecklingsmiljö som Visual Studio.
3. .NET Framework: Se till att du har .NET installerat på din dator.
4. Tillfällig licens: Om du vill testa alla funktioner i Aspose.PDF utan begränsningar, skaffa en [tillfällig licens](https://purchase.aspose.com/temporary-license/).

## Importera paket

Innan du börjar skriva koden måste du importera de nödvändiga paketen som gör att du kan arbeta med PDF-filer och anteckningar.

```csharp
using Aspose.Pdf.Annotations;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
```

Dessa importer ger dig alla nödvändiga klasser och metoder för att manipulera PDF-dokument och skapa anteckningar som callout.

## Steg 1: Initiera PDF-dokumentet

Det första steget i vår resa är att initiera ett nytt PDF-dokument där vi ska lägga till vår callout-annotering. Tänk på detta som att skapa en tom arbetsyta där du kan börja lägga till element.

```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Initiera ett nytt PDF-dokument
Document doc = new Document();
```
Här skapar vi ett nytt `Document` objekt som kommer att fungera som vår PDF-fil. Den `dataDir` variabeln är inställd på den katalog där du vill spara din PDF-fil när vi är klara.

## Steg 2: Lägg till en ny sida i dokumentet

Ett PDF-dokument kan ha flera sidor, och i det här steget lägger vi till en ny sida i vårt dokument. Det är på den här sidan som vår anteckning för bildtexten kommer att placeras.

```csharp
// Lägg till en ny sida i dokumentet
Page page = doc.Pages.Add();
```
De `Pages.Add()` Metoden används för att lägga till en ny sida till `doc` objektet. Den nya sidan lagras i `page` variabel, som vi kommer att använda senare när vi lägger till annoteringen.

## Steg 3: Definiera standardutseendet

Annoteringar, liksom bildtexten, har ett visuellt utseende som du kan anpassa. I det här steget definierar vi hur texten i bildtexten ska se ut.

```csharp
// Definiera standardutseendet för annoteringen
DefaultAppearance da = new DefaultAppearance();
da.TextColor = System.Drawing.Color.Red;
da.FontSize = 10;
```
Vi skapar en `DefaultAppearance` objekt som definierar textfärg och teckenstorlek. Här kommer texten att vara röd och teckenstorleken är inställd på 10. Detta utseende kommer att tillämpas på annoteringen av callout-texten.

## Steg 4: Skapa fritextannoteringen

Nu är det dags att skapa själva annoteringen. Fritextannoteringen är det som låter oss lägga till en callout med specifik text och stil.

```csharp
// Skapa en FreeTextAnnotation med en callout
FreeTextAnnotation fta = new FreeTextAnnotation(page, new Rectangle(422.25, 645.75, 583.5, 702.75), da);
fta.Intent = FreeTextIntent.FreeTextCallout;
fta.EndingStyle = LineEnding.OpenArrow;
```
Vi skapar en `FreeTextAnnotation` objekt med specifika koordinater, vilket definierar dess position på sidan. Den `Intent` är inställd på `FreeTextCallout`, vilket indikerar att detta är en annotering för utrop. `EndingStyle` är inställd på `OpenArrow`, vilket betyder att raden med meddelanden slutar med en öppen pil.

## Steg 5: Definiera punkterna för callout-linjen

En callout-annotering har en linje som pekar mot det aktuella området. Här definierar vi punkterna som utgör denna linje.

```csharp
// Definiera punkterna för callout-linjen
fta.Callout = new Point[]
{
    new Point(428.25, 651.75), 
    new Point(462.75, 681.375), 
    new Point(474, 681.375)
};
```
De `Callout` egenskapen är en matris av `Point` objekt, som vart och ett representerar en koordinat på sidan. Dessa punkter definierar vägen för callout-linjen, vilket ger den det klassiska pratbubblautseendet.

## Steg 6: Lägg till anteckningen på sidan

Efter att ha skapat och konfigurerat vår annotering är nästa steg att lägga till den på sidan.

```csharp
// Lägg till anteckningen på sidan
page.Annotations.Add(fta);
```
De `Annotations.Add()` Metoden används för att placera anteckningen på sidan vi skapade tidigare. Detta steg "ritar" effektivt ut callout-filen på PDF-sidan.

## Steg 7: Ställ in RTF-innehållet

Annoteringar i bildtexter kan innehålla RTF, vilket möjliggör formaterat innehåll i bubblan. Nu lägger vi till lite exempeltext.

```csharp
// Ange RTF för anteckningen
fta.RichText = "<body xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:xfa=\"http://www.xfa.org/schema/xfa-data/1.0/\" xfa:APIVersion=\"Acrobat:11.0.23\" xfa:spec=\"2.0.2\" style=\"color:#FF0000;font-weight:normal;font-style:normal;font-stretch:normal\"><p dir=\"ltr\"><span style=\"font-size:9.0pt;font-family:Helvetica\">Detta är ett exempel</span></p></body>";
```
De `RichText` egenskapen är inställd med HTML-innehåll. Detta möjliggör detaljerad formatering inom anropet, till exempel att ange teckenstorlek, färg och stil.

## Steg 8: Spara PDF-dokumentet

Slutligen, efter att allt är klart, behöver vi spara dokumentet. Detta steg slutför skapandet av PDF-filen med annoteringen för callout.

```csharp
// Spara dokumentet
doc.Save(dataDir + "SetCalloutProperty.pdf");
```
De `Save()` Metoden sparar dokumentet i den angivna katalogen med filnamnet "SetCalloutProperty.pdf". Detta steg avslutar vår process för att skapa PDF-filer.

## Slutsats

Och där har du det! Du har precis skapat ett PDF-dokument med en callout-annotering med Aspose.PDF för .NET. Denna annotering kan vara otroligt användbar för att markera eller förklara specifika delar av ditt dokument. Aspose.PDF erbjuder ett kraftfullt API som gör PDF-manipulering enkel och flexibel. Oavsett om du lägger till annoteringar, konverterar dokument eller hanterar komplexa PDF-uppgifter, har Aspose.PDF det du behöver.

## Vanliga frågor

### Kan jag anpassa utseendet på bildtexten ytterligare?

Absolut! Du kan anpassa olika aspekter som linjefärg, tjocklek och textens typsnitt och stil.

### Är det möjligt att lägga till flera callouts på en och samma sida?

Ja, du kan lägga till så många anteckningar som behövs genom att upprepa stegen för varje annotering.

### Hur ändrar jag placeringen av callouten?

Ändra helt enkelt koordinaterna i `Rectangle` och `Callout` egenskaper för att omplacera anteckningen.

### Kan jag lägga till andra typer av anteckningar med Aspose.PDF?

Ja, Aspose.PDF stöder olika anteckningstyper, inklusive markeringar, stämplar och filbilagor.

### Är RTF-innehållet begränsat till HTML?

De `RichText` egenskapen stöder en delmängd av HTML, vilket gör att du kan inkludera formaterad text och grundläggande formatering.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}