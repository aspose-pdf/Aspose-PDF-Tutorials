---
category: general
date: 2026-10-07
description: Lägg till grafikstatus i PDF med Aspose.Pdf i C# för att ändra PDF‑transparensen.
  Följ den här steg‑för‑steg‑guiden för att bädda in anpassade grafikstatusar och
  kontrollera opaciteten.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- modify pdf transparency
language: sv
lastmod: 2026-10-07
og_description: Lägg till grafikstatus i PDF med Aspose.Pdf i C#. Lär dig hur du ändrar
  PDF-transparensen genom att skapa en anpassad grafikstatusordlista.
og_image_alt: Screenshot showing the add graphics state pdf code editor in Visual
  Studio
og_title: Lägg till grafikstatus i PDF med Aspose.Pdf – kontrollera PDF-transparens
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Add graphics state pdf using Aspose.Pdf in C# to modify PDF transparency.
    Follow this step‑by‑step guide to embed custom graphics states and control opacity.
  headline: Add graphics state pdf with Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Lägg till grafikstatus i PDF med Aspose.Pdf i C#
url: /sv/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till grafikstatus pdf med Aspose.Pdf i C#

Om du behöver **add graphics state pdf** till ett dokument, visar den här handledningen exakt hur du gör det med Aspose.Pdf för .NET. I slutet av guiden kommer du också att veta hur du **modify PDF transparency**, så att du kan ange anpassade opacitetsvärden för alla ritningsoperationer.

Att arbeta med PDF-grafikstatusar låter dig styra parametrar som linjebredd, blandningsläge och, viktigast för den här artikeln, transparensen i innehållet. Stegen nedan är skrivna för utvecklare som är bekväma med C# och vill ha en färdig‑till‑körning‑lösning utan att gräva igenom den officiella SDK-dokumentationen.

## Vad du kommer att lära dig

* Hur man skapar en ny grafikstatus‑ordbok och fyller den med `CA`, `ca` och `BM`‑poster.  
* Hur man infogar den ordboken i sidans `ExtGState`‑resurs så att PDF‑filen känner igen den.  
* Hur `ca` (stroke) och `CA` (fill)‑värdena påverkar **modify PDF transparency** för efterföljande ritningskommandon.  
* Vanliga fallgropar såsom namnkonflikter och versionskompatibilitet, samt pro‑tips för att utöka grafikstatusen senare.

**Förutsättningar**

* .NET 6.0 eller senare (koden fungerar också med .NET Framework 4.7+).  
* En giltig Aspose.Pdf för .NET‑licens (den kostnadsfria utvärderingen fungerar för testning).  
* Visual Studio 2022 eller någon C#‑IDE du föredrar.  

---

## Steg 1: Installera Aspose.Pdf för .NET

Lägg till NuGet‑paketet i ditt projekt:

```bash
dotnet add package Aspose.Pdf
```

Paketet innehåller `Aspose.Pdf`‑namnutrymmet som tillhandahåller klasserna `Document`, `DictionaryEditor` och `CosPdfDictionary` som används senare.

> **Pro tip:** Om du planerar att bearbeta många PDF‑filer i ett batch‑jobb, aktivera **License** tidigt i `Program.cs` för att undvika utvärderingsvattenstämpeln.

```csharp
// Apply your license (optional for evaluation)
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Aspose.Pdf.lic");
```

## Steg 2: Definiera in- och utdata‑sökvägar

Du måste peka SDK:n på en befintlig PDF (`input.pdf`) och ange var den modifierade filen ska sparas (`output.pdf`).

```csharp
// Define input and output PDF file paths
string inputPath = @"C:\MyPdfs\input.pdf";
string outputPath = @"C:\MyPdfs\output.pdf";
```

> **Varför detta är viktigt:** Att använda absoluta sökvägar förhindrar att SDK:n letar i fel arbetskatalog, vilket är en vanlig källa till `FileNotFoundException`.

## Steg 3: Öppna PDF‑filen och lokalisera den första sidans resurser

`ExtGState`‑ordboken finns i varje sidas resursordbok. Vi kommer att redigera den första sidan för enkelhetens skull, men samma metod fungerar för vilket sidindex som helst.

```csharp
using (var pdfDocument = new Aspose.Pdf.Document(inputPath))
{
    // Get the first page (pages are 1‑based)
    var firstPage = pdfDocument.Pages[1];

    // Access the page’s resource dictionary via DictionaryEditor
    var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);

    // Retrieve (or create) the ExtGState entry
    var extGStateDict = resourcesEditor["ExtGState"]
        .ToCosPdfDictionary(); // Throws if ExtGState does not exist
```

**Edge case:** Om sidan saknar `ExtGState`‑post, måste du skapa den:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
{
    var emptyDict = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", emptyDict);
    extGStateDict = emptyDict;
}
```

## Steg 4: Bygg en ny grafikstatus‑ordbok

En grafikstatus är en samling nyckel/värde‑par som beskriver hur ritningsoperationer beter sig. För transparens behöver vi tre nycklar:

| Nyckel | Betydelse | Typiskt värde |
|-----|---------|---------------|
| `CA` | Fyllningsopacitet (0 = transparent, 1 = opak) | `1` (fully opaque) |
| `ca` | Linjeopacitet (samma skala) | `0.5` (50 % transparent) |
| `BM` | Blandningsläge (t.ex. `Normal`, `Multiply`) | `Normal` |

```csharp
    // Create an empty dictionary that will hold the graphics state
    var newGraphicsState = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Populate the dictionary with transparency and blend mode entries
    var graphicsStateEntries = new[]
    {
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "CA", new Aspose.Pdf.CosPdfNumber(1)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "ca", new Aspose.Pdf.CosPdfNumber(0.5)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "BM", new Aspose.Pdf.CosPdfName("Normal"))
    };

    foreach (var entry in graphicsStateEntries)
        newGraphicsState.Add(entry);
```

**Varför dessa värden?**  
`ca = 0.5` gör att alla strokade banor (linjer, kanter) visas med 50 % opacitet, medan `CA = 1` lämnar fyllda former helt opaka. Justera båda siffrorna för att uppnå exakt **modify PDF transparency**‑effekt som du behöver.

## Steg 5: Infoga grafikstatusen i ExtGState‑ordboken

Du måste ge den nya statusen ett unikt namn (t.ex. `GS0`). Om namnet redan finns, kommer Aspose.Pdf att skriva över den befintliga posten, vilket kan bryta annat innehåll som är beroende av den.

```csharp
    // Add the new graphics state under a custom name
    const string stateName = "GS0";

    // Ensure we don’t clash with an existing entry
    if (extGStateDict.ContainsKey(stateName))
        extGStateDict.Remove(stateName);

    extGStateDict.Add(stateName, newGraphicsState);
```

Nu känner sidans resurser till `GS0`. För att faktiskt använda den skulle du referera till grafikstatusen i ett innehållsflöde via `gs`‑operatorn (t.ex. `GS0 gs`). Aspose.Pdf låter dig injicera råa PDF‑operatorer om du behöver rita anpassade former.

## Steg 6: Spara den modifierade PDF‑filen

```csharp
    // Persist the changes to a new file
    pdfDocument.Save(outputPath);
}
```

Den resulterande `output.pdf` innehåller samma visuella innehåll som originalet, men alla efterföljande ritningskommandon som väljer `GS0` kommer att följa de transparensinställningar du definierat.

### Förväntat resultat

Öppna `output.pdf` i Adobe Acrobat eller någon PDF‑visare. Om du lägger till en ny strokad linje med hjälp av `GS0`‑grafikstatusen (t.ex. via `pdfDocument.Pages[1].Contents.Add(...)`), kommer linjen att visas halvtransparent medan fyllningar förblir opaka. Detta visar att du framgångsrikt har **add graphics state pdf** och **modify PDF transparency**.

---

## Fullt körbart exempel

Nedan är det kompletta programmet som du kan kopiera‑och‑klistra in i en konsolapplikation. Det inkluderar licensladdning, felhantering och kommentarer som förklarar varje icke‑uppenbart steg.

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣  Apply license (optional for evaluation)
        // -------------------------------------------------
        try
        {
            var license = new License();
            license.SetLicense("Aspose.Pdf.lic");
        }
        catch (Exception) { /* License not found – continue in evaluation mode */ }

        // -------------------------------------------------
        // 2️⃣  Define file locations
        // -------------------------------------------------
        string inputPath = @"C:\MyPdfs\input.pdf";
        string outputPath = @"C:\MyPdfs\output.pdf";

        // -------------------------------------------------
        // 3️⃣  Open document and prepare resources
        // -------------------------------------------------
        using (var pdfDocument = new Document(inputPath))
        {
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            if (!resourcesEditor.ContainsKey("ExtGState"))
            {
                var emptyExtGState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
                resourcesEditor.Add("ExtGState", emptyExtGState);
            }

            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // -------------------------------------------------
            // 4️⃣  Create custom graphics state (transparency)
            // -------------------------------------------------
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            newGraphicsState.Add("CA", new CosPdfNumber(1));   // Fill opacity
            newGraphicsState.Add("ca", new CosPdfNumber(0.5)); // Stroke opacity
            newGraphicsState.Add("BM", new CosPdf


## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig behärska ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Lägg till transparens i PDF med Aspose PDF i C# – Steg‑för‑steg‑guide](/pdf/english/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Lägg till transparens i PDF med Aspose – Komplett C#‑guide](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [Hur man lägger till en bildstämpel i en PDF med Aspose.PDF för .NET: En omfattande guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}