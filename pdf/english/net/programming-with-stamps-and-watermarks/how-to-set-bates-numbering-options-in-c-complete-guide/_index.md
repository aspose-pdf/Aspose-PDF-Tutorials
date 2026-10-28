---
category: general
date: 2026-08-14
description: How to set bates numbering options in C# using GroupDocs. Follow this
  step‑by‑step tutorial to add custom prefixes and start numbers when converting Word
  to PDF.
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
language: en
lastmod: 2026-08-14
og_description: How to set bates numbering options in C# quickly. This guide shows
  you how to add custom prefixes and start numbers when converting Word to PDF.
og_image_alt: Screenshot of C# code applying Bates numbering to a PDF
og_title: How to set bates numbering options in C# – step‑by‑step tutorial
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
title: How to set bates numbering options in C# – complete guide
url: /net/programming-with-stamps-and-watermarks/how-to-set-bates-numbering-options-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to set bates numbering options in C# – complete guide

If you need **how to set bates numbering options** in C#, this guide walks you through the exact steps. You’ll learn how to configure the start number, add a prefix, and apply the numbering while converting a Word document to PDF using the GroupDocs API.

Document processing often requires unique identifiers on each page for legal or archival purposes. By the end of this tutorial you will have a reusable snippet that you can drop into any .NET project, whether you’re building a litigation support tool or an automated report generator. No external tools are needed—just the GroupDocs.Conversion library and a few lines of C#.

## What you’ll need

Before you start, make sure you have:

* .NET 6.0 SDK or later installed  
* Visual Studio 2022 (or any IDE that supports .NET)  
* A valid GroupDocs.Conversion license (the free trial works for testing)  
* A sample Word document (`input.docx`) you want to number  

These prerequisites ensure the code runs without additional configuration.

## How to set bates numbering options – overview

The core of **how to set bates numbering options** lies in three objects:

1. `Document` – loads the source file.  
2. `BatesNumberingOptions` – holds the start number, prefix, and other formatting details.  
3. `AddBatesNumbering` – the method that injects the numbering into each page.

Understanding why each piece exists helps you adapt the solution to more complex scenarios, such as custom fonts or multi‑language numbering.

## Step 1: Install the GroupDocs.Conversion NuGet package

Open a terminal in your solution folder and run:

```bash
dotnet add package GroupDocs.Conversion
```

The **GroupDocs API** provides the `Document` class and the `AddBatesNumbering` extension method used later in the tutorial.

## Step 2: Load the source document

```csharp
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;

// Step 2: Load the source Word document
Document document = new Document(@"C:\Docs\input.docx");
```

*Why this step?*  
Loading the file creates an in‑memory representation that the conversion engine can manipulate. Without a `Document` instance you cannot apply Bates numbering or any other transformation.

## Step 3: Create the Bates numbering options

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

*Why this step?*  
`BatesNumberingOptions` encapsulates all the settings you might need when **setting bates numbering options**. Adjusting `StartNumber` and `Prefix` lets you align the output with your case‑management system. The `Position` property controls visual placement, which is often a compliance requirement.

## Step 4: Apply Bates numbering to the document

```csharp
// Step 4: Apply the numbering to every page
document.AddBatesNumbering(batesOptions);
```

The `AddBatesNumbering` method walks through each page of the loaded `Document` and inserts the configured string. Because the method works on the in‑memory representation, you can chain additional processing steps (e.g., watermarking) before saving.

## Step 5: Convert and save the result as PDF

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

*Why this step?*  
Saving as PDF is a common final format for legal documents. The `PdfConvertOptions` object lets you fine‑tune the output, but it isn’t required for basic numbering. The `Save` call writes the fully numbered PDF to disk.

## Complete, runnable example

Putting everything together, here is a self‑contained console application you can compile and run:

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

**Expected output**

Running the program creates `output.pdf` where every page shows a label such as `CASE-1000`, `CASE-1001`, etc., positioned in the right footer. Open the PDF in any viewer to verify the numbers appear as intended.

## Common pitfalls and best practices

| Issue | Why it happens | How to avoid it |
|-------|----------------|-----------------|
| **Relative paths cause `FileNotFoundException`** | The working directory of a console app may differ from Visual Studio’s. | Use absolute paths or `Path.Combine(AppContext.BaseDirectory, "input.docx")`. |
| **Numbering overlaps existing footers** | If the source document already has content in the chosen footer area, the new number can be hidden. | Choose a different `Position` (e.g., `HeaderLeft`) or adjust the source template. |
| **Large documents are slow** | Bates numbering iterates over each page; memory usage grows with file size. | Process the document in chunks using `Document.Split` if you exceed 500 pages. |
| **License expiration** | The free trial of GroupDocs expires after 30 days, causing an exception on `AddBatesNumbering`. | Apply a valid license key before loading the document: `License license = new License(); license.SetLicense("license.lic");`. |

**Pro tip:** If you need a different number format per case (e.g., `2023-CASE-001`), build the prefix dynamically before creating `BatesNumberingOptions`.

## Extending the solution

The same **Bates numbering C#** approach works with other source formats such as `.txt`, `.html`, or even images. Simply change the file extension when constructing the `Document` object, and the conversion engine will handle the rest.

You might also combine **document conversion C#** with OCR for scanned PDFs:

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

## Conclusion

You now know **how to set bates numbering options** in C# from start to finish. By creating a `BatesNumberingOptions` object, applying it with `AddBatesNumbering`, and saving the result as PDF, you can automate the production of legally compliant, uniquely identified documents.  

From here you can explore related topics such as **C# PDF generation**, **document conversion C#**, or advanced **GroupDocs API** features like watermarking and digital signatures. Experiment with different prefixes, positions, and number formats to fit your workflow.

Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Add Bates Numbering PDF in C# – Complete Guide](/pdf/english/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add a Text Stamp Footer in PDFs Using Aspose.PDF for .NET&#58; A Step‑By‑Step Guide](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}