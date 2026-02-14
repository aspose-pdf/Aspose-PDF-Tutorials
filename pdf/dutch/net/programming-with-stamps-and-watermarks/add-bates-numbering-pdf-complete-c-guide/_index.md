---
category: general
date: 2026-02-14
description: Voeg moeiteloos Bates‑nummering toe aan je PDF‑documenten. Leer hoe je
  paginanummers in de voettekst en opeenvolgende nummers aan een PDF kunt toevoegen
  met Aspose.Pdf in enkele minuten.
draft: false
keywords:
- add bates numbering pdf
- add footer page numbers
- how to add bates numbers
- add sequential numbers pdf
language: nl
og_description: Voeg snel Bates-nummers toe aan PDF. Deze gids laat zien hoe je voettekst‑paginanummers
  en opeenvolgende nummers aan een PDF toevoegt met Aspose.Pdf, inclusief volledige
  code en tips.
og_title: Bates‑nummering toevoegen aan PDF – Stapsgewijze C#‑tutorial
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Bates-nummering toevoegen aan PDF – Complete C#-gids
url: /nl/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates-nummers toevoegen aan PDF – Complete C#-gids

Heb je ooit **Bates-nummers toevoegen PDF** bestanden nodig gehad, maar wist je niet waar je moest beginnen? Je bent niet de enige. Juridische teams, auditors en iedereen die met grote documentensets werkt, vragen voortdurend: “Hoe voeg ik Bates-nummers toe zonder de lay-out te breken?” Het goede nieuws is dat je met Aspose.Pdf voor .NET die nummers kunt injecteren als een eenvoudige voettekst—geen handmatige bewerking nodig.

In deze tutorial lopen we een praktische, end‑to‑end‑oplossing door die niet alleen **voettekst paginanummers toevoegt**, maar je ook laat **sequentiële nummers PDF** bestanden toevoegen met een aangepast voorvoegsel, lettergrootte en uitlijning. Aan het einde heb je een kant‑klaar C#‑programma, een duidelijk begrip van waarom elke instelling belangrijk is, en een paar pro‑tips om de meest voorkomende valkuilen te vermijden.

## Wat je zult leren

- Hoe een bestaande PDF te laden en voor te bereiden op Bates-nummering.  
- Welke **BatesNumberingOptions**‑eigenschappen uiterlijk en plaatsing regelen.  
- Hoe nummering toe te passen op elke pagina in één oproep.  
- Manieren om het voorvoegsel, startnummer en marges aan te passen voor verschillende juridische formaten.  
- Afhandeling van randgevallen—wat te doen met versleutelde PDF's of documenten die al voetteksten bevatten.  

**Prerequisites**: .NET 6+ (of .NET Framework 4.7+), een recente versie van Aspose.Pdf (het voorbeeld gebruikt 23.10), en een invoer‑PDF waarvan je de rechten hebt om te wijzigen. Er zijn geen andere externe bibliotheken nodig.

---

## Stap 1 – Laad de PDF die je wilt nummeren

Het eerste wat we doen is een `Document`‑instantie maken die naar het bronbestand wijst. Het gebruik van het `using var`‑patroon zorgt ervoor dat de bestands­handle automatisch wordt vrijgegeven.

```csharp
using Aspose.Pdf;

// Replace with the path to your source PDF
using var doc = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Why this matters:** Aspose.Pdf leest de volledige PDF‑structuur in het geheugen, waardoor we pagina's, annotaties en metadata kunnen manipuleren zonder het oorspronkelijke bestand op schijf aan te raken. Als de PDF met een wachtwoord is beveiligd, kun je het wachtwoord doorgeven aan de constructor—zie de “Encrypted PDFs”‑opmerking aan het einde.

---

## Stap 2 – Definieer je Bates‑nummeringsopties

Bates‑nummers zijn in wezen paginavoetteksten met een configureerbaar voorvoegsel en een opeenvolgende teller. De `BatesNumberingOptions`‑klasse stelt je in staat elk visueel aspect nauwkeurig af te stemmen.

```csharp
var batesOptions = new BatesNumberingOptions
{
    // The text that will appear before the numeric part
    Prefix = "ABC-",

    // Starting number; the library will increment this automatically
    StartNumber = 1000,

    // Font size of the footer text (points)
    FontSize = 12,

    // Align the number to the right side of the page
    HorizontalAlignment = HorizontalAlignment.Right,

    // Place the number at the bottom of the page
    VerticalAlignment = VerticalAlignment.Bottom,

    // Margins: left, top, right, bottom (in points)
    Margin = new MarginInfo(0, 20, 0, 0)
};
```

### Snelle tip

- **Prefix**: Gebruik een korte, unieke identifier (bijv. zaaknummer) om de voettekst leesbaar te houden.  
- **StartNumber**: Juridische kantoren beginnen vaak bij `1` of een aangepaste offset; kies wat past bij je archiveringssysteem.  
- **Margins**: De ondermarge van `20` punten houdt de tekst vrij van voetnoten of handtekeningen die al dicht bij de paginarand kunnen staan.

---

## Stap 3 – Pas de nummering toe op alle pagina's

Met de opties geconfigureerd is de daadwerkelijke injectie een één‑regel‑code. Aspose.Pdf behandelt paginering, werkt bestaande content‑streams bij en respecteert automatisch de paginaverdraaiing.

```csharp
doc.Pages.AddBatesNumbering(batesOptions);
```

> **What’s happening under the hood?** De bibliotheek doorloopt elk `Page`‑object, maakt een `TextFragment` aan die het voorvoegsel en de huidige teller bevat, en tekent deze vervolgens met behulp van het coördinatensysteem van de pagina. Omdat we `HorizontalAlignment.Right` en `VerticalAlignment.Bottom` hebben ingesteld, plakt de tekst in de rechter‑onderhoek, ongeacht de paginagrootte.

---

## Stap 4 – Sla de gewijzigde PDF op

Schrijf tenslotte het resultaat naar een nieuw bestand. Het overschrijven van het origineel is mogelijk, maar een kopie bewaren helpt bij versiebeheer.

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

Als je de oorspronkelijke metadata (auteur, aanmaakdatum) wilt behouden, kopieert Aspose.Pdf deze standaard. Je kunt ook een `SaveOptions`‑object opgeven voor PDF/A‑naleving of compressie.

---

## Volledig werkend voorbeeld

Hieronder staat het volledige, kant‑klaar programma. Plak het in een console‑app‑project, pas de bestandspaden aan, en druk op **F5**.

```csharp
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using var doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Configure Bates numbering options
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC-",
            StartNumber = 1000,
            FontSize = 12,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(0, 20, 0, 0)
        };

        // 3️⃣ Apply numbering to every page
        doc.Pages.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the output PDF
        doc.Save("YOUR_DIRECTORY/output.pdf");

        System.Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Expected result:** Elke pagina van `output.pdf` toont nu een voettekst zoals `ABC-1000`, `ABC-1001`, … verankerd in de rechter‑onderhoek. Open het bestand in een PDF‑lezer om te verifiëren.

---

## Omgaan met veelvoorkomende variaties

### Alleen voettekst paginanummers toevoegen

Als je alleen eenvoudige paginanummers zonder voorvoegsel nodig hebt, stel dan `Prefix = ""` in en pas eventueel de marge aan om botsingen met bestaande voetteksten te voorkomen.

```csharp
batesOptions.Prefix = "";
batesOptions.StartNumber = 1; // classic page numbering
```

### Een andere uitlijning gebruiken

Juridische documenten vereisen soms dat het nummer gecentreerd onderaan staat. Verander de uitlijning:

```csharp
batesOptions.HorizontalAlignment = HorizontalAlignment.Center;
```

### Omgaan met versleutelde PDF's

Wanneer de bron‑PDF met een wachtwoord is beveiligd, geef je het wachtwoord als volgt op:

```csharp
using var doc = new Document("secure.pdf", new LoadOptions { Password = "mySecret" });
```

De rest van de workflow blijft identiek.

### Bestaande voetteksten overslaan

Als een document al een voettekst bevat die je niet wilt overschrijven, kun je een aangepast tekenreeks voorvoegen die het nieuwe nummer onderscheidt, of je kunt handmatig pagina's doorlopen en alleen een `TextFragment` toevoegen waar de voettekst ontbreekt. De `Page`‑klasse van de bibliotheek biedt de collecties `Annotations` en `Contents` voor fijnmazige controle.

---

## Pro‑tips & valkuilen

- **Avoid clipping**: Zeer kleine ondermarges kunnen ervoor zorgen dat de tekst op printers wordt afgekapt. Test met een fysieke afdruk als je harde kopieën gaat verspreiden.  
- **Performance**: Het toevoegen van Bates‑nummers aan een PDF van 500 pagina's duurt minder dan een seconde op een moderne laptop, maar grote batches profiteren van parallelle verwerking—onthoud wel dat `Document` niet thread‑safe is, dus elke thread heeft een eigen instantie nodig.  
- **Version compatibility**: De code werkt met Aspose.Pdf 23.10 en nieuwer. Als je een oudere versie gebruikt, zijn de eigenschapsnamen hetzelfde, maar kan de `MarginInfo`‑constructor `float`‑argumenten vereisen.  
- **Legal compliance**: Sommige rechtsgebieden eisen dat het Bates‑nummer op een specifieke locatie wordt geplaatst (bijv. onder‑links). Pas de `HorizontalAlignment` dienovereenkomstig aan.

---

## Conclusie

We hebben zojuist laten zien hoe je **Bates-nummers toevoegen PDF** bestanden kunt gebruiken met Aspose.Pdf voor .NET, waarbij we alles behandelen van het laden van het document tot het opslaan van de uiteindelijke versie met een nette voettekst. Door een handvol eigenschappen aan te passen kun je ook **voettekst paginanummers toevoegen**, **sequentiële nummers PDF toevoegen**, of het uiterlijk aanpassen om aan elke juridische standaard te voldoen.

Klaar voor de volgende stap? Probeer deze techniek te combineren met OCR‑tekstekstractie om doorzoekbare trefwoorden naast je Bates‑nummers in te voegen, of automatiseer het proces voor volledige mappen met `Directory.GetFiles`. De mogelijkheden zijn eindeloos, en de basis die je nu hebt maakt die uitbreidingen moeiteloos.

Veel programmeerplezier, en moge je PDF's altijd perfect genummerd zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}