---
category: general
date: 2026-10-07
description: Lär dig hur du lägger till bates‑nummerering i en PDF med C#. Denna steg‑för‑steg‑guide
  täcker också PDF‑sidnumrering och andra nummereringstrick.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- pdf page numbering
- number pdf pages
- how to add bates
- bates numbering pdf
language: sv
lastmod: 2026-10-07
og_description: Lägg till Bates‑nummerering i en PDF snabbt. Följ den här handledningen
  för att bemästra PDF‑sidnumrering, numrera PDF‑sidor och automatisera dokumentspårning.
og_image_alt: Screenshot of a PDF with Bates numbers added using Aspose.Pdf
og_title: Lägg till Bates-nummerering i PDF-filer i C# – komplett Aspose-guide
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  headline: How to add bates numbering to a PDF with Aspose.Pdf
  type: TechArticle
- description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  name: How to add bates numbering to a PDF with Aspose.Pdf
  steps:
  - name: 1. Can I change the location of the numbers?
    text: Yes. Set `batesOptions.Position = new Position(10, 10, 10, 10);` where the
      four values represent margins from the top, bottom, left, and right edges. Aspose
      also provides predefined enums such as `BatesNumberingPosition.BottomCenter`.
  - name: 2. What if my PDF already contains page numbers?
    text: Adding Bates numbers will **stack** on top of existing numbers. To avoid
      visual clutter, either hide the original numbers (if they are part of a text
      layer) or adjust the `batesOptions` font size and position.
  - name: 3. Does this work with encrypted PDFs?
    text: 'Aspose can open password‑protected PDFs if you supply the password:'
  - name: 4. How do I **number pdf pages** with a simple sequential counter (no prefix/suffix)?
    text: 'Just set `Prefix = string.Empty` and `Suffix = string.Empty`:'
  - name: 5. Can I use this approach in ASP.NET Core to serve PDFs on‑the‑fly?
    text: 'Absolutely. Load the document, apply the numbering, then write the stream
      to the HTTP response:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Hur man lägger till Bates-nummerering i en PDF med Aspose.Pdf
url: /sv/net/programming-with-pdf-pages/how-to-add-bates-numbering-to-a-pdf-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man lägger till Bates-numrering i en PDF med Aspose.Pdf

Om du behöver **lägga till Bates-numrering** i en PDF, visar den här guiden exakt hur du gör det i C#. Oavsett om du förbereder juridiska paket, hanterar ärendefiler, eller bara vill ha pålitlig **pdf sidnumrering**, ger stegen nedan en komplett, körbar lösning.

I den här tutorialen kommer du att lära dig hur du:

* Läser in en befintlig PDF-fil.
* Konfigurerar Bates-numreringsalternativ såsom prefix, startnummer, siffrutfyllnad, separator och suffix.
* Applicerar numreringen på varje sida.
* Sparar det uppdaterade dokumentet.

Inga externa verktyg krävs utöver Aspose.Pdf för .NET-biblioteket, och koden fungerar med .NET 6+ samt .NET Framework 4.7.2+.

---

## Förutsättningar

Innan du börjar, se till att du har:

| Requirement | Why it matters |
|-------------|----------------|
| **Aspose.Pdf for .NET** (NuGet package `Aspose.Pdf`) | Tillhandahåller klasserna `Document` och `BatesNumberingOptions` som används i koden. |
| **.NET SDK** (6.0 or later recommended) | Gör det möjligt att kompilera och köra C#-konsolapplikationen. |
| **A source PDF** you want to number | Tutorialen använder `source.pdf` som exempel; ersätt sökvägen med din egen fil. |
| **Write permission** to the output folder | `Save`-anropet måste skriva den nya filen. |

Du kan installera biblioteket med följande CLI-kommando:

```bash
dotnet add package Aspose.Pdf
```

---

## Steg 1: Skapa ett nytt konsolprojekt

Öppna en terminal och kör:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
```

Detta skapar ett minimalt C#-projekt som vi kommer att fylla med koden som behövs för att **lägga till Bates-numrering**.

---

## Steg 2: Lägg till de nödvändiga `using`-direktiven

Öppna `Program.cs` och lägg till namnutrymmena högst upp i filen:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

* `Aspose.Pdf` ger dig åtkomst till `Document`-klassen för att läsa in och spara PDF-filer.  
* `Aspose.Pdf.Text` innehåller `BatesNumberingOptions`, objektet som definierar hur siffrorna visas.

---

## Steg 3: Läs in käll-PDF:en

Den första handlingsbara raden läser in PDF:en du vill numrera. Ersätt `"YOUR_DIRECTORY/source.pdf"` med den faktiska sökvägen till din fil.

```csharp
// Load the source PDF
Document pdf = new Document("YOUR_DIRECTORY/source.pdf");
```

Om filen inte kan hittas kastar Aspose ett `FileNotFoundException`. För att undvika detta kan du vilja validera sökvägen i förväg:

```csharp
if (!System.IO.File.Exists("YOUR_DIRECTORY/source.pdf"))
{
    Console.WriteLine("Source PDF not found.");
    return;
}
```

---

## Steg 4: Definiera Bates-numreringsalternativ

`BatesNumberingOptions` låter dig kontrollera varje visuellt element i numreringen. Exemplet nedan visar en typisk konfiguration för juridiska ärendefiler:

```csharp
// Define Bates numbering options
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",          // Text before the numeric part
    StartNumber = 1000,       // First number to use
    Digits = 6,               // Pad with leading zeros (e.g., 001000)
    Separator = "-",          // Character between prefix, number, and suffix
    Suffix = "-2025"          // Text after the numeric part
};
```

**Varför varje egenskap är viktig**

| Property | Purpose |
|----------|---------|
| `Prefix` | Hjälper dig att gruppera dokument efter projekt, kund eller ärende. |
| `StartNumber` | Ställer in den initiala räknaren; användbart när du redan har befintliga numrerade filer. |
| `Digits` | Säkerställer en enhetlig bredd, vilket underlättar sortering. |
| `Separator` | Förbättrar läsbarheten, särskilt när du kombinerar prefix och suffix. |
| `Suffix` | Gör det möjligt att lägga till ett år, en version eller någon annan efterföljande identifierare. |

Du kan också kontrollera placeringen (top, bottom, left, right) och teckensnittsstilen genom att komma åt `batesOptions.Position` och `batesOptions.Font`. För de flesta scenarier fungerar standardinställningarna (nedre‑höger, 12‑pt Times New Roman) bra.

---

## Steg 5: Applicera numreringen på varje sida

Anropet `pdf.BatesNumbering.Add` infogar siffrorna på varje sida i den ordning de visas.

```csharp
// Apply Bates numbering to every page
pdf.BatesNumbering.Add(batesOptions);
```

Om du bara behöver **numrera pdf-sidor** på en delmängd (t.ex. hoppa över framsidan), kan du istället skicka en `PageCollection`:

```csharp
// Example: skip the first page
pdf.BatesNumbering.Add(batesOptions, pdf.Pages.Skip(1));
```

---

## Steg 6: Spara den uppdaterade PDF-filen

Slutligen skriver du det modifierade dokumentet till disk. Filnamnet speglar vanligtvis att PDF:en nu innehåller Bates-nummer.

```csharp
// Save the PDF with Bates numbers applied
pdf.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering added successfully.");
```

Om målmappen inte finns skapar Aspose den automatiskt. Du bör dock säkerställa att du har skrivbehörighet för att undvika ett `UnauthorizedAccessException`.

---

## Fullt, körbart exempel

När alla delar sätts ihop, är här ett komplett program som du kan kopiera, klistra in och köra:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source PDF
        // -------------------------------------------------
        const string inputPath = "YOUR_DIRECTORY/source.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        Document pdf = new Document(inputPath);

        // -------------------------------------------------
        // 2️⃣ Configure Bates numbering
        // -------------------------------------------------
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            Digits = 6,
            Separator = "-",
            Suffix = "-2025"
        };

        // -------------------------------------------------
        // 3️⃣ Apply the numbering to every page
        // -------------------------------------------------
        pdf.BatesNumbering.Add(batesOptions);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";
        pdf.Save(outputPath);
        Console.WriteLine($"Bates numbering added. Saved to {outputPath}");
    }
}
```

**Förväntad output** (konsol):

```
Bates numbering added. Saved to YOUR_DIRECTORY/bates_numbered.pdf
```

Öppna `bates_numbered.pdf` så kommer du att se varje sida märkt med något i stil med `CASE-001000-2025`, `CASE-001001-2025` osv., placerade i standardnedre‑höger hörnet.

---

## Vanliga frågor (FAQ)

### 1. Kan jag ändra placeringen av siffrorna?
Ja. Sätt `batesOptions.Position = new Position(10, 10, 10, 10);` där de fyra värdena representerar marginaler från toppen, botten, vänster och höger kant. Aspose tillhandahåller också fördefinierade enum:er såsom `BatesNumberingPosition.BottomCenter`.

### 2. Vad händer om min PDF redan innehåller sidnummer?
Att lägga till Bates-nummer kommer att **läggas ovanpå** befintliga nummer. För att undvika visuell rörighet, antingen dölj de ursprungliga numren (om de är en del av ett textlager) eller justera `batesOptions` teckenstorlek och position.

### 3. Fungerar detta med krypterade PDF-filer?
Aspose kan öppna lösenordsskyddade PDF-filer om du anger lösenordet:

```csharp
Document pdf = new Document("source.pdf", new LoadOptions { Password = "mySecret" });
```

### 4. Hur **numrerar jag pdf-sidor** med en enkel sekventiell räknare (utan prefix/suffix)?
Bara sätt `Prefix = string.Empty` och `Suffix = string.Empty`:

```csharp
BatesNumberingOptions simple = new BatesNumberingOptions
{
    StartNumber = 1,
    Digits = 4   // 0001, 0002, …
};
pdf.BatesNumbering.Add(simple);
```

### 5. Kan jag använda detta tillvägagångssätt i ASP.NET Core för att leverera PDF-filer i realtid?
Absolut. Läs in dokumentet, applicera numreringen och skriv sedan strömmen till HTTP-svaret:

```csharp
using (var ms = new MemoryStream())
{
    pdf.Save(ms);
    ms.Position = 0;
    return File(ms, "application/pdf", "bates_numbered.pdf");
}
```

---

## Särskilda fall och bästa praxis‑tips

| Situation | Recommended approach |
|-----------|----------------------|
| **Stora PDF-filer (hundratals sidor)** | Anropa `pdf.BatesNumbering.Add` **efter** att du har gjort eventuella sidnivå‑transformeringar för att undvika att bearbeta samma sidor flera gånger. |
| **Anpassade teckensnitt** | Sätt `batesOptions.Font = FontRepository.FindFont("Arial")` och justera `batesOptions.FontSize` för bättre läsbarhet på skannade dokument. |
| **Prestandakritiska batch‑jobb** | Återanvänd en enda `Document`‑instans när du bearbetar många filer i en loop; disponera den efter varje iteration för att frigöra minne. |
| **Internationella tecken** | Använd Unicode‑kompatibla teckensnitt (t.ex. `Times New Roman Unicode`) för att säkerställa att prefix eller suffix visas korrekt. |
| **Versionskompatibilitet** | Koden fungerar med Aspose.Pdf 23.10 och nyare. Om du riktar dig mot en äldre version, kontrollera API‑referensen för eventuella ändringar av egenskapsnamn. |

---

## Slutsats

Du vet nu hur du **lägger till Bates-numrering** i en PDF med Aspose.Pdf för .NET. Tutorialen täckte inläsning av en PDF, konfiguration av `BatesNumberingOptions`, applicering av siffrorna på varje sida och sparande av resultatet. Med dessa byggstenar kan du också implementera generell **pdf sidnumrering**, **numrera pdf-sidor** med anpassade format, och integrera processen i större automatiseringspipeline.

**Nästa steg**

* Utforska **bates numbering pdf**-API:n vidare för att anpassa teckensnitt, färg och placering.  
* Kombinera denna teknik med **digitala signaturer** för att skapa manipulering‑säkra juridiska paket.  
* Titta på Asposes **PDF-sammanslagning**-funktioner om du behöver sammanfoga flera ärendefiler innan numrering.

Känn dig fri att experimentera med olika prefix, suffix och siffrulängder för att matcha din organisations arkiveringsstandarder. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Create PDF Document C# – Add Bates Numbering Guide](/pdf/english/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/)
- [How to Add Bates Numbering in PDF with C# – Complete Guide](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-c-complete-guide/)
- [Aspose PDF Tutorial – Insert a Blank Page and Update Bates Numbering](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}