---
category: general
date: 2026-07-20
description: 'PDF-document maken in C# met Aspose.Pdf: tekst positioneren in PDF en
  een structurele boom toevoegen voor toegankelijkheid. Volg deze stapsgewijze handleiding.'
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document c#
- position text in pdf
- add structural tree
- Aspose.Pdf tagging
- PDF/A‑2b generation
language: nl
lastmod: 2026-07-20
og_description: Maak direct een PDF‑document in C#. Leer hoe je tekst in een PDF positioneert
  en een structurele boom toevoegt met Aspose.Pdf voor PDF/A‑2b‑naleving.
og_image_alt: Screenshot showing positioned text inside a PDF generated with Aspose.Pdf
  in C#
og_title: PDF-document maken in C# – Volledige gids voor het positioneren van tekst
  en tagstructuur
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: 'Create PDF document C# with Aspose.Pdf: position text in PDF and add
    structural tree for accessibility. Follow this step‑by‑step guide.'
  headline: Create PDF Document C# – Position Text and Add Structural Tree
  type: TechArticle
- description: 'Create PDF document C# with Aspose.Pdf: position text in PDF and add
    structural tree for accessibility. Follow this step‑by‑step guide.'
  name: Create PDF Document C# – Position Text and Add Structural Tree
  steps:
  - name: Can I use other units (mm, cm) for positioning?
    text: Aspose.Pdf works natively with points. If you prefer millimeters, convert
      using `1 mm ≈ 2.83465 pt`. For example, `Position(25.4, 254)` places the paragraph
      1 cm from the left and 9 cm from the bottom.
  - name: What if I need to add multiple tags (headings, tables)?
    text: Simply create additional `StructureElement` objects with tags like `"H1"`
      for headings or `"Table"` for tables, and add the corresponding content as kids.
      Nesting works the same way—children inherit the parent’s logical order.
  - name: Does this approach work for PDF/A‑1b or PDF/A‑3b?
    text: Yes. Replace `SaveFormat.PdfA2b` with `SaveFormat.PdfA1b` or `SaveFormat.PdfA3b`.
      Keep in mind that each PDF/A version has its own set of required metadata; Aspose.Pdf
      will prompt you if something is missing.
  type: HowTo
tags:
- C#
- PDF
- Aspose.Pdf
title: PDF-document maken in C# – Tekst positioneren en structuurboom toevoegen
url: /nl/net/programming-with-tagged-pdf/create-pdf-document-c-position-text-and-add-structural-tree/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF-document maken C# – Tekst positioneren en structurele boom toevoegen

Heb je ooit een **create PDF document C#** nodig gehad die niet alleen tekst precies daar plaatst waar je wilt, maar ook een juiste structurele boom voor toegankelijkheid invoegt? Je bent niet de enige—ontwikkelaars die facturen, rapporten of e‑books maken, hebben deze behoefte voortdurend. In deze tutorial lopen we een compleet, kant‑klaar voorbeeld door dat precies dat doet, met behulp van de krachtige Aspose.Pdf bibliotheek.

We behandelen hoe je **position text in PDF** kunt doen, een semantische tag kunt toevoegen via de **add structural tree** stap, en uiteindelijk het bestand opslaat als een PDF/A‑2b‑conform document. Aan het einde heb je een herbruikbare snippet die je in elk .NET‑project kunt gebruiken.

---

## Wat je nodig hebt

- **.NET 6.0** of later (de code werkt ook met .NET Framework 4.6+)  
- **Aspose.Pdf for .NET** NuGet‑pakket (`Install-Package Aspose.Pdf`)  
- Een basis C#‑ontwikkelomgeving (Visual Studio, Rider of VS Code)  

Er zijn geen extra third‑party tools nodig; de bibliotheek regelt alles van paginalay‑out tot PDF/A‑conformiteit.

---

## Stap 1: PDF-document initialiseren (Create PDF Document C#)

Het eerste wat we doen is een nieuw `Document`‑object aanmaken. Beschouw het als een leeg canvas—nog niets erop, maar klaar om pagina’s, tekst en structurele metadata te ontvangen.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Struct;

// Create a new PDF document – this is the core of our create pdf document c# workflow
Document pdfDoc = new Document();

// Add a blank page to the document; the page will host our positioned text
Page pdfPage = pdfDoc.Pages.Add();
```

> **Waarom dit belangrijk is:** De `Document`‑klasse is het toegangspunt voor alle Aspose.Pdf‑bewerkingen. Een pagina vroeg toevoegen geeft ons een oppervlak om zowel visuele inhoud als later de structurele boom eraan te koppelen.

---

## Stap 2: Een alinea definiëren en positioneren (Position Text in PDF)

Nu maken we een `Paragraph`‑object en vertellen we Aspose precies waar op de pagina het moet verschijnen. PDF‑coördinaten worden gemeten in points (1 inch = 72 pt), dus we gebruiken `Position(72, 720)` om de alinea 1 inch van de linkerrand en 10 inches van de onderkant te plaatsen.

```csharp
// Define a paragraph positioned 1 inch from the left and 10 inches from the bottom
Paragraph positionedParagraph = new Paragraph
{
    // Position(x, y) – X is horizontal, Y is vertical from the bottom-left corner
    Position = new Position(72, 720) // 72 pt = 1 inch, 720 pt = 10 inch
};

// Add the actual text we want to display
positionedParagraph.Segments.Add(
    new TextFragment("Tagged paragraph at a specific location.")
);
```

> **Pro tip:** Als je meerdere regels moet positioneren, pas dan de `Y`‑coördinaat voor elke volgende alinea aan, of gebruik een `TextBuilder` voor fijnere controle.

---

## Stap 3: Een structureel element maken (Add Structural Tree)

Toegankelijkheids‑bewuste PDF’s vertrouwen op een *structure tree* die de logische volgorde van de inhoud beschrijft. Hier maken we een `StructureElement` met de tag `"P"` (paragraph) en koppelen we onze gepositioneerde alinea als kind.

```csharp
// Create a structural element (tag) for the paragraph – this is the add structural tree step
StructureElement structElement = new StructureElement("P");

// Attach the paragraph as a child of the structural element
structElement.AddKid(positionedParagraph);
```

> **Waarom we een structurele boom toevoegen:** Schermlezers en andere assistieve technologieën gebruiken deze tags om door het document te navigeren. Zonder deze tags is je PDF visueel perfect maar ontoegankelijk.

---

## Stap 4: Het structurele element aan de pagina koppelen

Elke pagina heeft zijn eigen collectie van structurele elementen. Door ons `structElement` toe te voegen aan `pdfPage.StructElements`, integreren we de logische hiërarchie met de visuele lay‑out.

```csharp
// Attach the structural element to the page's structure tree
pdfPage.StructElements.Add(structElement);
```

> **Veelgemaakte valkuil:** Als je deze stap vergeet, bestaat de tag wel in het geheugen, maar is hij niet gekoppeld aan een pagina, waardoor de toegankelijkheidsinformatie onzichtbaar blijft voor lezers.

---

## Stap 5: Opslaan als PDF/A‑2b (Zorg voor langdurige bewaring)

PDF/A‑2b is een subset van PDF ontworpen voor archivering. Aspose.Pdf kan dit formaat met één enkele aanroep produceren. Vervang `"YOUR_DIRECTORY"` door een echt pad op jouw machine.

```csharp
// Save the document as a PDF/A‑2b file – ideal for long‑term storage and compliance
pdfDoc.Save("YOUR_DIRECTORY/TaggedWithPosition.pdf", SaveFormat.PdfA2b);
```

> **Resultaat:** Je hebt nu een PDF waarin de tekst precies staat waar je hem hebt geplaatst, en het document bevat een juiste structurele boom voor toegankelijkheidstools.

---

## Volledig werkend voorbeeld

Hieronder staat het complete programma dat je kunt kopiëren‑plakken in een console‑applicatie. Het compileert en draait direct (zodra je de Aspose.Pdf NuGet‑referentie hebt toegevoegd).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Struct;

namespace PdfPositioningDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Initialize the document
            Document pdfDoc = new Document();
            Page pdfPage = pdfDoc.Pages.Add();

            // Step 2: Define and position the paragraph
            Paragraph positionedParagraph = new Paragraph
            {
                Position = new Position(72, 720) // 1 inch left, 10 inches up
            };
            positionedParagraph.Segments.Add(
                new TextFragment("Tagged paragraph at a specific location.")
            );

            // Step 3: Create the structural element (tag)
            StructureElement structElement = new StructureElement("P");
            structElement.AddKid(positionedParagraph);

            // Step 4: Attach the structural element to the page
            pdfPage.StructElements.Add(structElement);

            // Step 5: Save as PDF/A‑2b
            string outputPath = @"C:\Temp\TaggedWithPosition.pdf";
            pdfDoc.Save(outputPath, SaveFormat.PdfA2b);

            Console.WriteLine($"PDF created successfully at: {outputPath}");
        }
    }
}
```

**Verwachte output:** Na het uitvoeren, open `TaggedWithPosition.pdf`. Je ziet de zin “Tagged paragraph at a specific location.” dicht bij de rechter‑onderhoek van de eerste pagina. Als je de tags van de PDF inspecteert (bijv. met Adobe Acrobat’s “Tags”‑paneel), vind je een `<P>`‑element gekoppeld aan die alinea.

---

![Screenshot van gepositioneerde tekst in een PDF gegenereerd met Aspose.Pdf](/images/pdf-positioned.png){: .align-center }

*Afbeeldingsalt‑tekst:* **create pdf document c#** – screenshot die gepositioneerde tekst binnen een PDF gegenereerd met Aspose.Pdf toont.

---

## Veelgestelde vragen & randgevallen

### Kan ik andere eenheden (mm, cm) gebruiken voor positionering?

Aspose.Pdf werkt natively met points. Als je millimeters verkiest, converteer dan met `1 mm ≈ 2.83465 pt`. Bijvoorbeeld, `Position(25.4, 254)` plaatst de alinea 1 cm van de linkerkant en 9 cm van de onderkant.

### Wat als ik meerdere tags moet toevoegen (koppen, tabellen)?

Maak eenvoudig extra `StructureElement`‑objecten met tags zoals `"H1"` voor koppen of `"Table"` voor tabellen, en voeg de bijbehorende inhoud als kinderen toe. Nesting werkt op dezelfde manier—kinderen erven de logische volgorde van de ouder.

### Werkt deze aanpak voor PDF/A‑1b of PDF/A‑3b?

Ja. Vervang `SaveFormat.PdfA2b` door `SaveFormat.PdfA1b` of `SaveFormat.PdfA3b`. Houd er rekening mee dat elke PDF/A‑versie zijn eigen set verplichte metadata heeft; Aspose.Pdf zal je waarschuwen als er iets ontbreekt.

---

## Samenvatting

We hebben een **create pdf document c#**‑scenario doorlopen dat:

1. Een nieuw PDF‑document instantiateert met Aspose.Pdf.  
2. **Position text in PDF** door exacte coördinaten te zetten.  
3. **Add structural tree**‑elementen toevoegt voor toegankelijkheid.  
4. Het resultaat opslaat als een standaarden‑conform PDF/A‑2b‑bestand.

Alle stappen zijn volledig zelf‑voorzienend, en je kunt de snippet aanpassen voor complexere lay‑outs, meerdere pagina’s, of verschillende tag‑typen.

---

## Wat volgt?

- **Tekst stylen** – verken `TextState` om lettertypen, kleuren en groottes te wijzigen.  
- **Afbeeldingen insluiten** – gebruik `ImageFragment` en positioneer deze naast de alinea.  
- **Tabellen genereren** – maak `Table`‑objecten en tag ze met `"Table"` voor rijkere semantiek.  
- **Automatiserings‑pipelines** – integreer deze code in een achtergrondservice die ’s nachts facturen genereert.

Voel je vrij om te experimenteren, en laat ons weten welke variaties je het meest nuttig vindt. Happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Gepersonaliseerde PDF's maken met Aspose.PDF voor .NET: Een complete gids voor het verbeteren van toegankelijkheid en documentstructuur](/pdf/english/net/advanced-features/create-tagged-pdfs-aspose-pdf-net/)
- [PDF-document maken met Aspose.PDF – Stapsgewijze gids](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Tekst maken & roteren in PDF's met Aspose.PDF .NET: Een uitgebreide gids voor ontwikkelaars](/pdf/english/net/text-operations/create-rotate-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}