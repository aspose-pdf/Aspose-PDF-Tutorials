---
category: general
date: 2026-10-10
description: Lär dig hur du lägger till en rektangel i PDF, ritar en form på PDF och
  sparar den modifierade PDF-filen med Aspose.PDF. Inkluderar en steg‑för‑steg‑guide
  för att komma åt en specifik PDF-sida.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to PDF
- draw shape on PDF
- save modified PDF
- add shape to PDF
- access specific PDF page
language: sv
lastmod: 2026-10-10
og_description: Lägg till en rektangel i PDF med Aspose.PDF i C#. Den här handledningen
  visar hur du ritar en form i PDF, får åtkomst till en specifik PDF-sida och sparar
  den ändrade PDF-filen.
og_image_alt: Screenshot of a PDF page with a blue rectangle overlay created by Aspose.PDF
og_title: Lägg till rektangel i PDF med Aspose.PDF – komplett C#‑guide
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  headline: How to add rectangle to PDF with Aspose.PDF in C#
  type: TechArticle
- description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  name: How to add rectangle to PDF with Aspose.PDF in C#
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: What if the PDF has only one page?
    text: Attempting to access `pdfDocument.Pages[1]` throws an `ArgumentOutOfRangeException`.
      Guard against this by checking `pdfDocument.Pages.Count` before indexing.
  - name: How to add multiple rectangles on different pages?
    text: Repeat Steps 2‑4 for each target page, adjusting the rectangle’s coordinates
      as needed. You can place the logic inside a loop that iterates over `pdfDocument.Pages`.
  - name: Can I use other shapes such as circles or polygons?
    text: Yes. Aspose.PDF provides `Ellipse`, `Polygon`, and `Polyline` classes that
      follow the same pattern as `Rectangle`. Replace the `new Aspose.Pdf.Drawing.Rectangle`
      call with the desired shape class.
  - name: Does the library support PDFs with rotated pages?
    text: Aspose.PDF automatically respects page rotation when rendering shapes. The
      rectangle’s coordinates are interpreted in the page’s native coordinate system,
      so no extra transformation is required.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Hur man lägger till en rektangel i PDF med Aspose.PDF i C#
url: /sv/net/images-graphics/how-to-add-rectangle-to-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man lägger till rektangel i PDF med Aspose.PDF i C#

Om du behöver **lägga till rektangel i PDF**‑filer programatiskt visar den här guiden exakt hur du gör. Du lär dig att **rita form på PDF**, rikta in dig på en specifik sida och **spara modifierad PDF** utan fel.

Att arbeta med PDF‑dokument är ett vanligt krav för rapportering, fakturering eller dokumentanteckningar. I slutet av den här tutorialen kan du självsäkert **lägga till form i PDF**‑filer, hantera out‑of‑bounds‑fel och integrera lösningen i vilket .NET‑projekt som helst.

## Förutsättningar

Innan du börjar, se till att du har:

* .NET 6.0 SDK eller senare installerat  
* Visual Studio 2022 (eller någon C#‑IDE)  
* En Aspose.PDF för .NET‑licens eller en gratis utvärderingsnyckel – API‑et fungerar på samma sätt i båda lägena  
* En PDF‑fil med namnet `input.pdf` placerad i en mapp som du kan referera till från din kod  

Dessa objekt är de enda externa beroenden för exemplet.

## Steg 1: Installera Aspose.PDF NuGet‑paketet

Aspose.PDF‑biblioteket tillhandahåller `Document`, `Rectangle` och andra ritklasser du behöver.

```bash
dotnet add package Aspose.PDF
```

Att köra detta kommando lägger till den senaste stabila versionen av Aspose.PDF i ditt projekt, vilket gör PDF‑klasserna tillgängliga för kompilering.

## Steg 2: Ladda PDF‑dokumentet

Den första operationen är att ladda källfilen. Detta skapar en minnesrepresentation som du kan modifiera.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;

class PdfRectangleExample
{
    static void Main()
    {
        // Load the PDF document from disk
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

*Varför detta är viktigt*: Att ladda dokumentet ger dig åtkomst till dess sidcollection, vilket krävs för att **åtkomma specifik PDF‑sida** senare.

## Steg 3: Åtkom den andra sidan (noll‑baserat index)

PDF‑sidor indexeras från `0`. För att placera en rektangel på den andra sidan, hämta sidan med index `1`.

```csharp
        // Access the second page (pages are zero‑based)
        var page = pdfDocument.Pages[1];
```

Om dokumentet har färre än två sidor kastas ett `ArgumentOutOfRangeException`, vilket varnar dig om behovet av en guard‑clause i produktionskod.

## Steg 4: Skapa rektangelformen

Definiera rektangelns position och storlek med `Rectangle`‑strukturen, och omslut den sedan i ett Aspose‑ritobjekt.

```csharp
        // Define rectangle bounds: (x, y, width, height)
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            // Optional visual styling
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };
```

*Varför detta är viktigt*: Egenskaperna `BorderInfo` och `FillColor` låter dig **rita form på PDF** med en synlig kontur och valfri fyllning, vilket får rektangeln att sticka ut för läsarna.

## Steg 5: Lägg till rektangeln i sidans paragrafcollection

Aspose.PDF behandlar ritobjekt som paragraf‑element. Att lägga till rektangeln i sidans `Paragraphs`‑collection renderar den på sidan.

```csharp
        // Add the rectangle shape to the page
        page.Paragraphs.Add(rectangleShape);
```

Vid detta tillfälle innehåller PDF‑dokumentet i minnet den nya formen, men filen på disk är oförändrad tills du sparar den.

## Steg 6: Spara den modifierade PDF‑filen och hantera out‑of‑bounds‑fel

Att anropa `Save` skriver det uppdaterade dokumentet till en ny fil. Om rektangeln överskrider sidans dimensioner kastar Aspose ett `PdfException`. Att fånga detta undantag låter dig rapportera problemet på ett rent sätt.

```csharp
        try
        {
            // Save the altered PDF to a new file
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            // Handle shape that does not fit on the page
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

*Varför detta är viktigt*: `try/catch`‑blocket säkerställer att din applikation **sparar modifierad PDF** på ett säkert sätt, och felmeddelandet hjälper dig att justera rektangelns koordinater om det behövs.

## Fullt fungerande exempel

När alla steg sätts ihop får du det kompletta, körklara programmet:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;
using System.Drawing; // Required for Color

class PdfRectangleExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // Step 2: Access the second page (zero‑based)
        var page = pdfDocument.Pages[1];

        // Step 3: Create a rectangle shape positioned at (100,100) with width 300 and height 200
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };

        // Step 4: Add the rectangle shape to the page's paragraph collection
        page.Paragraphs.Add(rectangleShape);

        // Step 5: Save the modified PDF, handling out‑of‑bounds cases
        try
        {
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

### Förväntad output

Att köra programmet skriver ut:

```
PDF saved successfully with rectangle added.
```

och skapar `output.pdf` som visar det ursprungliga innehållet plus en blå rektangel på de angivna koordinaterna på den andra sidan.

Om rektangeln vore större än sidan skulle du se:

```
Shape out of bounds: The shape exceeds page margins.
```

## Vanliga frågor och kantfall

### Vad händer om PDF‑filen bara har en sida?

Att försöka åtkomma `pdfDocument.Pages[1]` kastar ett `ArgumentOutOfRangeException`. Skydda mot detta genom att kontrollera `pdfDocument.Pages.Count` innan du indexerar.

```csharp
if (pdfDocument.Pages.Count < 2)
{
    Console.WriteLine("Document does not contain a second page.");
    return;
}
```

### Hur lägger jag till flera rektanglar på olika sidor?

Upprepa Steg 2‑4 för varje mål‑sida och justera rektangelns koordinater efter behov. Du kan placera logiken i en loop som itererar över `pdfDocument.Pages`.

### Kan jag använda andra former som cirklar eller polygoner?

Ja. Aspose.PDF tillhandahåller `Ellipse`, `Polygon` och `Polyline`‑klasser som följer samma mönster som `Rectangle`. Byt ut anropet `new Aspose.Pdf.Drawing.Rectangle` mot den önskade formklassen.

### Stöder biblioteket PDF‑filer med roterade sidor?

Aspose.PDF respekterar automatiskt sidrotation när former renderas. Rektangelns koordinater tolkas i sidans inhemska koordinatsystem, så ingen extra transformation krävs.

## Prestandaöverväganden

* **Minnesanvändning** – Att ladda en stor PDF (hundratals megabyte) förbrukar proportionellt minne. Om du bara behöver modifiera en enda sida, överväg att använda `PdfFileInfo` för att extrahera den sidan, ändra den och sedan slå ihop den igen.  
* **Batch‑bearbetning** – När du lägger till former i många dokument, återanvänd en enda `License`‑instans för att undvika upprepad licensvalideringskostnad.

## Nästa steg

Nu när du kan **lägga till rektangel i PDF**, utforska dessa relaterade ämnen:

* **draw shape on PDF** – lär dig att överlagra text, bilder och vattenstämplar  
* **add shape to PDF** – kombinera flera former till ett enda annoteringslager  
* **save modified PDF** – använd strömmar (`MemoryStream`) för att returnera PDF‑filer direkt från webb‑API:er  
* **access specific PDF page** – implementera sid‑intervallsextraktion för anpassade rapporter  

Experimentera med olika färger, linjestilar och transparensnivåer för att matcha dina varumärkesriktlinjer.

---

*Glad kodning! Om den här tutorialen hjälpte dig att **lägga till rektangel i PDF**, överväg att dela den med kollegor eller bidra med förbättringar tillbaka till communityn.*

## Vad bör du lära dig härnäst?

De följande tutorialerna täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide](/pdf/english/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [How to Add a Line Object in PDF Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}