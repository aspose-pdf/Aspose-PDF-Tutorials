---
"description": "Lär dig hur du stryker över ord i en PDF med Aspose.PDF för .NET med den här omfattande steg-för-steg-guiden. Förbättra dina dokumentredigeringsfärdigheter."
"linktitle": "Stryk ut ord"
"second_title": "Aspose.PDF för .NET API-referens"
"title": "Stryk ut ord"
"url": "/sv/net/annotations/strikeoutwords/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Stryk ut ord

## Introduktion

Har du någonsin behövt betona specifik text i en PDF genom att stryka över den? Oavsett om du granskar dokument, markerar text eller helt enkelt behöver markera vissa avsnitt kan strykning av ord vara ett värdefullt verktyg. I den här handledningen utforskar vi hur du gör just det med Aspose.PDF för .NET. Den här omfattande guiden guidar dig genom varje steg och säkerställer att du har all information som behövs för att effektivt implementera den här funktionen i dina .NET-applikationer. 

## Förkunskapskrav

Innan vi går in i koden finns det några förutsättningar du måste uppfylla för att följa den här handledningen:

1. Aspose.PDF för .NET-biblioteket: Se till att du har Aspose.PDF för .NET-biblioteket installerat. Du kan [ladda ner den här](https://releases.aspose.com/pdf/net/).

2. .NET Framework: Se till att du har .NET Framework installerat på din dator. Den här handledningen är utformad för .NET-applikationer.

3. Utvecklingsmiljö: Du behöver en IDE som Visual Studio för att skriva och köra din kod.

4. PDF-dokument: Ha en exempel-PDF-fil redo som du vill arbeta med. Det här är dokumentet där vi stryker över texten.

5. Grundläggande C#-kunskaper: Bekantskap med C#-programmering är nödvändig för att förstå och implementera stegen i den här handledningen.

## Importera paket

Innan vi kan börja koda måste vi importera de nödvändiga namnrymderna i vårt .NET-projekt. Detta ger oss tillgång till de klasser och metoder som krävs för att manipulera PDF-filer med Aspose.PDF.

```csharp
using System;
using System.IO;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
```

Dessa namnrymder är viktiga för att arbeta med PDF-dokument, hantera text och lägga till anteckningar som överstrukna tecken.

I det här avsnittet kommer vi att dela upp processen att stryka ut ord i ett PDF-dokument i enkla, hanterbara steg. Varje steg kommer att åtföljas av en detaljerad förklaring för att säkerställa att du förstår hur allt fungerar.

## Steg 1: Ladda PDF-dokumentet

Det första steget är att ladda PDF-dokumentet som du vill redigera. Det är i det här dokumentet du kommer att stryka över specifika ord eller fraser.

```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Öppna PDF-dokumentet
Document document = new Document(dataDir + "input.pdf");
```

- `dataDir`Den här variabeln innehåller sökvägen till din dokumentkatalog. Ersätt `"YOUR DOCUMENT DIRECTORY"` med den faktiska sökvägen där din PDF-fil finns.
- `Document`: Den `Document` klassen representerar ett PDF-dokument. Genom att skicka sökvägen till dess konstruktor öppnar vi PDF-filen för bearbetning.

## Steg 2: Skapa en TextFragment Absorber för att hitta specifik text

Nästa steg är att skapa en instans av `TextFragmentAbsorber` för att söka efter ett specifikt textfragment i PDF-dokumentet. Detta gör att vi kan hitta den text vi vill stryka över.

```csharp
// Skapa en TextFragment Absorber-instans för att söka efter ett specifikt textfragment
Aspose.Pdf.Text.TextFragmentAbsorber textFragmentAbsorber = new Aspose.Pdf.Text.TextFragmentAbsorber("Estoque");
```

- `TextFragmentAbsorber`Den här klassen används för att hitta och arbeta med specifika textfragment i PDF-dokumentet. I det här exemplet söker vi efter ordet "Estoque". Ersätt "Estoque" med ordet eller frasen du vill hitta i dokumentet.

## Steg 3: Bläddra igenom sidorna i PDF-dokumentet

Nu när vi har våra `TextFragmentAbsorber`, måste vi iterera igenom varje sida i PDF-dokumentet för att hitta den angivna texten.

```csharp
// Iterera genom sidorna i PDF-dokumentet
for (int i = 1; i <= document.Pages.Count; i++)
{
    // Hämta den aktuella sidan i PDF-dokumentet
    Page page = document.Pages[i];
    page.Accept(textFragmentAbsorber);
}
```

- `for (int i = 1; i <= document.Pages.Count; i++)`Denna loop itererar genom varje sida i PDF-dokumentet.
- `document.Pages[i]`Hämtar den aktuella sidan som bearbetas.
- `page.Accept(textFragmentAbsorber)`Den här metoden tillämpar `TextFragmentAbsorber` till den aktuella sidan och söker efter den angivna texten.

## Steg 4: Samla in och bearbeta textfragmenten

Efter att ha itererat igenom sidorna samlar vi in de funna textfragmenten och förbereder dem för vidare bearbetning.

```csharp
// Skapa en samling av absorberade textfragment
Aspose.Pdf.Text.TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- `TextFragmentCollection`Den här samlingen lagrar alla textfragment som hittades i dokumentet. Vi använder den här samlingen i nästa steg för att stryka över texten.

## Steg 5: Gå igenom textfragmenten och stryk ut dem

I det här steget loopar vi igenom varje textfragment i vår samling och tillämpar en utstrykningsanteckning på det.

```csharp
// Iterera över samlingen av textfragment
for (int j = 1; j <= textFragmentCollection.Count; j++)
{
	Aspose.Pdf.Text.TextFragment textFragment = textFragmentCollection[j];

    // Hämta de rektangulära dimensionerna för TextFragment-objektet
    Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(
        (float)textFragment.Position.XIndent,
        (float)textFragment.Position.YIndent,
        (float)textFragment.Position.XIndent + (float)textFragment.Rectangle.Width,
        (float)textFragment.Position.YIndent + (float)textFragment.Rectangle.Height);

    // Instansiera StrikeOut Annotation-instansen
    StrikeOutAnnotation strikeOut = new StrikeOutAnnotation(textFragment.Page, rect);

    // Ange egenskaper för den utstrykta annoteringen
    strikeOut.Opacity = .80f;
    strikeOut.Border = new Border(strikeOut);
    strikeOut.Color = Aspose.Pdf.Color.Red;

    // Lägg till anteckningen i anteckningssamlingen på textfragmentets sida
    textFragment.Page.Annotations.Add(strikeOut);
}
```

- `TextFragment textFragment = textFragmentCollection[j]`Den här raden hämtar det aktuella textfragmentet.
- `Aspose.Pdf.Rectangle`Vi beräknar textfragmentets rektangulära dimensioner för att avgöra var överstrykningen ska appliceras.
- `StrikeOutAnnotation`Den här klassen representerar den utstrykta annoteringen. Vi instansierar den med den beräknade rektangeln och den aktuella sidan.
- `strikeOut.Opacity`Den här egenskapen anger opaciteten för den överstrukna texten, vilket gör den 80 % synlig.
- `strikeOut.Color`Vi har satt färgen på den överstrukna texten till röd. Du kan ändra den till vilken färg du vill.
- `textFragment.Page.Annotations.Add(strikeOut)`Detta lägger till den överstrukna anteckningen på sidan.

## Steg 6: Spara det modifierade PDF-dokumentet

Det sista steget är att spara det modifierade PDF-dokumentet med överstrukningarna tillämpade.

```csharp
// Spara det uppdaterade PDF-dokumentet
dataDir = dataDir + "StrikeOutWords_out.pdf";
document.Save(dataDir);
```

- `dataDir + "StrikeOutWords_out.pdf"`Detta skapar ett nytt filnamn för det ändrade dokumentet. Den ursprungliga filen förblir oförändrad.
- `document.Save(dataDir)`Sparar PDF-dokumentet med överstrukna tecken på den angivna platsen.

## Slutsats

Grattis! Du har lyckats stryka över specifika ord i ett PDF-dokument med Aspose.PDF för .NET. Genom att följa den här steg-för-steg-guiden kan du nu anpassa PDF-dokument genom att markera eller stryka över text, vilket gör dem mer dynamiska och anpassade efter dina behov. Oavsett om du kommenterar juridiska dokument, förbereder rapporter eller bara markerar text för granskning, har den här handledningen utrustat dig med de färdigheter som krävs för att göra det effektivt.

## Vanliga frågor

### Kan jag ändra färgen på den överstrukna texten?

Ja, du kan ändra färgen genom att modifiera `strikeOut.Color` egenskap. Du kan till exempel ställa in den på `Aspose.Pdf.Color.Blue` för en blå strikeout.

### Är det möjligt att stryka ut flera ord samtidigt?

Absolut! Den `TextFragmentAbsorber` kan användas för att söka efter valfritt ord eller fras i dokumentet. Du kan använda överstrukningen på flera förekomster genom att iterera igenom `TextFragmentCollection`.

### Vad händer om jag bara vill stryka över text på specifika sidor?

Du kan ändra loopen som itererar genom sidorna så att den bara inkluderar de sidor du vill ändra. Till exempel, `for (int i = 1; i <= 3; i++)` skulle endast tillämpa överstrykningen på de tre första sidorna.

### Hur kan jag justera tjockleken på den utstrykta linjen?

Du kan justera tjockleken på den överstrukna linjen genom att modifiera `Border` egendomen tillhörande `StrikeOutAnnotation`Detta möjliggör anpassning av utseendet på den överstrukna texten.

### Finns det något sätt att ångra överstrykningen efter att dokumentet har sparats?

När dokumentet har sparats är överstrukningen permanent. Om du behöver behålla originaltexten utan överstrukningen kan du överväga att spara en säkerhetskopia av originaldokumentet innan du gör några ändringar.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}