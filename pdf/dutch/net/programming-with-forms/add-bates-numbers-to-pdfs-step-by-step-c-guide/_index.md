---
category: general
date: 2026-02-12
description: Voeg snel Bates-nummers toe aan PDF‑bestanden. Leer hoe je een tekstveld
  aan een PDF toevoegt, een formulierveld aan een PDF toevoegt en paginanummers aan
  een PDF toevoegt met Aspose.PDF.
draft: false
keywords:
- add bates numbers
- add text field pdf
- add form field pdf
- add page numbers pdf
- how to add bates
language: nl
og_description: Voeg Bates-nummers toe aan PDF‑documenten in C#. Deze gids laat zien
  hoe je een tekstveld aan een PDF toevoegt, een formulierveld aan een PDF toevoegt
  en paginanummers aan een PDF toevoegt met Aspose.PDF.
og_title: Bates-nummers toevoegen aan PDF's – Complete C#-tutorial
tags:
- PDF
- C#
- Aspose.PDF
title: Bates-nummers toevoegen aan PDF’s – Stapsgewijze C#‑gids
url: /nl/net/programming-with-forms/add-bates-numbers-to-pdfs-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates-nummers toevoegen aan PDF's – Complete C#-gids

Heb je ooit **bates numbers** moeten toevoegen aan een stapel juridische PDF's, maar wist je niet waar je moest beginnen? Je bent niet de enige. In veel advocatenkantoren en e‑discovery‑projecten is het stempelen van elke pagina met een unieke identifier een dagelijkse taak, en handmatig doen is een nachtmerrie.  

Het goede nieuws? Met een paar regels C# en Aspose.PDF kun je het hele proces automatiseren. In deze tutorial lopen we stap voor stap door **hoe bates-nummers toe te voegen**, voegen we een tekstveld toe aan elke pagina, en slaan we een schone, doorzoekbare PDF op — allemaal zonder zweet.  

> **Wat je krijgt:** een volledig uitvoerbaar codevoorbeeld, uitleg waarom elke regel belangrijk is, tips voor randgevallen, en een snelle checklist om je output te verifiëren.  

We zullen ook gerelateerde taken behandelen zoals **add text field pdf**, **add form field pdf**, en **add page numbers pdf**, zodat je een gereedschapskist hebt voor elke document‑automatiseringsuitdaging.

---

## Vereisten

- .NET 6.0 of later (de code werkt ook met .NET Framework 4.6+)  
- Visual Studio 2022 (of een IDE naar keuze)  
- Een geldige Aspose.PDF for .NET-licentie (de gratis proefversie werkt voor testen)  
- Een bron‑PDF genaamd `source.pdf` geplaatst in een map die je kunt refereren  

Als een van deze onbekend klinkt, pauzeer dan en installeer het ontbrekende onderdeel voordat je verder gaat. De onderstaande stappen gaan ervan uit dat je het Aspose.PDF NuGet‑pakket al hebt toegevoegd:

```bash
dotnet add package Aspose.Pdf
```

## Hoe bates-nummers toe te voegen aan een PDF met Aspose.PDF

Hieronder staat het volledige, kant‑klaar programma. Het laadt een PDF, maakt een **text box field** op elke pagina, schrijft een geformatteerd Bates‑nummer, en slaat uiteindelijk het gewijzigde bestand op.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 👉 Step 1: Load the source PDF document
        using (var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf"))
        {
            // 👉 Step 2: Add a Bates number text field to each page
            for (int pageNumber = 1; pageNumber <= pdfDocument.Pages.Count; pageNumber++)
            {
                // Define the rectangle where the field will appear (10,10) = lower‑left corner
                var fieldRect = new Rectangle(10, 10, 150, 30);

                // Create the TextBoxField – this is the “add text field pdf” part
                var batesField = new TextBoxField(pdfDocument.Pages[pageNumber], fieldRect)
                {
                    // Format the number: BATES-00001, BATES-00002, …
                    Value = $"BATES-{pageNumber:D5}"
                };

                // Register the field with the form collection – “add form field pdf”
                pdfDocument.Form.Add(batesField, $"Bates_{pageNumber}", pageNumber);
            }

            // 👉 Step 3: Save the modified PDF with Bates numbers
            pdfDocument.Save(@"YOUR_DIRECTORY\bates.pdf");
        }

        Console.WriteLine("✅ Bates numbers added successfully!");
    }
}
```

### Waarom dit werkt

- **`Document`** is het toegangspunt; het vertegenwoordigt het volledige PDF‑bestand.  
- **`Rectangle`** bepaalt waar het veld op de pagina staat. De nummers zijn in points (1 pt ≈ 1/72 in). Pas de coördinaten aan als je het nummer in een andere hoek wilt plaatsen.  
- **`TextBoxField`** is een *form field* dat elke tekenreeks kan bevatten. Door `Value` toe te wijzen, voegen we effectief **add page numbers pdf** toe met een aangepast voorvoegsel.  
- **`pdfDocument.Form.Add`** registreert het veld bij het AcroForm van de PDF, waardoor het zichtbaar wordt in viewers zoals Adobe Acrobat.  

Als je ooit het uiterlijk (lettertype, kleur, grootte) moet wijzigen, kun je de `TextBoxField`‑eigenschappen aanpassen — zie de Aspose‑documentatie voor `DefaultAppearance` en `Border`.

## Een tekstveld toevoegen aan elke PDF‑pagina (de “add text field pdf” stap)

Soms wil je alleen een zichtbaar label, geen interactief formulierveld. In dat geval kun je de `TextBoxField` vervangen door een `TextFragment` en deze direct toevoegen aan de `Paragraphs`‑collectie van de pagina. Hier is een snelle alternatieve aanpak:

```csharp
var fragment = new TextFragment($"BATES-{pageNumber:D5}")
{
    // Position the text using a TextState (font, size, color)
    TextState = new TextState
    {
        Font = FontRepository.FindFont("Arial"),
        FontSize = 12,
        ForegroundColor = Color.Black
    }
};

// Set the fragment’s rectangle (same coordinates as before)
fragment.Position = new Position(10, 10);
pdfDocument.Pages[pageNumber].Paragraphs.Add(fragment);
```

De **add text field pdf**‑aanpak is handig wanneer het uiteindelijke document alleen‑lezen is, terwijl de **add form field pdf**‑methode de nummers later bewerkbaar houdt.

## De PDF opslaan met Bates‑nummers (het “add page numbers pdf” moment)

Nadat de lus is voltooid, schrijft `pdfDocument.Save` alles naar schijf. Als je het originele bestand wilt behouden, wijzig dan simpelweg het uitvoerpad of gebruik `pdfDocument.Save`‑overloads om het resultaat direct naar een response in een web‑API te streamen.

```csharp
// Example: stream to HTTP response (ASP.NET Core)
Response.ContentType = "application/pdf";
pdfDocument.Save(Response.Body);
```

Dat is het mooie deel — geen tijdelijke bestanden, geen extra bibliotheken, alleen Aspose die het zware werk doet.

## Verwacht resultaat & snelle verificatie

Open `bates.pdf` in een PDF‑viewer. Je zou een klein vakje in de linker‑onderhoek van elke pagina moeten zien met de tekst:

```
BATES-00001
BATES-00002
…
```

Als je de documenteigenschappen inspecteert, zie je een AcroForm met velden genaamd `Bates_1`, `Bates_2`, enz. Dat bevestigt dat de **add form field pdf**‑stap geslaagd is.

## Veelvoorkomende valkuilen & pro‑tips

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| Nummers verschijnen niet gecentreerd | Rechthoekcoördinaten zijn relatief ten opzichte van de linker‑onderhoek van de pagina. | Draai de Y‑waarde (`pageHeight - marginTop`) om of gebruik `page.PageInfo.Height` om een boven‑marge positie te berekenen. |
| Velden zijn onzichtbaar in Adobe Reader | De standaardrand is ingesteld op “No”. | Set `batesField.Border = new Border { Width = 0.5f, Color = Color.Black };` |
| Grote PDF's veroorzaken geheugenbelasting | `using` verwijdert het document pas nadat de lus is voltooid. | Verwerk pagina's in delen of gebruik `pdfDocument.Save` met `SaveOptions` die streaming mogelijk maken. |
| Licentie niet toegepast | Aspose plaatst een watermerk op de eerste pagina. | Register your license early: `License lic = new License(); lic.SetLicense("Aspose.Pdf.lic");` |

## De oplossing uitbreiden

- **Custom prefixes:** Vervang `"BATES-"` door een willekeurige string (`"DOC-"`, `"CASE-"`, …).  
- **Zero‑padding length:** Verander `{pageNumber:D5}` naar `{pageNumber:D3}` voor drie cijfers.  
- **Dynamic placement:** Gebruik `pdfDocument.Pages[pageNumber].PageInfo.Width` om het veld aan de rechterkant te positioneren.  
- **Conditional numbering:** Sla lege pagina's over door `pdfDocument.Pages[pageNumber].IsBlank` te controleren.  

Al deze variaties behouden het kernpatroon van **add bates numbers**, **add text field pdf**, en **add form field pdf** ongewijzigd.

## Volledig werkend voorbeeld (alles‑in‑één)

Hieronder staat het uiteindelijke, kant‑klaar programma dat de bovenstaande tips bevat. Kopieer het naar een nieuwe console‑app en druk op F5.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;

class AddBatesNumbers
{
    static void Main()
    {
        // Register your license here (optional for trial)
        // var license = new License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        using (var pdfDocument = new Document(inputPath))
        {
            int totalPages = pdfDocument.Pages.Count;

            for (int i = 1; i <= totalPages; i++)
            {
                // Position the field 10 pts from left and 10 pts from bottom
                var rect = new Rectangle(10, 10, 150, 30);

                var batesField = new TextBoxField(pdfDocument.Pages[i], rect)
                {
                    Value = $"BATES-{i:D5}"
                };

                // Optional: make the field look nicer
                batesField.Border = new Border
                {
                    Width = 0.5f,
                    Color = Color.Gray
                };
                batesField.DefaultAppearance = new DefaultAppearance
                {
                    Font = FontRepository.FindFont("Arial"),
                    FontSize = 10,
                    ForegroundColor = Color.DarkBlue
                };

                pdfDocument.Form.Add(batesField, $"Bates_{i}", i);
            }

            pdfDocument.Save(outputPath);
        }

        Console.WriteLine($"✅ Finished! Bates numbers saved to: {outputPath}");
    }
}
```

Voer het uit, open het resultaat, en je ziet een professioneel uitziende identifier op elke pagina — precies wat een litigation support‑specialist zou verwachten.

## Conclusie

We hebben zojuist **how to add bates numbers** aangetoond voor elke PDF met C# en Aspose.PDF. Door een **text box field** op elke pagina te maken, voegen we tegelijkertijd **add text field pdf**, **add form field pdf**, en **add page numbers pdf** toe in één enkele stap. De aanpak is snel, schaalbaar, en eenvoudig aan te passen voor aangepaste voorvoegsels, verschillende lay-outs, of conditionele logica.

Klaar voor de volgende uitdaging? Probeer een QR‑code in te sluiten die linkt naar het originele dossier, of genereer een aparte indexpagina die alle Bates‑nummers met hun bijbehorende paginatitels opsomt. dezelfde API laat je PDF's samenvoegen, pagina's extraheren, en zelfs gevoelige gegevens redigeren — de mogelijkheden zijn eindeloos.

Als je ergens vastloopt, laat dan een reactie achter of raadpleeg de officiële documentatie van Aspose voor meer verdieping. Veel plezier met coderen, en moge je PDF's altijd perfect genummerd blijven!  

---  

![add bates numbers screenshot](https://example.com/images/add-bates-numbers.png "add bates numbers example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}