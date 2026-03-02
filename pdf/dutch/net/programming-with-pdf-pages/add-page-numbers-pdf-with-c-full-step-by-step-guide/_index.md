---
category: general
date: 2026-01-02
description: Voeg snel paginanummers toe aan PDF met Aspose.Pdf in C#. Leer hoe je
  batesnummering, voettekst, aangepaste watermerk toevoegt en door PDF-pagina's loopt
  in één script.
draft: false
keywords:
- add page numbers pdf
- add bates numbering
- add footer text
- add custom watermark
- loop through pdf pages
language: nl
og_description: Voeg direct paginanummers toe aan PDF met Aspose.Pdf. Deze gids behandelt
  ook het toevoegen van Bates-nummers, voettekst, aangepaste watermerken en het doorlopen
  van PDF-pagina's.
og_title: Voeg paginanummers toe aan PDF met C# – Volledige programmeertutorial
tags:
- C#
- Aspose.Pdf
- PDF manipulation
title: Paginanummers toevoegen aan PDF met C# – Volledige stapsgewijze handleiding
url: /nl/net/programming-with-pdf-pages/add-page-numbers-pdf-with-c-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pagina nummers toevoegen pdf met C# – Complete Programmeertutorial

Heb je ooit **pagina nummers toevoegen pdf** bestanden nodig gehad, maar wist je niet waar te beginnen? Je bent niet de enige—ontwikkelaars vragen constant hoe ze nummers, voetteksten of zelfs een Bates‑stijl identifier op elke pagina van een PDF kunnen stempelen.  

In deze tutorial zie je een kant‑klaar C#‑voorbeeld dat **door pdf‑pagina's loopt**, een paginanummer‑voettekst stempelt, en (optioneel) een aangepaste watermerk toevoegt. We laten ook zien hoe je de stempel kunt omzetten naar een Bates‑nummer, wat simpelweg betekent “Bates‑nummering toevoegen” voor juridische of forensische documenten. Aan het einde heb je een enkele, herbruikbare methode die al deze taken afhandelt zonder moeite.

## Pagina nummers toevoegen pdf – Overzicht

Voordat we in de code duiken, laten we verduidelijken wat “pagina nummers toevoegen pdf” echt betekent in de Aspose.Pdf‑wereld. De bibliotheek behandelt elk stuk tekst dat je op een pagina plaatst als een **TextStamp**. Door één stempel te maken met een paginaplaathouder (`{page}`) en deze op elke pagina toe te passen, krijg je automatisch opeenvolgende nummering. dezelfde stempel kan extra tekst bevatten, zodat je **voettekst toevoegen** kunt doen, zoals “Vertrouwelijk” of een zaak‑specifieke identifier.

> **Waarom een stempel gebruiken in plaats van de PDF‑content‑stream te bewerken?**  
> Stempels zijn high‑level objecten die paginamarges, rotatie en bestaande grafische elementen respecteren. Ze zijn bovendien veel makkelijker te onderhouden—wijzig een paar eigenschappen en voer het script opnieuw uit.

## Door PDF‑pagina's lopen om stempels toe te passen

De eerste praktische stap is het openen van de bron‑PDF en itereren over de pagina's. Dit is het klassieke **loop through pdf pages**‑patroon dat de meeste Aspose‑voorbeelden gebruiken.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Paths – change these to match your environment
string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // The loop – every Page object lives in pdfDocument.Pages
    foreach (Page page in pdfDocument.Pages)
    {
        // We'll attach a stamp later (see next section)
    }

    // Save the modified document
    pdfDocument.Save(outputPdfPath);
}
```

> **Pro tip:** Als je PDF enorm is (honderden pagina's), overweeg dan om deze in batches te verwerken om het geheugenverbruik laag te houden. Aspose.Pdf streamt pagina's lui, dus de lus zelf is al behoorlijk efficiënt.

## Bates‑nummering en voettekst toevoegen

Nu we door elke pagina kunnen lopen, laten we een **herbruikbare TextStamp** maken die zowel het paginanummer als optionele voettekst bevat. De `{page}`‑plaatsaanduiding wordt automatisch vervangen door het huidige paginanummer.

```csharp
// Create a stamp that will be reused for every page
var batesStamp = new TextStamp("Bates-{page} – Confidential")
{
    // Position the stamp 20 points from the left and bottom edges
    XIndent = 20,
    YIndent = 20,
    // Align left‑bottom so it behaves like a traditional footer
    HorizontalAlignment = HorizontalAlignment.Left,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Font styling – Times New Roman, 10pt, bold, gray
    Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Gray }
};

// Attach the stamp to every page
foreach (Page page in pdfDocument.Pages)
    page.AddStamp(batesStamp);
```

### Waarom dit werkt

* **`Bates-{page}`** – Aspose vervangt `{page}` door het daadwerkelijke paginanummer, waardoor je automatisch een klassieke Bates‑nummer krijgt.
* **`Confidential`** – Dit is het **add footer text**‑gedeelte. Je kunt het vervangen door elke string, zelfs data uit een database halen.
* **Styling** – Met `TextState` kun je kleur, doorzichtigheid en zelfs rotatie aanpassen zonder de interne content‑streams van de PDF aan te raken.

Als je alleen platte nummers nodig hebt, laat dan het “Bates‑”‑voorvoegsel en de extra tekst weg:

```csharp
var simpleStamp = new TextStamp("{page}")
{
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    Font = new Font(FontFamily.Helvetica, 12, FontStyle.Regular),
    TextState = { ForegroundColor = Color.Black }
};
```

## Een aangepast watermerk toevoegen (optioneel)

Soms wil je meer dan alleen een voettekst—je hebt een semi‑transparant logo of een “DRAFT”‑overlay over de hele pagina nodig. Dan komt **add custom watermark** van pas. Dezelfde `TextStamp`‑klasse kan opnieuw worden gebruikt; wijzig alleen de uitlijning en doorzichtigheid.

```csharp
var watermark = new TextStamp("DRAFT")
{
    // Center it both horizontally and vertically
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Center,
    // Make it big and light
    Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Red, FontSize = 72, FontStyle = FontStyle.Bold, 
                  Transparency = 0.5f }   // 50% transparent
};

// Apply the watermark on top of the page‑number stamp
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(watermark);   // watermark on top
    page.AddStamp(batesStamp);  // then the footer
}
```

> **Opmerking:** Volgorde is belangrijk. Het watermerk eerst toevoegen zorgt ervoor dat de paginanummers leesbaar blijven boven de semi‑transparante tekst.

## De PDF opslaan en resultaten verifiëren

Na het stempelen is de laatste stap de wijzigingen terug naar schijf schrijven. De `Save`‑aanroep die we eerder plaatsten doet het zware werk, maar laten we een korte verificatiesnippet toevoegen die het nieuwe bestand opent en print hoeveel pagina's verwerkt zijn.

```csharp
pdfDocument.Save(outputPdfPath);

// Quick verification
using (var resultDoc = new Document(outputPdfPath))
{
    Console.WriteLine($"✅ Successfully added page numbers to {resultDoc.Pages.Count} pages.");
}
```

Wanneer je het volledige programma uitvoert, zou je een PDF moeten zien waarbij elke pagina eindigt met iets als **“Bates‑3 – Confidential”** (of alleen “3” als je de eenvoudige stempel gebruikte) en, als je het watermerk hebt ingeschakeld, een zwakke “DRAFT” over het midden.

### Verwachte output

| Pagina | Voettekst (voorbeeld) |
|--------|-----------------------|
| 1      | Bates‑1 – Confidential |
| 2      | Bates‑2 – Confidential |
| …      | … |
| N      | Bates‑N – Confidential |

Als je het bestand in een viewer opent, staan de nummers 20 pts vanaf de linker‑ en ondermarge, conform de gebruikelijke conventies voor juridische documenten.

## Volledig werkend voorbeeld (klaar om te kopiëren en plakken)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // ---------- Create the page‑number/footer stamp ----------
    var batesStamp = new TextStamp("Bates-{page} – Confidential")
    {
        XIndent = 20,
        YIndent = 20,
        HorizontalAlignment = HorizontalAlignment.Left,
        VerticalAlignment   = VerticalAlignment.Bottom,
        Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Gray }
    };

    // ---------- Optional watermark ----------
    var watermark = new TextStamp("DRAFT")
    {
        HorizontalAlignment = HorizontalAlignment.Center,
        VerticalAlignment   = VerticalAlignment.Center,
        Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Red, Transparency = 0.5f }
    };

    // ---------- Apply stamps to every page ----------
    foreach (Page page in pdfDocument.Pages)
    {
        page.AddStamp(watermark);   // comment out if you don't need a watermark
        page.AddStamp(batesStamp);
    }

    // ---------- Save and verify ----------
    pdfDocument.Save(outputPdfPath);
    Console.WriteLine($"✅ Added page numbers and watermark to {pdfDocument.Pages.Count} pages.");
}
```

Sla dit op als `AddPageNumbers.cs`, herstel het Aspose.Pdf NuGet‑pakket (`Install-Package Aspose.Pdf`), en voer het uit. Je krijgt een **add page numbers pdf** bestand dat ook **add bates numbering**, **add footer text**, **add custom watermark**, en het klassieke **loop through pdf pages**‑patroon demonstreert—alles in één net script.

![add page numbers pdf example](https://example.com/images/add-page-numbers-pdf.png "Screenshot showing numbered PDF pages with footer and watermark")

## Conclusie

We hebben alles behandeld wat je nodig hebt om **pagina nummers toevoegen pdf** bestanden te maken met Aspose.Pdf in C#. Van het doorlopen van elke pagina, tot het stempelen van Bates‑nummers, het toevoegen van aangepaste voettekst, en zelfs het leggen van een semi‑transparant watermerk, de code is compact genoeg om in elk bestaand project te plaatsen.  

Vervolgens kun je meer geavanceerde scenario’s verkennen—zoals de voettekst uit een database halen, verschillende lettertypen per sectie toepassen, of een aparte index‑PDF genereren die alle Bates‑nummers opsomt. Al deze uitbreidingen bouwen voort op dezelfde kernideeën die we hier hebben getoond, zodat je goed gepositioneerd bent om de oplossing uit te breiden naarmate je eisen groeien.  

Probeer het, pas de styling aan, en laat in de reacties weten hoe het voor jou werkte. Veel programmeerplezier!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}