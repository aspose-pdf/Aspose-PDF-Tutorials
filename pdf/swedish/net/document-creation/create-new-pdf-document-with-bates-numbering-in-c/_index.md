---
category: general
date: 2026-08-04
description: Skapa ett nytt PDF-dokument i C# och lägg snabbt till Bates‑nummerering
  i PDF med Aspose.Pdf – lär dig att lägga till en tom PDF-sida och anpassade sidnummer.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new pdf document
- add bates numbering pdf
- how to add bates
- add blank page pdf
- add custom page numbers
language: sv
lastmod: 2026-08-04
og_description: Skapa ett nytt PDF-dokument i C# och automatiskt lägga till Bates‑numrering
  i PDF för juridisk ärendehantering – komplett kodexempel medföljer.
og_image_alt: Screenshot of a C# program creating a PDF document with Bates numbers
  applied
og_title: Skapa nytt PDF-dokument med Bates-nummerering i C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create new PDF document in C# and add Bates numbering pdf quickly using
    Aspose.Pdf – learn to add blank page pdf and custom page numbers.
  headline: Create new PDF document with Bates numbering in C#
  type: TechArticle
tags:
- C#
- PDF
- Aspose.Pdf
- Bates numbering
title: Skapa nytt PDF-dokument med Bates‑nummerering i C#
url: /sv/net/document-creation/create-new-pdf-document-with-bates-numbering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa nytt PDF-dokument med Bates-numrering i C#

Om du behöver **create new PDF document** i C# visar den här guiden hur du **add Bates numbering pdf** med Aspose.Pdf. Du kommer att lära dig att **add blank page pdf**, konfigurera **add custom page numbers**, och spara den slutliga filen.

Handledningen täcker varje steg från installation av biblioteket till att generera en PDF som uppfyller juridiska ärende‑filstandarder. I slutet kan du generera en PDF, infoga en tom sida, tillämpa Bates-nummer och anpassa nummerformatet — allt med ett enda körbart program.

## Förutsättningar

Innan du börjar, se till att du har:

* .NET 6.0 SDK eller senare installerat  
* Visual Studio 2022 (eller någon C#‑IDE)  
* En aktiv Aspose.Pdf för .NET-licens eller en gratis utvärderingsnyckel  

Du behöver inga ytterligare NuGet‑paket; handledningen installerar allt automatiskt.

## Steg 1: Installera Aspose.Pdf via NuGet

Öppna en terminal i din projektmapp och kör:

```bash
dotnet add package Aspose.Pdf
```

Kommandot lägger till den senaste stabila versionen av Aspose.Pdf i ditt projekt, vilket tillhandahåller `Document`, `BatesNumbering` och andra PDF‑manipuleringsklasser du kommer att använda.

## Steg 2: Skapa nytt PDF-dokument – initial konfiguration

Att skapa PDF-filen är grunden för alla efterföljande operationer. Klassen `Document` representerar hela PDF‑behållaren.

```csharp
using Aspose.Pdf;

// Step 2: Create a new PDF document
using var doc = new Document();
```

*Varför detta är viktigt*: Att instansiera `Document` allokerar de interna strukturer som krävs för sidor, teckensnitt och grafik. Att använda `using var` säkerställer att filen tas bort korrekt efter sparning.

## Steg 3: Lägg till tom sida pdf

En PDF måste innehålla minst en sida innan du kan placera innehåll på den. Att lägga till en tom sida ger dig en ren canvas för Bates-nummer.

```csharp
// Step 3: Add a blank page to the document
Page page = doc.Pages.Add();
```

`Pages.Add()`‑metoden lägger till en ny, tom sida i slutet av dokumentets sidainsamling. Du kan upprepa detta anrop för att lägga till fler sidor om du senare behöver **add custom page numbers** över flera sidor.

## Steg 4: Konfigurera Bates-numrering – hur man lägger till bates

Bates-numrering är en sekventiell identifierare som ofta används i juridiska dokument. Du konfigurerar den via klassen `BatesNumbering`.

```csharp
// Step 4: Set up Bates numbering options
var bates = new BatesNumbering
{
    StartNumber = 1000,      // Starting number for the sequence
    Prefix = "CaseA-",       // Text to prepend to each number
    Increment = 1,           // Increment between consecutive numbers
    // Optional: Set the location, font size, etc.
};
```

*Varför detta är viktigt*: `StartNumber` definierar det första numret, `Prefix` lägger till en läsbar etikett, och `Increment` styr steglängden. Du kan också justera `HorizontalAlignment`, `VerticalAlignment`, `FontSize` och `Margins` för att styra hur numret visas på varje sida.

## Steg 5: Tillämpa Bates-numrering pdf på sidan

Nu när nummeralternativen är klara, tillämpa dem på sidan (eller på hela dokumentet).

```csharp
// Step 5: Apply the Bates numbering to the page
bates.Apply(page);
```

Att anropa `Apply` infogar det formaterade numret i sidans sidfot som standard. Om du behöver numret någon annanstans, sätt `bates.Position` innan du anropar `Apply`.

## Steg 6: Spara PDF:en med tillämpade Bates-nummer

Slutligen, skriv det minnesbaserade dokumentet till disk.

```csharp
// Step 6: Save the PDF with Bates numbers applied
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumbered.pdf");

doc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

Den sparade filen innehåller nu en enda sida med Bates-numret **CaseA-1000** visat längst ner. Öppna PDF:en i någon visare för att verifiera numreringen.

## Förväntat resultat

När du öppnar `BatesNumbered.pdf` bör du se:

* En tom sida (eller fler om du har lagt till extra sidor)  
* Texten **CaseA-1000** placerad längst ner på sidan (standardposition)  

Om du lägger till fler sidor och återanvänder samma `BatesNumbering`‑instans, kommer numren att öka automatiskt (CaseA-1001, CaseA-1002, …).

## Proffstips: Lägga till anpassade sidnummer utöver Bates-nummer

Ibland behöver du både Bates-nummer och traditionella sidnummer. Du kan kombinera dem genom att lägga till ett `TextFragment` efter att ha tillämpat Bates-numrering:

```csharp
// Add a traditional page number in the header
var pageNumber = new TextFragment($"Page {page.Number}")
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Top,
    FontSize = 12,
    Font = FontRepository.FindFont("Arial")
};
page.Paragraphs.Add(pageNumber);
```

Detta kodsnutt demonstrerar **add custom page numbers** samtidigt som Bates‑etiketten bevaras.

## Edge case: Tillämpa Bates-numrering på flera sidor

Om ditt dokument innehåller flera sidor kan du tillämpa samma `BatesNumbering`‑instans på varje sida i en loop:

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    bates.Apply(doc.Pages[i]);
}
```

Loopen säkerställer att varje sida får ett sekventiellt nummer baserat på `StartNumber` och `Increment` som du definierade.

## Vanliga fallgropar och hur du undviker dem

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| Nummer visas off‑center | Standardjusteringen kanske inte matchar din layout | Sätt `bates.HorizontalAlignment` och `bates.VerticalAlignment` explicit |
| Nummer överlappar befintligt innehåll | Ingen marginal är definierad | Justera `bates.Margin` eller använd `bates.Position` för att flytta numret |
| Licensundantag vid körning | Utvärderingsversionen begränsar utdata | Applicera en giltig Aspose.Pdf‑licens innan du skapar dokumentet (`License license = new License(); license.SetLicense("Aspose.Pdf.lic");`) |

## Fullt fungerande exempel

Nedan är ett självständigt program som du kan kopiera, klistra in och köra.

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1. Create a new PDF document
        using var doc = new Document();

        // 2. Add a blank page pdf
        Page page = doc.Pages.Add();

        // 3. Configure Bates numbering – how to add bates
        var bates = new BatesNumbering
        {
            StartNumber = 1000,
            Prefix = "CaseA-",
            Increment = 1,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(20, 20, 20, 20),
            FontSize =


## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig behärska ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man lägger till och anpassar sidnummer i PDF‑filer med Aspose.PDF för .NET | Dokumentmanipuleringsguide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF .NET&#58; Lägg till sidnummer i PDF‑filer med FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Skapa PDF‑dokument med Aspose.PDF – Lägg till sida, form & spara](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}