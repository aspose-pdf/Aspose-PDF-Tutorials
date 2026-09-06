---
category: general
date: 2026-09-05
description: Maak een PDF‑document in C# door een lege pagina toe te voegen, een rechthoek
  te tekenen en het PDF‑bestand op te slaan. Volg een stapsgewijs Aspose.PDF‑voorbeeld.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add blank page pdf
- draw rectangle pdf
- save pdf file
- how to add rectangle
language: nl
lastmod: 2026-09-05
og_description: Maak een PDF-document in C# door een lege pagina toe te voegen, een
  rechthoek te tekenen en het PDF‑bestand op te slaan. Volg dit volledige voorbeeld
  met Aspose.PDF.
og_image_alt: Screenshot showing a PDF document with a drawn rectangle on a blank
  page
og_title: Maak PDF-document met lege pagina en rechthoek – C#-gids
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  headline: How to create PDF document with a blank page and rectangle
  type: TechArticle
- description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  name: How to create PDF document with a blank page and rectangle
  steps:
  - name: 'Edge case: custom page size'
    text: 'If your layout requires a 6 × 9 inch page, replace the default call with:'
  - name: 'Pro tip: styling the rectangle'
    text: 'You can change the stroke color and line width:'
  - name: 'Edge case: overwriting existing files'
    text: 'Aspose.PDF overwrites an existing file by default. To protect previous
      outputs, check for file existence first:'
  - name: Expected output
    text: Running the program creates a single‑page PDF. When you open `output.pdf`
      you will see a blank white page with a red rectangle positioned 100 points from
      the left and bottom edges, measuring 200 × 200 points.
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
- PDF generation
title: Hoe maak je een PDF‑document met een lege pagina en een rechthoek
url: /nl/net/document-creation/how-to-create-pdf-document-with-a-blank-page-and-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een PDF-document te maken met een lege pagina en rechthoek

Als je **PDF-document maken** programmatically, laat deze gids een volledige oplossing zien in C#. Je leert hoe je een lege pagina toevoegt, een rechthoek op die pagina tekent, en uiteindelijk het PDF‑bestand opslaat. Het voorbeeld maakt gebruik van de Aspose.PDF‑bibliotheek, die werkt met .NET 6+ en .NET Framework 4.5+.

Het toevoegen van een lege pagina en het tekenen van vormen is een veelvoorkomende eis voor facturen, certificaten of aangepaste rapporten. Aan het einde van deze tutorial heb je een uitvoerbaar project dat een PDF produceert met een enkele rechthoek gepositioneerd op (100, 100) met een grootte van 200 × 200 punten.

## Vereisten

* Visual Studio 2022 (of een andere C# IDE)
* .NET 6 SDK of .NET Framework 4.5+
* Aspose.PDF for .NET NuGet‑pakket  
  ```bash
  dotnet add package Aspose.PDF
  ```
* Schrijfrechten voor de uitvoermap

Er is geen extra configuratie vereist; de code werkt direct out‑of‑the‑box.

## PDF-document maken – overzicht

Het volledige proces bestaat uit vier logische stappen:

1. **Instantiate** een `Document`‑object – dit vertegenwoordigt het PDF‑bestand.
2. **Add a blank page** – de pagina biedt een canvas voor tekenen.
3. **Draw a rectangle** – een `Path`‑object definieert de vorm.
4. **Save the PDF file** – slaat het document op schijf op.

Elke stap staat in een eigen sectie, zodat je onderdelen kunt hergebruiken of vervangen indien nodig.

![Diagram van een PDF met een rechthoek op een lege pagina](https://example.com/placeholder-image.png){.img-fluid alt="Schermafbeelding die een PDF-document toont met een getekende rechthoek op een lege pagina"}

## Lege pagina toevoegen pdf

Een PDF moet minimaal één pagina bevatten voordat er grafische elementen geplaatst kunnen worden. De methode `Pages.Add()` maakt een lege pagina met standaardafmetingen (A4). Als je een andere grootte nodig hebt, geef je een `PageSize`‑argument mee.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();

// Step 2: Add a blank page to the document
Page pdfPage = pdfDocument.Pages.Add();   // adds an A4 page by default
```

*Waarom deze stap belangrijk is* – Het paginobject bevat collecties voor tekst, afbeeldingen en vector‑graphics. Zonder een pagina zou elke poging om een rechthoek toe te voegen een uitzondering veroorzaken.

### Randgeval: aangepaste paginagrootte

Als je lay‑out een pagina van 6 × 9 inch vereist, vervang dan de standaardaanroep door:

```csharp
var pageSize = new Size(432, 648); // 72 points per inch
Page pdfPage = pdfDocument.Pages.Add(pageSize);
```

## Rechthoek tekenen pdf

Een rechthoek tekenen bestaat uit het maken van een `Rectangle`‑geometrie en deze in een `Path` te wikkelen. De aanroep `ValidateBounds()` zorgt ervoor dat de vorm binnen de paginamarges past, waardoor afkappen wordt voorkomen.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

// Step 4: Add the rectangle to the page contents
Path rectanglePath = new Path(shapeRect).ValidateBounds();
pdfPage.Contents.Add(rectanglePath);
```

*Waarom deze stap belangrijk is* – Het `Path`‑object is de low‑level vector‑primitive die door Aspose.PDF wordt gebruikt. Door de grenzen te valideren voorkom je runtime‑fouten wanneer de rechthoek de paginalimieten overschrijdt.

### Pro‑tip: de rechthoek stylen

Je kunt de lijnkleur en lijndikte aanpassen:

```csharp
rectanglePath.GraphInfo = new GraphInfo
{
    StrokeColor = Color.Red,
    LineWidth = 2
};
```

Dit resulteert in een rode omtrek met een dikte van 2 punten.

## PDF-bestand opslaan

Het document opslaan maakt het bestand definitief op schijf. De methode `Save` accepteert een bestandspad of een stream. Het opgeven van een absoluut pad maakt de locatie expliciet, wat nuttig is voor automatiseringsscripts.

```csharp
// Step 5: Save the PDF to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

*Waarom deze stap belangrijk is* – Opslaan is het enige moment waarop de in‑memory representatie een fysiek bestand wordt. Als je de PDF vanuit een web‑API moet retourneren, vervang je het bestandspad door een `MemoryStream`.

### Randgeval: bestaande bestanden overschrijven

Aspose.PDF overschrijft standaard een bestaand bestand. Om eerdere uitvoer te beschermen, controleer je eerst of het bestand bestaat:

```csharp
if (File.Exists(outputPath))
{
    File.Delete(outputPath);
}
pdfDocument.Save(outputPath);
```

## Hoe een rechthoek toe te voegen – best practices

- **Houd coördinaten binnen de paginamarges** – gebruik `ValidateBounds()` of bereken de marges handmatig.
- **Herbruik `GraphInfo`‑objecten** bij het tekenen van meerdere vormen; dit vermindert geheugenallocatie.
- **Dispose het `Document`‑object** (zoals getoond met `using var`) om native resources snel vrij te geven.
- **Test met verschillende DPI‑instellingen** als je later rasterafbeeldingen inbedt; vectorvormen zoals rechthoeken blijven scherp bij elke resolutie.

## Volledig werkend voorbeeld

Hieronder staat het volledige programma dat je kunt kopiëren naar een console‑applicatie. Het compileert zonder aanpassingen en produceert `output.pdf` in de projectmap.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using var pdfDocument = new Document();

        // Add a blank page to the document
        Page pdfPage = pdfDocument.Pages.Add();

        // Define a rectangle shape (x, y, width, height)
        Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

        // Create a path for the rectangle and validate its bounds
        Path rectanglePath = new Path(shapeRect).ValidateBounds();

        // Optional: style the rectangle (red outline, 2‑pt width)
        rectanglePath.GraphInfo = new GraphInfo
        {
            StrokeColor = Color.Red,
            LineWidth = 2
        };

        // Add the rectangle to the page contents
        pdfPage.Contents.Add(rectanglePath);

        // Determine output path
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");

        // Ensure no leftover file blocks the save operation
        if (File.Exists(outputPath))
        {
            File.Delete(outputPath);
        }

        // Save the PDF to a file
        pdfDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

### Verwachte output

Het uitvoeren van het programma maakt een PDF met één pagina. Wanneer je `output.pdf` opent, zie je een lege witte pagina met een rode rechthoek die 100 punten van de linker- en onderrand is gepositioneerd, met een afmeting van 200 × 200 punten.

## Conclusie

Je weet nu hoe je **PDF-document kunt maken**, **een lege pagina aan een PDF kunt toevoegen**, **een rechthoek in een PDF kunt tekenen**, en **een PDF-bestand kunt opslaan** met Aspose.PDF in C#. Het voorbeeld behandelt de essentiële API‑aanroepen, legt uit waarom elke aanroep nodig is, en biedt tips voor veelvoorkomende variaties zoals aangepaste paginagroottes of het stylen van een rechthoek.

Vervolgens kun je gerelateerde onderwerpen verkennen zoals **tekst toevoegen**, **afbeeldingen insluiten**, of **meerdere‑pagina‑rapporten maken**. Hetzelfde patroon — een `Document` instantiëren, pagina's manipuleren, vector‑ of rasterinhoud toevoegen, en vervolgens `Save` — is van toepassing op al deze scenario's. Voel je vrij om te experimenteren met verschillende vormen, kleuren en paginalay‑outs om aan de behoeften van je project te voldoen.

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [PDF-document maken C# – Pagina toevoegen, rechthoek tekenen & opslaan](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)
- [PDF-document maken met Aspose.PDF – Stapsgewijze gids](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [PDF-document maken met Aspose – Pagina toevoegen, tekstvak en formulier](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}