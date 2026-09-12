---
category: general
date: 2026-09-12
description: Lär dig hur du lägger till transparens i PDF, ritar en rektangel i PDF
  och sparar PDF med transparens med Aspose.PDF i C# – steg‑för‑steg‑guide.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- draw rectangle on pdf
- save pdf with transparency
language: sv
lastmod: 2026-09-12
og_description: Lägg till transparens i PDF, rita en rektangel på PDF och spara PDF
  med transparens med Aspose.PDF i C#. Följ den här kompletta handledningen.
og_image_alt: Screenshot of a PDF page showing a semi‑transparent rectangle drawn
  with Aspose.PDF
og_title: Lägg till transparens i PDF och rita en rektangel i PDF – komplett C#‑guide
schemas:
- author: Aspose
  dateModified: '2026-09-12'
  description: Learn how to add transparency to PDF, draw a rectangle on PDF, and
    save PDF with transparency using Aspose.PDF in C# – step‑by‑step guide.
  headline: How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Hur man lägger till transparens i PDF och ritar en rektangel i PDF med Aspose.PDF
url: /sv/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man lägger till transparens i PDF och ritar en rektangel i PDF med Aspose.PDF

Om du behöver **add transparency to PDF**-filer, visar den här guiden exakt hur du gör det i C#. Du kommer också att lära dig hur du **draw rectangle on PDF** och slutligen **save PDF with transparency** så att resultatet kan återanvändas i rapporter, fakturor eller någon dokument‑automatiseringsarbetsflöde.

I den här handledningen kommer du:

* Ladda ett befintligt PDF-dokument.
* Skapa ett anpassat graphics state som definierar stroke- och fill-opacitet.
* Applicera det graphics state på canvas och rita en rektangel.
* Spara den modifierade filen samtidigt som transparensinställningarna bevaras.

Inga externa verktyg krävs utöver Aspose.PDF för .NET-biblioteket, och varje kodrad förklaras så att du förstår *varför* varje steg är viktigt.

## Förutsättningar

* .NET 6.0 eller senare (koden fungerar också med .NET Framework 4.7+).
* En licensierad eller utvärderingskopi av **Aspose.PDF for .NET**. Installera den via NuGet:

```bash
dotnet add package Aspose.Pdf
```

* En inmatnings‑PDF (`input.pdf`) placerad i en mapp som du kan referera till från ditt projekt.

## Steg 1: Ladda PDF-dokumentet

Den första operationen är att öppna källfilen. Att använda `using`‑satsen garanterar att dokumentet tas bort på rätt sätt, vilket förhindrar fil‑låsning problem senare när du försöker spara.

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";
using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

*Varför detta är viktigt*: Att ladda dokumentet ger dig åtkomst till sidkollektionen, resursordböckerna och canvas‑objekten som krävs för ritning.

## Steg 2: Åtkomst till den första sidans resursordbok

Varje PDF-sida har en **resource dictionary** som lagrar objekt som teckensnitt, bilder och graphics states. För att införa en ny transparensinställning måste vi redigera `ExtGState`‑posten.

```csharp
// Step 2: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

*Varför detta är viktigt*: `DictionaryEditor` låter oss läsa och modifiera låg‑nivå PDF‑objekt utan att bryta dokumentstrukturen.

## Steg 3: Skapa ett anpassat graphics state med transparensvärden

Ett graphics state (`ExtGState`) styr hur ritningsoperationer renderas. Vi definierar två opacitetsparametrar:

* **CA** – stroke‑opacitet (konturen av former).
* **ca** – fill‑opacitet (formen inuti).

Vi sätter också blandningsläget (`BM`) till “Normal”, vilket är den vanligaste sammanslagningsoperationen.

```csharp
// Step 3: Create a custom graphics state (ExtGState) with transparency settings
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
var customGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "CA", new Aspose.Pdf.Cos.CosPdfNumber(1)),          // stroke opacity = 100 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),        // fill opacity = 50 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))      // normal blend mode
};

foreach (var p in parameters)
    customGs.Add(p);

// Register the new graphics state under the name "GS0"
extGStateDict.Add("GS0", customGs);
```

*Varför detta är viktigt*: Genom att lägga till `GS0` i `ExtGState`‑ordboken skapar vi en återanvändbar referens som canvas kan aktivera innan ritning. Fill‑opaciteten `0.5` gör rektangeln halvtransparent, vilket uppnår målet **add transparency to PDF**.

## Steg 4: Applicera graphics state och rita en rektangel

Nu instruerar vi sidans canvas att använda det graphics state vi just skapade, och sedan ritar vi en rektangel. Koordinaterna följer PDF:s koordinatsystem (ursprung i nedre vänstra hörnet).

```csharp
// Step 4: Apply the custom graphics state and draw a rectangle
var canvas = firstPage.Canvas;

// Activate the transparency graphics state
canvas.SetGraphicsState("GS0");

// Draw a rectangle from (100, 500) to (200, 600)
canvas.Rectangle(100, 500, 200, 600);

// Render the rectangle outline using the current graphics state
canvas.Stroke();
```

*Varför detta är viktigt*: `SetGraphicsState("GS0")` byter ritningskontexten till de tidigare definierade transparensinställningarna. `Rectangle`‑metoden definierar formen, och `Stroke` renderar konturen med den angivna opaciteten. Om du också vill ha en fylld rektangel, ersätt `Stroke()` med `FillAndStroke()`.

## Steg 5: Spara den modifierade PDF:n samtidigt som transparensen bevaras

Slutligen skriver vi dokumentet tillbaka till disk. Utdatafilen innehåller det nya graphics state, den ritade rektangeln och transparensinformationen.

```csharp
// Step 5: Save the modified PDF
string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
pdfDocument.Save(outputPath);
```

*Varför detta är viktigt*: Att spara dokumentet slutför alla ändringar. Den resulterande filen kan öppnas i vilken PDF‑visare som helst, och rektangeln kommer att visas med 50 % fill‑opacitet.

### Förväntat resultat

När du öppnar `output_with_extgstate.pdf` bör du se en rektangel vars kant är helt ogenomskinlig och vars inre är halvtransparent, så att underliggande sidinnehåll kan visas igenom.

## Kantfall och praktiska tips

| Situation | Recommended adjustment |
|-----------|------------------------|
| **Flera sidor** | Loop over `pdfDocument.Pages` and repeat steps 2‑4 for each target page. |
| **Olika opacitetsvärden** | Change the `CosPdfNumber` values for `CA` (stroke) and `ca` (fill) to any number between `0` (fully transparent) and `1` (fully opaque). |
| **Anpassade blandningslägen** | Replace `"Normal"` with `"Multiply"`, `"Screen"`, or any PDF‑standard blend mode supported by your viewer. |
| **Fylld rektangel** | Call `canvas.FillAndStroke()` instead of `canvas.Stroke()` to apply both fill and outline. |
| **Återanvända samma graphics state** | You can call `canvas.SetGraphicsState("GS0")` before drawing any number of shapes on the same page. |

**Pro tip:** Inspektera alltid resursordboken efter att ha lagt till ett nytt `ExtGState`. Om ordboken inte finns, skapa den först:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
    resourcesEditor.Add("ExtGState", new Aspose.Pdf.Cos.CosPdfDictionary(pdfDocument));
```

## Fullständigt, körbart exempel

Nedan är ett fristående program som du kan kopiera in i en konsolapplikation och köra omedelbart (byt ut `YOUR_DIRECTORY` mot en faktisk sökväg).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF document
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Access the first page’s resources
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        if (!resourcesEditor.ContainsKey("ExtGState"))
            resourcesEditor.Add("ExtGState", new CosPdfDictionary(pdfDocument));

        // 3️⃣ Create a custom graphics state with transparency
        var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        var customGs = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };

        foreach (var p in parameters)
            customGs.Add(p);

        extGStateDict.Add("GS0", customGs);

        // 4️⃣ Apply the graphics state and draw a rectangle
        var canvas = firstPage.Canvas;
        canvas.SetGraphicsState("GS0");
        canvas.Rectangle(100, 500, 200, 600);
        canvas.Stroke(); // use FillAndStroke() for a filled shape

        // 5️⃣ Save the PDF with transparency
        string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine("PDF saved with a transparent rectangle at: " + outputPath);
    }
}
```

När programmet körs produceras `output_with_extgstate.pdf`, vilket demonstrerar **add transparency to PDF**, **draw rectangle on PDF**, och **save PDF with transparency** i ett och samma flöde.

## Slutsats

Du vet nu hur du **add transparency to PDF**‑filer, **draw rectangle on PDF**, och **save PDF with transparency** med Aspose.PDF för .NET. Processen kretsar kring att skapa ett anpassat `ExtGState`, applicera det på canvas och spara ändringarna. Med dessa byggstenar kan du utöka tekniken till andra former, flera sidor eller dynamiska opacitetsvärden.

**Nästa steg**

* Utforska andra ritningsprimitive såsom `canvas.Ellipse`, `canvas.Path` eller `canvas.TextFragment` medan du återanvänder samma graphics state.
* Kombinera transparens med bildöverlägg för att skapa vattenstämplar (`canvas.Image` + custom `ExtGState`).
* Granska Aspose.PDF-dokumentationen om **graphics state parameters** för avancerade sammanslagningseffekter.

Lycka till med kodandet, och njut av den visuella flexibiliteten som transparens ger dina PDF‑arbetsflöden!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man skapar PDF i C# – Lägg till sida, rita rektangel & spara](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [Hur man lägger till ett linjeobjekt i PDF med Aspose.PDF för .NET: En steg‑för‑steg‑guide](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Lägg till bildstämplar i PDF med Aspose.PDF för .NET: En steg‑för‑steg‑guide](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}