---
category: general
date: 2026-06-21
description: Lägg till Bates‑numrering i PDF och lär dig hur du lägger till Bates‑nummer,
  konverterar PDF till PDF/X‑4, konverterar PDF till PDF/A‑4 och digitalt signerar
  PDF med C# i en enda genomgång.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbers
- digitally sign pdf c#
- convert pdf to pdf/x-4
- convert pdf to pdfa-4
language: sv
og_description: Lägg till Bates‑numrering i PDF, se hur du lägger till Bates‑nummer,
  konvertera PDF till PDF/X‑4, konvertera PDF till PDF/A‑4, och signera PDF digitalt
  med C# och Aspose.Pdf.
og_title: Lägg till Bates-nummerering i PDF – Steg‑för‑steg C#‑handledning
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add bates numbering pdf and learn how to add bates numbers, convert
    pdf to pdf/x-4, convert pdf to pdfa-4, and digitally sign pdf c# in a single walkthrough.
  headline: Add Bates Numbering PDF – Complete C# Guide with Signing & Conversion
  type: TechArticle
- questions:
  - answer: Yes. Use `BatesNumberingOptions` properties such as `Location` and `FontSize`
      to fine‑tune placement.
    question: Can I change the position of the Bates numbers?
  - answer: Switch `PdfFormat.PDF_X_4` to `PdfFormat.PDFA_4` in the conversion options.
      That satisfies the **convert pdf to pdfa-4** requirement.
    question: What if I need PDF/A‑4 instead of PDF/X‑4?
  - answer: Absolutely. Replace `DigestHashAlgorithm.Sha384` with `DigestHashAlgorithm.Sha256`
      (or any supported algorithm).
    question: My certificate uses a different hash algorithm—can I use SHA‑256?
  - answer: 'Not strictly. In this flow we save after conversion and after Bates numbering
      to give you intermediate files. You could defer saving until the end if you
      prefer a single write operation. ## Wrap‑Up We’ve just demonstrated a practical,
      end‑to‑end solution that **add bates numbering pdf**, explains **'
    question: Do I need to call `document.Save` after each step?
  type: FAQPage
tags:
- Aspose.Pdf
- C#
- PDF processing
- Bates numbering
title: Lägg till Bates-nummerering i PDF – Komplett C#-guide med signering och konvertering
url: /sv/net/programming-with-security-and-signatures/add-bates-numbering-pdf-complete-c-guide-with-signing-conver/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till Bates‑numrering PDF – Komplett C#‑guide med signering & konvertering

Har du någonsin funderat på **add bates numbering pdf** utan att dra i håret? Du är inte ensam. Juridiska team, revisorer och alla som behöver spårbara dokument frågar ständigt *hur man lägger till bates‑nummer* i en PDF, och de behöver dessutom att filen uppfyller PDF/X‑4‑ eller PDF/A‑4‑standarderna samt är digitalt signerad.  

I den här handledningen går vi igenom exakt det – med Aspose.Pdf för .NET **add bates numbering pdf**, visar **how to add bates numbers**, **convert pdf to pdf/x-4**, **convert pdf to pdfa-4**, och slutligen **digitally sign pdf c#**. När du är klar har du ett färdigt program som producerar tre polerade PDF‑filer: en PDF/X‑4‑version, en Bates‑numrerad version och en digitalt signerad version.

![add bates numbering pdf example](image-placeholder.png "Skärmbild som visar add bates numbering pdf i aktion")

## Vad du behöver

- **.NET 6+** (eller .NET Framework 4.6+). Aspose.Pdf stödjer båda.
- En **giltig Aspose.Pdf for .NET‑licens** (eller så kan du använda utvärderingsversionen, men vattenstämplar visas).
- En **PKCS#7‑certifikatfil** (`.pfx`) och dess lösenord för signering.
- **Exempel‑PDF‑filen** du vill transformera (placera den i en mapp du kontrollerar).
- Visual Studio, Rider eller någon annan C#‑IDE du föredrar.

Det är allt – inga extra NuGet‑paket utöver `Aspose.Pdf`. Om du ännu inte har lagt till biblioteket, kör:

```bash
dotnet add package Aspose.Pdf
```

Nu dyker vi ner i koden.

## Steg 1: Läs in källdokumentet PDF

Först måste vi läsa in den ursprungliga filen i minnet. Detta är grunden för alla efterföljande operationer.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

// Load the source PDF – adjust the path to your environment
var document = new Document("YOUR_DIRECTORY/sample.pdf");
```

> **Varför detta är viktigt:** Att ladda PDF‑en skapar ett `Document`‑objekt som representerar hela filen och ger oss åtkomst till konverterings‑, formulär‑ och säkerhets‑API:er.

## Steg 2: Konvertera PDF till PDF/X‑4 (PDF/A‑4‑kompatibilitet)

Om ditt arbetsflöde kräver arkiveringskvalitet är PDF/X‑4 (en underuppsättning av PDF/A‑4) rätt väg. Så här **convert pdf to pdf/x-4** med Aspose.

```csharp
// Set conversion options – PDF/X‑4 is the target format
var conversionOptions = new PdfFormatConversionOptions(PdfFormat.PDF_X_4, ConvertErrorAction.Delete);

// Perform the conversion
document.Convert(conversionOptions);
```

> **Tips:** Flaggan `ConvertErrorAction.Delete` tar bort allt innehåll som skulle bryta mot kompatibiliteten och säkerställer en ren PDF/X‑4‑utgång.

## Steg 3: Spara PDF/X‑4‑versionen

Nu när dokumentet uppfyller PDF/X‑4 sparar vi det till disk.

```csharp
document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");
```

Du har nu en **convert pdf to pdfa-4**‑kompatibel fil (PDF/X‑4 är en medlem av PDF/A‑4‑familjen). Öppna den gärna i Acrobat för att verifiera kompatibilitets‑märket.

## Steg 4: Lägg till Bates‑numrering – Kärnan i “Add Bates Numbering PDF”

Bates‑numrering är en sekventiell identifierare som placeras på varje sida. Detta är det exakta svaret på *how to add bates numbers* programmässigt.

```csharp
// Configure Bates numbering options
var batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",   // Optional prefix
    Start = 5000        // Starting number
};

// Apply Bates numbering to the document
document.AddBatesNumbering(batesOptions);
```

> **Varför detta fungerar:** `AddBatesNumbering` går igenom varje sida och stämplar numret på standardpositionen (nedre‑höger). Du kan senare justera positionen via `BatesNumberingOptions` om så önskas.

## Steg 5: Spara den Bates‑numrerade PDF‑en

Efter att vi har **add bates numbering pdf** behöver vi en separat fil som bevarar numreringen.

```csharp
document.Save("YOUR_DIRECTORY/sample_bates.pdf");
```

Öppna filen; du bör se “CASE‑5000”, “CASE‑5001” osv. längst ner på varje sida.

## Steg 6: Digitalt signera PDF – “Digitally Sign PDF C#” i praktiken

En digital signatur garanterar äkthet och integritet. Nedan **digitally sign pdf c#** med en SHA‑384‑hash.

```csharp
// Prepare the signature handler
var signature = new PdfFileSignature(document);

// Load the PKCS#7 certificate (adjust password)
var pkcs7 = new PKCS7Detached(
    "YOUR_DIRECTORY/mycert.pfx", // Path to .pfx
    "pwd",                       // Certificate password
    DigestHashAlgorithm.Sha384   // Strong hashing algorithm
);

// Sign page 1, place signature rectangle at (100,100)-(200,150)
signature.Sign(
    pageNumber: 1,
    signatureAppearance: true,
    rectangle: new Rectangle(100, 100, 200, 150),
    pkcs7: pkcs7
);
```

> **Pro‑tips:** `Rectangle` definierar var den synliga signaturen visas. Om du inte behöver en visuell indikation, sätt `signatureAppearance` till `false`.

## Steg 7: Spara den digitalt signerade PDF‑en

Till sist skriver vi den signerade dokumentet till disk.

```csharp
signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
```

Du har nu en **digitally sign pdf c#**‑fil som kan valideras i vilken PDF‑läsare som helst som stödjer digitala signaturer.

## Fullständig källkod – All‑i‑ett‑lösning

Nedan är det kompletta, färdiga programmet som binder ihop allt. Kopiera‑klistra, justera sökvägarna och tryck **F5**.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source PDF document
        // -------------------------------------------------
        var document = new Document("YOUR_DIRECTORY/sample.pdf");

        // -------------------------------------------------
        // Step 2: Convert the document to PDF/X‑4 format
        // (PDF/A‑4 compliance)
        // -------------------------------------------------
        var conversionOptions = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_4,
            ConvertErrorAction.Delete);
        document.Convert(conversionOptions);

        // -------------------------------------------------
        // Step 3: Save the PDF/X‑4 version
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");

        // -------------------------------------------------
        // Step 4: Add Bates numbering – how to add bates numbers
        // -------------------------------------------------
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 5000
        };
        document.AddBatesNumbering(batesOptions);

        // -------------------------------------------------
        // Step 5: Save the Bates‑numbered PDF
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_bates.pdf");

        // -------------------------------------------------
        // Step 6: Sign the document using SHA‑384 hashing
        // -------------------------------------------------
        var signature = new PdfFileSignature(document);
        var pkcs7 = new PKCS7Detached(
            "YOUR_DIRECTORY/mycert.pfx",
            "pwd",
            DigestHashAlgorithm.Sha384);
        signature.Sign(
            pageNumber: 1,
            signatureAppearance: true,
            rectangle: new Rectangle(100, 100, 200, 150),
            pkcs7: pkcs7);

        // -------------------------------------------------
        // Step 7: Save the digitally signed PDF
        // -------------------------------------------------
        signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
    }
}
```

### Förväntad utdata

| Fil | Syfte | Nyckelfunktion |
|------|---------|-------------|
| `sample_pdfx4.pdf` | PDF/X‑4‑version | Uppfyller PDF/A‑4‑kompatibilitet |
| `sample_bates.pdf` | Bates‑numrerad PDF | **add bates numbering pdf** tillämpad |
| `sample_signed.pdf` | Digitalt signerad PDF | **digitally sign pdf c#** med SHA‑384 |

Öppna någon av de tre filerna i Adobe Acrobat Reader; du ser Bates‑numren i den andra filen och ett signaturfält i den tredje.

## Vanliga frågor (FAQ)

**Q: Kan jag ändra positionen för Bates‑numren?**  
A: Ja. Använd egenskaper i `BatesNumberingOptions` såsom `Location` och `FontSize` för att finjustera placeringen.

**Q: Vad händer om jag behöver PDF/A‑4 istället för PDF/X‑4?**  
A: Byt `PdfFormat.PDF_X_4` till `PdfFormat.PDFA_4` i konverteringsalternativen. Det uppfyller kravet **convert pdf to pdfa-4**.

**Q: Mitt certifikat använder en annan hash‑algoritm – kan jag använda SHA‑256?**  
A: Absolut. Ersätt `DigestHashAlgorithm.Sha384` med `DigestHashAlgorithm.Sha256` (eller någon annan stödjande algoritm).

**Q: Måste jag anropa `document.Save` efter varje steg?**  
A: Inte nödvändigt. I detta flöde sparar vi efter konvertering och efter Bates‑numrering för att ge dig mellanfiler. Du kan skjuta upp sparandet till slutet om du föredrar en enda skrivoperation.

## Sammanfattning

Vi har just demonstrerat en praktisk, end‑to‑end‑lösning som **add bates numbering pdf**, förklarar **how to add bates numbers**, visar **convert pdf to pdf/x-4**, och täcker

## Vad bör du lära dig härnäst?

Följande handledningar behandlar nära besläktade ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationssätt i dina egna projekt.

- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/german/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/french/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/japanese/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}