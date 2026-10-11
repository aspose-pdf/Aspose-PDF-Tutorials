---
category: general
date: 2026-10-10
description: Leer hoe je een rechthoek aan een PDF toevoegt, een vorm op een PDF tekent
  en de gewijzigde PDF opslaat met Aspose.PDF. Inclusief een stapsgewijze handleiding
  om een specifieke PDF-pagina te benaderen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to PDF
- draw shape on PDF
- save modified PDF
- add shape to PDF
- access specific PDF page
language: nl
lastmod: 2026-10-10
og_description: Voeg een rechthoek toe aan PDF met Aspose.PDF in C#. Deze tutorial
  laat zien hoe je een vorm op een PDF tekent, een specifieke PDF-pagina benadert
  en de gewijzigde PDF opslaat.
og_image_alt: Screenshot of a PDF page with a blue rectangle overlay created by Aspose.PDF
og_title: Rechthoek toevoegen aan PDF met Aspose.PDF – volledige C#‑gids
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  headline: How to add rectangle to PDF with Aspose.PDF in C#
  type: TechArticle
- description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  name: How to add rectangle to PDF with Aspose.PDF in C#
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: What if the PDF has only one page?
    text: Attempting to access `pdfDocument.Pages[1]` throws an `ArgumentOutOfRangeException`.
      Guard against this by checking `pdfDocument.Pages.Count` before indexing.
  - name: How to add multiple rectangles on different pages?
    text: Repeat Steps 2‑4 for each target page, adjusting the rectangle’s coordinates
      as needed. You can place the logic inside a loop that iterates over `pdfDocument.Pages`.
  - name: Can I use other shapes such as circles or polygons?
    text: Yes. Aspose.PDF provides `Ellipse`, `Polygon`, and `Polyline` classes that
      follow the same pattern as `Rectangle`. Replace the `new Aspose.Pdf.Drawing.Rectangle`
      call with the desired shape class.
  - name: Does the library support PDFs with rotated pages?
    text: Aspose.PDF automatically respects page rotation when rendering shapes. The
      rectangle’s coordinates are interpreted in the page’s native coordinate system,
      so no extra transformation is required.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Hoe een rechthoek aan een PDF toe te voegen met Aspose.PDF in C#
url: /nl/net/images-graphics/how-to-add-rectangle-to-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een rechthoek toe te voegen aan PDF met Aspose.PDF in C#

Als je programmatisch **rechthoek aan PDF** bestanden wilt **toevoegen**, laat deze gids je precies zien hoe. Je leert **vorm op PDF te tekenen**, een specifieke pagina te targeten, en **aangepaste PDF op te slaan** zonder fouten.

Werken met PDF‑documenten is een veelvoorkomende eis voor rapportage, facturering of documentannotatie. Aan het einde van deze tutorial kun je vol vertrouwen **vorm aan PDF** bestanden **toevoegen**, out‑of‑bounds‑fouten afhandelen, en de oplossing integreren in elk .NET‑project.

## Vereisten

* .NET 6.0 SDK of later geïnstalleerd  
* Visual Studio 2022 (of een andere C#‑IDE)  
* Een Aspose.PDF voor .NET‑licentie of een gratis evaluatiesleutel – de API werkt op dezelfde manier in beide modi  
* Een PDF‑bestand met de naam `input.pdf` geplaatst in een map die je vanuit je code kunt refereren  

Deze items zijn de enige externe afhankelijkheden voor het voorbeeld.

## Stap 1: Installeer het Aspose.PDF NuGet‑pakket

De Aspose.PDF‑bibliotheek biedt de `Document`, `Rectangle` en andere tekenklassen die je nodig hebt.

```bash
dotnet add package Aspose.PDF
```

Het uitvoeren van dit commando voegt de nieuwste stabiele versie van Aspose.PDF toe aan je project, waardoor de PDF‑klassen beschikbaar zijn voor compilatie.

## Stap 2: Laad het PDF‑document

De eerste handeling is het laden van het bronbestand. Dit maakt een in‑memory‑representatie die je kunt aanpassen.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;

class PdfRectangleExample
{
    static void Main()
    {
        // Load the PDF document from disk
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

*Waarom dit belangrijk is*: Het laden van het document geeft je toegang tot de collectie pagina's, wat nodig is om later **specifieke PDF‑pagina te benaderen**.

## Stap 3: Toegang tot de tweede pagina (nul‑gebaseerde index)

PDF‑pagina's worden geïndexeerd vanaf `0`. Om een rechthoek op de tweede pagina te plaatsen, haal je de pagina op met index `1`.

```csharp
        // Access the second page (pages are zero‑based)
        var page = pdfDocument.Pages[1];
```

Als het document minder dan twee pagina's heeft, wordt een `ArgumentOutOfRangeException` gegooid, wat je waarschuwt voor de noodzaak van een guard‑clausule in productiecodel.

## Stap 4: Maak de rechthoek‑vorm

Definieer de positie en grootte van de rechthoek met de `Rectangle`‑structuur, en wikkel deze vervolgens in een Aspose‑tekenobject.

```csharp
        // Define rectangle bounds: (x, y, width, height)
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            // Optional visual styling
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };
```

*Waarom dit belangrijk is*: De `BorderInfo`‑ en `FillColor`‑eigenschappen laten je **vorm op PDF tekenen** met een zichtbare omtrek en optionele vulling, waardoor de rechthoek opvalt voor lezers.

## Stap 5: Voeg de rechthoek toe aan de alinea‑collectie van de pagina

Aspose.PDF behandelt tekenobjecten als alinea‑elementen. Het toevoegen van de rechthoek aan de `Paragraphs`‑collectie van de pagina rendert deze op de pagina.

```csharp
        // Add the rectangle shape to the page
        page.Paragraphs.Add(rectangleShape);
```

Op dit moment bevat het PDF‑document in het geheugen de nieuwe vorm, maar het bestand op schijf blijft ongewijzigd totdat je het opslaat.

## Stap 6: Sla de aangepaste PDF op en handel out‑of‑bounds‑fouten af

Het aanroepen van `Save` schrijft het bijgewerkte document naar een nieuw bestand. Als de rechthoek de paginadimensies overschrijdt, gooit Aspose een `PdfException`. Het opvangen van deze uitzondering stelt je in staat het probleem netjes te rapporteren.

```csharp
        try
        {
            // Save the altered PDF to a new file
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            // Handle shape that does not fit on the page
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

*Waarom dit belangrijk is*: Het `try/catch`‑blok zorgt ervoor dat je applicatie **aangepaste PDF veilig opslaat**, en het foutbericht helpt je de coördinaten van de rechthoek indien nodig aan te passen.

## Volledig werkend voorbeeld

Door alle stappen samen te voegen, hier is het volledige, kant‑klaar programma:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;
using System.Drawing; // Required for Color

class PdfRectangleExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // Step 2: Access the second page (zero‑based)
        var page = pdfDocument.Pages[1];

        // Step 3: Create a rectangle shape positioned at (100,100) with width 300 and height 200
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };

        // Step 4: Add the rectangle shape to the page's paragraph collection
        page.Paragraphs.Add(rectangleShape);

        // Step 5: Save the modified PDF, handling out‑of‑bounds cases
        try
        {
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

### Verwachte output

Het uitvoeren van het programma geeft:

```
PDF saved successfully with rectangle added.
```

en maakt `output.pdf` aan die de originele inhoud toont plus een blauwe rechthoek op de opgegeven coördinaten op de tweede pagina.

Als de rechthoek groter zou zijn dan de pagina, zou je zien:

```
Shape out of bounds: The shape exceeds page margins.
```

## Veelgestelde vragen en randgevallen

### Wat als de PDF slechts één pagina heeft?

Poging om `pdfDocument.Pages[1]` te benaderen veroorzaakt een `ArgumentOutOfRangeException`. Bescherm hiertegen door `pdfDocument.Pages.Count` te controleren vóór het indexeren.

```csharp
if (pdfDocument.Pages.Count < 2)
{
    Console.WriteLine("Document does not contain a second page.");
    return;
}
```

### Hoe meerdere rechthoeken op verschillende pagina's toe te voegen?

Herhaal Stappen 2‑4 voor elke doelpagina, waarbij je de coördinaten van de rechthoek naar behoefte aanpast. Je kunt de logica in een lus plaatsen die over `pdfDocument.Pages` itereren.

### Kan ik andere vormen gebruiken, zoals cirkels of polygonen?

Ja. Aspose.PDF biedt `Ellipse`, `Polygon` en `Polyline` klassen die hetzelfde patroon volgen als `Rectangle`. Vervang de `new Aspose.Pdf.Drawing.Rectangle`‑aanroep door de gewenste vormklasse.

### Ondersteunt de bibliotheek PDF's met geroteerde pagina's?

Aspose.PDF houdt automatisch rekening met paginaverschuiving bij het renderen van vormen. De coördinaten van de rechthoek worden geïnterpreteerd in het native coördinatensysteem van de pagina, dus er is geen extra transformatie nodig.

## Prestatie‑overwegingen

* **Geheugengebruik** – Het laden van een grote PDF (honderden megabytes) verbruikt evenredig geheugen. Als je slechts één pagina hoeft te wijzigen, overweeg dan `PdfFileInfo` te gebruiken om die pagina te extraheren, aan te passen, en vervolgens terug te voegen.  
* **Batchverwerking** – Bij het toevoegen van vormen aan veel documenten, hergebruik een enkele `License`‑instantie om herhaalde licentie‑validatie‑overhead te vermijden.

## Volgende stappen

Nu je **rechthoek aan PDF kunt toevoegen**, verken deze gerelateerde onderwerpen:

* **draw shape on PDF** – leer hoe je tekst, afbeeldingen en watermerken kunt overlappen  
* **add shape to PDF** – combineer meerdere vormen tot één annotatielaag  
* **save modified PDF** – gebruik streams (`MemoryStream`) om PDF's direct vanuit web‑API's terug te geven  
* **access specific PDF page** – implementeer paginabereik‑extractie voor aangepaste rapporten  

Experimenteer met verschillende kleuren, lijntypen en transparantieniveaus om aan je merk‑richtlijnen te voldoen.

---

*Happy coding! Als deze tutorial je heeft geholpen **rechthoek aan PDF toe te voegen**, overweeg dan om het te delen met teamgenoten of verbeteringen terug te dragen aan de community.*

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe vorm toe te voegen aan PDF met Aspose.PDF in C# – Stap‑voor‑stap gids](/pdf/english/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Hoe een lijnobject toe te voegen in PDF met Aspose.PDF voor .NET&#58; Een stap‑voor‑stap gids](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Hoe PDF te maken in C# – Pagina toevoegen, rechthoek tekenen & opslaan](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}