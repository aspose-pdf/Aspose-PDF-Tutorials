---
category: general
date: 2026-08-20
description: Maak een aangepaste grafische toestand in PDF met Aspose.Pdf. Leer hoe
  je PDF‑resources bewerkt en transparantie toevoegt aan PDF in slechts een paar stappen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom graphics state
- edit pdf resources
- add transparency pdf
- Aspose.Pdf graphics state
- PDF resource dictionary
language: nl
lastmod: 2026-08-20
og_description: Maak een aangepaste grafische toestand in PDF met Aspose.Pdf. Deze
  tutorial laat zien hoe je PDF‑resources bewerkt en snel transparantie aan een PDF
  toevoegt.
og_image_alt: Screenshot of C# code that creates a custom graphics state in a PDF
og_title: Aangepaste grafische toestand maken in PDF – Aspose.Pdf‑gids
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create custom graphics state in PDF with Aspose.Pdf. Learn how to edit
    PDF resources and add transparency PDF in just a few steps.
  headline: Create custom graphics state in PDF using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- Aspose.Pdf
- C#
- Graphics state
title: Aangepaste grafische toestand maken in PDF met Aspose.Pdf
url: /nl/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aangepaste graphics state maken in PDF met Aspose.Pdf

Als je een **aangepaste graphics state** in een PDF moet **maken**, laat deze gids je precies zien hoe je dat doet met Aspose.Pdf voor .NET. Aan het einde van de tutorial kun je **PDF‑resources bewerken**, een nieuw graphics‑state‑woordenboek injecteren en **transparantie‑PDF**‑inhoud toevoegen zonder je C#‑project te verlaten.

Je ziet een compleet, uitvoerbaar voorbeeld, een uitleg waarom elke regel belangrijk is, en tips voor het omgaan met documenten met meerdere pagina’s of verschillende blend‑modi. Er zijn geen externe tools nodig – alleen de Aspose.Pdf‑bibliotheek en een basis .NET‑ontwikkelomgeving.

## Prerequisites

Voordat je begint, zorg dat je het volgende hebt:

* .NET 6.0 of later (de code werkt ook met .NET Framework 4.7+)
* Een gelicentieerde kopie van **Aspose.Pdf for .NET** (de gratis proefversie werkt voor testen)
* Een invoer‑PDF‑bestand genaamd `input.pdf` geplaatst in een map die je vanuit code kunt refereren
* Visual Studio 2022 of een andere IDE die C#‑ontwikkeling ondersteunt

De tutorial gaat ervan uit dat je bekend bent met basis C#‑syntaxis en het concept van PDF‑pagina’s.

## Stap 1: Laad de bron‑PDF en krijg toegang tot de eerste pagina

De eerste handeling is het openen van het PDF‑bestand en het ophalen van de pagina waarvan je de resources wilt aanpassen. Aspose.Pdf vertegenwoordigt elke pagina als een `Page`‑object, en elke pagina bevat een **resource‑dictionary** die graphics states, fonts, XObjects en meer opslaat.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

// Load the PDF you want to edit
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Get the first page (pages are 1‑based in Aspose.Pdf)
    Page firstPage = pdfDocument.Pages[1];
```

*Waarom dit belangrijk is:* De `Document`‑klasse laadt het bestand in het geheugen, en `Pages[1]` geeft je directe toegang tot de resource‑dictionary van de eerste pagina, waar een graphics state zich bevindt.

## Stap 2: Open de resource‑dictionary voor bewerking

Aspose.Pdf biedt een `DictionaryEditor`‑helper waarmee je een resource‑dictionary kunt behandelen als een gewone .NET `Dictionary`. Dit maakt het eenvoudig om items zoals `ExtGState` te lezen, toe te voegen of te vervangen.

```csharp
    // Create an editor for the page’s resources
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Waarom dit belangrijk is:* `DictionaryEditor` abstraheert de low‑level COS‑objecten, zodat je kunt werken met bekende sleutel/waarde‑paren terwijl je toch PDF‑conformiteit behoudt.

## Stap 3: Haal (of maak) het ExtGState‑woordenboek op

Het **ExtGState**‑item bevat alle externe graphics‑state‑objecten voor de pagina. Als het woordenboek niet bestaat, maakt Aspose.Pdf er een leeg exemplaar voor je aan.

```csharp
    // Ensure the ExtGState dictionary exists
    var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
        ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
        : new CosPdfDictionary(pdfDocument);
```

*Waarom dit belangrijk is:* Een ontbrekend `ExtGState`‑item zou later een `KeyNotFoundException` veroorzaken. Deze controle zorgt ervoor dat de code werkt op PDF’s die nog nooit een aangepaste graphics state hebben gedefinieerd – een essentieel onderdeel van de robuustheid van **PDF‑resources bewerken**.

## Stap 4: Bouw het aangepaste graphics‑state‑woordenboek

Een graphics state beschrijft hoe teken‑operaties worden gerenderd. Om **transparantie‑PDF** toe te voegen, moet je de `ca` (vullings‑opacity) en `CA` (stroke‑opacity) items instellen, en eventueel een blend‑mode (`BM`). De volgende code bouwt een nieuw woordenboek met die parameters.

```csharp
    // Create an empty dictionary that will become the new graphics state
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Define the parameters you want for the custom state
    var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
    {
        // Stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        // Fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        // Blend mode – "Normal" is the default, but you can use "Multiply", "Screen", etc.
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };

    // Populate the dictionary with the parameters
    foreach (var param in graphicsStateParams)
        newGraphicsState.Add(param);
```

*Waarom dit belangrijk is:* De `ca`‑ en `CA`‑items regelen respectievelijk de transparantie voor vulling en lijn. Het instellen van `BM` laat je experimenteren met verschillende compositing‑effecten, wat nuttig is wanneer je later **transparantie‑PDF**‑inhoud toevoegt, zoals half‑transparante vormen of afbeeldingen.

## Stap 5: Registreer de nieuwe graphics state onder een unieke naam

Elke graphics state in het `ExtGState`‑woordenboek moet een unieke naam hebben (bijv. `GS0`, `GS1`). Je kunt elke naam kiezen die niet conflicteert met bestaande items.

```csharp
    // Choose a name that is unlikely to collide with existing states
    const string graphicsStateName = "GS0";

    // Add the new graphics state to the ExtGState dictionary
    extGStateDict.Add(graphicsStateName, newGraphicsState);

    // If the ExtGState entry was missing, attach it back to the page resources
    if (!resourcesEditor.ContainsKey("ExtGState"))
        resourcesEditor["ExtGState"] = extGStateDict;
```

*Waarom dit belangrijk is:* Door het nieuwe woordenboek onder `GS0` in te voegen, maak je de state aanspreekbaar vanuit de content‑streams van de pagina. Het voorwaardelijke blok zorgt ervoor dat het `ExtGState`‑item aanwezig is, zelfs voor PDF’s die zonder een dergelijk item zijn begonnen – een extra **PDF‑resources bewerken**‑bescherming.

## Stap 6: Gebruik de aangepaste graphics state in de paginacontent (optioneel)

De vorige stappen definiëren alleen de graphics state. Om het effect daadwerkelijk te zien, moet je ernaar verwijzen in de content‑stream van de pagina. Hieronder een kort voorbeeld dat een half‑transparante rechthoek tekent met de state die we zojuist hebben aangemaakt.

```csharp
    // Get the page’s content stream (or create a new one if empty)
    var content = firstPage.Contents[1];
    var graphics = new ContentWriter(content);

    // Save current graphics state
    graphics.WriteOperator(OperatorName.SaveState);
    // Set the custom graphics state we just defined
    graphics.WriteOperand($"/{graphicsStateName}");
    graphics.WriteOperator(OperatorName.SetExtGState);
    // Draw a rectangle (coordinates are in points)
    graphics.WriteOperand(100);   // lower‑left x
    graphics.WriteOperand(500);   // lower‑left y
    graphics.WriteOperand(200);   // width
    graphics.WriteOperand(100);   // height
    graphics.WriteOperator(OperatorName.Rectangle);
    // Fill the rectangle using the current fill opacity (ca = 0.5)
    graphics.WriteOperator(OperatorName.Fill);
    // Restore the previous graphics state
    graphics.WriteOperator(OperatorName.RestoreState);
```

*Waarom dit belangrijk is:* De `SetExtGState`‑operator (`gs`) vertelt de PDF‑renderer de parameters toe te passen die in `GS0` zijn gedefinieerd. De rechthoek verschijnt met 50 % vullings‑opacity terwijl de lijn volledig ondoorzichtig blijft.

## Stap 7: Sla de gewijzigde PDF op

Schrijf tenslotte de wijzigingen terug naar de schijf. Je kunt het oorspronkelijke bestand overschrijven of een nieuw bestand aanmaken.

```csharp
    // Save the updated PDF
    pdfDocument.Save("YOUR_DIRECTORY/output_with_custom_gs.pdf");
}
```

Wanneer je `output_with_custom_gs.pdf` opent in een PDF‑viewer, zou je een half‑transparante rechthoek op de eerste pagina moeten zien. Dit bevestigt dat je succesvol **aangepaste graphics state hebt gemaakt**, **PDF‑resources hebt bewerkt**, en **transparantie‑PDF**‑inhoud hebt toegevoegd.

## Veelvoorkomende variaties en randgevallen

| Situatie | Wat aan te passen |
|-----------|-------------------|
| **Meerdere pagina’s hebben dezelfde state nodig** | Registreer de graphics state één keer (stappen 1‑5) en verwijs naar `GS0` in de content‑stream van elke gewenste pagina. |
| **Verschillende opacity per element** | Definieer extra states (`GS1`, `GS2`, …) met verschillende `ca`/`CA`‑waarden en schakel tussen hen met `SetExtGState`. |
| **Blend‑mode anders dan Normal** | Vervang `"Normal"` door `"Multiply"`, `"Screen"` of een andere PDF‑standaard blend‑mode in het `BM`‑item. |
| **Naamconflict** | Controleer vóór het toevoegen of `extGStateDict.ContainsKey(yourName)` en kies een unieke suffix indien nodig. |
| **PDF bevat al een ExtGState‑woordenboek** | De code in Stap 3 hergebruikt het bestaande woordenboek, dus er is geen extra handling nodig. |

**Pro‑tip:** Bij het werken met grote PDF’s, wikkel het gebruik van `Document` in een `using`‑blok (zoals getoond) om native resources snel vrij te geven. Overweeg bovendien om de `PdfCompliance`‑eigenschap van Aspose.Pdf in te schakelen als je PDF/A‑ of PDF/X‑conformiteit moet garanderen na het bewerken van resources.

## Volledig werkend voorbeeld

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Load the PDF you want to edit
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 1: Get the first page
            Page firstPage = pdfDocument.Pages[1];

            // Step 2: Open the page resources for editing
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 3: Retrieve or create the ExtGState dictionary
            var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
                ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
                : new CosPdfDictionary(pdfDocument);

            // Step 4: Build a custom graphics state (50 % fill opacity, 100 % stroke opacity)
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var param in graphicsStateParams)
                newGraphicsState.Add(param);

            // Step 5: Register the graphics state under the name GS0
            const string graphicsStateName = "GS0";
            extGStateDict.Add(graphicsStateName, newGraphics


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Create PDF with Aspose – Add Form Field and Pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [How to Create Custom Tables in PDFs Using Aspose.PDF .NET](/pdf/english/net/tables-lists/create-custom-tables-in-pdfs-aspose-pdf-dot-net/)
- [Create Custom Pdf Stamps Aspose Pdf Net](/pdf/hongkong/net/images-graphics/create-custom-pdf-stamps-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}