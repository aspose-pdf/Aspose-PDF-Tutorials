---
"description": "Lär dig hur du extraherar text från ett PDF-dokument med hjälp av textenheten i Aspose.PDF för .NET."
"linktitle": "Extrahera text med hjälp av textenhet"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Extrahera text med hjälp av textenhet"
"url": "/sv/net/programming-with-text/extract-text-using-text-device/"
"weight": 210
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text med hjälp av textenhet

## Introduktion

Att extrahera text från en PDF kan vara knepigt, särskilt när man har att göra med dokument som har olika format, inbäddade teckensnitt eller komplexa layouter. Men med Aspose.PDF för .NET blir den här processen en barnlek! Oavsett om du vill konvertera sidor i en PDF till vanlig text för vidare analys eller helt enkelt behöver extrahera specifika avsnitt, har Aspose.PDF det du behöver. I den här handledningen kommer vi steg för steg att förklara hur man extraherar text från en PDF med hjälp av TextDevice-klassen i Aspose.PDF. Vi ger också tydliga förklaringar, så att du enkelt kan tillämpa samma metoder på dina egna projekt.

## Förkunskapskrav

Innan vi går in i koden, se till att du har allt på plats för att följa med. Här är vad du behöver:

1. Aspose.PDF för .NET: Ladda ner den senaste versionen från [Aspose.PDF för .NET nedladdningssida](https://releases.aspose.com/pdf/net/).
2. Utvecklingsmiljö: Visual Studio eller annan C#-utvecklingsmiljö.
3. .NET Framework: Se till att ditt projekt riktar sig mot .NET Framework 4.x eller senare.
4. Inmatnings-PDF-fil: En PDF-fil som du ska använda för textutvinning. Placera den i en katalog på din dator (vi kommer att referera till detta som `YOUR DOCUMENT DIRECTORY`).

## Importera paket

Överst i din kod måste du importera de namnrymder som krävs för att fungera med Aspose.PDF:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Devices;
using System;
using System.Text;
```

## Steg 1: Ladda ditt PDF-dokument

Innan vi extraherar text måste vi ladda PDF-dokumentet till minnet. I det här steget öppnar du din PDF med hjälp av Aspose.PDF:s `Document` klass. Detta ger dig åtkomst till alla sidor och innehåll i filen.

```csharp
// Definiera sökvägen till ditt PDF-dokument
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Ladda PDF-dokumentet
Document pdfDocument = new Document(dataDir + "input.pdf");
```

Här använder vi `Document pdfDocument = new Document(dataDir + "input.pdf");` för att ladda PDF-filen. `dataDir` variabeln innehåller sökvägen till din PDF-fil. Detta ger oss tillgång till hela dokumentet, vilket gör att vi kan loopa igenom sidor och extrahera innehåll.

## Steg 2: Konfigurera en strängbyggare för textlagring

Nu när dokumentet är laddat behöver vi ett sätt att lagra den extraherade texten. För detta använder vi en `StringBuilder` vilket möjliggör effektiv strängsammankoppling.

```csharp
// StringBuilder för att lagra den extraherade texten
StringBuilder builder = new StringBuilder();
```

Vi initierar en `StringBuilder` instans, som samlar in text som extraherats från varje sida. Det är ett mer effektivt sätt att hantera stora strängar jämfört med vanlig strängsammanfogning i en loop.

## Steg 3: Loopa igenom PDF-sidor

Därefter loopar vi igenom varje sida i PDF-dokumentet för att extrahera texten. Vi bearbetar varje sida individuellt med hjälp av `TextDevice` klass, som ansvarar för att konvertera PDF-innehållet till textformat.

```csharp
// Loopa igenom alla sidor i PDF-filen
foreach (Page pdfPage in pdfDocument.Pages)
{
    // Bearbeta varje sida för textutvinning
}
```

Denna loop går igenom varje sida i PDF-filen (`pdfDocument.Pages`). För varje sida extraherar vi texten och lägger till den i vår `StringBuilder`.

## Steg 4: Extrahera text från varje sida

Nu konfigurerar vi textutvinningsprocessen för varje sida. Här skapar vi en `TextDevice` objektet och använd det för att bearbeta PDF-sidorna. `TextDevice` extraherar rå eller formaterad text baserat på de extraheringsalternativ vi anger.

```csharp
using (MemoryStream textStream = new MemoryStream())
{
    // Skapa en textenhet för textutvinning
    TextDevice textDevice = new TextDevice();
    
    // Ställ in textutvinningsalternativen på "Rent"-läge
    TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);
    textDevice.ExtractionOptions = textExtOptions;

    // Extrahera text från aktuell sida och spara den i minnesströmmen
    textDevice.Process(pdfPage, textStream);

    // Konvertera minnesström till text
    string extractedText = Encoding.Unicode.GetString(textStream.ToArray());

    // Lägg till den extraherade texten i StringBuilder
    builder.Append(extractedText);
}
```

- `TextDevice textDevice = new TextDevice();`: Den `TextDevice` Klassen används för att extrahera text från PDF-filen.
- `TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);`: Det här alternativet extraherar råtexten utan att behålla någon formatering som teckensnitt eller positioner. Du kan också använda `TextFormattingMode.Raw` om du behöver mer kontroll över formateringen.
- `textDevice.Process(pdfPage, textStream);`Detta bearbetar varje sida i PDF-filen och lagrar den extraherade texten i en `MemoryStream`.
- Slutligen konverterar vi texten från `MemoryStream` till en sträng och lägg till den `StringBuilder`.

## Steg 5: Spara extraherad text till en fil

Efter att alla sidor har bearbetats lagras texten i `StringBuilder`Det sista steget är att spara den extraherade texten till en fil.

```csharp
// Definiera utdatasökvägen för textfilen
dataDir = dataDir + "input_Text_Extracted_out.txt";

// Spara den extraherade texten till en fil
File.WriteAllText(dataDir, builder.ToString());

Console.WriteLine("\nText extracted successfully from PDF document.\nFile saved at " + dataDir);
```

- `File.WriteAllText(dataDir, builder.ToString());`Detta skriver hela innehållet i `StringBuilder` in i en textfil.
- Sökvägen för utdatafilen anges genom att lägga till ett filnamn (`"input_Text_Extracted_out.txt"`) till `dataDir` väg.

## Slutsats

Att extrahera text från en PDF med Aspose.PDF för .NET är en enkel och effektiv process. Genom att följa stegen som beskrivs i den här guiden kan du enkelt öppna PDF-dokument, loopa igenom sidor och extrahera text till en textfil. Detta är särskilt användbart för att bearbeta stora mängder PDF-data, utföra textanalys eller konvertera dokument för vidare manipulation.

Med Aspose.PDF är du inte begränsad till textutvinning – du kan hantera anteckningar, manipulera bilder eller till och med konvertera PDF-filer till andra format som HTML eller Word. Flexibiliteten och kraften i detta bibliotek gör det till ett ovärderligt verktyg för PDF-hantering i .NET-applikationer.

## Vanliga frågor

### Kan Aspose.PDF extrahera text från bildbaserade PDF-filer?
Nej, Aspose.PDF är utformat för att extrahera text från innehållsbaserade PDF-filer. För bildbaserade PDF-filer behövs OCR-teknik.

### Behåller Aspose.PDF formateringen vid extrahering av text?
Som standard extraheras texten utan formatering, men du kan justera extraheringsalternativen om du vill behålla viss formatering.

### Kan jag extrahera text från ett specifikt sidintervall?
Ja, du kan ändra koden så att den loopar över ett specifikt sidintervall istället för alla sidor.

### Vilka är textutvinningslägena i Aspose.PDF?
Aspose.PDF erbjuder två lägen: Raw och Pure. Raw-läget försöker behålla den ursprungliga layouten, medan Pure-läget bara extraherar texten utan formatering.

### Är Aspose.PDF för .NET kompatibelt med .NET Core?
Ja, Aspose.PDF för .NET är helt kompatibel med .NET Core och .NET Framework.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}