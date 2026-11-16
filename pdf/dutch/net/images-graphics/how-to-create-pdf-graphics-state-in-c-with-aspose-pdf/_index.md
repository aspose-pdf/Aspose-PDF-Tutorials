---
category: general
date: 2026-11-16
description: Leer hoe je een PDF‑grafische toestand maakt in C# met Aspose.Pdf. Deze
  gids behandelt doorzichtigheid, mengmodus en een volledig codevoorbeeld.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf graphics state
- Aspose.Pdf ExtGState
- PDF opacity
- C# PDF manipulation
- PDF blend mode
- Aspose.Pdf graphics state
language: nl
lastmod: 2026-11-16
og_description: Maak een PDF‑grafische toestand in C# met Aspose.Pdf. Volg deze volledige
  tutorial om de doorzichtigheid en mengmodus programmatisch in te stellen.
og_image_alt: Illustration of how to create PDF graphics state with Aspose.Pdf in
  C#
og_title: PDF-grafische toestand maken in C# – stapsgewijze Aspose.Pdf-gids
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to create PDF graphics state in C# using Aspose.Pdf. This
    guide covers opacity, blend mode, and full code example.
  headline: How to create PDF graphics state in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF
title: Hoe maak je een PDF‑grafische toestand in C# met Aspose.Pdf
url: /nl/net/images-graphics/how-to-create-pdf-graphics-state-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe PDF graphics state te maken in C# met Aspose.Pdf

Als je **PDF graphics state** moet maken in een .NET‑project, laat deze tutorial je precies zien hoe je dat doet met Aspose.Pdf. Of je nu de opacity wilt regelen, de blend‑mode wilt wijzigen, of een aangepaste graphics state wilt hergebruiken over pagina’s, de onderstaande stappen bieden een complete, kant‑klaar oplossing.

In deze gids leer je hoe je toegang krijgt tot de paginabronnen, een **ExtGState**‑item toevoegt en de wijzigingen opslaat in een nieuw bestand. Het voorbeeld werkt met Aspose.Pdf 23.12 (of later) en richt zich op .NET 6+, maar de concepten gelden ook voor eerdere versies.

## Voorvereisten

Voordat je begint, zorg dat je het volgende hebt:

* Visual Studio 2022 (of een andere C#‑IDE) met .NET 6 SDK geïnstalleerd.  
* Een Aspose.Pdf for .NET‑licentie of een tijdelijke evaluatiesleutel.  
* Een PDF‑bestand genaamd `input.pdf` geplaatst in een map die je vanuit code kunt refereren.  

Er zijn geen extra NuGet‑pakketten nodig naast `Aspose.Pdf`.

## Wat de tutorial behandelt

* Het laden van een bestaand PDF‑document.  
* Navigeren naar de resources‑dictionary van de eerste pagina.  
* Een nieuwe graphics‑state‑dictionary maken die stroke‑opacity (`CA`), fill‑opacity (`ca`) en blend‑mode (`BM`) definieert.  
* Het toevoegen van de nieuwe graphics state aan de **ExtGState**‑collectie met een aangepaste naam (`GS0`).  
* Het opslaan van de bijgewerkte PDF zodat latere teken‑opdrachten kunnen verwijzen naar de nieuwe state.

Aan het einde van de tutorial kun je **PDF graphics state**‑objecten programmatically maken en ze hergebruiken in elke tekenbewerking.

## Stap 1: Het project instellen en namespaces importeren

Maak een nieuwe console‑applicatie (of integreer de code in een bestaand project). Voeg de Aspose.Pdf‑referentie toe en include de benodigde namespaces:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Generator;
```

> **Pro tip:** Als je de gratis evaluatieversie gebruikt, voeg dan `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` toe vóór het laden van het document om watermerk‑meldingen te voorkomen.

## Stap 2: Het PDF‑document laden

Het openen van het bestand is eenvoudig. De `Document`‑klasse vertegenwoordigt de volledige PDF en geeft je toegang tot de pagina’s en resources.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";

using (var document = new Document(inputPath))
{
    // All subsequent steps run inside this using block
```

Het plaatsen van de code binnen een `using`‑block garandeert dat de bestands‑handle wordt vrijgegeven na de bewerking, wat essentieel is voor **C# PDF-manipulatie** in productie‑services.

## Stap 3: De resources‑dictionary van de eerste pagina ophalen

Elke PDF‑pagina heeft een *Resources*‑dictionary die fonts, afbeeldingen en graphics‑states opslaat. We hebben een `DictionaryEditor` nodig om die structuur te bewerken.

```csharp
    // Step 3: Get the first page and its resources dictionary
    var page = document.Pages[1];
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

Als de PDF al een `ExtGState`‑item bevat, zal `resourcesEditor["ExtGState"]` dat teruggeven; anders maakt Aspose.Pdf automatisch een lege dictionary voor ons aan wanneer we het eerste item toevoegen.

## Stap 4: De ExtGState‑dictionary openen of aanmaken

De **ExtGState**‑dictionary bevat benoemde graphics‑state‑objecten. We halen er een bestaande op of maken een nieuwe container.

```csharp
    // Step 4: Access (or create) the ExtGState dictionary within the resources
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

Wanneer `ExtGState` niet bestaat, retourneert `resourcesEditor["ExtGState"]` automatisch een nieuwe lege dictionary, zodat de code voor elke PDF werkt.

## Stap 5: De nieuwe graphics‑state‑dictionary bouwen

Een graphics state is een `CosPdfDictionary` met specifieke sleutels:

* `CA` – stroke opacity (0‑1)  
* `ca` – fill opacity (0‑1)  
* `BM` – blend mode (`Normal`, `Multiply`, etc.)

We maken een lege dictionary, vullen die, en voegen hem vervolgens toe aan `ExtGState`.

```csharp
    // Step 5: Create a new graphics state dictionary with desired parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (50% transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };

    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

Je kunt `0.5` vervangen door elke waarde tussen `0` en `1` om de fill‑opacity aan te passen, of `"Normal"` vervangen door `"Multiply"` voor een andere **PDF blend mode**. Deze flexibiliteit maakt het creëren van een aangepaste graphics state tot een krachtige techniek bij **Aspose.Pdf graphics state**‑beheer.

## Stap 6: De graphics‑state registreren met een naam

PDF‑content‑streams verwijzen naar graphics‑states via een naam. Hier gebruiken we `GS0`, maar elke unieke naam werkt.

```csharp
    // Step 6: Add the new graphics state to the ExtGState dictionary with a name (e.g., GS0)
    extGState.Add("GS0", newGraphicsState);
```

Als je meerdere states nodig hebt, herhaal dan de creatiestap met andere parameters en voeg ze toe als `GS1`, `GS2`, enz. Dit patroon schaalt goed voor complexe documenten die verschillende opacity‑ of blend‑instellingen op verschillende lagen vereisen.

## Stap 7: De aangepaste PDF opslaan

Schrijf tenslotte het bijgewerkte document naar een nieuw bestand. Het origineel intact houden maakt debuggen makkelijker.

```csharp
    // Step 7: Save the updated PDF document
    string outputPath = @"YOUR_DIRECTORY\output.pdf";
    document.Save(outputPath);
}
```

Na uitvoering bevat `output.pdf` een `ExtGState`‑item met de naam `GS0`. Elke latere teken‑operator kan hiernaar verwijzen met de `gs`‑operator (bijv. `GS0 gs` in een content‑stream).  

> **Waarom dit belangrijk is:** Door een herbruikbare graphics state te maken, vermijd je het herhalen van opacity‑ en blend‑instellingen voor elke teken‑opdracht, wat zowel de prestaties als het onderhoud verbetert.

## De nieuwe graphics‑state gebruiken in een content‑stream (optioneel)

Wil je het effect meteen zien, voeg dan een eenvoudige rechthoek toe die de zojuist gemaakte state gebruikt:

```csharp
using (var document = new Document(outputPath))
{
    var page = document.Pages[1];
    var content = page.Contents[1]; // Get the first content stream

    // Insert graphics state selection and a semi‑transparent rectangle
    var operators = new List<Operator>
    {
        new Operator("GS0", "gs"),                     // Select our custom graphics state
        new Operator("0.5", "w"),                      // Set line width (optional)
        new Operator("100", "100", "200", "150", "re"), // Rectangle (x, y, width, height)
        new Operator("B")                              // Stroke the rectangle
    };

    foreach (var op in operators)
        content.Operators.Add(op);

    document.Save(@"YOUR_DIRECTORY\final_output.pdf");
}
```

De rechthoek wordt getekend met 50 % fill‑opacity terwijl de stroke volledig ondoorzichtig blijft, precies zoals gedefinieerd in de **create PDF graphics state**‑dictionary.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| `ExtGState`‑item niet gevonden | Sommige PDF‑bestanden laten de dictionary volledig weg. | De `DictionaryEditor` maakt deze automatisch aan wanneer je het eerste item toevoegt, dus extra controle is niet nodig. |
| Opacity‑waarden > 1 of < 0 | De PDF‑specificatie beperkt opacity tot het bereik `[0,1]`. | Beperk de waarden voordat je `CosPdfNumber` maakt. |
| Foutieve blend‑mode | Blend‑mode namen in PDF zijn hoofdlettergevoelig. | Gebruik exacte namen zoals `"Normal"`, `"Multiply"`, `"Screen"`. |
| Licentie‑watermerk | Evaluatieversie voegt een watermerk toe op de eerste pagina. | Pas een geldige licentiebestand toe vóór het openen van het document. |

Door deze randgevallen af te handelen, werkt je **create PDF graphics state**‑implementatie betrouwbaar met verschillende PDF‑bronnen.

## Volledig, uitvoerbaar voorbeeld

Hieronder staat een zelfstandige applicatie die je kunt kopiëren, plakken en uitvoeren. Vervang `YOUR_DIRECTORY` door een daadwerkelijke map op je computer.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;

class Program
{
    static void Main()
    {
        // Optional: apply license to remove evaluation watermark
        // var license = new Aspose.Pdf.License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        using (var document = new Document(inputPath))
        {
            // 1️⃣ Get first page and its resources
            var page = document.Pages[1];
            var resourcesEditor = new DictionaryEditor(page.Resources);

            // 2️⃣ Access (or create) ExtGState dictionary
            var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // 3️⃣ Build new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // 4️⃣ Register the state with a name (GS0)
            extGState.Add("


## Wat je hierna moet leren


De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Create custom graphics state in PDF using Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Add graphics state to PDF using Aspose.PDF for .NET (C#)](/pdf/english/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/)
- [How to create empty graphics state in a PDF with C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}