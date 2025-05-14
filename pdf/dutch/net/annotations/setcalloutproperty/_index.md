---
"description": "Leer hoe u de callout-eigenschap in een PDF-bestand instelt met Aspose.PDF voor .NET in deze gedetailleerde, stapsgewijze zelfstudie."
"linktitle": "Callout-eigenschap instellen in PDF-bestand"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Callout-eigenschap instellen in PDF-bestand"
"url": "/nl/net/annotations/setcalloutproperty/"
"weight": 130
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Callout-eigenschap instellen in PDF-bestand

## Invoering

Het creëren van professionele en visueel aantrekkelijke PDF-documenten vereist vaak het toevoegen van annotaties die de aandacht vestigen op specifieke inhoud. Een voorbeeld van zo'n annotatie is de callout, vergelijkbaar met de tekstballonnen die je in stripverhalen ziet. Ze helpen tekst in je PDF te verduidelijken of te benadrukken. Aspose.PDF voor .NET maakt het ongelooflijk eenvoudig om dergelijke annotaties aan je documenten toe te voegen. In deze tutorial laten we zien hoe je de callout-eigenschap in een PDF-bestand instelt met behulp van deze krachtige bibliotheek. Of je nu een ervaren ontwikkelaar bent of net begint, aan het einde van deze handleiding heb je een duidelijk begrip van hoe je met callouts in PDF-bestanden kunt werken.

## Vereisten

Voordat we in de code duiken, leggen we eerst de basisprincipes uit die je nodig hebt om aan de slag te gaan.

1. Aspose.PDF voor .NET: Zorg ervoor dat u de Aspose.PDF voor .NET-bibliotheek hebt geïnstalleerd. U kunt deze downloaden van [hier](https://releases.aspose.com/pdf/net/).
2. IDE: Een ontwikkelomgeving zoals Visual Studio.
3. .NET Framework: zorg ervoor dat .NET op uw computer is geïnstalleerd.
4. Tijdelijke licentie: Als u de volledige functies van Aspose.PDF zonder beperkingen wilt uitproberen, koop dan een [tijdelijke licentie](https://purchase.aspose.com/temporary-license/).

## Pakketten importeren

Voordat u begint met het schrijven van de code, moet u de benodigde pakketten importeren waarmee u met PDF-bestanden en annotaties kunt werken.

```csharp
using Aspose.Pdf.Annotations;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
```

Met deze imports krijgt u de beschikking over alle benodigde klassen en methoden om PDF-documenten te bewerken en aantekeningen te maken, zoals de callout.

## Stap 1: Initialiseer het PDF-document

De eerste stap in onze reis is het initialiseren van een nieuw PDF-document waaraan we onze callout-annotatie toevoegen. Zie dit als het opzetten van een leeg canvas waar je elementen kunt toevoegen.

```csharp
// Het pad naar de documentenmap.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Een nieuw PDF-document initialiseren
Document doc = new Document();
```
Hier creëren we een nieuwe `Document` object dat zal dienen als ons PDF-bestand. De `dataDir` variabele wordt ingesteld op de map waar u uw PDF-bestand wilt opslaan nadat we klaar zijn.

## Stap 2: Een nieuwe pagina toevoegen aan het document

Een PDF-document kan meerdere pagina's bevatten. In deze stap voegen we een nieuwe pagina aan ons document toe. Op deze pagina wordt onze callout-annotatie geplaatst.

```csharp
// Een nieuwe pagina aan het document toevoegen
Page page = doc.Pages.Add();
```
De `Pages.Add()` methode wordt gebruikt om een nieuwe pagina toe te voegen aan de `doc` object. De nieuwe pagina wordt opgeslagen in de `page` variabele, die we later zullen gebruiken bij het toevoegen van de annotatie.

## Stap 3: Definieer het standaarduiterlijk

Annotaties hebben, net als de callout, een visuele weergave die u kunt aanpassen. In deze stap definiëren we hoe de tekst in de callout eruit moet zien.

```csharp
// Definieer het standaarduiterlijk voor de annotatie
DefaultAppearance da = new DefaultAppearance();
da.TextColor = System.Drawing.Color.Red;
da.FontSize = 10;
```
Wij creëren een `DefaultAppearance` Object dat de tekstkleur en lettergrootte definieert. Hier is de tekst rood en is de lettergrootte ingesteld op 10. Deze weergave wordt toegepast op de callout-annotatie.

## Stap 4: Maak de vrije tekstannotatie

Nu is het tijd om de annotatie zelf te maken. Met de vrije-tekstannotatie kunnen we een tekstballon met specifieke tekst en stijl toevoegen.

```csharp
// Maak een FreeTextAnnotation met een callout
FreeTextAnnotation fta = new FreeTextAnnotation(page, new Rectangle(422.25, 645.75, 583.5, 702.75), da);
fta.Intent = FreeTextIntent.FreeTextCallout;
fta.EndingStyle = LineEnding.OpenArrow;
```
Wij creëren een `FreeTextAnnotation` object met specifieke coördinaten, die de positie ervan op de pagina definiëren. `Intent` is ingesteld op `FreeTextCallout`, wat aangeeft dat dit een callout-annotatie is. De `EndingStyle` is ingesteld op `OpenArrow`, wat betekent dat de callout-regel eindigt met een open pijl.

## Stap 5: Definieer de callout-lijnpunten

Een callout-annotatie heeft een lijn die naar het interessegebied wijst. Hier definiëren we de punten waaruit deze lijn bestaat.

```csharp
// Definieer de punten voor de callout-lijn
fta.Callout = new Point[]
{
    new Point(428.25, 651.75), 
    new Point(462.75, 681.375), 
    new Point(474, 681.375)
};
```
De `Callout` eigenschap is een reeks van `Point` Objecten, die elk een coördinaat op de pagina vertegenwoordigen. Deze punten definiëren het pad van de tekstregel, waardoor deze de klassieke tekstballonvorm krijgt.

## Stap 6: Voeg de annotatie toe aan de pagina

Nadat u uw annotatie hebt gemaakt en geconfigureerd, voegt u deze toe aan de pagina.

```csharp
// Voeg de annotatie toe aan de pagina
page.Annotations.Add(fta);
```
De `Annotations.Add()` Deze methode wordt gebruikt om de annotatie te plaatsen op de pagina die we eerder hebben gemaakt. Deze stap "tekent" de toelichting effectief op de PDF-pagina.

## Stap 7: Stel de inhoud van de Rich Text in

Callout-annotaties kunnen rich text bevatten, wat opgemaakte inhoud binnen de tekstballon mogelijk maakt. Laten we wat voorbeeldtekst toevoegen.

```csharp
// Stel de rijke tekst voor de annotatie in
fta.RichText = "<body xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:xfa=\"http://www.xfa.org/schema/xfa-data/1.0/\" xfa:APIVersion=\"Acrobat:11.0.23\" xfa:spec=\"2.0.2\" style=\"color:#FF0000;font-weight:normal;font-style:normal;font-stretch:normal\"><p dir=\"ltr\"><span style=\"font-size:9.0pt;font-family:Helvetica\">Dit is een voorbeeld</span></p></body>";
```
De `RichText` De eigenschap wordt ingesteld met HTML-inhoud. Dit maakt gedetailleerde opmaak in de callout mogelijk, zoals het specificeren van lettergrootte, kleur en stijl.

## Stap 8: Sla het PDF-document op

Nadat we alles hebben ingesteld, moeten we het document opslaan. Deze stap voltooit het aanmaken van de PDF met de callout-annotatie.

```csharp
// Sla het document op
doc.Save(dataDir + "SetCalloutProperty.pdf");
```
De `Save()` Deze methode slaat het document op in de opgegeven directory met de bestandsnaam "SetCalloutProperty.pdf". Deze stap rondt ons PDF-creatieproces af.

## Conclusie

En voilà! Je hebt zojuist een PDF-document gemaakt met een callout-annotatie met Aspose.PDF voor .NET. Deze annotatie kan ontzettend handig zijn om specifieke delen van je document te markeren of toe te lichten. Aspose.PDF biedt een krachtige API die PDF-bewerking eenvoudig en flexibel maakt. Of je nu annotaties toevoegt, documenten converteert of complexe PDF-taken uitvoert, Aspose.PDF helpt je daarbij.

## Veelgestelde vragen

### Kan ik het uiterlijk van de callout verder aanpassen?

Absoluut! Je kunt verschillende aspecten aanpassen, zoals de kleur van de lijnen, de dikte en het lettertype en de stijl van de tekst.

### Is het mogelijk om meerdere callouts op één pagina toe te voegen?

Ja, u kunt zoveel callouts toevoegen als nodig is door de stappen voor elke annotatie te herhalen.

### Hoe verander ik de positie van de callout?

Wijzig eenvoudig de coördinaten in de `Rectangle` En `Callout` Eigenschappen om de annotatie opnieuw te positioneren.

### Kan ik andere soorten annotaties toevoegen met Aspose.PDF?

Ja, Aspose.PDF ondersteunt verschillende soorten annotaties, waaronder markeringen, stempels en bestandsbijlagen.

### Is de rich text-inhoud beperkt tot HTML?

De `RichText` De eigenschap ondersteunt een subset van HTML, zodat u opgemaakte tekst en basisopmaak kunt opnemen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}