---
category: general
date: 2026-06-18
description: Hur man lägger till en form i PDF med Aspose.PDF i C# – ladda en PDF,
  rita en rektangel och spara den.
draft: false
keywords:
- how to add shape to pdf
- load pdf document in c#
- how to draw shapes in pdf
- aspose pdf add rectangle
language: sv
og_description: Hur man lägger till en form i PDF med Aspose.PDF i C#. Lär dig att
  läsa in ett PDF-dokument, rita en rektangel och spara den uppdaterade filen.
og_title: Hur man lägger till en form i PDF med Aspose.PDF i C#
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: How to add shape to PDF using Aspose.PDF in C# – load a PDF, draw a
    rectangle, and save it.
  headline: How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide
  type: TechArticle
- description: How to add shape to PDF using Aspose.PDF in C# – load a PDF, draw a
    rectangle, and save it.
  name: How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide
  steps:
  - name: What if I need to draw on multiple pages?
    text: Simply loop over `pdfDoc.Pages` and call `AddRectangle` (or any other shape)
      for each page. Remember to adjust coordinates if pages have different sizes.
  - name: Can I fill the rectangle with a color?
    text: Absolutely. Change `FillColor` from `Transparent` to any `Color` you like,
      e.g., `Color.Yellow`. The shape will appear as a solid block.
  - name: Does this work with password‑protected PDFs?
    text: 'Aspose.PDF can open encrypted files if you supply the password:'
  - name: How to add a rectangle with rounded corners?
    text: Use the `RoundedRectangle` class instead of `Rectangle`. The rest of the
      steps stay identical.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Hur man lägger till en form i PDF med Aspose.PDF i C# – Steg‑för‑steg‑guide
url: /sv/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så lägger du till en form i PDF med Aspose.PDF i C# – Komplett handledning

Har du någonsin undrat **hur man lägger till en form i PDF** utan att kämpa med lågnivå‑byte‑strömmar? I många verkliga applikationer behöver du markera ett område, understryka ett villkor eller helt enkelt rita en avgränsningsruta för ett signaturfält. Den goda nyheten är att Aspose.PDF gör detta till en barnlek. I den här guiden laddar vi ett PDF‑dokument i C#, ritar en rektangel och sparar resultatet – inget mer, inget mindre.

Vi går igenom varje kodrad, förklarar *varför* varje del är viktig, och visar även ett snabbt sätt att verifiera att formen verkligen hamnade där du förväntar dig. När du är klar kommer du att känna dig bekväm med **hur man ritar former i PDF**‑filer, och du har ett återanvändbart kodexempel som du kan klistra in i vilket .NET‑projekt som helst.

## Förutsättningar

Innan vi börjar, se till att du har:

- **.NET 6.0** (eller någon nyare .NET‑version) installerad på din maskin.  
- En **giltig Aspose.PDF för .NET‑licens** (eller en gratis utvärderingsnyckel).  
- Visual Studio 2022, Rider eller någon annan editor du föredrar.  
- En befintlig PDF‑fil (`input.pdf`) placerad i en mapp du kan referera till.

> **Pro‑tips:** Om du bara testar är den fria utvärderingsversionen helt tillräcklig – den lägger till ett litet vattenstämpel men beter sig annars som den fullständiga produkten.

## Steg 1: Skapa projektet och importera namnrymder

Skapa först ett nytt konsolprojekt (eller lägg till i ett befintligt) och ta in de nödvändiga namnrymderna.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;   // Required for shape classes
```

Varför detta är viktigt: `Aspose.Pdf` ger dig kärn‑dokumentmodellen, medan `Aspose.Pdf.Drawing` innehåller `Rectangle`‑klassens form som vi kommer att använda senare. Utan den senare kommer kompilatorn klaga på att `Rectangle` inte är definierad.

## Steg 2: Ladda PDF‑dokument i C#

Nu **laddar vi pdf‑dokument i c#**. Detta är den första operationen du alltid utför när du avser att modifiera en befintlig fil.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";
Document pdfDoc = new Document(inputPath);
Console.WriteLine($"Loaded PDF with {pdfDoc.Pages.Count} page(s).");
```

*Förklaring*:  
- `Document` är Asposes representation av hela filen.  
- Att skicka hela sökvägen till konstruktorn läser in filen i minnet.  
- `Console.WriteLine`‑raden är valfri men praktisk för felsökning – om sidantalet är noll vet du att något gick fel tidigt.

## Steg 3: Definiera rektangelformen

Här kommer vi till själva kärnan i **hur man lägger till en form i PDF**. Vi skapar ett `Rectangle`‑objekt som specificerar position och storlek med koordinatsystemet där (0,0) är sidans nedre vänstra hörn.

```csharp
// Step 3: Define a rectangle (left, bottom, right, top)
Rectangle rect = new Rectangle(0, 0, 200, 100)
{
    // Optional styling – you can tweak these as needed
    FillColor = Color.Transparent,          // No fill, just the border
    Border = new Border(BorderStyle.Solid, 2, Color.Red)
};
```

Varför vi sätter `FillColor` till transparent: de flesta användningsfall vill bara ha en kontur (tänk på en markeringsruta). `Border`‑egenskapen låter dig styra tjocklek och färg; rött får rektangeln att sticka ut på en typisk vit sida.

## Steg 4: Verifiera att formen får plats inom sidans gränser

Innan vi **lägger till rektangel**, är det en god vana att säkerställa att formen inte sträcker sig utanför sidans kanter. Aspose tillhandahåller `ValidateShapeBounds` just för detta ändamål.

```csharp
// Step 4: Validate that the rectangle fits on the first page
bool fits = pdfDoc.Pages[1].ValidateShapeBounds(rect);
if (!fits)
{
    Console.WriteLine("Rectangle exceeds page dimensions – adjusting...");
    // Simple fallback: shrink to fit the page width
    rect.Right = pdfDoc.Pages[1].PageInfo.Width - 10;
    rect.Top  = pdfDoc.Pages[1].PageInfo.Height - 10;
}
```

*Varför*: Att rita utanför sidan kan orsaka renderingsfel eller till och med kasta ett undantag. Denna kontroll gör handledningen robust för PDF‑filer av alla storlekar.

## Steg 5: Lägg till rektangeln på önskad sida

Nu **lägger vi till formen i pdf**. Metoden `AddRectangle` fäster formen i sidans annotationssamling, vilket betyder att PDF‑visare renderar den precis som alla andra teckningar.

```csharp
// Step 5: Add the rectangle to the first page
pdfDoc.Pages[1].AddRectangle(rect);
Console.WriteLine("Rectangle added to page 1.");
```

Om du behöver rikta in dig på en annan sida, ersätt helt enkelt indexet `1` med rätt sidnummer (Aspose använder 1‑baserad indexering).

## Steg 6: Spara den modifierade PDF‑filen

Det sista steget är att skriva tillbaka förändringarna till disk. Du kan skriva över originalfilen eller skapa en ny – här genererar vi `output.pdf`.

```csharp
// Step 6: Save the updated PDF
string outputPath = @"YOUR_DIRECTORY\output.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved as {outputPath}");
```

*Vad du kan förvänta dig*: Öppna `output.pdf` i Adobe Reader eller någon annan läsare så bör du se en skarp röd rektangel förankrad i sidans nedre vänstra hörn på den första sidan.

![Diagram som visar rektangel tillagd i PDF](https://example.com/rectangle-diagram.png "exempel på hur man lägger till en form i pdf")

*Alt‑text*: "exempel på hur man lägger till en form i pdf – rektangel ritad på första sidan av en PDF‑fil"

## Steg 7: Fullt fungerande exempel (klar att kopiera och klistra in)

Nedan är hela programmet som du kan kompilera och köra omedelbart. Kom ihåg att ersätta `YOUR_DIRECTORY` med den faktiska sökvägen på din maskin.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;   // For color definitions

namespace PdfShapeDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the PDF document in C#
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document pdfDoc = new Document(inputPath);
            Console.WriteLine($"Loaded PDF with {pdfDoc.Pages.Count} page(s).");

            // Define the rectangle shape
            Rectangle rect = new Rectangle(0, 0, 200, 100)
            {
                FillColor = Color.Transparent,
                Border = new Border(BorderStyle.Solid, 2, Color.Red)
            };

            // Validate bounds on the first page
            if (!pdfDoc.Pages[1].ValidateShapeBounds(rect))
            {
                Console.WriteLine("Rectangle exceeds page dimensions – adjusting...");
                rect.Right = pdfDoc.Pages[1].PageInfo.Width - 10;
                rect.Top  = pdfDoc.Pages[1].PageInfo.Height - 10;
            }

            // Add the rectangle (how to add shape to pdf)
            pdfDoc.Pages[1].AddRectangle(rect);
            Console.WriteLine("Rectangle added to page 1.");

            // Save the modified PDF
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved as {outputPath}");
        }
    }
}
```

Kör programmet, öppna `output.pdf`, och du kommer att se den röda rektangeln exakt där vi placerade den. Om du behöver en annan form – ellips, linje eller polygon – byt bara `Rectangle` mot `Ellipse`, `Line` eller `Polygon` samtidigt som du behåller samma arbetsflöde. Det är i princip **hur man ritar former i pdf** med Aspose.

## Vanliga frågor & kantfall

### Vad gör jag om jag måste rita på flera sidor?
Loopa helt enkelt över `pdfDoc.Pages` och anropa `AddRectangle` (eller någon annan form) för varje sida. Kom ihåg att justera koordinaterna om sidorna har olika storlekar.

```csharp
foreach (Page page in pdfDoc.Pages)
{
    page.AddRectangle(rect);
}
```

### Kan jag fylla rektangeln med en färg?
Absolut. Ändra `FillColor` från `Transparent` till någon `Color` du föredrar, t.ex. `Color.Yellow`. Formen visas då som ett solid block.

### Fungerar detta med lösenordsskyddade PDF‑filer?
Aspose.PDF kan öppna krypterade filer om du anger lösenordet:

```csharp
Document pdfDoc = new Document(inputPath, new LoadOptions { Password = "mySecret" });
```

### Hur lägger jag till en rektangel med rundade hörn?
Använd klassen `RoundedRectangle` istället för `Rectangle`. Resten av stegen förblir identiska.

## Sammanfattning

Vi har gått igenom **hur man lägger till en form i PDF** med Aspose.PDF i C#. Processen kan sammanfattas till:

1. **Ladda pdf‑dokument i c#** – skapa ett `Document`‑objekt.  
2. **Definiera en rektangel** (eller någon annan form).  
3. **Validera gränser** för att undvika överspill.  
4. **Lägg till rektangeln** på mål‑sidan.  
5. **Spara** den modifierade filen.

Det är hela arbetsflödet för **aspose pdf add rectangle**, och du har nu en mall som du kan anpassa för cirklar, linjer eller egna polygoner.

## Vad blir nästa steg?

- **Utforska andra ritningsprimitiver**: `Ellipse`, `Line`, `Polygon`.  
- **Lägg till text‑annotationer** bredvid dina former för rikare interaktivitet.  
- **Kombinera med PDF‑formulärfält** om du bygger ett ifyllbart avtal.  
- **Kolla in Asposes PDF‑konverteringsfunktioner** för att omvandla dina annoterade PDF‑filer till bilder för förhandsgranskning.

Känn dig fri att experimentera – kanske rita ett vattenstämpel, markera en tabellcell eller avgränsa ett signaturfält. API:et är flexibelt, och nu känner du till grunderna.

Lycka till med kodandet, och må dina PDF‑filer alltid se precis ut som du tänkt dig!


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add Hyperlinks in PDFs Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/bookmarks-navigation/add-hyperlinks-pdf-aspose-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}