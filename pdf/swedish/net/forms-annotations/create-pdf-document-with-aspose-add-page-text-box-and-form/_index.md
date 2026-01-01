---
category: general
date: 2025-12-31
description: Skapa PDF-dokument med Aspose.PDF i C#. Lär dig hur du lägger till en
  sida i PDF, lägger till en textruta och sparar PDF med formulär i en enda guide.
draft: false
keywords:
- create pdf document
- add page to pdf
- save pdf with form
- how to add text box
- how to create pdf form
language: sv
og_description: Skapa PDF-dokument med Aspose.PDF. Denna handledning visar hur du
  lägger till en sida i PDF, infogar en textruta och sparar PDF med formulär.
og_title: Skapa PDF-dokument med Aspose – Lägg till sida, textruta, formulär
tags:
- Aspose.Pdf
- C#
- PDF Forms
title: Skapa PDF-dokument med Aspose – Lägg till sida, textruta och formulär
url: /sv/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa PDF‑dokument med Aspose – Lägg till sida, textruta och formulär

Har du någonsin behövt **skapa PDF‑dokument** programatiskt och undrat var du ska börja? Du är inte ensam—utvecklare frågar ständigt: “Hur lägger jag till en sida i PDF och bäddar in ett formulärfält utan krångel?” Den goda nyheten är att Aspose.PDF gör det till en barnlek. I den här handledningen går vi igenom hela processen: från att initiera PDF‑filen, **lägga till sida i PDF**, infoga en **textruta**, och slutligen **spara PDF med formulär** så att den är klar för slutanvändare.

Vi täcker allt du behöver veta, inklusive varför varje steg är viktigt, vanliga fallgropar och några pro‑tips som sparar tid senare. När du är klar har du en fullt funktionell PDF‑fil som innehåller två länkade textrutewidgets—perfekt för signaturer, kommentarer eller någon annan datainsamlingsscenario.

## Vad du kommer att lära dig

- Hur du **skapar PDF‑dokument** från grunden med Aspose.PDF för .NET.  
- Den exakta koden för att **lägga till sida i PDF** och positionera element exakt.  
- Det korrekta sättet att **lägga till textruta** som ett formulärfält, och hur du kopplar flera widgets till samma fält.  
- Hur du **sparar PDF med formulär** så att fälten förblir interaktiva när de öppnas i Adobe Reader eller någon annan PDF‑visare.  
- Tips för felsökning och utökning av exemplet (t.ex. lägga till validering, ställa in typsnitt eller slå ihop flera sidor).

### Förutsättningar

- .NET 6.0 eller senare (koden fungerar även med .NET Framework 4.6+).  
- Aspose.PDF för .NET NuGet‑paket (`Install-Package Aspose.Pdf`).  
- Grundläggande förståelse för C#‑syntax—ingen djup PDF‑kunskap krävs.  

Om du har detta, låt oss dyka ner.

## Skapa PDF‑dokument – Initiera Aspose PDF

Det första vi måste göra är att instansiera ett **Document**‑objekt. Tänk på det som den tomma canvasen där allt annat kommer att leva.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

// Step 1: Create a new PDF document (this is the core of create pdf document)
Document pdfDocument = new Document();
```

> **Varför detta är viktigt:** `Document`‑klassen kapslar hela PDF‑filen—metadata, sidor, annotationer och formulärfält. Utan den kan du varken lägga till en sida eller ett widget senare.

## Lägg till sida i PDF – Ställ in canvasen

En PDF utan sidor är i princip en spökfil. Att lägga till en sida är enkelt, men de koordinater du väljer påverkar var dina formulärfält visas.

```csharp
// Step 2: Add a single page to the document
Page pdfPage = pdfDocument.Pages.Add();

// Optional: set page size if you need something other than A4
// pdfPage.SetPageSize(PageSize.A4.Width, PageSize.A4.Height);
```

> **Pro‑tips:** Aspose använder ett koordinatsystem där (0,0) är nedre vänstra hörnet. `Rectangle`‑objektet vi använder senare förväntar sig värden i punkter (1 punkt = 1/72 tum). Ha detta i åtanke när du placerar dina widgets.

## Hur man lägger till textruta – Definiera formulärfält

Nu kommer den roliga delen: att skapa en **textruta** som användare kan fylla i. I PDF‑terminologi är detta ett `TextBoxField`. Vi skapar ett fält med två visuella widgets—så att samma värde visas på två ställen på sidan.

```csharp
// Step 3: Define the first text box widget (the actual field definition)
TextBoxField firstTextBox = new TextBoxField(pdfPage, new Rectangle(100, 600, 300, 650))
{
    PartialName = "tb1",          // field name – must be unique within the form
    Value = "Enter text here",    // default placeholder text
    // Optional visual tweaks:
    Border = new Border(BorderStyle.Solid, 1, Color.Black),
    BackgroundColor = Color.LightGray,
    TextAlignment = HorizontalAlignment.Center
};

// Step 4: Define a second widget for the same field (appears lower on the page)
TextBoxField secondTextBoxWidget = new TextBoxField(pdfPage, new Rectangle(100, 500, 300, 550))
{
    PartialName = "tb1"   // same name links it to the first widget
};
```

> **Varför två widgets?** Att länka flera rektanglar till samma `PartialName` skapar ett *enkelt* logiskt fält med flera visuella representationer. Vad användaren skriver i en ruta visas omedelbart i den andra—praktiskt för upprepade data som “Kund‑ID”.

### Lägg till fältet i formuläret

Aspose kräver att du registrerar fältet i dokumentets formulärsamling och sedan manuellt bifogar eventuella extra widgets.

```csharp
// Step 5: Register the field (the first widget is automatically added)
pdfDocument.Form.Add(firstTextBox, "tb1", 1);

// Attach the second widget to the same field
pdfPage.Annotations.Add(secondTextBoxWidget);
```

> **Gotcha:** Om du glömmer att anropa `Form.Add` blir fältet icke‑interaktivt när PDF‑filen öppnas. Lägg alltid till den primära widgeten först, sedan eventuella extra.

## Spara PDF med formulär – Slutför dokumentet

Vi har byggt strukturen; nu sparar vi den till disk. `Save`‑metoden skriver filen och bevarar alla interaktiva element.

```csharp
// Step 6: Save the PDF – the file will contain both text box widgets
string outputPath = @"C:\Temp\TextBoxWithTwoWidgets.pdf";
pdfDocument.Save(outputPath);
```

> **Resultat:** Öppna den resulterande PDF‑filen i Adobe Reader. Du kommer att se två identiska textrutor; att skriva i den ena uppdaterar den andra omedelbart. Filen är helt **save pdf with form**‑klar och kan distribueras till användare för datainsamling.

## Fullständigt fungerande exempel

Nedan är det kompletta, kopiera‑och‑klistra‑klara programmet. Det kompileras som ett konsol‑app, men du kan bädda in samma logik i vilket .NET‑projekt som helst.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;   // for Color, Border, etc.

class Program
{
    static void Main()
    {
        // 1️⃣ Create PDF document
        Document pdfDocument = new Document();

        // 2️⃣ Add a page
        Page pdfPage = pdfDocument.Pages.Add();

        // 3️⃣ First text box (primary widget)
        TextBoxField firstTextBox = new TextBoxField(pdfPage,
            new Rectangle(100, 600, 300, 650))
        {
            PartialName = "tb1",
            Value = "Enter text here",
            Border = new Border(BorderStyle.Solid, 1, Color.Black),
            BackgroundColor = Color.LightGray,
            TextAlignment = HorizontalAlignment.Center
        };

        // 4️⃣ Second widget linked to the same field
        TextBoxField secondTextBoxWidget = new TextBoxField(pdfPage,
            new Rectangle(100, 500, 300, 550))
        {
            PartialName = "tb1"
        };

        // 5️⃣ Register field and attach extra widget
        pdfDocument.Form.Add(firstTextBox, "tb1", 1);
        pdfPage.Annotations.Add(secondTextBoxWidget);

        // 6️⃣ Save the document
        string outputPath = @"C:\Temp\TextBoxWithTwoWidgets.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"PDF created successfully at: {outputPath}");
    }
}
```

### Förväntad output

- En fil med namnet **TextBoxWithTwoWidgets.pdf** i den angivna mappen.  
- Två identiska textrutor märkta “Enter text here”.  
- Att redigera någon av rutorna uppdaterar den andra omedelbart—bevis på att fältet verkligen är delat.  

Öppna PDF‑filen med någon visare som stödjer AcroForms (Adobe Reader, Foxit, Chrome) och testa interaktiviteten.

## Vanliga frågor & kantfall

**Q: Vad händer om jag behöver fler än två widgets?**  
A: Skapa bara ytterligare `TextBoxField`‑instanser med samma `PartialName` och lägg till dem i `pdfPage.Annotations`. Det finns ingen hård gräns.

**Q: Kan jag sätta en maximal teckenlängd?**  
A: Ja. Sätt `firstTextBox.MaxLength = 50;` (eller vilket heltal som helst) innan du lägger till fältet.

**Q: Hur gör jag fältet obligatoriskt?**  
A: Använd `firstTextBox.Required = true;`. De flesta visare markerar fältet om formuläret skickas utan värde.

**Q: Jag siktar på PDF/A för arkivering—fungerar detta fortfarande?**  
A: Absolut. Anropa bara `pdfDocument.Convert(new PdfFormatConversionOptions(PdfFormat.PDFA_1_A));` innan du sparar. Formulärfälten förblir funktionella.

## Pro‑tips & bästa praxis

- **Återanvänd fältnamn med omsorg:** Om du behöver distinkta fält, ge varje ett unikt `PartialName`. Att återanvända samma namn skapar ett delat värde, vilket kan vara en kraftfull funktion eller en källa till buggar om du glömmer bort det.  
- **Koordinatkonvertering:** När du designar på skärm kan du arbeta i pixlar. Konvertera till punkter (`points = pixels * 72 / DPI`) för att undvika felplacerade element.  
- **Prestandatips:** Om du genererar många sidor, återanvänd en enda `TextBoxField`‑definition och klona den med `firstTextBox.Clone()`—det minskar minnesanvändningen.  
- **Stil:** Aspose låter dig bädda in typsnitt (`pdfDocument.Fonts.Add(FontRepository.FindFont("Arial"))`) så att utseendet blir konsekvent på alla plattformar.

## Nästa steg

Nu när du vet **hur man skapar pdf document**, **lägger till sida i pdf**, **hur man lägger till textruta**, och **sparar pdf med formulär**, kan du bygga vidare:

- Lägg till **checkboxar** eller **radioknappar** för enkäter.  
- Fyll i formuläret programatiskt från en databas (t.ex. fyll i fakturor).  
- Slå ihop flera PDF‑filer till en enda fil samtidigt som du bevarar formulärfält.

Om du är nyfiken på att generera tabeller, bilder eller digitala signaturer, kolla in våra andra guider om *Aspose.PDF för .NET*.

---

**Lycka till med kodningen!** Kommentera gärna om något är oklart, eller dela hur du anpassade formuläret för ditt eget projekt. 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}