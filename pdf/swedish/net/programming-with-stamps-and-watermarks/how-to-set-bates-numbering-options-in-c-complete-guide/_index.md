---
category: general
date: 2026-08-14
description: Hur man ställer in Bates‑numreringsalternativ i C# med GroupDocs. Följ
  den här steg‑för‑steg‑handledningen för att lägga till anpassade prefix och startnummer
  när du konverterar Word till PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set bates numbering options
- Bates numbering C#
- GroupDocs API
- document conversion C#
- AddBatesNumbering method
- C# PDF generation
language: sv
lastmod: 2026-08-14
og_description: Hur du snabbt ställer in Bates-nummereringsalternativ i C#. Den här
  guiden visar hur du lägger till anpassade prefix och startnummer när du konverterar
  Word till PDF.
og_image_alt: Screenshot of C# code applying Bates numbering to a PDF
og_title: Hur man ställer in Bates‑nummereringsalternativ i C# – steg‑för‑steg‑handledning
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  headline: How to set bates numbering options in C# – complete guide
  type: TechArticle
- description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  name: How to set bates numbering options in C# – complete guide
  steps:
  - name: '`Document` – loads the source file.'
    text: '`Document` – loads the source file.'
  - name: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
    text: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
  - name: '`AddBatesNumbering` – the method that injects the numbering into each page.'
    text: '`AddBatesNumbering` – the method that injects the numbering into each page.'
  type: HowTo
tags:
- Bates numbering
- C#
- .NET
- GroupDocs
- PDF conversion
title: Hur man ställer in Bates-nummereringsalternativ i C# – komplett guide
url: /sv/net/programming-with-stamps-and-watermarks/how-to-set-bates-numbering-options-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man ställer in Bates‑numreringsalternativ i C# – komplett guide

Om du behöver **how to set bates numbering options** i C#, så guidar den här guiden dig genom de exakta stegen. Du kommer att lära dig hur du konfigurerar startnumret, lägger till ett prefix och tillämpar numreringen medan du konverterar ett Word‑dokument till PDF med hjälp av GroupDocs API.

Dokumentbehandling kräver ofta unika identifierare på varje sida för juridiska eller arkiveringsändamål. I slutet av den här handledningen har du ett återanvändbart kodsnutt som du kan släppa in i vilket .NET‑projekt som helst, oavsett om du bygger ett verktyg för rättsligt stöd eller en automatiserad rapportgenerator. Inga externa verktyg behövs – bara GroupDocs.Conversion‑biblioteket och några rader C#.

## Vad du behöver

Innan du börjar, se till att du har:

* .NET 6.0 SDK eller senare installerat  
* Visual Studio 2022 (eller någon IDE som stödjer .NET)  
* En giltig GroupDocs.Conversion‑licens (gratis provversion fungerar för testning)  
* Ett exempel‑Word‑dokument (`input.docx`) som du vill numrera  

Dessa förutsättningar säkerställer att koden körs utan ytterligare konfiguration.

## Så ställer du in Bates‑numreringsalternativ – översikt

Kärnan i **how to set bates numbering options** ligger i tre objekt:

1. `Document` – laddar källfilen.  
2. `BatesNumberingOptions` – innehåller startnummer, prefix och andra formateringsdetaljer.  
3. `AddBatesNumbering` – metoden som injicerar numreringen på varje sida.

Att förstå varför varje del finns hjälper dig att anpassa lösningen till mer komplexa scenarier, såsom anpassade typsnitt eller flerspråkig numrering.

## Steg 1: Installera GroupDocs.Conversion NuGet‑paketet

Öppna en terminal i din lösningsmapp och kör:

```bash
dotnet add package GroupDocs.Conversion
```

GroupDocs‑API‑et tillhandahåller `Document`‑klassen och `AddBatesNumbering`‑utökningmetoden som används senare i guiden.

## Steg 2: Ladda källdokumentet

```csharp
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;

// Step 2: Load the source Word document
Document document = new Document(@"C:\Docs\input.docx");
```

*Varför detta steg?*  
Att ladda filen skapar en in‑memory‑representation som konverteringsmotorn kan manipulera. Utan en `Document`‑instans kan du inte applicera Bates‑numrering eller någon annan transformation.

## Steg 3: Skapa Bates‑numreringsalternativen

```csharp
// Step 3: Configure Bates numbering
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // The first page will be numbered 1000
    StartNumber = 1000,
    // Each page will be prefixed with "CASE-"
    Prefix = "CASE-",
    // Optional: set the number format (e.g., 4 digits)
    NumberFormat = "#0000",
    // Optional: choose where the number appears (header/footer)
    Position = BatesNumberingPosition.FooterRight
};
```

*Varför detta steg?*  
`BatesNumberingOptions` kapslar in alla inställningar du kan behöva när du **setting bates numbering options**. Genom att justera `StartNumber` och `Prefix` kan du anpassa utdata till ditt ärendehanteringssystem. `Position`‑egenskapen styr den visuella placeringen, vilket ofta är ett efterlevnadskrav.

## Steg 4: Tillämpa Bates‑numrering på dokumentet

```csharp
// Step 4: Apply the numbering to every page
document.AddBatesNumbering(batesOptions);
```

`AddBatesNumbering`‑metoden går igenom varje sida i den laddade `Document` och infogar den konfigurerade strängen. Eftersom metoden arbetar på in‑memory‑representationen kan du kedja ytterligare bearbetningssteg (t.ex. vattenstämpel) innan du sparar.

## Steg 5: Konvertera och spara resultatet som PDF

```csharp
// Step 5: Define PDF conversion options (optional)
PdfConvertOptions pdfOptions = new PdfConvertOptions
{
    // Preserve original layout
    EmbedStandardFonts = true
};

// Save the numbered document as PDF
document.Save(@"C:\Docs\output.pdf", pdfOptions);
```

*Varför detta steg?*  
Att spara som PDF är ett vanligt slutformat för juridiska dokument. `PdfConvertOptions`‑objektet låter dig finjustera utdata, men det krävs inte för grundläggande numrering. `Save`‑anropet skriver den fullt numrerade PDF‑filen till disk.

## Komplett, körbart exempel

När allt sätts ihop, här är ett fristående konsolprogram som du kan kompilera och köra:

```csharp
using System;
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;
using GroupDocs.Conversion.Options.Convert.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the source Word document
            Document document = new Document(@"C:\Docs\input.docx");

            // Configure Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1000,
                Prefix = "CASE-",
                NumberFormat = "#0000",
                Position = BatesNumberingPosition.FooterRight
            };

            // Apply numbering to each page
            document.AddBatesNumbering(batesOptions);

            // Optional: set PDF conversion preferences
            PdfConvertOptions pdfOptions = new PdfConvertOptions
            {
                EmbedStandardFonts = true
            };

            // Save the numbered PDF
            document.Save(@"C:\Docs\output.pdf", pdfOptions);

            Console.WriteLine("Bates numbering applied successfully. Output saved to output.pdf");
        }
    }
}
```

**Förväntat resultat**

När programmet körs skapas `output.pdf` där varje sida visar en etikett som `CASE-1000`, `CASE-1001` osv., placerad i högra sidfoten. Öppna PDF‑filen i någon visare för att verifiera att siffrorna visas som avsett.

## Vanliga fallgropar och bästa praxis

| Problem | Varför det händer | Hur man undviker det |
|---------|-------------------|----------------------|
| **Relativa sökvägar orsakar `FileNotFoundException`** | Arbetskatalogen för ett konsolprogram kan skilja sig från Visual Studios. | Använd absoluta sökvägar eller `Path.Combine(AppContext.BaseDirectory, "input.docx")`. |
| **Numrering överlappar befintliga sidfötter** | Om källdokumentet redan har innehåll i det valda sidfotområdet kan den nya siffran döljas. | Välj en annan `Position` (t.ex. `HeaderLeft`) eller justera källmall. |
| **Stora dokument är långsamma** | Bates‑numrering itererar över varje sida; minnesanvändning ökar med filstorleken. | Bearbeta dokumentet i delar med `Document.Split` om du överskrider 500 sidor. |
| **Licensutgång** | Gratisprovversionen av GroupDocs går ut efter 30 dagar, vilket orsakar ett undantag på `AddBatesNumbering`. | Använd en giltig licensnyckel innan dokumentet laddas: `License license = new License(); license.SetLicense("license.lic");`. |

**Proffstips:** Om du behöver ett annat nummerformat per ärende (t.ex. `2023-CASE-001`), bygg prefixet dynamiskt innan du skapar `BatesNumberingOptions`.

## Utöka lösningen

Samma **Bates numbering C#**‑metod fungerar med andra källformat såsom `.txt`, `.html` eller till och med bilder. Ändra bara filändelsen när du konstruerar `Document`‑objektet, så hanterar konverteringsmotorn resten.

Du kan också kombinera **document conversion C#** med OCR för skannade PDF‑filer:

```csharp
// Example: add OCR before numbering (requires GroupDocs.Viewer)
using GroupDocs.Viewer;
using GroupDocs.Viewer.Options;

Document scannedPdf = new Document(@"C:\Docs\scanned.pdf");
var viewer = new Viewer(scannedPdf);
var viewOptions = new HtmlViewOptions();
viewer.View(viewOptions); // OCR step
// Then apply Bates numbering as shown earlier
```

## Slutsats

Du vet nu **how to set bates numbering options** i C# från början till slut. Genom att skapa ett `BatesNumberingOptions`‑objekt, applicera det med `AddBatesNumbering` och spara resultatet som PDF kan du automatisera produktionen av juridiskt korrekta, unikt identifierade dokument.

Härifrån kan du utforska relaterade ämnen som **C# PDF generation**, **document conversion C#**, eller avancerade **GroupDocs API**‑funktioner som vattenstämpling och digitala signaturer. Experimentera med olika prefix, positioner och nummerformat för att passa ditt arbetsflöde.

Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker nära besläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Add Bates Numbering PDF in C# – Complete Guide](/pdf/english/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add a Text Stamp Footer in PDFs Using Aspose.PDF for .NET&#58; A Step‑By‑Step Guide](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}