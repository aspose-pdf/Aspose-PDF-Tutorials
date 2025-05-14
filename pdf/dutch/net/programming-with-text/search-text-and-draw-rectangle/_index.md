---
"description": "Leer hoe je tekst in PDF's kunt zoeken en markeren met rechthoeken met Aspose.PDF voor .NET! Eenvoudige stapsgewijze handleiding voor verbeterde PDF-bewerkingsvaardigheden."
"linktitle": "Zoek tekst en teken rechthoek"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Zoek tekst en teken rechthoek"
"url": "/nl/net/programming-with-text/search-text-and-draw-rectangle/"
"weight": 460
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Zoek tekst en teken rechthoek

## Invoering

Wil je je vaardigheden in PDF-bewerking verbeteren? Wil je leren hoe je specifieke tekst in PDF-bestanden kunt zoeken en deze met een rechthoek kunt markeren? Dan heb je de perfecte gids gevonden! Vandaag laat ik je zien hoe je Aspose.PDF voor .NET kunt gebruiken om naar tekst in een PDF-document te zoeken en er rechthoeken omheen te tekenen. Dit artikel biedt een stapsgewijze handleiding die is ontworpen met duidelijkheid en bruikbaarheid in gedachten, zodat je deze technieken kunt volgen en toepassen op je projecten. 

## Vereisten

Voordat we met de tutorial beginnen, bereiden we voor wat je nodig hebt om een soepele workflow te garanderen:

1. Basiskennis van .NET: U dient bekend te zijn met C#-programmering en het .NET Framework om deze tutorial effectief te kunnen volgen.
   
2. Visual Studio geïnstalleerd: Je hebt een Integrated Development Environment (IDE) nodig om je code te schrijven en te testen. Visual Studio Community is een geweldige optie, en het is gratis.
   
3. Aspose.PDF voor .NET: U moet de Aspose.PDF-bibliotheek in uw project geïnstalleerd hebben. U kunt deze downloaden. [hier](https://releases.aspose.com/pdf/net/) of overweeg een [tijdelijke licentie](https://purchase.aspose.com/temporary-license/) voor uitgebreide functies.
   
4. Voorbeeld PDF-document: Voor deze tutorial hebt u een voorbeeld PDF-bestand nodig met de naam `SearchAndGetTextFromAll.pdf` opgeslagen in uw projectmap. 

## Pakketten importeren

Om te beginnen, moet u eerst de benodigde pakketten in uw .NET-project importeren. Volg deze stappen:

### Visual Studio openen

Start Visual Studio en maak een nieuwe consoletoepassing of gebruik een bestaande consoletoepassing waarin u de PDF-functionaliteiten wilt implementeren.

### Voeg Aspose.PDF toe aan uw project

1. Klik met de rechtermuisknop op uw project in Solution Explorer.
2. Selecteer 'NuGet-pakketten beheren'.
3. Zoeken naar `Aspose.PDF` en installeer de nieuwste versie.

Als u dit doet, legt u de basis voor alle fantastische PDF-bewerkingen die u gaat uitvoeren.

## Naamruimten importeren

Bovenaan uw programmabestand wilt u de relevante naamruimten uit de Aspose-bibliotheek importeren:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
using Aspose.Pdf.Facades;
```

Hierdoor hebt u eenvoudiger toegang tot klassen en methoden in de Aspose.PDF-bibliotheek voor uw taken.


Nu u alles hebt ingesteld, kunnen we het proces van het zoeken naar tekst in een PDF en het tekenen van een rechthoek eromheen opsplitsen in beheersbare stappen.

## Stap 1: Stel het pad voor uw document in

Stel eerst het pad naar uw PDF-bestand in. Zorg ervoor dat u `YOUR DOCUMENT DIRECTORY` met het werkelijke pad waar je `SearchAndGetTextFromAll.pdf` wordt opgeslagen.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

## Stap 2: Open het PDF-document

Maak vervolgens een exemplaar van de `Document` klasse om uw PDF te laden:

```csharp
Document document = new Document(dataDir + "SearchAndGetTextFromAll.pdf");
```

Met deze regel code opent u het door u opgegeven PDF-bestand, zodat u het verder kunt bewerken.

## Stap 3: Maak een tekstabsorber

Nu heb je een manier nodig om naar tekst in dat document te zoeken. Hiervoor gebruiken we de `TextFragmentAbsorber`:

```csharp
TextFragmentAbsorber textAbsorber = new TextFragmentAbsorber(@"[\S]+");
```

De reguliere expressie `@"[\S]+"` is ontworpen om elke tekenreeks zonder spaties in het PDF-bestand te matchen. 

## Stap 4: Configureer tekstzoekopties

Vervolgens moet u de opties voor het zoeken in tekst instellen:

```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions(true);
textAbsorber.TextSearchOptions = textSearchOptions;
```

Hier, de `true` parameter betekent dat de zoekopdracht hoofdlettergevoelig is. U kunt dit instellen op `false` als u een hoofdletterongevoelige zoekopdracht wilt.

## Stap 5: Accepteer de tekstabsorber in het document

Met jouw `TextFragmentAbsorber` en de zoekopties gereed zijn, is het tijd om de tekst uit het document op te nemen:

```csharp
document.Pages.Accept(textAbsorber);
```

Met deze methode wordt elke pagina in uw PDF onderzocht om tekstfragmenten te vinden die voldoen aan het opgegeven patroon.

## Stap 6: Een PDF-inhoudseditor maken

Om vormen op het document te tekenen, hebt u de volgende hulpmiddelen nodig: `PdfContentEditor`:

```csharp
var editor = new PdfContentEditor(document);
```

Met deze editor kunt u de inhoud van een PDF eenvoudig bewerken.

## Stap 7: Loop door gevonden tekstfragmenten

Nu wilt u door de gevonden tekstfragmenten heen lopen om er rechthoeken omheen te tekenen:

```csharp
foreach (TextFragment textFragment in textAbsorber.TextFragments)
{
    foreach (TextSegment textSegment in textFragment.Segments)
    {
        DrawBox(editor, textFragment.Page.Number, textSegment, System.Drawing.Color.Red);
    }
}
```

Deze lus itereert over elk tekstfragment en hun segmenten en roept een `DrawBox` Methode voor het tekenen van rechthoeken.

## Stap 8: Definieer de DrawBox-methode

Je moet de `DrawBox` Methode die de logica voor het tekenen van rechthoeken afhandelt. Hier is een eenvoudige implementatie:

```csharp
private static void DrawBox(PdfContentEditor editor, int pageNumber, TextSegment textSegment, System.Drawing.Color color)
{
    // Bereken de afmetingen van de rechthoek op basis van het tekstsegment
    float x = textSegment.Rectangle.LLX;
    float y = textSegment.Rectangle.LLY;
    float width = textSegment.Rectangle.Width;
    float height = textSegment.Rectangle.Height;

    // Teken een rechthoek met behulp van de berekende waarden
    editor.DrawRectangle(pageNumber, x, y, width, height, color, 1);
}
```

Met deze methode worden de positie en de grootte van de rechthoek bepaald op basis van de begrenzende rechthoek van het segment en wordt de editor gebruikt om de rechthoek te tekenen.

## Stap 9: Sla het gewijzigde document op

Nadat u de rechthoeken rond de gevonden tekst hebt getekend, kunt u het gewijzigde document opslaan:

```csharp
dataDir = dataDir + "SearchTextAndDrawRectangle_out.pdf";
document.Save(dataDir);
```

Zorg ervoor dat u het nieuwe bestand met een unieke naam opslaat, om te voorkomen dat uw oorspronkelijke document wordt overschreven.

## Stap 10: Bevestigingsbericht

Druk ten slotte een bevestigingsbericht af op de console om u te laten weten dat de bewerking is geslaagd:

```csharp
Console.WriteLine("\nRectangle drawn successfully on searched text.\nFile saved at " + dataDir);
```

En voilà! Je hebt met succes een script gemaakt om tekst in een PDF te zoeken en te markeren met rechthoeken.

## Conclusie

Gefeliciteerd! Je hebt zojuist een krachtige vaardigheid ontgrendeld die je PDF-bewerkingsmogelijkheden aanzienlijk zal verbeteren met Aspose.PDF voor .NET. Met slechts een paar eenvoudige stappen kun je naar tekst in je document zoeken en deze visueel markeren, waardoor je PDF-documenten interactiever en beter beheerbaar worden. Experimenteer gerust met verschillende regex-patronen en kleuropties om deze tool echt helemaal naar je eigen hand te zetten!

## Veelgestelde vragen

### Wat is Aspose.PDF voor .NET?
Aspose.PDF voor .NET is een bibliotheek die een uitgebreide manier biedt om PDF-documenten programmatisch te maken, te bewerken en te converteren.

### Kan ik Aspose.PDF gratis gebruiken?
Ja, Aspose biedt een gratis proefperiode aan waarmee u de functionaliteiten van de bibliotheek kunt testen. Bekijk het eens. [hier](https://releases.aspose.com/).

### Welke programmeertaal moet ik gebruiken met Aspose.PDF voor .NET?
Aspose.PDF voor .NET is ontworpen voor gebruik met C# en andere .NET-talen.

### Hoe krijg ik hulp met Aspose.PDF?
kunt het Aspose-ondersteuningsforum bezoeken voor hulp bij elk probleem of elke vraag die u heeft. Vind ondersteuning [hier](https://forum.aspose.com/c/pdf/10).

### Waar kan ik Aspose.PDF voor .NET downloaden?
U kunt de bibliotheek downloaden van de Aspose-website, [hier](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}