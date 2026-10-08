---
category: general
date: 2026-04-12
description: Voeg snel een figuur toe aan Word met C#. Leer hoe je een figuur positioneert
  in Word, een figuur invoegt in een docx, en aangepaste XML toevoegt voor geavanceerde
  lay‑out.
draft: false
keywords:
- add figure to word
- position figure in word
- insert figure into docx
- how to add custom xml
- how to position shape word
language: nl
og_description: Voeg snel een afbeelding toe aan Word met C#. Leer hoe je een afbeelding
  in Word positioneert, een afbeelding in een docx invoegt en aangepaste XML toevoegt
  voor geavanceerde lay‑out.
og_title: Figuur toevoegen aan Word – Complete C#‑programmeerhandleiding
tags:
- C#
- Word Automation
- Document Generation
title: Figuur toevoegen aan Word – Complete C#‑programmeerhandleiding
url: /nl/net/programming-with-images/add-figure-to-word-complete-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Voeg figuur toe aan Word – Complete C# Programmeergids

Heb je ooit **figuur toevoegen aan Word** nodig gehad maar wist je niet waar te beginnen? Je bent niet de enige. In veel office‑automatiseringsprojecten is het ontbrekende stuk een mooi geplaatste afbeelding of diagram die zich bevindt in een custom XML‑deel. Deze gids laat je precies zien hoe je **figuur positioneren in Word**, de figuur in een *.docx*‑bestand invoegt, en zelfs de onderliggende custom XML aanpast zodat de vorm zich gedraagt als elk native Word‑object.

We lopen een praktijkvoorbeeld door met de GemBox.Document‑bibliotheek (gratis voor kleine bestanden, commercieel voor grotere workloads). Aan het einde heb je een zelfstandige, uitvoerbare programma dat een figuur plaatst op coördinaten X = 50, Y = 200 binnen een tagged‑content container. Geen vage “zie de docs” shortcuts—alleen duidelijke code, waarom het werkt, en tips die je direct in je eigen project kunt kopiëren.

## Vereisten

- .NET 6.0 of later (de code compileert ook met .NET Core 3.1)
- **GemBox.Document** NuGet‑pakket (`Install-Package GemBox.Document`)
- Een start‑Word‑bestand (`input.docx`) dat al een custom XML‑tag bevat waar je de figuur wilt laten verschijnen
- Basis C#‑kennis (je zult zien waarom elke regel belangrijk is)

> **Pro tip:** Als je geen vooraf getagde document hebt, kun je er een maken in Word door een *Content Control* → *XML Mapping Pane* → een custom XML‑deel te mappen. De bibliotheek behandelt die controle als `TaggedContent`.

## Stap 1 – Laad het bron‑document

Het eerste wat we doen is het bestaande *.docx*‑bestand openen. `Document` is het toegangspunt voor alle GemBox‑bewerkingen.

```csharp
using GemBox.Document;
using System.Drawing;

// Set the license key (free version uses a limited license key)
ComponentInfo.SetLicense("FREE-LIMITED-KEY");

// Step 1: Load the source document
Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
```

*Waarom?* Het laden van het bestand geeft ons toegang tot de interne onderdelen, inclusief eventuele custom XML‑containers. Zonder dit konden we de `TaggedContent`‑node die onze figuur zal bevatten niet vinden.

## Stap 2 – Toegang tot de Tagged Content (Custom XML‑container)

Custom XML wordt opgeslagen in een *content control* in Word. GemBox maakt het beschikbaar als `TaggedContent`. 

```csharp
// Step 2: Access the document's tagged content (the container for custom XML)
TaggedContent taggedContent = doc.TaggedContent;
```

Als het document meerdere getagde secties heeft, retourneert `TaggedContent` de **eerste**. Je kunt ook `doc.TaggedContents` enumereren om een specifieke tag op naam te kiezen.

## Stap 3 – Maak het Figure‑element

Een `FigureElement` vertegenwoordigt een afbeelding, diagram of elk visueel object dat Word beschouwt als een *shape*. We zullen het maken binnen de getagde container.

```csharp
// Step 3: Create a new figure element that will be placed inside the tagged content
FigureElement figure = taggedContent.CreateFigureElement();
```

*Waarom hier een figuur maken?* Door het aan de custom XML‑node te koppelen, weet Word dat de figuur tot die logische sectie behoort, wat cruciaal is voor latere bewerkingen of content‑control‑gebaseerde workflows.

## Stap 4 – Positioneer de figuur nauwkeurig

Word gebruikt punten (1 pt ≈ 1/72 in) voor positionering. De `PointF`‑struct maakt het mogelijk om X/Y‑coördinaten eenvoudig in te stellen.

```csharp
// Step 4: Position the figure at the desired coordinates (X = 50, Y = 200)
figure.Position = new PointF(50, 200);
```

> **Hoe shape positioneren in Word:** De `Position`‑eigenschap accepteert een `PointF` waarbij de eerste waarde de horizontale offset (links) is en de tweede de verticale offset (boven) ten opzichte van de paginamarge. Pas deze getallen aan om de plaatsing fijn af te stemmen.

## Stap 5 – Voeg de figuur in de Tagged Content‑boom in

Nu koppelen we de figuur aan het root‑element van de custom XML‑boom. Dit voegt de shape fysiek toe aan het Word‑document.

```csharp
// Step 5: Insert the figure into the root element of the tagged content tree
taggedContent.RootElement.AppendChild(figure);
```

Op dit punt bevindt de figuur zich in het document, maar heeft nog geen afbeeldingsbron. Laten we een eenvoudige PNG van de schijf toevoegen.

```csharp
// Optional: Load an image and assign it to the figure
using (var imageStream = System.IO.File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
{
    figure.Image = new Image(imageStream);
}
```

## Stap 6 – Sla het gewijzigde document op

Tot slot schrijven we de wijzigingen terug naar een nieuw *.docx*‑bestand.

```csharp
// Step 6: Save the updated document
doc.Save(@"YOUR_DIRECTORY\output.docx");
```

Wanneer je `output.docx` in Word opent, zie je de afbeelding precies gepositioneerd op (50, 200) binnen het custom‑XML‑blok dat je hebt getarget.

### Volledig werkend voorbeeld

```csharp
using GemBox.Document;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // License (free version)
        ComponentInfo.SetLicense("FREE-LIMITED-KEY");

        // Load the source DOCX
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // Access the first tagged content container
        TaggedContent taggedContent = doc.TaggedContent;

        // Create a new figure element
        FigureElement figure = taggedContent.CreateFigureElement();

        // Position the figure (X = 50 pt, Y = 200 pt)
        figure.Position = new PointF(50, 200);

        // Load an image file and assign it
        using (FileStream fs = File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
        {
            figure.Image = new Image(fs);
        }

        // Append the figure to the custom XML root
        taggedContent.RootElement.AppendChild(figure);

        // Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

**Verwacht resultaat:** Het openen van `output.docx` toont de PNG precies op de opgegeven locatie, genest binnen het custom XML‑deel. Als je de XML van het document inspecteert (`.docx` → unzip → `word/document.xml`), zie je een `<w:pict>`‑element met de juiste `<v:shape>`‑coördinaten.

## Veelgestelde vragen & randgevallen

### Wat als het document meerdere getagde secties heeft?

Gebruik `doc.TaggedContents` om te enumereren en te selecteren op tag‑naam:

```csharp
TaggedContent myTag = doc.TaggedContents.First(tc => tc.TagName == "MyCustomTag");
```

### Hoe een bijschrift aan de figuur toevoegen?

```csharp
figure.Caption = new CaptionElement("Figure 1 – Sample Diagram");
```

### Werkt dit met Word 2010 en later?

Ja. GemBox.Document richt zich op de Open XML‑standaard, die compatibel is met Word 2007 + (inclusief 2010, 2013, 2016, 2019 en Microsoft 365).

### Wat als ik de shape moet roteren?

```csharp
figure.Rotation = 45; // degrees
```

### Hoe een vectorafbeelding toevoegen in plaats van een rasterafbeelding?

```csharp
figure.Image = new Image(@"YOUR_DIRECTORY\vector.svg");
```

## Pro‑tips & valkuilen

- **Bestandspaden:** Gebruik `Path.Combine` om hard‑gecodeerde scheidingstekens te vermijden, vooral op niet‑Windows platformen.
- **Licentie‑limieten:** De gratis GemBox‑licentie beperkt de documentgrootte tot 20 KB. Voor grotere bestanden koop je een commerciële sleutel.
- **Prestaties:** Het hergebruiken van één `Document`‑instantie voor batchverwerking vermindert het geheugenverbruik drastisch.
- **Shape‑overflow:** Als de afmetingen van de figuur de paginamarges overschrijden, zal Word deze afsnijden. Pas `figure.Width` en `figure.Height` dienovereenkomstig aan.

## Conclusie

Je weet nu **hoe je een figuur toevoegt aan Word**, nauwkeurig **een figuur positioneert in Word**, en hoe je de onderliggende custom XML manipuleert zodat de shape zich gedraagt als elk native element. Het volledige, uitvoerbare voorbeeld demonstreert elke stap—van het laden van het document, het maken van een `FigureElement`, het instellen van de coördinaten, het koppelen van een afbeelding, tot het uiteindelijk opslaan van de bijgewerkte *.docx*.

Probeer nu te experimenteren met **figuur invoegen in docx** door meerdere figuren toe te voegen, loops te gebruiken, of charts on‑the‑fly te genereren. Je kunt ook **custom xml toevoegen** verkennen voor rijkere content controls of leren **hoe shape te positioneren in Word** in tabellen en headers. De mogelijkheden zijn eindeloos, en met de hier behandelde basis ben je klaar om Word‑documenten te automatiseren als een professional.

Veel plezier met coderen, en voel je vrij om een reactie achter te laten als je ergens tegenaan loopt!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}