---
category: general
date: 2026-05-27
description: Voeg Bates-nummers toe aan PDF met Aspose.Pdf in C#. Leer hoe je snel
  Bates-nummers kunt toevoegen, het formaat kunt aanpassen en de tagging van juridische
  documenten kunt automatiseren.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbering
language: nl
og_description: Voeg Bates-nummering toe aan PDF met Aspose.Pdf in C#. Deze gids laat
  zien hoe je Bates-nummering toevoegt, prefixen configureert en het resultaat opslaat.
og_title: Bates-nummering toevoegen aan PDF in C# – Stapsgewijze tutorial
schemas:
- author: Aspose
  dateModified: '2026-05-27'
  description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  headline: Add Bates Numbering PDF in C# – Complete Guide
  type: TechArticle
- description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  name: Add Bates Numbering PDF in C# – Complete Guide
  steps:
  - name: Expected Output
    text: 'When you run the program, the console prints:'
  - name: Can I position the Bates number elsewhere?
    text: Yes. Use the `BatesNumberingArtifact`’s `Location` property (e.g., `Location
      = new Position(10, 10)`) to place the number at custom X/Y coordinates. You
      can also set `HorizontalAlignment` and `VerticalAlignment` for more control.
  - name: What if my PDF has thousands of pages?
    text: Aspose.Pdf streams pages efficiently, but it’s still a good idea to process
      in batches if you hit memory limits. The `Document` class also supports `PdfConverter`
      for incremental saving.
  - name: How do I change the font or color?
    text: 'Wrap the artifact in a `TextState` object:'
  - name: Do I need a license for production use?
    text: A licensed version removes evaluation watermarks and unlocks full performance.
      The free trial works fine for testing and proof‑of‑concepts.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- Bates numbering
- PDF automation
title: Bates-nummers toevoegen aan PDF in C# – Complete gids
url: /nl/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Batesnummering PDF toevoegen in C# – Complete gids

Heb je je ooit afgevraagd **hoe je Bates‑nummering** aan een PDF kunt toevoegen zonder uren te verspillen met handmatige tools? Je bent niet de enige—juridische teams, auditors en e‑discovery‑specialisten hebben allemaal een betrouwbare manier nodig om **Bates‑nummering PDF**‑bestanden programmatisch toe te voegen.  

In deze tutorial lopen we stap voor stap door een beknopte, end‑to‑end‑oplossing met Aspose.Pdf voor .NET, zodat je Bates‑nummers op elk document kunt plaatsen met slechts een paar regels C#‑code.

## Wat je leert

- Hoe je een bestaande PDF opent met Aspose.Pdf  
- Hoe je een Bates‑nummerings‑artifact maakt en het formaat fijnstemt  
- Hoe je het artifact aan elke pagina (of alleen de eerste) koppelt  
- Hoe je het bijgewerkte bestand opslaat en het resultaat verifieert  

Ervaring met Aspose is niet vereist—een basisbegrip van C# en .NET is voldoende. Aan het einde heb je een herbruikbare snippet die je in elk project kunt kopiëren‑en‑plakken.

## Voorwaarden

- .NET 6.0 of later (de code werkt ook op .NET Framework 4.7+)  
- Aspose.Pdf for .NET NuGet‑pakket (`Install-Package Aspose.Pdf`)  
- Een bron‑PDF‑bestand dat je wilt labelen (plaats het in een map die je kunt refereren)

> **Pro tip:** Als je nog geen licentie hebt, biedt Aspose een gratis tijdelijke sleutel die evaluatiewatermerken verwijdert.

## Stap 1 – Open het bron‑PDF‑document  

Eerst hebben we een `Document`‑object nodig dat het bestand op schijf vertegenwoordigt. Beschouw dit als het laden van een leeg canvas waarop we later Bates‑nummers gaan schilderen.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Adjust the path to point at your source PDF
        string sourcePath = @"C:\Docs\source.pdf";

        // Load the PDF – this is where we start to add Bates numbering
        using (var pdfDocument = new Document(sourcePath))
        {
            // The rest of the logic lives inside this using block
        }
    }
}
```

**Waarom dit belangrijk is:** Het openen van het document binnen een `using`‑blok zorgt ervoor dat alle unmanaged resources direct worden vrijgegeven, wat vooral bij grote PDF’s cruciaal is.

## Stap 2 – Maak een Bates‑nummerings‑artifact  

Een *BatesNumberingArtifact* is de manier waarop Aspose beschrijft hoe de nummers eruit moeten zien. Je kunt een prefix, startnummer, increment en zelfs een aangepast format‑string instellen.

```csharp
// Step 2: Define the Bates numbering artifact
var batesNumbering = new BatesNumberingArtifact
{
    Prefix = "ABC",            // Text that appears before each number
    StartNumber = 1000,        // First number in the sequence
    Increment = 1,             // Step between consecutive numbers
    Format = "{0:D5}"          // Zero‑padded 5‑digit number (e.g., 01000)
};
```

**Waarom je deze waarden zou kunnen aanpassen:**  
- **Prefix** is handig voor zaak‑ID’s (“CASE‑”, “DOC‑”).  
- **StartNumber** laat je een eerdere reeks voortzetten.  
- **Increment** kan op 2 worden gezet als je oneven/even nummering nodig hebt.  
- **Format** ondersteunt elke .NET‑composite‑format; `{0:D5}` garandeert vijf cijfers met voorloopnullen.

## Stap 3 – Koppel het artifact aan de gewenste pagina’s  

Je kunt het artifact aan één pagina, een bereik of het hele document toevoegen. Voor de meeste juridische workflows koppelen we het aan *elke* pagina, maar het voorbeeld hieronder toont het minimale geval—toevoegen aan de eerste pagina.

```csharp
// Step 3: Attach the artifact to the first page (index is 1‑based)
pdfDocument.Pages[1].Artifacts.Add(batesNumbering);
```

Als je alle pagina’s wilt behandelen, doorloop je ze:

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesNumbering);
}
```

**Waarom deze stap cruciaal is:** Artifacts worden *na* de paginainhoud gerenderd, zodat de nummers bovenop bestaande tekst verschijnen zonder de oorspronkelijke lay‑out te wijzigen.

## Stap 4 – Sla de gewijzigde PDF op  

Tot slot schrijf je de wijzigingen terug naar schijf. Je kunt het origineel overschrijven of een nieuw bestand maken—hier genereren we een frisse kopie genaamd `bates.pdf`.

```csharp
// Step 4: Persist the changes
string outputPath = @"C:\Docs\bates.pdf";
pdfDocument.Save(outputPath);

Console.WriteLine($"Bates numbering added successfully. File saved to: {outputPath}");
```

Wanneer je `bates.pdf` opent, zie je “ABC01000” (of welk format je ook hebt gekozen) gestempeld op de standaardlocatie—meestal de rechteronderhoek.

## Volledig werkend voorbeeld  

Alles bij elkaar, hier is het complete programma dat je kunt compileren en uitvoeren:

```csharp
using Aspose.Pdf;
using System;

class AddBatesNumbering
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Open the source PDF
        // -----------------------------------------------------------------
        string sourcePath = @"C:\Docs\source.pdf";
        using (var pdfDocument = new Document(sourcePath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Create and configure the Bates numbering artifact
            // -----------------------------------------------------------------
            var batesNumbering = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                StartNumber = 1000,
                Increment = 1,
                Format = "{0:D5}"
            };

            // -----------------------------------------------------------------
            // 3️⃣ Attach the artifact to each page (or a specific page)
            // -----------------------------------------------------------------
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesNumbering);
            }

            // -----------------------------------------------------------------
            // 4️⃣ Save the new PDF
            // -----------------------------------------------------------------
            string outputPath = @"C:\Docs\bates.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbers added. Output: {outputPath}");
        }
    }
}
```

### Verwachte output

Wanneer je het programma draait, print de console:

```
Bates numbers added. Output: C:\Docs\bates.pdf
```

Het openen van `bates.pdf` toont de prefix “ABC” gevolgd door een nul‑gevulde vijf‑cijferige reeks op elke pagina—precies wat de code moet doen.

## Veelgestelde vragen & randgevallen

### Kan ik het Bates‑nummer ergens anders positioneren?

Ja. Gebruik de `Location`‑eigenschap van `BatesNumberingArtifact` (bijv. `Location = new Position(10, 10)`) om het nummer op aangepaste X/Y‑coördinaten te plaatsen. Je kunt ook `HorizontalAlignment` en `VerticalAlignment` instellen voor meer controle.

### Wat als mijn PDF duizenden pagina’s heeft?

Aspose.Pdf streamt pagina’s efficiënt, maar het is nog steeds verstandig om in batches te verwerken als je geheugenlimieten bereikt. De `Document`‑klasse ondersteunt bovendien `PdfConverter` voor incrementeel opslaan.

### Hoe wijzig ik het lettertype of de kleur?

Wikkel het artifact in een `TextState`‑object:

```csharp
batesNumbering.TextState = new TextState
{
    FontSize = 12,
    Font = FontRepository.FindFont("Arial"),
    ForegroundColor = Color.FromRgb(255, 0, 0) // red
};
```

### Heb ik een licentie nodig voor productiegebruik?

Een gelicentieerde versie verwijdert evaluatiewatermerken en ontgrendelt volledige prestaties. De gratis proefversie werkt prima voor testen en proof‑of‑concepts.

## Verificatie – Snelle visuele controle  

Als je een geautomatiseerde controle verkiest, kan Aspose de tekst van een pagina extraheren en de aanwezigheid van de prefix bevestigen:

```csharp
string pageText = pdfDocument.Pages[1].ExtractText();
bool hasBates = pageText.Contains("ABC01000");
Console.WriteLine(hasBates ? "Bates number verified." : "Number missing!");
```

Het uitvoeren hiervan na de opslaan‑stap print `Bates number verified.` als alles soepel is verlopen.

## Conclusie  

Je weet nu **hoe je Bates‑nummering PDF**‑bestanden toevoegt met Aspose.Pdf in C#. Van het openen van het document tot het configureren van het artifact, het koppelen aan pagina’s en het opslaan van het resultaat, het proces is eenvoudig en volledig scriptbaar.  

Volgende stappen? Experimenteer met:

- Verschillende `Prefix`‑waarden voor meerdere zaak‑batches  
- Aangepaste `Location` en `TextState` voor branding  
- Pagina‑specifieke prefixes (bijv. “VOL‑1‑”, “VOL‑2‑”) door `StartNumber` per iteratie aan te passen  

Met deze aanpassingen kun je de oplossing afstemmen op vrijwel elke juridische of archiveringsworkflow.  

Heb je meer vragen over **hoe je Bates‑nummering** toevoegt voor meertalige PDF’s of versleutelde bestanden? Laat een reactie achter, en happy coding!

## Gerelateerde tutorials

- [Hoe paginanummers toevoegen en aanpassen in PDF’s met Aspose.PDF voor .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Hoe verschillende kopteksten toevoegen in PDF met Aspose.PDF voor .NET: Een stapsgewijze handleiding](/pdf/english/net/document-manipulation/add-different-headers-aspose-pdf-net/)
- [Hoe een tekststempel‑footer toevoegen in PDF’s met Aspose.PDF voor .NET: Een stapsgewijze handleiding](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}