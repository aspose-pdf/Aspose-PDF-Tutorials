---
category: general
date: 2026-08-17
description: Maak een lege grafische toestand aan in een PDF met C# en Aspose.Pdf.
  Volg deze stapsgewijze handleiding om ExtGState‑resources veilig te bewerken.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty graphics state
- Aspose PDF graphics state
- C# modify PDF resources
- add ExtGState dictionary
- PDF page resources editing
language: nl
lastmod: 2026-08-17
og_description: Maak een lege grafische toestand aan in een PDF met C#. Deze tutorial
  laat zien hoe je ExtGState‑resources bewerkt met Aspose.Pdf voor betrouwbare PDF‑wijzigingen.
og_image_alt: Screenshot of C# code that adds an empty graphics state to a PDF document
og_title: Maak een lege grafische toestand in PDF met C# – stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Create empty graphics state in a PDF using C# and Aspose.Pdf. Follow
    this step‑by‑step guide to edit ExtGState resources safely.
  headline: How to create empty graphics state in a PDF with C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Hoe een lege grafische toestand in een PDF te maken met C#
url: /nl/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een lege graphics state te maken in een PDF met C#

Als je een **lege graphics state** in een PDF moet **maken**, laat deze gids je precies zien hoe je dit doet met C# en Aspose.Pdf. Je ziet een volledig, uitvoerbaar voorbeeld dat een nieuw item toevoegt aan het ExtGState‑woordenboek van de pagina zonder bestaande inhoud te beïnvloeden.

Werken met PDF‑graphics‑states is een veelvoorkomende behoefte wanneer je transparantie, mengmodi of andere render‑parameters per object wilt regelen. De onderstaande code demonstreert de aanbevolen aanpak, legt uit waarom elke stap belangrijk is, en behandelt typische variaties die je kunt tegenkomen.

## Voorvereisten

Voordat je begint, zorg dat je het volgende hebt:

* .NET 6.0 of later (het voorbeeld compileert ook met .NET Core).
* Een Aspose.Pdf for .NET‑licentie (of een tijdelijke evaluatiesleutel).
* Een map die een `input.pdf`‑bestand bevat dat je wilt aanpassen.
* Basiskennis van C#‑syntaxis en PDF‑concepten zoals resource‑woordenboeken.

## Stap 1: Het project opzetten en namespaces importeren

Maak een nieuwe console‑applicatie of integreer de code in een bestaand project. Voeg het Aspose.Pdf‑NuGet‑pakket toe:

```bash
dotnet add package Aspose.Pdf
```

Importeer vervolgens de benodigde namespaces:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
```

Deze imports geven je toegang tot de `Document`, `DictionaryEditor` en PDF‑primitieve klassen die nodig zijn om **lege graphics state**‑items te **maken**.

## Stap 2: De map definiëren die de PDF‑bestanden bevat

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfSamples\";
```

Vervang het pad door de locatie van jouw eigen PDF‑bestanden. Het opslaan van de directory in een variabele maakt de code herbruikbaar en makkelijker te testen.

## Stap 3: Het bron‑PDF‑document laden

```csharp
// Step 2: Load the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // All subsequent operations happen inside this using block
```

Het openen van het document binnen een `using`‑statement zorgt ervoor dat de bestands‑handle automatisch wordt vrijgegeven nadat je de wijzigingen hebt opgeslagen.

## Stap 4: Toegang krijgen tot de eerste pagina en het Resources‑woordenboek

```csharp
    // Step 3: Get the first page and its Resources dictionary
    var firstPage = pdfDocument.Pages[1];
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
    var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

* `Pages[1]` haalt de eerste pagina op (PDF‑paginanummers beginnen bij 1).
* `DictionaryEditor` biedt een handige manier om PDF‑woordenboeken te lezen en te wijzigen.
* Het `ExtGState`‑item bevat alle graphics‑state‑objecten voor de pagina. Als de sleutel niet bestaat, maakt Aspose.Pdf automatisch een leeg woordenboek aan.

## Stap 5: Een nieuw leeg graphics‑state‑woordenboek bouwen

De graphics‑state die je toevoegt kan leeg zijn of vooraf gevuld met parameters zoals opacity (`CA`, `ca`) of blend‑mode (`BM`). In deze tutorial maken we een **lege graphics state** en stellen vervolgens een paar typische waarden in om te illustreren hoe het woordenboek werkt.

```csharp
    // Step 4: Create a new empty graphics‑state dictionary and set its parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // Stroke opacity
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };
    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

* `CosPdfDictionary.CreateEmptyDictionary` maakt een schone container die je kunt vullen met willekeurige graphics‑state‑sleutels.
* Het toevoegen van `CA`, `ca` en `BM` is optioneel; je kunt ze weglaten als je echt een lege state nodig hebt. De code laat zien hoe je items toevoegt wanneer je later de rendering wilt regelen.

## Stap 6: De nieuwe graphics state invoegen in het ExtGState‑woordenboek

```csharp
    // Step 5: Add the new graphics state to the page's ExtGState dictionary (e.g., name it "GS0")
    extGStateDict.Add("GS0", newGraphicsState);
```

Het benoemen van het item `"GS0"` volgt de gangbare conventie om graphics‑state‑namen te prefixen met “GS”. Je kunt elke geldige PDF‑naam kiezen die niet conflicteert met bestaande sleutels.

## Stap 7: Het gewijzigde PDF‑document opslaan

```csharp
    // Step 6: Save the modified PDF document
    pdfDocument.Save(dataDir + "output.pdf");
}
```

De `Save`‑aanroep schrijft het bijgewerkte bestand naar `output.pdf`. Het openen van dit bestand in een PDF‑viewer bevestigt dat de nieuwe graphics state bestaat; je kunt er later naar verwijzen met de `gs`‑operator in content‑streams.

### Volledige broncode

Alles samengevoegd ziet het complete programma er als volgt uit:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;

class Program
{
    static void Main()
    {
        // Define the folder that contains the PDF files
        string dataDir = @"C:\PdfSamples\";

        // Load the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Get the first page and its Resources dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create a new empty graphics‑state dictionary and set its parameters
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters)
                newGraphicsState.Add(p);

            // Add the new graphics state to the page's ExtGState dictionary (name it "GS0")
            extGStateDict.Add("GS0", newGraphicsState);

            // Save the modified PDF document
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("Empty graphics state created and saved to output.pdf");
    }
}
```

Het uitvoeren van het programma geeft een bevestigingsregel weer en produceert `output.pdf` met de nieuw toegevoegde graphics state.

## Waarom deze aanpak het beste werkt

* **Direct woordenboek bewerken** – Met `DictionaryEditor` hoef je de volledige content‑stream niet te parseren. Je wijzigt alleen de resources die je interesseren.
* **Getypeerde PDF‑primitieven** – `CosPdfNumber`, `CosPdfName` en `CosPdfDictionary` garanderen dat de gegenereerde PDF voldoet aan de PDF 1.7‑specificatie.
* **Veiligheid** – Het `using`‑blok maakt het `Document`‑object schoon, waardoor bestands‑locks die latere builds kunnen corrupt maken, worden voorkomen.
* **Uitbreidbaarheid** – Zodra de lege graphics state bestaat, kun je er vanuit elke content‑operator (`gs`) naar verwijzen om opacity, blend‑mode of andere parameters voor geselecteerde teken‑commando’s te wijzigen.

## Veelvoorkomende variaties en randgevallen

| Situatie | Aanbevolen aanpassing |
|-----------|-------------------|
| **Meerdere pagina's** | Loop over `pdfDocument.Pages` en herhaal de woordenboek‑invoeging voor elke pagina die je wilt aanpassen. |
| **Geen bestaand ExtGState‑item** | `resourcesEditor["ExtGState"]` maakt automatisch een leeg woordenboek aan als het niet bestaat. Er is geen extra code nodig. |
| **Andere graphics‑state‑naam** | Vervang `"GS0"` door een naam die past bij jouw naamgevingsconventie, bv. `"MyTransparentState"`. |
| **Alleen een lege state toevoegen** | Laat de `parameters`‑array en de `foreach`‑lus weg; het woordenboek blijft leeg. |
| **Werken met versleutelde PDF's** | Geef het wachtwoord op bij het aanmaken van `new Document(path, password)` voordat je resources bewerkt. |

## Het resultaat verifiëren

Je kunt controleren of de graphics state is toegevoegd door de PDF te inspecteren met een low‑level viewer zoals **PDF‑Tron** of **iText Sharp**. Zoek naar een item dat er ongeveer zo uitziet:

```
/ExtGState << /GS0 << /CA 1 /ca 0.5 /BM /Normal >> >>
```

Als het item verschijnt, is de **create empty graphics state**‑operatie geslaagd.

## Conclusie

Je weet nu hoe je een **lege graphics state** in een PDF kunt **maken** met C# en Aspose.Pdf. De tutorial heeft elke stap behandeld – van het laden van het document tot het bewerken van het `ExtGState`‑woordenboek en het opslaan van het resultaat – en de reden achter elke handeling uitgelegd.  

Vanaf hier kun je:

* De nieuwe graphics state gebruiken in content‑streams (`gs /GS0`).
* Experimenteren met extra sleutels zoals `/SM` (stroke adjustment) of `/OPM` (overprint mode).
* Dezelfde techniek toepassen op andere resource‑typen zoals `/XObject` of `/ColorSpace`.

Veel plezier met PDF‑hacking, en voel je vrij om andere **Aspose PDF graphics state**‑scenario’s te verkennen, zoals dynamische opacity‑wijzigingen of aangepaste blend‑modi!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [How to Remove Graphics from PDFs Using Aspose.PDF .NET&#58; A Complete Guide](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Create & Fill Rectangles in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}