---
category: general
date: 2026-02-28
description: Skapa PDF-dokument i C# med Bates-nummerering. Lär dig hur du lägger
  till Bates-nummerering i PDF, ställer in prefix och genererar sekventiella PDF-nummer
  i en enda genomgång.
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add document identification numbers
- add sequential pdf numbers
language: sv
og_description: Skapa PDF-dokument i C# med Bates-nummerering. Denna handledning visar
  hur du lägger till Bates-nummerering i PDF, ställer in anpassade prefix och genererar
  sekventiella PDF-nummer.
og_title: Skapa PDF-dokument C# – Lägg till Bates-nummerering
tags:
- Aspose.PDF
- C#
- PDF automation
title: Skapa PDF-dokument C# – Guide för att lägga till Bates-nummerering
url: /sv/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa PDF-dokument C# – Guide för att lägga till Bates‑nummer

Har du någonsin funderat på hur du **create PDF document C#** som redan har en unik identifierare på varje sida? Det är ett vanligt problem när du måste spåra juridiska filer, domstolsinlagor eller någon samling PDF‑filer som måste kunna sökas efter ett nummer. Den goda nyheten? Med Aspose.PDF kan du lägga till Bates‑nummer med bara några rader kod – ingen manuell redigering behövs.

I den här guiden går vi igenom hela processen: läsa in en befintlig PDF, konfigurera **add bates numbering pdf**, applicera numren och slutligen spara resultatet. När du är klar kan du **add document identification numbers** och till och med **add sequential PDF numbers** automatiskt, helt från C#.

## Förutsättningar

- .NET 6.0 eller senare (API‑et fungerar även med .NET Framework 4.5+)
- En licensierad kopia av **Aspose.PDF for .NET** (gratis provversion räcker för testning)
- En inmatnings‑PDF‑fil som du vill numrera (vi kallar den `input.pdf`)
- Visual Studio 2022 (eller någon annan IDE du föredrar)

Inga extra NuGet‑paket behövs utöver Aspose.PDF.

![Skapa PDF-dokument C# med Bates‑numrering](https://example.com/image.png "Create PDF Document C# example")

## Steg 1: Läs in käll‑PDF‑dokumentet

Innan du kan **add bates numbering pdf** behöver du ett `Document`‑objekt som representerar filen på disken.

```csharp
using Aspose.Pdf;

// Load the source PDF document
var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*Varför detta är viktigt*: `Document`‑klassen är ingångspunkten för varje operation i Aspose.PDF. Den abstraherar filsystemet så att du kan arbeta med sidor, kommentarer och metadata utan att röra de råa bytena.

> **Proffstips:** Om du bearbetar många filer i en loop, återanvänd samma `Document`‑instans endast när källan är identisk; annars, skapa ett nytt objekt för varje fil för att undvika minnesläckor.

## Steg 2: Definiera alternativ för Bates‑numrering

Här blir delen **how to add bates** konkret. Du konfigurerar ett `BatesNumberingOptions`‑objekt för att tala om för Aspose vilket prefix som ska användas, var numreringen ska börja och hur stor teckenstorlek som krävs.

```csharp
// Define Bates numbering options (prefix, start number, font size)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",   // You can change this to any string you need
    Start = 1000,      // Starting number – useful for continuous numbering across batches
    FontSize = 9       // Small enough to fit in the margin but still readable
};
```

*Varför detta är viktigt*: `Prefix` låter dig bädda in ett ärende‑identifierare (t.ex. “ABC-”). `Start`‑egenskapen är avgörande när du **adding sequential PDF numbers** över flera dokument – bara fortsätt att öka den. Och `FontSize` säkerställer att siffrorna inte skymmer befintligt innehåll.

## Steg 3: Applicera Bates‑numrering på hela dokumentet

Nu stämplar vi faktiskt numren på varje sida. Klassen `BatesNumbering` sköter allt det tunga arbetet.

```csharp
// Apply Bates numbering to the entire document
var bates = new BatesNumbering();
bates.AddBatesNumbering(pdfDocument, batesOptions);
```

*Varför detta är viktigt*: Under huven går Aspose igenom varje sida, beräknar rätt nummer (Prefix + (Start + pageIndex)) och ritar det i det nedre högra hörnet som standard. Du kan anpassa positionen senare, men standardinställningen fungerar för de flesta juridiska dokument.

> **Vanlig fråga:** *Vad händer om jag bara behöver numrera ett delmängd av sidor?*  
> Använd överlagringen `AddBatesNumbering(Document, BatesNumberingOptions, int startPage, int endPage)` för att begränsa intervallet.

## Steg 4: Spara PDF‑filen med Bates‑nummer applicerade

Det sista steget är att skriva tillbaka det modifierade dokumentet till disk.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*Varför detta är viktigt*: `Save`‑metoden respekterar det ursprungliga filformatet, så du får en standard‑PDF som vilken läsare som helst kan öppna – komplett med **add document identification numbers** på varje sida.

## Fullt fungerande exempel

Sätter vi ihop allt får du ett självständigt program som du kan klistra in i en ny konsolapp och köra direkt.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF document
            var inputPath = @"YOUR_DIRECTORY/input.pdf";
            var pdfDocument = new Document(inputPath);

            // 2️⃣ Define Bates numbering options (prefix, start number, font size)
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                FontSize = 9
            };

            // 3️⃣ Apply Bates numbering to the entire document
            var bates = new BatesNumbering();
            bates.AddBatesNumbering(pdfDocument, batesOptions);

            // 4️⃣ Save the PDF with Bates numbers applied
            var outputPath = @"YOUR_DIRECTORY/output.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbering added successfully. Output saved to {outputPath}");
        }
    }
}
```

**Förväntat resultat:** Öppna `output.pdf` i någon läsare; du kommer att se “ABC‑1000”, “ABC‑1001”, … utskrivna i varje sidas nedre högra hörn. Numren är markerbar text, så de är sökbara och kan kopieras – exakt vad du förväntar dig av en korrekt **add sequential PDF numbers**‑implementation.

## Kantfall & Variationer

### Anpassad positionering

Om standardhörnet kolliderar med befintliga sidfötter kan du flytta placeringen:

```csharp
batesOptions.Position = new Position(10, 10); // X, Y from the bottom‑left
```

### Olika nummerformat

Vill du ha nollutfyllda nummer (t.ex. 001000)? Använd `NumberFormat`:

```csharp
batesOptions.NumberFormat = "D6"; // Pads to 6 digits
```

### Flera filer i en batch

När du bearbetar många PDF‑filer, håll ett löpande räknare:

```csharp
int globalStart = 5000;
foreach (var file in Directory.GetFiles(@"YOUR_DIRECTORY\Batch", "*.pdf"))
{
    var doc = new Document(file);
    var opts = new BatesNumberingOptions
    {
        Prefix = "BATCH-",
        Start = globalStart,
        FontSize = 9
    };
    new BatesNumbering().AddBatesNumbering(doc, opts);
    doc.Save(Path.ChangeExtension(file, ".bated.pdf"));
    globalStart += doc.Pages.Count; // Increment for the next file
}
```

### Hantera lösenordsskyddade PDF‑filer

Om käll‑PDF‑filen är krypterad, skicka lösenordet när du skapar `Document`:

```csharp
var pdfDocument = new Document("protected.pdf", new LoadOptions { Password = "mySecret" });
```

## Vanliga frågor

| Fråga | Svar |
|----------|--------|
| **Kan jag använda ett annat bibliotek?** | Ja, bibliotek som iTextSharp eller PdfSharp stödjer också textinläggning på sidnivå, men Aspose.PDF erbjuder det mest raka API‑et för Bates‑numrering. |
| **Påverkar detta filstorleken?** | Att lägga till några byte text per sida är försumbar; den resulterande storleken ökar vanligtvis med mindre än 1 KB per sida. |
| **Är numreringen sökbar?** | Absolut. Aspose skriver numren som textobjekt, inte som bilder, så de indexeras av PDF‑läsare. |
| **Vad händer om jag vill ha ett annat teckensnitt?** | Sätt `batesOptions.Font` till ett `Font`‑objekt (t.ex. `FontRepository.FindFont("Arial")`). |

## Slutsats

Vi har just demonstrerat hur du **create PDF document C#** och omedelbart **add bates numbering pdf** med Aspose.PDF. Processen är enkel, pålitlig och fullt programmerbar – perfekt för juridiska firmor, myndigheter eller vilken organisation som helst som måste **add document identification numbers** och **add sequential PDF numbers** till stora mängder filer.

Ta detta som grund och experimentera: prova olika prefix för olika avdelningar, kedja numreringen över flera filer, eller bädda in QR‑koder bredvid Bates‑numren för extra spårbarhet. Himlen är gränsen när du har arbetsflödet på plats.

Om du fann den här handledningen användbar, dela den, lämna en kommentar eller utforska våra andra guider om PDF‑manipulering med C#. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}