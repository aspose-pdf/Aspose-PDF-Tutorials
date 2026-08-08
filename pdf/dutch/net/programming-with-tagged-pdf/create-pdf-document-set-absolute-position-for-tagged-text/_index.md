---
category: general
date: 2026-03-24
description: Maak een PDF-document en leer hoe je een absolute positie voor getagde
  tekst instelt. Deze tutorial laat zien hoe je een span‑element toevoegt, hoe je
  getagde inhoud toevoegt en tekst op de pagina positioneert.
draft: false
keywords:
- create pdf document
- set absolute position
- add span element
- how to add tagged
- position text on page
language: nl
og_description: Maak een PDF-document en zie direct hoe je een absolute positie instelt,
  een span-element toevoegt en tekst op de pagina positioneert met getagde PDF-inhoud.
og_title: PDF-document maken – Absolute positionering van getagde tekst
tags:
- Aspose.Pdf
- C#
- PDF Tagging
title: PDF-document maken – Absolute positie instellen voor getagde tekst
url: /nl/net/programming-with-tagged-pdf/create-pdf-document-set-absolute-position-for-tagged-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF‑document maken – Absolute positie instellen voor getagde tekst

Heb je ooit een **pdf document** moeten **maken** dat toegankelijke, getagde tekst bevat die precies op de gewenste plek staat? Misschien bouw je een formulier‑achtige PDF waarbij het label op een exacte coördinaat moet staan, of je genereert een certificaat en de naam moet perfect uitgelijnd zijn met een achtergrondafbeelding.  

In deze gids lopen we stap voor stap door een volledig, uitvoerbaar voorbeeld dat laat zien **hoe je getagde** inhoud toevoegt, **absolute positie** instelt en **een span‑element** toevoegt zodat je **tekst op de pagina** kunt **positioneren** zonder te gokken. Geen externe verwijzingen – alleen de code die je kunt copy‑pasten, plus uitleg over het “waarom” achter elke regel.

## Voorwaarden

- .NET 6+ (of .NET Framework 4.6+) met een C#‑compiler  
- Aspose.Pdf for .NET (nieuwste versie op het moment van schrijven, 23.12) geïnstalleerd via NuGet  
- Basiskennis van C#‑syntaxis  

Als je dat hebt, laten we beginnen.

---

## PDF‑document maken – Absolute positie instellen

Het eerste wat we doen is een lege `Document` instantieren. Dit object vertegenwoordigt het volledige PDF‑bestand en geeft ons toegang tot de getagde‑content‑boom.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();
```

**Waarom dit belangrijk is:**  
`Document` is de root van de PDF‑structuur. Door het eerst te maken zorgen we voor een canvas voor zowel visuele elementen (pagina’s, graphics) als de logische structuur (tags). De `using`‑statement zorgt ervoor dat het bestand correct wordt vrijgegeven, waardoor bestands‑handle‑lekken op Windows worden voorkomen.

---

## Getagde content inschakelen (Hoe getagde toevoegen)

Voordat we getagde elementen kunnen invoegen, moet het document gemarkeerd zijn als *getagd*. Aspose.Pdf maakt automatisch een `TaggedContent`‑object aan, maar je moet de vlag nog wel aanzetten.

```csharp
// Step 2: Mark the document as tagged (required for accessibility)
pdfDocument.TaggedContent = true;
```

**Wat er onder de motorkap gebeurt:**  
Het instellen van `TaggedContent` op `true` vertelt PDF‑readers dat het bestand een logische structuurboom bevat. Dit is cruciaal voor schermlezers en voor de `SetPosition`‑methode om correct te werken op een span‑element.

---

## Het root‑element van de getagde‑content‑boom ophalen

Het root‑element is het toegangspunt voor alle structurele tags (zoals `<Document>`, `<Section>`, `<Span>`). Beschouw het als het onzichtbare “body” van de PDF.

```csharp
// Step 3: Retrieve the root element of the tag tree
var rootElement = pdfDocument.TaggedContent.RootElement;
```

**Waarom we de root nodig hebben:**  
Alle volgende tags moeten ergens in de boom worden gekoppeld; anders verschijnen ze niet in de toegankelijkheids‑hiërarchie.

---

## Een span‑element toevoegen – Het bouwblok voor inline tekst

Een *span* is het PDF‑equivalent van een HTML‑`<span>`—perfect voor korte stukjes tekst die je precies wilt positioneren.

```csharp
// Step 4: Create a span element that will hold the text
var spanElement = rootElement.CreateSpanElement();
```

**Ontwerpsopmerking:**  
Als je rijkere opmaak nodig hebt (vet, cursief, hyperlinks), kun je de span in een `<Paragraph>` wikkelen of later `TextFragment`‑objecten gebruiken. Voor absolute positionering is een eenvoudige span het lichtste gewicht.

---

## Absolute positie instellen – X=100, Y=200

Nu het leuke deel: de span op een exacte locatie op de pagina plaatsen. Het coördinatensysteem begint in de linker‑onderhoek (0,0) en gebruikt punten (1 pt ≈ 1/72 in).

```csharp
// Step 5: Position the span at an absolute location (X=100, Y=200)
spanElement.SetPosition(100, 200);
```

**Waarom absolute positionering?**  
Wanneer je een pixel‑perfecte lay-out nodig hebt—denk aan certificaten, facturen of formulieren—volgt relatieve flow (zoals links‑naar‑rechts tekst) niet. `SetPosition` omzeilt de normale tekstflow en verankert het element op de opgegeven plek.

---

## Tekst aan de span toevoegen

Met de span gepositioneerd, injecteren we nu de eigenlijke tekenreeks.

```csharp
// Step 6: Add the desired text to the span
spanElement.AddText("Positioned tagged text");
```

**Tip:**  
Als je Unicode‑tekens of rechts‑naar‑links scripts nodig hebt, geef dan gewoon de string door; Aspose.Pdf handelt de codering automatisch af.

---

## De span aan het root‑element toevoegen

Tot slot koppelen we de span aan de logische boom van het document zodat deze onderdeel wordt van de uiteindelijke PDF.

```csharp
// Step 7: Append the span to the root so it becomes part of the PDF structure
rootElement.AppendChild(spanElement);
```

**Wat gebeurt er als je deze stap vergeet?**  
De span bestaat dan alleen in het geheugen maar wordt nooit geserialiseerd naar het bestand, waardoor je geen tekst ziet en de toegankelijkheidsboom onvolledig blijft.

---

## Volledig, uitvoerbaar voorbeeld

Hieronder staat het volledige programma dat je in een console‑app kunt plakken. Het maakt een één‑pagina PDF, voegt een getagde span toe op (100, 200) en slaat het bestand op als `TaggedPositioned.pdf`.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Enable tagging for accessibility
        pdfDocument.TaggedContent = true;

        // 3️⃣ Add a blank page (required for visual placement)
        var page = pdfDocument.Pages.Add();

        // 4️⃣ Get the root element of the tagged‑content tree
        var rootElement = pdfDocument.TaggedContent.RootElement;

        // 5️⃣ Create a span element that will hold the text
        var spanElement = rootElement.CreateSpanElement();

        // 6️⃣ Position the span at an absolute location on the page (X=100, Y=200)
        spanElement.SetPosition(100, 200);

        // 7️⃣ Add the desired text to the span
        spanElement.AddText("Positioned tagged text");

        // 8️⃣ Append the span to the root so it becomes part of the PDF structure
        rootElement.AppendChild(spanElement);

        // 9️⃣ Save the document
        pdfDocument.Save("TaggedPositioned.pdf");

        Console.WriteLine("PDF created successfully – check TaggedPositioned.pdf");
    }
}
```

**Verwachte output:**  
Open `TaggedPositioned.pdf` in een viewer (Adobe Acrobat, Foxit, etc.). Je ziet de zin **“Positioned tagged text”** precies 100 pt vanaf de linkerrand en 200 pt vanaf de onderkant van de pagina. Als je het *Tags*‑paneel inspecteert, zie je een `<Span>`‑element onder de root van het document, wat bevestigt dat de inhoud correct getagd is.

---

## Veelgestelde vragen & randgevallen

### Wat als ik tekst op een specifieke pagina anders dan de eerste moet positioneren?

Voeg de gewenste pagina toe (`var page = pdfDocument.Pages[3];`) voordat je `SetPosition` aanroept. De span wordt automatisch gekoppeld aan de actieve paginacontext.

### Kan ik de positie in inches of centimeters instellen?

`SetPosition` accepteert punten. Converteer met de formules:  
- **Inches → points:** `points = inches * 72`  
- **Centimeters → points:** `points = cm * 28.3465`

### Hoe wijzig ik het lettertype of de kleur van de span?

Nadat je de span hebt aangemaakt, kun je de `TextState` ophalen en aanpassen:

```csharp
var textState = spanElement.TextState;
textState.Font = FontRepository.FindFont("Arial");
textState.FontSize = 12;
textState.ForegroundColor = Color.GetBlack();
```

### Wat als het document al bestaande tags heeft?

Je kunt nog steeds een nieuwe span maken en deze toevoegen aan elk bestaand element (`rootElement`, een specifieke `<Section>`, etc.). Zorg er alleen voor dat je een logische hiërarchie behoudt—schermlezers verwachten een goed gestructureerde boom.

### Werkt dit met PDF/A of PDF/UA compliance?

Ja. Getagde PDF’s zijn een kernvereiste voor PDF/UA. Als je PDF/A nodig hebt, roep dan `pdfDocument.Convert(new PdfAConversionOptions(PdfAStandard.PdfA_1b));` aan na het opbouwen van de inhoud.

---

## Pro‑tips & valkuilen

- **Pro tip:** Voeg altijd een pagina toe vóór je inhoud positioneert. Zonder pagina faalt `SetPosition` stilletjes omdat er nergens gerenderd kan worden.
- **Let op eenheden:** Het mixen van pixels uit een UI‑ontwerp met PDF‑punten verplaatst je tekst verkeerd. Controleer je conversie dubbel.
- **Performance‑hint:** Als je duizenden PDF’s genereert, hergebruik dan één `Document`‑instantie en roep `pdfDocument.Pages.Clear()` aan tussen runs om overmatig geheugenverbruik te voorkomen.
- **Toegankelijkheids‑herinnering:** Taggen is niet alleen een extraatje; veel regelgeving (Section 508, EN 301 549) vereist het. Het gebruik van `CreateSpanElement` zorgt ervoor dat de tekst vindbaar is voor assistieve technologieën.

---

## Conclusie

We hebben zojuist een **pdf document** vanaf nul **gemaakt**, **absolute positie** ingesteld, een **span‑element** toegevoegd en laten zien **hoe je getagde** inhoud kunt **toevoegen** zodat je **tekst op de pagina** kunt **positioneren** met pixel‑perfecte nauwkeurigheid. Het volledige voorbeeld staat klaar om te draaien, en de uitleg behandelt zowel het *hoe* als het *waarom*—precies wat ontwikkelaars (en AI‑assistenten) zoeken wanneer ze een betrouwbare oplossing nodig hebben.

Vervolgens kun je verkennen:

- Afbeeldingen achter de gepositioneerde tekst toevoegen voor watermerken op certificaten.  
- `CreateParagraphElement` gebruiken voor meer‑regelige blokken die toch absolute plaatsing nodig hebben.  
- Exporteren naar PDF/UA om te voldoen aan strenge toegankelijkheidsaudits.  

Voel je vrij om de coördinaten, lettertypen of kleuren aan te passen—experimenteren is de snelste manier om meester te worden in getagde PDF‑generatie. Als je ergens vastloopt, laat dan een reactie achter; happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}