---
category: general
date: 2026-08-08
description: Lägg till Bates‑nummerering i PDF med Aspose.Pdf i C#. Denna handledning
  visar också hur man lägger till en tom sida i en PDF och genererar PDF programatiskt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering pdf
- add blank page pdf
- generate pdf programmatically
- create pdf aspose
language: sv
lastmod: 2026-08-08
og_description: Lägg till Bates‑nummerering i PDF med Aspose.Pdf i C#. Lär dig att
  lägga till en tom PDF‑sida, generera PDF programatiskt och spara det färdiga dokumentet
  på några minuter.
og_image_alt: Screenshot of C# code adding Bates numbering and a blank page to a PDF
  using Aspose.Pdf
og_title: Lägg till Bates‑nummerering i PDF med Aspose – komplett C#‑guide
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  headline: Add bates numbering pdf with Aspose – step‑by‑step guide
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  name: Add bates numbering pdf with Aspose – step‑by‑step guide
  steps:
  - name: What if I need a different font or position?
    text: 'The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`,
      `HorizontalAlignment`, and `VerticalAlignment`. For example:'
  - name: How do I exclude a specific page from numbering?
    text: Create a separate `BatesNumberingArtifact` for the pages you want to number
      and add it only to those pages. Pages without an attached artifact will remain
      unnumbered.
  - name: Does this work with existing PDFs?
    text: 'Yes. Instead of `new Document()`, load an existing file:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF generation
- Bates numbering
title: Lägg till Bates‑nummerering i PDF med Aspose – steg‑för‑steg‑guide
url: /sv/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till Bates‑numrering pdf med Aspose – steg‑för‑steg guide

Att lägga till Bates‑numrering pdf med Aspose.Pdf är enkelt när du förstår de grundläggande stegen. Om du också behöver lägga till en tom sida pdf eller generera pdf programatiskt, täcker den här guiden allt du behöver.

I detta tutorial kommer du att:

* Skapa ett nytt PDF‑dokument från grunden.  
* Lägg till en tom sida pdf som kommer att innehålla Bates‑numren.  
* Konfigurera Bates‑numreringsartefakten med ett anpassat prefix.  
* Spara PDF‑en så att numren visas i den genererade filen.  

I slutet kommer du att ha en fullt fungerande C#‑konsolapplikation som producerar en PDF som innehåller Bates‑nummer som **CASE‑1000**, **CASE‑1001**, … – ett vanligt krav för juridiska och e‑discovery‑arbetsflöden.

## Förutsättningar

* .NET 6.0 SDK eller senare (koden fungerar också med .NET Framework 4.8).  
* Visual Studio 2022 eller någon C#‑kompatibel IDE.  
* En giltig Aspose.Pdf för .NET‑licens (eller en gratis utvärderingsnyckel).  
* Grundläggande kunskap om C#‑syntax.

> **Proffstips:** Om du kör koden utan licens kommer Aspose att lägga till ett litet vattenstämpel i den genererade PDF:en.

## Steg 1: Ställ in projektet och importera Aspose.Pdf

Skapa ett nytt konsolprojekt och lägg till Aspose.Pdf NuGet‑paketet:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

De `using`‑direktiv som krävs för exemplet är:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
```

Dessa namnrymder ger dig åtkomst till klasserna `Document`, `Page` och `BatesNumberingArtifact` som används senare.

## Steg 2: Lägg till en tom sida pdf

Ett Bates‑nummer måste fästas vid en sida, så vi skapar först en tom sida som kommer att ta emot numreringsartefakten.

```csharp
// Step 2: Add a blank page pdf
Document pdfDocument = new Document();          // creates an empty PDF
Page pdfPage = pdfDocument.Pages.Add();         // adds the first (blank) page
```

`Document`‑klassen representerar hela PDF‑filen, medan `Pages.Add()` infogar en ny, tom sida i slutet av dokumentets sidainsamling. Eftersom dokumentet börjar tomt skapar detta anrop även den första sidan.

## Steg 3: Konfigurera Bates‑numreringsartefakten

Nu definierar vi hur Bates‑numren ska se ut. `BatesNumberingArtifact` låter dig ange startnummer, prefix, suffix och formateringsalternativ.

```csharp
// Step 3: Define Bates numbering settings
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
{
    StartNumber = 1000,          // first number in the sequence
    Prefix = "CASE-",            // custom prefix before each number
    // Optional: you can also set Suffix, FontSize, FontColor, etc.
};
```

**Varför detta är viktigt:**  
Att sätta `StartNumber` till **1000** matchar vanliga juridiska ärendefils konventioner. `Prefix` säkerställer att varje nummer visas som **CASE‑1000**, **CASE‑1001**, … vilket gör det enklare att söka och sortera.

## Steg 4: Fäst artefakten på sidan

Artefakten måste läggas till sidans `Artifacts`‑samling så att Aspose renderar den på varje sida vid sparning.

```csharp
// Step 4: Attach the Bates numbering artifact to the PDF page
pdfPage.Artifacts.Add(batesArtifact);
```

När dokumentet sparas upprepar Aspose automatiskt artefakten på alla sidor och ökar numret för varje efterföljande sida.

## Steg 5: (Valfritt) Lägg till ytterligare sidor

Om du behöver fler sidor, upprepa helt enkelt `pdfDocument.Pages.Add()`. Bates‑numreringsartefakten du fäste i föregående steg kommer automatiskt att visas på varje ny sida.

```csharp
// Example: add two more pages
pdfDocument.Pages.Add();
pdfDocument.Pages.Add();
```

## Steg 6: Spara PDF – generera pdf programatiskt

Till sist sparas dokumentet till disk. Detta är punkten där Bates‑numren renderas på sidorna.

```csharp
// Step 6: Save the PDF – generate pdf programmatically
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumberedDocument.pdf");

// Ensure the directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);

pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to: {outputPath}");
```

**Förväntat resultat:**  
Öppna *BatesNumberedDocument.pdf* så ser du en tre‑sidig PDF. Varje sida visar ett Bates‑nummer i nedre högra hörnet:

* Sida 1 → **CASE‑1000**  
* Sida 2 → **CASE‑1001**  
* Sida 3 → **CASE‑1002**

Numren ökas automatiskt eftersom artefakten är fäst vid sidans samling.

## Fullt, körbart exempel

När vi sätter ihop allt, här är ett komplett konsolprogram som du kan kopiera, klistra in och köra:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new PDF document
            Document pdfDocument = new Document();

            // Add a blank page pdf
            Page pdfPage = pdfDocument.Pages.Add();

            // Define Bates numbering settings (add bates numbering pdf)
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
            {
                StartNumber = 1000,
                Prefix = "CASE-"
            };

            // Attach the artifact to the page
            pdfPage.Artifacts.Add(batesArtifact);

            // (Optional) add more pages to see incremented numbers
            pdfDocument.Pages.Add(); // page 2
            pdfDocument.Pages.Add(); // page 3

            // Save the PDF – generate pdf programmatically
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "BatesNumberedDocument.pdf");

            Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);
            pdfDocument.Save(outputPath);

            Console.WriteLine($"PDF saved to: {outputPath}");
        }
    }
}
```

Kör programmet med `dotnet run`. Efter körning, hitta filen på ditt skrivbord och verifiera Bates‑numren.

![Add bates numbering pdf example](/images/bates-numbering.png "Add bates numbering pdf example")

## Vanliga frågor och specialfall

### Vad händer om jag behöver ett annat teckensnitt eller en annan position?

`BatesNumberingArtifact` exponerar egenskaper som `FontSize`, `FontColor`, `HorizontalAlignment` och `VerticalAlignment`. Till exempel:

```csharp
batesArtifact.FontSize = 12;
batesArtifact.FontColor = Color.Blue;
batesArtifact.HorizontalAlignment = HorizontalAlignment.Left;
batesArtifact.VerticalAlignment = VerticalAlignment.Top;
```

### Hur exkluderar jag en specifik sida från numrering?

Skapa en separat `BatesNumberingArtifact` för de sidor du vill numrera och lägg till den endast på dessa sidor. Sidor utan en fäst artefakt förblir utan nummer.

### Fungerar detta med befintliga PDF-filer?

Ja. Istället för `new Document()`, ladda en befintlig fil:

```csharp
Document pdfDocument = new Document("input.pdf");
```

Fäst sedan artefakten på önskade sidor och spara.

## Slutsats

Du vet nu hur du **lägger till bates numbering pdf** med Aspose.Pdf, hur du **lägger till en tom sida pdf**, och hur du **genererar pdf programatiskt** i en ren, återanvändbar C#‑lösning. Metoden fungerar med valfritt antal sidor, anpassade prefix och stilalternativ, vilket ger dig full kontroll över det slutliga dokumentet.

Next steps you might explore:

* Use **create pdf as

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man lägger till och anpassar sidnummer i PDF:er med Aspose.PDF för .NET | Guide för dokumentmanipulation](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Hur man lägger till en tom sida i slutet av en PDF med Aspose.PDF för .NET | Steg‑för‑steg‑guide](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)
- [Skapa PDF-dokument med Aspose.PDF – Lägg till sida, form & spara](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}