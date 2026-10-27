---
category: general
date: 2026-10-26
description: Leer hoe u een leeg PDF‑woordenboek maakt en PDF‑resources bewerkt met
  Aspose.PDF voor C#. Stapsgewijze handleiding met volledig codevoorbeeld.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- edit PDF resources
- Aspose.PDF C#
- PDF manipulation C#
- PDF graphics state
language: nl
lastmod: 2026-10-26
og_description: Maak een leeg PDF-woordenboek en bewerk PDF-resources met Aspose.PDF
  voor C#. Volg deze volledige tutorial om grafische toestanden in PDF’s te wijzigen.
og_image_alt: Screenshot showing creation of empty PDF dictionary in Aspose.PDF
og_title: Maak een leeg PDF-woordenboek & bewerk PDF-resources in C# – Aspose.PDF-gids
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  headline: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  type: TechArticle
- description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  name: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  steps:
  - name: Populate the graphics state entries
    text: 'Add the standard keys:'
  - name: Register the new graphics state in the resource dictionary
    text: Give the state a name (`GS0`) and add it to the `ExtGState` dictionary that
      lives inside the page resources.
  - name: Expected output
    text: 'Running the program prints:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF
title: Hoe een leeg PDF‑woordenboek maken en PDF‑resources bewerken met Aspose.PDF
  in C#
url: /nl/net/programming-with-document/how-to-create-empty-pdf-dictionary-and-edit-pdf-resources-wi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe maak je een lege PDF-woordenboek en bewerk je PDF-resources met Aspose.PDF in C#

Als je een **leeg PDF-woordenboek** moet **maken** en vervolgens **PDF-resources** moet **bewerken** in een C#-applicatie, laat deze gids je de exacte stappen zien. Je ziet een volledig, uitvoerbaar voorbeeld dat een aangepaste graphics state toevoegt aan de eerste pagina van een bestaande PDF.

Werken met low‑level PDF‑objecten kan ontmoedigend aanvoelen, maar Aspose.PDF biedt een duidelijke API voor het manipuleren van woordenboeken. Aan het einde van deze tutorial begrijp je waarom elke bewerking belangrijk is en hoe je de code kunt aanpassen voor andere resource‑typen.

## Vereisten

* .NET 6.0 (of later) geïnstalleerd.
* Een gelicentieerde kopie van **Aspose.PDF for .NET** – de gratis proefversie werkt voor testen.
* Een IDE zoals Visual Studio 2022.
* Een PDF‑bestand met de naam `input.pdf` geplaatst in een map die je vanuit de code kunt refereren.

Er zijn geen extra NuGet‑pakketten vereist naast `Aspose.Pdf`.

## Stap 1: Zet het project op en importeer namespaces

Maak een nieuw console‑project aan en voeg het Aspose.PDF‑pakket toe:

```bash
dotnet new console -n PdfDictionaryDemo
cd PdfDictionaryDemo
dotnet add package Aspose.Pdf
```

Importeer in `Program.cs` de namespaces die je gaat gebruiken:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
```

Deze imports maken de `Document`, `DictionaryEditor` en COS (Canonical Object Structure) klassen beschikbaar, waarmee je **leeg PDF-woordenboek** objecten kunt **maken** en bestaande resource‑woordenboeken kunt wijzigen.

## Stap 2: Definieer de map die de PDF‑bestanden bevat

Geef de directory op die `input.pdf` bevat. Het gebruik van een absoluut pad voorkomt onduidelijkheid wanneer het programma vanuit een andere werkmap wordt uitgevoerd.

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfDemo\";
```

Vervang `C:\PdfDemo\` door het pad op jouw machine. Het bewaren van het pad in een variabele maakt het gemakkelijk om het zowel voor invoer‑ als uitvoerbestanden te hergebruiken.

## Stap 3: Open het bron‑PDF‑document

Laad de PDF die je wilt aanpassen binnen een `using`‑blok zodat de bestands‑handle automatisch wordt vrijgegeven.

```csharp
// Step 2: Open the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // The rest of the workflow lives inside this block
}
```

Het openen van het document geeft je toegang tot de paginacollectie, resource‑woordenboeken en low‑level COS‑objecten.

## Stap 4: Toegang tot de eerste pagina en het resource‑woordenboek

De eerste pagina heeft index `1` (PDF‑pagina's zijn 1‑gebaseerd). Haal het `Resources`‑woordenboek van de pagina op en wikkel het in een `DictionaryEditor` om veilig te kunnen bewerken.

```csharp
// Step 3: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` abstraheert de onderliggende COS‑structuur, waardoor je items kunt lezen of aanmaken zonder de PDF te corrupten.

## Stap 5: **Leeg PDF-woordenboek maken** voor een nieuwe graphics state

Een graphics state regelt transparantie, blend‑mode en andere tekenparameters. Om een aangepaste state toe te voegen heb je eerst een leeg woordenboek nodig, waarna je het vult met de vereiste items.

```csharp
// Step 4: Retrieve the ExtGState dictionary and add a new graphics state
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

// Create an empty dictionary that will hold the graphics state parameters
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
```

De aanroep van `CreateEmptyDictionary` is de kern van **leeg PDF-woordenboek maken** objecten. Het retourneert een COS‑woordenboek dat tot hetzelfde document behoort, waardoor de cross‑reference integriteit gewaarborgd blijft.

### Vul de graphics state items in

Voeg de standaard sleutels toe:

* `CA` – stroking alfa‑constante (bereik 0 – 1).
* `ca` – non‑stroking alfa‑constante.
* `BM` – blend‑mode naam.

```csharp
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

Elke entry wordt toegevoegd aan het lege woordenboek dat je zojuist hebt aangemaakt. Door de definitie te scheiden van de insertielus houd je de code leesbaar en maak je het later eenvoudig om extra sleutels toe te voegen.

### Registreer de nieuwe graphics state in het resource‑woordenboek

Geef de state een naam (`GS0`) en voeg deze toe aan het `ExtGState`‑woordenboek dat zich binnen de page‑resources bevindt.

```csharp
// Name the new graphics state "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

Nu bevat het resource‑woordenboek van de pagina een referentie naar de aangepaste graphics state, die je later kunt toepassen op content‑streams.

## Stap 6: Sla de bijgewerkte PDF op

Schrijf tenslotte het gewijzigde document naar een nieuw bestand. Het origineel ongewijzigd laten helpt je de wijzigingen te verifiëren.

```csharp
// Step 5: Save the updated PDF
pdfDocument.Save(dataDir + "output.pdf");
```

Wanneer je `output.pdf` opent in een viewer die graphics‑state inspectie ondersteunt (bijv. Adobe Acrobat Pro), zie je dat het `ExtGState`‑woordenboek een entry met de naam `GS0` bevat met de waarden die je hebt gedefinieerd.

## Volledige broncode

Alle onderdelen samenvoegen levert een zelfstandige applicatie op:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

class Program
{
    static void Main()
    {
        // Step 1: Define the folder that contains the PDF files
        string dataDir = @"C:\PdfDemo\"; // adjust to your environment

        // Step 2: Open the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Step 3: Access the first page and its resource dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 4: Retrieve the ExtGState dictionary and add a new graphics state
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // **Create empty PDF dictionary** for the new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateEntries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };

            foreach (var entry in graphicsStateEntries)
                newGraphicsState.Add(entry);

            // Register the new graphics state as "GS0"
            extGStateDict.Add("GS0", newGraphicsState);

            // Step 5: Save the updated PDF
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

### Verwachte output

Het uitvoeren van het programma geeft het volgende weer:

```
PDF updated successfully.
```

en maakt `output.pdf` aan in dezelfde map. Het openen van het bestand onthult een nieuwe entry onder **Resources → ExtGState → GS0** met de parameters die je hebt ingesteld.

## Veelvoorkomende variaties en randgevallen

| Situatie | Hoe de code aan te passen |
|-----------|-----------------------|
| **Meerdere pagina's** hebben dezelfde graphics state nodig | Maak het woordenboek één keer aan en voeg vervolgens dezelfde `GS0`‑referentie toe aan het `ExtGState`‑woordenboek van elke pagina. |
| **Andere blend‑mode** (bijv. `Multiply`) | Verander de waarde `CosPdfName("Normal")` naar `CosPdfName("Multiply")`. |
| **Geen bestaand ExtGState‑woordenboek** | Controleer vóór het benaderen van `resourcesEditor["ExtGState"]` of `resourcesEditor.ContainsKey("ExtGState")` true is. Indien ontbrekend, maak een nieuw leeg woordenboek aan en voeg het toe aan `firstPage.Resources`. |
| **Grote PDF’s** veroorzaken geheugenbelasting | Gebruik de `PdfDocument.Load`‑overload die pagina's streamt, of verwerk pagina's één voor één binnen het `using`‑blok. |
| **Andere resources bewerken nodig** (fonts, XObjects) | Vervang `"ExtGState"` door `"Font"` of `"XObject"` in de `resourcesEditor`‑lookup, en volg vervolgens hetzelfde patroon van een leeg woordenboek maken en vullen. |

Deze variaties tonen aan hoe hetzelfde **leeg PDF-woordenboek maken** patroon toepasbaar is op elk resource‑type dat je wilt **PDF-resources bewerken**.

## Pro‑tips

* **Valideer het resultaat** – na het opslaan, open de PDF in een tool die het ruwe resource‑woordenboek kan weergeven (bijv. PDF‑Box’s `PDFDebugger`) om te bevestigen dat de entry bestaat.
* **Herbruik woordenboeken** – als je dezelfde graphics state aan veel pagina's toevoegt, bewaar het woordenboek in een variabele en verwijs ernaar in plaats van het elke keer opnieuw aan te maken.
* **Versie‑compatibiliteit** – de code werkt met Aspose.PDF 23.12 en later. Eerdere versies kunnen `CosDictionary` vereisen in plaats van `CosPdfDictionary`.

## Conclusie

Je weet nu hoe je **leeg PDF-woordenboek** objecten kunt **maken** en **PDF-resources** kunt **bewerken** met Aspose.PDF voor C#. De tutorial besprak het openen van een document, toegang tot het resource‑woordenboek van de pagina, het bouwen van een aangepaste graphics state, het registreren ervan en het opslaan van het resultaat. Vanaf hier kun je experimenteren met andere resource‑typen, meerdere graphics states combineren, of de techniek integreren in een grotere PDF‑verwerkingspipeline.

---

*Klaar om meer te verkennen? Probeer een aangepaste **ExtGState** toe te voegen aan een content‑stream, of bewerk het **Font**‑woordenboek om nieuwe fonts in te sluiten. Beide volgen hetzelfde patroon van een leeg woordenboek maken en PDF‑resources bewerken.*

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [PDF Resource Dictionary bewerken met Aspose.PDF – C# gids](/pdf/english/net/programming-with-operators/edit-pdf-resource-dictionary-with-aspose-pdf-c-guide/)
- [Aangepaste graphics state maken in PDF met Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Hoe maak je een lege graphics state in een PDF met C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}