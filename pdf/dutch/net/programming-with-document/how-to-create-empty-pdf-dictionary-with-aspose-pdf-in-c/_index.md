---
category: general
date: 2026-09-18
description: Leer hoe je een lege PDF-dictionary maakt in C# met Aspose.PDF. Deze
  stapsgewijze gids behandelt ExtGState, grafische toestand en CosPdfDictionary-manipulatie.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.PDF
- ExtGState dictionary
- graphics state
- CosPdfDictionary
- PDF manipulation C#
language: nl
lastmod: 2026-09-18
og_description: Maak een leeg PDF-woordenboek in C# met Aspose.PDF. Volg deze uitgebreide
  tutorial om ExtGState- en graphics state-woordenboeken te bewerken.
og_image_alt: Screenshot showing creation of an empty PDF dictionary in C#
og_title: Maak een leeg PDF‑woordenboek in C# – volledige Aspose.PDF‑gids
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn to create empty PDF dictionary in C# using Aspose.PDF. This step‑by‑step
    guide covers ExtGState, graphics state, and CosPdfDictionary manipulation.
  headline: How to create empty PDF dictionary with Aspose.PDF in C#
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: Hoe maak je een lege PDF-dictionary met Aspose.PDF in C#
url: /nl/net/programming-with-document/how-to-create-empty-pdf-dictionary-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe maak je een leeg PDF-dictionary met Aspose.PDF in C#

Als je een **leeg PDF-dictionary** moet **maken** tijdens het verwerken van een PDF‑bestand, laat deze gids je precies zien hoe je dit doet met Aspose.PDF voor .NET. Of je nu transparantie, blend‑modi of een aangepaste graphics‑state aanpast, de onderstaande stappen laten je de `ExtGState`‑dictionary veilig en efficiënt bewerken.

In deze tutorial leer je:

* Een PDF‑document laden met Aspose.PDF.
* De resources van de eerste pagina en de bestaande `ExtGState`‑dictionary benaderen.
* Een nieuw leeg `CosPdfDictionary` bouwen en vullen met graphics‑state‑items.
* De gewijzigde PDF opslaan zonder enige originele inhoud te verliezen.

De oplossing werkt met elke PDF die minstens één pagina bevat en vereist alleen de Aspose.PDF‑bibliotheek (versie 23.10 of later).

## Vereisten

* .NET 6.0 of later (de code werkt ook op .NET Framework 4.8).
* Een referentie naar het **Aspose.PDF** NuGet‑pakket.
* Een invoer‑PDF‑bestand op `YOUR_DIRECTORY/input.pdf`.
* Basiskennis van C# en PDF‑concepten zoals resources en graphics‑state.

> **Pro tip:** Wanneer je met grote PDF‑bestanden werkt, plaats het `Document`‑object in een `using`‑block om ervoor te zorgen dat alle bestands‑handles direct worden vrijgegeven.

## Stap 1: Laad het PDF‑document

De eerste bewerking opent het bronbestand. Aspose.PDF leest het volledige document in het geheugen, zodat je interne objecten kunt bewerken.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

*Waarom dit belangrijk is*: Het laden van het document creëert een mutabel objectmodel. Zonder deze stap kun je de paginabronnen die nodig zijn voor dictionary‑manipulatie niet bereiken.

## Stap 2: Haal de resources van de eerste pagina op

Elke pagina bevat een `Resources`‑dictionary die lettertypen, afbeeldingen en graphics‑states opslaat. Toegang daartoe geeft je een `DictionaryEditor` die lees‑/schrijf‑operaties vereenvoudigt.

```csharp
// Step 2: Get the resources of the first page
Page firstPage = pdfDocument.Pages[1];
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Waarom dit belangrijk is*: De `ExtGState`‑dictionary bevindt zich binnen de paginabronnen. Het bewerken van de verkeerde dictionary heeft geen effect op de weergave.

## Stap 3: Zoek de bestaande ExtGState‑dictionary

De `ExtGState`‑entry kan al graphics‑state‑objecten bevatten. We halen deze op als een `CosPdfDictionary` zodat we nieuwe items kunnen toevoegen.

```csharp
// Step 3: Access the existing ExtGState dictionary
CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

Als de `ExtGState`‑entry niet bestaat, maakt Aspose.PDF automatisch een lege dictionary aan wanneer je later een nieuwe toewijst.

## Stap 4: **Leeg PDF-dictionary maken** voor een nieuwe graphics‑state

Hier bouwen we een gloednieuwe `CosPdfDictionary` — de kern van de **leeg PDF-dictionary maken**‑operatie. Vervolgens vullen we deze met standaard graphics‑state‑sleutels:

* `CA` – stroke‑opacity.
* `ca` – fill‑opacity.
* `BM` – blend‑mode.

```csharp
// Step 4: Create a new graphics state dictionary and define its entries
CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

KeyValuePair<string, ICosPdfPrimitive>[] graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),          // Stroke opacity
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),       // Fill opacity
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))    // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

*Waarom dit belangrijk is*: Door elke entry expliciet te definiëren, bepaal je hoe objecten op de pagina mengen en renderen. De dictionary is **leeg** totdat je deze sleutels toevoegt, wat voldoet aan de eis om **leeg PDF-dictionary maken** vóór het vullen.

## Stap 5: Voeg de nieuwe graphics‑state toe aan de ExtGState‑dictionary

Elke graphics‑state moet een unieke naam hebben (bijv. `GS0`). We voegen de zojuist gebouwde dictionary onder die naam in.

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary with a unique name
extGStateDict.Add("GS0", graphicsStateDict);
```

Als je meerdere states nodig hebt, blijf dan entries toevoegen zoals `GS1`, `GS2`, enz., en zorg ervoor dat elke naam uniek is binnen de `ExtGState`‑dictionary.

## Stap 6: Sla het bijgewerkte PDF‑document op

Schrijf tenslotte de wijzigingen terug naar schijf. Het oorspronkelijke bestand blijft onaangeroerd omdat we naar een nieuw pad opslaan.

```csharp
// Step 6: Save the updated PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

Het resulterende `output.pdf` bevat nu een extra graphics‑state (`GS0`) die je vanuit elke paginacontent‑stream kunt refereren met de `/GS0`‑operator.

## Volledig werkend voorbeeld

Alle stappen samengevoegd vormen een zelfstandige applicatie die je direct kunt uitvoeren.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources
            Page firstPage = pdfDocument.Pages[1];
            DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Get (or create) ExtGState dictionary
            CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Build a new empty PDF dictionary for graphics state
            CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var entry in entries)
                graphicsStateDict.Add(entry);

            // Insert the new graphics state with a unique name
            extGStateDict.Add("GS0", graphicsStateDict);

            // Save the modified document
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

**Verwachte output**: Na het uitvoeren van het programma bevat `output.pdf` dezelfde visuele inhoud als `input.pdf`. Het inspecteren van de PDF met een tool zoals Adobe Acrobat of PDF‑Tron toont een nieuwe entry `GS0` onder de `ExtGState`‑dictionary van de eerste pagina.

## Veelvoorkomende variaties en randgevallen

| Situatie | Wat aan te passen |
|-----------|-------------------|
| **Geen bestaande ExtGState‑entry** | Vervang `resourcesEditor["ExtGState"]` door `new CosPdfDictionary(pdfDocument)` en wijs het opnieuw toe aan `firstPage.Resources["ExtGState"]`. |
| **Meerdere pagina's hebben dezelfde state nodig** | Voeg dezelfde `GS0`‑entry toe aan de `ExtGState`‑dictionary van elke pagina, of verwijs naar de dictionary vanuit een gedeeld resource‑object. |
| **Andere blend‑mode** | Wijzig de `CosPdfName`‑waarde van `"Normal"` naar `"Multiply"`, `"Screen"` enz., afhankelijk van het gewenste effect. |
| **Hogere opaciteitswaarden** | Gebruik `new CosPdfNumber(0.8)` voor `ca` of `CA` om de vul‑ of lijn‑opacity te verhogen. |
| **Een stream‑operator gebruiken** | Schrijf in de content‑stream `"/GS0 gs"` vóór teken‑operaties om de nieuwe graphics‑state toe te passen. |

## Prestatie‑overwegingen

* **Geheugengebruik** – Het laden van een zeer grote PDF verbruikt geheugen evenredig aan het aantal pagina’s. Als je alleen de eerste pagina hoeft te bewerken, overweeg dan `pdfDocument.Pages.Delete(pageNumber)` na de verwerking om bronnen vrij te maken.
* **Thread‑veiligheid** – Aspose.PDF‑objecten zijn niet thread‑safe. Voer dictionary‑bewerkingen uit op één thread of maak aparte `Document`‑instanties per thread.

## Conclusie

Je weet nu hoe je **leeg PDF-dictionary**‑objecten maakt met Aspose.PDF, ze vult met graphics‑state‑items en koppelt ze aan de `ExtGState`‑dictionary van een pagina. Deze techniek biedt fijnmazige controle over opacity, blend‑mode en andere render‑parameters direct vanuit C#.

Vervolgens kun je gerelateerde onderwerpen verkennen zoals **PDF-manipulatie C#**, het toevoegen van aangepaste **ExtGState‑dictionary**‑entries voor geavanceerde transparantie‑effecten, of het gebruik van **CosPdfDictionary** om andere resource‑typen zoals lettertypen of XObjects te wijzigen. Experimenteer met meerdere graphics‑states om complexe visuele effecten in je PDF’s te bouwen.

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Rechthoeken maken en vullen in PDF's met Aspose.PDF voor .NET: Een stapsgewijze gids](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)
- [Hoe gestippelde lijnen te maken in PDF's met Aspose.PDF voor .NET: Een stapsgewijze gids](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Hoe een lege pagina toevoegen aan het einde van een PDF met Aspose.PDF voor .NET | Stapsgewijze gids](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}