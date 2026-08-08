---
category: general
date: 2026-06-21
description: Add bates numbering pdf and learn how to add bates numbers, convert pdf
  to pdf/x-4, convert pdf to pdfa-4, and digitally sign pdf c# in a single walkthrough.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbers
- digitally sign pdf c#
- convert pdf to pdf/x-4
- convert pdf to pdfa-4
language: en
og_description: Add bates numbering pdf, see how to add bates numbers, convert pdf
  to pdf/x-4, convert pdf to pdfa-4, and digitally sign pdf c# with Aspose.Pdf.
og_title: Add Bates Numbering PDF – Step‑by‑Step C# Tutorial
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
title: Add Bates Numbering PDF – Complete C# Guide with Signing & Conversion
url: /net/programming-with-security-and-signatures/add-bates-numbering-pdf-complete-c-guide-with-signing-conver/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Bates Numbering PDF – Complete C# Guide with Signing & Conversion

Ever wondered **add bates numbering pdf** without pulling your hair out? You're not the only one. Legal teams, auditors, and anyone who needs traceable documents constantly ask *how to add bates numbers* to a PDF, and then they also need the file to meet PDF/X‑4 or PDF/A‑4 standards and be digitally signed.  

In this tutorial we’ll walk through exactly that—using Aspose.Pdf for .NET we’ll **add bates numbering pdf**, show **how to add bates numbers**, **convert pdf to pdf/x-4**, **convert pdf to pdfa-4**, and finally **digitally sign pdf c#**. By the end you’ll have a ready‑to‑run program that produces three polished PDFs: a PDF/X‑4 version, a Bates‑numbered version, and a digitally signed version.

![add bates numbering pdf example](image-placeholder.png "Screenshot showing add bates numbering pdf in action")

## What You’ll Need

- **.NET 6+** (or .NET Framework 4.6+). Aspose.Pdf supports both.
- A **valid Aspose.Pdf for .NET license** (or you can work with the evaluation, but watermarks will appear).
- A **PKCS#7 certificate file** (`.pfx`) and its password for signing.
- The **sample PDF** you want to transform (place it in a folder you control).
- Visual Studio, Rider, or any C# IDE you like.

That’s it—no extra NuGet packages beyond `Aspose.Pdf`. If you haven’t added the library yet, run:

```bash
dotnet add package Aspose.Pdf
```

Now let’s dive into the code.

## Step 1: Load the Source PDF Document

First, we need to bring the original file into memory. This is the foundation for every later operation.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

// Load the source PDF – adjust the path to your environment
var document = new Document("YOUR_DIRECTORY/sample.pdf");
```

> **Why this matters:** Loading the PDF creates a `Document` object that represents the entire file, giving us access to conversion, form fields, and security APIs.

## Step 2: Convert PDF to PDF/X‑4 (PDF/A‑4 Compliance)

If your workflow demands archival quality, PDF/X‑4 (a subset of PDF/A‑4) is the way to go. Here’s how to **convert pdf to pdf/x-4** with Aspose.

```csharp
// Set conversion options – PDF/X‑4 is the target format
var conversionOptions = new PdfFormatConversionOptions(PdfFormat.PDF_X_4, ConvertErrorAction.Delete);

// Perform the conversion
document.Convert(conversionOptions);
```

> **Tip:** The `ConvertErrorAction.Delete` flag strips out any content that would break compliance, ensuring a clean PDF/X‑4 output.

## Step 3: Save the PDF/X‑4 Version

Now that the document complies with PDF/X‑4, we persist it to disk.

```csharp
document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");
```

You now have a **convert pdf to pdfa-4**‑compatible file (PDF/X‑4 is a member of the PDF/A‑4 family). Feel free to open it in Acrobat to verify the compliance badge.

## Step 4: Add Bates Numbering – The Core of “Add Bates Numbering PDF”

Bates numbering is a sequential identifier placed on each page. This is the exact answer to *how to add bates numbers* programmatically.

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

> **Why this works:** `AddBatesNumbering` walks through every page and stamps the number in the default location (bottom‑right). You can later tweak the position via `BatesNumberingOptions` if needed.

## Step 5: Save the Bates‑Numbered PDF

After we’ve **add bates numbering pdf**, we need a separate file that preserves the numbers.

```csharp
document.Save("YOUR_DIRECTORY/sample_bates.pdf");
```

Open the file; you should see “CASE‑5000”, “CASE‑5001”, and so on at the bottom of each page.

## Step 6: Digitally Sign PDF – “Digitally Sign PDF C#” in Action

A digital signature guarantees authenticity and integrity. Below we’ll **digitally sign pdf c#** using a SHA‑384 hash.

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

> **Pro tip:** The `Rectangle` defines where the visible signature appears. If you don’t need a visual cue, set `signatureAppearance` to `false`.

## Step 7: Save the Digitally Signed PDF

Finally, write the signed document to disk.

```csharp
signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
```

You now have a **digitally sign pdf c#** file that can be validated in any PDF reader supporting digital signatures.

## Full Source Code – One‑Stop Solution

Below is the complete, ready‑to‑run program that ties everything together. Copy‑paste, adjust the paths, and hit **F5**.

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

### Expected Output

| File | Purpose | Key Feature |
|------|---------|-------------|
| `sample_pdfx4.pdf` | PDF/X‑4 version | Meets PDF/A‑4 compliance |
| `sample_bates.pdf` | Bates‑numbered PDF | **add bates numbering pdf** applied |
| `sample_signed.pdf` | Digitally signed PDF | **digitally sign pdf c#** with SHA‑384 |

Open any of the three files in Adobe Acrobat Reader; you’ll see the Bates numbers on the second file and a signature field on the third.

## Frequently Asked Questions (FAQ)

**Q: Can I change the position of the Bates numbers?**  
A: Yes. Use `BatesNumberingOptions` properties such as `Location` and `FontSize` to fine‑tune placement.

**Q: What if I need PDF/A‑4 instead of PDF/X‑4?**  
A: Switch `PdfFormat.PDF_X_4` to `PdfFormat.PDFA_4` in the conversion options. That satisfies the **convert pdf to pdfa-4** requirement.

**Q: My certificate uses a different hash algorithm—can I use SHA‑256?**  
A: Absolutely. Replace `DigestHashAlgorithm.Sha384` with `DigestHashAlgorithm.Sha256` (or any supported algorithm).

**Q: Do I need to call `document.Save` after each step?**  
A: Not strictly. In this flow we save after conversion and after Bates numbering to give you intermediate files. You could defer saving until the end if you prefer a single write operation.

## Wrap‑Up

We’ve just demonstrated a practical, end‑to‑end solution that **add bates numbering pdf**, explains **how to add bates numbers**, shows **convert pdf to pdf/x-4**, covers


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/german/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/french/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/japanese/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}