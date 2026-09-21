---
category: general
date: 2026-01-15
description: Voeg snel batesnummers toe aan uw PDF met Aspose.Pdf. Leer hoe u een
  voettekst aan een PDF toevoegt, paginanummers aan een PDF toevoegt en aangepaste
  paginanummering toevoegt.
draft: false
keywords:
- add bates numbers
- bates numbering pdf
- add footer to pdf
- add page numbers pdf
- add custom page numbering
language: nl
og_description: Voeg snel Bates-nummers toe aan uw PDF met Aspose.Pdf. Leer hoe u
  een voettekst aan een PDF kunt toevoegen, paginanummers aan een PDF kunt toevoegen
  en aangepaste paginanummering kunt toepassen.
og_title: Bates-nummers toevoegen aan PDF – bates nummering pdf
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Bates-nummers toevoegen aan PDF – Bates-nummering pdf
url: /nl/net/programming-with-text/add-bates-numbers-to-pdf-bates-numbering-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Voeg Bates-nummers toe aan PDF – Complete gids

Heb je ooit **Bates-nummers** aan een PDF moeten toevoegen, maar wist je niet waar te beginnen? Je bent niet de enige—juridische teams, auditors en iedereen die met enorme documentensets werkt, loopt hier dagelijks tegenaan. Het goede nieuws? Met Aspose.Pdf voor .NET kun je die nummers met slechts een handvol regels op elke pagina strooien.

In deze tutorial lopen we het volledige proces door: van het importeren van de Aspose.Pdf‑bibliotheek, het laden van je bronbestand, het configureren van een *BatesNumberingArtifact*, het toevoegen ervan als voettekst, en uiteindelijk het opslaan van het resultaat. Aan het einde weet je ook hoe je **voettekst aan pdf toevoegt**, **paginanummers pdf toevoegt**, en zelfs **aangepaste paginanummering toevoegt** voor die lastige randgevallen.

## Wat je nodig hebt

- .NET 6+ (of .NET Framework 4.8 als je nog op de klassieke stack zit)  
- Een referentie naar het **Aspose.Pdf** NuGet‑pakket (`Install-Package Aspose.Pdf`)  
- Een PDF‑bestand dat je wilt stempelen (we noemen het `source.pdf`)  

Dat is alles—geen extra tools, geen zware PDF‑editors. Laten we beginnen.

![add bates numbers example](https://example.com/images/add-bates-numbers.png "add bates numbers example")

## Stap 1: Voeg Bates-nummers toe – Laad het PDF‑document

Eerst hebben we een `Document`‑object nodig dat het PDF‑bestand vertegenwoordigt dat we gaan aanpassen. Zie dit als het openen van een Word‑document voordat je begint te typen.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the PDF you want to add bates numbers to
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // The rest of the steps go here...
    }
}
```

> **Waarom dit belangrijk is:** Het laden van het bestand geeft je toegang tot de `Pages`‑collectie, waar we later het Bates‑nummerings‑artifact aan gaan koppelen. Als het bestand niet gevonden kan worden, gooit Aspose een duidelijke `FileNotFoundException`, dus controleer het pad goed.

## Stap 2: Configureer bates numbering pdf‑instellingen

Nu definiëren we *hoe* de nummers eruit moeten zien. De `BatesNumberingArtifact` laat je een prefix, startnummer, cijfer‑opvulling, suffix en plaatsing instellen. Dit is de kern van **bates numbering pdf**.

```csharp
// Step 2: Create and configure the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    NumberDigits = 5,          // forces 5 digits, e.g., 01000
    Suffix = "-A",
    Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
};
```

> **Pro tip:** Als je de nummers in de header wilt laten verschijnen, vervang `BottomCenter` door `TopCenter`. De plaatsings‑enum ondersteunt ook `BottomLeft`, `BottomRight`, enz., waardoor je flexibiliteit hebt voor verschillende **add footer to pdf**‑stijlen.

## Stap 3: Voeg paginanummers pdf toe – Koppel het artifact aan elke pagina

Met het artifact klaar, lopen we door elke pagina en voegen het toe aan de `Artifacts`‑collectie. Dit is de stap die daadwerkelijk **adds page numbers pdf**.

```csharp
// Step 3: Attach the artifact to each page
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

> **Wat er onder de motorkap gebeurt:** De `Artifacts`‑collectie wordt gerenderd na de hoofdinhoud van de pagina, waardoor het Bates‑nummer boven eventuele bestaande tekst maar onder annotaties verschijnt. Als je het nummer achter de inhoud wilt (zeldzaam), gebruik je `page.Artifacts.Insert(0, batesArtifact)`.

## Stap 4: Voeg aangepaste paginanummering toe – Sla de bijgewerkte PDF op

Tot slot schrijven we het aangepaste document naar schijf. Het uitvoerbestand bevat de Bates‑nummers als een permanent onderdeel van elke pagina.

```csharp
// Step 4: Save the PDF with the new numbering
pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
```

> **Verificatietip:** Open `bates_out.pdf` in een viewer. Je zou iets moeten zien als `CASE-01000-A` gecentreerd onderaan elke pagina. Als de nummers ontbreken, controleer dan of de eigenschap `Placement` overeenkomt met de gewenste locatie.

## Volledig werkend voorbeeld

Alles bij elkaar, hier is het complete, kant‑klaar programma:

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the source PDF
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // Configure Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            NumberDigits = 5,
            Suffix = "-A",
            Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
        };

        // Attach artifact to each page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.Artifacts.Add(batesArtifact);
        }

        // Save the new PDF (adds footer to pdf)
        pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

        Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
    }
}
```

### Verwacht resultaat

- **Bestand:** `bates_out.pdf` in dezelfde map als `source.pdf`
- **Visueel:** Tekst `CASE-01000-A`, `CASE-01001-A`, … gecentreerd onderaan elke pagina
- **Gedrag:** Nummers zijn permanent ingebed; ze overleven afdrukken, flattenen en verdere bewerking.

## Veelvoorkomende variaties & randgevallen

| Situatie | Hoe aan te passen |
|-----------|---------------|
| **Ander startnummer** | Verander `StartNumber` naar elk geheel getal (bijv. `StartNumber = 500`). |
| **Letter‑suffixen per volume** | Gebruik een lus om `Suffix` per pagina aan te passen, of maak meerdere artifacts met verschillende suffixen. |
| **Rechts‑gealigneerde nummering** | Stel `Placement = BatesNumberingArtifact.PlacementLocation.BottomRight`. |
| **Grote documenten (10k+ pagina's)** | Overweeg pagina’s in batches te verwerken of verhoog `NumberDigits` om overflow te voorkomen. |
| **Nummers verbergen op bepaalde pagina's** | Sla die pagina’s over in de `foreach`‑lus (bijv. `if (page.Number != 1) page.Artifacts.Add(batesArtifact);`). |

> **Let op:** Het gebruik van een `Prefix` of `Suffix` die illegale bestandsnaam‑tekens bevat (bijv. `*` of `?`). Aspose embedt ze nog steeds, maar ze kunnen problemen veroorzaken bij later tekst‑extractie.

## Pro‑tips voor productiegebruik

- **Cache het artifact** als je veel PDF’s achter elkaar verwerkt; één keer aanmaken bespaart enkele milliseconden per bestand.  
- **Thread‑veiligheid:** De `BatesNumberingArtifact`‑instantie is niet thread‑safe, geef elke thread zijn eigen kopie.  
- **Prestaties:** Schakel voor enorme batches PDF‑compressie uit (`pdfDocument.Compress = false`) vóór het opslaan, en zet het later weer aan indien nodig.  
- **Testen:** Voer altijd een snelle visuele controle uit op de eerste gegenereerde PDF om te bevestigen dat de plaatsing voldoet aan de eisen van je juridische team.

## Conclusie

Je beschikt nu over een solide, end‑to‑end‑recept om **Bates-nummers** aan elke PDF toe te voegen met Aspose.Pdf, inclusief opties om **voettekst aan pdf toe te voegen**, **paginanummers pdf toe te voegen**, en **aangepaste paginanummering toe te voegen**. De code is volledig zelfstandig, werkt met .NET 6 en hoger, en kan in elke bestaande automatiseringspipeline worden geïntegreerd.

Wat nu? Probeer de `BottomCenter`‑plaatsing te vervangen door een header‑stijl, experimenteer met dynamische prefixes (bijv. zaak‑ID’s uit een database), of combineer dit met Aspose’s tekst‑extractie‑functies om een doorzoekbare index van je nieuw genummerde documenten te genereren. De mogelijkheden zijn eindeloos, en je hebt zojuist een krachtig hulpmiddel voor documentbeheer in handen.

Veel programmeerplezier, en moge je PDF‑bestanden altijd perfect genummerd blijven!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}