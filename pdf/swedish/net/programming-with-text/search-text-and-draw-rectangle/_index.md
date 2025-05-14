---
"description": "Lär dig söka efter text i PDF-filer och markera den med rektanglar med Aspose.PDF för .NET! Enkel steg-för-steg-handledning för förbättrade PDF-hanteringsfärdigheter."
"linktitle": "Sök text och rita rektangel"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Sök text och rita rektangel"
"url": "/sv/net/programming-with-text/search-text-and-draw-rectangle/"
"weight": 460
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Sök text och rita rektangel

## Introduktion

Vill du förbättra dina PDF-hanteringsfärdigheter? Vill du lära dig hur du söker efter specifik text i PDF-filer och markerar den med en rektangel? Då har du kommit till rätt ställe! Idag ska jag guida dig genom hur du använder Aspose.PDF för .NET för att söka efter text i ett PDF-dokument och rita rektanglar runt det. Den här artikeln ger en steg-för-steg-handledning utformad med tydlighet och användbarhet i åtanke, så att du kan följa med och tillämpa dessa tekniker i dina projekt. 

## Förkunskapskrav

Innan vi går in i handledningen, låt oss förbereda vad du behöver för att säkerställa ett smidigt arbetsflöde:

1. Grundläggande förståelse för .NET: Du bör vara bekant med C#-programmering och .NET-ramverket för att kunna följa den här handledningen effektivt.
   
2. Visual Studio installerat: Du behöver en integrerad utvecklingsmiljö (IDE) för att skriva och testa din kod. Visual Studio Community är ett bra alternativ och det är gratis.
   
3. Aspose.PDF för .NET: Du måste ha Aspose.PDF-biblioteket installerat i ditt projekt. Du kan ladda ner det [här](https://releases.aspose.com/pdf/net/) eller överväga en [tillfällig licens](https://purchase.aspose.com/temporary-license/) för utökade funktioner.
   
4. Exempel på PDF-dokument: För den här handledningen behöver du en exempel-PDF-fil med namnet `SearchAndGetTextFromAll.pdf` lagras i din projektkatalog. 

## Importera paket

För att komma igång måste du först importera de nödvändiga paketen till ditt .NET-projekt. Följ dessa steg:

### Öppna Visual Studio

Starta Visual Studio och skapa ett nytt konsolprogram eller använd ett befintligt program där du vill implementera PDF-funktionerna.

### Lägg till Aspose.PDF i ditt projekt

1. Högerklicka på ditt projekt i lösningsutforskaren.
2. Välj "Hantera NuGet-paket".
3. Leta efter `Aspose.PDF` och installera den senaste versionen.

Genom att göra detta lägger du grunden för alla fantastiska PDF-manipulationer du ska utföra.

## Importera namnrymder

Överst i din programfil vill du importera relevanta namnrymder från Aspose-biblioteket:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
using Aspose.Pdf.Facades;
```

Detta gör det enklare att komma åt klasser och metoder i Aspose.PDF-biblioteket för dina uppgifter.


Nu när du har allt konfigurerat, låt oss dela upp processen att söka efter text i en PDF och rita en rektangel runt den i hanterbara steg.

## Steg 1: Ange sökvägen för ditt dokument

Ange först sökvägen till din PDF-fil. Se till att ersätta den. `YOUR DOCUMENT DIRECTORY` med den faktiska vägen dit din `SearchAndGetTextFromAll.pdf` lagras.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

## Steg 2: Öppna PDF-dokumentet

Skapa sedan en instans av `Document` klass för att ladda din PDF:

```csharp
Document document = new Document(dataDir + "SearchAndGetTextFromAll.pdf");
```

Den här kodraden öppnar din angivna PDF-fil, så att du kan manipulera den ytterligare.

## Steg 3: Skapa en textabsorberare

Nu behöver du ett sätt att söka efter text i dokumentet. För detta använder vi `TextFragmentAbsorber`:

```csharp
TextFragmentAbsorber textAbsorber = new TextFragmentAbsorber(@"[\S]+");
```

Det reguljära uttrycket `@"[\S]+"` är utformad för att matcha alla strängar som inte är blanksteg i PDF-filen. 

## Steg 4: Konfigurera alternativ för textsökning

Nästa steg är att ställa in alternativen för textsökning:

```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions(true);
textAbsorber.TextSearchOptions = textSearchOptions;
```

Här, den `true` parametern innebär att sökningen kommer att vara skiftlägeskänslig. Du kan ställa in den på `false` om du vill ha en sökning som inte känsligar för versaler.

## Steg 5: Acceptera textabsorberaren i dokumentet

Med din `TextFragmentAbsorber` och sökalternativen är redo, det är dags att ta till sig text från dokumentet:

```csharp
document.Pages.Accept(textAbsorber);
```

Den här metoden undersöker varje sida i din PDF för att hitta textfragment som matchar det angivna mönstret.

## Steg 6: Skapa en PDF-innehållsredigerare

För att rita former i dokumentet behöver du `PdfContentEditor`:

```csharp
var editor = new PdfContentEditor(document);
```

Den här redigeraren låter dig enkelt manipulera och redigera PDF-innehållet.

## Steg 7: Loopa igenom funna textfragment

Nu vill du loopa igenom de funna textfragmenten för att rita rektanglar runt dem:

```csharp
foreach (TextFragment textFragment in textAbsorber.TextFragments)
{
    foreach (TextSegment textSegment in textFragment.Segments)
    {
        DrawBox(editor, textFragment.Page.Number, textSegment, System.Drawing.Color.Red);
    }
}
```

Denna loop itererar över varje textfragment och deras segment och anropar en `DrawBox` metod för rektangelritning.

## Steg 8: Definiera DrawBox-metoden

Du behöver definiera `DrawBox` metod, som hanterar logiken för rektangelritning. Här är en enkel implementering:

```csharp
private static void DrawBox(PdfContentEditor editor, int pageNumber, TextSegment textSegment, System.Drawing.Color color)
{
    // Beräkna rektangelns dimensioner baserat på textsegmentet
    float x = textSegment.Rectangle.LLX;
    float y = textSegment.Rectangle.LLY;
    float width = textSegment.Rectangle.Width;
    float height = textSegment.Rectangle.Height;

    // Rita en rektangel med hjälp av de beräknade värdena
    editor.DrawRectangle(pageNumber, x, y, width, height, color, 1);
}
```

Den här metoden bestämmer rektangelns position och storlek baserat på segmentets begränsande rektangel och använder redigeraren för att rita den.

## Steg 9: Spara det ändrade dokumentet

Efter att du har ritat rektanglarna runt den funna texten kan du spara det ändrade dokumentet:

```csharp
dataDir = dataDir + "SearchTextAndDrawRectangle_out.pdf";
document.Save(dataDir);
```

Se till att din nya fil sparas med ett distinkt namn för att undvika att skriva över ditt ursprungliga dokument.

## Steg 10: Bekräftelsemeddelande

Slutligen, skriv ut ett bekräftelsemeddelande till konsolen för att meddela att operationen lyckades:

```csharp
Console.WriteLine("\nRectangle drawn successfully on searched text.\nFile saved at " + dataDir);
```

Och där har du det! Du har skapat ett skript för att söka efter text i en PDF och markera den med rektanglar.

## Slutsats

Grattis! Du har precis låst upp en kraftfull färdighet som avsevärt kan förbättra dina PDF-manipulationsförmågor med Aspose.PDF för .NET. Med bara några få enkla steg kan du söka efter valfri text i ditt dokument och markera den visuellt, vilket gör dina PDF-dokument mer interaktiva och hanterbara. Tveka inte att experimentera med olika regex-mönster och färgalternativ för att verkligen göra det här verktyget till ditt eget!

## Vanliga frågor

### Vad är Aspose.PDF för .NET?
Aspose.PDF för .NET är ett bibliotek som erbjuder ett omfattande sätt att skapa, manipulera och konvertera PDF-dokument programmatiskt.

### Kan jag använda Aspose.PDF gratis?
Ja, Aspose erbjuder en gratis provperiod som du kan använda för att testa bibliotekets funktioner. Kolla in det. [här](https://releases.aspose.com/).

### Vilket programmeringsspråk behöver jag använda med Aspose.PDF för .NET?
Aspose.PDF för .NET är utformat för att användas med C# och andra .NET-språk.

### Hur får jag hjälp med Aspose.PDF?
Du kan besöka Asposes supportforum för att få hjälp med eventuella problem eller frågor du kan ha. Hitta support [här](https://forum.aspose.com/c/pdf/10).

### Var laddar jag ner Aspose.PDF för .NET?
Du kan ladda ner biblioteket från Asposes webbplats, [här](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}