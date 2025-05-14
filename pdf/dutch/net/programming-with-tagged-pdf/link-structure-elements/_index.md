---
"description": "Leer hoe u linkstructuurelementen in een PDF maakt met Aspose.PDF voor .NET. Stapsgewijze handleiding voor het toevoegen van toegankelijke links, afbeeldingen en nalevingsvalidatie."
"linktitle": "Linkstructuurelementen"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Linkstructuurelementen"
"url": "/nl/net/programming-with-tagged-pdf/link-structure-elements/"
"weight": 120
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Linkstructuurelementen

## Invoering

Het creëren en beheren van linkstructuurelementen in een PDF kan cruciaal zijn voor documenten die toegankelijkheid en soepele navigatie vereisen. In deze tutorial laten we je zien hoe je dit kunt doen met Aspose.PDF voor .NET. Als je nieuw bent met Aspose.PDF of PDF-bewerking in het algemeen, maak je dan geen zorgen. Ik leg elke stap gedetailleerd uit, zodat je het gemakkelijk kunt volgen!

## Vereisten  

Voordat we in de code duiken, willen we eerst een paar dingen duidelijk maken. Dit zijn de basisvereisten voor een soepele ontwikkelervaring.

1. Aspose.PDF voor .NET: U kunt de nieuwste versie downloaden [hier](https://releases.aspose.com/pdf/net/).
2. .NET-ontwikkelomgeving: Zorg dat het geïnstalleerd en klaar voor gebruik is, ongeacht of het Visual Studio of een .NET-compatibele IDE is.
3. Aspose-licentie: U kunt de gratis proefversie van Aspose.PDF gebruiken [hier](https://releases.aspose.com/) of een [tijdelijke licentie](https://purchase.aspose.com/temporary-license/).
4. Basiskennis van C#: We gaan met C#-code werken, dus als je de basisbeginselen begrijpt, wordt het een stuk makkelijker.

## Pakketten importeren

Je moet een paar pakketten importeren voordat je de code voor linkstructuurelementen schrijft. Begin met het verwijzen naar de benodigde Aspose.PDF-bibliotheken in je project:

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Dankzij deze imports kunnen we met PDF-documenten werken, tags toevoegen en structuurelementen beheren.

We gaan nu een PDF-document maken met verschillende soorten linkstructuren. Elke stap wordt uitgelegd, zodat u het proces beter begrijpt.

## Stap 1: Initialiseer het document  

Laten we beginnen met het maken van een nieuw PDF-document en het instellen van getagde inhoud voor toegankelijkheid.

```csharp
// Het pad naar de documentenmap.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "LinkStructureElements_Output.pdf";
string logFile = dataDir + "46035_log.xml";
string imgFile = dataDir + "google-icon-512.png";

// Een nieuw PDF-document maken
Document document = new Document(); 

// De TaggedContent-interface ophalen
ITaggedContent taggedContent = document.TaggedContent;
```
  
Hier initialiseren we de `Document` object, dat ons PDF-bestand vertegenwoordigt. We halen ook de `TaggedContent` interface, waarmee we structuurelementen zoals alinea's, links en afbeeldingen kunnen toevoegen.

## Stap 2: Titel en taal instellen  

Elk PDF-bestand moet een titel en taalinstelling hebben, vooral als u wilt voldoen aan de PDF-/UA-standaarden.

```csharp
// Stel de documenttitel en taal in
taggedContent.SetTitle("Link Elements Example");
taggedContent.SetLanguage("en-US");
```
  
Met deze stap zorgt u ervoor dat uw PDF een betekenisvolle titel heeft en wordt de taal ingesteld op Engels (`en-US`). Dit is essentieel voor de toegankelijkheid en zorgt ervoor dat schermlezers of andere ondersteunende technologieën uw document correct kunnen interpreteren.

## Stap 3: Alinea's maken en toevoegen  

In deze stap voegen we alinea's toe om de linkelementen in te plaatsen.

```csharp
// Het rootelement aanmaken
StructureElement rootElement = taggedContent.RootElement;

// Maak een alinea en voeg deze toe aan het root-element
ParagraphElement p1 = taggedContent.CreateParagraphElement();
rootElement.AppendChild(p1);
```
  
We creëren een rootstructuurelement, dat in wezen de bovenste container is voor alle andere elementen. Vervolgens maken we een alinea (`p1`) en voeg het toe aan het rootelement.

## Stap 4: Een eenvoudige link toevoegen  

Laten we nu een eenvoudige hyperlink toevoegen die naar Google verwijst.

```csharp
// Maak een linkelement en voeg het toe aan de alinea
LinkElement link1 = taggedContent.CreateLinkElement();
p1.AppendChild(link1);

// Stel een hyperlink en tekst voor de link in
link1.Hyperlink = new WebHyperlink("http://google.com");
link1.SetText("Google");
link1.AlternateDescriptions = "Link to Google";
```
  
In deze stap hebben we een linkelement gemaakt, de hyperlink ingesteld op "http://google.com" en tekst ("Google") voor de link toegevoegd. We hebben ook een alternatieve beschrijving toegevoegd om de toegankelijkheid te garanderen.

## Stap 5: Een link toevoegen met overspanningen  

We kunnen ook links maken met verschillende tekstgedeeltes.

```csharp
// Maak een nieuwe alinea
ParagraphElement p2 = taggedContent.CreateParagraphElement();
rootElement.AppendChild(p2);

// Een link maken met een span-element
LinkElement link2 = taggedContent.CreateLinkElement();
p2.AppendChild(link2);
link2.Hyperlink = new WebHyperlink("http://google.com");

SpanElement span2 = taggedContent.CreateSpanElement();
span2.SetText("Google");
link2.AppendChild(span2);

link2.AlternateDescriptions = "Link to Google";
```
  
Hier hebben we een span-element gebruikt om een deel van de tekst binnen de link te omsluiten. Zo kunnen we aanpassen hoe bepaalde delen van de link worden weergegeven.

## Stap 6: Multiline-koppeling  

Wat als je linktekst te lang is? Geen zorgen, je kunt hem over meerdere regels verdelen.

```csharp
ParagraphElement p4 = taggedContent.CreateParagraphElement();
rootElement.AppendChild(p4);

LinkElement link4 = taggedContent.CreateLinkElement();
p4.AppendChild(link4);
link4.Hyperlink = new WebHyperlink("http://google.com");
link4.SetText("The multiline link: Google Google Google Google Google...");
link4.AlternateDescriptions = "Link to Google (multiline)";
```
  
In dit geval hebben we een link met meerdere regels gemaakt door simpelweg een lange tekstwaarde in te stellen. De tekst wordt nu automatisch over meerdere regels verdeeld.

## Stap 7: Voeg een afbeelding toe aan de link  

Ten slotte kunt u ook afbeeldingen aan een link toevoegen.

```csharp
// Een nieuwe alinea en een linkelement maken
ParagraphElement p5 = taggedContent.CreateParagraphElement();
rootElement.AppendChild(p5);

LinkElement link5 = taggedContent.CreateLinkElement();
p5.AppendChild(link5);
link5.Hyperlink = new WebHyperlink("http://google.com");

// Voeg een afbeelding toe aan de link
FigureElement figure5 = taggedContent.CreateFigureElement();
figure5.SetImage(imgFile, 1200);
figure5.AlternativeText = "Google icon";
link5.AppendChild(figure5);

link5.AlternateDescriptions = "Link to Google";
```
  
Deze stap laat zien hoe je je links kunt verbeteren met een afbeelding. In dit geval hebben we een Google-icoontje aan de link toegevoegd. We hebben de toegankelijkheid ook gewaarborgd door alternatieve tekst voor de afbeelding in te stellen.

## Stap 8: PDF valideren op naleving  

Als u PDF/UA-compatibel wilt zijn (een toegankelijkheidsstandaard), is het een goed idee om uw document te valideren.

```csharp
// Sla het PDF-document op
document.Save(outFile);

// Valideer het document op PDF/UA-compatibiliteit
bool isPdfUaCompliance = document.Validate(logFile, PdfFormat.PDF_UA_1);
Console.WriteLine($"PDF/UA compliance: {isPdfUaCompliance}");
```
  
We hebben het document opgeslagen en gevalideerd aan de hand van de PDF/UA-standaard. Dit garandeert dat de PDF voldoet aan de toegankelijkheidsvereisten.

## Conclusie  

In deze tutorial hebben we behandeld hoe je gestructureerde PDF-documenten maakt met Aspose.PDF voor .NET. Van het toevoegen van eenvoudige hyperlinks tot complexere structuren zoals spans, meerregelige links en zelfs afbeeldingen: deze handleiding biedt een solide basis voor het bewerken van linkelementen in je PDF's. Met het extra voordeel van PDF/UA-compatibiliteit ben je nu klaar om toegankelijke en navigeerbare PDF's te maken.

## Veelgestelde vragen

### Kan ik complexere structuren zoals tabellen binnen links toevoegen?  
Nee, links zijn voornamelijk bedoeld voor tekst en afbeeldingen, maar u kunt er complexe elementen in opnemen.

### Is PDF/UA-validatie verplicht?  
Niet altijd, maar het is zeker aan te raden als u bezorgd bent over de toegankelijkheid.

### Wat gebeurt er als het pad naar het afbeeldingsbestand onjuist is?  
De afbeelding wordt niet weergegeven in het document en er kan een fout optreden tijdens het renderen.

### Kan ik de tekst in de link opmaken?  
Ja, u kunt tekststijlen toepassen met behulp van de span-elementen.

### Is het mogelijk om interne documentlinks te maken?  
Absoluut! Je kunt naar specifieke secties binnen hetzelfde document linken.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}