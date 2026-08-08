---
category: general
date: 2026-06-05
description: Maak een span‑element in een Word‑document met C#. Leer hoe je een span
  toevoegt, een absolute positie instelt en een aangepaste tag toevoegt in slechts
  een paar stappen.
draft: false
keywords:
- create span element
- how to add span
- set absolute position
- position text in word
- add custom tag
language: nl
og_description: Maak een span‑element in een Word‑bestand met C#. Deze tutorial laat
  zien hoe je een span toevoegt, een absolute positie instelt en efficiënt een aangepaste
  tag toevoegt.
og_title: Span‑element maken in Word met C# – Stap voor stap
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Create span element in a Word document using C#. Learn how to add span,
    set absolute position, and add custom tag in just a few steps.
  headline: Create Span Element in Word with C# – Complete Guide
  type: TechArticle
- questions:
  - answer: Word will clip the content, or it may push the span onto a new page. Always
      validate against page size (`doc.FirstSection.PageSetup.PageWidth`) and margins.
    question: What if the coordinates are outside the printable area?
  - answer: Yes—use `span.AddPicture("path/to/image.png")` before saving. The same
      absolute positioning rules apply.
    question: Can I add images to a span?
  - answer: Not directly. It behaves like an inline object, so you’ll see its text
      or image, but the tag itself stays hidden.
    question: Is the span visible in the Word UI?
  - answer: '`Document` implements `IDisposable`, so wrapping it in a `using` block
      is a good practice, especially for large files.'
    question: Do I need to dispose of the `Document` object?
  type: FAQPage
tags:
- C#
- Aspose.Words
- Word Automation
title: Span-element maken in Word met C# – Complete gids
url: /nl/net/programming-with-text/create-span-element-in-word-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak Span-element in Word met C# – Complete Gids

Heb je ooit een **span‑element** in een Word‑document moeten **maken**, maar wist je niet waar te beginnen? Je bent niet de enige—veel ontwikkelaars lopen tegen dit probleem aan wanneer ze voor het eerst programmatic Word‑manipulatie verkennen. In deze gids lopen we stap voor stap door **hoe je een span toevoegt**, deze precies positioneert en zelfs een aangepaste tag toevoegt, allemaal met nette C#‑code.

We gebruiken de Aspose.Words for .NET‑bibliotheek, die het werken met Word‑bestanden een fluitje van een cent maakt. Aan het einde van deze tutorial kun je **een absolute positie instellen** voor elk stuk tekst, de lay‑out controleren en de wijzigingen opslaan zonder de documentstructuur te breken.

## Wat je nodig hebt

- .NET 6.0 of later (de code compileert ook met .NET Core)  
- Aspose.Words for .NET (NuGet‑pakket `Aspose.Words`)  
- Een basisbegrip van C# (lussen, objecten, enz.)  
- Een invoer‑DOCX‑bestand om mee te experimenteren (we noemen het `input.docx`)

Dat is alles—geen extra tools, geen obscure afhankelijkheden. Klaar? Laten we duiken.

![Create span element positioned in Word document](image-placeholder.png)

*Alt‑tekst: span‑element gepositioneerd in Word‑document*

## Stap 1: Initialiseer het document en maak een Span-element

Het eerste wat je moet doen is het bron‑DOCX‑bestand laden en Aspose.Words vragen je een nieuw **span‑element** object te geven. Beschouw een span als een klein container‑object dat tekst, afbeeldingen of zelfs andere inline‑objecten kan bevatten.

```csharp
using Aspose.Words;
using Aspose.Words.Tagging;

class Program
{
    static void Main()
    {
        // Load the existing Word document
        Document doc = new Document("YOUR_DIRECTORY/input.docx");

        // Create a new span element – this is the core of our tutorial
        var span = doc.TaggedContent.CreateSpanElement();

        // We'll add the span to the document in the next step
    }
}
```

**Waarom dit belangrijk is:** `CreateSpanElement` is de enige manier om een getagde inline‑object te genereren dat Aspose.Words herkent als een *span*. Zonder deze methode zou je alleen ruwe tekst kunnen invoegen die niet absoluut gepositioneerd kan worden.

## Stap 2: Hoe Span toe te voegen aan de TaggedContent‑hiërarchie

Nu we een span hebben, moeten we **span toevoegen** aan de getagde‑content‑boom van het document. Het root‑element werkt als de bovenste map in een bestandssysteem—alles wat je eronder toevoegt, wordt onderdeel van de stroom.

```csharp
// Append the newly created span to the root of the TaggedContent hierarchy
doc.TaggedContent.RootElement.AppendChild(span);
```

Als je deze stap overslaat, bestaat de span alleen in het geheugen maar verschijnt nooit in het opgeslagen bestand. Het is een klassiek “aangemaakt maar niet gekoppeld”‑bug dat nieuwkomers vaak tegenkomt.

## Stap 3: Absolute positie instellen – Tekst precies positioneren in Word

Absolute positionering in Word gebruikt punten (1 pt = 1/72 in). Door `SetPosition(x, y)` aan te roepen, vertellen we Aspose.Words precies waar op de pagina de span moet komen, los van de gebruikelijke alinea‑stroom.

```csharp
// Set the X and Y coordinates in points (100 pt ≈ 1.39 in, 200 pt ≈ 2.78 in)
span.SetPosition(100, 200);
```

**Een snelle tip:** De coördinaten‑origin (0,0) begint in de linkerbovenhoek van het afdrukbare gebied, niet aan de fysieke paginarand. Als je rekening moet houden met marges, tel dan de marge‑grootte op bij de X/Y‑waarden.

## Stap 4: Voeg aangepaste tag toe – Verrijk de Span met metadata

Aangepaste tags laten je extra informatie opslaan die je later kunt opvragen of vervangen. Bijvoorbeeld, je kunt een span taggen als “AuthorSignature” zodat een later proces deze automatisch kan lokaliseren.

```csharp
// Attach a custom tag named "MyCustomTag" with a simple value
span.CustomTags.Add("MyCustomTag", "SampleValue");
```

**Wanneer te gebruiken:** Als je een templating‑engine bouwt, zijn aangepaste tags je geheime saus. Ze overleven opslagen en kunnen worden gelezen zonder de visuele inhoud te parseren.

## Stap 5: Sla het document op om de wijzigingen te behouden

Tot slot schrijf je het aangepaste document terug naar de schijf. De `Save`‑methode doet al het zware werk en zorgt ervoor dat de positie en tags van de span correct worden opgeslagen.

```csharp
// Save the modified document; this writes the span with its absolute position
doc.Save("YOUR_DIRECTORY/output.docx");
```

Open `output.docx` in Word, en je ziet de tekst (of elke inline‑inhoud die je later aan de span toevoegt) precies op de coördinaten die je hebt opgegeven. De aangepaste tag is onzichtbaar in de UI maar kan worden geïnspecteerd via de Aspose.Words‑API’s.

## Volledig werkend voorbeeld

Alles samengevoegd, hier is het volledige programma dat je kunt kopiëren‑plakken en uitvoeren:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Tagging;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source document
        Document doc = new Document("YOUR_DIRECTORY/input.docx");

        // 2️⃣ Create a new span element
        var span = doc.TaggedContent.CreateSpanElement();

        // 3️⃣ Append the span to the root hierarchy
        doc.TaggedContent.RootElement.AppendChild(span);

        // 4️⃣ Set absolute position (X = 100 pt, Y = 200 pt)
        span.SetPosition(100, 200);

        // 5️⃣ Add a custom tag for later identification
        span.CustomTags.Add("MyCustomTag", "SampleValue");

        // 6️⃣ Optionally, insert some text into the span
        span.Text = "Hello, positioned world!";

        // 7️⃣ Save the document
        doc.Save("YOUR_DIRECTORY/output.docx");

        Console.WriteLine("Span element created, positioned, and saved successfully.");
    }
}
```

**Verwacht resultaat:** Het openen van `output.docx` toont de zin *“Hello, positioned world!”* zwevend op de exacte plek die je hebt ingesteld, onafhankelijk van omliggende alinea’s. De aangepaste tag `MyCustomTag` is gekoppeld en kan later worden opgevraagd met `doc.TaggedContent.GetElementsByTag("MyCustomTag")`.

## Veelgestelde vragen & randgevallen

- **Wat gebeurt er als de coördinaten buiten het afdrukbare gebied liggen?**  
  Word zal de inhoud afsnijden, of de span naar een nieuwe pagina verplaatsen. Valideer altijd tegen de paginagrootte (`doc.FirstSection.PageSetup.PageWidth`) en marges.

- **Kan ik afbeeldingen aan een span toevoegen?**  
  Ja—gebruik `span.AddPicture("path/to/image.png")` vóór het opslaan. Dezelfde absolute positioneringsregels gelden.

- **Is de span zichtbaar in de Word‑UI?**  
  Niet direct. Hij gedraagt zich als een inline‑object, dus je ziet de tekst of afbeelding, maar de tag zelf blijft verborgen.

- **Moet ik het `Document`‑object zelf vrijgeven?**  
  `Document` implementeert `IDisposable`, dus het in een `using`‑blok plaatsen is een goede gewoonte, vooral bij grote bestanden.

## Pro Tips

- **Batch‑positionering:** Als je veel spans moet plaatsen, loop dan door een gegevensbron en bereken X/Y dynamisch.  
- **Coördinaten‑conversie:** Voor ontwerpers die in centimeters denken, vermenigvuldig centimeters met 28,35 om punten te krijgen.  
- **Versie‑veiligheid:** De code werkt met Aspose.Words 23.3 en later; oudere versies gebruiken mogelijk `CreateSpan` in plaats van `CreateSpanElement`.

## Conclusie

Je weet nu precies hoe je een **span‑element maakt**, **span toevoegt** aan een Word‑document, **absolute positie instelt**, en **een aangepaste tag toevoegt** met C#. Deze aanpak geeft je pixel‑perfecte controle over tekstplaatsing en opent de deur naar geavanceerde templating‑scenario’s.

Wat nu? Probeer de platte tekst te vervangen door een logo‑afbeelding, experimenteer met verschillende coördinaten, of bouw een kleine engine die alle spans met een specifieke tag tijdens runtime vervangt. De mogelijkheden zijn eindeloos zodra je de workflow rondom span‑elementen onder de knie hebt.

Veel plezier met coderen, en voel je vrij om een reactie achter te laten als iets niet helemaal duidelijk is!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Add Structure Element into Element in PDF using Java](/pdf/english/java/pdf-structure-elements/add-structure-element-into-element-in-pdf-using-java/)
- [How to Add Text to PDFs Using Aspose.PDF for Java: A Comprehensive Guide](/pdf/english/java/text-operations/aspose-pdf-java-add-text-to-pdf/)
- [How to Add Text Stamps to PDFs Using Aspose.PDF for Java](/pdf/english/java/watermarks-backgrounds/aspose-pdf-java-add-text-stamp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}