---
"description": "Leer hoe u afbeeldingen in bestaande PDF's kunt taggen met Aspose.PDF voor .NET. Stapsgewijze handleiding voor het verbeteren van de toegankelijkheid met PDF/UA-compatibiliteit."
"linktitle": "Afbeelding taggen in bestaande PDF"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Afbeelding taggen in bestaande PDF"
"url": "/nl/net/programming-with-tagged-pdf/tag-image-in-existing-pdf/"
"weight": 210
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Afbeelding taggen in bestaande PDF

## Invoering

In deze tutorial laten we je zien hoe je een afbeelding in een bestaande PDF kunt taggen met Aspose.PDF voor .NET. Aan het einde van deze handleiding kun je alternatieve tekst voor afbeeldingen instellen, lay-outkenmerken aanpassen en ervoor zorgen dat je PDF voldoet aan de toegankelijkheidsnormen.

## Vereisten

Voordat we beginnen, leggen we eerst uit wat je nodig hebt om te beginnen:

- Aspose.PDF voor .NET: Zorg ervoor dat u de nieuwste versie van Aspose.PDF voor .NET hebt gedownload en geïnstalleerd. [Download hier](https://releases.aspose.com/pdf/net/).
- .NET Framework: Zorg ervoor dat u een .NET-ontwikkelomgeving zoals Visual Studio hebt ingesteld.
- Basiskennis van de PDF-structuur: kennis van de elementen van de PDF-structuur, zoals alinea's, reeksen, tabellen en afbeeldingen.
- Een geldige licentie: U kunt een licentie kopen [hier](https://purchase.aspose.com/buy) of gebruik een tijdelijke [hier](https://purchase.aspose.com/temporary-license/).

## Pakketten importeren

Om te beginnen met coderen, moet u de essentiële naamruimten uit Aspose.PDF voor .NET importeren. Deze geven u toegang tot de benodigde klassen en methoden om het PDF-document te bewerken.

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Nu we alles hebben uiteengezet, kunnen we het proces van het taggen van een afbeelding opsplitsen in meerdere stappen.

## Stap 1: Het bestaande PDF-document laden

De eerste stap is het laden van het PDF-bestand waarmee u wilt werken. Dit kan elk PDF-bestand zijn met een afbeelding die u wilt taggen.

```csharp
// Het pad naar de documentenmap.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string inFile = dataDir + "TH.pdf";
string outFile = dataDir + "TH_out.pdf";
string logFile = dataDir + "TH_out.xml";

// Open het document
Document document = new Document(inFile);
```

- Vervangen `"YOUR DOCUMENT DIRECTORY"` met het daadwerkelijke pad naar uw bestand.
- De `Document` Met de klasse kun je een bestaande PDF laden. Je gaat deze PDF aanpassen om de afbeelding te taggen.

## Stap 2: Toegang tot getagde inhoud en rootstructuurelement

Nadat u de PDF hebt geopend, is de volgende stap het openen van de getagde content en het identificeren van het root-structuurelement. Dit is cruciaal, omdat u hiermee door de elementen in de PDF kunt navigeren en wijzigingen kunt aanbrengen.

```csharp
// Getagde inhoud en rootstructuurelement ophalen
ITaggedContent taggedContent = document.TaggedContent;
StructureElement rootElement = taggedContent.RootElement;
```

- `TaggedContent` geeft toegang tot de gestructureerde elementen in de PDF.
- De `RootElement` is het bovenste structuurelement, van waaruit u naar andere elementen kunt navigeren, zoals alinea's, tabellen en afbeeldingen.

## Stap 3: Stel de titel in voor het gelabelde PDF-document

Als u een titel toevoegt aan het PDF-document met tags, weet u zeker dat uw document correct is gelabeld. Dit is handig voor de toegankelijkheid en PDF/UA-compatibiliteit.

```csharp
// Titel instellen voor het getagde PDF-document
taggedContent.SetTitle("Document with images");
```

- Door een titel in te stellen voor uw getagde PDF verbetert u de toegankelijkheid en de duidelijkheid van het document voor schermlezers en ondersteunende technologieën.

## Stap 4: Zoek en tag de afbeelding

Laten we nu het beeldelement vinden (ook wel een `FigureElement` in Aspose.PDF), stel een alternatieve tekst hiervoor in en configureer de lay-outkenmerken.

```csharp
// Doorloop alle figuurelementen (afbeeldingen) en stel alternatieve tekst- en lay-outkenmerken in
foreach (FigureElement figureElement in rootElement.FindElements<FigureElement>(true))
{
    // Alternatieve tekst voor de afbeelding instellen
    figureElement.AlternativeText = "Figure alternative text (technique 2)";
    
    // BBox-kenmerk (begrenzende doos) maken en instellen
    StructureAttribute bboxAttribute = new StructureAttribute(AttributeKey.BBox);
    bboxAttribute.SetRectangleValue(new Aspose.Pdf.Rectangle(0.0, 0.0, 100.0, 100.0));
    
    // Lay-outkenmerken voor de figuur instellen
    StructureAttributes figureLayoutAttributes = figureElement.Attributes.GetAttributes(AttributeOwnerStandard.Layout);
    figureLayoutAttributes.SetAttribute(bboxAttribute);
}
```

- Deze code loopt door alle `FigureElement` objecten in de wortelstructuur, die afbeeldingen voorstellen.
- Hiermee wordt de alternatieve tekst voor toegankelijkheid ingesteld (schermlezers gebruiken deze om de afbeelding te beschrijven).
- Het selectiekader (`BBox`) geeft de coördinaten voor de lay-out van de afbeelding op, zodat deze correct in het document wordt weergegeven.

## Stap 5: Span-elementen in de tabel wijzigen

In sommige gevallen moet u mogelijk span-elementen in een tabel aanpassen. Hier laten we zien hoe u een `SpanElement` en verplaats het naar een alinea.

```csharp
// Vind de tabel-, span- en alinea-elementen
TableElement tableElement = rootElement.FindElements<TableElement>(true)[0];
SpanElement spanElement = tableElement.FindElements<SpanElement>(true)[0];
TableTDElement firstTdElement = tableElement.FindElements<TableTDElement>(true)[0];
ParagraphElement paragraph = firstTdElement.FindElements<ParagraphElement>(true)[0];

// Verplaats het span-element naar de alinea
spanElement.ChangeParentElement(paragraph);
```

- Hier vinden we de `TableElement`, `SpanElement`, En `ParagraphElement` in de PDF.
- Met behulp van de `ChangeParentElement` Met deze methode verplaatsen we de spanwijdte naar de alinea om de juiste tagging en structuur te garanderen.

## Stap 6: Sla het document op en valideer de PDF/UA-naleving

Zodra alle wijzigingen zijn doorgevoerd, slaat u als laatste stap de bijgewerkte PDF op en controleert u of deze voldoet aan de PDF/UA-standaarden.

```csharp
// Sla het bijgewerkte PDF-document op
document.Save(outFile);

// Valideer PDF/UA-naleving
document = new Document(outFile);
bool isPdfUaCompliance = document.Validate(logFile, PdfFormat.PDF_UA_1);
Console.WriteLine(String.Format("PDF/UA compliance: {0}", isPdfUaCompliance));
```

- De `Validate` methode controleert het PDF-document aan de hand van PDF/UA-standaarden en registreert de resultaten.
- Door naleving te waarborgen, verbetert u de toegankelijkheid en voldoet u aan de wettelijke vereisten voor het publiceren van documenten.

## Conclusie

In deze tutorial hebben we je laten zien hoe je afbeeldingen in een bestaande PDF kunt taggen met Aspose.PDF voor .NET. Door alternatieve tekst in te stellen, lay-outkenmerken aan te passen en het document te valideren op PDF/UA-compatibiliteit, kun je ervoor zorgen dat je PDF's toegankelijk zijn en voldoen aan moderne standaarden. Aspose.PDF maakt het gemakkelijk om met gestructureerde elementen te werken, waardoor je de controle hebt over de lay-out en toegankelijkheid van je document.

## Veelgestelde vragen

### Waarvoor wordt Aspose.PDF voor .NET gebruikt?
Aspose.PDF voor .NET is een krachtige bibliotheek voor het programmatisch maken, bewerken en manipuleren van PDF-documenten in een .NET-omgeving.

### Hoe zorg ik voor PDF/UA-compatibel?
U kunt Aspose.PDF's gebruiken `Validate` Methode om te controleren of het document PDF/UA-compatibel is nadat er wijzigingen in het document zijn aangebracht.

### Wat is alternatieve tekst in PDF's?
Alternatieve tekst is een beschrijving die aan afbeeldingen in PDF's wordt toegevoegd om de toegankelijkheid te verbeteren, met name voor gebruikers die schermlezers gebruiken.

### Kan ik tabellen en spans in een PDF bewerken met Aspose.PDF?
Ja, met Aspose.PDF kunt u tabellen, spans en andere gestructureerde elementen in een PDF-document bewerken.

### Waar kan ik Aspose.PDF voor .NET downloaden?
U kunt de nieuwste versie van Aspose.PDF voor .NET downloaden [hier](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}