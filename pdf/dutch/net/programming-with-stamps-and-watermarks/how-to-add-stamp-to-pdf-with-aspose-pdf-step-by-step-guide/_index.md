---
category: general
date: 2026-03-24
description: Hoe een stempel aan een PDF toe te voegen met Aspose.Pdf in C#. Leer
  hoe je een stempel‑PDF plaatst en een tekststempel‑PDF met automatische grootte
  toevoegt in een paar eenvoudige stappen.
draft: false
keywords:
- how to add stamp
- place stamp pdf
- add text stamp pdf
- Aspose.Pdf stamp example
- C# PDF annotation
language: nl
og_description: Hoe voeg je een stempel toe aan een PDF in C#? Deze gids laat zien
  hoe je een stempel in een PDF plaatst en een tekststempel toevoegt met automatische
  lettergrootte met behulp van Aspose.Pdf.
og_title: Hoe een stempel aan een PDF toevoegen met Aspose.Pdf – Snelle gids
tags:
- pdf
- csharp
- aspose
- stamping
title: Hoe een stempel aan een PDF toevoegen met Aspose.Pdf – Stapsgewijze handleiding
url: /nl/net/programming-with-stamps-and-watermarks/how-to-add-stamp-to-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een stempel aan een PDF toe te voegen met Aspose.Pdf – Stapsgewijze handleiding

**Hoe een stempel** aan een PDF toe te voegen is een veelvoorkomende behoefte wanneer je een document wilt branden, certificeren of simpelweg annoteren. Heb je je ooit afgevraagd wat de makkelijkste manier is om een stempel‑PDF te plaatsen zonder te worstelen met low‑level graphics? In deze tutorial lopen we een complete, kant‑klaar werkende oplossing door die niet alleen **laat zien hoe je een stempel toevoegt**, maar ook uitlegt *waarom* elke regel belangrijk is.

Je leert hoe je een **stempel‑PDF** op elke pagina kunt **plaatsen**, hoe je een **tekststempel‑PDF** maakt die automatisch krimpt om in zijn rechthoek te passen, en welke valkuilen je moet vermijden wanneer de tekst te lang is. Aan het einde heb je één C#‑bestand dat je in je project kunt dropen en direct PDF’s kunt gaan stempelen.

## Vereisten

Voordat we beginnen, zorg dat je het volgende hebt:

* .NET 6.0 of later (de code werkt ook met .NET Core en .NET Framework).
* Het Aspose.Pdf for .NET NuGet‑pakket (`Aspose.Pdf`) geïnstalleerd.
* Een PDF‑bestand met de naam `input.pdf` in een map die je kunt refereren (elke eenvoudige één‑pagina PDF volstaat).

Er is geen extra configuratie nodig—Aspose.Pdf handelt al het zware werk af.

## Stap 1: Het project opzetten en de bron‑PDF laden

Het eerste wat we nodig hebben is een `Document`‑object dat de PDF vertegenwoordigt die we willen annoteren. Beschouw het als het laden van een leeg canvas waarop we later een stempel gaan schilderen.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the source PDF document
// The using statement ensures the file is closed automatically.
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Waarom dit belangrijk is:** `Document` is het toegangspunt voor elke PDF‑manipulatie in Aspose.Pdf. Door het `using`‑patroon te gebruiken garanderen we dat de bestands­handle wordt vrijgegeven, waardoor lock‑problemen bij het later opslaan van de gewijzigde PDF worden voorkomen.

## Stap 2: Een tekststempel maken met automatisch aangepaste lettergrootte

Nu bouwen we een `TextStamp`. Het trucje dat dit voorbeeld onderscheidt is de vlag `AutoAdjustFontSizeToFitStampRectangle`—die vertelt Aspose de tekst te verkleinen totdat deze binnen de door ons gedefinieerde rechthoek past.

```csharp
// Create a text stamp that will automatically resize to fit its rectangle
var textStamp = new TextStamp("Long text that must fit")
{
    // Let Aspose shrink the text if it overflows
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Precision of the auto‑adjust algorithm (lower = more accurate)
    AutoAdjustFontSizePrecision = 0.01f,
    // Define the stamp's bounding box (in points)
    Width = 300,
    Height = 100,
    // Word‑wrap by whole words so we don’t split in the middle of a word
    WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
    // Optional: set background color or opacity if you want a visible box
    Background = new Background()
    {
        Color = Color.LightGray,
        Opacity = 0.5
    }
};
```

> **Pro‑tip:** Als je in plaats van tekst een logo of afbeelding nodig hebt, gebruik dan `ImageStamp`—dezelfde auto‑adjust‑logica bestaat voor het schalen van afbeeldingen.

## Stap 3: Bepalen waar je **stempel‑PDF** wilt **plaatsen** – eerste pagina, laatste pagina of aangepaste index

Aspose.Pdf slaat pagina’s op in een 1‑gebaseerde collectie (`pdfDocument.Pages[1]` is de eerste pagina). Je kunt **stempel‑PDF** op elke pagina plaatsen door de index aan te passen.

```csharp
// Place the stamp on the first page (index 1)
// To stamp the last page use pdfDocument.Pages[pdfDocument.Pages.Count]
pdfDocument.Pages[1].AddStamp(textStamp);
```

> **Waarom dit flexibel is:** Omdat de `Pages`‑collectie mutabel is, kun je door alle pagina’s lopen en dezelfde stempel aan elke toevoegen, of je kunt een specifieke pagina targeten op basis van bedrijfslogica (bijv. alleen de omslagpagina).

## Stap 4: Het gewijzigde document opslaan

Na het stempelen moet je de wijzigingen terug naar schijf schrijven. Je kunt het originele bestand overschrijven of een nieuw bestand aanmaken—het is jouw keuze.

```csharp
// Save the stamped PDF – change the path if you don’t want to overwrite
pdfDocument.Save("YOUR_DIRECTORY/output-stamped.pdf");
```

Wanneer je `output-stamped.pdf` opent, zie je een lichtgrijze rechthoek op de eerste pagina met de tekst “Long text that must fit”. Als de tekst langer zou zijn, zou Aspose deze automatisch verkleinen totdat hij perfect binnen de 300 × 100 pt‑rechthoek past.

## Volledig werkend voorbeeld

Hieronder staat het complete programma dat je kunt kopiëren‑plakken in een console‑app (`Program.cs`). Het bevat alle besproken onderdelen, plus een kleine helper om te verifiëren dat de stempel verschijnt.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;   // Needed for Background and Color

namespace PdfStampDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the source PDF
            using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

            // 2️⃣ Create a text stamp with auto‑adjusting font size
            var textStamp = new TextStamp("Long text that must fit")
            {
                AutoAdjustFontSizeToFitStampRectangle = true,
                AutoAdjustFontSizePrecision = 0.01f,
                Width = 300,
                Height = 100,
                WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
                Background = new Background()
                {
                    Color = Color.LightGray,
                    Opacity = 0.5
                }
            };

            // 3️⃣ Place the stamp on the first page (you can change the index)
            pdfDocument.Pages[1].AddStamp(textStamp);

            // 4️⃣ Save the result
            string outputPath = "YOUR_DIRECTORY/output-stamped.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Stamp added successfully! Check the file at: {outputPath}");
        }
    }
}
```

### Verwacht resultaat

* De PDF opent met een half‑transparante grijze doos op de eerste pagina.
* In de doos past de opgegeven tekst perfect, zelfs als je deze vervangt door een langere zin.
* Handmatige berekeningen van de lettergrootte zijn niet nodig—Aspose doet het zware werk.

## Veelvoorkomende valkuilen bij het **plaatsen van stempel‑PDF**

| Symptoom | Waarschijnlijke oorzaak | Oplossing |
|----------|--------------------------|-----------|
| Tekst wordt afgekapt | `AutoAdjustFontSizeToFitStampRectangle` is **false** of de rechthoek is te klein. | Schakel de vlag in en vergroot `Width`/`Height` of verkort de tekst. |
| Stempel staat niet gecentreerd | Standaard `HorizontalAlignment`/`VerticalAlignment` zijn `Left`/`Top`. | Stel `HorizontalAlignment = HorizontalAlignment.Center` en `VerticalAlignment = VerticalAlignment.Center` in. |
| Stempel is niet zichtbaar in sommige viewers | Achtergrond‑opacity is 0 of de stempelkleur komt overeen met de paginabackground. | Gebruik een contrasterende `Background.Color` of stel `Opacity` > 0.3 in. |
| Meerdere stempels overlappen | Stempels worden in een lus toegevoegd zonder de coördinaten aan te passen. | Gebruik `textStamp.XIndent` en `textStamp.YIndent` om elke stempel te verschuiven. |

Deze problemen vroegtijdig aanpakken bespaart je later veel debug‑werk.

## Uitbreiding van het voorbeeld: een afbeeldingstempel toevoegen

Als je zowel een **tekststempel‑PDF** *als* een afbeelding (bijv. een bedrijfslogo) nodig hebt, kun je beide combineren:

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    Width = 100,
    Height = 50,
    XIndent = 400,          // Position to the right of the text stamp
    YIndent = 20,
    Background = new Background()
    {
        Color = Color.Transparent
    }
};

pdfDocument.Pages[1].AddStamp(imageStamp);
```

Nu toont de pagina zowel een dynamische tekststempel als een statische afbeeldingstempel naast elkaar.

## Je implementatie testen

1. Voer de console‑app uit.  
2. Open `output-stamped.pdf` in Adobe Reader, Edge of een andere PDF‑viewer.  
3. Controleer of de stempelrechthoek aanwezig is en de tekst volledig zichtbaar is.  
4. Verander de tekst naar een langere zin, voer opnieuw uit, en bevestig dat de lettergrootte automatisch krimpt.

Als er iets niet klopt, controleer dan de afmetingen van de rechthoek en de instelling `AutoAdjustFontSizePrecision`.

## Conclusie

Je weet nu **hoe je een stempel** aan een PDF kunt toevoegen met Aspose.Pdf, hoe je **stempel‑PDF** op een specifieke pagina kunt **plaatsen**, en hoe je **tekststempel‑PDF** maakt die automatisch de lettergrootte aanpast. Het complete, uitvoerbare voorbeeld hierboven elimineert giswerk en biedt een solide basis voor meer geavanceerde stempel‑scenario’s—zoals batch‑verwerking van tientallen bestanden of conditioneel watermerken toevoegen.

Klaar voor de volgende stap? Probeer elke pagina in een lus te stempelen, experimenteer met verschillende lettertypen, of combineer afbeelding‑ en tekststempels om een professioneel uitziend zegel te maken. De mogelijkheden zijn eindeloos, en met Aspose.Pdf heb je een betrouwbaar motor onder de motorkap.

Als je ergens tegenaan loopt, laat dan een reactie achter of raadpleeg de Aspose.Pdf‑documentatie voor diepere aanpassingsopties. Veel plezier met stempelen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}