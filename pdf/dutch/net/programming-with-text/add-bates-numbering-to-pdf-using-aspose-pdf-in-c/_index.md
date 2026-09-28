---
category: general
date: 2026-09-27
description: Voeg Bates‑nummering toe aan PDF met Aspose.PDF in C#. Leer hoe je een
  PDF‑document laadt, Bates‑nummeringsopties instelt en het bijgewerkte bestand opslaat.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- load pdf document
- how to add bates numbering
- Aspose.PDF C#
- PDF Bates numbering example
language: nl
lastmod: 2026-09-27
og_description: Voeg Bates‑nummering toe aan PDF met Aspose.PDF in C#. Deze tutorial
  laat zien hoe je een PDF‑document laadt, Bates‑nummering configureert en het resultaat
  opslaat.
og_image_alt: Screenshot of a PDF page displaying Bates numbers in the footer
og_title: Bates-nummers toevoegen aan PDF met Aspose.PDF – C#-gids
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Add bates numbering to PDF using Aspose.PDF in C#. Learn how to load
    a PDF document, set Bates numbering options, and save the updated file.
  headline: Add bates numbering to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF processing
title: Batesnummering toevoegen aan PDF met Aspose.PDF in C#
url: /nl/net/programming-with-text/add-bates-numbering-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates‑nummering toevoegen aan PDF met Aspose.PDF in C#

Als je **Bates‑nummering** aan een PDF‑bestand wilt toevoegen, laat deze gids je een volledige, kant‑klaar oplossing zien. Je ziet hoe je een **PDF‑document laadt**, de Bates‑nummeringsopties configureert en het genummerde bestand terug naar schijf schrijft – alles met Aspose.PDF voor .NET.

Het toepassen van Bates‑nummers is gebruikelijk in juridische, wetshandhavings‑ en archiveringsprocessen. Aan het einde van deze tutorial kun je een opeenvolgende identificatie op elke pagina insluiten, het voorvoegsel aanpassen en de telling laten starten bij elk gewenst getal.

## Wat je leert

* Hoe je **PDF‑document**‑inhoud laadt in een `Aspose.Pdf.Document`‑object.  
* De exacte stappen **hoe je Bates‑nummering toevoegt** met `BatesNumberingOptions`.  
* Hoe je het gewijzigde bestand opslaat terwijl de oorspronkelijke lay‑out en kwaliteit behouden blijven.  

Er zijn geen externe tools nodig – alleen het Aspose.PDF NuGet‑pakket en een .NET‑ontwikkelomgeving (Visual Studio, VS Code of Rider).  

---

## Stap 1: Installeer Aspose.PDF voor .NET

Open je projectmap in een terminal en voer uit:

```bash
dotnet add package Aspose.PDF
```

Het pakket bevat de `Aspose.Pdf`‑namespace, die alle klassen levert die in deze tutorial worden gebruikt. Na installatie herlaad je het project zodat de IDE de nieuwe referentie oppikt.

## Stap 2: Laad PDF‑document

Het laden van het bronbestand is de eerste handeling omdat de Bates‑nummeringsengine werkt op een bestaand `Document`‑object.

```csharp
using Aspose.Pdf;

// ...

// Replace with the path to your input PDF
string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Load the PDF document into memory
Document doc = new Document(inputPath);
```

**Waarom dit belangrijk is:** De `Document`‑klasse parseert de PDF‑structuur en geeft je toegang tot pagina’s, annotaties en metadata. Zonder het bestand eerst te laden kun je geen nummering toepassen.

## Stap 3: Configureer Bates‑nummeringsopties

Maak een `BatesNumberingOptions`‑object aan en stel het gewenste voorvoegsel, startnummer en optionele opmaakparameters in.

```csharp
using Aspose.Pdf;

// ...

BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Text that appears before the numeric part
    Prefix = "CASE01",

    // First number to use (1 means the first page gets CASE01-1)
    StartNumber = 1,

    // Optional: customize the appearance
    // The default places the number in the footer, centered.
    // You can change Font, FontSize, Color, and Position if needed.
    // Example:
    // Font = FontRepository.FindFont("Arial"),
    // FontSize = 10,
    // Color = Color.Black,
    // Margin = new Margin(0, 0, 0, 20)
};
```

**Waarom dit belangrijk is:** `BatesNumberingOptions` vertelt Aspose.PDF hoe het label voor elke pagina moet worden gegenereerd. Het `Prefix` helpt je gerelateerde zaken te groeperen, terwijl `StartNumber` je in staat stelt een reeks voort te zetten vanaf een eerdere batch.

## Stap 4: Sla de PDF op met toegepaste Bates‑nummers

Geef het opties‑object door aan de `Save`‑methode. Aspose.PDF schrijft de nummers direct op elke pagina.

```csharp
// Replace with the desired output path
string outputPath = @"YOUR_DIRECTORY\output.pdf";

// Save the document, applying the Bates numbering
doc.Save(outputPath, batesOptions);
```

**Waarom dit belangrijk is:** De overload `Save(string, BatesNumberingOptions)` combineert de renderstap met het nummeringsproces, zodat het uitvoerbestand de zichtbare identificatoren bevat.

## Volledig voorbeeld – alles samen

Hieronder staat een enkel, zelfstandig programma dat je kunt kopiëren, plakken en uitvoeren. Het demonstreert **hoe je Bates‑nummering toevoegt** van begin tot eind.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the PDF document
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Set up Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                Prefix = "CASE01",
                StartNumber = 1,
                // Optional appearance tweaks:
                // Font = FontRepository.FindFont("Times New Roman"),
                // FontSize = 9,
                // Color = Color.DarkBlue,
                // Margin = new Margin(0, 0, 0, 15)
            };

            // 3️⃣ Save the document with Bates numbers
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath, batesOptions);

            Console.WriteLine($"Bates numbering added. Output saved to: {outputPath}");
        }
    }
}
```

### Verwachte output

Het uitvoeren van het programma levert `output.pdf` op waarin elke pagina een label toont dat lijkt op:

```
CASE01-1
CASE01-2
CASE01-3
...
```

Standaard verschijnen de nummers in de voettekst, maar je kunt ze verplaatsen door de `Margin`‑eigenschap in `BatesNumberingOptions` aan te passen.

## Randgevallen en veelvoorkomende variaties

| Situatie | Wat aan te passen |
|-----------|-------------------|
| **Verschillend voorvoegsel per batch** | Wijzig `Prefix` vóór het aanroepen van `Save`. Je kunt over meerdere documenten met verschillende voorvoegsels itereren. |
| **Nummering voortzetten vanaf een vorig bestand** | Stel `StartNumber` in op het laatst gebruikte nummer + 1. |
| **Nummers in de kop plaatsen** | Gebruik `batesOptions.Margin = new Margin(20, 0, 0, 0);` (bovenmarge) of pas `batesOptions.Position` aan. |
| **Aangepast lettertype of kleur** | Ken `Font`, `FontSize` en `Color` toe zoals getoond in het commentaargedeelte. |
| **Grote PDF’s (1000+ pagina’s)** | De bewerking is geheugen‑efficiënt; je kunt echter `doc.OptimizeResources()` inschakelen vóór het opslaan om de bestandsgrootte te verkleinen. |

**Pro‑tip:** Als je workflow verschillende nummeringsschema’s per document vereist, verpak de logica dan in een hulpfunctie:

```csharp
static void ApplyBatesNumbering(string src, string dst, string prefix, int start)
{
    var doc = new Document(src);
    var opts = new BatesNumberingOptions { Prefix = prefix, StartNumber = start };
    doc.Save(dst, opts);
}
```

## Conclusie

Je weet nu **hoe je Bates‑nummering toevoegt** aan elke PDF met Aspose.PDF in C#. De tutorial behandelde het laden van het PDF‑document, het configureren van de nummeringsopties en het opslaan van het uiteindelijke bestand – alles in één uitvoerbaar programma.  

Vanaf hier kun je gerelateerde onderwerpen verkennen, zoals **watermerken toevoegen**, **meerdere PDF’s samenvoegen** of **tekst extraheren** met Aspose.PDF. Experimenteer met verschillende lettertypen, kleuren en posities om te voldoen aan de opmaakstandaarden van jouw organisatie.

Klaar om je juridische documentworkflow te automatiseren? Voeg de code toe aan je build‑pipeline, voer het uit tegen batches bestanden, en laat Aspose.PDF het zware werk doen. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Create PDF Document C# – Add Bates Numbering](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/)
- [Add Bates Numbering PDF – Step‑by‑Step Guide to Number PDF Pages](/pdf/english/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/)
- [Aspose PDF Tutorial – Insert a Blank Page and Update Bates Numbering](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}