---
category: general
date: 2026-03-03
description: PDF-document maken in C# met Bates-nummering – leer hoe je Bates toevoegt,
  opeenvolgende paginanummers toevoegt en Bates genereert in slechts een paar stappen.
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- how to generate bates
language: nl
og_description: Maak PDF-document C# met Bates‑nummering. Deze gids laat zien hoe
  je Bates toevoegt, opeenvolgende paginanummers toevoegt en Bates snel genereert.
og_title: PDF-document maken C# – Bates‑nummering toevoegen
tags:
- C#
- PDF
- Bates numbering
title: PDF-document maken in C# – Bates‑nummering toevoegen
url: /nl/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF-document maken C# – Bates-nummers toevoegen

Heb je ooit **PDF-document maken C#** nodig gehad en vervolgens elke pagina willen markeren met een unieke identifier voor juridische of archiveringsdoeleinden? Je bent niet de enige—advocatenkantoren, rechtbanken en zelfs grote bedrijven vragen voortdurend: “Hoe voeg ik Bates-nummers automatisch toe aan mijn PDF's?” Het goede nieuws is dat je met een paar regels code een PDF kunt genereren, Bates-nummers over elke pagina kunt strooien, en het resultaat kunt opslaan zonder ooit een editor te openen.

In deze tutorial lopen we een praktisch, end‑to‑end voorbeeld door dat laat zien **hoe je Bates toevoegt**, hoe je **volgnummer pagina's toevoegt**, en zelfs hoe je **Bates genereert** met aangepaste prefixes. Aan het einde heb je een herbruikbare codefragment die je in elk .NET‑project kunt gebruiken.

## Wat je nodig hebt

- **.NET 6+** (de code werkt ook op .NET Framework 4.6+)
- **Aspose.Pdf for .NET** – een commerciële bibliotheek die een nette API biedt voor PDF-manipulatie. Een gratis evaluatieversie werkt prima voor testen.
- Een basisbegrip van C# (je bent waarschijnlijk al vertrouwd met `using`‑statements en objecten).

Er zijn geen extra NuGet‑pakketten vereist naast `Aspose.Pdf`. Als je het nog niet hebt geïnstalleerd, voer dan uit:

```bash
dotnet add package Aspose.Pdf
```

> **Pro tip:** Houd je Aspose‑versie up‑to‑date; de nieuwste 23.x‑release voegt prestatie‑verbeteringen toe voor grote documenten.

## Stap 1: Open (of maak) het bron‑PDF‑document

Eerst hebben we een PDF nodig om mee te werken. In veel praktijksituaties heb je al een invoerbestand—bijvoorbeeld een gescand contract. Voor dit voorbeeld openen we een bestaand bestand genaamd `input.pdf`.

```csharp
using Aspose.Pdf;

// Step 1 – Load the PDF you want to number
var pdfPath = @"C:\Docs\input.pdf";
using var pdfDocument = new Document(pdfPath);
```

> **Waarom dit belangrijk is:** Het openen van het document binnen een `using`‑block garandeert dat de bestands‑handle snel wordt vrijgegeven, waardoor bestands‑lock‑problemen worden voorkomen wanneer je later probeert hetzelfde bestand te overschrijven.

## Stap 2: Definieer je Bates‑nummeringsopties

Bates‑nummers bestaan uit een **prefix** (vaak een zaak‑identificatie) en een **startnummer**. Je kunt ook het aantal cijfers, de plaatsing op de pagina en de lettertype‑stijl bepalen. Hier gebruiken we het secundaire trefwoord **add bates numbering pdf** door een `BatesNumberingOptions`‑object te configureren.

```csharp
// Step 2 – Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    // Primary keyword in action: create pdf document c# with custom settings
    Prefix = "CASE-",
    Start = 1000,
    // Optional: set zero‑padding to 6 digits (e.g., CASE-001000)
    NumberOfDigits = 6,
    // Optional: define where the number appears (bottom‑right corner)
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Optional: choose a readable font
    Font = FontRepository.FindFont("Arial")
};
```

> **Hoe Bates toe te voegen:** Door `Prefix` en `Start` aan te passen bepaal je de exacte tekenreeks die op elke pagina verschijnt. De eigenschap `NumberOfDigits` zorgt voor een consistente breedte, wat handig is voor juridische indieningen.

## Stap 3: Pas Bates‑nummering toe op elke pagina

Nu volgt de kernoperatie—het toevoegen van de nummers. De `AddBatesNumbering`‑methode doorloopt elke pagina, tekent de tekst, en respecteert de opties die we hebben gedefinieerd.

```csharp
// Step 3 – Apply Bates numbering to all pages
pdfDocument.AddBatesNumbering(batesOptions);
```

Onder de motorkap rendert Aspose de tekst als een *content*‑element, wat betekent dat de nummers onderdeel van de PDF worden en niet uitgeschakeld kunnen worden in een viewer. Dit is precies wat je nodig hebt wanneer je **volgnummer pagina's wilt toevoegen** die onveranderlijk zijn.

### Randgevallen & Variaties

- **Meerdere prefixes:** Als je verschillende prefixes per sectie nodig hebt, maak dan aparte `BatesNumberingOptions` en roep `AddBatesNumbering` aan op een paginabereik (`pdfDocument.Pages[1..5]`).
- **Zero‑padding controle:** Laat `NumberOfDigits` weg voor een variabel‑lengte nummer, of stel het in op een hogere waarde voor voorloopnullen.
- **Aangepaste positionering:** Gebruik `Margin` om het nummer van de rand te offsetten, of schakel `HorizontalAlignment` naar `Center` voor een voettekst‑stijl.

## Stap 4: Sla de gewijzigde PDF op

Tot slot schrijf je het bijgewerkte document naar schijf. Je kunt het origineel overschrijven of een gloednieuwe file maken.

```csharp
// Step 4 – Save the PDF with Bates numbers applied
var outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
```

Nadat deze regel is uitgevoerd, bevat `output.pdf` de originele inhoud plus een zichtbaar Bates‑label op elke pagina—precies wat je zou verwachten wanneer je **hoe Bates te genereren** voor een zaakbestand.

## Volledig, uitvoerbaar voorbeeld

Alles bij elkaar genomen, hier is het volledige snippet dat je kunt kopiëren‑plakken in een console‑applicatie:

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Open the source PDF
        var inputFile = @"C:\Docs\input.pdf";
        using var pdf = new Document(inputFile);

        // 2️⃣ Configure Bates numbering (add bates numbering pdf)
        var options = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 1000,
            NumberOfDigits = 6,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = FontRepository.FindFont("Arial")
        };

        // 3️⃣ Apply the numbering (how to add bates)
        pdf.AddBatesNumbering(options);

        // 4️⃣ Save the result (add sequential page numbers)
        var outputFile = @"C:\Docs\output.pdf";
        pdf.Save(outputFile);

        Console.WriteLine("Bates numbering applied successfully!");
    }
}
```

### Verwacht resultaat

Open `output.pdf` in een viewer (Adobe Reader, Edge, enz.). Je ziet elke pagina gestempeld met iets als **CASE-001000**, **CASE-001001**, … tot aan de laatste pagina. De nummers staan netjes rechtsonder, overeenkomstig de opties die we hebben ingesteld.

## Veelgestelde vragen & probleemoplossing

- **“Wat als mijn PDF met een wachtwoord beveiligd is?”**  
  Laad het met het wachtwoord: `new Document(inputFile, new LoadOptions { Password = "secret" })`.

- **“Kan ik Bates‑nummers toevoegen aan een nieuw aangemaakte PDF?”**  
  Zeker. Maak eerst het document (`var doc = new Document();`) en volg daarna Stap 2‑4 voordat je opslaat.

- **“Wordt het lettertype altijd ingebed?”**  
  Aspose embedt het lettertype automatisch als het nog niet in de PDF aanwezig is. Als je een specifiek lettertype‑familie nodig hebt, stel `options.Font` dienovereenkomstig in.

- **“Hoe zit het met de prestaties bij bestanden van 10.000 pagina’s?”**  
  De bibliotheek streamt pagina’s, waardoor het geheugenverbruik bescheiden blijft. Je kunt echter de `PdfSaveOptions.CompressionMode` verhogen voor snellere I/O.

## Pro‑tips voor productiegebruik

1. **Batchverwerking:** Plaats de bovenstaande logica in een lus die over een map met PDF’s itereren. Gebruik `Directory.GetFiles("*.pdf")` en verwerk elk bestand afzonderlijk.
2. **Logging:** Schrijf het eerste en laatste Bates‑nummer naar een log‑bestand—helpt auditors te verifiëren dat de nummering doorlopend was.
3. **Foutafhandeling:** Omring het hele blok met een `try/catch` en geef een duidelijke melding als de bron‑PDF ontbreekt of corrupt is.
4. **Zero‑padding flexibiliteit:** Als je een dynamisch aantal cijfers nodig hebt op basis van het totaal aantal pagina’s, bereken `NumberOfDigits = (pdf.Pages.Count + options.Start).ToString().Length`.

## Conclusie

We hebben zojuist laten zien hoe je **PDF-document maken C#** en naadloos **Bates‑nummering toevoegt**—van het initiële laden tot het uiteindelijke opslaan. Het korte voorbeeld demonstreert **hoe je Bates toevoegt**, **volgnummer pagina's toevoegt**, en **hoe je Bates genereert** met aangepaste prefixes en zero‑padding. Met een paar aanpassingen kun je dit patroon toepassen op batch‑taken, verschillende lay-outs, of zelfs integreren in een web‑API die op aanvraag een vers getallen PDF retourneert.

Klaar voor de volgende stap? Probeer dit te combineren met Aspose’s **watermark**‑functie, of genereer een samenvattende index die elk Bates‑nummer vermeldt naast een korte beschrijving van de paginainhoud. De mogelijkheden zijn eindeloos, en de code die je nu hebt is een solide basis voor elke document‑automatiseringsworkflow.

Veel plezier met coderen, en moge je PDF’s altijd perfect genummerd zijn!

![Schermafbeelding van een PDF-viewer die PDF-document maken C# met Bates-nummers toont](image-placeholder.png "PDF-document maken C# met Bates-nummers")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}