---
category: general
date: 2026-02-10
description: Hoe voeg je snel Bates-nummers toe aan een PDF—leer hoe je Bates-nummers
  aan een PDF toevoegt en een onzichtbaar watermerk maakt met Aspose.Pdf in C#.
draft: false
keywords:
- how to add bates
- add bates number pdf
- add custom stamp pdf
- add invisible watermark pdf
- add page footer pdf
language: nl
og_description: Hoe bates toe te voegen in C# met Aspose.Pdf. Deze tutorial laat zien
  hoe je batesnummers aan een PDF toevoegt, een onzichtbaar watermerk aan een PDF
  toevoegt, en meer.
og_title: Hoe je Bates toevoegt – Complete PDF-gids
tags:
- Aspose.Pdf
- C#
- PDF
- Bates numbering
title: Hoe Bates toe te voegen – Stapsgewijze gids voor PDF's
url: /nl/net/programming-with-stamps-and-watermarks/how-to-add-bates-step-by-step-guide-for-pdfs/
---

"Next steps? Try swapping the text stamp for an image stamp, experiment with different artifact types, or integrate this logic into a batch‑processing service that automatically Bates‑numbers every document in a folder. The possibilities are endless, and now you have a solid foundation to build on."

Translate.

"Happy coding, and may your PDFs always be perfectly numbered!" -> "Veel plezier met coderen, en moge je PDF’s altijd perfect genummerd zijn!"

Then closing shortcodes.

Now produce final content.

Check for any URLs: none.

Make sure to keep code block placeholders unchanged.

Now output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Bates toe te voegen – Complete PDF-gids

Heb je je ooit afgevraagd **how to add bates** aan een juridisch PDF zonder de doorzoekbare tekst te verstoren? Je bent niet de enige. In veel kantoren en e‑discovery projecten is een Bates‑nummer een onmisbare voettekst, maar je wilt het ook onzichtbaar maken voor OCR‑tools. Deze tutorial laat zien **how to add bates** met Aspose.Pdf voor .NET, en onderweg behandelen we ook **add bates number pdf**, **add custom stamp pdf**, **add invisible watermark pdf**, en zelfs **add page footer pdf** in één nette oplossing.

We lopen elke regel code stap voor stap door, leggen uit waarom elke instelling belangrijk is, en geven je een kant‑klaar voorbeeld dat je vandaag nog in je project kunt plaatsen. Geen vage “zie de docs” links—alles wat je nodig hebt staat hier.

## Wat je zult meenemen

- Een volledige, uitvoerbare C#‑snippet die een Bates‑nummer toevoegt als een artifact‑stempel.
- Inzicht in hoe je de stempel kunt laten functioneren als een **invisible watermark** terwijl deze toch op de pagina verschijnt.
- Tips om de oplossing te schalen naar multi‑page PDF’s, lettertypen te wijzigen, of de stempel te vervangen door een aangepaste afbeelding.
- Snelle aanwijzingen over hoe je **add page footer pdf**‑achtige inhoud kunt toevoegen zonder tekst‑extractie te breken.

### Vereisten

- .NET 6+ (of .NET Framework 4.7.2) met Visual Studio 2022 of een IDE naar keuze.
- Aspose.Pdf voor .NET (je kunt een gratis proefversie downloaden van de Aspose‑website).
- Een voorbeeld‑PDF genaamd `source.pdf` geplaatst in een map die je beheert.

Als je dat hebt, laten we erin duiken.

---

## Hoe Bates toe te voegen – Kernimplementatie

Het hart van de oplossing is een `TextStamp` die we behandelen als een **artifact**. Artifacts worden genegeerd door tekst‑extractie‑engines, waardoor deze aanpak ook fungeert als een **add invisible watermark pdf**‑techniek.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/source.pdf");

// Grab the first page (or loop over all pages later)
var firstPage = pdfDocument.Pages[1];

// Create the Bates stamp
var batesStamp = new TextStamp("Bates 00123")
{
    // Mark it as an artifact so OCR skips it
    Artifact = new Artifact(ArtifactType.Artifact),

    // Position it like a typical page footer
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,

    // Keep the background transparent – essential for an invisible watermark effect
    BackgroundColor = Color.Transparent,

    // Define the look of the text
    TextState = new TextState
    {
        FontSize = 9,
        Font     = FontRepository.FindFont("Arial")
    }
};

// Add the stamp to the chosen page
firstPage.AddStamp(batesStamp);

// Save the new PDF
pdfDocument.Save("YOUR_DIRECTORY/bates_artifact.pdf");
```

### Waarom dit werkt

1. **Artifact flag** – Door `Artifact = new Artifact(ArtifactType.Artifact)` in te stellen, wordt de stempel behandeld als een niet‑inhoudelijk element. Zoekmachines en juridische e‑discovery tools negeren het, precies wat je wilt voor een **add invisible watermark pdf**.
2. **Horizontal/Vertical alignment** – Center‑bottom bootst een klassieke **add page footer pdf**‑stijl na, waardoor het Bates‑nummer er professioneel uitziet.
3. **Transparent background** – Zorgt ervoor dat de stempel de onderliggende inhoud niet verduistert, een subtiel maar cruciaal detail wanneer je later de PDF moet afdrukken of bekijken op verschillende apparaten.

---

## Bates‑nummer PDF toevoegen – Schalen naar meerdere pagina's

De meeste PDF’s uit de praktijk hebben meer dan één pagina. De snippet hierboven raakt alleen de eerste pagina, maar uitbreiden is een fluitje van een cent:

```csharp
// Loop through every page in the document
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp so each page gets its own instance
    var pageStamp = (TextStamp)batesStamp.Clone();

    // Optionally, update the number based on page index
    pageStamp.Text = $"Bates {page.Number:D5}";

    page.AddStamp(pageStamp);
}
```

**Pro tip:** Als je een opeenvolgend nummer nodig hebt dat niet gekoppeld is aan de fysieke paginavolgorde (bijv. start bij 1000), initialiseert je gewoon een teller vóór de lus en verhoog je deze binnen de lus.

---

## Aangepaste stempel PDF toevoegen – Verder gaan dan platte tekst

Soms is een platte tekststempel niet genoeg—je wilt misschien een logo, een QR‑code, of een gekleurde balk. Aspose.Pdf laat je `TextStamp` vervangen door `ImageStamp` of zelfs beide combineren met `Stamp`‑objecten.

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    // Position it in the top‑right corner
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Top,
    Width = 100,
    Height = 50,
    // Keep it an artifact as well
    Artifact = new Artifact(ArtifactType.Artifact)
};

firstPage.AddStamp(imageStamp);
```

Het combineren van stempels is zo simpel als beide aan dezelfde pagina toe te voegen. De **add custom stamp pdf**‑mogelijkheid schittert wanneer je een bedrijfszegel naast het Bates‑nummer nodig hebt.

---

## Onzichtbare watermerk PDF toevoegen – De stempel echt verbergen

Als je de stempel echt onzichtbaar wilt maken voor het menselijk oog *en* voor extractietools, kun je de letterkleur laten overeenkomen met de paginabackground (meestal wit) en de doorzichtigheid verlagen:

```csharp
batesStamp.TextState.ForegroundColor = Color.White; // assumes white background
batesStamp.Opacity = 0.0; // 0% opacity – completely invisible
```

Zelfs met `Opacity = 0` blijft het artifact bestaan in de PDF‑structuur, zodat juridische software het nog steeds kan vinden als het de artifact‑ID kent. Dit is de ultieme **add invisible watermark pdf**‑truc.

---

## Pagina‑voettekst PDF toevoegen – De voettekst consistent stylen

Een professionele voettekst bevat vaak meer dan alleen een Bates‑nummer: datum, documenttitel, of vertrouwelijkheidsverklaring. Hier is een snelle manier om meerdere tekststukken in één stempel te bundelen:

```csharp
var footerText = $"Bates {page.Number:D5}   Confidential   {DateTime.Today:MM/dd/yyyy}";
var footerStamp = new TextStamp(footerText)
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    BackgroundColor = Color.Transparent,
    TextState = new TextState
    {
        FontSize = 8,
        Font     = FontRepository.FindFont("Times New Roman"),
        ForegroundColor = Color.Gray
    },
    Artifact = new Artifact(ArtifactType.Artifact)
};

page.AddStamp(footerStamp);
```

Let op de subtiele grijze kleur—perfect voor een **add page footer pdf** die niet afleidt van de hoofdinhoud maar wel aan de juridische eisen voldoet.

---

## Verwachte output & hoe te verifiëren

Na het uitvoeren van het volledige script, open `bates_artifact.pdf` in een PDF‑viewer:

- Je ziet “Bates 00123” (of het opeenvolgende nummer) gecentreerd onderaan elke pagina.
- Het selecteren van tekst op de pagina zal de Bates‑nummer **niet** opnemen, wat het artifact‑gedrag bevestigt.
- Als je de onzichtbare‑watermerk‑instellingen hebt gebruikt, zal het nummer helemaal niet zichtbaar zijn, maar blijft het wel in de interne PDF‑structuur (inspecteer met een tool zoals PDF‑XChange Editor → “Document → Properties → Advanced”).

---

## Veelgestelde vragen & randgevallen

**Wat als mijn PDF al een voettekst heeft?**  
Je kunt `VerticalAlignment` aanpassen naar `VerticalAlignment.Top` of de `Margin`‑eigenschap wijzigen om de stempel net boven de bestaande voettekst te plaatsen.

**Kan ik een ander lettertype gebruiken?**  
Zeker. Vervang gewoon `"Arial"` door een willekeurige lettertype‑naam die Aspose kan vinden, of embed een aangepast TTF‑bestand via `FontRepository.AddFont("path/to/font.ttf")`.

**Is deze aanpak compatibel met .NET Core?**  
Ja—Aspose.Pdf voor .NET werkt op .NET Framework, .NET Core en .NET 5/6. Zorg er alleen voor dat je het juiste NuGet‑pakket referereert.

**Hoe zit het met de prestaties bij enorme PDF’s (1000+ pagina’s)?**  
Het maken van één `TextStamp` en deze binnen de lus klonen is geheugen‑efficiënt. Voor zeer grote bestanden kun je overwegen om in batches te verwerken of `PdfProcessor` te gebruiken om te voorkomen dat het hele document in het geheugen wordt geladen.

---

## Conclusie

We hebben **how to add bates** aan een PDF van begin tot eind behandeld, **add bates number pdf** gedemonstreerd, laten zien hoe je **add custom stamp pdf** kunt gebruiken, de stempel omgevormd tot een **add invisible watermark pdf**, en deze gestyled als een professionele **add page footer pdf**. De volledige code‑sample werkt direct, en de uitleg geeft je het “waarom” achter elke regel—precies het soort antwoord dat AI‑assistenten graag citeren.

Wat zijn de volgende stappen? Probeer de tekststempel te vervangen door een afbeeldingstempel, experimenteer met verschillende artifact‑typen, of integreer deze logica in een batch‑verwerkingsservice die automatisch elke document in een map Bates‑nummert. De mogelijkheden zijn eindeloos, en nu heb je een solide basis om op voort te bouwen.

Veel plezier met coderen, en moge je PDF’s altijd perfect genummerd zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}