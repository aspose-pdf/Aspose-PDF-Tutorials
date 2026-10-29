---
category: general
date: 2026-08-14
description: Hoe bates‑nummeringsopties in C# instellen met GroupDocs. Volg deze stapsgewijze
  tutorial om aangepaste voorvoegsels en startnummers toe te voegen bij het converteren
  van Word naar PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set bates numbering options
- Bates numbering C#
- GroupDocs API
- document conversion C#
- AddBatesNumbering method
- C# PDF generation
language: nl
lastmod: 2026-08-14
og_description: Hoe je snel batesnummeringsopties instelt in C#. Deze gids laat zien
  hoe je aangepaste voorvoegsels en startnummers toevoegt bij het converteren van
  Word naar PDF.
og_image_alt: Screenshot of C# code applying Bates numbering to a PDF
og_title: Hoe bates‑nummeringsopties in C# in te stellen – stapsgewijze handleiding
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  headline: How to set bates numbering options in C# – complete guide
  type: TechArticle
- description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  name: How to set bates numbering options in C# – complete guide
  steps:
  - name: '`Document` – loads the source file.'
    text: '`Document` – loads the source file.'
  - name: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
    text: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
  - name: '`AddBatesNumbering` – the method that injects the numbering into each page.'
    text: '`AddBatesNumbering` – the method that injects the numbering into each page.'
  type: HowTo
tags:
- Bates numbering
- C#
- .NET
- GroupDocs
- PDF conversion
title: Hoe batesnummeringsopties in C# in te stellen – volledige gids
url: /nl/net/programming-with-stamps-and-watermarks/how-to-set-bates-numbering-options-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe bates numbering options in C# in te stellen – volledige gids

Als je **how to set bates numbering options** in C# nodig hebt, leidt deze gids je stap voor stap door het proces. Je leert hoe je het startnummer configureert, een prefix toevoegt en de nummering toepast tijdens het converteren van een Word‑document naar PDF met de GroupDocs API.

Documentverwerking vereist vaak unieke identificatoren op elke pagina voor juridische of archiveringsdoeleinden. Aan het einde van deze tutorial heb je een herbruikbaar fragment dat je in elk .NET‑project kunt plaatsen, of je nu een tool voor juridische ondersteuning bouwt of een geautomatiseerde rapportgenerator. Er zijn geen externe tools nodig – alleen de GroupDocs.Conversion‑bibliotheek en een paar regels C#.

## Wat je nodig hebt

Voordat je begint, zorg dat je het volgende hebt:

* .NET 6.0 SDK of later geïnstalleerd  
* Visual Studio 2022 (of een IDE die .NET ondersteunt)  
* Een geldige GroupDocs.Conversion‑licentie (de gratis proefversie werkt voor testen)  
* Een voorbeeld‑Word‑document (`input.docx`) dat je wilt nummeren  

Deze voorwaarden zorgen ervoor dat de code zonder extra configuratie draait.

## Hoe bates numbering options in te stellen – overzicht

De kern van **how to set bates numbering options** bestaat uit drie objecten:

1. `Document` – laadt het bronbestand.  
2. `BatesNumberingOptions` – bevat het startnummer, de prefix en andere opmaakdetails.  
3. `AddBatesNumbering` – de methode die de nummering in elke pagina injecteert.

Begrijpen waarom elk onderdeel bestaat, helpt je de oplossing aan te passen aan complexere scenario's, zoals aangepaste lettertypen of meertalige nummering.

## Stap 1: Installeer het GroupDocs.Conversion NuGet‑pakket

Open een terminal in je solution‑map en voer uit:

```bash
dotnet add package GroupDocs.Conversion
```

De **GroupDocs API** levert de `Document`‑klasse en de `AddBatesNumbering`‑extensiemethode die later in de tutorial worden gebruikt.

## Stap 2: Laad het bron‑document

```csharp
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;

// Step 2: Load the source Word document
Document document = new Document(@"C:\Docs\input.docx");
```

*Waarom deze stap?*  
Het laden van het bestand creëert een in‑memory‑representatie die de conversie‑engine kan manipuleren. Zonder een `Document`‑instantie kun je geen Bates‑nummering of andere transformaties toepassen.

## Stap 3: Maak de Bates‑nummeringsopties aan

```csharp
// Step 3: Configure Bates numbering
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // The first page will be numbered 1000
    StartNumber = 1000,
    // Each page will be prefixed with "CASE-"
    Prefix = "CASE-",
    // Optional: set the number format (e.g., 4 digits)
    NumberFormat = "#0000",
    // Optional: choose where the number appears (header/footer)
    Position = BatesNumberingPosition.FooterRight
};
```

*Waarom deze stap?*  
`BatesNumberingOptions` omvat alle instellingen die je nodig kunt hebben bij **setting bates numbering options**. Het aanpassen van `StartNumber` en `Prefix` laat je de output afstemmen op je case‑managementsysteem. De eigenschap `Position` bepaalt de visuele plaatsing, wat vaak een compliance‑vereiste is.

## Stap 4: Pas Bates‑nummering toe op het document

```csharp
// Step 4: Apply the numbering to every page
document.AddBatesNumbering(batesOptions);
```

De `AddBatesNumbering`‑methode doorloopt elke pagina van het geladen `Document` en voegt de geconfigureerde string in. Omdat de methode werkt op de in‑memory‑representatie, kun je extra verwerkingsstappen (bijv. watermerken) ketenen voordat je opslaat.

## Stap 5: Converteer en sla het resultaat op als PDF

```csharp
// Step 5: Define PDF conversion options (optional)
PdfConvertOptions pdfOptions = new PdfConvertOptions
{
    // Preserve original layout
    EmbedStandardFonts = true
};

// Save the numbered document as PDF
document.Save(@"C:\Docs\output.pdf", pdfOptions);
```

*Waarom deze stap?*  
Opslaan als PDF is een veelgebruikt eindformaat voor juridische documenten. Het `PdfConvertOptions`‑object laat je de output fijn afstemmen, maar is niet vereist voor basisnummering. De `Save`‑aanroep schrijft de volledig genummerde PDF naar schijf.

## Volledig, uitvoerbaar voorbeeld

Alles samengevoegd, hier is een zelfstandige console‑applicatie die je kunt compileren en uitvoeren:

```csharp
using System;
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;
using GroupDocs.Conversion.Options.Convert.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the source Word document
            Document document = new Document(@"C:\Docs\input.docx");

            // Configure Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1000,
                Prefix = "CASE-",
                NumberFormat = "#0000",
                Position = BatesNumberingPosition.FooterRight
            };

            // Apply numbering to each page
            document.AddBatesNumbering(batesOptions);

            // Optional: set PDF conversion preferences
            PdfConvertOptions pdfOptions = new PdfConvertOptions
            {
                EmbedStandardFonts = true
            };

            // Save the numbered PDF
            document.Save(@"C:\Docs\output.pdf", pdfOptions);

            Console.WriteLine("Bates numbering applied successfully. Output saved to output.pdf");
        }
    }
}
```

**Verwachte output**

Het uitvoeren van het programma maakt `output.pdf` aan waarin elke pagina een label toont zoals `CASE-1000`, `CASE-1001`, enz., geplaatst in de rechter voettekst. Open de PDF in een viewer om te verifiëren dat de nummers verschijnen zoals bedoeld.

## Veelvoorkomende valkuilen en best practices

| Probleem | Waarom het gebeurt | Hoe te voorkomen |
|----------|-------------------|-------------------|
| **Relatieve paden veroorzaken `FileNotFoundException`** | De werkmap van een console‑app kan verschillen van die van Visual Studio. | Gebruik absolute paden of `Path.Combine(AppContext.BaseDirectory, "input.docx")`. |
| **Nummering overlapt bestaande voetteksten** | Als het bron‑document al inhoud heeft in het gekozen voettekstgebied, kan het nieuwe nummer verborgen worden. | Kies een andere `Position` (bijv. `HeaderLeft`) of pas de bron‑template aan. |
| **Grote documenten zijn traag** | Bates‑nummering iterereert over elke pagina; het geheugenverbruik groeit met de bestandsgrootte. | Verwerk het document in delen met `Document.Split` als je meer dan 500 pagina’s overschrijdt. |
| **Licentie‑verloop** | De gratis proefversie van GroupDocs verloopt na 30 dagen, wat een uitzondering veroorzaakt bij `AddBatesNumbering`. | Pas een geldige licentiesleutel toe vóór het laden van het document: `License license = new License(); license.SetLicense("license.lic");`. |

**Pro‑tip:** Als je per zaak een ander nummerformaat nodig hebt (bijv. `2023-CASE-001`), bouw dan de prefix dynamisch op voordat je `BatesNumberingOptions` maakt.

## De oplossing uitbreiden

Dezelfde **Bates numbering C#**‑aanpak werkt met andere bronformaten zoals `.txt`, `.html` of zelfs afbeeldingen. Verander simpelweg de bestandsextensie bij het construeren van het `Document`‑object, en de conversie‑engine regelt de rest.

Je kunt ook **document conversion C#** combineren met OCR voor gescande PDF’s:

```csharp
// Example: add OCR before numbering (requires GroupDocs.Viewer)
using GroupDocs.Viewer;
using GroupDocs.Viewer.Options;

Document scannedPdf = new Document(@"C:\Docs\scanned.pdf");
var viewer = new Viewer(scannedPdf);
var viewOptions = new HtmlViewOptions();
viewer.View(viewOptions); // OCR step
// Then apply Bates numbering as shown earlier
```

## Conclusie

Je weet nu **how to set bates numbering options** in C# van begin tot eind. Door een `BatesNumberingOptions`‑object te maken, toe te passen met `AddBatesNumbering` en het resultaat op te slaan als PDF, kun je de productie van juridisch conforme, uniek geïdentificeerde documenten automatiseren.  

Vanaf hier kun je gerelateerde onderwerpen verkennen zoals **C# PDF generation**, **document conversion C#**, of geavanceerde **GroupDocs API**‑functies zoals watermerken en digitale handtekeningen. Experimenteer met verschillende prefixes, posities en nummerformaten om ze in jouw workflow te passen.

Happy coding!


## Wat moet je hierna leren?


De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑features onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Add Bates Numbering PDF in C# – Complete Guide](/pdf/english/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add a Text Stamp Footer in PDFs Using Aspose.PDF for .NET&#58; A Step‑By‑Step Guide](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}