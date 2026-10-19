---
category: general
date: 2026-09-05
description: Skapa PDF‑dokument i C# genom att lägga till en tom sida, rita en rektangel
  och spara PDF‑filen. Följ ett steg‑för‑steg Aspose.PDF‑exempel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add blank page pdf
- draw rectangle pdf
- save pdf file
- how to add rectangle
language: sv
lastmod: 2026-09-05
og_description: Skapa PDF-dokument i C# genom att lägga till en tom sida, rita en
  rektangel och spara PDF-filen. Följ detta kompletta exempel med Aspose.PDF.
og_image_alt: Screenshot showing a PDF document with a drawn rectangle on a blank
  page
og_title: Skapa PDF-dokument med tom sida och rektangel – C#‑guide
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  headline: How to create PDF document with a blank page and rectangle
  type: TechArticle
- description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  name: How to create PDF document with a blank page and rectangle
  steps:
  - name: 'Edge case: custom page size'
    text: 'If your layout requires a 6 × 9 inch page, replace the default call with:'
  - name: 'Pro tip: styling the rectangle'
    text: 'You can change the stroke color and line width:'
  - name: 'Edge case: overwriting existing files'
    text: 'Aspose.PDF overwrites an existing file by default. To protect previous
      outputs, check for file existence first:'
  - name: Expected output
    text: Running the program creates a single‑page PDF. When you open `output.pdf`
      you will see a blank white page with a red rectangle positioned 100 points from
      the left and bottom edges, measuring 200 × 200 points.
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
- PDF generation
title: Hur man skapar PDF-dokument med en tom sida och en rektangel
url: /sv/net/document-creation/how-to-create-pdf-document-with-a-blank-page-and-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar PDF-dokument med en tom sida och rektangel

Om du behöver **create PDF document** programatiskt, visar den här guiden en komplett lösning i C#. Du kommer att lära dig hur du lägger till en tom sida, ritar en rektangel på den sidan och slutligen sparar PDF-filen. Exemplet använder Aspose.PDF-biblioteket, som fungerar med .NET 6+ och .NET Framework 4.5+.

Att lägga till en tom sida och rita former är ett vanligt krav för fakturor, certifikat eller anpassade rapporter. I slutet av den här handledningen har du ett körbart projekt som producerar en PDF som innehåller en enda rektangel placerad på (100, 100) med en storlek på 200 × 200 punkter.

## Förutsättningar

* Visual Studio 2022 (eller någon C#-IDE)
* .NET 6 SDK eller .NET Framework 4.5+
* Aspose.PDF for .NET NuGet-paket  
  ```bash
  dotnet add package Aspose.PDF
  ```
* Skrivbehörighet till utmatningskatalogen

Ingen ytterligare konfiguration krävs; koden körs direkt.

## Skapa PDF-dokument – översikt

Hela processen består av fyra logiska steg:

1. **Instantiate** ett `Document`-objekt – detta representerar PDF-filen.
2. **Add a blank page** – sidan ger en duk för ritning.
3. **Draw a rectangle** – ett `Path`-objekt definierar formen.
4. **Save the PDF file** – sparar dokumentet till disk.

Varje steg är isolerat i sin egen sektion så att du kan återanvända eller ersätta delar vid behov.

![Diagram av en PDF med en rektangel på en tom sida](https://example.com/placeholder-image.png){.img-fluid alt="Skärmdump som visar ett PDF-dokument med en ritad rektangel på en tom sida"}

## Lägg till tom sida pdf

En PDF måste innehålla minst en sida innan någon grafik kan placeras. Metoden `Pages.Add()` skapar en tom sida med standarddimensioner (A4). Om du behöver en annan storlek, skicka ett `PageSize`-argument.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();

// Step 2: Add a blank page to the document
Page pdfPage = pdfDocument.Pages.Add();   // adds an A4 page by default
```

*Varför detta steg är viktigt* – Sidobjektet innehåller samlingar för text, bilder och vektorgrafik. Utan en sida skulle varje försök att lägga till en rektangel resultera i ett undantag.

### Kantfall: anpassad sidstorlek

Om din layout kräver en 6 × 9 tumssida, ersätt standardanropet med:

```csharp
var pageSize = new Size(432, 648); // 72 points per inch
Page pdfPage = pdfDocument.Pages.Add(pageSize);
```

## Rita rektangel pdf

Att rita en rektangel handlar om att skapa en `Rectangle`-geometri och omsluta den i ett `Path`. Anropet `ValidateBounds()` säkerställer att formen passar inom sidmarginalerna, vilket förhindrar beskärning.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

// Step 4: Add the rectangle to the page contents
Path rectanglePath = new Path(shapeRect).ValidateBounds();
pdfPage.Contents.Add(rectanglePath);
```

*Varför detta steg är viktigt* – `Path`-objektet är den lågnivå vektorprimitive som används av Aspose.PDF. Genom att validera gränser undviker du körningstidfel när rektangeln överskrider sidgränserna.

### Proffstips: stilisering av rektangeln

Du kan ändra linjefärgen och linjebredden:

```csharp
rectanglePath.GraphInfo = new GraphInfo
{
    StrokeColor = Color.Red,
    LineWidth = 2
};
```

Detta ger en röd kontur med en tjocklek på 2 punkter.

## Spara pdf-fil

Att spara dokumentet färdigställer filen på disken. Metoden `Save` accepterar en filsökväg eller en ström. Att ange en absolut sökväg gör platsen tydlig, vilket är användbart för automatiseringsskript.

```csharp
// Step 5: Save the PDF to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

*Varför detta steg är viktigt* – Sparande är den enda punkten där den minnesbaserade representationen blir en fysisk fil. Om du behöver returnera PDF:en från ett webb‑API, ersätt filsökvägen med en `MemoryStream`.

### Kantfall: skriva över befintliga filer

Aspose.PDF skriver över en befintlig fil som standard. För att skydda tidigare utdata, kontrollera först om filen finns:

```csharp
if (File.Exists(outputPath))
{
    File.Delete(outputPath);
}
pdfDocument.Save(outputPath);
```

## Hur man lägger till rektangel – bästa praxis

* **Keep coordinates within the page margins** – använd `ValidateBounds()` eller beräkna marginaler manuellt.
* **Reuse `GraphInfo` objects** när du ritar flera former; detta minskar minnesallokering.
* **Dispose of the `Document` object** (som visas med `using var`) för att snabbt frigöra inhemska resurser.
* **Test with different DPI settings** om du senare bäddar in rasterbilder; vektorformer som rektanglar förblir skarpa i alla upplösningar.

## Komplett fungerande exempel

Nedan är hela programmet som du kan kopiera in i en konsolapplikation. Det kompileras utan ändringar och producerar `output.pdf` i projektmappen.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using var pdfDocument = new Document();

        // Add a blank page to the document
        Page pdfPage = pdfDocument.Pages.Add();

        // Define a rectangle shape (x, y, width, height)
        Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

        // Create a path for the rectangle and validate its bounds
        Path rectanglePath = new Path(shapeRect).ValidateBounds();

        // Optional: style the rectangle (red outline, 2‑pt width)
        rectanglePath.GraphInfo = new GraphInfo
        {
            StrokeColor = Color.Red,
            LineWidth = 2
        };

        // Add the rectangle to the page contents
        pdfPage.Contents.Add(rectanglePath);

        // Determine output path
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");

        // Ensure no leftover file blocks the save operation
        if (File.Exists(outputPath))
        {
            File.Delete(outputPath);
        }

        // Save the PDF to a file
        pdfDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

### Förväntad output

När programmet körs skapas en PDF med en enda sida. När du öppnar `output.pdf` kommer du att se en tom vit sida med en röd rektangel placerad 100 punkter från vänster- och bottenkanten, med måtten 200 × 200 punkter.

## Slutsats

Du vet nu hur du **create PDF document**, **add blank page pdf**, **draw rectangle pdf**, och **save pdf file** med Aspose.PDF i C#. Exemplet täcker de viktigaste API-anropen, förklarar varför varje anrop behövs och ger tips för vanliga variationer såsom anpassade sidstorlekar eller stilisering av rektangel.

Nästa steg, utforska relaterade ämnen som **adding text**, **embedding images**, eller **creating multi‑page reports**. Samma mönster—instantiating a `Document`, manipulera sidor, lägga till vektor- eller rasterinnehåll, sedan `Save`—gäller för alla dessa scenarier. Känn dig fri att experimentera med olika former, färger och sidlayouter för att passa ditt projekts behov.

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa PDF-dokument C# – Lägg till sida, rita rektangel & spara](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)
- [Skapa PDF-dokument med Aspose.PDF – Steg‑för‑steg‑guide](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Skapa PDF-dokument med Aspose – Lägg till sida, textruta och formulär](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}