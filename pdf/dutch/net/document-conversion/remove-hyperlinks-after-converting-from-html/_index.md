---
"description": "Leer in deze stapsgewijze handleiding hoe u hyperlinks uit HTML-documenten verwijdert na conversie naar PDF met Aspose.PDF voor .NET."
"linktitle": "Hyperlinks verwijderen na conversie van HTML"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Hyperlinks verwijderen na conversie van HTML"
"url": "/nl/net/document-conversion/remove-hyperlinks-after-converting-from-html/"
"weight": 250
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Hyperlinks verwijderen na conversie van HTML

## Invoering

In het digitale tijdperk is het converteren van HTML-documenten naar PDF een veelvoorkomende taak. Soms wilt u echter om verschillende redenen hyperlinks uit de geconverteerde PDF verwijderen, bijvoorbeeld om de leesbaarheid te verbeteren of ongewenste navigatie te voorkomen. In deze tutorial leggen we uit hoe u dit kunt doen met Aspose.PDF voor .NET. 

## Vereisten

Voordat u aan de slag gaat met de code, moet u ervoor zorgen dat u aan de volgende vereisten voldoet:

1. Visual Studio: Zorg ervoor dat Visual Studio op uw computer is geïnstalleerd. Dit wordt uw ontwikkelomgeving.
2. Aspose.PDF voor .NET: U hebt de Aspose.PDF-bibliotheek nodig. U kunt deze downloaden van [hier](https://releases.aspose.com/pdf/net/).
3. Basiskennis van C#: Kennis van C#-programmering helpt u de code beter te begrijpen.

## Pakketten importeren

Om te beginnen moet je de benodigde pakketten in je C#-project importeren. Zo doe je dat:

1. Open uw Visual Studio-project.
2. Klik met de rechtermuisknop op uw project in Solution Explorer en selecteer 'NuGet-pakketten beheren'.
3. Zoeken naar `Aspose.PDF` en installeer het.

```csharp
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
using System.IO;
```

Nu u alles hebt ingesteld, gaan we dieper in op het proces voor het verwijderen van hyperlinks uit een HTML-bestand nadat u het bestand naar PDF hebt geconverteerd.

## Stap 1: De documentenmap instellen

Allereerst moet u het pad naar uw documentenmap opgeven. Dit is waar uw HTML-bestand zich bevindt en waar de PDF-uitvoer wordt opgeslagen.

```csharp
// Het pad naar de documentenmap.
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Vervangen `"YOUR DOCUMENT DIRECTORY"` met het werkelijke pad waar uw HTML-bestand is opgeslagen.

## Stap 2: Laad het HTML-document

Vervolgens laadt u het HTML-document met behulp van de `Document` klasse van Aspose.PDF. Met deze klasse kunt u eenvoudig met PDF-documenten werken.

```csharp
Document doc = new Document(dataDir + "SampleHtmlFile.html", new HtmlLoadOptions());
```

Hier laden we het HTML-bestand met de naam `SampleHtmlFile.html`Zorg ervoor dat dit bestand in de opgegeven directory staat.

## Stap 3: Sla het document op in de geheugenstroom

Voordat we beginnen met het verwerken van de annotaties, moeten we het document opslaan in een geheugenstroom. Deze stap is cruciaal omdat het het document voorbereidt op verdere bewerking.

```csharp
doc.Save(new MemoryStream());
```

Met deze regel wordt het document in het geheugen opgeslagen, zodat we ermee kunnen werken zonder dat we het eerst naar schijf hoeven te schrijven.

## Stap 4: Door annotaties itereren

Nu gaan we de annotaties in het document doorlopen. Annotaties zijn elementen zoals links, opmerkingen en markeringen. We zijn specifiek geïnteresseerd in linkannotaties.

```csharp
foreach (Annotation a in doc.Pages[1].Annotations)
{
    if (a.AnnotationType == AnnotationType.Link)
    {
        // Verwerk de linkannotatie
    }
}
```

In deze lus controleren we of het annotatietype een link is. Zo ja, dan gaan we verder met de volgende stappen.

## Stap 5: De hyperlinkactie verwijderen

Voor elke linkannotatie moeten we controleren of deze een hyperlinkactie heeft. Zo ja, dan verwijderen we de hyperlink door de URI in te stellen op een lege string.

```csharp
LinkAnnotation la = (LinkAnnotation)a;
if (la.Action is GoToURIAction)
{
    GoToURIAction gta = (GoToURIAction)la.Action;
    gta.URI = "";
```

Met dit codefragment wordt ervoor gezorgd dat de hyperlinkactie effectief wordt verwijderd.

## Stap 6: Tekstfragmenten absorberen

Vervolgens verwerken we de tekstfragmenten die bij de linkannotatie horen. Dit stelt ons in staat om de tekstweergave te manipuleren.

```csharp
TextFragmentAbsorber tfa = new TextFragmentAbsorber();
tfa.TextSearchOptions = new TextSearchOptions(a.Rect);
doc.Pages[a.PageIndex].Accept(tfa);
```

Hier creëren we een `TextFragmentAbsorber` en stel de zoekopties in op de rechthoek van de annotatie. Dit helpt ons de gekoppelde tekst te vinden.

## Stap 7: Wijzig de tekstweergave

Zodra we de tekstfragmenten hebben, kunnen we hun weergave aanpassen. In dit geval verwijderen we de onderstreping en veranderen we de tekstkleur naar zwart.

```csharp
foreach (TextFragment tf in tfa.TextFragments)
{
    tf.TextState.Underline = false;
    tf.TextState.ForegroundColor = Color.Black;
}
```

Met deze stap wordt de leesbaarheid van de tekst verbeterd door de hyperlinkstijl te verwijderen.

## Stap 8: Verwijder de annotatie

Nadat we de tekst hebben aangepast, kunnen we de linkannotatie veilig uit het document verwijderen.

```csharp
doc.Pages[a.PageIndex].Annotations.Delete(a);
}
```

Met deze regel verwijdert u de hyperlink uit het PDF-bestand, zodat deze niet meer in de uiteindelijke uitvoer aanwezig is.

## Stap 9: Sla het gewijzigde document op

Ten slotte moeten we het gewijzigde document opslaan als een nieuw PDF-bestand. Dit is de laatste stap in ons proces.

```csharp
doc.Save(dataDir + "RemoveHyperlinksFromText_out.pdf");
```

Met deze regel wordt het document opgeslagen met de hyperlinks verwijderd, waardoor een nieuw PDF-bestand met de naam wordt gemaakt `RemoveHyperlinksFromText_out.pdf`.

## Conclusie

En voilà! Je hebt met succes hyperlinks uit een HTML-document verwijderd na conversie naar PDF met Aspose.PDF voor .NET. Dit proces verbetert niet alleen de leesbaarheid van je PDF, maar geeft je ook controle over de inhoud die je presenteert. 

## Veelgestelde vragen

### Kan ik hyperlinks uit elk PDF-document verwijderen?
Ja, u kunt hyperlinks uit elk PDF-document verwijderen met Aspose.PDF voor .NET.

### Is Aspose.PDF gratis te gebruiken?
Aspose.PDF biedt een gratis proefperiode, maar voor alle functies moet u een licentie aanschaffen. Bekijk de [kooppagina](https://purchase.aspose.com/buy).

### Wat moet ik doen als ik problemen ondervind bij het gebruik van Aspose.PDF?
U kunt hulp zoeken op de [ondersteuningsforum](https://forum.aspose.com/c/pdf/10).

### Kan ik andere bestandsformaten met Aspose naar PDF converteren?
Ja, Aspose ondersteunt verschillende bestandsformaten voor conversie naar PDF.

### Waar kan ik Aspose.PDF voor .NET downloaden?
Je kunt het downloaden van de [downloadlink](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}