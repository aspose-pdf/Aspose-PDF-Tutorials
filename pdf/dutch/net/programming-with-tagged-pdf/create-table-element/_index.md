---
"description": "Stapsgewijze handleiding voor het maken van een array-element met Aspose.PDF voor .NET. Genereer eenvoudig dynamische PDF's met tabellen."
"linktitle": "Tabelelement maken"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Tabelelement maken"
"url": "/nl/net/programming-with-tagged-pdf/create-table-element/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tabelelement maken

## Invoering

Heb je je ooit afgevraagd hoe je moeiteloos tabelelementen in een PDF kunt maken en aanpassen met .NET? Nou, Aspose.PDF voor .NET is dé oplossing! Of je nu automatisch rapporten wilt genereren of dynamisch tabellen voor verschillende documenten wilt aanmaken, Aspose.PDF biedt een uitgebreide API om met tabelelementen te werken. Deze handleiding leidt je stap voor stap door het maken van een tabel, het opmaken ervan en zelfs het garanderen dat deze voldoet aan de PDF/UA-normen. Klinkt spannend, toch? Laten we er meteen induiken!

## Vereisten

Voordat we beginnen, moeten er een paar dingen geregeld zijn:
1. Aspose.PDF voor .NET: Download de nieuwste versie van [Aspose.PDF voor .NET downloaden](https://releases.aspose.com/pdf/net/).
2. Ontwikkelomgeving: Elke .NET-ondersteunde IDE (bijv. Visual Studio).
3. Basiskennis van C#: Kennis van C#-programmering wordt aanbevolen.

Vergeet ten slotte uw Aspose.PDF-licentie niet. Als u die niet hebt, kunt u de [gratis proefperiode](https://releases.aspose.com/) of vraag een [tijdelijke licentie](https://purchase.aspose.com/temporary-license/) om alles uit te testen.

## Pakketten importeren

Laten we beginnen met het importeren van de benodigde pakketten. Zo kunnen we met alle relevante klassen werken voor het maken van tabellen in PDF-documenten.

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

In deze sectie splitsen we het proces van het maken van een tabel op in meerdere stappen. Elke stap richt zich op verschillende onderdelen van het proces van het maken en aanpassen van de tabel.

## Stap 1: Een nieuw PDF-document maken

Het eerste wat we moeten doen, is een nieuw PDF-document aanmaken. Dit zal dienen als container voor onze tabel.

```csharp
// Het pad naar de documentenmap.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Een nieuw PDF-document maken
Document document = new Document();
```

Hier initialiseren we een nieuw exemplaar van de `Document` klasse, wat ons lege PDF-bestand wordt. Vergeet niet het bestandspad te definiëren!

## Stap 2: Getagde inhoud instellen

Vervolgens moeten we getagde content inschakelen, wat de toegankelijkheid van de tabel garandeert. Getagde PDF's zijn vereist voor PDF/UA (Universele Toegankelijkheid).

```csharp
// Getagde inhoud inschakelen
ITaggedContent taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example Table");
taggedContent.SetLanguage("en-US");
```

In deze stap worden de documenttitel en -taal ingesteld, zodat de tabel voldoet aan de toegankelijkheidsnormen. Toegankelijke documenten zijn cruciaal voor de gebruikerservaring en wettelijke vereisten in sommige sectoren.

## Stap 3: Het tabelelement maken

Nu komt het leukste gedeelte: het maken van de tafel zelf!

```csharp
// Verkrijg het wortelstructuurelement
StructureElement rootElement = taggedContent.RootElement;
TableElement tableElement = taggedContent.CreateTableElement();
rootElement.AppendChild(tableElement);
```

Hier gebruiken we de `RootElement` van de getagde inhoud om onze tabel toe te voegen. Dit komt in feite neer op het toevoegen van een tabel als onderliggend knooppunt aan de documentstructuur.

## Stap 4: Tabelranden en kopteksten aanpassen

Je wilt toch niet dat je tafel er saai uitziet? Laten we wat stijl toevoegen!

```csharp
tableElement.Border = new BorderInfo(BorderSide.All, 1.2F, Color.DarkBlue);
TableTHeadElement tableTHeadElement = tableElement.CreateTHead();
TableTBodyElement tableTBodyElement = tableElement.CreateTBody();
TableTFootElement tableTFootElement = tableElement.CreateTFoot();
```

We definiëren randen en voegen kopteksten, hoofdteksten en voetteksten toe aan de tabel. Let op het gebruik van `BorderInfo` om de tabelranden donkerblauw te maken.

## Stap 5: Rijen en cellen toevoegen aan de tabel

Laten we nu onze tabel vullen met rijen en cellen. In dit deel van het proces definiëren we de lay-out van onze tabel.

### Stap 5.1: Koptekstrij maken

```csharp
TableTRElement headTrElement = tableTHeadElement.CreateTR();
headTrElement.AlternativeText = "Head Row";
headTrElement.BackgroundColor = Color.LightGray;

for (int colIndex = 0; colIndex < 4; colIndex++)
{
    TableTHElement thElement = headTrElement.CreateTH();
    thElement.SetText($"Head {colIndex}");
    thElement.BackgroundColor = Color.GreenYellow;
    thElement.Border = new BorderInfo(BorderSide.All, 4.0F, Color.Gray);
    thElement.Alignment = HorizontalAlignment.Right;
}
```

We maken een koptekstrij met 4 kolommen en elke koptekstcel is gestyled met een achtergrondkleur van `GreenYellow`We stellen ook een rand en uitlijning in voor de headers.

### Stap 5.2: Bodyrijen toevoegen

```csharp
for (int rowIndex = 0; rowIndex < 50; rowIndex++)
{
    TableTRElement trElement = tableTBodyElement.CreateTR();
    trElement.AlternativeText = $"Row {rowIndex}";

    for (int colIndex = 0; colIndex < 4; colIndex++)
    {
        TableTDElement tdElement = trElement.CreateTD();
        tdElement.SetText($"Cell [{rowIndex}, {colIndex}]");
        tdElement.BackgroundColor = Color.Yellow;
        tdElement.Alignment = HorizontalAlignment.Center;
    }
}
```

Hier maken we dynamisch 50 rijen en 4 kolommen aan, vullen deze met tekst en stylen de cellen. De achtergrondkleur is geel, met de tekst gecentreerd.

### Stap 5.3: Voettekstrij toevoegen

```csharp
TableTRElement footTrElement = tableTFootElement.CreateTR();
footTrElement.AlternativeText = "Foot Row";
footTrElement.BackgroundColor = Color.LightSeaGreen;

for (int colIndex = 0; colIndex < 4; colIndex++)
{
    TableTDElement tdElement = footTrElement.CreateTD();
    tdElement.SetText($"Foot {colIndex}");
    tdElement.Alignment = HorizontalAlignment.Center;
}
```

Om de tabel compleet te maken, voegen we een voettekst toe met gecentreerde tekst en een `LightSeaGreen` achtergrond.

## Stap 6: PDF/UA-naleving valideren

Nadat u de tabel hebt gemaakt, moet u ervoor zorgen dat de PDF PDF/UA-compatibel is.

```csharp
document.Save(dataDir + "CreateTableElement.pdf");

// Valideer PDF/UA-naleving
document = new Document(dataDir + "CreateTableElement.pdf");
bool isPdfUaCompliance = document.Validate(dataDir + "table.xml", PdfFormat.PDF_UA_1);
Console.WriteLine($"PDF/UA compliance: {isPdfUaCompliance}");
```

Dit fragment slaat het PDF-bestand op en controleert of het voldoet aan de PDF/UA-normen. Als het document hieraan voldoet, is het toegankelijk voor gebruikers met een beperking.

## Conclusie

Gefeliciteerd! U hebt met succes een volledig aangepaste tabel in een PDF gemaakt met Aspose.PDF voor .NET. Van het stylen van de tabel tot het garanderen van PDF/UA-compatibiliteit, u beschikt nu over een robuuste basis voor het genereren van dynamische tabellen in uw PDF-documenten. Vergeet niet de uitgebreide functies van Aspose.PDF te verkennen om uw documenten verder te verbeteren!

## Veelgestelde vragen

### Kan ik het lettertype en de tekststijl van de tabel aanpassen?
Ja, met Aspose.PDF kunt u lettertypen, tekststijlen en uitlijning volledig aanpassen met behulp van de `TextState` klas.

### Hoe voeg ik dynamisch meer kolommen of rijen toe?
U kunt het aantal kolommen of rijen aanpassen door de `rowIndex` En `colIndex` in de lussen.

### Is het mogelijk om cellen in de tabel samen te voegen?
Ja, u kunt de `ColSpan` En `RowSpan` Eigenschappen om cellen over kolommen of rijen samen te voegen.

### Wat is PDF/UA-compatibel?
PDF/UA-compliance garandeert dat het document toegankelijk is voor gebruikers met een beperking en voldoet aan de internationale toegankelijkheidsnormen.

### Hoe test ik de PDF/UA-compatibiliteit in Aspose.PDF?
Je kunt de `Validate` Methode om te controleren of het document voldoet aan de PDF/UA-standaarden.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}