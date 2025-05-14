---
"description": "Lär dig hur du lägger till en bild och sidnummer i din PDF-fils sidhuvud och sidfot med hjälp av Aspose.PDF för .NET i den här steg-för-steg-handledningen."
"linktitle": "Bild och sidnummer i sidhuvuds- och sidfotssektionen"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Bild och sidnummer i sidhuvuds- och sidfotssektionen"
"url": "/sv/net/programming-with-stamps-and-watermarks/image-and-page-number-in-header-footer-section/"
"weight": 110
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Bild och sidnummer i sidhuvuds- och sidfotssektionen

## Introduktion

När det gäller att skapa PDF-dokument av professionell kvalitet är det viktigt att ha kontroll över mindre detaljer som sidhuvud och sidfot. Du vill att dina dokument ska se snygga och välorganiserade ut, eller hur? Med Aspose.PDF för .NET kan du lägga till bilder och sidnummer sömlöst i dokumentets sidhuvud och sidfot. I den här handledningen kommer vi att guida dig genom varje steg, vilket gör det enkelt att följa med.

## Förkunskapskrav

Innan du går in på detaljerna i den här handledningen, se till att du har följande ordning:

1. .NET Framework: Du behöver ha valfri version av .NET Framework installerad på din dator. Om du inte har den kan du enkelt ladda ner den från Microsofts webbplats.
2. Aspose.PDF för .NET: Eftersom vi kommer att använda Aspose.PDF, se till att du har det installerat i ditt projekt. Du kan ladda ner en testversion. [här](https://releases.aspose.com/pdf/net/).
3. Grundläggande kunskaper i C#: Bekantskap med grundläggande C#-programmering kommer säkerligen att hjälpa dig att förstå koden utan större krångel.
4. En bildfil: Du behöver en bild som du vill lägga till i sidhuvudet på ditt PDF-dokument, till exempel en logotyp. Spara den i en lättillgänglig katalog. 
5. IDE: Använd en integrerad utvecklingsmiljö (IDE) som du väljer, som Visual Studio, för att arbeta med ditt .NET-projekt.

När du har alla förkunskaper redo är du redo att skapa en fantastisk PDF-fil!

## Importera paket

För att börja använda Aspose.PDF för .NET måste du importera de nödvändiga namnrymderna. Överst i din C#-fil lägger du till:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Image;
```

Dessa namnrymder ger dig tillgång till de klasser som behövs för att manipulera PDF-filer.

Nu ska vi gå vidare till det verkliga! Följ dessa steg för att skapa ditt PDF-dokument, med en bild i sidhuvudet och sidnummer i sidfoten.

## Steg 1: Ställ in din dokumentkatalog

Varje bra projekt börjar med organisation. Definiera din dokumentkatalog där du ska spara dina filer och var din bild finns. Så här gör du:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Kom ihåg att byta ut `"YOUR DOCUMENT DIRECTORY"` med den faktiska sökvägen där du vill spara din PDF och var din bild finns.

## Steg 2: Skapa ett nytt PDF-dokument

Nästa steg är att skapa ett nytt PDF-dokument där all magi kommer att hända:

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

Vid det här laget har du skapat ett tomt PDF-dokument. Spännande, eller hur?

## Steg 3: Lägg till en sida i dokumentet

En PDF handlar om sidor. Låt oss lägga till en ny sida i vårt dokument med hjälp av:

```csharp
Aspose.Pdf.Page page = doc.Pages.Add();
```

Nu har du en duk där du kan börja designa!

## Steg 4: Skapa rubriksektionen

Din rubrik kommer att innehålla bilden (som en logotyp) som du vill visa. Skapa rubrikavsnittet med följande kod:

```csharp
Aspose.Pdf.HeaderFooter header = new Aspose.Pdf.HeaderFooter();
page.Header = header;
```

Nu har du en rubrik som du kan anpassa!

## Steg 5: Lägg till en bild i sidhuvudet

Nu kommer vi till det roliga! Du måste lägga till bilden i din rubrik. Först skapar du ett bildobjekt:

```csharp
Aspose.Pdf.Image image1 = new Aspose.Pdf.Image();
```

Ange sökvägen för din bild:

```csharp
image1.File = dataDir + "aspose-logo.jpg";
```

Slutligen, lägg till bilden i din rubrik:

```csharp
header.Paragraphs.Add(image1);
```

Grattis! Du har just lagt till en bild i din PDF-rubrik.

## Steg 6: Skapa sidfotssektionen

Nu ska vi arbeta med sidfoten. I likhet med sidhuvudprocessen, skapa ett sidfotsobjekt:

```csharp
Aspose.Pdf.HeaderFooter footer = new Aspose.Pdf.HeaderFooter();
page.Footer = footer;
```

Det är här du placerar ditt sidnummer. 

## Steg 7: Lägg till text i sidfoten

Skapa ett textfragment som innehåller sidnumret:

```csharp
Aspose.Pdf.Text.TextFragment txt = new Aspose.Pdf.Text.TextFragment("Page: ($p of $P ) ");
```

Lägg sedan till detta textfragment i sidfoten:

```csharp
footer.Paragraphs.Add(txt);
```

Ser du hur enkelt det var? Du har ställt in ditt sidnummer dynamiskt!

## Steg 8: Spara PDF-dokumentet

Det sista steget i vårt äventyr är att spara dokumentet. Använd det här kommandot för att spara din nyskapade PDF:

```csharp
doc.Save(dataDir + "ImageAndPageNumberInHeaderFooter_out.pdf");
```

Och precis så är din PDF klar och laddad med en sidhuvudbild och sidnummer i sidfoten!

## Slutsats

Och där har du det! Du har precis skapat en PDF med en bild i sidhuvudet och dynamiska sidnummer i sidfoten med Aspose.PDF för .NET. Det är helt otroligt hur några få rader kod kan resultera i en så polerad utskrift. Oavsett om det är för en företagsrapport eller ett personligt dokument, förändrar dessa element tonen och professionalismen i din PDF.

## Vanliga frågor

### Kan jag använda Aspose.PDF på vilken .NET-plattform som helst?
Ja, Aspose.PDF för .NET stöder flera .NET-plattformar, inklusive .NET Framework, .NET Core och mer.

### Finns det en gratis testversion av Aspose.PDF?
Absolut! Du kan ladda ner en gratis testversion [här](https://releases.aspose.com/).

### Vilka bildformat stöds för rubriker?
Aspose.PDF stöder de vanligaste bildformaten som JPG, PNG och BMP för sidhuvud och sidfot.

### Kan jag anpassa sidnummerformatet?
Ja, du kan enkelt anpassa sidfotstexten och formatet efter dina behov.

### Finns teknisk support tillgänglig?
Ja, Aspose erbjuder dedikerad support via sitt forum. Du kan kontakta dem för att få hjälp. [här](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}