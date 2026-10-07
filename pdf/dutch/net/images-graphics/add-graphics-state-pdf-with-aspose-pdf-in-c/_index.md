---
category: general
date: 2026-10-07
description: Voeg een graphics state toe aan een PDF met Aspose.Pdf in C# om de transparantie
  van de PDF te wijzigen. Volg deze stap‑voor‑stap gids om aangepaste graphics states
  in te sluiten en de doorzichtigheid te regelen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- modify pdf transparency
language: nl
lastmod: 2026-10-07
og_description: Grafische toestand toevoegen aan PDF met Aspose.Pdf in C#. Leer hoe
  je de transparantie van een PDF kunt wijzigen door een aangepast grafische‑toestand‑dictionary
  te maken.
og_image_alt: Screenshot showing the add graphics state pdf code editor in Visual
  Studio
og_title: Grafische toestand toevoegen aan PDF met Aspose.Pdf – PDF-transparantie
  beheren
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Add graphics state pdf using Aspose.Pdf in C# to modify PDF transparency.
    Follow this step‑by‑step guide to embed custom graphics states and control opacity.
  headline: Add graphics state pdf with Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Grafische toestand toevoegen aan PDF met Aspose.Pdf in C#
url: /nl/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Grafische status pdf toevoegen met Aspose.Pdf in C#

Als je een **add graphics state pdf** aan een document moet toevoegen, laat deze tutorial precies zien hoe je dat doet met Aspose.Pdf voor .NET. Aan het einde van de gids weet je ook hoe je **modify PDF transparency** kunt aanpassen, waardoor je aangepaste opaciteitswaarden kunt instellen voor elke tekenbewerking.

Werken met PDF‑grafische statussen stelt je in staat parameters zoals lijndikte, blend‑mode en, het belangrijkste voor dit artikel, de transparantie van inhoud te regelen. De onderstaande stappen zijn geschreven voor ontwikkelaars die vertrouwd zijn met C# en een kant‑klaar‑te‑gebruiken‑oplossing willen zonder door de officiële SDK‑documentatie te moeten graven.

## Wat je zult leren

* Hoe je een nieuw graphics state‑woordenboek maakt en vult met de `CA`, `ca` en `BM`‑items.  
* Hoe je dat woordenboek invoegt in de `ExtGState`‑resource van de pagina zodat de PDF het herkent.  
* Hoe de `ca` (stroke) en `CA` (fill) waarden **modify PDF transparency** beïnvloeden voor daaropvolgende tekenopdrachten.  
* Veelvoorkomende valkuilen zoals naamconflicten en versie‑compatibiliteit, plus pro‑tips voor het later uitbreiden van de graphics state.

**Prerequisites**

* .NET 6.0 of later (de code werkt ook met .NET Framework 4.7+).  
* Een geldige Aspose.Pdf for .NET‑licentie (de gratis evaluatie werkt voor testen).  
* Visual Studio 2022 of een andere C#‑IDE naar keuze.  

---

## Stap 1: Installeer Aspose.Pdf voor .NET

Voeg het NuGet‑pakket toe aan je project:

```bash
dotnet add package Aspose.Pdf
```

Het pakket bevat de `Aspose.Pdf`‑namespace die de klassen `Document`, `DictionaryEditor` en `CosPdfDictionary` levert die later worden gebruikt.

> **Pro tip:** Als je van plan bent om veel PDF‑bestanden in één batch te verwerken, schakel dan de **License** vroegtijdig in `Program.cs` in om het evaluatiewatermerk te vermijden.

```csharp
// Apply your license (optional for evaluation)
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Aspose.Pdf.lic");
```

## Stap 2: Definieer invoer‑ en uitvoer‑paden

Je moet de SDK wijzen naar een bestaand PDF‑bestand (`input.pdf`) en aangeven waar het gewijzigde bestand moet worden opgeslagen (`output.pdf`).

```csharp
// Define input and output PDF file paths
string inputPath = @"C:\MyPdfs\input.pdf";
string outputPath = @"C:\MyPdfs\output.pdf";
```

> **Waarom dit belangrijk is:** Het gebruik van absolute paden voorkomt dat de SDK in de verkeerde werkmap zoekt, wat een veelvoorkomende oorzaak is van `FileNotFoundException`.

## Stap 3: Open de PDF en lokaliseer de resources van de eerste pagina

Het `ExtGState`‑woordenboek bevindt zich binnen het resource‑woordenboek van elke pagina. We bewerken de eerste pagina voor de eenvoud, maar dezelfde aanpak werkt voor elke paginanummer.

```csharp
using (var pdfDocument = new Aspose.Pdf.Document(inputPath))
{
    // Get the first page (pages are 1‑based)
    var firstPage = pdfDocument.Pages[1];

    // Access the page’s resource dictionary via DictionaryEditor
    var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);

    // Retrieve (or create) the ExtGState entry
    var extGStateDict = resourcesEditor["ExtGState"]
        .ToCosPdfDictionary(); // Throws if ExtGState does not exist
```

**Edge case:** Als de pagina geen `ExtGState`‑item heeft, moet je deze aanmaken:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
{
    var emptyDict = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", emptyDict);
    extGStateDict = emptyDict;
}
```

## Stap 4: Bouw een nieuw graphics state‑woordenboek

Een graphics state is een verzameling sleutel/waarde‑paren die beschrijven hoe tekenbewerkingen zich gedragen. Voor transparantie hebben we drie sleutels nodig:

| Sleutel | Betekenis | Typische waarde |
|---------|-----------|-----------------|
| `CA`    | Fill opacity (0 = transparent, 1 = opaque) | `1` (volledig ondoorzichtig) |
| `ca`    | Stroke opacity (zelfde schaal) | `0.5` (50 % transparant) |
| `BM`    | Blend mode (bijv. `Normal`, `Multiply`) | `Normal` |

```csharp
    // Create an empty dictionary that will hold the graphics state
    var newGraphicsState = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Populate the dictionary with transparency and blend mode entries
    var graphicsStateEntries = new[]
    {
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "CA", new Aspose.Pdf.CosPdfNumber(1)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "ca", new Aspose.Pdf.CosPdfNumber(0.5)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "BM", new Aspose.Pdf.CosPdfName("Normal"))
    };

    foreach (var entry in graphicsStateEntries)
        newGraphicsState.Add(entry);
```

**Waarom deze waarden?**  
`ca = 0.5` maakt elk getekend pad (lijnen, randen) 50 % transparant, terwijl `CA = 1` gevulde vormen volledig ondoorzichtig laat. Pas beide getallen aan om het exacte **modify PDF transparency**‑effect te bereiken dat je nodig hebt.

## Stap 5: Voeg de graphics state toe aan het ExtGState‑woordenboek

Je moet de nieuwe state een unieke naam geven (bijv. `GS0`). Als die naam al bestaat, zal Aspose.Pdf het bestaande item overschrijven, wat andere inhoud die ervan afhankelijk is kan breken.

```csharp
    // Add the new graphics state under a custom name
    const string stateName = "GS0";

    // Ensure we don’t clash with an existing entry
    if (extGStateDict.ContainsKey(stateName))
        extGStateDict.Remove(stateName);

    extGStateDict.Add(stateName, newGraphicsState);
```

Nu kennen de resources van de pagina `GS0`. Om het daadwerkelijk te gebruiken, zou je de graphics state refereren in een content‑stream via de `gs`‑operator (bijv. `GS0 gs`). Aspose.Pdf laat je ruwe PDF‑operators injecteren als je aangepaste vormen moet tekenen.

## Stap 6: Sla de gewijzigde PDF op

```csharp
    // Persist the changes to a new file
    pdfDocument.Save(outputPath);
}
```

De resulterende `output.pdf` bevat dezelfde visuele inhoud als het origineel, maar alle daaropvolgende tekenopdrachten die `GS0` selecteren, respecteren de door jou gedefinieerde transparantie‑instellingen.

### Verwacht resultaat

Open `output.pdf` in Adobe Acrobat of een andere PDF‑viewer. Als je een nieuwe getekende lijn toevoegt met de `GS0` graphics state (bijv. via `pdfDocument.Pages[1].Contents.Add(...)`), zal de lijn semi‑transparant verschijnen terwijl vullingen ondoorzichtig blijven. Dit toont aan dat je succesvol **add graphics state pdf** en **modify PDF transparency** hebt uitgevoerd.

---

## Volledig uitvoerbaar voorbeeld

Hieronder staat het complete programma dat je kunt kopiëren‑plakken in een console‑applicatie. Het bevat licentie‑laden, foutafhandeling en commentaren die elke niet‑voor de hand liggende stap uitleggen.

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣  Apply license (optional for evaluation)
        // -------------------------------------------------
        try
        {
            var license = new License();
            license.SetLicense("Aspose.Pdf.lic");
        }
        catch (Exception) { /* License not found – continue in evaluation mode */ }

        // -------------------------------------------------
        // 2️⃣  Define file locations
        // -------------------------------------------------
        string inputPath = @"C:\MyPdfs\input.pdf";
        string outputPath = @"C:\MyPdfs\output.pdf";

        // -------------------------------------------------
        // 3️⃣  Open document and prepare resources
        // -------------------------------------------------
        using (var pdfDocument = new Document(inputPath))
        {
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            if (!resourcesEditor.ContainsKey("ExtGState"))
            {
                var emptyExtGState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
                resourcesEditor.Add("ExtGState", emptyExtGState);
            }

            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // -------------------------------------------------
            // 4️⃣  Create custom graphics state (transparency)
            // -------------------------------------------------
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            newGraphicsState.Add("CA", new CosPdfNumber(1));   // Fill opacity
            newGraphicsState.Add("ca", new CosPdfNumber(0.5)); // Stroke opacity
            newGraphicsState.Add("BM", new CosPdf


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Transparantie toevoegen aan PDF met Aspose PDF in C# – Stapsgewijze gids](/pdf/english/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Transparantie toevoegen aan PDF met Aspose – Complete C# gids](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [Hoe een afbeeldingstempel toe te voegen aan een PDF met Aspose.PDF voor .NET: Een uitgebreide gids](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}