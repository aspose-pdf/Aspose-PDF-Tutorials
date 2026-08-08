---
category: general
date: 2026-08-08
description: Bates-nummering toevoegen aan PDF met Aspose.Pdf in C#. Deze tutorial
  laat ook zien hoe je een lege pagina aan een PDF toevoegt en een PDF programmatically
  genereert.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering pdf
- add blank page pdf
- generate pdf programmatically
- create pdf aspose
language: nl
lastmod: 2026-08-08
og_description: Batesnummering toevoegen aan PDF met Aspose.Pdf in C#. Leer hoe je
  een lege PDF-pagina toevoegt, PDF programmatically genereert en het uiteindelijke
  document binnen enkele minuten opslaat.
og_image_alt: Screenshot of C# code adding Bates numbering and a blank page to a PDF
  using Aspose.Pdf
og_title: Bates-nummers toevoegen aan PDF met Aspose – volledige C#-gids
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  headline: Add bates numbering pdf with Aspose – step‑by‑step guide
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  name: Add bates numbering pdf with Aspose – step‑by‑step guide
  steps:
  - name: What if I need a different font or position?
    text: 'The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`,
      `HorizontalAlignment`, and `VerticalAlignment`. For example:'
  - name: How do I exclude a specific page from numbering?
    text: Create a separate `BatesNumberingArtifact` for the pages you want to number
      and add it only to those pages. Pages without an attached artifact will remain
      unnumbered.
  - name: Does this work with existing PDFs?
    text: 'Yes. Instead of `new Document()`, load an existing file:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF generation
- Bates numbering
title: Bates‑nummering toevoegen aan PDF met Aspose – stapsgewijze handleiding
url: /nl/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates‑nummers toevoegen aan pdf met Aspose – stap‑voor‑stap gids

Bates‑nummers toevoegen aan pdf met Aspose.Pdf is eenvoudig zodra je de kernstappen begrijpt. Als je ook een lege pagina pdf moet toevoegen of pdf programmatisch moet genereren, behandelt deze gids alles wat je nodig hebt.

In deze tutorial zul je:

* Een nieuw PDF‑document vanaf nul maken.  
* Een lege pdf‑pagina toevoegen die de Bates‑nummers zal bevatten.  
* Het Bates‑nummering‑artifact configureren met een aangepast voorvoegsel.  
* De PDF opslaan zodat de nummers in het gegenereerde bestand verschijnen.  

Aan het einde heb je een volledig functionele C# console‑applicatie die een PDF produceert met Bates‑nummers zoals **CASE‑1000**, **CASE‑1001**, … – een veelvoorkomende eis voor juridische en e‑discovery‑werkstromen.

## Vereisten

* .NET 6.0 SDK of later (de code werkt ook met .NET Framework 4.8).  
* Visual Studio 2022 of een andere C#‑compatibele IDE.  
* Een geldige Aspose.Pdf for .NET‑licentie (of een gratis evaluatiesleutel).  
* Basiskennis van C#‑syntaxis.

> **Pro tip:** Als je de code zonder licentie uitvoert, voegt Aspose een klein watermerk toe aan de uitvoer‑PDF.

## Stap 1: Het project instellen en Aspose.Pdf importeren

Maak een nieuw console‑project aan en voeg het Aspose.Pdf‑NuGet‑pakket toe:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

De `using`‑directieven die voor het voorbeeld nodig zijn:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
```

Deze namespaces geven je toegang tot de `Document`, `Page` en `BatesNumberingArtifact`‑klassen die later worden gebruikt.

## Stap 2: Een lege pdf‑pagina toevoegen

Een Bates‑nummer moet aan een pagina worden gekoppeld, dus we maken eerst een lege pagina die het nummer‑artifact zal ontvangen.

```csharp
// Step 2: Add a blank page pdf
Document pdfDocument = new Document();          // creates an empty PDF
Page pdfPage = pdfDocument.Pages.Add();         // adds the first (blank) page
```

De `Document`‑klasse vertegenwoordigt het volledige PDF‑bestand, terwijl `Pages.Add()` een nieuwe, lege pagina toevoegt aan het einde van de paginaverzameling van het document. Omdat het document leeg begint, maakt deze aanroep ook de eerste pagina aan.

## Stap 3: Het Bates‑nummering‑artifact configureren

Nu definiëren we hoe de Bates‑nummers eruit moeten zien. De `BatesNumberingArtifact` stelt je in staat om het startnummer, voorvoegsel, achtervoegsel en opmaakopties in te stellen.

```csharp
// Step 3: Define Bates numbering settings
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
{
    StartNumber = 1000,          // first number in the sequence
    Prefix = "CASE-",            // custom prefix before each number
    // Optional: you can also set Suffix, FontSize, FontColor, etc.
};
```

**Waarom dit belangrijk is:**  
Het instellen van `StartNumber` op **1000** komt overeen met de gebruikelijke conventies voor juridische dossiers. Het `Prefix` zorgt ervoor dat elk nummer verschijnt als **CASE‑1000**, **CASE‑1001**, …, wat zoeken en sorteren vergemakkelijkt.

## Stap 4: Het artifact aan de pagina koppelen

Het artifact moet worden toegevoegd aan de `Artifacts`‑collectie van de pagina zodat Aspose het bij het opslaan op elke pagina rendert.

```csharp
// Step 4: Attach the Bates numbering artifact to the PDF page
pdfPage.Artifacts.Add(batesArtifact);
```

Wanneer het document wordt opgeslagen, herhaalt Aspose het artifact automatisch op alle pagina's en verhoogt het nummer voor elke volgende pagina.

## Stap 5: (Optioneel) Extra pagina's toevoegen

Als je meer pagina's nodig hebt, herhaal dan eenvoudig `pdfDocument.Pages.Add()`. Het Bates‑nummering‑artifact dat je in de vorige stap hebt gekoppeld, verschijnt automatisch op elke nieuwe pagina.

```csharp
// Example: add two more pages
pdfDocument.Pages.Add();
pdfDocument.Pages.Add();
```

## Stap 6: De PDF opslaan – pdf programmatisch genereren

Sla tenslotte het document op schijf op. Dit is het moment waarop de Bates‑nummers op de pagina's worden gerenderd.

```csharp
// Step 6: Save the PDF – generate pdf programmatically
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumberedDocument.pdf");

// Ensure the directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);

pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to: {outputPath}");
```

**Verwacht resultaat:**  
Open *BatesNumberedDocument.pdf* en je ziet een PDF van drie pagina's. Elke pagina toont een Bates‑nummer in de rechter‑onderhoek:

* Pagina 1 → **CASE‑1000**  
* Pagina 2 → **CASE‑1001**  
* Pagina 3 → **CASE‑1002**

De nummers worden automatisch verhoogd omdat het artifact is gekoppeld aan de paginaverzameling.

## Volledig, uitvoerbaar voorbeeld

Alles samenvoegend, hier is een compleet console‑programma dat je kunt kopiëren, plakken en uitvoeren:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new PDF document
            Document pdfDocument = new Document();

            // Add a blank page pdf
            Page pdfPage = pdfDocument.Pages.Add();

            // Define Bates numbering settings (add bates numbering pdf)
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
            {
                StartNumber = 1000,
                Prefix = "CASE-"
            };

            // Attach the artifact to the page
            pdfPage.Artifacts.Add(batesArtifact);

            // (Optional) add more pages to see incremented numbers
            pdfDocument.Pages.Add(); // page 2
            pdfDocument.Pages.Add(); // page 3

            // Save the PDF – generate pdf programmatically
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "BatesNumberedDocument.pdf");

            Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);
            pdfDocument.Save(outputPath);

            Console.WriteLine($"PDF saved to: {outputPath}");
        }
    }
}
```

Voer het programma uit met `dotnet run`. Na uitvoering, zoek het bestand op je bureaublad en controleer de Bates‑nummers.

![Add bates numbering pdf example](/images/bates-numbering.png "Add bates numbering pdf example")

## Veelgestelde vragen en randgevallen

### Wat als ik een ander lettertype of een andere positie nodig heb?

De `BatesNumberingArtifact` biedt eigenschappen zoals `FontSize`, `FontColor`, `HorizontalAlignment` en `VerticalAlignment`. Bijvoorbeeld:

```csharp
batesArtifact.FontSize = 12;
batesArtifact.FontColor = Color.Blue;
batesArtifact.HorizontalAlignment = HorizontalAlignment.Left;
batesArtifact.VerticalAlignment = VerticalAlignment.Top;
```

### Hoe sluit ik een specifieke pagina uit van nummering?

Maak een apart `BatesNumberingArtifact` voor de pagina's die je wilt nummeren en voeg het alleen aan die pagina's toe. Pagina's zonder gekoppeld artifact blijven ongenummerd.

### Werkt dit met bestaande PDF's?

Ja. In plaats van `new Document()`, laad een bestaand bestand:

```csharp
Document pdfDocument = new Document("input.pdf");
```

Koppel vervolgens het artifact aan de gewenste pagina's en sla op.

## Conclusie

Je weet nu hoe je **bates numbering pdf** kunt toevoegen met Aspose.Pdf, hoe je **blank page pdf** kunt toevoegen, en hoe je **pdf programmatisch kunt genereren** in een schone, herbruikbare C#‑oplossing. De aanpak werkt met elk aantal pagina's, aangepaste voorvoegsels en stijlopties, waardoor je volledige controle over het uiteindelijke document hebt.

Volgende stappen die je kunt verkennen:

* Use **create pdf as

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add an Empty Page at the End of a PDF Using Aspose.PDF for .NET | Step-by-Step Guide](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)
- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}