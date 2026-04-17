---
category: general
date: 2026-03-27
description: Voeg snel Bates‑nummering toe in C#. Leer hoe je aangepaste paginanummers,
  opeenvolgende paginanummers en aangepaste nummers aan Word‑documenten kunt toevoegen.
draft: false
keywords:
- add bates numbering
- how to add bates
- add custom page numbers
- add sequential page numbers
- add custom numbers
language: nl
og_description: Voeg Bates‑nummering toe in C# met een duidelijk voorbeeld. Deze gids
  laat zien hoe je aangepaste paginanummers kunt toevoegen, opeenvolgende paginanummers
  kunt toevoegen, en meer.
og_title: Bates-nummering toevoegen in C# – Complete tutorial
tags:
- C#
- Document Processing
- Bates Numbering
title: Bates-nummering toevoegen in C# – Stapsgewijze handleiding
url: /nl/net/programming-with-pdf-pages/add-bates-numbering-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates‑nummering toevoegen in C# – Stapsgewijze handleiding

Heb je je ooit afgevraagd hoe je **bates‑nummering** aan een Word‑document kunt toevoegen zonder je haar uit te trekken? Je bent niet de enige. In veel juridische of compliance‑projecten moet elke pagina een unieke identifier hebben, en dit handmatig doen is een nachtmerrie.  

In deze tutorial lopen we een volledig, uitvoerbaar voorbeeld door dat **bates‑nummering toevoegt**, je **laat zien hoe je bates toevoegt** in een paar regels, en zelfs behandelt hoe je **aangepaste paginanummers** en **opeenvolgende paginanummers** kunt toevoegen wanneer dat nodig is. Aan het einde heb je een .docx‑bestand gestempeld met de nummers die jij kiest—zonder derde‑partij tools.

## Wat je zult leren

- Een DOCX‑bestand laden met de Aspose.Words for .NET API (of een andere compatibele bibliotheek).  
- **Aangepaste nummers** configureren, zoals een prefix, een startwaarde en een lettergrootte.  
- De nummering toepassen op elke pagina in één oproep.  
- Het resultaat opslaan en verifiëren dat de nummers verschijnen zoals verwacht.  

Ervaring met Bates‑nummering is niet vereist; alleen een basis C#‑omgeving en een kopie van het bron‑document. Laten we beginnen.

## Voorwaarden

- .NET 6+ (de code werkt zowel op .NET Core als .NET Framework).  
- Aspose.Words for .NET geïnstalleerd via NuGet (`Install-Package Aspose.Words`).  
- Een Word‑document met de naam `input.docx` geplaatst in een map die je kunt refereren (`YOUR_DIRECTORY`).  
- Visual Studio, VS Code, of een andere C#‑IDE naar keuze.

> **Pro tip:** Als je een andere bibliotheek gebruikt (bijv. Open XML SDK), blijven de concepten hetzelfde—vervang alleen de API‑aanroepen.

## Stap 1: Het bron‑document laden

Eerst moeten we het Word‑bestand in het geheugen laden.

```csharp
using Aspose.Words;

// Step 1: Load the source document
Document document = new Document("YOUR_DIRECTORY/input.docx");
```

*Waarom dit belangrijk is:* Het laden van het bestand creëert een `Document`‑object dat je toegang geeft tot pagina's, secties en de low‑level node‑boom. Zonder dit kun je geen nummering toevoegen.

## Stap 2: Bates‑nummeringsopties configureren

Nu definiëren we precies hoe de nummers eruit moeten zien. Hier kun je **aangepaste paginanummers** of **opeenvolgende paginanummers** toevoegen.

```csharp
// Step 2: Define Bates numbering options (prefix, start number, font size)
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Prefix that appears before every number, e.g., "ABC"
    Prefix = "ABC",
    // The first number in the sequence; change to 1 if you prefer
    Start = 1000,
    // Font size in points; 9 works well for most legal docs
    FontSize = 9
};
```

*Waarom dit belangrijk is:* De `Prefix` laat je **aangepaste nummers** toevoegen, zoals een zaak‑ID, terwijl `Start` de initiële teller bepaalt. Het aanpassen van `FontSize` zorgt ervoor dat de nummers de paginamarges niet overlappen.

## Stap 3: Bates‑nummering toepassen op elke pagina

Met de opties klaar, vertellen we de bibliotheek elke pagina te stempelen.

```csharp
// Step 3: Apply Bates numbering to all pages of the document
document.Pages.AddBatesNumbering(batesOptions);
```

*Waarom dit belangrijk is:* De `AddBatesNumbering`‑methode doorloopt de interne paginacollectie en injecteert een tekstvak in de rechter‑onderhoek (de standaardlocatie). Het is de kern van **hoe je bates toevoegt** zonder zelf een lus te schrijven.

## Stap 4: Het bijgewerkte document opslaan

Tot slot schrijven we het aangepaste bestand terug naar de schijf.

```csharp
// Step 4: Save the updated document
document.Save("YOUR_DIRECTORY/output.docx");
```

*Waarom dit belangrijk is:* Opslaan creëert een nieuw `output.docx` dat je kunt openen in Word, LibreOffice of een andere viewer om te bevestigen dat de nummers verschijnen.

## Verwacht resultaat

Open `output.docx`. Elke pagina zou iets moeten tonen als:

```
ABC‑1000   (on page 1)
ABC‑1001   (on page 2)
ABC‑1002   (on page 3)
...
```

Als je de afdrukvoorbeeld van het document opent, zie je de nummers in de rechter‑onderhoek, met de door jou ingestelde lettergrootte.

## Randgevallen & Variaties

| Situatie | Wat te wijzigen | Waarom |
|-----------|----------------|-----|
| **Geen prefix nodig** | `Prefix = string.Empty` | Verwijdert het “ABC‑”‑gedeelte, laat alleen de numerieke reeks over. |
| **Start bij 1** | `Start = 1` | Handig voor eenvoudige **opeenvolgende paginanummers** zonder een aangepaste prefix. |
| **Grote documenten (>10.000 pagina's)** | Verhoog `FontSize` of pas `Location` aan (gebruik overloads van `AddBatesNumbering`) | Voorkomt overlapping met voetteksten of kopteksten. |
| **Alleen‑lezen bronbestand** | Open met `LoadOptions` die schrijfrechten toestaan, of kopieer het bestand eerst | Anders zal `document.Save` een uitzondering werpen. |
| **Andere plaatsing** | Gebruik `batesOptions.Position = BatesNumberingPosition.TopLeft` (of een andere enum) | Sommige kantoren eisen nummers bovenaan de pagina. |

> **Opmerking:** Niet alle bibliotheken bieden een `BatesNumberingOptions`‑klasse. Met Open XML SDK zou je handmatig een `TextBox` invoegen—hetzelfde principe, meer code.

## Volledig werkend voorbeeld

Hier is het volledige programma in één stuk. Kopieer‑en‑plak het in een console‑applicatie en voer uit.

```csharp
using System;
using Aspose.Words;

class Program
{
    static void Main()
    {
        // Load the source document
        Document document = new Document("YOUR_DIRECTORY/input.docx");

        // Define Bates numbering options
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC",      // custom prefix
            Start = 1000,        // starting number
            FontSize = 9         // font size in points
        };

        // Apply numbering to every page
        document.Pages.AddBatesNumbering(batesOptions);

        // Save the result
        document.Save("YOUR_DIRECTORY/output.docx");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

Voer het programma uit, open `output.docx`, en je ziet de nummering precies op de plek die je verwachtte. 🎉

## Veelgestelde vragen

**V: Kan ik de kleur van de nummers wijzigen?**  
A: Ja. Na het aanroepen van `AddBatesNumbering` kun je de gegenereerde `Shape`‑objecten ophalen en hun `FillColor`‑eigenschap instellen.

**V: Wat als ik de nummers aan de linkerkant in plaats van rechts wil?**  
A: Gebruik `batesOptions.Position = BatesNumberingPosition.BottomLeft` (of `TopLeft`, `TopRight`). De API ondersteunt alle vier hoeken.

**V: Werkt dit ook met PDF‑output?**  
A: Absoluut. Na het toevoegen van de nummering, roep `document.Save("output.pdf")` aan. De nummers worden in de PDF gerenderd net zoals in Word.

## Conclusie

Je weet nu **hoe je bates‑nummering toevoegt** aan een Word‑bestand met C#. De tutorial behandelde het laden van een document, het configureren van **aangepaste nummers**, het toepassen van **opeenvolgende paginanummers**, en het opslaan van het eindresultaat. Met het volledige code‑voorbeeld kun je dit in elk project drop‑en en direct documenten stempelen.

Klaar voor de volgende uitdaging? Probeer dit te combineren met een batch‑processor die door een map met bestanden loopt, of verken **aangepaste paginanummers** in de kop‑ of voettekst voor een meer gepolijste uitstraling. Hoe dan ook, je hebt nu een solide basis voor elke legal‑tech of compliance‑automatiseringstaak.

Heb je vragen of een cool use‑case? Laat een reactie achter hieronder, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}