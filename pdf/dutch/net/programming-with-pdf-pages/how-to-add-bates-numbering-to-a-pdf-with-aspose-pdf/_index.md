---
category: general
date: 2026-10-07
description: Leer hoe je Bates‑nummering aan een PDF kunt toevoegen met C#. Deze stapsgewijze
  gids behandelt ook PDF‑paginanummering en andere nummeringstrucs.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- pdf page numbering
- number pdf pages
- how to add bates
- bates numbering pdf
language: nl
lastmod: 2026-10-07
og_description: Voeg snel Bates-nummering toe aan een PDF. Volg deze tutorial om pdf-paginanummering
  te beheersen, pdf-pagina's te nummeren en documenttracking te automatiseren.
og_image_alt: Screenshot of a PDF with Bates numbers added using Aspose.Pdf
og_title: Voeg Bates-nummering toe aan PDF's in C# – volledige Aspose-gids
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  headline: How to add bates numbering to a PDF with Aspose.Pdf
  type: TechArticle
- description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  name: How to add bates numbering to a PDF with Aspose.Pdf
  steps:
  - name: 1. Can I change the location of the numbers?
    text: Yes. Set `batesOptions.Position = new Position(10, 10, 10, 10);` where the
      four values represent margins from the top, bottom, left, and right edges. Aspose
      also provides predefined enums such as `BatesNumberingPosition.BottomCenter`.
  - name: 2. What if my PDF already contains page numbers?
    text: Adding Bates numbers will **stack** on top of existing numbers. To avoid
      visual clutter, either hide the original numbers (if they are part of a text
      layer) or adjust the `batesOptions` font size and position.
  - name: 3. Does this work with encrypted PDFs?
    text: 'Aspose can open password‑protected PDFs if you supply the password:'
  - name: 4. How do I **number pdf pages** with a simple sequential counter (no prefix/suffix)?
    text: 'Just set `Prefix = string.Empty` and `Suffix = string.Empty`:'
  - name: 5. Can I use this approach in ASP.NET Core to serve PDFs on‑the‑fly?
    text: 'Absolutely. Load the document, apply the numbering, then write the stream
      to the HTTP response:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Hoe batesnummering aan een PDF toe te voegen met Aspose.Pdf
url: /nl/net/programming-with-pdf-pages/how-to-add-bates-numbering-to-a-pdf-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe bates‑nummering toevoegen aan een PDF met Aspose.Pdf

Als je **bates‑nummering** aan een PDF wilt **toevoegen**, laat deze gids je precies zien hoe je dat in C# doet. Of je nu juridische dossiers samenstelt, casusbestanden beheert, of gewoon betrouwbare **pdf paginanummering** wilt, de onderstaande stappen bieden een complete, uitvoerbare oplossing.

In deze tutorial leer je hoe je:

* Een bestaande PDF‑bestand laadt.
* Bates‑nummeringsopties configureert zoals prefix, startnummer, cijfer‑padding, scheidingsteken en suffix.
* De nummering op elke pagina toepast.
* Het bijgewerkte document opslaat.

Er zijn geen externe tools nodig buiten de Aspose.Pdf for .NET‑bibliotheek, en de code werkt met .NET 6+ evenals .NET Framework 4.7.2+.

---

## Vereisten

Voordat je begint, zorg dat je het volgende hebt:

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| **Aspose.Pdf for .NET** (NuGet‑pakket `Aspose.Pdf`) | Biedt de `Document`‑ en `BatesNumberingOptions`‑klassen die in de code worden gebruikt. |
| **.NET SDK** (6.0 of later aanbevolen) | Stelt je in staat om de C#‑console‑applicatie te compileren en uit te voeren. |
| **Een bron‑PDF** die je wilt nummeren | De tutorial gebruikt `source.pdf` als voorbeeld; vervang het pad door je eigen bestand. |
| **Schrijfrechten** voor de doelmap | De `Save`‑aanroep moet het nieuwe bestand kunnen wegschrijven. |

Je kunt de bibliotheek installeren met de volgende CLI‑opdracht:

```bash
dotnet add package Aspose.Pdf
```

---

## Stap 1: Maak een nieuw console‑project

Open een terminal en voer uit:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
```

Dit maakt een minimaal C#‑project dat we zullen vullen met de code die nodig is om **bates‑nummering toe te voegen**.

---

## Stap 2: Voeg de vereiste `using`‑directives toe

Open `Program.cs` en voeg de namespaces toe aan de bovenkant van het bestand:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

* `Aspose.Pdf` geeft je toegang tot de `Document`‑klasse voor het laden en opslaan van PDF’s.  
* `Aspose.Pdf.Text` bevat `BatesNumberingOptions`, het object dat bepaalt hoe de nummers verschijnen.

---

## Stap 3: Laad de bron‑PDF

De eerste uitvoerbare regel laadt de PDF die je wilt nummeren. Vervang `"YOUR_DIRECTORY/source.pdf"` door het daadwerkelijke pad naar je bestand.

```csharp
// Load the source PDF
Document pdf = new Document("YOUR_DIRECTORY/source.pdf");
```

Als het bestand niet gevonden kan worden, gooit Aspose een `FileNotFoundException`. Om dit te voorkomen, kun je het pad van tevoren valideren:

```csharp
if (!System.IO.File.Exists("YOUR_DIRECTORY/source.pdf"))
{
    Console.WriteLine("Source PDF not found.");
    return;
}
```

---

## Stap 4: Definieer Bates‑nummeringsopties

`BatesNumberingOptions` laat je elk visueel element van de nummering regelen. Het voorbeeld hieronder toont een typische configuratie voor juridische dossiers:

```csharp
// Define Bates numbering options
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",          // Text before the numeric part
    StartNumber = 1000,       // First number to use
    Digits = 6,               // Pad with leading zeros (e.g., 001000)
    Separator = "-",          // Character between prefix, number, and suffix
    Suffix = "-2025"          // Text after the numeric part
};
```

**Waarom elke eigenschap belangrijk is**

| Eigenschap | Doel |
|------------|------|
| `Prefix` | Helpt je documenten te groeperen per project, klant of zaak. |
| `StartNumber` | Stelt de initiële teller in; handig wanneer je al genummerde bestanden hebt. |
| `Digits` | Garandeert een uniforme breedte, waardoor sorteren makkelijker wordt. |
| `Separator` | Verbetert de leesbaarheid, vooral bij combinatie van prefix en suffix. |
| `Suffix` | Stelt je in staat een jaar, versie of andere achtervoegsel‑identifier toe te voegen. |

Je kunt ook de plaatsing (boven, onder, links, rechts) en het lettertype regelen via `batesOptions.Position` en `batesOptions.Font`. Voor de meeste scenario’s werken de standaardinstellingen (onder‑rechts, 12‑pt Times New Roman) prima.

---

## Stap 5: Pas de nummering op elke pagina toe

Het aanroepen van `pdf.BatesNumbering.Add` voegt de nummers toe op elke pagina in de volgorde waarin ze verschijnen.

```csharp
// Apply Bates numbering to every page
pdf.BatesNumbering.Add(batesOptions);
```

Als je alleen een subset van pagina’s wilt nummeren (bijv. de omslagpagina overslaan), kun je een `PageCollection` doorgeven:

```csharp
// Example: skip the first page
pdf.BatesNumbering.Add(batesOptions, pdf.Pages.Skip(1));
```

---

## Stap 6: Sla de bijgewerkte PDF op

Schrijf tenslotte het gewijzigde document naar schijf. De bestandsnaam geeft meestal aan dat de PDF nu Bates‑nummers bevat.

```csharp
// Save the PDF with Bates numbers applied
pdf.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering added successfully.");
```

Als de doelmap niet bestaat, maakt Aspose deze automatisch aan. Zorg er echter wel voor dat je schrijfrechten hebt om een `UnauthorizedAccessException` te voorkomen.

---

## Volledig, uitvoerbaar voorbeeld

Alle onderdelen samengevoegd, hier is een compleet programma dat je kunt kopiëren, plakken en uitvoeren:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source PDF
        // -------------------------------------------------
        const string inputPath = "YOUR_DIRECTORY/source.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        Document pdf = new Document(inputPath);

        // -------------------------------------------------
        // 2️⃣ Configure Bates numbering
        // -------------------------------------------------
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            Digits = 6,
            Separator = "-",
            Suffix = "-2025"
        };

        // -------------------------------------------------
        // 3️⃣ Apply the numbering to every page
        // -------------------------------------------------
        pdf.BatesNumbering.Add(batesOptions);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";
        pdf.Save(outputPath);
        Console.WriteLine($"Bates numbering added. Saved to {outputPath}");
    }
}
```

**Verwachte uitvoer** (console):

```
Bates numbering added. Saved to YOUR_DIRECTORY/bates_numbered.pdf
```

Open `bates_numbered.pdf` en je ziet elke pagina gelabeld met iets als `CASE-001000-2025`, `CASE-001001-2025`, enz., gepositioneerd in de standaard onder‑rechts hoek.

---

## Veelgestelde vragen (FAQ)

### 1. Kan ik de locatie van de nummers wijzigen?
Ja. Stel `batesOptions.Position = new Position(10, 10, 10, 10);` in, waarbij de vier waarden de marges vanaf respectievelijk de boven‑, onder‑, linker‑ en rechterrand aangeven. Aspose biedt ook vooraf gedefinieerde enums zoals `BatesNumberingPosition.BottomCenter`.

### 2. Wat als mijn PDF al paginanummers bevat?
Het toevoegen van Bates‑nummers **stapelt** zich bovenop bestaande nummers. Om visuele rommel te vermijden, kun je de originele nummers verbergen (als ze deel uitmaken van een tekstlaag) of de lettergrootte en positie van `batesOptions` aanpassen.

### 3. Werkt dit met versleutelde PDF’s?
Aspose kan wachtwoord‑beveiligde PDF’s openen als je het wachtwoord opgeeft:

```csharp
Document pdf = new Document("source.pdf", new LoadOptions { Password = "mySecret" });
```

Bates‑nummering wordt vervolgens op dezelfde manier toegepast.

### 4. Hoe **nummer ik pdf‑pagina’s** met een eenvoudige opeenvolgende teller (geen prefix/suffix)?
Stel simpelweg `Prefix = string.Empty` en `Suffix = string.Empty` in:

```csharp
BatesNumberingOptions simple = new BatesNumberingOptions
{
    StartNumber = 1,
    Digits = 4   // 0001, 0002, …
};
pdf.BatesNumbering.Add(simple);
```

### 5. Kan ik deze aanpak gebruiken in ASP.NET Core om PDF’s on‑the‑fly te serveren?
Absoluut. Laad het document, pas de nummering toe, en schrijf de stream naar de HTTP‑respons:

```csharp
using (var ms = new MemoryStream())
{
    pdf.Save(ms);
    ms.Position = 0;
    return File(ms, "application/pdf", "bates_numbered.pdf");
}
```

---

## Randgevallen en best‑practice tips

| Situatie | Aanbevolen aanpak |
|----------|-------------------|
| **Grote PDF’s (honderden pagina’s)** | Roep `pdf.BatesNumbering.Add` **na** eventuele paginaniveau‑transformaties aan om herhaaldelijk verwerken van dezelfde pagina’s te vermijden. |
| **Aangepaste lettertypen** | Stel `batesOptions.Font = FontRepository.FindFont("Arial")` in en pas `batesOptions.FontSize` aan voor betere leesbaarheid op gescande documenten. |
| **Prestaties‑kritische batch‑taken** | Hergebruik één `Document`‑instantie bij het verwerken van vele bestanden in een lus; maak deze na elke iteratie vrij om geheugen te besparen. |
| **Internationale tekens** | Gebruik Unicode‑compatibele lettertypen (bijv. `Times New Roman Unicode`) zodat prefix of suffix correct wordt weergegeven. |
| **Versie‑compatibiliteit** | De code werkt met Aspose.Pdf 23.10 en nieuwer. Als je een oudere versie target, controleer dan de API‑referentie op eventuele wijzigingen in eigenschapsnamen. |

---

## Conclusie

Je weet nu hoe je **bates‑nummering** aan een PDF kunt toevoegen met Aspose.Pdf for .NET. De tutorial behandelde het laden van een PDF, het configureren van `BatesNumberingOptions`, het toepassen van de nummers op elke pagina, en het opslaan van het resultaat. Met deze bouwblokken kun je ook generieke **pdf paginanummering**, **nummer pdf‑pagina’s** met aangepaste formaten implementeren, en het proces integreren in grotere automatiserings‑pipelines.

**Volgende stappen**

* Verken de **bates numbering pdf** API verder om lettertype, kleur en plaatsing aan te passen.  
* Combineer deze techniek met **digitale handtekeningen** om tamper‑evidente juridische dossiers te creëren.  
* Kijk naar Aspose’s **PDF‑samenvoeg‑functionaliteit** als je meerdere casusbestanden moet concatenaten vóór het nummeren.

Voel je vrij om te experimenteren met verschillende prefixes, suffixes en cijferlengtes om te voldoen aan de archiveringsnormen van jouw organisatie. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementaties in je eigen projecten te verkennen.

- [Create PDF Document C# – Add Bates Numbering Guide](/pdf/english/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/)
- [How to Add Bates Numbering in PDF with C# – Complete Guide](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-c-complete-guide/)
- [Aspose PDF Tutorial – Insert a Blank Page and Update Bates Numbering](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}