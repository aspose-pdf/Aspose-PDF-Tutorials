---
category: general
date: 2026-08-04
description: Voeg een rechthoek toe aan een PDF met C#. Leer hoe je een vorm tekent
  in een PDF met C# en Aspose.Pdf in een duidelijk, volledig voorbeeld.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to pdf
- how to draw shape in pdf c#
language: nl
lastmod: 2026-08-04
og_description: Voeg een rechthoek toe aan PDF met C#. Deze tutorial laat zien hoe
  je snel en betrouwbaar een vorm in een PDF kunt tekenen met C#.
og_image_alt: Screenshot of a PDF page with a blue rectangle drawn by C# code
og_title: Rechthoek toevoegen aan PDF met C# – volledige programmeergids
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  headline: Add rectangle to PDF with C# – step‑by‑step guide
  type: TechArticle
- description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  name: Add rectangle to PDF with C# – step‑by‑step guide
  steps:
  - name: '**Create a new console project**'
    text: '**Create a new console project**'
  - name: '**Add the Aspose.Pdf package**'
    text: '**Add the Aspose.Pdf package**'
  - name: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
    text: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Rechthoek toevoegen aan PDF met C# – stap‑voor‑stap gids
url: /nl/net/images-graphics/add-rectangle-to-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rechthoek toevoegen aan PDF met C# – stapsgewijze handleiding

Als je **een rechthoek aan PDF**‑bestanden wilt toevoegen vanuit een C#‑applicatie, laat deze gids je precies zien hoe je dat doet. Je ziet een volledig, uitvoerbaar voorbeeld dat een vorm tekent in PDF C# met de Aspose.Pdf‑bibliotheek, en je begrijpt waarom elke regel code van belang is.

Vormen tekenen in PDF’s is een veelvoorkomende eis voor rapportgeneratoren, factuursjablonen en aangepaste documentbranding. Aan het einde van deze tutorial kun je elke rechthoekige annotatie invoegen, de grootte, kleur of positie wijzigen, en het gewijzigde document opslaan zonder bestaande inhoud te verliezen.

**Wat je zult leren**

* Hoe je een bestaande PDF laadt met Aspose.Pdf.
* Hoe je rechthoekige grenzen definieert en een rechthoekvorm maakt.
* Hoe je de rechthoek toevoegt aan de alinea‑collectie van een pagina.
* Hoe je de bijgewerkte PDF opslaat en het resultaat verifieert.
* Variaties voor meerdere pagina’s, transparantie en aangepaste lijntypen.

**Prerequisites**

* .NET 6.0 of later (de code werkt ook met .NET Framework 4.7+).
* Visual Studio 2022 of een andere C#‑IDE.
* Een NuGet‑referentie naar `Aspose.Pdf` (gratis proefversie of gelicentieerde versie).
* Een invoer‑PDF‑bestand genaamd `input.pdf` geplaatst in een map die jij beheert.

---

## Hoe vorm te tekenen in PDF C# – project opzetten

1. **Maak een nieuw console‑project**  

   ```bash
   dotnet new console -n PdfRectangleDemo
   cd PdfRectangleDemo
   ```

2. **Voeg het Aspose.Pdf‑pakket toe**  

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. **Plaats `input.pdf`** in de projectmap (of een andere map die je later referentieert).

Het project is nu klaar om code te compileren die **een rechthoek aan PDF**‑bestanden toevoegt.

---

## Stap 1: Laad het PDF‑document

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // Load the existing PDF file.
        Document pdfDoc = new Document("input.pdf");
```

*De `Document`‑klasse parseert het bestand en stelt een `Pages`‑collectie beschikbaar. Laden is de eerste vereiste handeling voordat er getekend kan worden.*

---

## Stap 2: Kies de doelpagina

```csharp
        // Get the first page (pages are 1‑based).
        Page firstPage = pdfDoc.Pages[1];
```

*Als je de rechthoek op een andere pagina wilt toevoegen, vervang dan de index door het gewenste paginanummer. De bibliotheek gooit een uitzondering wanneer de index buiten het bereik ligt, dus zorg ervoor dat de PDF voldoende pagina’s bevat.*

---

## Stap 3: Definieer rechthoekige grenzen

```csharp
        // Define the rectangle's position and size (points).
        // (left, bottom, right, top) – origin is bottom‑left.
        Rectangle bounds = new Rectangle(50, 700, 300, 800);
```

*Het coördinatensysteem gebruikt punten (1 pt = 1/72 inch). Het voorbeeld maakt een rechthoek van 250 pt breed en 100 pt hoog dicht bij de bovenkant van de pagina. Pas de getallen aan om bij jouw lay‑out te passen.*

---

## Stap 4: Maak de rechthoekvorm

```csharp
        // Create a rectangle shape with the defined bounds.
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            // Optional styling – a semi‑transparent blue fill.
            FillColor = Color.FromRgb(0, 120, 215),
            FillOpacity = 0.4,

            // Optional border – 2 pt thick, dark gray.
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };
```

*De `Rectangle`‑klasse erft van `GraphicalObject`. Het instellen van `FillColor` en `Border` is optioneel, maar het laat zien hoe je het uiterlijk kunt regelen wanneer je **hoe vorm te tekenen in PDF C#** wilt gaan verder dan een eenvoudige omtrek.*

---

## Stap 5: Voeg de rechthoek toe aan de pagina

```csharp
        // Add the rectangle shape to the page's paragraph collection.
        firstPage.Paragraphs.Add(rectangleShape);
```

*Paragraphs zijn de container voor elk tekenbaar object. Door de vorm in `Paragraphs` te plaatsen, rendert Aspose.Pdf deze bij het opslaan van het document.*

---

## Stap 6: Sla de gewijzigde PDF op

```csharp
        // Save the updated PDF to a new file.
        pdfDoc.Save("output.pdf");

        // Inform the user.
        Console.WriteLine("Rectangle added and saved to output.pdf");
    }
}
```

*Opslaan maakt een nieuw bestand aan zodat het originele `input.pdf` ongewijzigd blijft. Je kunt het bronbestand overschrijven door hetzelfde pad te gebruiken, maar een back‑up behouden is een goede gewoonte.*

---

## Volledige broncode (uitvoerbaar)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color struct

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document
        Document pdfDoc = new Document("input.pdf");

        // Step 2: Get the first page (pages are 1‑based)
        Page firstPage = pdfDoc.Pages[1];

        // Step 3: Define rectangle bounds (left, bottom, right, top)
        Rectangle bounds = new Rectangle(50, 700, 300, 800);

        // Step 4: Create a rectangle shape with optional styling
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            FillColor = Color.FromArgb(102, 0, 120, 215), // 40 % opacity blue
            FillOpacity = 0.4,
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };

        // Step 5: Add the rectangle shape to the page
        firstPage.Paragraphs.Add(rectangleShape);

        // Step 6: Save the modified PDF
        pdfDoc.Save("output.pdf");

        Console.WriteLine("Rectangle added to PDF successfully.");
    }
}
```

**Verwacht resultaat** – Open `output.pdf` in een PDF‑viewer. Je zou een blauwgevulde rechthoek moeten zien dicht bij de rechter‑bovenhoek van de eerste pagina, omlijnd met een donkergrijze rand.

---

## Hoe vorm te tekenen in PDF C# op meerdere pagina’s

Als je **een rechthoek aan PDF** wilt toevoegen op elke pagina, doorloop dan de `Pages`‑collectie:

```csharp
foreach (Page page in pdfDoc.Pages)
{
    Rectangle rect = new Rectangle(50, 700, 300, 800);
    Rectangle shape = new Rectangle(rect)
    {
        FillColor = Color.FromArgb(80, 255, 0, 0), // semi‑transparent red
        Border = new Border { Width = 1, Color = Color.Black }
    };
    page.Paragraphs.Add(shape);
}
```

*Dit patroon hergebruikt dezelfde grenzen op elke pagina. Pas de coördinaten per pagina aan als je verschillende posities nodig hebt.*

---

## Veelvoorkomende valkuilen en best‑practice tips

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| Rectangle appears off‑page | Coordinates are measured from the bottom‑left; using a top‑oriented coordinate system can cause confusion. | Remember that the Y‑axis grows upward. Use values that fit within the page size (`page.PageInfo.Width`, `page.PageInfo.Height`). |
| Shape is invisible | Fill opacity set to `0` or border width set to `0`. | Ensure `FillOpacity` is greater than `0` and `Border.Width` is at least `0.5`. |
| Saving throws `AccessDeniedException` | Output file is open in another program. | Close any viewers before running the code, or save to a different path. |
| Rectangle overlaps existing content | No layering control was set. | Use `ZIndex` property (higher values render on top) if you need to control layering. |

---

## De rechthoek uitbreiden – verlopen, rotatie en transparantie

Aspose.Pdf ondersteunt geavanceerde graphics. Om een geroteerde rechthoek met een lineair verloop te maken:

```csharp
Rectangle gradientRect = new Rectangle(bounds)
{
    // Gradient fill from left (blue) to right (green)
    FillColor = Color.Blue,
    FillColor2 = Color.Green,
    FillMode = FillMode.LinearGradient,
    // Rotate 45 degrees around the rectangle's center
    Rotation = 45
};
firstPage.Paragraphs.Add(gradientRect);
```

*Hetzelfde code‑patroon laat zien **hoe vorm te tekenen in PDF C#** met rijkere visuele effecten.*

---

## Het resultaat programmatisch verifiëren

Je kunt bevestigen dat de rechthoek is toegevoegd door het aantal alinea’s op de pagina te controleren:

```csharp
int shapeCount = firstPage.Paragraphs.Count;
Console.WriteLine($"Page 1 now contains {shapeCount} paragraph objects.");
```

Als het aantal met één is toegenomen na de invoeging, is de bewerking geslaagd.

---

## Conclusie

Je weet nu hoe je **een rechthoek aan PDF**‑bestanden toevoegt met C#. De tutorial behandelde het laden van een document, het definiëren van grenzen, het maken van een rechthoekvorm, het invoegen in een pagina en het opslaan van het resultaat. Je hebt ook gezien hoe je meerdere pagina’s behandelt, veelvoorkomende fouten voorkomt en geavanceerde styling toepast.

Ga vervolgens verder met gerelateerde onderwerpen zoals **hoe vorm te tekenen in PDF C#** voor cirkels, polygonen of vrije‑vorm paden, en leer vormen te combineren met tekst en afbeeldingen om volledig uitgeruste PDF‑rapporten te bouwen.

Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds Guide](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)
- [How to Add an Image Stamp to a PDF Using Aspose.PDF for .NET: A Comprehensive Guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [How to Add a Rotating Image Watermark to PDFs Using Aspose.PDF for .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}