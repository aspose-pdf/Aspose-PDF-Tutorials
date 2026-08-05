---
category: general
date: 2026-08-04
description: Maak een nieuw PDF‑document in C# en voeg snel Bates‑nummering toe met
  Aspose.Pdf – leer hoe je een lege PDF‑pagina toevoegt en aangepaste paginanummers.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new pdf document
- add bates numbering pdf
- how to add bates
- add blank page pdf
- add custom page numbers
language: nl
lastmod: 2026-08-04
og_description: Maak een nieuw PDF‑document in C# en voeg automatisch Bates‑nummering
  toe aan de PDF voor juridisch casebeheer – volledig codevoorbeeld inbegrepen.
og_image_alt: Screenshot of a C# program creating a PDF document with Bates numbers
  applied
og_title: Maak een nieuw PDF‑document met Bates‑nummering in C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create new PDF document in C# and add Bates numbering pdf quickly using
    Aspose.Pdf – learn to add blank page pdf and custom page numbers.
  headline: Create new PDF document with Bates numbering in C#
  type: TechArticle
tags:
- C#
- PDF
- Aspose.Pdf
- Bates numbering
title: Maak een nieuw PDF‑document met Bates‑nummering in C#
url: /nl/net/document-creation/create-new-pdf-document-with-bates-numbering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak een nieuw PDF-document met Bates-nummering in C#

Als je een **nieuw PDF-document wilt maken** in C#, laat deze gids je zien hoe je **Bates-nummering aan een PDF toevoegt** met Aspose.Pdf. Je leert hoe je **een lege pagina aan een PDF toevoegt**, **aangepaste paginanummers configureert**, en het uiteindelijke bestand opslaat.

De tutorial behandelt elke stap, van het installeren van de bibliotheek tot het genereren van een PDF die voldoet aan de wettelijke dossiernormen. Aan het einde kun je een PDF genereren, een lege pagina invoegen, Bates-nummers toepassen en het nummerformaat aanpassen — allemaal met één enkel uitvoerbaar programma.

## Vereisten

* .NET 6.0 SDK of later geïnstalleerd  
* Visual Studio 2022 (of een andere C# IDE)  
* Een actieve Aspose.Pdf for .NET-licentie of een gratis evaluatiesleutel  

Je hebt geen extra NuGet-pakketten nodig; de tutorial installeert alles automatisch.

## Stap 1: Installeer Aspose.Pdf via NuGet

Open een terminal in je projectmap en voer uit:

```bash
dotnet add package Aspose.Pdf
```

Het commando voegt de nieuwste stabiele versie van Aspose.Pdf toe aan je project, die de `Document`, `BatesNumbering` en andere PDF‑manipulatieklassen levert die je zult gebruiken.

## Stap 2: Maak een nieuw PDF-document – initiële setup

Het maken van het PDF-bestand is de basis voor elke latere bewerking. De `Document`-klasse vertegenwoordigt de volledige PDF-container.

```csharp
using Aspose.Pdf;

// Step 2: Create a new PDF document
using var doc = new Document();
```

*Waarom dit belangrijk is*: Het instantieren van `Document` reserveert de interne structuren die nodig zijn voor pagina's, lettertypen en graphics. Het gebruik van `using var` zorgt ervoor dat het bestand correct wordt vrijgegeven na het opslaan.

## Stap 3: Voeg een lege pagina toe aan de PDF

Een PDF moet minstens één pagina bevatten voordat je er inhoud op kunt plaatsen. Het toevoegen van een lege pagina geeft je een schoon canvas voor Bates-nummers.

```csharp
// Step 3: Add a blank page to the document
Page page = doc.Pages.Add();
```

De `Pages.Add()`-methode voegt een nieuwe, lege pagina toe aan het einde van de paginacollectie van het document. Je kunt deze oproep herhalen om meer pagina's toe te voegen als je later **aangepaste paginanummers** over meerdere pagina's moet **toevoegen**.

## Stap 4: Configureer Bates-nummering – hoe Bates toe te voegen

Bates-nummering is een opeenvolgende identifier die vaak wordt gebruikt in juridische documenten. Je configureert het via de `BatesNumbering`-klasse.

```csharp
// Step 4: Set up Bates numbering options
var bates = new BatesNumbering
{
    StartNumber = 1000,      // Starting number for the sequence
    Prefix = "CaseA-",       // Text to prepend to each number
    Increment = 1,           // Increment between consecutive numbers
    // Optional: Set the location, font size, etc.
};
```

*Waarom dit belangrijk is*: `StartNumber` bepaalt het eerste nummer, `Prefix` voegt een leesbaar label toe, en `Increment` bepaalt de stapgrootte. Je kunt ook `HorizontalAlignment`, `VerticalAlignment`, `FontSize` en `Margins` aanpassen om het uiterlijk van het nummer op elke pagina te regelen.

## Stap 5: Pas de Bates-nummering toe op de pagina

Nu de nummeringsopties klaar zijn, kun je ze toepassen op de pagina (of op het hele document).

```csharp
// Step 5: Apply the Bates numbering to the page
bates.Apply(page);
```

Het aanroepen van `Apply` voegt het geformatteerde nummer standaard in de voettekst van de pagina in. Als je het nummer elders nodig hebt, stel dan `bates.Position` in voordat je `Apply` aanroept.

## Stap 6: Sla de PDF op met toegepaste Bates-nummers

Schrijf tenslotte het in‑memory document naar de schijf.

```csharp
// Step 6: Save the PDF with Bates numbers applied
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumbered.pdf");

doc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

Het opgeslagen bestand bevat nu één pagina met het Bates-nummer **CaseA-1000** onderaan weergegeven. Open de PDF in een viewer om de nummering te verifiëren.

## Verwachte output

Wanneer je `BatesNumbered.pdf` opent, zou je moeten zien:

* Een lege pagina (of meer als je extra pagina's hebt toegevoegd)  
* De tekst **CaseA-1000** onderaan de pagina geplaatst (standaardlocatie)  

Als je meer pagina's toevoegt en dezelfde `BatesNumbering`-instantie opnieuw gebruikt, zullen de nummers automatisch oplopen (CaseA-1001, CaseA-1002, …).

## Pro tip: Aangepaste paginanummers toevoegen naast Bates-nummers

Soms heb je zowel Bates-nummers als traditionele paginanummers nodig. Je kunt ze combineren door een `TextFragment` toe te voegen na het toepassen van Bates-nummering:

```csharp
// Add a traditional page number in the header
var pageNumber = new TextFragment($"Page {page.Number}")
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Top,
    FontSize = 12,
    Font = FontRepository.FindFont("Arial")
};
page.Paragraphs.Add(pageNumber);
```

Deze code laat zien hoe je **aangepaste paginanummers toevoegt** terwijl je het Bates-label behoudt.

## Randgeval: Bates-nummering toepassen op meerdere pagina's

Als je document meerdere pagina's bevat, kun je dezelfde `BatesNumbering`-instantie op elke pagina toepassen in een lus:

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    bates.Apply(doc.Pages[i]);
}
```

De lus zorgt ervoor dat elke pagina een opeenvolgend nummer krijgt op basis van de `StartNumber` en `Increment` die je hebt gedefinieerd.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| Nummers verschijnen niet gecentreerd | Standaarduitlijning komt mogelijk niet overeen met je lay-out | Stel `bates.HorizontalAlignment` en `bates.VerticalAlignment` expliciet in |
| Nummers overlappen bestaande inhoud | Er is geen marge gedefinieerd | Pas `bates.Margin` aan of gebruik `bates.Position` om het nummer te verplaatsen |
| Licentie‑exception tijdens uitvoering | Evaluatieversie beperkt de output | Pas een geldige Aspose.Pdf-licentie toe voordat je het document maakt (`License license = new License(); license.SetLicense("Aspose.Pdf.lic");`) |

## Volledig werkend voorbeeld

Hieronder staat een zelfstandige programma dat je kunt kopiëren, plakken en uitvoeren.

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1. Create a new PDF document
        using var doc = new Document();

        // 2. Add a blank page pdf
        Page page = doc.Pages.Add();

        // 3. Configure Bates numbering – how to add bates
        var bates = new BatesNumbering
        {
            StartNumber = 1000,
            Prefix = "CaseA-",
            Increment = 1,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(20, 20, 20, 20),
            FontSize =


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe paginanummers toe te voegen en aan te passen in PDF's met Aspose.PDF voor .NET | Document Manipulatie Gids](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF .NET: Pagina nummers toevoegen aan PDF's met FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [PDF-document maken met Aspose.PDF – Pagina, Vorm toevoegen & Opslaan](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}