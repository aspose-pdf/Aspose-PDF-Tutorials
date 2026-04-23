---
category: general
date: 2026-03-24
description: Skapa PDF-dokument med Aspose.PDF i C#. Lär dig hur du lägger till ett
  textrutefält i PDF-formuläret och snabbt lägger till formulärfält i PDF.
draft: false
keywords:
- create pdf document
- add text box pdf
- add form field pdf
- how to create pdf
- how to add textbox
language: sv
og_description: Skapa PDF-dokument med Aspose.PDF i C#. Denna guide visar hur du lägger
  till en textruta som PDF-formulärfält och hur du lägger till formulärfält i PDF
  på några minuter.
og_title: Skapa PDF-dokument med Aspose – Lägg till textfält
tags:
- Aspose.PDF
- C#
- PDF Forms
title: Skapa PDF-dokument med Aspose – Lägg till textrutefält
url: /sv/net/programming-with-forms/create-pdf-document-with-aspose-add-text-box-field/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa PDF-dokument med Aspose – Lägg till textruta-fält

Har du någonsin behövt **create PDF document** programatiskt och undrat var du ska börja? Du är inte ensam—många utvecklare stöter på samma problem när deras appar måste samla in användarinmatning utan att dra in ett tungt UI‑bibliotek. Den goda nyheten? Med Aspose.PDF för .NET kan du skapa en PDF, placera en textruta på vilken sida som helst och till och med fästa samma fält på flera sidor—allt i några få rader.

I den här handledningen går vi igenom hela processen: från att initiera PDF‑filen, till **add text box PDF** formulärfält, till **add form field PDF**‑registrering, och slutligen hur du verifierar att allt fungerar. I slutet kommer du att veta **how to create PDF**‑filer som är interaktiva, och du kommer också att se **how to add textbox**‑kontroller som beter sig exakt som inbyggda Acrobat‑fält.

---

## Vad du behöver

- **ASP.NET Core** eller något .NET 6+ projekt (koden fungerar även på .NET Framework 4.6+).  
- **Aspose.PDF for .NET** NuGet‑paket (version 23.9 eller nyare).  
- En måttlig mängd C#‑erfarenhet—inget avancerat, bara grunderna.  

Om du har markerat dessa rutor är du redo att köra. Inga extra verktyg, inga externa tjänster, bara ren C#‑kod som du kan klistra in i en konsolapp och köra.

---

## Skapa PDF-dokument och lägg till ett textruta‑formulärfält

Det första steget är, som förväntat, att **create PDF document**. Tänk på `Document`‑klassen som en tom duk; när du har den kan du börja måla sidor, former och interaktiva element.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

// Step 1: Create a new PDF document (the blank canvas)
using var document = new Document();

// Step 2: Add a new page where the text box will live
var page1 = document.Pages.Add();
```

> **Varför detta är viktigt:** Att instansiera `Document` utan några sidor kastar ett undantag så snart du försöker placera en widget. Att först lägga till en sida garanterar ett giltigt sidindex (`Pages[1]`) för nästa steg.

---

## Lägg till ett textruta‑PDF‑formulärfält på sida 1

Nu när vi har en sida, låt oss **add text box PDF** formulärfält. Klassen `TextBoxField` representerar ett enda logiskt fält; du kan tänka på det som “namnet” på inmatningen som kan visas på många ställen.

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

> **Proffstips:** Rektangeln använder punkter (1/72 tum). Justera koordinaterna för att passa din layout; origo (0,0) är i sidans nedre‑vänstra hörn.

---

## Skapa en andra widget på en annan sida

Ett enda logiskt fält kan ha flera visuella widgets—perfekt för formulär med flera sidor. Här är **how to add textbox** på en andra sida, med återanvändning av samma fältnamn.

```csharp
// Step 5: Add a second page for the extra widget
var page2 = document.Pages.Add();

// Step 6: Create a widget for the same field on page 2
var secondWidget = textBoxField.CreateWidget(new Rectangle(100, 400, 300, 420));
```

> **Varför vi gör detta:** Användare behöver ofta fylla i samma information i olika sektioner (t.ex. “Name” högst upp och igen i en sammanfattning). Genom att dela det logiska namnet säkerställer Aspose att båda widgets hålls synkroniserade.

---

## Registrera formulärfältet i PDF‑filen

Att skapa fältobjektet räcker inte; du måste lägga till det i dokumentets formulärsamling. Detta är steget där du **add form field PDF** till den interna strukturen.

```csharp
// Step 7: Register the field (with both widgets) in the document's form collection
document.Form.Add(textBoxField, "MultiWidget");

// Optional: Save the PDF to disk
document.Save("MultiWidgetExample.pdf");
```

> **Vad som händer under huven:** `Form.Add` skriver fältdefinitionen till AcroForm‑ordboken, vilket gör PDF‑filen interaktiv när den öppnas i Acrobat Reader eller någon PDF‑visare som stöder formulär.

---

## Kör och verifiera resultatet

Kompilera och kör konsolappen. Öppna `MultiWidgetExample.pdf` i Adobe Acrobat (eller någon visare som stöder formulär) så ser du två identiska textrutor på sidor 1 och 2. Skriv något i en ruta—se den andra uppdateras omedelbart. Det är kraften i ett delat logiskt fält.

```text
Expected outcome:
- PDF with two pages.
- Each page shows a white rectangle (the text box).
- Editing one box updates the other automatically.
```

Om du inte ser rutorna, dubbelkolla att rektanglarna ligger inom sidans gränser och att du sparade dokumentet efter att ha lagt till fältet.

---

## Vanliga frågor & kantfall

### Vad händer om jag behöver ett annat utseende på varje sida?

Du kan anpassa varje widget efter skapandet:

```csharp
secondWidget.Rect = new Rectangle(150, 350, 350, 370); // reposition
secondWidget.Border = new Border(BorderStyle.Solid, 1, Color.Black);
secondWidget.BackgroundColor = Color.LightYellow;
```

### Kan jag ange ett standardvärde?

Självklart—tilldela bara `Value` innan du sparar:

```csharp
textBoxField.Value = "Enter your name here";
```

Alla widgets kommer att visa den platsen tills användaren skriver över den.

### Hur gör man fältet obligatoriskt?

```csharp
textBoxField.Required = true;
```

Acrobat kommer att varna användaren om de försöker skicka formuläret utan att fylla i det.

### Fungerar detta med PDF/A‑kompatibilitet?

Aspose.PDF stödjer PDF/A‑1b,‑2b,‑3b. När du har byggt färdigt formuläret kan du konvertera:

```csharp
document.Convert(new PdfConversionOptions { Compliance = PdfCompliance.PdfA2b });
```

---

## Fullt fungerande exempel

Nedan är det kompletta, kopiera‑och‑klistra‑klara programmet. Spara det som `Program.cs` i ett .NET‑konsolprojekt, lägg till Aspose.PDF‑NuGet‑paketet och kör.

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