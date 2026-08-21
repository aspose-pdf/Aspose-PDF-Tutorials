---
category: general
date: 2026-08-20
description: Skapa anpassat grafikläge i PDF med Aspose.Pdf. Lär dig hur du redigerar
  PDF-resurser och lägger till transparens i PDF på bara några steg.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom graphics state
- edit pdf resources
- add transparency pdf
- Aspose.Pdf graphics state
- PDF resource dictionary
language: sv
lastmod: 2026-08-20
og_description: Skapa ett anpassat grafikstillstånd i PDF med Aspose.Pdf. Denna handledning
  visar hur du redigerar PDF‑resurser och snabbt lägger till transparens i PDF.
og_image_alt: Screenshot of C# code that creates a custom graphics state in a PDF
og_title: Skapa anpassat grafikstillstånd i PDF – Aspose.Pdf-guide
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create custom graphics state in PDF with Aspose.Pdf. Learn how to edit
    PDF resources and add transparency PDF in just a few steps.
  headline: Create custom graphics state in PDF using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- Aspose.Pdf
- C#
- Graphics state
title: Skapa anpassat grafiskt tillstånd i PDF med Aspose.Pdf
url: /sv/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa anpassat grafikläge i PDF med Aspose.Pdf

Om du behöver **skapa anpassat grafikläge** i en PDF, visar den här guiden exakt hur du gör det med Aspose.Pdf för .NET. I slutet av handledningen kommer du att kunna **redigera PDF-resurser**, injicera en ny grafik‑tillståndsordbok och **lägga till transparens-PDF**-innehåll utan att lämna ditt C#-projekt.

Du får se ett komplett, körbart exempel, en förklaring av varför varje rad är viktig, samt tips för att hantera flersidiga dokument eller olika blandningslägen. Inga externa verktyg krävs – bara Aspose.Pdf‑biblioteket och en grundläggande .NET‑utvecklingsmiljö.

## Förutsättningar

Innan du börjar, se till att du har:

* .NET 6.0 eller senare (koden fungerar också med .NET Framework 4.7+)
* En licensierad kopia av **Aspose.Pdf for .NET** (gratis provversion fungerar för testning)
* En inmatnings‑PDF‑fil med namnet `input.pdf` placerad i en mapp du kan referera till från kod
* Visual Studio 2022 eller någon IDE som stödjer C#‑utveckling

Handledningen förutsätter att du är bekant med grundläggande C#‑syntax och konceptet med PDF‑sidor.

## Steg 1: Läs in käll‑PDF:en och få åtkomst till den första sidan

Den första operationen är att öppna PDF‑filen och hämta sidan vars resurser du vill ändra. Aspose.Pdf representerar varje sida som ett `Page`‑objekt, och varje sida innehåller en **resursordbok** som lagrar grafiklägen, teckensnitt, XObjects och mer.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

// Load the PDF you want to edit
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Get the first page (pages are 1‑based in Aspose.Pdf)
    Page firstPage = pdfDocument.Pages[1];
```

*Varför detta är viktigt:* `Document`‑klassen laddar filen i minnet, och `Pages[1]` ger dig direkt åtkomst till den första sidans resursordbok, där ett grafikläge finns.

## Steg 2: Öppna resursordboken för redigering

Aspose.Pdf tillhandahåller en hjälparklass `DictionaryEditor` som låter dig behandla en resursordbok som en vanlig .NET `Dictionary`. Detta gör det enkelt att läsa, lägga till eller ersätta poster såsom `ExtGState`.

```csharp
    // Create an editor for the page’s resources
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Varför detta är viktigt:* `DictionaryEditor` abstraherar de lågnivå‑COS‑objekten, så att du kan arbeta med välbekanta nyckel/värde‑par samtidigt som PDF‑kompatibiliteten bevaras.

## Steg 3: Hämta (eller skapa) ExtGState‑ordboken

**ExtGState**‑posten innehåller alla externa grafik‑tillståndsobjekt för sidan. Om ordboken inte finns skapar Aspose.Pdf en tom en åt dig.

```csharp
    // Ensure the ExtGState dictionary exists
    var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
        ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
        : new CosPdfDictionary(pdfDocument);
```

*Varför detta är viktigt:* En saknad `ExtGState`‑post skulle orsaka ett `KeyNotFoundException` senare. Detta skydd låter koden fungera på PDF‑filer som aldrig har definierat ett anpassat grafikläge – en väsentlig del av **redigera PDF-resurser**‑robustheten.

## Steg 4: Bygg den anpassade grafiklägesordboken

Ett grafikläge beskriver hur ritoperationer renderas. För att **lägga till transparens PDF** måste du sätta `ca` (fyllningsopacitet) och `CA` (linjeopacitet) samt eventuellt ett blandningsläge (`BM`). Följande kod bygger en ny ordbok med dessa parametrar.

```csharp
    // Create an empty dictionary that will become the new graphics state
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Define the parameters you want for the custom state
    var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
    {
        // Stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        // Fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        // Blend mode – "Normal" is the default, but you can use "Multiply", "Screen", etc.
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };

    // Populate the dictionary with the parameters
    foreach (var param in graphicsStateParams)
        newGraphicsState.Add(param);
```

*Varför detta är viktigt:* `ca`‑ och `CA`‑poster styr transparens för fyllning respektive linje. Att sätta `BM` låter dig experimentera med olika sammansättnings‑effekter, vilket är användbart när du senare **lägger till transparens PDF**‑innehåll som halvtransparenta former eller bilder.

## Steg 5: Registrera det nya grafikläget under ett unikt namn

Varje grafikläge i `ExtGState`‑ordboken måste ha ett unikt namn (t.ex. `GS0`, `GS1`). Du kan välja vilket namn som helst så länge det inte kolliderar med befintliga poster.

```csharp
    // Choose a name that is unlikely to collide with existing states
    const string graphicsStateName = "GS0";

    // Add the new graphics state to the ExtGState dictionary
    extGStateDict.Add(graphicsStateName, newGraphicsState);

    // If the ExtGState entry was missing, attach it back to the page resources
    if (!resourcesEditor.ContainsKey("ExtGState"))
        resourcesEditor["ExtGState"] = extGStateDict;
```

*Varför detta är viktigt:* Genom att infoga den nya ordboken under `GS0` gör du tillståndet adresserbart från sidans innehållsströmmar. Det villkorliga blocket säkerställer att `ExtGState`‑posten finns även för PDF‑filer som startade utan en sådan – ytterligare ett **redigera PDF-resurser**‑skydd.

## Steg 6: Använd det anpassade grafikläget i sidans innehåll (valfritt)

De föregående stegen *definierar* bara grafikläget. För att faktiskt se effekten måste du referera det i sidans innehållsström. Nedan är ett snabbt exempel som ritar en halvtransparent rektangel med det tillstånd vi just skapade.

```csharp
    // Get the page’s content stream (or create a new one if empty)
    var content = firstPage.Contents[1];
    var graphics = new ContentWriter(content);

    // Save current graphics state
    graphics.WriteOperator(OperatorName.SaveState);
    // Set the custom graphics state we just defined
    graphics.WriteOperand($"/{graphicsStateName}");
    graphics.WriteOperator(OperatorName.SetExtGState);
    // Draw a rectangle (coordinates are in points)
    graphics.WriteOperand(100);   // lower‑left x
    graphics.WriteOperand(500);   // lower‑left y
    graphics.WriteOperand(200);   // width
    graphics.WriteOperand(100);   // height
    graphics.WriteOperator(OperatorName.Rectangle);
    // Fill the rectangle using the current fill opacity (ca = 0.5)
    graphics.WriteOperator(OperatorName.Fill);
    // Restore the previous graphics state
    graphics.WriteOperator(OperatorName.RestoreState);
```

*Varför detta är viktigt:* Operatören `SetExtGState` (`gs`) talar om för PDF‑renderaren att tillämpa parametrarna som definierats i `GS0`. Rektangeln kommer att visas med 50 % fyllningsopacitet medan dess linje förblir helt opak.

## Steg 7: Spara den modifierade PDF:en

Till sist skriver du tillbaka ändringarna till disk. Du kan skriva över originalfilen eller skapa en ny.

```csharp
    // Save the updated PDF
    pdfDocument.Save("YOUR_DIRECTORY/output_with_custom_gs.pdf");
}
```

När du öppnar `output_with_custom_gs.pdf` i en PDF‑visare bör du se en halvtransparent rektangel på den första sidan. Detta bekräftar att du framgångsrikt **skapat anpassat grafikläge**, **redigerat PDF-resurser** och **lagt till transparens PDF**‑innehåll.

## Vanliga variationer och kantfall

| Situation | Vad som ska justeras |
|-----------|----------------------|
| **Flera sidor behöver samma tillstånd** | Registrera grafikläget en gång (steg 1‑5) och referera `GS0` i någon sidans innehållsström. |
| **Olika opacitet per element** | Definiera ytterligare tillstånd (`GS1`, `GS2`, …) med olika `ca`/`CA`‑värden och växla mellan dem med `SetExtGState`. |
| **Blandningsläge annat än Normal** | Byt ut `"Normal"` mot `"Multiply"`, `"Screen"` eller något PDF‑standardblandningsläge i `BM`‑posten. |
| **Namnkollision** | Innan du lägger till, kontrollera `extGStateDict.ContainsKey(yourName)` och välj ett unikt suffix om det behövs. |
| **PDF innehåller redan en ExtGState-ordbok** | Koden i Steg 3 återanvänder redan den befintliga ordboken, så ingen extra hantering krävs. |

**Proffstips:** När du arbetar med stora PDF‑filer, omslut användningen av `Document` i ett `using`‑block (som visas) för att frigöra inhemska resurser snabbt. Överväg också att aktivera Aspose.Pdf:s `PdfCompliance`‑egenskap om du måste garantera PDF/A‑ eller PDF/X‑konformitet efter att ha redigerat resurser.

## Fullständigt fungerande exempel

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Load the PDF you want to edit
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 1: Get the first page
            Page firstPage = pdfDocument.Pages[1];

            // Step 2: Open the page resources for editing
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 3: Retrieve or create the ExtGState dictionary
            var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
                ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
                : new CosPdfDictionary(pdfDocument);

            // Step 4: Build a custom graphics state (50 % fill opacity, 100 % stroke opacity)
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var param in graphicsStateParams)
                newGraphicsState.Add(param);

            // Step 5: Register the graphics state under the name GS0
            const string graphicsStateName = "GS0";
            extGStateDict.Add(graphicsStateName, newGraphics


## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Hur man skapar PDF med Aspose – Lägg till formulärfält och sidor](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Hur man skapar anpassade tabeller i PDF:er med Aspose.PDF .NET](/pdf/english/net/tables-lists/create-custom-tables-in-pdfs-aspose-pdf-dot-net/)
- [Skapa anpassade PDF-stämplar Aspose Pdf Net](/pdf/hongkong/net/images-graphics/create-custom-pdf-stamps-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}