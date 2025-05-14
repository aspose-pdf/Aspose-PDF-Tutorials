---
"description": "Lär dig hur du söker efter och hämtar text från alla sidor i ett PDF-dokument med Aspose.PDF för .NET."
"linktitle": "Sök och hämta all text"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Sök och hämta all text"
"url": "/sv/net/programming-with-text/search-and-get-text-all/"
"weight": 420
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Sök och hämta all text

## Introduktion

Har du någonsin behövt extrahera specifik text från en PDF men tyckt att det var knepigt? PDF-filer kan ibland kännas som låsta behållare, vilket gör det svårt att få den information du behöver. Men här är de goda nyheterna: med Aspose.PDF för .NET kan du enkelt söka och hämta text från vilken PDF som helst. Detta kraftfulla bibliotek ger allt du behöver för att arbeta med PDF-filer i dina .NET-applikationer, vilket gör textutvinning till en barnlek. I den här handledningen guidar vi dig genom processen att söka och extrahera text från en PDF-fil med Aspose.PDF för .NET. Oavsett om du bygger ett textanalysverktyg eller bara behöver automatisera datautvinning från PDF-rapporter, är du på rätt plats!

## Förkunskapskrav

Innan vi går in i koden, låt oss se till att du har allt konfigurerat:

1. Aspose.PDF för .NET: Du måste ladda ner och installera Aspose.PDF för .NET. Du kan hämta det från nedladdningssidan. [här](https://releases.aspose.com/pdf/net/).
2. .NET-miljö: Se till att du har .NET Framework eller .NET Core konfigurerat på din utvecklingsdator.
3. Grundläggande C##-kunskaper: Viss förtrogenhet med C# och arbete med .NET-projekt rekommenderas.
4. PDF-dokument: Ett exempel på en PDF-fil från vilken vi kommer att extrahera text. I det här exemplet använder vi `SearchAndGetTextFromAll.pdf`.

## Importera paket

Innan du skriver någon kod måste du importera de namnrymder som behövs till ditt projekt för att fungera med Aspose.PDF.

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

Dessa namnrymder ger åtkomst till dokumentobjektmodellen för PDF-filen och låter oss manipulera text i filen.

Låt oss dela upp processen i enkla steg så att du enkelt kan följa den.

## Steg 1: Ställ in dokumentkatalogen

Först och främst måste du ange sökvägen till katalogen där din PDF finns. Detta hjälper programmet att hitta filen från vilken du ska extrahera texten.

```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

- De `dataDir` variabeln ska peka på katalogen där din `SearchAndGetTextFromAll.pdf` filen lagras.
- Ersätta `"YOUR DOCUMENT DIRECTORY"` med den faktiska sökvägen på din maskin.

## Steg 2: Öppna PDF-dokumentet

Nästa steg är att öppna PDF-dokumentet med hjälp av Aspose.PDF. `Document` objekt.

```csharp
// Öppna dokumentet
Document pdfDocument = new Document(dataDir + "SearchAndGetTextFromAll.pdf");
```

- Vi skapar en ny instans av `Document` klassen genom att skicka PDF-filens fullständiga sökväg.
- Detta laddar PDF-filen till minnet och gör den redo för bearbetning.

## Steg 3: Skapa en textabsorberare

De `TextFragmentAbsorber` objektet används för att söka efter specifik text i PDF-filen. I det här fallet letar vi efter ordet ”text”.

```csharp
// Skapa ett TextAbsorber-objekt för att hitta alla förekomster av den inmatade sökfrasen
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("text");
```

- De `TextFragmentAbsorber` initieras med strängen `"text"`Det betyder att den kommer att leta efter alla förekomster av ordet ”text” i PDF-dokumentet.

## Steg 4: Acceptera absorberingsfunktionen för alla sidor

Nu ska vi instruera PDF-dokumentet att acceptera absorberingsverktyget och söka efter texten på alla dess sidor.

```csharp
// Acceptera absorberingsverktyget för alla sidor
pdfDocument.Pages.Accept(textFragmentAbsorber);
```

- De `Accept` Metoden tillämpas på dokumentets sidor. Detta kommer att söka igenom alla sidor efter den angivna texten.

## Steg 5: Extrahera textfragment

När absorberingsprogrammet har skannat dokumentet kan vi hämta de extraherade textfragmenten.

```csharp
// Hämta de extraherade textfragmenten
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- De `TextFragments` egendomen tillhörande `TextFragmentAbsorber` returnerar en samling av alla textfragment som matchar söktermen.

## Steg 6: Loopa igenom textfragmenten

Nu när vi har samlingen av textfragment ska vi loopa igenom dem och extrahera detaljerna.

```csharp
// Loopa igenom fragmenten
foreach (TextFragment textFragment in textFragmentCollection)
{
    Console.WriteLine("Text : {0} ", textFragment.Text);
    Console.WriteLine("Position : {0} ", textFragment.Position);
    Console.WriteLine("XIndent : {0} ", textFragment.Position.XIndent);
    Console.WriteLine("YIndent : {0} ", textFragment.Position.YIndent);
    Console.WriteLine("Font - Name : {0}", textFragment.TextState.Font.FontName);
    Console.WriteLine("Font - IsAccessible : {0} ", textFragment.TextState.Font.IsAccessible);
    Console.WriteLine("Font - IsEmbedded : {0} ", textFragment.TextState.Font.IsEmbedded);
    Console.WriteLine("Font - IsSubset : {0} ", textFragment.TextState.Font.IsSubset);
    Console.WriteLine("Font Size : {0} ", textFragment.TextState.FontSize);
    Console.WriteLine("Foreground Color : {0} ", textFragment.TextState.ForegroundColor);
}
```

- De `foreach` loopar itererar genom varje `TextFragment` i samlingen.
- Vi skriver ut olika egenskaper för varje fragment, såsom den faktiska texten, dess position på sidan, teckensnittsdetaljer och teckenstorlek.
- De `XIndent` och `YIndent` egenskaperna anger de exakta koordinaterna för textfragmentet i PDF-filen.

## Slutsats

Och där har du det! Med bara några få rader kod har vi framgångsrikt sökt och extraherat text från en PDF med hjälp av Aspose.PDF för .NET. Flexibiliteten hos Aspose.PDF låter dig manipulera PDF-filer på många olika sätt, vilket gör det till ett utmärkt val för utvecklare som behöver robusta PDF-lösningar i .NET-miljöer. Du kan enkelt utöka det här exemplet för att söka efter andra ord, extrahera fler detaljer eller till och med manipulera PDF-innehållet baserat på dina behov. Förhoppningsvis har den här guiden gett dig ett tydligt och enkelt sätt att arbeta med PDF-filer. Testa det med dina egna PDF-filer!

## Vanliga frågor

### Kan jag söka efter flera ord samtidigt?  
Ja, du kan ändra `TextFragmentAbsorber` att söka efter flera fraser genom att justera söksträngen därefter.

### Vad händer om texten sträcker sig över flera rader?  
Aspose.PDF kommer fortfarande att känna igen och extrahera text även om den sträcker sig över flera rader. Du kan hantera dessa fragment individuellt.

### Hur sparar jag den extraherade texten till en fil?  
Du kan skriva den extraherade texten till en fil med hjälp av vanliga C#-fil-I/O-operationer, till exempel `StreamWriter`.

### Stöder Aspose.PDF extraktion av text från skannade PDF-filer?  
Aspose.PDF stöder inte OCR. För skannade PDF-filer behöver du ett OCR-verktyg för att tolka texten.

### Hur hanterar jag krypterade PDF-filer?  
Om din PDF är lösenordsskyddad kan du låsa upp den med Aspose.PDF genom att ange lösenordet när du laddar dokumentet.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}