---
category: general
date: 2026-11-12
description: Lär dig hur du ändrar PDF‑opacitet med Aspose.Pdf, lägger till transparens,
  ställer in blandningsläge och sparar den modifierade PDF‑filen i C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF opacity
- how to add transparency
- save modified PDF
- how to set blend mode
- set fill opacity
language: sv
lastmod: 2026-11-12
og_description: Ändra PDF-opacitet med Aspose.Pdf, lär dig hur du lägger till transparens,
  ställer in blandningsläge och sparar modifierade PDF-filer i C#.
og_image_alt: Screenshot of a PDF page with altered opacity using Aspose.Pdf
og_title: Ändra PDF-opacitet med Aspose.Pdf – lägg till transparens och spara
schemas:
- author: Aspose
  dateModified: '2026-11-12'
  description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  headline: Change PDF opacity with Aspose.Pdf and save the file
  type: TechArticle
- description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  name: Change PDF opacity with Aspose.Pdf and save the file
  steps:
  - name: Load the PDF document
    text: Start by creating a `Document` instance that points to your source file.
      The constructor reads the entire PDF into memory, allowing you to manipulate
      its internal objects.
  - name: Access the first page’s resources
    text: Each PDF page stores a *resource dictionary* that holds objects such as
      fonts, images, and graphics states. You need to edit this dictionary to inject
      a new `ExtGState` entry.
  - name: Ensure an ExtGState dictionary exists
    text: The `ExtGState` dictionary holds custom graphics states. If it does not
      exist, the code creates one automatically.
  - name: Define a new graphics state (ExtGState)
    text: A graphics state defines how drawing operations behave. The following dictionary
      sets stroke opacity (`CA`), fill opacity (`ca`), and blend mode (`BM`).
  - name: Register the graphics state in the resource dictionary
    text: Give the new state a name (e.g., `GS0`) and add it to the `ExtGState` dictionary.
      This name will be referenced later in the page content stream.
  - name: Apply the graphics state to page content
    text: To actually see the opacity effect, insert the `/GS0 gs` operator before
      the drawing commands you want to affect. The example below draws a semi‑transparent
      rectangle.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The `Save` method overwrites
      the target file or creates a new one if it does not exist.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Ändra PDF‑opacitet med Aspose.Pdf och spara filen
url: /sv/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-and-save-the-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ändra PDF-opacitet med Aspose.Pdf och spara filen

Om du behöver **ändra PDF-opacitet** i ett dokument, erbjuder Aspose.Pdf ett enkelt API för att justera både linjens och fyllningens transparens. Denna handledning visar exakt **hur man lägger till transparens**, **hur man ställer in blandningsläge**, och **sparar modifierade PDF**-filer med bara några rader C#-kod.

Du kommer att gå igenom varje steg—från att ladda en befintlig PDF till att definiera ett nytt grafikstatus och spara ändringarna. I slutet av den här guiden kan du:

* Minska synligheten för vektorgrafik eller bilder.
* Använd ett anpassat blandningsläge såsom *Normal* eller *Multiply*.
* Exportera den uppdaterade filen utan att förlora något annat innehåll.

Det enda förutsättningen är en fungerande .NET‑utvecklingsmiljö och en referens till Aspose.Pdf‑biblioteket (version 23.9 eller senare). Inga externa verktyg krävs.

## Prerequisites

| Krav | Varför det är viktigt |
|------|-----------------------|
| .NET 6.0 SDK eller senare | Säkerställer kompatibilitet med de senaste Aspose.Pdf‑API:erna. |
| Aspose.Pdf för .NET NuGet‑paket | Tillhandahåller `Document`, `CosPdfDictionary` och relaterade klasser som används i koden. |
| En PDF‑fil att redigera (t.ex. `input.pdf`) | Fungerar som källa för opacitetsändringar. |

Installera NuGet‑paketet med:

```bash
dotnet add package Aspose.Pdf
```

## Ändra PDF-opacitet med Aspose.Pdf

### Steg 1: Ladda PDF‑dokumentet

Börja med att skapa en `Document`‑instans som pekar på din källfil. Konstruktorn läser in hela PDF‑filen i minnet, vilket gör att du kan manipulera dess interna objekt.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;

// Load the existing PDF
var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");
```

> **Varför detta steg?** Att ladda filen skapar en manipulerbar objektmodell. Alla efterföljande ändringar sker på denna representation i minnet, vilket säkerställer att originalfilen förblir orörd tills du explicit sparar.

### Steg 2: Åtkomst till den första sidans resurser

Varje PDF‑sida lagrar en *resursordbok* som innehåller objekt som teckensnitt, bilder och grafikstatusar. Du måste redigera denna ordbok för att infoga ett nytt `ExtGState`‑element.

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor simplifies access to the page's resource dictionary
var resourcesEditor = new DictionaryEditor(page.Resources);
```

> **Tips:** Om din PDF innehåller flera sidor som behöver samma opacitet, upprepa detta steg för varje sida eller dela ett enda `ExtGState` över sidor.

### Steg 3: Säkerställ att en ExtGState‑ordbok finns

`ExtGState`‑ordboken innehåller anpassade grafikstatusar. Om den inte finns skapar koden en automatiskt.

```csharp
// Get or create the ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                     ?? new CosPdfDictionary(pdfDoc);
resourcesEditor["ExtGState"] = extGStateDict;
```

> **Varför detta steg?** Utan en `ExtGState`‑behållare skulle alla försök att referera till en ny grafikstatus misslyckas, vilket resulterar i en PDF som ignorerar dina opacitetsinställningar.

### Steg 4: Definiera en ny grafikstatus (ExtGState)

En grafikstatus definierar hur ritoperationer beter sig. Följande ordbok sätter linjeopacitet (`CA`), fyllningsopacitet (`ca`) och blandningsläge (`BM`).

```csharp
// Create an empty dictionary for the new graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Set desired parameters
var parameters = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (1 = opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (0.5 = 50% transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var param in parameters)
    newGraphicsState.Add(param);
```

> **Hur man sätter fyllningsopacitet:** `ca`‑elementet styr opaciteten för fyllda former (text, banor). Justera det numeriska värdet mellan `0` (helt transparent) och `1` (helt ogenomskinlig) för att uppfylla dina designkrav.

> **Hur man sätter blandningsläge:** `BM`‑elementet väljer sammansättningsalgoritmen. Vanliga värden inkluderar `Normal`, `Multiply`, `Screen` och `Overlay`. Välj det som matchar din visuella avsikt.

### Steg 5: Registrera grafikstatusen i resursordboken

Ge den nya statusen ett namn (t.ex. `GS0`) och lägg till den i `ExtGState`‑ordboken. Detta namn kommer att refereras senare i sidans innehållsström.

```csharp
// Add the graphics state with a symbolic name
extGStateDict.Add("GS0", newGraphicsState);
```

> **Pro‑tips:** Använd en namngivningskonvention som `GS0`, `GS1`, … när du skapar flera statusar. Det förhindrar namnkonflikter och underlättar felsökning.

### Steg 6: Tillämpa grafikstatusen på sidinnehållet

För att faktiskt se opacitets‑effekten, infoga operatorn `/GS0 gs` före de ritkommandon du vill påverka. Exemplet nedan ritar en halvtransparent rektangel.

```csharp
// Build a content stream that uses the new graphics state
var content = new MemoryStream();
var writer = new StreamWriter(content);

// Activate the graphics state
writer.WriteLine("q");                 // Save graphics state
writer.WriteLine("/GS0 gs");           // Apply custom ExtGState
writer.WriteLine("0.2 0.5 0.8 rg");    // Set fill color (RGB)
writer.WriteLine("100 500 200 100 re"); // Rectangle (x y width height)
writer.WriteLine("f");                 // Fill rectangle
writer.WriteLine("Q");                 // Restore graphics state
writer.Flush();

content.Position = 0;
page.Contents.Add(new ContentStream(content));
```

> **Varför `q`‑ och `Q`‑operatorerna?** De lägger till och tar bort grafikstatus‑stacken, vilket säkerställer att opacitetsändringen endast påverkar rektangeln och inte resten av sidan.

### Steg 7: Spara den modifierade PDF‑filen

Slutligen, skriv det uppdaterade dokumentet till disk. `Save`‑metoden skriver över målfilen eller skapar en ny om den inte finns.

```csharp
// Persist the changes
pdfDoc.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **Hur man sparar modifierad PDF:** `Save`‑anropet skriver alla ändringar i minnet, inklusive den nya `ExtGState`, till den angivna sökvägen. Du kan också strömma resultatet till en `MemoryStream` för webb‑svar.

## Fullständigt fungerande exempel

Nedan är ett enda, självständigt program som innehåller alla steg som beskrivits ovan. Kopiera det till en konsolapplikation och kör det för att verifiera opacitetsändringen.



## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Hur man sparar modifierad PDF med Aspose.Pdf och lägger till transparens](/pdf/english/net/document-manipulation/how-to-save-modified-pdf-with-aspose-pdf-and-add-transparenc/)
- [Hur man lägger till transparens i PDF med Aspose.PDF i C#](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [Hur man lägger till grafikstatus i PDF och kontrollerar transparens med Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}