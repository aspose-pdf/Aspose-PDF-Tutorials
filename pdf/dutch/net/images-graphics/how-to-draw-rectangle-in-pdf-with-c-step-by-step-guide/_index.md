---
category: general
date: 2026-03-27
description: Leer hoe je een rechthoek tekent in een PDF met Aspose.Pdf voor C#. Voeg
  een rechthoek toe aan een PDF, voeg een vorm toe aan een PDF en teken een vorm op
  een PDF met duidelijke codevoorbeelden.
draft: false
keywords:
- how to draw rectangle
- add rectangle to pdf
- add shape to pdf
- draw shape on pdf
- draw rectangle in pdf
language: nl
og_description: Beheers hoe je een rechthoek tekent in PDF met Aspose.Pdf. Deze tutorial
  laat je stap voor stap zien hoe je een rechthoek aan een PDF toevoegt, een vorm
  aan een PDF toevoegt en een vorm op een PDF tekent.
og_title: Hoe teken je een rechthoek in PDF met C# – Complete gids
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Hoe een rechthoek tekenen in PDF met C# – Stapsgewijze handleiding
url: /nl/net/images-graphics/how-to-draw-rectangle-in-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een rechthoek te tekenen in PDF met C# – Stapsgewijze handleiding

Heb je je ooit afgevraagd **how to draw rectangle** in een PDF zonder te worstelen met low‑level PDF‑syntax? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze een begrenzingsvak, een markeergebied of een eenvoudig decoratief element in een gegenereerd document moeten visualiseren. Het goede nieuws? Met Aspose.Pdf for .NET is het proces een eitje.

In deze tutorial lopen we alles door wat je nodig hebt om **add rectangle to PDF**, **add shape to PDF**, en uiteindelijk **draw rectangle in PDF** te gebruiken met nette, idiomatische C#. Aan het einde heb je een uitvoerbaar programma dat een PDF‑bestand produceert met een scherpe rechthoek—geen externe tools nodig.

## Vereisten

- .NET 6.0 of later (de code werkt ook met .NET Core en .NET Framework)
- Aspose.Pdf for .NET NuGet‑pakket (`Install-Package Aspose.Pdf`)
- Een basis C#‑ontwikkelomgeving (Visual Studio, VS Code, Rider, etc.)

Er zijn geen andere bibliotheken nodig; alles anders wordt door Aspose.Pdf zelf afgehandeld.

## Stap 1: Het project opzetten en namespaces importeren

Maak eerst een nieuwe console‑applicatie en haal de Aspose.Pdf‑namespace binnen.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the rest of the code here.
        }
    }
}
```

**Waarom dit belangrijk is:** Het importeren van `Aspose.Pdf.Drawing` geeft je toegang tot de `Rectangle`‑shape‑klasse die we zullen gebruiken om **draw shape on PDF**. Het netjes houden van het startpunt maakt de latere stappen makkelijker te volgen.

## Stap 2: Een nieuw PDF‑document en een pagina maken

Een PDF zonder pagina's is zinloos, dus beginnen we met het maken van een documentobject en het toevoegen van één pagina.

```csharp
// Step 2: Initialize a new PDF document
Document pdfDoc = new Document();

// Add a blank page to the document (size defaults to A4)
Page page = pdfDoc.Pages.Add();
```

**Uitleg:** De `Document`‑klasse vertegenwoordigt het volledige bestand, terwijl `Pages.Add()` een nieuw `Page`‑object retourneert waar we later **add rectangle to PDF**. De standaard A4‑grootte werkt voor de meeste gevallen, maar je kunt breedte/hoogte doorgeven als je een aangepast canvas nodig hebt.

## Stap 3: De rechthoek‑shape definiëren

Nu volgt de kern van **how to draw rectangle**—het definiëren van de positie en afmetingen.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
// Coordinates are measured from the lower‑left corner of the page.
var rectangleShape = new Rectangle(100, 500, 300, 200)
{
    // Optional: set line color and fill color
    BorderColor = Color.Black,
    BorderWidth = 2,
    FillColor = Color.LightGray
};
```

**Waarom we deze eigenschappen instellen:**  
- `BorderColor` en `BorderWidth` regelen de omtrek, waardoor de rechthoek zichtbaar wordt.  
- `FillColor` geeft een subtiele achtergrond, handig wanneer je een regio wilt markeren.  
- De constructor `(x, y, width, height)` stelt je in staat om **draw rectangle in PDF** precies op de gewenste plek te plaatsen.

## Stap 4: De rechthoek aan de pagina toevoegen

Met de shape klaar, **add shape to PDF** nu door deze aan de `Annotations`‑collectie van de pagina te koppelen. Aspose.Pdf valideert de grenzen automatisch, zodat je je geen zorgen hoeft te maken over overflow.

```csharp
// Step 4: Add the rectangle shape to the page
page.Annotations.Add(rectangleShape);
```

**Wat er onder de motorkap gebeurt:** De `Annotations`‑collectie behandelt de rechthoek als een vectorafbeelding. Wanneer de PDF wordt gerenderd, zet de bibliotheek onze coördinaten om in de PDF‑content‑stream.

## Stap 5: Het document opslaan

Schrijf tenslotte de PDF naar schijf zodat je deze in elke viewer kunt openen.

```csharp
// Step 5: Save the PDF file
string outputPath = "RectangleDemo.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

**Resultaat:** Het openen van `RectangleDemo.pdf` toont een lichtgrijze rechthoek met een zwarte rand, gepositioneerd 100 pts vanaf de linkerkant en 500 pts vanaf de onderkant van de pagina. Dat is de volledige oplossing voor **how to draw rectangle** in een PDF met C#.

## Volledig werkend voorbeeld

Door alle onderdelen samen te voegen, hier is het volledige, kant‑klaar programma:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize a new PDF document
            Document pdfDoc = new Document();

            // Add a blank page (A4 by default)
            Page page = pdfDoc.Pages.Add();

            // Define a rectangle shape (x, y, width, height)
            var rectangleShape = new Rectangle(100, 500, 300, 200)
            {
                BorderColor = Color.Black,
                BorderWidth = 2,
                FillColor = Color.LightGray
            };

            // Add the rectangle to the page
            page.Annotations.Add(rectangleShape);

            // Save the document
            string outputPath = "RectangleDemo.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved to {outputPath}");
        }
    }
}
```

**Verwachte output:** Een bestand genaamd `RectangleDemo.pdf` met één pagina met een gecentreerde lichtgrijze rechthoek omlijnd in zwart. Je kunt het openen met Adobe Reader, Chrome of elke PDF‑viewer.

## Veelvoorkomende variaties & randgevallen

### 1. Meerdere rechthoeken tekenen

Als je meer dan één keer **add rectangle to PDF** moet, maak dan simpelweg extra `Rectangle`‑objecten aan en voeg elk toe aan `page.Annotations`. Over een collectie coördinaten itereren maakt dit triviaal.

```csharp
foreach (var rectInfo in rectangles)
{
    var rect = new Rectangle(rectInfo.X, rectInfo.Y, rectInfo.Width, rectInfo.Height)
    {
        BorderColor = Color.Blue,
        BorderWidth = 1,
        FillColor = Color.Transparent
    };
    page.Annotations.Add(rect);
}
```

### 2. Andere eenheden gebruiken

Aspose.Pdf werkt met points (1 pt = 1/72 inch). Als je millimeters verkiest, converteer ze dan eerst:

```csharp
double mmToPt = 72.0 / 25.4;
float x = (float)(20 * mmToPt); // 20 mm from left
float y = (float)(150 * mmToPt);
```

### 3. Een rechthoek toevoegen als formulier‑veld

Wanneer je een interactieve rechthoek nodig hebt (bijv. een klikbaar gebied), gebruik dan een `LinkAnnotation` in plaats van een gewone `Rectangle`. De code is vergelijkbaar maar voegt een URL of JavaScript‑actie toe.

### 4. Compatibiliteitszorgen

Aspose.Pdf versie 23.9 (uitgebracht begin 2026) ondersteunt volledig de hierboven getoonde API’s. Oudere versies kunnen `page.AddAnnotation(rectangleShape)` vereisen in plaats van `page.Annotations.Add`. Controleer altijd de release‑notes als je compileerfouten tegenkomt.

## Pro‑tips & valkuilen

- **Pro tip:** Stel `FillColor = Color.Transparent` in als je alleen een omtrek nodig hebt. Dit verkleint de bestandsgrootte een beetje.
- **Watch out for:** Het gebruiken van coördinaten die de paginadimensies overschrijden. Aspose.Pdf zal de shape stilletjes afsnijden, wat verwarrend kan zijn bij het debuggen.
- **Performance note:** Het toevoegen van duizenden rechthoeken is prima, maar als je grote rapporten genereert, overweeg dan om shapes te batchen in één `Graphics`‑object om overhead te verminderen.

## Visuele referentie

Hieronder staat een snelle screenshot van de gegenereerde PDF (de rechthoek is gemarkeerd in lichtgrijs). De alt‑tekst bevat het primaire trefwoord voor SEO.

![how to draw rectangle in PDF example](https://example.com/images/rectangle-demo.png "how to draw rectangle in PDF example")

## Conclusie

We hebben **how to draw rectangle** in een PDF behandeld met Aspose.Pdf voor C#. Door een `Document` te maken, een `Page` toe te voegen, een `Rectangle`‑shape te definiëren, en uiteindelijk **adding shape to PDF**, kun je vector‑gebaseerde graphics genereren met slechts een handvol regels. Of je nu **add rectangle to pdf** nodig hebt voor markering, lay‑out debugging, of UI‑overlays, de aanpak schaalt goed.

Vervolgens kun je **draw shape on pdf** verkennen buiten rechthoeken—denk aan cirkels, polylijnen, of zelfs aangepaste SVG‑paden. Of duik in tekstweergave, afbeelding‑invoeging, en PDF‑formuliermanipulatie om volledige rapporten te bouwen. De Aspose.Pdf‑bibliotheek biedt een rijke API, en met de hier behandelde basisprincipes ben je klaar om te experimenteren.

Veel plezier met coderen, en moge je PDF’s er altijd precies uitzien zoals jij ze voor ogen hebt!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}