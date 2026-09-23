---
category: general
date: 2026-03-06
description: Maak een PDF‑document in C# en voeg eenvoudig batesnummers toe. Leer
  hoe je een lege pagina aan een PDF toevoegt, een stempel op een pagina plaatst en
  batesnummering implementeert.
draft: false
keywords:
- create pdf document
- add bates number
- add blank page pdf
- how to add bates numbering
- place stamp on page
language: nl
og_description: Maak een PDF‑document in C# en voeg een batesnummer toe. Deze gids
  laat zien hoe je een lege PDF‑pagina toevoegt, een stempel op de pagina plaatst
  en batesnummering toepast.
og_title: PDF-document maken met Bates-nummering – C#-tutorial
tags:
- Aspose.Pdf
- C#
- PDF automation
title: PDF-document maken met Bates-nummering in C# – Volledige gids
url: /nl/net/programming-with-stamps-and-watermarks/create-pdf-document-with-bates-numbering-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF‑document maken met Bates‑nummering in C#

Heb je ooit een **PDF‑document** moeten maken in C# en je afgevraagd hoe je een Bates‑nummer toevoegt zonder je haar uit te trekken? Je bent niet de enige—advocatenkantoren, rechtbanken en zelfs sommige corporate compliance‑teams staan elke dag voor precies dit vraagstuk. Het goede nieuws? Met een paar regels Aspose.Pdf‑code kun je een gloednieuwe PDF genereren, een lege pagina toevoegen en een correct Bates‑nummer in één soepele flow plaatsen.

In deze tutorial lopen we het volledige proces door: van het opzetten van het project, tot het toevoegen van een lege pagina‑PDF, tot het uitzoeken **hoe je Bates‑nummering toevoegt**, en uiteindelijk **het stempel op de pagina plaatsen** en het resultaat opslaan. Aan het einde heb je een kant‑klaar fragment dat je in elke .NET‑app kunt gebruiken. Geen vage verwijzingen, alleen een compleet, uitvoerbaar voorbeeld.

## Wat je nodig hebt

- **.NET 6+** (of .NET Framework 4.6+ – Aspose.Pdf werkt met beide)
- **Aspose.Pdf for .NET** NuGet‑package (`Install-Package Aspose.Pdf`)
- Een degelijke IDE (Visual Studio, Rider, of VS Code met C#‑extensie)

Dat is alles. Geen extra DLL‑s, geen externe services. Laten we beginnen.

## Stap 1: PDF‑document maken – Initiële setup

Allereerst hebben we een verse `Document`‑object nodig. Beschouw het als het lege canvas waarop alles andere zal leven.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Initialize a new PDF document
Document pdfDocument = new Document();
```

> **Waarom dit belangrijk is:** De `Document`‑klasse is het startpunt voor elke Aspose‑bewerking. Een instantie maken geeft je toegang tot de `Pages`‑collectie, metadata en beveiligingsinstellingen—alle bouwstenen voor een professioneel PDF‑document.

## Stap 2: Lege pagina‑PDF toevoegen

Een PDF zonder pagina's is als een boek zonder bladzijden—tamelijk nutteloos. Het toevoegen van een lege pagina is eenvoudig, en het geeft ons een oppervlak om het Bates‑nummer op te stempelen.

```csharp
// Add a single blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **Pro‑tip:** Als je meerdere pagina's nodig hebt, roep dan `pdfDocument.Pages.Add()` aan in een lus. Elke aanroep retourneert een nieuw `Page`‑object dat je onafhankelijk kunt aanpassen.

## Stap 3: Hoe Bates‑nummering toe te voegen – De TextStamp maken

Nu komt het hart van de zaak: het **Bates‑nummer**. In Aspose.Pdf is het gewoon een `TextStamp` met een speciale artifact‑vlag.

```csharp
// Create a text stamp that will serve as a Bates number
TextStamp batesStamp = new TextStamp("Bates-001")
{
    // Mark the stamp as a Bates‑numbering artifact (helps PDF viewers treat it specially)
    Artifact = ArtifactType.BatesNumbering,
    // Align the stamp to the bottom‑right corner of the page
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Add a small margin so the number isn’t glued to the edge
    Margin = new Margin { Bottom = 10, Right = 10 }
};
```

> **Waarom we `Artifact` instellen:** Sommige PDF‑readers tonen Bates‑nummers als doorzoekbare metadata. Het markeren van het stempel als een `BatesNumbering`‑artifact zorgt ervoor dat downstream‑tools het automatisch herkennen.

## Stap 4: Stempel op pagina plaatsen

Met het stempel klaar, **plaatsen we het stempel op de pagina**. Dit is de stap waarin het visuele nummer daadwerkelijk in de PDF verschijnt.

```csharp
// Add the Bates number stamp to the previously created page
page.AddStamp(batesStamp);
```

> **Randgeval:** Als je wilt dat het nummer op elke pagina oploopt, doorloop je `pdfDocument.Pages` en werk je `batesStamp.Value` bij voordat je `AddStamp` aanroept. Het voorbeeld hier houdt het simpel met een statisch “Bates‑001”.

## Stap 5: Opslaan en resultaat verifiëren

Tot slot slaan we de PDF op schijf op. Kies een map waarin je schrijfrechten hebt; anders krijg je een `UnauthorizedAccessException`.

```csharp
// Save the stamped PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/BatesStamped.pdf");
```

Wanneer je `BatesStamped.pdf` opent in een viewer, zou je een klein “Bates‑001” netjes in de rechter‑onderhoek van de lege pagina moeten zien.

> **Verwachte output:**  
> ![PDF met Bates‑nummerstempel](image-placeholder.png "PDF met Bates‑nummerstempel")  
> *Alt‑tekst: PDF met Bates‑nummerstempel in de rechter‑onderhoek.*

Als het nummer niet verschijnt, controleer dan de marge‑waarden en zorg dat de paginagrootte niet te klein is (standaard A4 werkt prima). Controleer ook of de `Artifact`‑vlag niet wordt verwijderd door eventuele post‑processing‑tools.

## Volledig werkend voorbeeld

Hieronder staat het complete, kant‑en‑klaar programma. Het bevat alle `using`‑directieven en commentaren om je georiënteerd te houden.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize a new PDF document
        Document pdfDocument = new Document();

        // 2️⃣ Add a blank page – this is where we’ll put the Bates number
        Page page = pdfDocument.Pages.Add();

        // 3️⃣ Create a TextStamp for the Bates number
        TextStamp batesStamp = new TextStamp("Bates-001")
        {
            Artifact = ArtifactType.BatesNumbering,          // Marks it as a Bates‑numbering artifact
            HorizontalAlignment = HorizontalAlignment.Right, // Align right
            VerticalAlignment = VerticalAlignment.Bottom,    // Align bottom
            Margin = new Margin { Bottom = 10, Right = 10 }  // Small margin from edges
        };

        // 4️⃣ Place the stamp on the page
        page.AddStamp(batesStamp);

        // 5️⃣ Save the PDF to disk
        string outputPath = @"C:\Temp\BatesStamped.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"PDF created successfully: {outputPath}");
    }
}
```

Voer het programma uit, open de PDF, en je ziet het Bates‑nummer precies op de plek waar we het hebben geplaatst. 🎉

## Veelvoorkomende variaties & valkuilen

| Scenario | Wat te wijzigen | Waarom |
|----------|----------------|--------|
| **Meerdere pagina's, oplopende nummers** | Doorloop `pdfDocument.Pages`, stel `batesStamp.Value = $"Bates-{i:D3}"` in vóór `AddStamp` | Geeft elke pagina een uniek identificatienummer, gebruikelijk voor juridische bundels |
| **Andere plaatsing (boven‑links)** | Verander `HorizontalAlignment = HorizontalAlignment.Left` en `VerticalAlignment = VerticalAlignment.Top` | Sommige organisaties geven de voorkeur aan het nummer in de header in plaats van de footer |
| **Aangepast lettertype of kleur** | Stel `batesStamp.TextState.Font = FontRepository.FindFont("Arial"); batesStamp.TextState.FontSize = 12; batesStamp.TextState.ForegroundColor = Color.Red;` in | Verbetert leesbaarheid of voldoet aan huisstijlrichtlijnen |
| **Een bestaande PDF als achtergrond toevoegen** | Laad de bron‑PDF met `Document src = new Document("source.pdf"); pdfDocument.Pages.Add(src.Pages[1]);` | Handig wanneer je over een vooraf gegenereerd formulier moet stempelen |

## Afronding

We hebben zojuist laten zien hoe je **PDF‑document** maakt, **een lege pagina‑pdf** toevoegt, en **Bates‑nummer** toepast met Aspose.Pdf voor .NET, vervolgens **stempel op pagina** plaatst en het bestand opslaat. De code is bewust compact gehouden zodat je hem kunt aanpassen aan grotere workflows—of je nu tientallen bestanden batch‑verwerkt of integreert in een webservice.

Als je klaar bent om verder te gaan, overweeg dan:

- Het automatiseren van de increment‑logica voor grote dossiers.
- Het embedden van de PDF‑generatie in een ASP.NET Core API.
- Het toevoegen van beveiliging (wachtwoordbeveiliging) met `pdfDocument.Encrypt(...)`.

Voel je vrij om te experimenteren, dingen kapot te maken, en vragen te stellen in de reacties. Veel programmeerplezier, en moge je PDF‑bestanden altijd perfect gestempeld zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}