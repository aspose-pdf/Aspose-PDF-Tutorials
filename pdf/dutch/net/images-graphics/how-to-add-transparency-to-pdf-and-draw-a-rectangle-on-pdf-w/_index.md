---
category: general
date: 2026-09-12
description: Leer hoe je transparantie aan een PDF toevoegt, een rechthoek op een
  PDF tekent en een PDF met transparantie opslaat met Aspose.PDF in C# – stap‑voor‑stap
  gids.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- draw rectangle on pdf
- save pdf with transparency
language: nl
lastmod: 2026-09-12
og_description: Voeg transparantie toe aan PDF, teken een rechthoek op PDF en sla
  PDF op met transparantie met behulp van Aspose.PDF in C#. Volg deze volledige tutorial.
og_image_alt: Screenshot of a PDF page showing a semi‑transparent rectangle drawn
  with Aspose.PDF
og_title: Transparantie toevoegen aan PDF en een rechthoek tekenen op PDF – volledige
  C#‑gids
schemas:
- author: Aspose
  dateModified: '2026-09-12'
  description: Learn how to add transparency to PDF, draw a rectangle on PDF, and
    save PDF with transparency using Aspose.PDF in C# – step‑by‑step guide.
  headline: How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Hoe transparantie toe te voegen aan een PDF en een rechthoek te tekenen op
  een PDF met Aspose.PDF
url: /nl/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe transparantie toe te voegen aan PDF en een rechthoek te tekenen op PDF met Aspose.PDF

Als je **transparantie wilt toevoegen aan PDF**-bestanden, laat deze gids je precies zien hoe je dat in C# doet. Je leert ook hoe je een **rechthoek op PDF tekent** en uiteindelijk **PDF opslaat met transparantie**, zodat het resultaat kan worden hergebruikt in rapporten, facturen of elke document‑automatiseringsworkflow.

In deze tutorial zul je:

* Een bestaand PDF-document laden.
* Een aangepaste graphics state maken die de lijn- en vulopaciteit definieert.
* Die graphics state toepassen op het canvas en een rechthoek tekenen.
* Het gewijzigde bestand opslaan terwijl de transparantie‑instellingen behouden blijven.

Er zijn geen externe tools nodig, behalve de Aspose.PDF for .NET-bibliotheek, en elke regel code wordt uitgelegd zodat je begrijpt *waarom* elke stap belangrijk is.

## Vereisten

* .NET 6.0 of hoger (de code werkt ook met .NET Framework 4.7+).
* Een gelicentieerde of evaluatiekopie van **Aspose.PDF for .NET**. Installeer deze via NuGet:

```bash
dotnet add package Aspose.Pdf
```

* Een invoer‑PDF (`input.pdf`) geplaatst in een map die je vanuit je project kunt refereren.

## Stap 1: Laad het PDF‑document

De eerste handeling is het openen van het bronbestand. Het gebruik van de `using`‑statement garandeert dat het document correct wordt vrijgegeven, waardoor later bij het opslaan geen bestandsvergrendelingsproblemen ontstaan.

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";
using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

*Waarom dit belangrijk is*: Het laden van het document geeft je toegang tot de paginaverzameling, resource‑dictionaries en canvas‑objecten die nodig zijn voor het tekenen.

## Stap 2: Toegang tot de resource‑dictionary van de eerste pagina

Elke PDF-pagina heeft een **resource‑dictionary** die objecten zoals lettertypen, afbeeldingen en graphics states opslaat. Om een nieuwe transparantie‑instelling toe te voegen, moeten we de `ExtGState`‑vermelding bewerken.

```csharp
// Step 2: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

*Waarom dit belangrijk is*: De `DictionaryEditor` stelt ons in staat low‑level PDF‑objecten te lezen en te wijzigen zonder de documentstructuur te breken.

## Stap 3: Maak een aangepaste graphics state met transparantiewaarden

Een graphics state (`ExtGState`) bepaalt hoe tekenbewerkingen worden gerenderd. We definiëren twee opaciteitsparameters:

* **CA** – lijn‑opaciteit (de omtrek van vormen).
* **ca** – vul‑opaciteit (de binnenkant van vormen).

We stellen ook de blend‑mode (`BM`) in op “Normal”, wat de meest voorkomende compositie‑operatie is.

```csharp
// Step 3: Create a custom graphics state (ExtGState) with transparency settings
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
var customGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "CA", new Aspose.Pdf.Cos.CosPdfNumber(1)),          // stroke opacity = 100 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),        // fill opacity = 50 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))      // normal blend mode
};

foreach (var p in parameters)
    customGs.Add(p);

// Register the new graphics state under the name "GS0"
extGStateDict.Add("GS0", customGs);
```

*Waarom dit belangrijk is*: Door `GS0` toe te voegen aan de `ExtGState`‑dictionary creëren we een herbruikbare referentie die het canvas kan activeren vóór het tekenen. De vul‑opaciteit van `0.5` maakt de rechthoek semi‑transparant, waardoor het doel **transparantie toevoegen aan PDF** wordt bereikt.

## Stap 4: Pas de graphics state toe en teken een rechthoek

Nu laten we het canvas van de pagina de graphics state die we zojuist hebben gemaakt gebruiken, en vervolgens tekenen we een rechthoek. De coördinaten volgen het PDF‑coördinatensysteem (oorsprong in de linker‑onderhoek).

```csharp
// Step 4: Apply the custom graphics state and draw a rectangle
var canvas = firstPage.Canvas;

// Activate the transparency graphics state
canvas.SetGraphicsState("GS0");

// Draw a rectangle from (100, 500) to (200, 600)
canvas.Rectangle(100, 500, 200, 600);

// Render the rectangle outline using the current graphics state
canvas.Stroke();
```

*Waarom dit belangrijk is*: `SetGraphicsState("GS0")` schakelt de tekencontext over naar de eerder gedefinieerde transparantie‑instellingen. De `Rectangle`‑methode definieert de vorm, en `Stroke` rendert de omtrek met de opgegeven opaciteit. Als je ook een gevulde rechthoek wilt, vervang dan `Stroke()` door `FillAndStroke()`.

## Stap 5: Sla de gewijzigde PDF op terwijl je transparantie behoudt

Tot slot schrijf je het document terug naar de schijf. Het uitvoerbestand bevat de nieuwe graphics state, de getekende rechthoek en de transparantie‑informatie.

```csharp
// Step 5: Save the modified PDF
string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
pdfDocument.Save(outputPath);
```

*Waarom dit belangrijk is*: Het opslaan van het document maakt alle wijzigingen definitief. Het resulterende bestand kan worden geopend in elke PDF‑viewer, en de rechthoek zal verschijnen met 50 % vul‑opaciteit.

### Verwacht resultaat

Wanneer je `output_with_extgstate.pdf` opent, zou je een rechthoek moeten zien waarvan de rand volledig ondoorzichtig is en waarvan de binnenkant semi‑transparant is, zodat onderliggende paginainhoud erdoorheen zichtbaar wordt.

## Randgevallen en praktische tips

| Situatie | Aanbevolen aanpassing |
|-----------|------------------------|
| **Meerdere pagina's** | Loop over `pdfDocument.Pages` en herhaal stappen 2‑4 voor elke doelpagina. |
| **Verschillende opaciteitswaarden** | Wijzig de `CosPdfNumber`‑waarden voor `CA` (lijn) en `ca` (vulling) naar elk getal tussen `0` (volledig transparant) en `1` (volledig ondoorzichtig). |
| **Aangepaste blend‑modi** | Vervang `"Normal"` door `"Multiply"`, `"Screen"` of een andere PDF‑standaard blend‑mode die door je viewer wordt ondersteund. |
| **Gevulde rechthoek** | Roep `canvas.FillAndStroke()` aan in plaats van `canvas.Stroke()` om zowel vulling als omtrek toe te passen. |
| **Herhaald gebruik van dezelfde graphics state** | Je kunt `canvas.SetGraphicsState("GS0")` aanroepen voordat je een willekeurig aantal vormen op dezelfde pagina tekent. |

**Pro tip:** Inspecteer altijd de resource‑dictionary na het toevoegen van een nieuwe `ExtGState`. Als de dictionary niet bestaat, maak deze dan eerst aan:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
    resourcesEditor.Add("ExtGState", new Aspose.Pdf.Cos.CosPdfDictionary(pdfDocument));
```

## Volledig, uitvoerbaar voorbeeld

Hieronder staat een zelfstandig programma dat je kunt kopiëren naar een console‑applicatie en direct kunt uitvoeren (vervang `YOUR_DIRECTORY` door een daadwerkelijk pad).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF document
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Access the first page’s resources
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        if (!resourcesEditor.ContainsKey("ExtGState"))
            resourcesEditor.Add("ExtGState", new CosPdfDictionary(pdfDocument));

        // 3️⃣ Create a custom graphics state with transparency
        var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        var customGs = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };

        foreach (var p in parameters)
            customGs.Add(p);

        extGStateDict.Add("GS0", customGs);

        // 4️⃣ Apply the graphics state and draw a rectangle
        var canvas = firstPage.Canvas;
        canvas.SetGraphicsState("GS0");
        canvas.Rectangle(100, 500, 200, 600);
        canvas.Stroke(); // use FillAndStroke() for a filled shape

        // 5️⃣ Save the PDF with transparency
        string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine("PDF saved with a transparent rectangle at: " + outputPath);
    }
}
```

Het uitvoeren van het programma genereert `output_with_extgstate.pdf`, wat **transparantie toevoegen aan PDF**, **rechthoek op PDF tekenen** en **PDF opslaan met transparantie** allemaal in één stroom demonstreert.

## Conclusie

Je weet nu hoe je **transparantie kunt toevoegen aan PDF**‑bestanden, **een rechthoek op PDF kunt tekenen**, en **PDF kunt opslaan met transparantie** met behulp van Aspose.PDF for .NET. Het proces draait om het maken van een aangepaste `ExtGState`, deze toepassen op het canvas en de wijzigingen opslaan. Met deze bouwblokken kun je de techniek uitbreiden naar andere vormen, meerdere pagina's of dynamische opaciteitswaarden.

**Volgende stappen**

* Verken andere teken‑primitieven zoals `canvas.Ellipse`, `canvas.Path` of `canvas.TextFragment` terwijl je dezelfde graphics state hergebruikt.
* Combineer transparantie met afbeelding‑overlays om watermerken te maken (`canvas.Image` + aangepaste `ExtGState`).
* Bekijk de Aspose.PDF‑documentatie over **graphics state parameters** voor geavanceerde compositie‑effecten.

Veel plezier met coderen, en geniet van de visuele flexibiliteit die transparantie aan je PDF‑workflows toevoegt!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe PDF te maken in C# – Pagina toevoegen, rechthoek tekenen & opslaan](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [Hoe een lijnobject toe te voegen in PDF met Aspose.PDF for .NET: Een stapsgewijze handleiding](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Afbeeldingsstempels toevoegen aan PDF's met Aspose.PDF for .NET: Een stapsgewijze handleiding](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}