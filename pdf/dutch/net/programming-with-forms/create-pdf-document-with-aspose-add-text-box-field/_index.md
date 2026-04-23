---
category: general
date: 2026-03-24
description: Maak een PDF-document met Aspose.PDF in C#. Leer hoe je een tekstvak‑PDF‑formulierveld
  toevoegt en hoe je snel een PDF‑formulierveld toevoegt.
draft: false
keywords:
- create pdf document
- add text box pdf
- add form field pdf
- how to create pdf
- how to add textbox
language: nl
og_description: Maak een PDF-document met Aspose.PDF in C#. Deze gids laat zien hoe
  je een tekstvak‑PDF‑formulierveld en een PDF‑formulierveld in enkele minuten toevoegt.
og_title: PDF-document maken met Aspose – Tekstvakveld toevoegen
tags:
- Aspose.PDF
- C#
- PDF Forms
title: PDF-document maken met Aspose – Tekstvakveld toevoegen
url: /nl/net/programming-with-forms/create-pdf-document-with-aspose-add-text-box-field/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF-document maken met Aspose – Tekstvakveld toevoegen

Heb je ooit **PDF-document maken** programmatisch moeten doen en je afgevraagd waar je moet beginnen? Je bent niet de enige—veel ontwikkelaars lopen tegen die muur aan wanneer hun apps gebruikersinvoer moeten verzamelen zonder een zware UI‑bibliotheek te gebruiken. Het goede nieuws? Met Aspose.PDF voor .NET kun je een PDF aanmaken, een tekstvak op elke pagina plaatsen en zelfs hetzelfde veld aan meerdere pagina's koppelen—alles in een handvol regels.

In deze tutorial lopen we het volledige proces door: van het initialiseren van de PDF, tot **tekstvak PDF toevoegen** formuliervelden, tot **formulierveld PDF toevoegen** registratie, en uiteindelijk hoe je kunt verifiëren dat alles werkt. Aan het einde weet je **hoe PDF te maken** bestanden die interactief zijn, en zie je ook **hoe tekstvak toe te voegen** controles die zich precies gedragen als native Acrobat‑velden.

---

## Wat je nodig hebt

- **ASP.NET Core** of elk .NET 6+ project (de code werkt ook op .NET Framework 4.6+).  
- **Aspose.PDF for .NET** NuGet‑pakket (versie 23.9 of nieuwer).  
- Een bescheiden hoeveelheid C#‑ervaring—niets ingewikkelds, alleen de basis.  

Als je die punten hebt afgevinkt, kunnen we van start gaan. Geen extra tools, geen externe services, alleen pure C#‑code die je kunt plakken in een console‑app en uitvoeren.

---

## PDF-document maken en een tekstvak‑formulierveld toevoegen

De eerste stap is, zoals verwacht, om **PDF-document maken**. Beschouw de `Document`‑klasse als een leeg canvas; zodra je die hebt, kun je pagina's, vormen en interactieve elementen gaan tekenen.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

// Step 1: Create a new PDF document (the blank canvas)
using var document = new Document();

// Step 2: Add a new page where the text box will live
var page1 = document.Pages.Add();
```

> **Waarom dit belangrijk is:** Instantiëren van `Document` zonder pagina's veroorzaakt een uitzondering op het moment dat je een widget probeert te plaatsen. Het eerst toevoegen van een pagina garandeert een geldige paginanaam (`Pages[1]`) voor de volgende stappen.

---

## Tekstvak‑PDF‑formulierveld toevoegen aan pagina 1

Nu we een pagina hebben, laten we **tekstvak PDF toevoegen** formulierveld. De `TextBoxField`‑klasse vertegenwoordigt een enkel logisch veld; je kunt het zien als de “naam” van de invoer die op veel plaatsen kan verschijnen.

```csharp
// Step 3: Define the rectangle where the textbox will appear (x, y, width, height)
var textBoxRect = new Rectangle(100, 500, 300, 520);

// Step 4: Create the text box field on page 1
var textBoxField = new TextBoxField(document.Pages[1], textBoxRect)
{
    // This logical name is used later when you retrieve the value
    PartialName = "MultiWidget"
};
```

> **Pro tip:** De rechthoek gebruikt punten (1/72 inch). Pas de coördinaten aan om bij je lay-out te passen; de oorsprong (0,0) bevindt zich in de linker‑onderhoek van de pagina.

---

## Een tweede widget op een andere pagina maken

Een enkel logisch veld kan meerdere visuele widgets hebben—perfect voor formulieren over meerdere pagina's. Hier is **hoe tekstvak toe te voegen** op een tweede pagina, waarbij dezelfde veldnaam opnieuw wordt gebruikt.

```csharp
// Step 5: Add a second page for the extra widget
var page2 = document.Pages.Add();

// Step 6: Create a widget for the same field on page 2
var secondWidget = textBoxField.CreateWidget(new Rectangle(100, 400, 300, 420));
```

> **Waarom we dit doen:** Gebruikers moeten vaak dezelfde informatie invullen in verschillende secties (bijv. “Naam” bovenaan en opnieuw in een samenvatting). Door de logische naam te delen, zorgt Aspose ervoor dat beide widgets synchroon blijven.

---

## Het formulierveld registreren in de PDF

Het aanmaken van het veldobject is niet genoeg; je moet het toevoegen aan de formulierverzameling van het document. Dit is de stap waarin je **formulierveld PDF toevoegen** aan de interne structuur.

```csharp
// Step 7: Register the field (with both widgets) in the document's form collection
document.Form.Add(textBoxField, "MultiWidget");

// Optional: Save the PDF to disk
document.Save("MultiWidgetExample.pdf");
```

> **Wat er onder de motorkap gebeurt:** `Form.Add` schrijft de velddefinitie naar het AcroForm‑woordenboek, waardoor de PDF interactief wordt wanneer deze wordt geopend in Acrobat Reader of een andere PDF‑viewer die formulieren ondersteunt.

---

## Uitvoeren en het resultaat verifiëren

Compileer en voer de console‑app uit. Open `MultiWidgetExample.pdf` in Adobe Acrobat (of een viewer die formulieren ondersteunt) en je ziet twee identieke tekstvakken op pagina 1 en 2. Typ iets in één vak—zie hoe het andere onmiddellijk wordt bijgewerkt. Dat is de kracht van een gedeeld logisch veld.

```text
Expected outcome:
- PDF with two pages.
- Each page shows a white rectangle (the text box).
- Editing one box updates the other automatically.
```

Als je de vakken niet ziet, controleer dan dubbel of de rechthoeken binnen de paginagrenzen liggen en of je het document hebt opgeslagen na het toevoegen van het veld.

---

## Veelgestelde vragen & randgevallen

### Wat als ik op elke pagina een andere weergave nodig heb?

Je kunt elke widget na creatie aanpassen:

```csharp
secondWidget.Rect = new Rectangle(150, 350, 350, 370); // reposition
secondWidget.Border = new Border(BorderStyle.Solid, 1, Color.Black);
secondWidget.BackgroundColor = Color.LightYellow;
```

### Kan ik een standaardwaarde instellen?

Zeker—wijs `Value` toe vóór het opslaan:

```csharp
textBoxField.Value = "Enter your name here";
```

Alle widgets zullen die placeholder weergeven totdat de gebruiker deze overschrijft.

### Hoe maak ik het veld verplicht?

```csharp
textBoxField.Required = true;
```

Acrobat zal de gebruiker waarschuwen als hij probeert het formulier in te dienen zonder het in te vullen.

### Werkt dit met PDF/A‑compliance?

Aspose.PDF ondersteunt PDF/A‑1b,‑2b,‑3b. Nadat je het formulier hebt gebouwd, kun je converteren:

```csharp
document.Convert(new PdfConversionOptions { Compliance = PdfCompliance.PdfA2b });
```

---

## Volledig werkend voorbeeld

Hieronder staat het volledige, kant‑klaar‑om‑te‑kopiëren‑en‑plakken programma. Sla het op als `Program.cs` in een .NET console‑project, voeg het Aspose.PDF‑NuGet‑pakket toe, en voer het uit.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var document = new Document();

        // 2️⃣ Add two pages (page 1 will host the first widget, page 2 the second)
        var page1 = document.Pages.Add();
        var page2 = document.Pages.Add();

        // 3️⃣ Define the rectangle for the first widget
        var rect1 = new Rectangle(100, 500, 300, 520);

        // 4️⃣ Create the text box field (logical name = "MultiWidget")
        var textBoxField = new TextBoxField(document.Pages[1], rect1)
        {
            PartialName = "MultiWidget",
            Value = "Sample text",        // optional default value
            Required = true               // makes the field mandatory
        };

        // 5️⃣ Add a second widget on page

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}