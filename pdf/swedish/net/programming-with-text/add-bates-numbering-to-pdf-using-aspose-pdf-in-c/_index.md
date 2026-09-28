---
category: general
date: 2026-09-27
description: Lägg till Bates-numrering i PDF med Aspose.PDF i C#. Lär dig hur du laddar
  ett PDF-dokument, ställer in Bates-numreringsalternativ och sparar den uppdaterade
  filen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- load pdf document
- how to add bates numbering
- Aspose.PDF C#
- PDF Bates numbering example
language: sv
lastmod: 2026-09-27
og_description: Lägg till Bates‑numrering i PDF med Aspose.PDF i C#. Denna handledning
  visar hur du laddar ett PDF‑dokument, konfigurerar Bates‑numrering och sparar resultatet.
og_image_alt: Screenshot of a PDF page displaying Bates numbers in the footer
og_title: Lägg till Bates-nummerering i PDF med Aspose.PDF – C#‑guide
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Add bates numbering to PDF using Aspose.PDF in C#. Learn how to load
    a PDF document, set Bates numbering options, and save the updated file.
  headline: Add bates numbering to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF processing
title: Lägg till Bates-nummerering i PDF med Aspose.PDF i C#
url: /sv/net/programming-with-text/add-bates-numbering-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till Bates‑numrering i PDF med Aspose.PDF i C#

Om du behöver **lägga till Bates‑numrering** i en PDF‑fil visar den här guiden en komplett, färdig‑att‑köra lösning. Du får se hur du **läser in ett PDF‑dokument**, konfigurerar Bates‑numreringsalternativen och skriver tillbaka den numrerade filen till disk – allt med Aspose.PDF för .NET.

Att tillämpa Bates‑nummer är vanligt i juridiska, brottsbekämpande och arkiveringsarbetsflöden. I slutet av den här tutorialen kan du bädda in en sekventiell identifierare på varje sida, anpassa prefixet och börja räkningen från vilket tal du önskar.

## Vad du kommer att lära dig

* Hur du **läser in PDF‑dokument** till ett `Aspose.Pdf.Document`‑objekt.  
* De exakta stegen **hur du lägger till Bates‑numrering** med `BatesNumberingOptions`.  
* Hur du sparar den modifierade filen samtidigt som du bevarar originallayout och kvalitet.  

Inga externa verktyg krävs – bara Aspose.PDF‑paketet från NuGet och en .NET‑utvecklingsmiljö (Visual Studio, VS Code eller Rider).  

---

## Steg 1: Installera Aspose.PDF för .NET

Öppna din projektmapp i en terminal och kör:

```bash
dotnet add package Aspose.PDF
```

Paketet innehåller namnutrymmet `Aspose.Pdf`, som tillhandahåller alla klasser som används i den här tutorialen. Efter installationen, ladda om projektet så att IDE:n hittar den nya referensen.

## Steg 2: Läs in PDF‑dokument

Att läsa in källfilen är den första operationen eftersom Bates‑numreringsmotorn arbetar på en befintlig `Document`‑instans.

```csharp
using Aspose.Pdf;

// ...

// Replace with the path to your input PDF
string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Load the PDF document into memory
Document doc = new Document(inputPath);
```

**Varför detta är viktigt:** `Document`‑klassen analyserar PDF‑strukturen och ger dig åtkomst till sidor, annotationer och metadata. Utan att först läsa in filen kan du inte applicera någon numrering.

## Steg 3: Konfigurera Bates‑numreringsalternativ

Skapa ett `BatesNumberingOptions`‑objekt och ange önskat prefix, startnummer och eventuella formateringsparametrar.

```csharp
using Aspose.Pdf;

// ...

BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Text that appears before the numeric part
    Prefix = "CASE01",

    // First number to use (1 means the first page gets CASE01-1)
    StartNumber = 1,

    // Optional: customize the appearance
    // The default places the number in the footer, centered.
    // You can change Font, FontSize, Color, and Position if needed.
    // Example:
    // Font = FontRepository.FindFont("Arial"),
    // FontSize = 10,
    // Color = Color.Black,
    // Margin = new Margin(0, 0, 0, 20)
};
```

**Varför detta är viktigt:** `BatesNumberingOptions` talar om för Aspose.PDF hur etiketten för varje sida ska genereras. `Prefix` hjälper dig att gruppera relaterade ärenden, medan `StartNumber` låter dig fortsätta en sekvens från en tidigare batch.

## Steg 4: Spara PDF‑filen med Bates‑nummer applicerade

Skicka alternativ‑objektet till `Save`‑metoden. Aspose.PDF skriver numren direkt på varje sida.

```csharp
// Replace with the desired output path
string outputPath = @"YOUR_DIRECTORY\output.pdf";

// Save the document, applying the Bates numbering
doc.Save(outputPath, batesOptions);
```

**Varför detta är viktigt:** Överlagringen `Save(string, BatesNumberingOptions)` kombinerar renderingssteget med numreringsprocessen, vilket säkerställer att utdatafilen innehåller de synliga identifierarna.

## Fullt exempel – allt tillsammans

Nedan är ett enda, självständigt program som du kan kopiera, klistra in och köra. Det demonstrerar **hur du lägger till Bates‑numrering** från början till slut.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the PDF document
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Set up Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                Prefix = "CASE01",
                StartNumber = 1,
                // Optional appearance tweaks:
                // Font = FontRepository.FindFont("Times New Roman"),
                // FontSize = 9,
                // Color = Color.DarkBlue,
                // Margin = new Margin(0, 0, 0, 15)
            };

            // 3️⃣ Save the document with Bates numbers
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath, batesOptions);

            Console.WriteLine($"Bates numbering added. Output saved to: {outputPath}");
        }
    }
}
```

### Förväntad utdata

När programmet körs skapas `output.pdf` där varje sida visar en etikett liknande:

```
CASE01-1
CASE01-2
CASE01-3
...
```

Numren visas som standard i sidfoten, men du kan flytta dem genom att justera `Margin`‑egenskapen i `BatesNumberingOptions`.

## Edge cases och vanliga variationer

| Situation | Vad som bör justeras |
|-----------|----------------------|
| **Olika prefix per batch** | Ändra `Prefix` innan du anropar `Save`. Du kan loopa över flera dokument med olika prefix. |
| **Fortsätt numrering från en tidigare fil** | Sätt `StartNumber` till det sista använda numret + 1. |
| **Placera nummer i sidhuvudet** | Använd `batesOptions.Margin = new Margin(20, 0, 0, 0);` (övre marginal) eller anpassa `batesOptions.Position`. |
| **Eget teckensnitt eller färg** | Tilldela `Font`, `FontSize` och `Color`‑egenskaperna enligt den kommenterade sektionen. |
| **Stora PDF‑filer (1000+ sidor)** | Operationen är minnes‑effektiv; du kan dock vilja aktivera `doc.OptimizeResources()` innan du sparar för att minska filstorleken. |

**Proffstips:** Om ditt arbetsflöde kräver olika numreringsscheman per dokument, kapsla in logiken i en hjälpfunktion:

```csharp
static void ApplyBatesNumbering(string src, string dst, string prefix, int start)
{
    var doc = new Document(src);
    var opts = new BatesNumberingOptions { Prefix = prefix, StartNumber = start };
    doc.Save(dst, opts);
}
```

## Slutsats

Du vet nu **hur du lägger till Bates‑numrering** i vilken PDF som helst med Aspose.PDF i C#. Tutorialen gick igenom hur du läser in PDF‑dokumentet, konfigurerar numreringsalternativen och sparar den slutgiltiga filen – allt i ett enda körbart program.  

Härifrån kan du utforska relaterade ämnen som **lägga till vattenstämplar**, **sammanfoga flera PDF‑filer** eller **extrahera text** med Aspose.PDF. Experimentera med olika teckensnitt, färger och positioner för att matcha din organisations formateringsstandarder.

Redo att automatisera ditt juridiska dokumentflöde? Lägg till koden i din byggpipeline, kör den mot batcher av filer och låt Aspose.PDF sköta det tunga arbetet. Lycka till med kodandet!


## Vad bör du lära dig härnäst?


Följande tutorialer täcker nära besläktade ämnen som bygger vidare på de tekniker som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Create PDF Document C# – Add Bates Numbering](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/)
- [Add Bates Numbering PDF – Step‑by‑Step Guide to Number PDF Pages](/pdf/english/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/)
- [Aspose PDF Tutorial – Insert a Blank Page and Update Bates Numbering](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}