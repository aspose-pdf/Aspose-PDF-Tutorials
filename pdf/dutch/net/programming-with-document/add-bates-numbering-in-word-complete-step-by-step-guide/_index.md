---
category: general
date: 2026-06-21
description: Voeg snel Bates-nummering toe in Word. Leer hoe je Bates toevoegt, Bates-nummering
  toepast voor juridische documenten en nummering automatiseert met C#.
draft: false
keywords:
- add bates numbering
- how to add bates
- bates numbering in word
- bates numbering for legal
- apply bates numbering
language: nl
og_description: Voeg Bates-nummering toe in Word met C#. Deze gids laat zien hoe je
  Bates toevoegt, Bates-nummering toepast voor juridische documenten en het proces
  automatiseert.
og_title: Batesnummering toevoegen in Word – Volledige programmeerhandleiding
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  headline: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  name: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: '| Page | Bates Number | |------|--------------| | 1 | ABC-1000 | | 2 |
      ABC-1001 | | … | … | | N | ABC‑(1000 + N‑1) |'
  - name: What if the document already contains page numbers?
    text: The `AddBatesNumbering` method will **not** overwrite existing page number
      fields; it simply adds a new field. If you want to replace the existing numbers,
      remove them first or set `batesOptions.Position` to the same location as the
      current page numbers.
  - name: Can I skip pages (e.g., exclude a cover page)?
    text: 'Yes. Use the overload that accepts a `PageRange`:'
  - name: How do I change the numbering format (Roman numerals, letters)?
    text: 'The `BatesNumberingOptions` class supports a `NumberFormat` property:'
  - name: What about performance on huge files?
    text: Loading a 2‑GB Word file can consume a lot of RAM. To mitigate, process
      the document in chunks using the `DocumentSplitter` utility, apply Bates numbering
      to each chunk, then merge the parts back together. This pattern keeps memory
      usage under control while still letting you **apply bates numbering*
  type: HowTo
tags:
- document‑automation
- csharp
- legal‑tech
title: Batesnummering toevoegen in Word – Complete stap‑voor‑stap gids
url: /nl/net/programming-with-document/add-bates-numbering-in-word-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates-nummers toevoegen in Word – Complete Stapsgewijze Gids

Heb je je ooit afgevraagd hoe je Bates-nummers aan een Word‑bestand kunt toevoegen zonder elk nummer handmatig te typen? Je bent niet de enige. Veel advocaten, paralegals en e‑discovery‑specialisten hebben een betrouwbare manier nodig om **Bates-nummers toe te voegen** aan honderden pagina’s, en dit handmatig doen is een nachtmerrie.

In deze tutorial lopen we een nette C#‑oplossing door die **Bates-nummers toepast** op een `.docx`‑bestand, legt uit waarom elke regel belangrijk is, en laat zien hoe je de code kunt aanpassen voor juridische specifieke behoeften. Aan het einde kun je in enkele seconden een perfect genummerd document genereren – zonder extra plug‑ins.

## Wat je gaat leren

- De exacte code die nodig is om **Bates-nummers toe te voegen** aan een Word‑document.
- Hoe de `BatesNumberingOptions`‑klasse werkt en waarom je het voorvoegsel of de startwaarde zou kunnen aanpassen.
- Tips voor het gebruik van deze aanpak op grote zaak‑bestanden, inclusief geheugen‑overwegingen.
- Een snelle opsomming van de vereisten zodat je de oplossing kunt kopiëren‑plakken en vandaag nog kunt uitvoeren.

**Vereisten**  
- .NET 6+ (of .NET Framework 4.7.2+ als je de oudere runtime verkiest).  
- Een referentie naar de Aspose.Words for .NET‑bibliotheek (of een vergelijkbare API die `AddBatesNumbering` exposeert).  
- Basiskennis van C# en Visual Studio (of je favoriete IDE).

Als je hiermee vertrouwd bent, laten we beginnen.

## Stap 1: Het project opzetten en de bibliotheek importeren

Maak eerst een nieuwe console‑app (of integreer in een bestaande service). Voeg vervolgens het Aspose.Words NuGet‑pakket toe:

```bash
dotnet add package Aspose.Words
```

> **Pro tip:** Gebruik de gratis evaluatielicentie voor testen; deze voegt een klein watermerk toe maar werkt verder precies als de volledige versie.

```csharp
using Aspose.Words;
using Aspose.Words.BatesNumbering;
```

Deze `using`‑statements brengen de `Document`‑ en `BatesNumberingOptions`‑klassen in scope, die essentieel zijn voor de **apply bates numbering**‑stap later.

## Stap 2: Het bron‑document laden

Je hebt een Word‑bestand nodig om mee te werken. De code hieronder laadt `input.docx` vanuit een map die je opgeeft. Vervang `"YOUR_DIRECTORY"` door het daadwerkelijke pad op jouw machine.

```csharp
// Step 1: Load the source document
var document = new Document("YOUR_DIRECTORY/input.docx");
```

Waarom eerst het bestand laden? Het `Document`‑object parseert het volledige Word‑pakket in het geheugen, waardoor we kop‑ en voetteksten, paginalay‑out en dergelijke kunnen manipuleren voordat we opslaan. Als het bestand enorm is (bijvoorbeeld 10.000 pagina’s), overweeg dan `LoadOptions` met `LoadFormat.Docx` te gebruiken om secties te streamen in plaats van alles in één keer te laden.

## Stap 3: Bates‑nummeringsopties configureren

Hier gebeurt de magie. Je vertelt de bibliotheek welk voorvoegsel te gebruiken (`"ABC-"` in het voorbeeld) en waar de telling moet beginnen (`1000`). Beide waarden zijn volledig aanpasbaar.

```csharp
// Step 2: Define Bates numbering options (prefix and starting number)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",
    Start = 1000,
    // Optional: set the position, alignment, and font if you need legal‑specific styling
    // Position = BatesNumberingPosition.Footer,
    // Alignment = BatesNumberingAlignment.Right,
    // Font = new Font("Times New Roman", 10, FontStyle.Bold)
};
```

**Waarom een voorvoegsel?** In de juridische praktijk identificeren voorvoegsels vaak de zaak of de producerende partij (`"ABC-"` kan staan voor *Acme Bank Corp.*). Beginnen bij `1000` is gebruikelijk omdat veel kantoren de eerste 999 nummers reserveren voor interne concepten.

Als je **Bates numbering for legal**‑documenten verwerkt, wil je misschien ook `batesOptions.Position` instellen op `Header` of `Footer` en de uitlijning aanpassen aan de rechtbankregels. De bibliotheek ondersteunt deze aanpassingen out‑of‑the‑box.

## Stap 4: Bates‑nummering toepassen op het volledige document

Nu injecteren we daadwerkelijk de nummers. De `AddBatesNumbering`‑methode doorloopt elke pagina, voegt de geformatteerde string in en werkt de interne paginatelling van het document bij.

```csharp
// Step 3: Apply Bates numbering to the entire document
document.AddBatesNumbering(batesOptions);
```

Achter de schermen maakt Aspose.Words een verborgen veld aan op elke pagina dat wordt weergegeven als `ABC-1000`, `ABC-1001`, enzovoort. Omdat het een veld is, kun je later het voorvoegsel of het startnummer wijzigen zonder het hele bestand opnieuw te genereren – handig voor **how to add bates** nadat een discovery‑verzoek verandert.

## Stap 5: Het gewijzigde document opslaan

Schrijf tenslotte de output naar een nieuw bestand. Het origineel ongewijzigd laten is een best practice, vooral bij bewijsmateriaal dat ongerept moet blijven.

```csharp
// Step 4: Save the modified document
document.Save("YOUR_DIRECTORY/output.docx");
```

Je hebt nu `output.docx` met opeenvolgende Bates‑nummers toegevoegd aan elke pagina. Open het in Word en je ziet de nummers precies op de door jou opgegeven plek (standaard in de voettekst). Het bestand kan iets groter worden door de extra velden, maar dat is verwaarloosbaar ten opzichte van de voordelen.

### Verwachte output

| Pagina | Bates‑nummer |
|--------|--------------|
| 1      | ABC-1000     |
| 2      | ABC-1001     |
| …      | …            |
| N      | ABC‑(1000 + N‑1) |

Als je de “Field Codes”‑weergave van het document opent (`Alt+F9` in Word), zie je iets als `{ BATES \* MERGEFORMAT ABC-1000 }` op elke pagina.

## Randgevallen & Veelgestelde Vragen

### Wat als het document al paginanummers bevat?

De `AddBatesNumbering`‑methode **zal** bestaande paginanummer‑velden niet overschrijven; hij voegt simpelweg een nieuw veld toe. Als je de bestaande nummers wilt vervangen, verwijder ze dan eerst of stel `batesOptions.Position` in op dezelfde locatie als de huidige paginanummers.

### Kan ik pagina’s overslaan (bijv. een omslagblad uitsluiten)?

Ja. Gebruik de overload die een `PageRange` accepteert:

```csharp
var range = new PageRange(2, document.PageCount); // start at page 2
document.AddBatesNumbering(batesOptions, range);
```

Dit is handig wanneer je **bates numbering for legal**‑brieven nodig hebt die pas na een titelpagina beginnen.

### Hoe wijzig ik het nummeringsformaat (Romeinse cijfers, letters)?

De `BatesNumberingOptions`‑klasse ondersteunt een `NumberFormat`‑eigenschap:

```csharp
batesOptions.NumberFormat = BatesNumberFormat.RomanUpper;
```

Stel deze in vóór het aanroepen van `AddBatesNumbering`. Deze flexibiliteit helpt wanneer een rechtbank een specifiek stijl vereist.

### Hoe zit het met prestaties bij enorme bestanden?

Het laden van een 2‑GB Word‑bestand kan veel RAM verbruiken. Om dit te beperken, verwerk het document in delen met de `DocumentSplitter`‑utility, pas Bates‑nummering toe op elk deel, en voeg de stukken daarna weer samen. Dit patroon houdt het geheugenverbruik onder controle terwijl je toch **apply bates numbering** efficiënt kunt uitvoeren.

## Volledig Werkend Voorbeeld

Alles bij elkaar, hier is een kant‑klaar console‑programma:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.BatesNumbering;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            var inputPath = @"C:\Docs\input.docx";
            var document = new Document(inputPath);

            // 2️⃣ Define Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                // Optional styling for legal compliance
                Position = BatesNumberingPosition.Footer,
                Alignment = BatesNumberingAlignment.Right,
                Font = new Font("Times New Roman", 9, FontStyle.Bold)
            };

            // 3️⃣ Apply Bates numbering across all pages
            document.AddBatesNumbering(batesOptions);

            // 4️⃣ Save the result
            var outputPath = @"C:\Docs\output.docx";
            document.Save(outputPath);

            Console.WriteLine($"✅ Bates numbering applied! Saved to {outputPath}");
        }
    }
}
```

Voer het programma uit, open `output.docx`, en je ziet een nette reeks nummers klaar voor indiening, discovery of gerechtelijke indiening.

## Conclusie

Je weet nu precies **how to add Bates** aan een Word‑document met C#. De stappen – laden, configureren, toepassen en opslaan – zijn eenvoudig, maar toch flexibel genoeg om **Bates numbering for legal**‑workflows, aangepaste voorvoegsels en zelfs grootschalige batchverwerking te ondersteunen.

Als je dit verder wilt uitbreiden, overweeg dan:

- De code integreren in een web‑API zodat collega's bestanden kunnen uploaden en genummerde PDF’s direct ontvangen.  
- Foutafhandeling toevoegen voor ontbrekende bestanden of machtigingsproblemen (een snelle `try/catch` rond `Document.Load`).  
- Andere Aspose.Words‑functies verkennen, zoals watermerken of redactie, voor een volledige e‑discovery‑toolkit.

Voel je vrij om te experimenteren met verschillende voorvoegsels, startnummers, of zelfs meerdere nummeringsschema’s in hetzelfde document te combineren. De wereld van **apply bates numbering** is verrassend veelzijdig zodra je de kernlogica onder de knie hebt.

Heb je vragen of een lastig scenario? Laat een reactie achter hieronder, en we lossen het samen op. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Apply Numbering Style in Heading of PDF using Java](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/french/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}