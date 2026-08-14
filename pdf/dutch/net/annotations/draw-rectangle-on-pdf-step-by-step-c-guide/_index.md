---
category: general
date: 2026-08-14
description: Teken snel een rechthoek op een PDF met C#. Leer hoe je de afmetingen
  van een rechthoek definieert en vormen toevoegt aan een PDF-pagina in slechts een
  paar regels.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- draw rectangle on pdf
- how to define rectangle dimensions
language: nl
lastmod: 2026-08-14
og_description: teken een rechthoek op pdf met C# in enkele seconden. Deze gids laat
  zien hoe je de afmetingen van een rechthoek definieert, een vorm toevoegt en de
  paginagrenzen verifieert voor betrouwbare PDF‑grafieken.
og_image_alt: Screenshot of a PDF page showing a black rectangle drawn with C# code
og_title: rechthoek tekenen op pdf – volledige C#-tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: draw rectangle on pdf quickly using C#. Learn how to define rectangle
    dimensions and add shapes to a PDF page in just a few lines.
  headline: draw rectangle on pdf – step‑by‑step C# guide
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
- RectangleShape
- Graphics
title: Rechthoek tekenen op PDF – stapsgewijze C#‑gids
url: /nl/net/annotations/draw-rectangle-on-pdf-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# rechthoek tekenen op pdf – volledige C#‑tutorial

Als je **rechthoek tekenen op pdf** met C# nodig hebt, toont deze gids een beknopte, productie‑klare oplossing. Je ziet precies **hoe je rechthoekafmetingen definieert**, controleert of de vorm past, en voegt deze toe aan een pagina met één methode‑aanroep.

De tutorial behandelt alles van het maken van een PDF‑document tot het renderen van de rechthoek, zodat je de code kunt kopiëren‑plakken in je eigen project en direct resultaat ziet. Geen externe documentatie nodig — alleen de onderstaande stappen.

## Vereisten

Voordat je begint, zorg dat je het volgende hebt:

* .NET 6.0 of later (de code werkt ook met .NET Framework 4.7+)
* Het **Aspose.PDF for .NET** NuGet‑pakket (`Install-Package Aspose.PDF`)
* Een basisbegrip van C#‑syntaxis
* Een IDE zoals Visual Studio of VS Code

> **Pro tip:** Gebruik de gratis evaluatielicentie van Aspose.PDF voor snelle experimenten; deze voegt een klein watermerk toe maar laat je alle functies testen.

## Hoe rechthoek tekenen op PDF met C#

De kern van de taak is het maken van een `RectangleShape`, het instellen van de grootte en de lijn, en het koppelen aan een `Page`. De volgende H2‑kop bevat het primaire zoekwoord, wat voldoet aan SEO‑eisen.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        Document pdfDoc = new Document();

        // 2️⃣ Add a blank page (default size: A4)
        Page page = pdfDoc.Pages.Add();

        // 3️⃣ Define the rectangle bounds (x, y, width, height)
        //    This demonstrates how to define rectangle dimensions.
        Rectangle rectBounds = new Rectangle(0, 0, 500, 700);

        // 4️⃣ Create the rectangle shape and set its stroke color
        RectangleShape rectangleShape = new RectangleShape(rectBounds)
        {
            StrokeColor = Color.Black   // black outline
        };

        // 5️⃣ Verify that the shape fits within the page boundaries
        page.CheckShapeBoundary(rectangleShape);

        // 6️⃣ Add the shape to the page
        page.Add(rectangleShape);

        // 7️⃣ Save the PDF to disk
        string outPath = "RectangleDemo.pdf";
        pdfDoc.Save(outPath);
        Console.WriteLine($"PDF saved to {outPath}");
    }
}
```

### Uitleg van elke stap

| Stap | Waarom het belangrijk is |
|------|--------------------------|
| **1️⃣ Maak een nieuw PDF‑document** | Initialiseert de container die pagina’s en grafische elementen zal bevatten. |
| **2️⃣ Voeg een lege pagina toe** | Je hebt een `Page`‑object nodig omdat vormen aan een pagina worden gekoppeld, niet direct aan het document. |
| **3️⃣ Definieer de rechthoek‑grenzen** | Dit is waar je **hoe je rechthoekafmetingen definieert**. De `Rectangle`‑constructor neemt `x`, `y`, `width` en `height` in points (1 pt = 1/72 in). |
| **4️⃣ Maak de rechthoekvorm** | `RectangleShape` is de Aspose‑klasse die een rechthoek rendert. Het instellen van `StrokeColor` bepaalt de omtrek; je kunt ook `FillColor` instellen voor een solide vulling. |
| **5️⃣ Controleer paginagrenzen** | `CheckShapeBoundary` gooit een uitzondering als de rechthoek groter is dan de paginagrootte, waardoor misvormde PDF’s worden voorkomen. |
| **6️⃣ Voeg de vorm toe aan de pagina** | De vorm wordt onderdeel van de content‑stream van de pagina. |
| **7️⃣ Sla de PDF op** | Slaat het document op in een bestand dat je met elke PDF‑viewer kunt openen. |

De resulterende `RectangleDemo.pdf` bevat een zwarte rechthoek gepositioneerd in de linkerbovenhoek van de pagina, exact 500 pt breed en 700 pt hoog.

![draw rectangle on pdf example](https://example.com/rectangle-demo.png "draw rectangle on pdf example")

*Afbeeldings‑alt‑tekst: draw rectangle on pdf example toont een zwarte rechthoek in de linkerbovenhoek van een PDF‑pagina.*

## Hoe rechthoekafmetingen definiëren voor verschillende paginagroottes

De bovenstaande code gebruikt vaste waarden (`500 x 700`). In echte toepassingen moet de rechthoek vaak aanpassen aan de breedte en hoogte van de pagina.

```csharp
// Get page dimensions (in points)
float pageWidth = page.PageInfo.Width;
float pageHeight = page.PageInfo.Height;

// Define a rectangle that occupies 80% of the page width and 50% of the height
float rectWidth  = pageWidth * 0.8f;
float rectHeight = pageHeight * 0.5f;

// Center the rectangle on the page
float rectX = (pageWidth - rectWidth) / 2;
float rectY = (pageHeight - rectHeight) / 2;

Rectangle dynamicRect = new Rectangle(rectX, rectY, rectWidth, rectHeight);
RectangleShape dynamicShape = new RectangleShape(dynamicRect)
{
    StrokeColor = Color.DarkBlue,
    FillColor   = Color.LightGray   // optional fill
};

page.CheckShapeBoundary(dynamicShape);
page.Add(dynamicShape);
```

**Belangrijke punten:**

* Gebruik `page.PageInfo.Width` en `Height` om de werkelijke paginagrootte te lezen.
* Vermenigvuldigen met een factor (bijv. `0.8f`) laat je afmetingen uitdrukken als een percentage van de pagina.
* Centreren bereik je door de rechthoekgrootte van de paginagrootte af te trekken en de rest te halveren.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Valkuil | Waarom het gebeurt | Oplossing |
|---------|--------------------|-----------|
| Rechthoek strekt zich uit buiten de pagina | Hard‑gecodeerde afmetingen groter dan de paginagrootte. | Roep `page.CheckShapeBoundary` **voordat** je de vorm toevoegt; pas afmetingen aan als er een uitzondering wordt gegooid. |
| Lijn niet zichtbaar | `StrokeColor` staat op de standaardwaarde (`Color.Empty`). | Stel `StrokeColor` expliciet in (bijv. `Color.Black`). |
| Rechthoek verschijnt buiten het scherm | Coördinaten beginnen in PDF‑ruimte links‑onder; het gebruik van scherm‑stijl top‑links coördinaten veroorzaakt een omkering. | Onthoud dat de oorsprong `(0,0)` de linksonderhoek is. Pas `y` dienovereenkomstig aan of gebruik `pageHeight - desiredY`. |
| Onverwachte lijndikte | De standaard lijndikte kan te dun zijn voor afdrukken. | Stel `rectangleShape.LineWidth = 2;` in om de dikte te verhogen. |

## Voorbeeld uitbreiden

Zodra je **rechthoek tekenen op pdf** kunt, kun je eenvoudig andere vormen toevoegen:

* **EllipseShape** – voor cirkels of ovalen.
* **PolygonShape** – voor aangepaste polygonen.
* **TextFragment** – om je rechthoeken te labelen.

Alle vormen volgen dezelfde workflow: grenzen definiëren, uiterlijk configureren, grenzen controleren, en vervolgens toevoegen aan de pagina.

## Volledig, uitvoerbaar programma

Hieronder staat het volledige programma dat de basisrechthoek en het dynamische formaatvoorbeeld combineert. Kopieer het naar een nieuw console‑project, herstel het `Aspose.PDF` NuGet‑pakket, en voer uit.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class RectangleDemo
{
    static void Main()
    {
        // Create document and page
        Document doc = new Document();
        Page page = doc.Pages.Add();

        // ==== Fixed‑size rectangle (basic example) ====
        Rectangle fixedRect = new Rectangle(0, 0, 500, 700);
        RectangleShape fixedShape = new RectangleShape(fixedRect)
        {
            StrokeColor = Color.Black,
            LineWidth   = 1
        };
        page.CheckShapeBoundary(fixedShape);
        page.Add(fixedShape);

        // ==== Dynamic rectangle that adapts to page size ====
        float pageW = page.PageInfo.Width;
        float pageH = page.PageInfo.Height;

        float dynWidth  = pageW * 0.6f;
        float dynHeight = pageH * 0.3f;
        float dynX      = (pageW - dynWidth) / 2;
        float dynY      = (pageH - dynHeight) / 2;

        Rectangle dynamicRect = new Rectangle(dynX, dynY, dynWidth, dynHeight);
        RectangleShape dynamicShape = new RectangleShape(dynamicRect)
        {
            StrokeColor = Color.DarkBlue,
            FillColor   = Color.LightYellow,
            LineWidth   = 2
        };
        page.CheckShapeBoundary(dynamicShape);
        page.Add(dynamicShape);

        // Save PDF
        string outFile = "CombinedRectangles.pdf";
        doc.Save(outFile);
        Console.WriteLine($"PDF created: {outFile}");
    }
}
```

**Verwachte output:**  
Open `CombinedRectangles.pdf`. Je ziet een zwarte rechthoek verankerd in de linksonderhoek en een gecentreerde donkerblauwe rechthoek met een lichtgele vulling. Beide rechthoeken respecteren de paginamarges.

## Conclusie

Je weet nu hoe je **rechthoek tekenen op pdf** met C# kunt doen en precies **hoe je rechthoekafmetingen definieert** voor zowel vaste als responsieve lay‑outs. De aanpak maakt gebruik van Aspose.PDF’s `RectangleShape`, grenscontrole en eenvoudige rekenkunde om zich aan elke paginagrootte aan te passen.

Vervolgens kun je verkennen:

* Het toevoegen van **vulkleuren** en **lijntypes** (gestreept, gestippeld) – secundair zoekwoord: hoe je rechthoekafmetingen definieert met stijl.
* Meerdere vormen combineren in één `Page` om diagrammen of formulieren te maken.
* De PDF exporteren naar een stream voor web‑API’s in plaats van op schijf op te slaan.

Experimenteer met verschillende groottes, kleuren en posities om PDF‑graphics in je .NET‑toepassingen onder de knie te krijgen. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies te beheersen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe PDF’s aanpassen met Aspose.PDF for .NET&#58; Pagina‑marges instellen en lijnen tekenen](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [Hoe paginastempels toevoegen in PDF’s met Aspose.PDF for .NET&#58; Een complete gids](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Hoe paginanummer‑stempels toevoegen in PDF’s met Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}