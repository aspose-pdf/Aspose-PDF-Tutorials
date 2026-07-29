---
category: general
date: 2026-06-30
description: Lägg till Bates‑nummerering i PDF med Aspose.PDF i C#. Lär dig hur du
  numrerar PDF‑sidor, anger ett anpassat prefix och skapar ett pålitligt Bates‑nummereringsdokument.
draft: false
keywords:
- add bates numbering
- how to add bates
- number pdf pages
- how to number pdf
- bates numbering document
language: sv
og_description: Lägg till Bates‑nummerering i PDF med Aspose.PDF. Denna guide visar
  hur du numrerar PDF‑sidor och skapar ett Bates‑nummereringsdokument i C#.
og_title: Lägg till Bates-nummerering i PDF – Aspose.PDF‑guide
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add Bates numbering to PDF using Aspose.PDF in C#. Learn how to number
    PDF pages, set a custom prefix, and create a reliable Bates numbering document.
  headline: Add Bates Numbering to PDF with Aspose.PDF – Complete Guide
  type: TechArticle
- description: Add Bates numbering to PDF using Aspose.PDF in C#. Learn how to number
    PDF pages, set a custom prefix, and create a reliable Bates numbering document.
  name: Add Bates Numbering to PDF with Aspose.PDF – Complete Guide
  steps:
  - name: Customizing Appearance (Optional)
    text: 'If you need a different font, size, or placement, you can tweak the `BatesNumbering`
      properties:'
  - name: Expected Output
    text: Open `bates_numbered.pdf` in any PDF viewer. You’ll see a label like **CASE‑1000**
      on the first page, **CASE‑1001** on the second, and so on. The numbers appear
      in the bottom‑left corner by default (or wherever you set `XIndent`/`YIndent`).
  - name: 1. What if the PDF is huge (hundreds of MB)?
    text: 'Aspose.PDF streams pages to disk by default, so memory consumption stays
      low. However, you can explicitly enable **compression**:'
  - name: 2. Need a different numbering format (e.g., suffix instead of prefix)?
    text: 'Set the `Suffix` property:'
  - name: 3. How to restart numbering for a new section?
    text: Call `bates.StartNumber = 1;` before processing the next batch, or create
      a second `BatesNumbering` instance.
  - name: 4. The PDF already contains watermarks—will the numbers overlap?
    text: 'Adjust `XIndent` and `YIndent` to move the numbers away from existing elements.
      You can also change the `Position` enum (`BatesNumberingPosition.TopRight`,
      etc.):'
  - name: 5. Does this work with encrypted PDFs?
    text: 'If the source PDF is password‑protected, open it like this:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF processing
- Bates numbering
title: Lägg till Bates‑nummerering i PDF med Aspose.PDF – Komplett guide
url: /sv/net/programming-with-pdf-pages/add-bates-numbering-to-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till Bates-nummerering i PDF med Aspose.PDF – Komplett guide

Har du någonsin behövt **add bates numbering** till en PDF men varit osäker på var du ska börja? Du är inte ensam—juridiska team, revisorer och till och med utvecklare frågar ofta *how to add bates* för att spåra stora dokumentuppsättningar. I den här handledningen går vi igenom en komplett, färdig‑att‑köra‑lösning som numrerar PDF‑sidor, applicerar ett anpassat prefix och sparar ett nytt **bates numbering document**. Inga onödiga detaljer, bara koden du kan kopiera‑klistra in idag.

Vi kommer att täcka allt från att konfigurera Aspose.PDF, välja ett startnummer, hantera kantfall som enorma filer, och även justera formatet om du behöver något utöver standarden. I slutet kommer du att kunna **number pdf pages** automatiskt, och du kommer att förstå varför detta tillvägagångssätt är både robust och lätt att underhålla.

## Förutsättningar

- .NET 6.0 eller senare (exemplet använder .NET 6 men fungerar med .NET Core 3.1+)
- En Aspose.PDF for .NET-licens (den kostnadsfria utvärderingen fungerar för testning)
- En PDF‑fil du vill bearbeta (namngiven `source.pdf` i exemplet)
- Visual Studio 2022 eller någon C#‑redigerare du föredrar

Det är allt—inga extra NuGet‑paket utöver Aspose.PDF.

## Steg 1: Installera Aspose.PDF för .NET

Öppna din terminal eller Package Manager Console och kör:

```bash
dotnet add package Aspose.PDF
```

eller, i Visual Studio:

```
Tools → NuGet Package Manager → Manage NuGet Packages for Solution…
Search “Aspose.PDF” and click Install.
```

> **Pro tip:** Om du planerar att bearbeta tusentals sidor, aktivera **Aspose.PDF:s minnes‑sparande läge** genom att sätta `PdfConversion.SaveOptions.UseObjectPooling = true;` senare.

## Steg 2: Skapa ett enkelt konsolprogram‑skelett

Låt oss skapa ett minimalt konsolprogram så att du kan köra koden omedelbart:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in the next steps.
        }
    }
}
```

Spara filen som `Program.cs`. Detta skelett ger oss en ren plats att lägga in **bates numbering**‑logiken.

## Steg 3: Öppna käll‑PDF‑dokumentet

Den första faktiska operationen är att öppna PDF‑filen du vill stämpla. Vi använder ett `using`‑block så att filhandtaget frigörs automatiskt:

```csharp
// Step 3: Open the source PDF document
using (var doc = new Document("YOUR_DIRECTORY/source.pdf"))
{
    // Subsequent steps go here.
}
```

> **Varför ett `using`‑block?** Det garanterar att den underliggande filströmmen stängs, vilket förhindrar låsningsproblem när du senare försöker skriva över samma fil.

## Steg 4: Ställ in BatesNumbering‑fasaden

Aspose.PDF tillhandahåller en bekväm fasad som heter `BatesNumbering`. Den döljer den lågnivå sid‑för‑sid‑hanteringen och låter dig fokusera på själva numreringen.

```csharp
// Step 4: Create a Bates numbering facade
var bates = new BatesNumbering
{
    // Step 4a: Choose the starting number
    StartNumber = 1000,

    // Step 4b: Add an optional prefix (e.g., CASE-)
    Prefix = "CASE-"
    
    // You can also set a suffix, font size, or position if needed.
};
```

### Anpassa utseende (valfritt)

Om du behöver ett annat teckensnitt, storlek eller placering kan du justera `BatesNumbering`‑egenskaperna:

```csharp
bates.FontSize = 10;               // Smaller than the default 12
bates.TextColor = Color.Black;    // Ensure high contrast
bates.XIndent = 20;               // Move number 20 points from the left edge
bates.YIndent = 30;               // Move number 30 points from the bottom edge
```

Dessa inställningar är praktiska när standardplaceringen stör befintligt innehåll.

## Steg 5: Applicera Bates‑numreringen på dokumentet

Nu stämplar vi faktiskt numren på varje sida:

```csharp
// Step 5: Apply the Bates numbering to the document
bates.AddBatesNumbering(doc);
```

Bakom kulisserna itererar Aspose.PDF över varje sida, infogar den formaterade strängen (t.ex. `CASE-1000`, `CASE-1001`, …) och respekterar eventuella layoutalternativ du ställt in tidigare.

## Steg 6: Spara den nynumrerade PDF‑filen

Slutligen skriver du resultatet till disk. Du kan skriva över originalfilen eller skapa en ny—här behåller vi båda för säkerhet:

```csharp
// Step 6: Save the newly numbered PDF
doc.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering applied successfully!");
```

Att köra programmet bör skapa en fil med namnet `bates_numbered.pdf` där varje sida är tydligt märkt.

### Förväntat resultat

Öppna `bates_numbered.pdf` i någon PDF‑visare. Du kommer att se en etikett som **CASE‑1000** på första sidan, **CASE‑1001** på den andra, och så vidare. Numren visas som standard i det nedre vänstra hörnet (eller där du har satt `XIndent`/`YIndent`).

## Fullt fungerande exempel

När vi sätter ihop alla bitar, här är den kompletta koden du kan kopiera‑klistra in:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to match your environment
            const string sourcePath = "YOUR_DIRECTORY/source.pdf";
            const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";

            // Open the source PDF
            using (var doc = new Document(sourcePath))
            {
                // Configure Bates numbering
                var bates = new BatesNumbering
                {
                    StartNumber = 1000,
                    Prefix = "CASE-",
                    // Optional customizations:
                    // FontSize = 10,
                    // TextColor = Color.Black,
                    // XIndent = 20,
                    // YIndent = 30
                };

                // Apply numbering
                bates.AddBatesNumbering(doc);

                // Save the result
                doc.Save(outputPath);
                Console.WriteLine($"Bates numbering added. Saved to: {outputPath}");
            }
        }
    }
}
```

Kör `dotnet run` från projektmappen, så ser du konsolmeddelandet som bekräftar att det lyckades.

## Kantfall & Vanliga frågor

### 1. Vad händer om PDF‑filen är enorm (hundratals MB)?

Aspose.PDF strömmar sidor till disk som standard, så minnesanvändningen hålls låg. Du kan dock explicit aktivera **komprimering**:

```csharp
doc.Compress();
```

### 2. Behöver ett annat numreringsformat (t.ex. suffix istället för prefix)?

Ställ in `Suffix`‑egenskapen:

```csharp
bates.Suffix = "-2026";
```

Du kan kombinera båda:

```csharp
bates.Prefix = "CASE-";
bates.Suffix = "-2026";
```

Resultat: `CASE-1000-2026`.

### 3. Hur återställer man numreringen för ett nytt avsnitt?

Anropa `bates.StartNumber = 1;` innan du bearbetar nästa batch, eller skapa en andra `BatesNumbering`‑instans.

### 4. PDF‑filen innehåller redan vattenstämplar—kommer numren att överlappa?

Justera `XIndent` och `YIndent` för att flytta numren bort från befintliga element. Du kan också ändra `Position`‑enum (`BatesNumberingPosition.TopRight`, etc.):

```csharp
bates.Position = BatesNumberingPosition.TopRight;
```

### 5. Fungerar detta med krypterade PDF‑filer?

Om käll‑PDF‑filen är lösenordsskyddad, öppna den så här:

```csharp
var doc = new Document(sourcePath, new LoadOptions { Password = "yourPassword" });
```

Resten av arbetsflödet förblir oförändrat.

## Tips för produktionsklara implementationer

- **Licensiera tidigt**: Infoga `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` i början av `Main` för att undvika utvärderingsvattenstämpeln.
- **Parallell bearbetning**: För batch‑operationer på många filer, omslut per‑fil‑logiken i en `Parallel.ForEach`‑loop—var bara medveten om I/O‑begränsningarna.
- **Logging**: Use `Ser

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man lägger till sidnummerstämplar i PDF‑filer med Aspose.PDF för .NET | Vattenstämplar & Bakgrunder](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [Hur man lägger till och anpassar sidnummer i PDF‑filer med Aspose.PDF för .NET | Dokumentmanipuleringsguide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Hur man lägger till en textstämpel i PDF med Aspose.PDF .NET: Omfattande guide](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}