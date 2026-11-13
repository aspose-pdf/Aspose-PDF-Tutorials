---
category: general
date: 2026-11-12
description: Leer hoe je de PDF‑opaciteit kunt wijzigen met Aspose.Pdf, transparantie
  kunt toevoegen, de mengmodus kunt instellen en de gewijzigde PDF kunt opslaan in
  C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF opacity
- how to add transparency
- save modified PDF
- how to set blend mode
- set fill opacity
language: nl
lastmod: 2026-11-12
og_description: Wijzig de PDF‑opaciteit met Aspose.Pdf, leer hoe je transparantie
  toevoegt, de blend‑modus instelt en gewijzigde PDF‑bestanden opslaat in C#.
og_image_alt: Screenshot of a PDF page with altered opacity using Aspose.Pdf
og_title: PDF-opaciteit wijzigen met Aspose.Pdf – transparantie toevoegen en opslaan
schemas:
- author: Aspose
  dateModified: '2026-11-12'
  description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  headline: Change PDF opacity with Aspose.Pdf and save the file
  type: TechArticle
- description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  name: Change PDF opacity with Aspose.Pdf and save the file
  steps:
  - name: Load the PDF document
    text: Start by creating a `Document` instance that points to your source file.
      The constructor reads the entire PDF into memory, allowing you to manipulate
      its internal objects.
  - name: Access the first page’s resources
    text: Each PDF page stores a *resource dictionary* that holds objects such as
      fonts, images, and graphics states. You need to edit this dictionary to inject
      a new `ExtGState` entry.
  - name: Ensure an ExtGState dictionary exists
    text: The `ExtGState` dictionary holds custom graphics states. If it does not
      exist, the code creates one automatically.
  - name: Define a new graphics state (ExtGState)
    text: A graphics state defines how drawing operations behave. The following dictionary
      sets stroke opacity (`CA`), fill opacity (`ca`), and blend mode (`BM`).
  - name: Register the graphics state in the resource dictionary
    text: Give the new state a name (e.g., `GS0`) and add it to the `ExtGState` dictionary.
      This name will be referenced later in the page content stream.
  - name: Apply the graphics state to page content
    text: To actually see the opacity effect, insert the `/GS0 gs` operator before
      the drawing commands you want to affect. The example below draws a semi‑transparent
      rectangle.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The `Save` method overwrites
      the target file or creates a new one if it does not exist.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: PDF-opaciteit wijzigen met Aspose.Pdf en het bestand opslaan
url: /nl/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-and-save-the-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF‑opaciteit wijzigen met Aspose.Pdf en het bestand opslaan

Als je de **PDF‑opaciteit** in een document moet **wijzigen**, biedt Aspose.Pdf een eenvoudige API om zowel de lijn‑ als de vultransparantie aan te passen. Deze tutorial laat precies zien **hoe je transparantie toevoegt**, **hoe je een blend‑mode instelt**, en **gewijzigde PDF‑bestanden opslaat** met slechts een paar regels C#‑code.

Je doorloopt elke stap — van het laden van een bestaande PDF tot het definiëren van een nieuwe graphics state en het opslaan van de wijzigingen. Aan het einde van deze gids kun je:

* De zichtbaarheid van vector‑graphics of afbeeldingen verminderen.
* Een aangepaste blend‑mode toepassen, zoals *Normal* of *Multiply*.
* Het bijgewerkte bestand exporteren zonder andere inhoud te verliezen.

De enige vereiste is een werkende .NET‑ontwikkelomgeving en een referentie naar de Aspose.Pdf‑bibliotheek (versie 23.9 of later). Er zijn geen externe tools nodig.

## Vereisten

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| .NET 6.0 SDK of later | Garandeert compatibiliteit met de nieuwste Aspose.Pdf‑API's. |
| Aspose.Pdf for .NET NuGet‑pakket | Levert de `Document`, `CosPdfDictionary` en gerelateerde klassen die in de code worden gebruikt. |
| Een PDF‑bestand om te bewerken (bijv. `input.pdf`) | Dient als bron voor de opaciteitswijzigingen. |

Installeer het NuGet‑pakket met:

```bash
dotnet add package Aspose.Pdf
```

## PDF‑opaciteit wijzigen met Aspose.Pdf

### Stap 1: Laad het PDF‑document

Begin met het maken van een `Document`‑instantie die naar je bronbestand wijst. De constructor leest de volledige PDF in het geheugen, zodat je de interne objecten kunt manipuleren.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;

// Load the existing PDF
var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");
```

> **Waarom deze stap?** Het laden van het bestand creëert een manipuleerbaar objectmodel. Alle daaropvolgende wijzigingen werken op deze in‑memory‑representatie, waardoor het oorspronkelijke bestand onaangeroerd blijft totdat je expliciet opslaat.

### Stap 2: Toegang tot de resources van de eerste pagina

Elke PDF‑pagina bevat een *resource‑dictionary* die objecten zoals lettertypen, afbeeldingen en graphics states opslaat. Je moet deze dictionary bewerken om een nieuw `ExtGState`‑item toe te voegen.

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor simplifies access to the page's resource dictionary
var resourcesEditor = new DictionaryEditor(page.Resources);
```

> **Tip:** Als je PDF meerdere pagina's bevat die dezelfde opaciteit nodig hebben, herhaal deze stap voor elke pagina of deel één `ExtGState` over pagina's.

### Stap 3: Zorg dat er een ExtGState‑dictionary bestaat

De `ExtGState`‑dictionary bevat aangepaste graphics states. Als deze niet bestaat, maakt de code er automatisch één aan.

```csharp
// Get or create the ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                     ?? new CosPdfDictionary(pdfDoc);
resourcesEditor["ExtGState"] = extGStateDict;
```

> **Waarom deze stap?** Zonder een `ExtGState`‑container zou elke poging om naar een nieuwe graphics state te verwijzen mislukken, waardoor de PDF je opaciteitsinstellingen negeert.

### Stap 4: Definieer een nieuwe graphics state (ExtGState)

Een graphics state bepaalt hoe tekenbewerkingen zich gedragen. De volgende dictionary stelt de lijn‑opaciteit (`CA`), vul‑opaciteit (`ca`) en blend‑mode (`BM`) in.

```csharp
// Create an empty dictionary for the new graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Set desired parameters
var parameters = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (1 = opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (0.5 = 50% transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var param in parameters)
    newGraphicsState.Add(param);
```

> **Hoe vul‑opaciteit in te stellen:** Het `ca`‑item regelt de opaciteit van gevulde vormen (tekst, paden). Pas de numerieke waarde aan tussen `0` (volledig transparant) en `1` (volledig ondoorzichtig) om aan je ontwerpvereisten te voldoen.

> **Hoe blend‑mode in te stellen:** Het `BM`‑item selecteert het compositing‑algoritme. Veelvoorkomende waarden zijn `Normal`, `Multiply`, `Screen` en `Overlay`. Kies degene die past bij je visuele bedoeling.

### Stap 5: Registreer de graphics state in de resource‑dictionary

Geef de nieuwe state een naam (bijv. `GS0`) en voeg deze toe aan de `ExtGState`‑dictionary. Deze naam wordt later in de content‑stream van de pagina gebruikt.

```csharp
// Add the graphics state with a symbolic name
extGStateDict.Add("GS0", newGraphicsState);
```

> **Pro‑tip:** Gebruik een naamgevingsconventie zoals `GS0`, `GS1`, … wanneer je meerdere states maakt. Dit voorkomt naamconflicten en maakt debuggen eenvoudiger.

### Stap 6: Pas de graphics state toe op de paginacontent

Om het opaciteitseffect daadwerkelijk te zien, voeg je de `/GS0 gs`‑operator in vóór de tekenopdrachten die je wilt beïnvloeden. Het voorbeeld hieronder tekent een half‑transparante rechthoek.

```csharp
// Build a content stream that uses the new graphics state
var content = new MemoryStream();
var writer = new StreamWriter(content);

// Activate the graphics state
writer.WriteLine("q");                 // Save graphics state
writer.WriteLine("/GS0 gs");           // Apply custom ExtGState
writer.WriteLine("0.2 0.5 0.8 rg");    // Set fill color (RGB)
writer.WriteLine("100 500 200 100 re"); // Rectangle (x y width height)
writer.WriteLine("f");                 // Fill rectangle
writer.WriteLine("Q");                 // Restore graphics state
writer.Flush();

content.Position = 0;
page.Contents.Add(new ContentStream(content));
```

> **Waarom de `q` en `Q`‑operators?** Ze duwen en halen de graphics‑state‑stack, waardoor de opaciteitswijziging alleen de rechthoek beïnvloedt en niet de rest van de pagina.

### Stap 7: Sla de gewijzigde PDF op

Schrijf tenslotte het bijgewerkte document naar schijf. De `Save`‑methode overschrijft het doelbestand of maakt een nieuw bestand aan als het nog niet bestaat.

```csharp
// Persist the changes
pdfDoc.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **Hoe een gewijzigde PDF op te slaan:** De `Save`‑aanroep schrijft alle in‑memory‑wijzigingen, inclusief de nieuwe `ExtGState`, naar het opgegeven pad. Je kunt het resultaat ook naar een `MemoryStream` streamen voor web‑responses.

## Volledig werkend voorbeeld

Hieronder staat een enkel, zelfstandig programma dat elke stap hierboven beschrijft. Kopieer het naar een console‑applicatie en voer het uit om de opaciteitswijziging te verifiëren.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Operators;

class ChangePdfOpacityDemo
{
    static void Main()
    {
        // 1. Load the PDF
        var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");

        // 2. Get first page and its resources
        var page = pdfDoc.Pages[1];
        var resourcesEditor = new DictionaryEditor(page.Resources);

        // 3. Ensure ExtGState dictionary exists
        var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                             ?? new CosPdfDictionary(pdfDoc);
        resourcesEditor["Ext


## Wat kun je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe een gewijzigde PDF op te slaan met Aspose.Pdf en transparantie toe te voegen](/pdf/english/net/document-manipulation/how-to-save-modified-pdf-with-aspose-pdf-and-add-transparenc/)
- [Hoe transparantie toe te voegen aan PDF met Aspose.PDF in C#](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [Hoe een graphics state toe te voegen aan PDF en transparantie te regelen met Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}