---
category: general
date: 2026-08-14
description: Maak een lege PDF-dictionary in C# met Aspose.Pdf – leer hoe je een grafische
  toestand toevoegt aan de ExtGState-collectie en PDF's programmatically wijzigt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.Pdf Document
- PDF graphics state
- ExtGState dictionary
- CosPdfDictionary usage
language: nl
lastmod: 2026-08-14
og_description: Maak een lege PDF-dictionary in C# met Aspose.Pdf. Volg deze volledige
  gids om een aangepaste grafische toestand toe te voegen aan de ExtGState-collectie
  van een PDF.
og_image_alt: Screenshot showing C# code that creates an empty PDF dictionary with
  Aspose.Pdf
og_title: Maak een leeg PDF‑woordenboek in C# – Aspose.Pdf stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  headline: Create empty PDF dictionary in C# with Aspose.Pdf
  type: TechArticle
- description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  name: Create empty PDF dictionary in C# with Aspose.Pdf
  steps:
  - name: Create a new **Console App** project in Visual Studio.
    text: Create a new **Console App** project in Visual Studio.
  - name: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
    text: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
  - name: 'Add the following `using` directives at the top of `Program.cs`:'
    text: 'Add the following `using` directives at the top of `Program.cs`:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Maak een leeg PDF‑woordenboek in C# met Aspose.Pdf
url: /nl/net/programming-with-operators/create-empty-pdf-dictionary-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak een lege PDF-dictionary in C# met Aspose.Pdf

Als je **lege PDF-dictionary** objecten moet maken tijdens het werken met PDF‑bestanden, laat deze gids je precies zien hoe je dat doet in C# met de Aspose.Pdf‑bibliotheek. Of je nu een aangepaste graphics‑state bouwt, een nieuwe resource toevoegt, of een sjabloon voorbereidt voor later gebruik, de onderstaande stappen bieden een complete, uitvoerbare oplossing.

Je leert hoe je een PDF laadt, de resource‑dictionary van de eerste pagina benadert, een gloednieuwe `CosPdfDictionary` bouwt en deze in de `ExtGState`‑collectie invoegt. Aan het einde van de tutorial heb je een werkende `output.pdf` die de nieuw aangemaakte dictionary bevat.

## Vereisten

- .NET 6.0 of later (de code werkt ook met .NET Framework 4.6+)
- Visual Studio 2022 of een andere C#‑IDE naar keuze
- Een Aspose.Pdf for .NET‑licentie (of een tijdelijke evaluatiesleutel)
- Een voorbeeld‑PDF met de naam **input.pdf** geplaatst in een map die je beheert (het mappad wordt gebruikt als `dataDir`)

Er zijn geen extra NuGet‑pakketten nodig naast `Aspose.Pdf`.

## Stap 1: Zet het project op en verwijs naar Aspose.Pdf

1. Maak een nieuw **Console App**‑project aan in Visual Studio.  
2. Open de **NuGet Package Manager** en installeer `Aspose.Pdf`:

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. Voeg de volgende `using`‑directieven toe bovenaan `Program.cs`:

   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Text;
   using Aspose.Pdf.Operators;
   using Aspose.Pdf.Facades;
   using Aspose.Pdf.InteractiveFeatures;
   using Aspose.Pdf.Xmp;
   using Aspose.Pdf.Operators.Filters;
   using Aspose.Pdf.Operators.Gfx;
   ```

   *Waarom deze namespaces?* `Aspose.Pdf` bevat de kern‑`Document`‑klasse, terwijl `Aspose.Pdf.Operators.Gfx` `CosPdfDictionary`, `CosPdfNumber` en gerelateerde low‑level PDF‑objecten levert die nodig zijn om **lege PDF-dictionary** structuren te **maken**.

## Stap 2: Laad de bron‑PDF

De eerste handeling is het laden van het bestaande PDF‑bestand in een `Document`‑instantie. Dit geeft je toegang tot alle pagina's, resources en low‑level dictionaries.

```csharp
// Step 2: Load the PDF document
string dataDir = @"C:\MyPdfFolder\";               // Change to your folder
using var pdfDocument = new Document(dataDir + "input.pdf");
```

*Uitleg*: `Document` leest het bestand in het geheugen en bereidt interne structuren voor. De `using`‑statement zorgt ervoor dat de bestands‑handle wordt vrijgegeven nadat we klaar zijn met verwerken.

## Stap 3: Benader de resource‑dictionary van de eerste pagina

Elke PDF‑pagina heeft een **Resources**‑dictionary die lettertypen, afbeeldingen, ExtGState‑objecten en andere gedeelde resources groepeert. Om een nieuwe graphics‑state in te voegen moeten we deze dictionary bewerken.

```csharp
// Step 3: Get the first page and its Resources dictionary
Page firstPage = pdfDocument.Pages[1];                     // PDF pages are 1‑based
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` is een hulpprogrammaklasse die je een PDF‑dictionary laat behandelen als een C# `Dictionary<string, object>`.

## Stap 4: Haal (of maak) de ExtGState‑collectie op

`ExtGState` bevat graphics‑state objecten zoals opacity, blend‑mode en lijnbreedte. Als de bron‑PDF al een `ExtGState`‑item bevat, gebruiken we die opnieuw; anders maken we een nieuwe lege dictionary.

```csharp
// Step 4: Ensure an ExtGState dictionary exists
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a brand‑new ExtGState dictionary and add it to Resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*Waarom deze controle?* Sommige PDF‑bestanden laten het `ExtGState`‑item volledig weg. Door beide gevallen af te handelen blijft de tutorial robuust voor elk invoerbestand.

## Stap 5: **Maak een lege PDF-dictionary** voor een nieuwe graphics‑state

Nu maken we daadwerkelijk **lege PDF-dictionary** objecten die de graphics‑state parameters definiëren. De dictionary begint leeg, en we voegen de vereiste sleutels toe:

```csharp
// Step 5: Build a new graphics state dictionary (empty PDF dictionary + entries)
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Stroke opacity (CA) – 1 means fully opaque strokes
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes semi‑transparent fills
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default compositing mode
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

### Wat elke entry doet

| Sleutel | Type | Betekenis |
|-----|------|---------|
| **CA** | `CosPdfNumber` | Streep‑opacity (bereik 0‑1). |
| **ca** | `CosPdfNumber` | Vullings‑opacity (bereik 0‑1). |
| **BM** | `CosPdfName`   | Blend‑mode; `"Normal"` is de meest voorkomende. |

Omdat we begonnen met een **lege PDF-dictionary**, hebben we volledige controle over welke entries worden toegevoegd. Je kunt deze dictionary uitbreiden met extra graphics‑state parameters zoals `LW` (lijnbreedte) of `LC` (lijncap) wanneer nodig.

## Stap 6: Voeg de nieuwe graphics‑state toe aan ExtGState

De `ExtGState`‑dictionary werkt als een map waarbij elke entry wordt geïdentificeerd door een naam (bijv. `GS0`, `GS1`). We voegen onze zojuist gebouwde dictionary toe onder een unieke sleutel.

```csharp
// Step 6: Add the graphics state to the ExtGState collection
extGStateDict.Add("GS0", newGraphicsState);
```

Als je van plan bent meerdere states toe te voegen, verhoog dan het achtervoegsel (`GS1`, `GS2`, …) om naamconflicten te voorkomen.

## Stap 7: Sla de gewijzigde PDF op

Tot slot schrijf je de wijzigingen terug naar schijf. De `Save`‑methode serialiseert automatisch de bijgewerkte dictionaries.

```csharp
// Step 7: Persist the changes
pdfDocument.Save(dataDir + "output.pdf");
```

Open `output.pdf` in een PDF‑viewer en inspecteer de **Resources → ExtGState**‑entry (de meeste viewers verbergen dit, maar tools zoals Adobe Acrobat Preflight of PDF‑Tron kunnen het tonen). Je zou een `GS0`‑entry moeten zien die de door jou gedefinieerde opacity‑ en blend‑mode‑waarden bevat.

## Volledig werkend voorbeeld

Door alle onderdelen samen te voegen, hier is het volledige programma dat je kunt kopiëren‑plakken in `Program.cs` en uitvoeren:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators.Gfx;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string dataDir = @"C:\MyPdfFolder\"; // <-- change to your folder
        using var pdfDocument = new Document(dataDir + "input.pdf");

        // -----------------------------------------------------------------
        // 2️⃣ Access the first page’s Resources dictionary
        // -----------------------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // -----------------------------------------------------------------
        // 3️⃣ Retrieve or create the ExtGState dictionary
        // -----------------------------------------------------------------
        CosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourcesEditor["ExtGState"] = extGStateDict;
        }

        // -----------------------------------------------------------------
        // 4️⃣ **Create empty PDF dictionary** for a new graphics state
        // -----------------------------------------------------------------
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode

        // -----------------------------------------------------------------
        // 5️⃣ Add the graphics state to ExtGState
        // -----------------------------------------------------------------
        extGStateDict.Add("GS0", newGraphicsState);

        // -----------------------------------------------------------------
        // 6️⃣ Save the modified PDF
        // -----------------------------------------------------------------
        pdfDocument.Save(dataDir + "output.pdf");

        Console.WriteLine("PDF saved with new empty dictionary at: " + dataDir + "output.pdf");
    }
}
```

**Verwachte output** – De console geeft een bevestigingsregel weer, en `output.pdf` bevat de nieuwe `GS0`‑entry onder `ExtGState`. Wanneer je een pagina rendert die `GS0` aanroept (bijv. via een content‑stream operator `gs`), zullen strepen volledig ondoorzichtig zijn terwijl vullingen 50 % transparant zijn.

## Veelgestelde vragen en edge‑case handling

| Vraag | Antwoord |
|----------|--------|
| *Wat als de PDF meerdere pagina's heeft?* | Het voorbeeld richt zich op de eerste pagina (`Pages[1]`). Om alle pagina's te beïnvloeden, loop je door `pdfDocument.Pages` en herhaal je stappen 3‑5 voor de resources van elke pagina. |
| *Kan ik de dictionary toevoegen aan een pagina die al een ExtGState‑entry met de naam “GS0” heeft?* | Ja, maar je moet een andere sleutel gebruiken (`GS1`, `GS2`, …) om het bestaande item niet te overschrijven. |
| *Is het veilig om de dictionary te wijzigen na het opslaan?* | Zodra je `Save` aanroept, is de in‑memory representatie losgekoppeld van het bestand. Je kunt het `Document`‑object blijven bewerken en opnieuw `Save` aanroepen indien nodig. |
| *Heb ik een licentie voor Aspose.Pdf nodig om ` |

## Wat kun je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe je gestippelde lijnen maakt in PDF's met Aspose.PDF voor .NET: Een stapsgewijze gids](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Hoe je graphics verwijdert uit PDF's met Aspose.PDF .NET: Een complete gids](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Hoe je multi‑layer PDF's maakt met Aspose.PDF voor .NET: Een uitgebreide gids](/pdf/english/net/advanced-features/create-multi-layer-pdfs-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}