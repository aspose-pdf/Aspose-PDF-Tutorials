---
category: general
date: 2026-09-27
description: Hoe tekst aan een PDF toevoegen met Aspose.PDF en tekst op PDF‑pagina’s
  positioneren. Volg deze stapsgewijze handleiding om efficiënt tekst in een PDF‑pagina
  in te voegen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to add text pdf
- position text in pdf
- insert text pdf page
- aspose pdf add text
- access specific pdf page
language: nl
lastmod: 2026-09-27
og_description: Hoe tekst aan een PDF toe te voegen met Aspose.PDF. Leer hoe je tekst
  in een PDF positioneert, tekst op een PDF-pagina invoegt en een specifieke PDF-pagina
  benadert, met duidelijke codevoorbeelden.
og_image_alt: Screenshot showing how to add text PDF with Aspose.PDF in C#
og_title: Hoe tekst toe te voegen aan PDF met Aspose.PDF – volledige C#-gids
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: How to add text PDF using Aspose.PDF and position text in PDF pages.
    Follow this step‑by‑step guide to insert text PDF page efficiently.
  headline: How to add text PDF with Aspose.PDF in C#
  type: TechArticle
- description: How to add text PDF using Aspose.PDF and position text in PDF pages.
    Follow this step‑by‑step guide to insert text PDF page efficiently.
  name: How to add text PDF with Aspose.PDF in C#
  steps:
  - name: Load the PDF document
    text: '```csharp // Step 1: Load the PDF document var document = new Aspose.Pdf.Document("YOUR_DIRECTORY/input.pdf");
      ```'
  - name: Access the specific PDF page
    text: '```csharp // Step 2: Access the second page (index starts at 1) var page
      = document.Pages[1]; ```'
  - name: Position text in PDF
    text: '```csharp // Step 3: Create a tagged content element positioned at (100,
      200) on the page var taggedContent = new Aspose.Pdf.TaggedContent(page) { X
      = 100, Y = 200 }; ```'
  - name: Insert text PDF page
    text: '```csharp // Step 4: Add a text fragment to the tagged content taggedContent.Add(new
      Aspose.Pdf.Text.TextFragment("Important")); ```'
  - name: Save the modified PDF
    text: '```csharp // Step 5: Save the modified PDF document.Save("YOUR_DIRECTORY/output.pdf");
      ```'
  - name: Expected output
    text: 'When you open `output.pdf`:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Hoe tekst aan een PDF toe te voegen met Aspose.PDF in C#
url: /nl/net/programming-with-text/how-to-add-text-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe tekst toevoegen aan PDF met Aspose.PDF in C#

Als je **tekst aan PDF wilt toevoegen** op een programmeerbare manier, laat deze gids je precies zien hoe je dat doet met Aspose.PDF voor .NET. Je leert tekst positioneren in PDF, tekst op een PDF‑pagina invoegen en een specifieke PDF‑pagina openen zonder je IDE te verlaten.

De tutorial behandelt alles, van het installeren van de bibliotheek tot het opslaan van het uiteindelijke document, zodat je de code kunt kopiëren en meteen kunt uitvoeren. Er zijn geen externe referenties nodig—alleen de onderstaande stappen.

## Vereisten

* .NET 6.0 (of later) geïnstalleerd.
* Visual Studio 2022 of een andere C#‑compatibele IDE.
* Een Aspose.PDF for .NET NuGet‑pakket (`Aspose.Pdf`) toegevoegd aan je project.
* Een bron‑PDF‑bestand (`input.pdf`) geplaatst in een bekende map.

Deze vereisten zorgen ervoor dat de code compileert en de PDF‑manipulatie werkt zoals verwacht.

## Hoe tekst toevoegen aan PDF met Aspose.PDF

De volgende secties splitsen het proces op in afzonderlijke, gemakkelijk te volgen stappen. Elke stap legt **waarom** het belangrijk is uit, niet alleen **wat** je moet typen.

### Stap 1: Laad het PDF‑document

```csharp
// Step 1: Load the PDF document
var document = new Aspose.Pdf.Document("YOUR_DIRECTORY/input.pdf");
```

**Waarom dit belangrijk is:** Het laden van het document maakt een in‑memory representatie die Aspose.PDF kan wijzigen. Zonder dit object kun je geen pagina's benaderen of inhoud toevoegen.

### Stap 2: Benader de specifieke PDF‑pagina

```csharp
// Step 2: Access the second page (index starts at 1)
var page = document.Pages[1];
```

**Waarom dit belangrijk is:** PDF‑pagina's zijn 1‑gebaseerd in Aspose.PDF, dus `Pages[1]` geeft de tweede pagina terug. Het gebruiken van de juiste index is essentieel wanneer je een **specifieke PDF‑pagina wilt benaderen** voor bewerking.

### Stap 3: Positioneer tekst in PDF

```csharp
// Step 3: Create a tagged content element positioned at (100, 200) on the page
var taggedContent = new Aspose.Pdf.TaggedContent(page) { X = 100, Y = 200 };
```

**Waarom dit belangrijk is:** De `X`‑ en `Y`‑eigenschappen definiëren de linker‑onderhoek van de tekst in punten (1 pt ≈ 1/72 in). Het aanpassen van deze waarden stelt je in staat om **tekst in PDF te positioneren** precies waar je wilt.

### Stap 4: Voeg tekst toe aan PDF‑pagina

```csharp
// Step 4: Add a text fragment to the tagged content
taggedContent.Add(new Aspose.Pdf.Text.TextFragment("Important"));
```

**Waarom dit belangrijk is:** `TextFragment` vertegenwoordigt een reeks tekens. Het toevoegen aan het `TaggedContent`‑element voegt daadwerkelijk **tekst toe aan de PDF‑pagina** op de coördinaten die in de vorige stap zijn ingesteld.

### Stap 5: Sla de gewijzigde PDF op

```csharp
// Step 5: Save the modified PDF
document.Save("YOUR_DIRECTORY/output.pdf");
```

**Waarom dit belangrijk is:** Het opslaan van de wijzigingen schrijft het nieuwe PDF‑bestand naar de schijf. Het uitvoerbestand bevat nu het woord “Important” op de tweede pagina op de exacte locatie die je hebt opgegeven.

## Volledig, uitvoerbaar voorbeeld

Hieronder staat het volledige programma dat je kunt kopiëren‑plakken in een console‑applicatie. Het bevat alle benodigde `using`‑directieven en commentaren voor duidelijkheid.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

namespace PdfTextAdder
{
    class Program
    {
        static void Main()
        {
            // Load the existing PDF
            var document = new Document("YOUR_DIRECTORY/input.pdf");

            // Access the second page (index starts at 1)
            var page = document.Pages[1];

            // Create a tagged content element at (100, 200)
            var taggedContent = new TaggedContent(page) { X = 100, Y = 200 };

            // Add the text fragment "Important"
            taggedContent.Add(new TextFragment("Important"));

            // Save the result
            document.Save("YOUR_DIRECTORY/output.pdf");

            Console.WriteLine("Text added successfully. Check output.pdf.");
        }
    }
}
```

### Verwachte output

Wanneer je `output.pdf` opent:

* De tweede pagina bevat het woord **Important** gepositioneerd 100 pt vanaf de linkerrand en 200 pt vanaf de onderrand.
* Alle andere pagina's blijven ongewijzigd.

Als de coördinaten de tekst buiten de paginagrenzen plaatsen, wordt de tekst bijgesneden. Pas `X` en `Y` dienovereenkomstig aan.

## Veelvoorkomende variaties en randgevallen

| Situatie | Hoe te handelen |
|-----------|-----------------|
| **Ander paginanummer** | Verander `document.Pages[1]` naar de gewenste 1‑gebaseerde index. |
| **Meerdere tekstfragmenten** | Roep `taggedContent.Add(new TextFragment("First"));` aan, gevolgd door extra `Add`‑aanroepen. |
| **Lettertype‑stijl wijzigen** | Maak een `TextFragment`, stel zijn `TextState.Font` en `TextState.FontSize` in, en voeg het vervolgens toe aan `taggedContent`. |
| **Gedraaide tekst** | Stel `taggedContent.Rotation = 90;` in voordat je het fragment toevoegt. |
| **Grote PDF‑bestanden** | Laad het document met `Document.LoadOptions` om geheugen‑efficiënte streaming mogelijk te maken. |

Deze variaties laten je het basis **aspose pdf add text**‑patroon uitbreiden om aan complexere eisen te voldoen.

## Pro‑tips

* **Coördinatensysteem:** PDF gebruikt een oorsprong links‑onder. Als je gewend bent aan coördinaten links‑boven (bijv. in HTML), trek dan de Y‑waarde af van de paginahoogte.
* **Prestaties:** Hergebruik een enkele `Document`‑instantie bij het verwerken van veel pagina's om herhaaldelijk bestand‑I/O te vermijden.
* **Veiligheid:** Werk altijd met een kopie van de originele PDF om het bronbestand te behouden.

## Conclusie

Je weet nu **hoe je tekst aan een PDF kunt toevoegen** met Aspose.PDF, hoe je **tekst in PDF kunt positioneren**, hoe je **tekst aan een PDF‑pagina kunt invoegen**, en hoe je **een specifieke PDF‑pagina kunt benaderen**. Door de bovenstaande stappen te volgen kun je elke tekenreeks op elke locatie in een PDF‑document programmatically invoegen.

Klaar om meer te ontdekken? Probeer afbeeldingen toe te voegen, vormen te tekenen of tabellen te maken met Aspose.PDF. Elk van die onderwerpen bouwt voort op dezelfde principes die je zojuist onder de knie hebt.

---

![voorbeeld van tekst toevoegen aan PDF](image.png)


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe een tekststempel toevoegen aan PDF met Aspose.PDF .NET: Uitgebreide gids](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)
- [Hoe tekst roteren in PDF's met Aspose.PDF voor .NET: Een stapsgewijze gids](/pdf/english/net/text-operations/rotate-text-aspose-pdf-net-guide/)
- [Tekst toevoegen, bewerken en extraheren met Aspose.PDF voor .NET](/pdf/english/net/programming-with-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}