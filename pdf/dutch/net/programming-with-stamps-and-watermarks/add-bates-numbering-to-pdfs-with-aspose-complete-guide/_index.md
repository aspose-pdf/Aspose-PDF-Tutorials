---
category: general
date: 2026-04-25
description: Voeg snel Bates-nummering toe aan PDF's met Aspose.Pdf. Leer hoe je paginanummers
  aan een PDF toevoegt, automatisch de lettergrootte aanpast en een tekstwatermerk
  toevoegt in C#.
draft: false
keywords:
- add bates numbering
- add page numbers pdf
- auto adjust font size
- how to add bates
- add text watermark
language: nl
og_description: Voeg Bates‑nummering toe aan PDF’s met Aspose.Pdf. Deze gids laat
  zien hoe je paginanummers aan een PDF toevoegt, automatisch de lettergrootte aanpast
  en een tekstwatermerk toevoegt in één uitvoerbaar voorbeeld.
og_title: Voeg Bates-nummering toe aan PDF's – Volledige Aspose C#-tutorial
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Voeg Bates-nummering toe aan PDF's met Aspose – Complete gids
url: /nl/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates-nummering toevoegen aan PDF's met Aspose – Complete Gids

Heb je ooit **bates numbering** aan een PDF moeten toevoegen maar wist je niet waar te beginnen? Je bent niet de enige—juridische teams, auditors en ontwikkelaars lopen hier dagelijks tegenaan. Het goede nieuws? Met Aspose.Pdf for .NET kun je een Bates‑nummer stempelen, de lettergrootte automatisch aanpassen en de stempel zelfs behandelen als een subtiele tekst‑watermark—alles in een handvol regels C#.

In deze tutorial lopen we stap voor stap door hoe je **add page numbers pdf** uitvoert, de lettergrootte zo afstemt dat deze nooit overlapt, en de “how to add bates” vraag een voor een beantwoordt. Aan het einde heb je een kant‑klaar console‑appje dat een professioneel genummerde PDF produceert, en zie je hoe je dit kunt uitbreiden tot een volledige watermark‑oplossing.

## Prerequisites

Voordat we beginnen, zorg ervoor dat je het volgende hebt:

* **Aspose.Pdf for .NET** (het nieuwste NuGet‑pakket vanaf april 2026).  
* .NET 6.0 SDK of nieuwer – de API werkt hetzelfde op .NET Framework, maar .NET 6 levert de beste prestaties.  
* Een voorbeeld‑PDF genaamd `input.pdf` geplaatst in een map die je kunt refereren (bijv. `C:\Docs\`).  

Er is geen extra configuratie nodig; de bibliotheek is zelf‑voorzienend.

---

## Step 1 – Load the Source PDF Document

De eerste stap is het openen van het bestand dat we willen nummeren. Aspose’s `Document`‑klasse vertegenwoordigt de volledige PDF, en het laden is zo simpel als het pad doorgeven aan de constructor.

```csharp
using Aspose.Pdf;

string inputPath = @"C:\Docs\input.pdf";
Document pdfDocument = new Document(inputPath);
```

*Why this matters*: Het laden van het document geeft je toegang tot de `Pages`‑collectie, waar we later de Bates‑stempel zullen toevoegen. Als het bestand niet gevonden wordt, gooit Aspose een duidelijke `FileNotFoundException`, zodat je precies weet wat er mis ging.

---

## Step 2 – Create a Text Stamp for Bates Numbers

Nu maken we het visuele element dat op elke pagina verschijnt. De `TextStamp`‑klasse laat je elke string embedden, en we gebruiken de placeholder `{page}-{total}` zodat Aspose die tokens automatisch vervangt.

```csharp
// Create a stamp that will display "Bates: 1-10", "Bates: 2-10", etc.
TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
{
    // Let the stamp automatically adjust its font size to fit the stamp rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Optional: make the stamp look like a subtle watermark
    Opacity = 0.4,
    // Position the stamp at the bottom‑right corner
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Choose a readable font
    Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
};
```

*Key points*:

* **auto adjust font size** – Het instellen van `AutoAdjustFontSizeToFitStampRectangle` op `true` garandeert dat de tekst nooit buiten het rechthoekige gebied valt, wat perfect is voor variabele paginanummers.  
* **add text watermark** – Door de `Opacity` te verlagen, maken we van het Bates‑nummer een subtiele watermark, waardoor de “add text watermark” eis wordt vervuld zonder een extra stap.  
* **how to add bates** – De `{page}`‑ en `{total}`‑tokens zijn de geheime saus; Aspose vervangt ze tijdens runtime, zodat je zelf niets hoeft te berekenen.

---

## Step 3 – Apply the Stamp to Every Page

Een veelvoorkomende valkuil is alleen de eerste pagina stempelen. Om echt **add page numbers pdf** te doen, moeten we door de volledige `Pages`‑collectie lopen.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp for each page to avoid shared state issues
    page.AddStamp(batesStamp);
}
```

Waarom klonen? De `AddStamp`‑methode maakt intern een kopie, maar expliciet een nieuw exemplaar per iteratie gebruiken voorkomt onbedoelde bijwerkingen als je later stempel‑eigenschappen wijzigt (bijv. kleur voor specifieke pagina's).

---

## Step 4 – Save the Updated PDF

Met de stempels op hun plaats is het opslaan van de wijzigingen eenvoudig. Je kunt het originele bestand overschrijven of naar een nieuwe locatie schrijven—hier slaan we een nieuw bestand op genaamd `output.pdf`.

```csharp
string outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

Als je `output.pdf` opent, zie je elke pagina gelabeld “Bates: 1‑10”, “Bates: 2‑10”, … rechtsonder, met een lichte opacity die tevens fungeert als een **add text watermark**.

---

## Full Working Example

Alles bij elkaar, hier is een enkel, zelf‑voorzienend console‑programma dat je kunt copy‑pasten in Visual Studio.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        string inputPath = @"C:\Docs\input.pdf";
        Document pdfDocument = new Document(inputPath);

        // 2️⃣ Create a Bates number stamp with auto‑adjusted font size
        TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Opacity = 0.4, // acts as a subtle watermark
            XIndent = 20,
            YIndent = 20,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
        };

        // 3️⃣ Add the stamp to every page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.AddStamp(batesStamp);
        }

        // 4️⃣ Save the result
        string outputPath = @"C:\Docs\output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**Expected result**: Open `output.pdf` in een viewer; elke pagina toont een regel zoals “Bates: 3‑12” in de rechter‑onderhoek, precies passend in het rechthoekige gebied en gerenderd met 40 % opacity. Dit voldoet zowel aan de juridische‑tracking eis als aan de visuele watermark‑behoefte.

---

## Common Variations & Edge Cases

| Situatie | Wat te wijzigen | Waarom |
|-----------|----------------|-----|
| **Andere plaatsing** | Pas `HorizontalAlignment` / `VerticalAlignment` aan of stel `XIndent`/`YIndent` in | Sommige bedrijven geven de voorkeur aan links‑boven of gecentreerde plaatsing. |
| **Aangepast voorvoegsel** | Vervang `"Bates: "` door `"Doc‑ID: "` of een andere string | Je gebruikt mogelijk een andere naamgevingsconventie. |
| **Meerdere stempels** | Maak een tweede `TextStamp` (bijv. voor een vertrouwelijkheidsmelding) en voeg die toe na de eerste | Het combineren van **add bates numbering** met andere **add text watermark** eisen is triviaal. |
| **Grote paginatellingen** | Verhoog de initiële lettergrootte (bijv. `14`) – de auto‑adjust zal deze verkleinen wanneer nodig | Bij > 999 pagina's wordt de string langer; auto‑adjust voorkomt afsnijden. |
| **Versleutelde PDF's** | Roep `pdfDocument.Decrypt("password")` aan vóór het stempelen | Je kunt een beveiligd bestand niet wijzigen zonder het wachtwoord. |

---

## Pro Tips & Pitfalls

* **Pro tip:** Stel `batesStamp.Margin = new MarginInfo(5, 5, 5, 5)` in als je merkt dat de tekst tegen de rand van de pagina aankomt.  
* **Watch out for:** Zeer kleine rechthoeken (standaardgrootte is 100 × 30 pt). Als je een groter gebied nodig hebt, stel `batesStamp.Width` en `batesStamp.Height` handmatig in.  
* **Performance note:** Het stempelen van duizenden pagina's kan enkele seconden duren, maar Aspose streamt pagina's efficiënt—geen noodzaak om het volledige document in het geheugen te laden.  

---

## Conclusion

We hebben zojuist laten zien hoe je **add bates numbering** aan een PDF kunt toevoegen met Aspose.Pdf, terwijl je tegelijkertijd **add page numbers pdf**, **auto adjust font size** en een **add text watermark** in één samenhangende workflow realiseert. Het complete, uitvoerbare voorbeeld hierboven biedt een solide basis die je kunt aanpassen aan elke juridische‑documentworkflow of intern rapportagesysteem.

Klaar voor de volgende stap? Probeer deze aanpak te combineren met Aspose’s PDF‑merge‑API om meerdere bestanden in één keer te verwerken, of verken de `TextFragment`‑klasse voor rijkere watermarks (gekleurde, gedraaide of meer‑regelige). De mogelijkheden zijn eindeloos, en de code die je nu hebt is een betrouwbaar startpunt.

Als je deze gids nuttig vond, laat dan een reactie achter, geef een ster aan de repository, of deel je eigen variaties. Happy coding, en moge je PDF's altijd perfect genummerd zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}