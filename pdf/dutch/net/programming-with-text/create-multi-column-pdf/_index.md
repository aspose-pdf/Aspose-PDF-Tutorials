---
"description": "Leer hoe je PDF's met meerdere kolommen maakt met Aspose.PDF voor .NET. Een stapsgewijze handleiding met codevoorbeelden en gedetailleerde uitleg. Perfect voor professionals."
"linktitle": "Maak een PDF met meerdere kolommen"
"second_title": "Aspose.PDF voor .NET API-referentie"
"title": "Maak een PDF met meerdere kolommen"
"url": "/nl/net/programming-with-text/create-multi-column-pdf/"
"weight": 110
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Maak een PDF met meerdere kolommen

## Invoering

Het maken van PDF's met meerdere kolommen is een geweldige manier om tekst in een overzichtelijker en leesbaarder formaat te presenteren. Of u nu een rapport, artikel of lay-out voor een publicatie schrijft, structuren met meerdere kolommen kunnen uw content aantrekkelijker maken. In deze tutorial laten we zien hoe u een PDF met meerdere kolommen maakt met Aspose.PDF voor .NET. Maak u geen zorgen, we leggen het allemaal uit in eenvoudige stappen die gemakkelijk te volgen zijn, zelfs als u nieuw bent op het platform.

## Vereisten

Voordat we met de code aan de slag gaan, zijn er een paar dingen die je moet doen om het proces soepel te kunnen volgen:

1. Aspose.PDF voor .NET: Deze bibliotheek moet geïnstalleerd zijn. U kunt deze downloaden van [hier](https://releases.aspose.com/pdf/net/).
2. Ontwikkelomgeving: Stel uw favoriete IDE in, zoals Visual Studio, voor het schrijven en uitvoeren van C#-code.
3. .NET Framework: Zorg ervoor dat u een compatibele versie van .NET hebt geïnstalleerd.
4. Basiskennis van C#: Kennis van de C#-syntaxis is nuttig, maar we leggen elke stap in detail uit.
5. Tijdelijke licentie: Aspose.PDF vereist een licentie om watermerken of beperkingen te vermijden. U kunt een [tijdelijke licentie](https://purchase.aspose.com/temporary-license/) indien nodig.

## Pakketten importeren

Voordat u begint met coderen, moet u de benodigde naamruimten importeren die u nodig hebt om met Aspose.PDF te kunnen werken. Dit is wat u moet importeren:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

Deze naamruimten bieden toegang tot klassen die nodig zijn voor het maken van PDF's, het tekenen van vormen en het verwerken van tekstopmaak.

Laten we het proces voor het maken van een PDF met meerdere kolommen opsplitsen in eenvoudige, beheersbare stappen.

## Stap 1: Het document instellen

Om te beginnen moet je een nieuw PDF-document maken. Dit houdt in dat je de marges definieert en een pagina toevoegt waar je de content wilt plaatsen.

```csharp
// Het pad naar de documentenmap.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Een nieuw PDF-document maken
Document doc = new Document();

// De marges voor het PDF-bestand instellen
doc.PageInfo.Margin.Left = 40;
doc.PageInfo.Margin.Right = 40;

// Een pagina toevoegen aan het document
Page page = doc.Pages.Add();
```

Hier hebben we een `Document` object en stel de linker- en rechtermarge in op 40 eenheden. Vervolgens hebben we een nieuwe pagina aan dit document toegevoegd, die onze lay-out met meerdere kolommen zal bevatten.

## Stap 2: Een lijn toevoegen om secties te scheiden

Voeg vervolgens een horizontale lijn toe aan de pagina voor visuele scheiding. Dit zorgt voor een strakke en professionele uitstraling.

```csharp
// Maak een grafiekobject om de lijn vast te houden
Aspose.Pdf.Drawing.Graph graph1 = new Aspose.Pdf.Drawing.Graph(500.0, 2.0);

// Voeg de regel toe aan de alineaverzameling van de pagina
page.Paragraphs.Add(graph1);

// Definieer de coördinaten voor de lijn
float[] posArr = new float[] { 1, 2, 500, 2 };

// Maak een lijn en voeg deze toe aan de grafiek
Aspose.Pdf.Drawing.Line l1 = new Aspose.Pdf.Drawing.Line(posArr);
graph1.Shapes.Add(l1);
```

Hier maken we een horizontale lijn met behulp van de `Graph` En `Line` klassen. Deze regel wordt toegevoegd aan de pagina `Paragraphs` collectie, die alle visuele elementen bevat.

## Stap 3: HTML-tekst toevoegen met opmaak

Vervolgens voegen we wat tekst in die HTML-tags bevat, zodat u kunt zien hoe u tekst dynamisch kunt opmaken in de PDF.

```csharp
// Maak een string met HTML-inhoud
string s = "<font face=\"Times New Roman\" size=4>" +
           "<strong> How to Steer Clear of Money Scams </strong>" +
           "</font>";

// Maak een nieuw HtmlFragment met de opgemaakte tekst
HtmlFragment heading_text = new HtmlFragment(s);

// Voeg de HTML-tekst toe aan de pagina
page.Paragraphs.Add(heading_text);
```

Met behulp van de `HtmlFragment` Klasse, we kunnen opgemaakte tekst toevoegen met HTML-tags zoals lettergrootte, stijl en vetgedrukte tekst. Dit is handig om de weergave van uw PDF-inhoud te verbeteren.

## Stap 4: Een lay-out met meerdere kolommen maken

Nu gaan we een lay-out met meerdere kolommen maken. Dit is waar de magie gebeurt: je kunt zelf aangeven hoeveel kolommen je wilt en hoe breed ze moeten zijn.

```csharp
// Maak een zwevende doos om de kolommen vast te houden
Aspose.Pdf.FloatingBox box = new Aspose.Pdf.FloatingBox();

// Stel het aantal kolommen en de afstand ertussen in
box.ColumnInfo.ColumnCount = 2;
box.ColumnInfo.ColumnSpacing = "5";
box.ColumnInfo.ColumnWidths = "105 105";

// Voeg het vakje toe aan de pagina
page.Paragraphs.Add(box);
```

Hier maken we een zwevend vak met twee kolommen. We stellen de afstand tussen de kolommen in en specificeren dat elke kolom 105 eenheden breed moet zijn. Zo kunnen we de gewenste kolomindeling in de PDF creëren.

## Stap 5: Tekst toevoegen aan de kolommen

Laten we de kolommen nu vullen met wat tekstinhoud. Je kunt verschillende `TextFragment` objecten aan elke kolom toe.

```csharp
// Maak en formatteer het eerste tekstfragment
TextFragment text1 = new TextFragment("By A Googler (The Official Google Blog)");
text1.TextState.FontSize = 8;
text1.TextState.FontStyle = FontStyles.Italic;
box.Paragraphs.Add(text1);

// Voeg een extra regel toe voor scheiding
Aspose.Pdf.Drawing.Graph graph2 = new Aspose.Pdf.Drawing.Graph(50.0, 10.0);
float[] posArr2 = new float[] { 1, 10, 100, 10 };
Aspose.Pdf.Drawing.Line l2 = new Aspose.Pdf.Drawing.Line(posArr2);
graph2.Shapes.Add(l2);
box.Paragraphs.Add(graph2);

// Maak en voeg een tweede tekstfragment toe
TextFragment text2 = new TextFragment("Lorem ipsum dolor sit amet, consectetur adipiscing elit...");
box.Paragraphs.Add(text2);
```

Wij voegen een toe `TextFragment` naar het zwevende vak, gevolgd door een andere horizontale lijn. De tweede `TextFragment` Bevat meer tekst om de tweede kolom te vullen. Met deze fragmenten kunnen we verschillende tekstelementen aan de PDF toevoegen met verschillende opmaakopties.

## Stap 6: De PDF opslaan

Nadat u alle inhoud hebt toegevoegd, slaat u het document als PDF-bestand op.

```csharp
// Definieer het uitvoerpad voor de PDF
dataDir = dataDir + "CreateMultiColumnPdf_out.pdf";

// Sla het PDF-document op
doc.Save(dataDir);

// Bericht over succes bij uitvoer
Console.WriteLine("\nMulti-column PDF file created successfully.\nFile saved at " + dataDir);
```

Dit blok slaat het PDF-bestand op in de opgegeven directory en geeft een succesmelding in de console. Het PDF-bestand is nu klaar om te bekijken!

## Conclusie

Door deze eenvoudige stappen te volgen, kunt u eenvoudig een professioneel ogende PDF met meerdere kolommen maken met Aspose.PDF voor .NET. Of het nu gaat om een rapport, artikel of nieuwsbrief, deze techniek helpt u bij het organiseren van inhoud in een visueel aantrekkelijke vorm. Aspose.PDF biedt krachtige tools voor het aanpassen van uw PDF's, van marges en lay-out tot tekstopmaak en het tekenen van vormen. Nu is het uw beurt om het uit te proberen en uw PDF-vaardigheden naar een hoger niveau te tillen!

## Veelgestelde vragen

### Kan ik meer dan twee kolommen in een PDF maken?
Ja, u kunt zoveel kolommen aanmaken als u nodig hebt. Pas eenvoudig de `ColumnCount` eigenschap aanpassen aan het gewenste aantal kolommen.

### Hoe verander ik de breedte van elke kolom?
U kunt de `ColumnWidths` Eigenschap om verschillende breedtes voor elke kolom op te geven. Deze eigenschap accepteert een reeks waarden gescheiden door spaties.

### Is het mogelijk om afbeeldingen aan de kolommen toe te voegen?
Absoluut! Je kunt afbeeldingen toevoegen met behulp van de `Image` klasse en neem ze op in het zwevende vak of een ander lay-outelement in uw PDF.

### Kan ik tekst opmaken met HTML-tags in de kolommen?
Ja, u kunt HTML-tags gebruiken binnen `HtmlFragment` Objecten om uw tekst te stylen. Dit omvat het toevoegen van lettertypen, groottes, kleuren en meer.

### Hoe kan ik meer pagina's toevoegen met dezelfde kolomindeling?
U kunt extra pagina's toevoegen met behulp van `doc.Pages.Add()` en herhaal het proces van het toevoegen van kolommen en inhoud voor elke pagina.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}