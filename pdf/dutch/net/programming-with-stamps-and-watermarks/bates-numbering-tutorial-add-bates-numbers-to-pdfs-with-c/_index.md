---
category: general
date: 2026-02-25
description: Bates‑numbering tutorial – leer hoe je paginanummers aan een PDF toevoegt
  en aangepaste Bates‑numbering toepast met Aspose.Pdf in C#. Stapsgewijze gids met
  volledige code.
draft: false
keywords:
- bates numbering tutorial
- add page numbers pdf
- how to add bates
- add bates numbering
language: nl
og_description: Bates-nummering tutorial laat zien hoe je paginanummers aan een pdf
  toevoegt en aangepaste Bates-nummering in C#. Complete code, uitleg en tips.
og_title: bates nummering tutorial – Voeg Bates-nummers toe aan PDF's met C#
tags:
- PDF
- C#
- Aspose.Pdf
title: 'batesnummering tutorial: Voeg Bates-nummers toe aan PDF''s met C#'
url: /nl/net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-bates-numbers-to-pdfs-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# bates numbering tutorial – Bates-nummers toevoegen aan PDF's in C#

Heb je je ooit afgevraagd hoe je paginanummers aan een PDF kunt toevoegen én tegelijkertijd een juridisch‑stijl Bates‑nummer kunt insluiten? Je bent niet de enige. In deze **bates numbering tutorial** lopen we stap voor stap door alles wat je moet weten om elke pagina van een PDF te voorzien van een aangepast voorvoegsel, leidende nullen en precieze positionering — met behulp van Aspose.Pdf voor .NET.

Het goede nieuws? Het is vrij eenvoudig zodra je de kernconcepten begrijpt. Aan het einde van deze gids heb je een werkend programma dat *input.pdf* neemt en *bates_out.pdf* produceert met een net “ABC‑01000”‑type label op elke pagina. Laten we beginnen.

## What You’ll Need

- **Aspose.Pdf for .NET** (versie 23.10 of later). De bibliotheek is commercieel, maar een gratis proefversie werkt prima voor leerdoeleinden.
- .NET 6+ SDK (elke recente versie volstaat).
- Een basis C#‑ontwikkelomgeving — Visual Studio, VS Code of Rider.
- Een invoer‑PDF om mee te experimenteren (elke meer‑pagina‑document zal het effect laten zien).

Er zijn geen extra NuGet‑pakketten nodig naast Aspose.Pdf, en de code draait op Windows, Linux of macOS zonder aanpassingen.

## Step 1: Load the Source PDF Document (bates numbering tutorial – initialization)

Eerst maken we een `Document`‑object dat de PDF vertegenwoordigt die we willen aanpassen. Beschouw het als het laden van een leeg canvas waarop je kunt tekenen.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF – replace the path with your actual file location
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// Quick sanity check – make sure the document actually has pages
if (pdfDocument.Pages.Count == 0)
{
    throw new InvalidOperationException("The PDF you provided contains no pages.");
}
```

**Why this matters:** Zonder het bestand te laden, is er niets om te annoteren. De sanity‑check voorkomt een stille fout later wanneer je artefacten probeert toe te voegen aan een niet‑bestaande paginacollectie.

## Step 2: Define the Bates Numbering Artifact (how to add bates)

Een *BatesNumberingArtifact* vertelt Aspose waar en hoe het de identifier moet tekenen. Je kunt het voorvoegsel, startnummer, nul‑opvulling, lettergrootte en exacte X/Y‑coördinaten bepalen.

```csharp
// Configure the Bates numbering artifact
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
{
    Prefix = "ABC",          // Text that appears before the number
    Start = 1000,            // First number in the sequence
    LeadingZeros = 5,        // Pad the number with zeros (e.g., 01000)
    FontSize = 9,            // Small enough to sit in the margin
    Position = new Position   // Position measured from the lower‑left corner
    {
        X = 50,               // Horizontal offset (points)
        Y = 30                // Vertical offset (points)
    }
};
```

**Why this matters:** De eigenschap `LeadingZeros` zorgt ervoor dat elk label dezelfde lengte heeft, wat cruciaal is voor juridische documenten waar uitlijning van belang is. Pas `X` en `Y` aan om de stempel naar rechts‑boven, links‑onder of waar je workflow het vereist te verplaatsen.

## Step 3: Attach the Artifact to Every Page (add page numbers pdf)

Nu doorlopen we elke pagina en koppelen we hetzelfde artefact. Dit is waar de *add page numbers pdf*‑vereiste wordt vervuld — elke pagina krijgt automatisch zijn eigen opeenvolgende label.

```csharp
// Iterate over each page and add the Bates artifact
foreach (Page page in pdfDocument.Pages)
{
    // The artifact is added to the page's Artifacts collection.
    // Aspose will handle the incrementing of the number for us.
    page.Artifacts.Add(batesArtifact);
}
```

**Why this matters:** Door het artefact toe te voegen aan de `Artifacts`‑collectie in plaats van tekst handmatig te tekenen, laat je Aspose de nummeringslogica, leidende nullen en rendering afhandelen. Dit vermindert bugs en houdt de code beknopt.

## Step 4: Save the Modified PDF (add bates numbering)

Tot slot slaan we de wijzigingen op in een nieuw bestand. Het is een goede gewoonte om naar een andere bestandsnaam te schrijven zodat je het origineel onaangeroerd houdt.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");

// Optional: let the user know we succeeded
Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
```

**Why this matters:** De `Save`‑methode schrijft de volledige PDF weg en embedde de artefacten als onderdeel van de paginacontent‑stream. Het resulterende bestand kan in elke PDF‑viewer worden geopend en toont de Bates‑nummers precies zoals gespecificeerd.

## Full Working Example (All Steps Combined)

Hieronder staat het complete, kant‑klaar programma. Kopieer‑en‑plak het in een console‑app‑project, vervang de voorbeeldpaden, en druk op **F5**.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
            if (pdfDocument.Pages.Count == 0)
                throw new InvalidOperationException("The PDF you provided contains no pages.");

            // 2️⃣ Configure the Bates numbering artifact
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                Start = 1000,
                LeadingZeros = 5,
                FontSize = 9,
                Position = new Position { X = 50, Y = 30 }
            };

            // 3️⃣ Attach the artifact to every page
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesArtifact);
            }

            // 4️⃣ Save the modified PDF
            pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");
            Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
        }
    }
}
```

### Expected Result

Open *bates_out.pdf* in Adobe Reader, Foxit of een andere viewer. Je zou een label moeten zien zoals **ABC‑01000** op de eerste pagina, **ABC‑01001** op de tweede, enzovoort, geplaatst 50 pt vanaf de linkerrand en 30 pt vanaf de onderkant. De nummers zijn rechts‑uitgelijnd dankzij de leidende nullen, waardoor het document er netjes en professioneel uitziet.

## Common Variations & Edge Cases

| Scenario | How to Adjust |
|----------|---------------|
| **Different prefix** | Verander `Prefix = "XYZ"` in de artefactdefinitie. |
| **Start at a custom number** | Stel `Start = 5000` in (of elk ander geheel getal). |
| **Place the number in the top‑right corner** | Gebruik `Position = new Position { X = pdfDocument.PageInfo.Width - 50, Y = pdfDocument.PageInfo.Height - 30 }`. |
| **Change font size for larger documents** | Pas `FontSize = 12` aan (of een andere grootte). |
| **Add a background rectangle** | Maak een `RectangleArtifact` aan en voeg die toe vóór de `BatesNumberingArtifact`. |
| **Skip certain pages** | Voeg binnen de `foreach`‑lus een `if (page.Number % 2 == 0) continue;` toe om even pagina’s over te slaan. |

**Pro tip:** Test altijd eerst met een korte PDF. Het is sneller om de positionering te verifiëren voordat je het script op een bestand met 200 pagina’s toepast.

## Frequently Asked Questions

- **Does this work with encrypted PDFs?**  
  Aspose.Pdf kan wachtwoord‑beveiligde bestanden openen als je het wachtwoord opgeeft via `Document(string, string)`. Het Bates‑artefact wordt nog steeds toegepast na ontcijfering.

- **Can I add both Bates numbers and regular page numbers?**  
  Ja. Voeg een `PageNumberArtifact` toe naast de `BatesNumberingArtifact`. Elk artefact behoudt zijn eigen teller.

- **What if my PDF has different page sizes?**  
  De `Position`‑waarden zijn absolute punten. Voor documenten met gemengde paginagroottes bereken je de positie per pagina binnen de lus met `page.PageInfo.Width` en `page.PageInfo.Height`.

## Next Steps & Related Topics

Nu je de **bates numbering tutorial** onder de knie hebt, kun je wellicht verder verkennen:

- **Adding watermarks** – vergelijkbare artefact‑aanpak met `TextArtifact`.
- **Merging multiple PDFs** – gebruik `Document.AppendDocument`.
- **Extracting text for search indexing** – `TextAbsorber`‑klasse.
- **Automating batch processing** – loop over een map met PDF’s en pas hetzelfde artefact toe.

Al deze onderwerpen bouwen voort op dezelfde concepten die je zojuist geleerd hebt, dus je bent goed gepositioneerd om je PDF‑automatiseringstoolkit uit te breiden.

---

*Happy coding! Als je ergens vastloopt of ideeën hebt voor verdere aanpassingen, laat dan gerust een reactie achter. De wereld van PDF‑manipulatie is enorm, maar met een solide **bates numbering tutorial** onder de riem ben je al een stap voor.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}