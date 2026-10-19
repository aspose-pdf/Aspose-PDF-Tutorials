---
category: general
date: 2026-03-27
description: Maak een span‑element in C# en leer hoe je een span aan een pagina kunt
  toevoegen tijdens het converteren van DOCX naar PDF en het opslaan als PDF. Stapsgewijze
  gids voor ontwikkelaars.
draft: false
keywords:
- create span element
- how to add span
- convert docx to pdf
- add element to page
- save as pdf
language: nl
og_description: Maak een span‑element in C# en leer hoe je een span aan een pagina
  toevoegt tijdens het converteren van DOCX naar PDF, en sla vervolgens op als PDF.
  Volledig codevoorbeeld inbegrepen.
og_title: Maak een span‑element en voeg het toe aan de pagina – Converteer DOCX naar
  PDF
tags:
- C#
- DocumentProcessing
- PDFConversion
title: Maak span‑element en voeg toe aan pagina – Converteer DOCX naar PDF
url: /nl/net/document-conversion/create-span-element-and-add-to-page-convert-docx-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Span‑element maken en toevoegen aan pagina – DOCX naar PDF converteren

Maak **span‑element** in een DOCX‑bestand is een veelvoorkomende taak wanneer je precieze lay‑outcontrole nodig hebt. In deze tutorial laten we je zien **hoe je een span toevoegt** aan een pagina, **DOCX naar PDF converteert**, en **opslaat als PDF**—alles in een paar nette stappen.  

Als je ooit naar een Word‑document hebt gekeken en dacht: “Ik wou dat ik een klein tekstvak op een exacte coördinaat kon plaatsen,” dan ben je hier op het juiste adres. We lopen de volledige workflow door, van het laden van het bronbestand tot het verkrijgen van een gepolijste PDF‑output.

## Wat je gaat bereiken

Aan het einde van deze gids kun je:

* Een `.docx`‑bestand laden met de `Document`‑klasse van de documentbibliotheek.  
* **Span‑element maken** met de `TaggedContent`‑API.  
* Dat span‑element positioneren op exacte X/Y‑coördinaten op een gekozen pagina.  
* **Element aan pagina toevoegen** betrouwbaar, zelfs wanneer de pagina niet de eerste is.  
* **DOCX naar PDF converteren** en **opslaan als PDF** met één enkele `Save`‑aanroep.

Geen externe tools, geen mysterieuze instellingen—alleen platte C#‑code die je kunt copy‑paste in je project.

## Vereisten

* .NET 6+ (of elke recente .NET‑runtime die jouw bibliotheek ondersteunt).  
* Het document‑verwerkings‑SDK dat `Document`, `TaggedContent`, `Position`, enz. levert.  
* Een basisbegrip van C#‑syntaxis—als je een `Console.WriteLine` kunt schrijven, ben je klaar.

> **Pro tip:** Houd je SDK‑versie up‑to‑date; de nieuwste release (v3.2 vanaf maart 2026) bevat prestatie‑verbeteringen voor pagina‑niveau bewerkingen.

---

![Diagram dat laat zien hoe je een span‑element maakt en op een PDF‑pagina plaatst](https://example.com/images/create-span-element.png "Diagram van span‑element plaatsing")

## Span‑element maken – Positioneren en toevoegen aan pagina

Hieronder staat de volledige, uitvoerbare code die alles doet, van het laden van de bron‑DOCX tot het schrijven van de uiteindelijke PDF. Voel je vrij om het in een console‑app te plakken, de paden aan te passen en uit te voeren.

```csharp
using DocumentProcessing;   // Replace with the actual namespace of your SDK
using DocumentProcessing.Models;

class Program
{
    static void Main()
    {
        // Step 1: Load the DOCX you want to modify
        // -------------------------------------------------
        // The constructor takes a file path; make sure the file exists.
        Document doc = new Document(@"C:\Docs\input.docx");

        // Step 2: Create a new span element using the TaggedContent API
        // -------------------------------------------------
        // A span is a lightweight container for inline content.
        var span = doc.TaggedContent.CreateSpanElement();
        // Optional: add some text inside the span
        span.Text = "Hello, world!";

        // Step 3: Position the span at the desired coordinates (X = 50, Y = 750)
        // -------------------------------------------------
        // Position uses points (1/72 inch). Adjust as needed.
        span.Position = new Position(50, 750);

        // Step 4: Add the span to the target page (page index 1 = second page)
        // -------------------------------------------------
        // Pages are zero‑based; index 1 means the second page in the document.
        doc.Pages[1].Add(span);

        // Step 5: Convert the modified DOCX to PDF and save the result
        // -------------------------------------------------
        // The Save method automatically detects the output format from the extension.
        doc.Save(@"C:\Docs\output.pdf");

        // Confirmation output
        Console.WriteLine("Span added, document converted, and PDF saved successfully.");
    }
}
```

### Stap‑voor‑stap uitleg

#### Stap 1 – Laad het DOCX‑document  
We instantieren een `Document`‑object dat wijst naar `input.docx`. Dit object vertegenwoordigt het volledige Word‑bestand in het geheugen en geeft ons toegang tot pagina’s, inhoud en metadata.  

#### Stap 2 – Maak een span‑element  
De aanroep `TaggedContent.CreateSpanElement()` retourneert een lichtgewicht inline‑container. Beschouw het als een klein, onzichtbaar vakje dat tekst, afbeeldingen of andere inline‑elementen kan bevatten. Het toevoegen van tekst (`span.Text`) is optioneel maar handig voor debugging.

#### Stap 3 – Positioneer het span‑element  
`new Position(50, 750)` zet de linkerbovenhoek van het span‑element 50 pt vanaf de linkermarge en 750 pt vanaf de bovenkant van de pagina. Deze waarden zijn absoluut, zodat je het span‑element overal kunt plaatsen—perfect voor precieze lay‑outs.

#### Stap 4 – Voeg het span‑element toe aan de doelpagina  
`doc.Pages[1].Add(span)` injecteert het span‑element in de tweede pagina. De API gebruikt nul‑gebaseerde indexering, dus pagina 0 is de eerste pagina. Als je het op de eerste pagina wilt toevoegen, gebruik dan simpelweg `doc.Pages[0]`.

#### Stap 5 – Converteer DOCX naar PDF en sla op als PDF  
Het aanroepen van `doc.Save("output.pdf")` doet twee dingen: het schrijft het gewijzigde document naar schijf **en** converteert de inhoud naar PDF vanwege de `.pdf`‑extensie. Geen extra conversiestap nodig—dit is de makkelijkste manier om **op te slaan als PDF**.

---

## Hoe span‑element op een andere pagina toe te voegen (geavanceerd)

Soms ken je de paginanaam niet van tevoren. Je kunt een pagina vinden op basis van zijn nummer (mensvriendelijk) of door te zoeken naar een specifiek trefwoord.

```csharp
// Find the page that contains the word "Summary"
int targetIndex = doc.Pages
    .Select((p, i) => new { Page = p, Index = i })
    .FirstOrDefault(x => x.Page.Text.Contains("Summary"))?.Index ?? 0;

// Fallback to first page if not found
targetIndex = Math.Max(targetIndex, 0);

// Add the span to the discovered page
doc.Pages[targetIndex].Add(span);
```

**Waarom dit belangrijk is:** In rapporten waarbij het aantal pagina’s varieert, kan een hard‑gecodeerde `Pages[1]` de lay‑out breken. Deze snippet toont een robuust patroon voor **hoe je span‑element dynamisch toevoegt**.

---

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Probleem | Wat gebeurt er | Oplossing |
|----------|----------------|-----------|
| **Span niet zichtbaar** | Coördinaten liggen buiten de pagina of het span‑element heeft geen breedte/hoogte. | Controleer de `Position`‑waarden; gebruik een liniaal in je PDF‑viewer. |
| **Verkeerde paginanaam** | Je voegt toe aan pagina 0 maar verwacht het op pagina 2. | Onthoud dat de API nul‑gebaseerd is; tel 1 op bij het mens‑vriendelijke paginanummer. |
| **Opslaan overschrijft bron** | `doc.Save("input.docx")` vervangt het originele bestand. | Sla altijd op naar een nieuw pad (`output.pdf`) bij het converteren. |
| **Ontbrekende SDK‑referentie** | Compileerfout op `Document`‑klasse. | Installeer het NuGet‑pakket: `dotnet add package DocumentProcessing.SDK`. |

---

## Het resultaat verifiëren

Na het uitvoeren van het programma, open `output.pdf` in een PDF‑viewer. Je zou de tekst “Hello, world!” exact op (50, 750) op de tweede pagina moeten zien. Als de tekst elders verschijnt, pas dan de `Position`‑waarden aan en voer opnieuw uit.  

Voor geautomatiseerde tests kun je een PDF‑parser (bijv. iTextSharp) gebruiken om de coördinaten van de tekst programmatisch te controleren.

```csharp
// Example using iTextSharp to verify position (pseudo‑code)
var pdfReader = new PdfReader(@"C:\Docs\output.pdf");
var page = pdfReader.GetPageContent(2);
Debug.Assert(page.Contains("Hello, world!"));
```

---

## Volgende stappen

* **Stijl het span‑element** – verken `span.Font`, `span.Color` en andere stijl‑eigenschappen.  
* **Afbeeldingen toevoegen** – gebruik `CreateImageElement()` in plaats van een span voor grafische elementen.  
* **Batch‑verwerking** – doorloop een map met DOCX‑bestanden

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}