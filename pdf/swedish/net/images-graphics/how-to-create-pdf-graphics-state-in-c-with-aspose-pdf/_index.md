---
category: general
date: 2026-11-16
description: Lär dig hur du skapar PDF-grafikstatus i C# med Aspose.Pdf. Denna guide
  täcker opacitet, blandningsläge och ett komplett kodexempel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf graphics state
- Aspose.Pdf ExtGState
- PDF opacity
- C# PDF manipulation
- PDF blend mode
- Aspose.Pdf graphics state
language: sv
lastmod: 2026-11-16
og_description: Skapa PDF‑grafikstatus i C# med Aspose.Pdf. Följ den här kompletta
  handledningen för att programatiskt ställa in opacitet och blandningsläge.
og_image_alt: Illustration of how to create PDF graphics state with Aspose.Pdf in
  C#
og_title: Skapa PDF-grafikstatus i C# – steg‑för‑steg Aspose.Pdf‑guide
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to create PDF graphics state in C# using Aspose.Pdf. This
    guide covers opacity, blend mode, and full code example.
  headline: How to create PDF graphics state in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF
title: Hur man skapar PDF‑grafikstatus i C# med Aspose.Pdf
url: /sv/net/images-graphics/how-to-create-pdf-graphics-state-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar PDF‑grafikstatus i C# med Aspose.Pdf

Om du behöver **skapa PDF‑grafikstatus** i ett .NET‑projekt visar den här handledningen exakt hur du gör det med Aspose.Pdf. Oavsett om du vill kontrollera opacitet, ändra blandningsläge eller återanvända en anpassad grafikstatus över sidor, ger stegen nedan en komplett, färdig‑att‑köra‑lösning.

I den här guiden lär du dig hur du får åtkomst till sidresurserna, lägger till ett **ExtGState**‑element och sparar ändringarna till en ny fil. Exemplet fungerar med Aspose.Pdf 23.12 (eller senare) och riktar sig mot .NET 6+, men koncepten gäller även för tidigare versioner.

## Förutsättningar

Innan du börjar, se till att du har:

* Visual Studio 2022 (eller någon C#‑IDE) med .NET 6 SDK installerad.  
* En Aspose.Pdf för .NET‑licens eller en tillfällig utvärderingsnyckel.  
* En PDF‑fil med namnet `input.pdf` placerad i en mapp som du kan referera till från kod.  

Inga ytterligare NuGet‑paket krävs utöver `Aspose.Pdf`.

## Vad handledningen täcker

* Laddar ett befintligt PDF‑dokument.  
* Navigerar till den första sidans resurser‑ordbok.  
* Skapar en ny grafikstatus‑ordbok som definierar linjeopacitet (`CA`), fyllopacitet (`ca`) och blandningsläge (`BM`).  
* Lägger till den nya grafikstatusen i **ExtGState**‑samlingen med ett anpassat namn (`GS0`).  
* Sparar den uppdaterade PDF‑filen så att efterföljande ritkommandon kan referera till den nya statusen.

När du har gått igenom handledningen kan du **skapa PDF‑grafikstatus**‑objekt programatiskt och återanvända dem i alla ritoperationer.

## Steg 1: Ställ in projektet och importera namnrymder

Skapa ett nytt konsolprogram (eller integrera koden i ett befintligt projekt). Lägg till Aspose.Pdf‑referensen och inkludera de nödvändiga namnrymderna:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Generator;
```

> **Pro tip:** Om du använder den kostnadsfria utvärderingsversionen, lägg till `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` innan du laddar dokumentet för att undvika vattenstämpelmeddelanden.

## Steg 2: Ladda PDF‑dokumentet

Att öppna filen är enkelt. Klassen `Document` representerar hela PDF‑filen och ger dig åtkomst till dess sidor och resurser.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";

using (var document = new Document(inputPath))
{
    // All subsequent steps run inside this using block
```

Att placera koden i ett `using`‑block garanterar att filhandtaget frigörs efter operationen, vilket är avgörande för **C# PDF‑manipulation** i produktionsmiljöer.

## Steg 3: Hämta den första sidans resurser‑ordbok

Varje PDF‑sida har en *Resources*-ordbok som lagrar teckensnitt, bilder och grafikstatusar. Vi behöver en `DictionaryEditor` för att redigera den strukturen.

```csharp
    // Step 3: Get the first page and its resources dictionary
    var page = document.Pages[1];
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

Om PDF‑filen redan innehåller ett `ExtGState`‑element kommer `resourcesEditor["ExtGState"]` att returnera det; annars skapar Aspose.Pdf en tom ordbok åt oss när vi lägger till det första elementet.

## Steg 4: Åtkomst till eller skapa ExtGState‑ordboken

**ExtGState**‑ordboken innehåller namngivna grafikstatus‑objekt. Vi antingen hämtar en befintlig eller skapar en ny behållare.

```csharp
    // Step 4: Access (or create) the ExtGState dictionary within the resources
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

När `ExtGState` inte finns, returnerar `resourcesEditor["ExtGState"]` automatiskt en ny tom ordbok, vilket säkerställer att koden fungerar för alla PDF‑filer.

## Steg 5: Bygg den nya grafikstatus‑ordboken

En grafikstatus är en `CosPdfDictionary` med specifika nycklar:

* `CA` – linjeopacitet (0‑1)  
* `ca` – fyllopacitet (0‑1)  
* `BM` – blandningsläge (`Normal`, `Multiply` osv.)

Vi skapar en tom ordbok, fyller i den och lägger sedan till den i `ExtGState`.

```csharp
    // Step 5: Create a new graphics state dictionary with desired parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (50% transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };

    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

Du kan ändra `0.5` till vilket värde som helst mellan `0` och `1` för att justera fyllopaciteten, eller ersätta `"Normal"` med `"Multiply"` för ett annat **PDF‑blandningsläge**. Denna flexibilitet är anledningen till att skapa en anpassad grafikstatus är en kraftfull teknik i **Aspose.Pdf graphics state**‑hantering.

## Steg 6: Registrera grafikstatusen med ett namn

PDF‑innehållsströmmar refererar till grafikstatusar med namn. Här använder vi `GS0`, men vilket unikt namn som helst fungerar.

```csharp
    // Step 6: Add the new graphics state to the ExtGState dictionary with a name (e.g., GS0)
    extGState.Add("GS0", newGraphicsState);
```

Om du behöver flera statusar, upprepa skapandet med olika parametrar och lägg till dem som `GS1`, `GS2` osv. Detta mönster skalar bra för komplexa dokument som kräver varierande opacitet eller blandningsinställningar på olika lager.

## Steg 7: Spara den modifierade PDF‑filen

Skriv slutligen det uppdaterade dokumentet till en ny fil. Att behålla originalet intakt underlättar felsökning.

```csharp
    // Step 7: Save the updated PDF document
    string outputPath = @"YOUR_DIRECTORY\output.pdf";
    document.Save(outputPath);
}
```

Efter körning innehåller `output.pdf` ett `ExtGState`‑element med namnet `GS0`. Alla efterföljande ritoperatorer kan referera till det med `gs`‑operatorn (t.ex. `GS0 gs` i en innehållsström).  

> **Varför detta är viktigt:** Genom att skapa en återanvändbar grafikstatus undviker du att upprepa opacitets‑ och blandningsinställningar för varje ritkommando, vilket förbättrar både prestanda och underhållbarhet.

## Använd den nya grafikstatusen i en innehållsström (valfritt)

Om du vill se effekten omedelbart kan du lägga till en enkel rektangel som använder den status vi just skapade:

```csharp
using (var document = new Document(outputPath))
{
    var page = document.Pages[1];
    var content = page.Contents[1]; // Get the first content stream

    // Insert graphics state selection and a semi‑transparent rectangle
    var operators = new List<Operator>
    {
        new Operator("GS0", "gs"),                     // Select our custom graphics state
        new Operator("0.5", "w"),                      // Set line width (optional)
        new Operator("100", "100", "200", "150", "re"), // Rectangle (x, y, width, height)
        new Operator("B")                              // Stroke the rectangle
    };

    foreach (var op in operators)
        content.Operators.Add(op);

    document.Save(@"YOUR_DIRECTORY\final_output.pdf");
}
```

Rektangeln kommer att ritas med 50 % fyllopacitet medan linjen förblir helt opak, exakt som definierat i **create PDF graphics state**‑ordboken.

## Vanliga fallgropar och hur du undviker dem

| Problem | Varför det händer | Lösning |
|---------|-------------------|---------|
| `ExtGState`‑elementet hittas inte | Vissa PDF‑filer utelämnar ordboken helt. | `DictionaryEditor` skapar den automatiskt när du lägger till det första elementet, så ingen extra kontroll behövs. |
| Opacitetsvärden > 1 eller < 0 | PDF‑specifikationen begränsar opacitet till intervallet `[0,1]`. | Kapa värdena innan du skapar `CosPdfNumber`. |
| Felstavning av blandningsläge | Namnen på PDF‑blandningslägen är skiftlägeskänsliga. | Använd exakt namn som `"Normal"`, `"Multiply"`, `"Screen"`. |
| Licens‑vattenstämpel | Utvärderingsversionen lägger till en vattenstämpel på första sidan. | Applicera en giltig licensfil innan du öppnar dokumentet. |

Genom att hantera dessa edge‑cases säkerställer du att din **create PDF graphics state**‑implementation fungerar pålitligt över olika PDF‑källor.

## Fullt, körbart exempel

Nedan finns ett självständigt program som du kan kopiera, klistra in och köra. Ersätt `YOUR_DIRECTORY` med en faktisk sökväg på din maskin.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;

class Program
{
    static void Main()
    {
        // Optional: apply license to remove evaluation watermark
        // var license = new Aspose.Pdf.License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        using (var document = new Document(inputPath))
        {
            // 1️⃣ Get first page and its resources
            var page = document.Pages[1];
            var resourcesEditor = new DictionaryEditor(page.Resources);

            // 2️⃣ Access (or create) ExtGState dictionary
            var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // 3️⃣ Build new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // 4️⃣ Register the state with a name (GS0)
            extGState.Add("


## Vad du bör lära dig härnäst?


De följande handledningarna täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa anpassad grafikstatus i PDF med Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Lägg till grafikstatus i PDF med Aspose.PDF för .NET (C#)](/pdf/english/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/)
- [Hur man skapar tom grafikstatus i en PDF med C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}