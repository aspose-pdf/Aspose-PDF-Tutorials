---
category: general
date: 2026-07-20
description: Hoe batesnummering aan een PDF toe te voegen met Aspose.Pdf. Leer hoe
  je batesnummers aan een PDF toevoegt en een stempel op elke pagina snel en betrouwbaar
  plaatst.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to add bates numbering
- add bates numbers pdf
- add stamp to each page
language: nl
lastmod: 2026-07-20
og_description: Hoe batesnummering toe te voegen aan een PDF met Aspose.Pdf. Deze
  gids laat zien hoe je batesnummers aan een PDF toevoegt en elke pagina stempelt
  in slechts een paar regels C#.
og_image_alt: Screenshot of a PDF page displaying Bates numbering added by Aspose.Pdf
og_title: Hoe Bates-nummering toe te voegen in PDF – Complete Aspose.Pdf-tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: How to add bates numbering to a PDF using Aspose.Pdf. Learn to add
    bates numbers pdf and add stamp to each page quickly and reliably.
  headline: How to Add Bates Numbering in PDF with Aspose – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: Yes. Load the document with a `PdfLoadOptions` object that supplies the
      password, then proceed exactly as shown.
    question: Does this work with password‑protected PDFs?
  - answer: Create multiple `BatesNumberingStamp` instances, configure each with its
      own `Prefix`, and apply them only to the appropriate page ranges.
    question: What if I need different prefixes per case?
  - answer: 'Aspose.Pdf offers a 30‑day trial. For production use you’ll need a license,
      but the API surface remains identical. --- ## Conclusion We’ve just covered
      **how to add bates numbering** to any PDF using Aspose.Pdf, demonstrated how
      to **add bates numbers pdf** in a clean, repeatable fashion, and showed'
    question: Is the library free?
  type: FAQPage
tags:
- Aspose.Pdf
- Bates numbering
- PDF automation
title: Hoe Bates‑nummering toe te voegen aan PDF met Aspose – Stapsgewijze gids
url: /nl/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-aspose-step-by-step-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Bates-nummering toe te voegen aan PDF met Aspose – Stapsgewijze gids

Heb je je ooit afgevraagd **hoe je bates-nummering** aan een juridisch document kunt toevoegen zonder uren in een GUI te besteden? Je bent niet de enige. In veel advocatenkantoren, overheidsinstanties en zelfs grote ondernemingen is het elke dag stempelen van elke pagina met een unieke identifier een routine—maar één regel C# kan het een fluitje van een cent maken.

In deze tutorial lopen we een volledig, uitvoerbaar voorbeeld door dat je precies laat zien **hoe je bates-nummering** kunt toevoegen met de Aspose.Pdf-bibliotheek. Aan het einde weet je ook hoe je **bates-nummers pdf** bestanden kunt **stempel aan elke pagina toevoegen** met slechts een paar regels code. Geen magie, alleen duidelijke redenering en praktische tips.

## Wat je zult leren

- Laad een bestaande PDF met Aspose.Pdf.
- Maak een `BatesNumberingStamp` en pas het uiterlijk aan.
- Loop door elke pagina en **stempel aan elke pagina toevoegen** automatisch.
- Sla het resultaat op als een nieuwe PDF die op elk blad een professioneel Bates-nummer bevat.

### Vereisten

- .NET 6.0 of later (de code werkt ook op .NET Framework 4.7+).
- Een geldige Aspose.Pdf for .NET-licentie (of een tijdelijke evaluatiesleutel).
- Een origineel PDF‑bestand dat je wilt nummeren (we noemen het `Original.pdf`).

Als je aan deze drie punten voldoet, ben je klaar om te beginnen.

---

## Stap 1: Stel je project in en installeer Aspose.Pdf

Maak eerst een nieuw console‑project aan (of voeg de code toe aan een bestaand project). Installeer vervolgens het NuGet‑pakket:

```bash
dotnet add package Aspose.Pdf
```

> **Pro tip:** Als je op een bedrijfsnetwerk zit, zorg er dan voor dat je NuGet‑bron is geconfigureerd om `https://www.nuget.org` te bereiken.

## Stap 2: Laad het bron‑PDF‑document

Een PDF laden is net zo eenvoudig als Aspose naar het bestandspad wijzen. De `Document`‑klasse vertegenwoordigt het volledige bestand.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the source PDF (replace the path with your own)
var document = new Document(@"C:\Temp\Original.pdf");

// Quick sanity check – how many pages are we dealing with?
Console.WriteLine($"Document contains {document.Pages.Count} pages.");
```

Waarom loggen we het aantal pagina's? Omdat Bates‑nummering opeenvolgend moet zijn over *alle* pagina's, en het is prettig om te controleren dat je niet per ongeluk een ander bestand laadt.

## Stap 3: Maak een Bates‑nummeringstempel

Het hart van de bewerking is de `BatesNumberingStamp`. Hiermee kun je een prefix, scheidingsteken, cijferopvulling definiëren en zelfs aangeven of de stempel moet worden behandeld als een *artifact* (d.w.z. onzichtbaar voor tekst‑extractietools).

```csharp
var batesStamp = new BatesNumberingStamp
{
    // Starting number – change this to whatever your workflow requires
    StartingNumber = 1000,

    // A human‑readable prefix, often a case or project code
    Prefix = "ABC-",

    // Separator between the running number and the total page count
    Separator = "/",

    // Pad the number with leading zeros to a fixed width (5 digits here)
    NumberOfDigits = 5,

    // Mark the stamp as an artifact so it won’t be indexed by search
    Artifact = true
};
```

**Waarom deze instellingen?**  
- `StartingNumber = 1000` bootst een typisch juridisch dossier na dat al een achterstand heeft.  
- `NumberOfDigits = 5` zorgt ervoor dat nummers zoals `01000`, `01001`, enz. netjes uitgelijnd zijn.  
- `Artifact = true` is essentieel wanneer de PDF wordt ingevoerd in OCR‑ of e‑discovery‑pijplijnen; de nummers blijven zichtbaar voor mensen maar worden genegeerd door tekst‑zoekmachines.

## Stap 4: Voeg de stempel toe aan elke pagina

Nu lopen we door `document.Pages` en passen we dezelfde stempel toe op elke pagina. Aspose verhoogt het nummer automatisch voor je.

```csharp
foreach (Page page in document.Pages)
{
    // The AddStamp method clones the stamp for the current page,
    // updates the running number, and positions it at the default location.
    page.AddStamp(batesStamp);
}
```

> **Veelgestelde vraag:** *Kan ik bepalen waar de stempel verschijnt?*  
> Absoluut. De `BatesNumberingStamp` erft van `Stamp`, dus je kunt eigenschappen zoals `HorizontalAlignment`, `VerticalAlignment`, `XIndent` en `YIndent` vóór de lus instellen. Voor de beknoptheid blijven we bij de standaard rechtsonder‑hoek.

## Stap 5: Sla de aangepaste PDF op

Sla tenslotte de wijzigingen op. Je kunt het originele bestand overschrijven of naar een nieuwe locatie schrijven—hier behouden we beide kopieën.

```csharp
// Save the new PDF with Bates numbers
document.Save(@"C:\Temp\BatesNumbered.pdf");

// Inform the user
Console.WriteLine("Bates numbering added successfully!");
```

Wanneer je `BatesNumbered.pdf` opent, zal elke pagina een stempel tonen die lijkt op:

```
ABC-01000/00123
ABC-01001/00123
…
ABC-01122/00123
```

waar `00123` het totale aantal pagina's is, en de prefix `ABC-` constant blijft.

---

## Volledig werkend voorbeeld

Kopieer het volledige blok hieronder naar een nieuw `Program.cs`‑bestand en voer het uit. Pas de bestandspaden aan op jouw omgeving.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            var srcPath = @"C:\Temp\Original.pdf";
            var document = new Document(srcPath);
            Console.WriteLine($"Loaded '{srcPath}' with {document.Pages.Count} pages.");

            // 2️⃣ Configure the Bates numbering stamp
            var batesStamp = new BatesNumberingStamp
            {
                StartingNumber = 1000,
                Prefix = "ABC-",
                Separator = "/",
                NumberOfDigits = 5,
                Artifact = true,
                // Optional: change alignment if you need a different location
                // HorizontalAlignment = HorizontalAlignment.Left,
                // VerticalAlignment = VerticalAlignment.Top,
                // XIndent = 20,
                // YIndent = 20
            };

            // 3️⃣ Apply the stamp to every page
            foreach (Page page in document.Pages)
            {
                page.AddStamp(batesStamp);
            }

            // 4️⃣ Save the new PDF
            var outPath = @"C:\Temp\BatesNumbered.pdf";
            document.Save(outPath);
            Console.WriteLine($"Saved Bates‑numbered PDF to '{outPath}'.");
        }
    }
}
```

**Verwachte uitvoer in de console:** 

```
Loaded 'C:\Temp\Original.pdf' with 12 pages.
Saved Bates-numbered PDF to 'C:\Temp\BatesNumbered.pdf'.
```

Open het opgeslagen bestand en je ziet de opeenvolgende nummers op elke pagina—precies wat je zou verwachten wanneer je **bates-nummers pdf toevoegt**.

## Geavanceerde aanpassingen (optioneel)

| Doel | Hoe te bereiken |
|------|-------------------|
| **Verander stempelkleur** | Stel `batesStamp.Color = Color.FromRgb(255, 0, 0);` vóór de lus in. |
| **Plaats stempel in de header** | Pas `HorizontalAlignment` en `VerticalAlignment` eigenschappen aan zoals getoond in de gecommentarieerde code. |
| **Sla bepaalde pagina's over** | Voeg een `if (page.Number % 2 == 0) continue;` voorwaarde toe binnen de `foreach`. |
| **Gebruik een aangepast lettertype** | Wijs `batesStamp.Font = FontRepository.FindFont("Arial");` toe. |
| **Maak de stempel zichtbaar voor OCR** | Stel `Artifact = false`. |

Deze variaties laten je **stempel aan elke pagina toevoegen** terwijl de kernlogica overzichtelijk blijft.

## Veelgestelde vragen

**V: Werkt dit met met wachtwoord‑beveiligde PDF's?**  
A: Ja. Laad het document met een `PdfLoadOptions`‑object dat het wachtwoord levert, en ga vervolgens precies zoals getoond verder.

**V: Wat als ik verschillende prefixes per zaak nodig heb?**  
A: Maak meerdere `BatesNumberingStamp`‑instanties, configureer elk met zijn eigen `Prefix`, en pas ze alleen toe op de juiste paginabereiken.

**V: Is de bibliotheek gratis?**  
A: Aspose.Pdf biedt een proefperiode van 30 dagen. Voor productie‑gebruik heb je een licentie nodig, maar de API blijft identiek.

## Conclusie

We hebben zojuist **hoe je bates-nummering** aan elke PDF kunt toevoegen met Aspose.Pdf behandeld, laten zien hoe je **bates-nummers pdf** op een schone, herhaalbare manier kunt toevoegen, en de eenvoudigste manier getoond om **stempel aan elke pagina toe te voegen** met één enkele lus. De code is volledig zelfstandig, draait in seconden, en kan zonder aanpassing in grotere document‑verwerkingspijplijnen worden geïntegreerd.

Klaar voor de volgende uitdaging? Probeer een voorblad te genereren dat het Bates‑bereik weergeeft, of embed een QR‑code naast elke stempel. De mogelijkheden zijn eindeloos, en hetzelfde patroon dat je vandaag hebt geleerd, zal je goed van pas komen waar je PDF‑metadata moet automatiseren.

Als je deze gids nuttig vond, deel hem, laat een reactie achter, of bekijk onze andere tutorials over PDF‑samenvoegen, watermerken en digitale handtekeningen. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe paginastempels toe te voegen in PDF's met Aspose.PDF voor .NET: Een volledige gids](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Hoe paginanummerstempels toe te voegen in PDF's met Aspose.PDF voor .NET | Watermerken & Achtergronden](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [Hoe paginanummers toe te voegen en aan te passen in PDF's met Aspose.PDF voor .NET | Documentmanipulatiegids](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}