---
category: general
date: 2026-03-22
description: Voeg snel Bates‑nummering toe aan PDF met Aspose.Pdf. Leer hoe je Bates,
  opeenvolgende paginanummers, een aangepaste voettekst en een artefact aan een PDF
  kunt toevoegen in enkele minuten.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- add custom footer pdf
- add artifact to pdf
language: nl
og_description: Bates-nummering toevoegen aan PDF met Aspose.Pdf. Deze gids laat zien
  hoe je Bates toevoegt, opeenvolgende paginanummers, een aangepaste voettekst aan
  een PDF en een artefact aan een PDF toevoegt.
og_title: Bates‑nummering toevoegen aan PDF – Stapsgewijze C#‑tutorial
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Bates-nummers toevoegen aan PDF – Complete C#-gids
url: /nl/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates-nummers toevoegen aan PDF – Complete C#‑gids

Heb je ooit **bates numbering pdf** moeten toevoegen aan een reeks juridische documenten, maar wist je niet waar te beginnen? Je bent niet de eerste—veel ontwikkelaars lopen tegen dit obstakel aan bij het bouwen van case‑management tools. Het goede nieuws? Met Aspose.Pdf kun je **bates toevoegen**, **volgorde‑pagina‑nummers toevoegen**, en zelfs **aangepaste footer pdf**‑elementen toevoegen in slechts een paar regels code.  

In deze tutorial lopen we het volledige proces door, van het installeren van de bibliotheek tot het opslaan van het uiteindelijke bestand, en we geven tips over hoe je **artifact to pdf**‑bestanden kunt toevoegen zonder bestaande inhoud te breken. Aan het einde heb je een kant‑klaar fragment dat je in elk .NET‑project kunt plaatsen.

## Wat je nodig hebt

- .NET 6+ (de code werkt zowel op .NET Core als .NET Framework)  
- Een geldige Aspose.Pdf for .NET‑licentie (je kunt beginnen met een gratis evaluatie)  
- Een invoer‑PDF (`input.pdf`) geplaatst in een map die je kunt refereren  
- Visual Studio, Rider, of een andere C#‑editor naar keuze  

Dat is alles—geen extra NuGet‑pakketten behalve Aspose.Pdf.

## Stap 1: Installeer Aspose.Pdf via NuGet

Allereerst—laten we de bibliotheek op je machine krijgen. Open een terminal in je projectmap en voer uit:

```bash
dotnet add package Aspose.Pdf
```

Of, als je de Package Manager Console van Visual Studio gebruikt:

```powershell
Install-Package Aspose.Pdf
```

*Pro tip:* Controleer na de installatie dat de `Aspose.Pdf`‑map verschijnt onder `Dependencies → Packages` in je solution explorer.

## Stap 2: Laad het bron‑PDF‑document

Nu maken we een `Document`‑object dat de PDF vertegenwoordigt die we willen stempelen. Het gebruik van de `using`‑statement zorgt ervoor dat de bestands‑handle automatisch wordt vrijgegeven.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing; // For Color

// Step 2: Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

Waarom `using var` gebruiken? Het garandeert disposen zelfs als er een uitzondering optreedt, waardoor later lock‑problemen bij het overschrijven van hetzelfde bestand worden voorkomen.

## Stap 3: Maak en configureer een Bates‑nummering‑artifact

Een Bates‑nummer is in wezen een tekst‑artifact dat leeft in de logische structuur van de PDF. Je kunt het behandelen als een **custom footer pdf** omdat het op elke pagina verschijnt zonder deel uit te maken van de content‑stream van de pagina.

```csharp
// Step 3: Define the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "INV-",          // Optional prefix – change as needed
    Start = 1000,             // Starting number
    Format = "0000",          // Zero‑padded format (e.g., 1000 → 1000)
    X = 500,                  // Horizontal position (points from left)
    Y = 20,                   // Vertical position (points from bottom)
    FontSize = 10,
    FontColor = Color.Black
};
```

### Waarom deze instellingen belangrijk zijn

- **Prefix**: Handig om documenttypen te onderscheiden (bijv. “INV‑” voor facturen).  
- **Start**: Stelt het eerste nummer in; je kunt dit uit een database halen als je continuïteit over bestanden heen nodig hebt.  
- **Format**: `"0000"` dwingt een viercijferige weergave af, waardoor uitlijning behouden blijft wanneer de nummers groeien.  
- **X/Y**: Coördinaten worden gemeten vanaf de linksonderhoek, dus `Y = 20` plaatst de tekst net boven de paginamarge. Pas `X` aan als je het nummer links‑gealigneerd of gecentreerd wilt hebben.

Als je **sequential page numbers** wilt toevoegen in plaats van Bates‑nummers, laat dan `Prefix` weg en pas `Format` aan naar `"###"` of een ander patroon naar keuze.

## Stap 4: Pas het artifact toe op alle pagina's

Aspose.Pdf laat je een artifact aan het hele document koppelen met één enkele aanroep. Dit is de meest efficiënte manier om **artifact to pdf** toe te voegen zonder handmatig door elke pagina te loopen.

```csharp
// Step 4: Apply the artifact to the whole document
pdfDocument.Pages.AddArtifact(batesArtifact);
```

Achter de schermen voegt Aspose het artifact toe aan de paginadictionary van elke pagina, waardoor de nummering deel wordt van de logische structuur van de PDF—perfect voor latere extractie of zoeken.

## Stap 5: Sla de bijgewerkte PDF op

Tot slot schrijf je de wijzigingen terug naar de schijf. Je kunt het origineel overschrijven of naar een nieuw bestand opslaan; het laatste is veiliger tijdens ontwikkeling.

```csharp
// Step 5: Save the PDF with Bates numbers
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

Wanneer je `output.pdf` opent in een viewer, zie je “INV‑1000”, “INV‑1001”, … rechtsonder op elke pagina.

### Het resultaat verifiëren

Open de PDF in Adobe Acrobat of een andere viewer en zoek naar de nummers. Als je dit programmatisch wilt bevestigen, kun je het artifact teruglezen:

```csharp
foreach (var page in pdfDocument.Pages)
{
    foreach (var artifact in page.Artifacts)
    {
        Console.WriteLine($"Page {page.Number}: {artifact.Text}");
    }
}
```

Dat fragment print het Bates‑label van elke pagina—handig voor geautomatiseerde tests.

## Randgevallen & Veelgestelde Vragen

### Wat als mijn PDF al een footer heeft?

Het toevoegen van een artifact overschrijft bestaande footers niet, omdat artifacts zich in een aparte laag bevinden. Als visuele overlapping een zorg is, pas dan de `Y`‑coördinaat aan of vergroot de `X`‑offset om het Bates‑nummer uit de weg te schuiven.

### Kan ik een ander lettertype of kleur gebruiken?

Zeker. `BatesNumberingArtifact` erft van `Artifact`, dus je kunt `Font`, `FontColor` en zelfs `Opacity` instellen. Voorbeeld:

```csharp
batesArtifact.Font = FontRepository.FindFont("Arial");
batesArtifact.FontColor = Color.FromArgb(255, 0, 0); // Red
```

### Hoe reset ik de teller voor een nieuw document?

Verander simpelweg `Start` voordat je `AddArtifact` aanroept. Als je veel PDF’s in een lus genereert, houd dan een teller bij in je applicatielogica.

### Is deze aanpak compatibel met versleutelde PDF’s?

Aspose.Pdf kan versleutelde PDF’s openen als je het wachtwoord opgeeft:

```csharp
var loadOptions = new LoadOptions { Password = "mySecret" };
using var pdfDocument = new Document("encrypted.pdf", loadOptions);
```

Na ontsleuteling werken dezelfde stappen om een artifact toe te voegen vlekkeloos.

## Volledig Werkend Voorbeeld

Hieronder staat het complete, kant‑klaar programma. Plak het in een console‑app, pas de paden aan, en druk op **F5**.

```csharp
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Create the Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "INV-",
            Start = 1000,
            Format = "0000",
            X = 500,
            Y = 20,
            FontSize = 10,
            FontColor = Color.Black
        };

        // Apply the artifact to every page
        pdfDocument.Pages.AddArtifact(batesArtifact);

        // Save the result
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Verwachte output:** De console print “Bates numbering added successfully!” en `output.pdf` bevat opeenvolgende labels zoals `INV‑1000`, `INV‑1001`, enz., gepositioneerd rechtsonder op elke pagina.

## Snelle Samenvatting

- **Primair doel:** **add bates numbering pdf** met Aspose.Pdf.  
- We hebben behandeld **how to add bates**, **add sequential page numbers**, en **add custom footer pdf**‑elementen via één enkel artifact.  
- De tutorial liet zien hoe je **add artifact to pdf** uitvoert, randgevallen afhandelt, en het resultaat verifieert.  

## Wat is de Volgende Stap?

- **Dynamische prefixes:** Haal waarden op uit een database om “CASE‑2023‑001”, “CASE‑2023‑002”, … te genereren.  
- **Conditionele plaatsing:** Gebruik paginagrootte‑detectie (`page.MediaBox`) om nummers te centreren op liggende pagina’s.  
- **Combineren met watermerken:** Voeg een half‑transparant logo toe naast het Bates‑nummer voor branding.  

Voel je vrij om te experimenteren—misschien ontdek je een slimmere manier om duizenden bestanden in batch te verwerken. Als je tegen problemen aanloopt, laat dan een reactie achter of raadpleeg de officiële documentatie van Aspose (die is verrassend duidelijk). Veel programmeerplezier!  

![add bates numbering pdf example](https://example.com/bates-numbering-screenshot.png "Schermafbeelding die add bates numbering pdf toont in een PDF‑viewer")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}