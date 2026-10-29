---
category: general
date: 2026-08-14
description: Skapa en tom PDF‑ordbok i C# med Aspose.Pdf – lär dig hur du lägger till
  ett grafikläge i ExtGState‑samlingen och modifierar PDF‑filer programatiskt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.Pdf Document
- PDF graphics state
- ExtGState dictionary
- CosPdfDictionary usage
language: sv
lastmod: 2026-08-14
og_description: Skapa en tom PDF‑ordbok i C# med Aspose.Pdf. Följ den här kompletta
  guiden för att lägga till ett anpassat grafikläge i en PDFs ExtGState‑samling.
og_image_alt: Screenshot showing C# code that creates an empty PDF dictionary with
  Aspose.Pdf
og_title: Skapa en tom PDF-ordbok i C# – Aspose.Pdf steg‑för‑steg guide
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  headline: Create empty PDF dictionary in C# with Aspose.Pdf
  type: TechArticle
- description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  name: Create empty PDF dictionary in C# with Aspose.Pdf
  steps:
  - name: Create a new **Console App** project in Visual Studio.
    text: Create a new **Console App** project in Visual Studio.
  - name: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
    text: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
  - name: 'Add the following `using` directives at the top of `Program.cs`:'
    text: 'Add the following `using` directives at the top of `Program.cs`:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Skapa en tom PDF‑ordbok i C# med Aspose.Pdf
url: /sv/net/programming-with-operators/create-empty-pdf-dictionary-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa tom PDF‑dictionary i C# med Aspose.Pdf

Om du behöver **skapa tom PDF‑dictionary**‑objekt när du arbetar med PDF‑filer, visar den här guiden exakt hur du gör det i C# med Aspose.Pdf‑biblioteket. Oavsett om du bygger ett anpassat grafik‑tillstånd, lägger till en ny resurs eller förbereder en mall för senare användning, ger stegen nedan en komplett, körbar lösning.

Du kommer att lära dig hur du laddar en PDF, får åtkomst till den första sidans resurs‑dictionary, bygger en helt ny `CosPdfDictionary` och sätter in den i `ExtGState`‑samlingen. I slutet av handledningen har du en fungerande `output.pdf` som innehåller den nyss skapade dictionaryn.

## Förutsättningar

Innan du börjar, se till att du har:

- .NET 6.0 eller senare (koden fungerar även med .NET Framework 4.6+)
- Visual Studio 2022 eller någon annan C#‑IDE du föredrar
- En Aspose.Pdf för .NET‑licens (eller en temporär utvärderingsnyckel)
- En exempel‑PDF med namnet **input.pdf** placerad i en mapp du kontrollerar (mappens sökväg kommer att användas som `dataDir`)

Inga ytterligare NuGet‑paket krävs utöver `Aspose.Pdf`.

## Steg 1: Ställ in projektet och referera Aspose.Pdf

1. Skapa ett nytt **Console App**‑projekt i Visual Studio.  
2. Öppna **NuGet Package Manager** och installera `Aspose.Pdf`:

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. Lägg till följande `using`‑direktiv högst upp i `Program.cs`:

   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Text;
   using Aspose.Pdf.Operators;
   using Aspose.Pdf.Facades;
   using Aspose.Pdf.InteractiveFeatures;
   using Aspose.Pdf.Xmp;
   using Aspose.Pdf.Operators.Filters;
   using Aspose.Pdf.Operators.Gfx;
   ```

   *Varför dessa namnrymder?* `Aspose.Pdf` innehåller kärnklassen `Document`, medan `Aspose.Pdf.Operators.Gfx` tillhandahåller `CosPdfDictionary`, `CosPdfNumber` och andra låg‑nivå PDF‑objekt som behövs för att **skapa tom PDF‑dictionary**‑strukturer.

## Steg 2: Läs in käll‑PDF‑filen

Den första operationen är att läsa in den befintliga PDF‑filen i en `Document`‑instans. Detta ger dig åtkomst till alla sidor, resurser och låg‑nivå dictionaries.

```csharp
// Step 2: Load the PDF document
string dataDir = @"C:\MyPdfFolder\";               // Change to your folder
using var pdfDocument = new Document(dataDir + "input.pdf");
```

*Förklaring*: `Document` läser in filen i minnet och förbereder interna strukturer. `using`‑satsen ser till att filhandtaget frigörs när vi är klara med bearbetningen.

## Steg 3: Få åtkomst till den första sidans resurs‑dictionary

Varje PDF‑sida har en **Resources**‑dictionary som grupperar teckensnitt, bilder, ExtGState‑objekt och andra delade resurser. För att infoga ett nytt grafik‑tillstånd måste vi redigera denna dictionary.

```csharp
// Step 3: Get the first page and its Resources dictionary
Page firstPage = pdfDocument.Pages[1];                     // PDF pages are 1‑based
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` är en hjälparklass som låter dig behandla en PDF‑dictionary som en C#‑`Dictionary<string, object>`.

## Steg 4: Hämta (eller skapa) ExtGState‑samlingen

`ExtGState` innehåller grafik‑tillståndsobjekt såsom opacitet, blandningsläge och linjebredd. Om käll‑PDF‑filen redan innehåller ett `ExtGState`‑element återanvänder vi det; annars skapar vi en ny tom dictionary.

```csharp
// Step 4: Ensure an ExtGState dictionary exists
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a brand‑new ExtGState dictionary and add it to Resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*Varför denna kontroll?* Vissa PDF‑filer saknar helt `ExtGState`‑elementet. Genom att hantera båda fallen blir handledningen robust för alla indatafiler.

## Steg 5: **Skapa tom PDF‑dictionary** för ett nytt grafik‑tillstånd

Nu skapar vi faktiskt **tom PDF‑dictionary**‑objekt som definierar grafik‑tillståndets parametrar. Dictionaryn startar tom och vi lägger till de nödvändiga nycklarna:

```csharp
// Step 5: Build a new graphics state dictionary (empty PDF dictionary + entries)
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Stroke opacity (CA) – 1 means fully opaque strokes
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes semi‑transparent fills
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default compositing mode
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

### Vad varje post gör

| Nyckel | Typ | Betydelse |
|--------|-----|-----------|
| **CA** | `CosPdfNumber` | Stroke‑opacitet (intervall 0‑1). |
| **ca** | `CosPdfNumber` | Fill‑opacitet (intervall 0‑1). |
| **BM** | `CosPdfName`   | Blandningsläge; `"Normal"` är det vanligaste. |

Eftersom vi började med en **tom PDF‑dictionary** har vi full kontroll över vilka poster som läggs till. Du kan utöka dictionaryn med ytterligare grafik‑tillståndsparametrar såsom `LW` (linjebredd) eller `LC` (linje‑cap) när du så önskar.

## Steg 6: Infoga det nya grafik‑tillståndet i ExtGState

`ExtGState`‑dictionaryn fungerar som en karta där varje post identifieras av ett namn (t.ex. `GS0`, `GS1`). Vi lägger vår nybyggda dictionary under en unik nyckel.

```csharp
// Step 6: Add the graphics state to the ExtGState collection
extGStateDict.Add("GS0", newGraphicsState);
```

Om du planerar att lägga till flera tillstånd, öka suffixet (`GS1`, `GS2`, …) för att undvika namnkonflikter.

## Steg 7: Spara den modifierade PDF‑filen

Till sist skriver vi tillbaka förändringarna till disk. `Save`‑metoden serialiserar automatiskt de uppdaterade dictionaries.

```csharp
// Step 7: Persist the changes
pdfDocument.Save(dataDir + "output.pdf");
```

Öppna `output.pdf` i någon PDF‑visare och inspektera **Resources → ExtGState**‑posten (de flesta visare döljer detta, men verktyg som Adobe Acrobat Preflight eller PDF‑Tron kan visa det). Du bör se en `GS0`‑post som innehåller de opacitets‑ och blandningsvärden du definierade.

## Komplett fungerande exempel

När alla bitar sätts ihop ser hela programmet ut så här – du kan kopiera och klistra in det i `Program.cs` och köra:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators.Gfx;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string dataDir = @"C:\MyPdfFolder\"; // <-- change to your folder
        using var pdfDocument = new Document(dataDir + "input.pdf");

        // -----------------------------------------------------------------
        // 2️⃣ Access the first page’s Resources dictionary
        // -----------------------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // -----------------------------------------------------------------
        // 3️⃣ Retrieve or create the ExtGState dictionary
        // -----------------------------------------------------------------
        CosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourcesEditor["ExtGState"] = extGStateDict;
        }

        // -----------------------------------------------------------------
        // 4️⃣ **Create empty PDF dictionary** for a new graphics state
        // -----------------------------------------------------------------
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode

        // -----------------------------------------------------------------
        // 5️⃣ Add the graphics state to ExtGState
        // -----------------------------------------------------------------
        extGStateDict.Add("GS0", newGraphicsState);

        // -----------------------------------------------------------------
        // 6️⃣ Save the modified PDF
        // -----------------------------------------------------------------
        pdfDocument.Save(dataDir + "output.pdf");

        Console.WriteLine("PDF saved with new empty dictionary at: " + dataDir + "output.pdf");
    }
}
```

**Förväntad output** – Konsolen skriver ut en bekräftelsesats, och `output.pdf` innehåller den nya `GS0`‑posten under `ExtGState`. När du renderar en sida som refererar `GS0` (t.ex. via en content‑stream‑operator `gs`), blir streck helt ogenomskinliga medan fyllningar är 50 % transparenta.

## Vanliga frågor och hantering av kantfall

| Fråga | Svar |
|-------|------|
| *Vad händer om PDF‑filen har flera sidor?* | Exemplet riktar sig mot den första sidan (`Pages[1]`). För att påverka alla sidor, loopa igenom `pdfDocument.Pages` och upprepa steg 3‑5 för varje sidas resurser. |
| *Kan jag lägga till dictionaryn på en sida som redan har ett ExtGState‑element med namnet “GS0”?* | Ja, men du måste använda en annan nyckel (`GS1`, `GS2`, …) för att undvika att skriva över den befintliga posten. |
| *Är det säkert att ändra dictionaryn efter att ha sparat?* | När du anropar `Save` är den minnes‑representation som ligger bakom filen fristående från filen. Du kan fortsätta redigera `Document`‑objektet och anropa `Save` igen om så behövs. |
| *Behöver jag en licens för Aspose.Pdf för att använda ` |

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationssätt i dina egna projekt.

- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [How to Remove Graphics from PDFs Using Aspose.PDF .NET&#58; A Complete Guide](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [How to Create Multi-Layer PDFs Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/advanced-features/create-multi-layer-pdfs-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}