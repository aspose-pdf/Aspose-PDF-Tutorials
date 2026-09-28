---
category: general
date: 2026-09-27
description: Add bates numbering to PDF using Aspose.PDF in C#. Learn how to load
  a PDF document, set Bates numbering options, and save the updated file.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- load pdf document
- how to add bates numbering
- Aspose.PDF C#
- PDF Bates numbering example
language: en
lastmod: 2026-09-27
og_description: Add bates numbering to PDF using Aspose.PDF in C#. This tutorial shows
  you how to load a PDF document, configure Bates numbering, and save the result.
og_image_alt: Screenshot of a PDF page displaying Bates numbers in the footer
og_title: Add bates numbering to PDF with Aspose.PDF – C# guide
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
title: Add bates numbering to PDF using Aspose.PDF in C#
url: /net/programming-with-text/add-bates-numbering-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add bates numbering to PDF using Aspose.PDF in C#

If you need to **add bates numbering** to a PDF file, this guide shows you a complete, ready‑to‑run solution. You’ll see how to **load a PDF document**, configure the Bates numbering options, and write the numbered file back to disk—all with Aspose.PDF for .NET.

Applying Bates numbers is common in legal, law‑enforcement, and archival workflows. By the end of this tutorial you can embed a sequential identifier on every page, customize the prefix, and start the count at any number you choose.

## What you’ll learn

* How to **load PDF document** content into an `Aspose.Pdf.Document` object.  
* The exact steps **how to add bates numbering** with `BatesNumberingOptions`.  
* How to save the modified file while preserving original layout and quality.  

No external tools are required—just the Aspose.PDF NuGet package and a .NET development environment (Visual Studio, VS Code, or Rider).  

---

## Step 1: Install Aspose.PDF for .NET

Open your project folder in a terminal and run:

```bash
dotnet add package Aspose.PDF
```

The package includes the `Aspose.Pdf` namespace, which provides all classes used in this tutorial. After installation, reload the project so the IDE picks up the new reference.

## Step 2: Load PDF document

Loading the source file is the first operation because the Bates numbering engine works on an existing `Document` instance.

```csharp
using Aspose.Pdf;

// ...

// Replace with the path to your input PDF
string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Load the PDF document into memory
Document doc = new Document(inputPath);
```

**Why this matters:** The `Document` class parses the PDF structure, giving you access to pages, annotations, and metadata. Without loading the file first, you cannot apply any numbering.

## Step 3: Configure Bates numbering options

Create a `BatesNumberingOptions` object and set the desired prefix, start number, and optional formatting parameters.

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

**Why this matters:** `BatesNumberingOptions` tells Aspose.PDF how to generate the label for each page. The `Prefix` helps you group related cases, while `StartNumber` lets you continue a sequence from a previous batch.

## Step 4: Save the PDF with Bates numbers applied

Pass the options object to the `Save` method. Aspose.PDF writes the numbers directly onto each page.

```csharp
// Replace with the desired output path
string outputPath = @"YOUR_DIRECTORY\output.pdf";

// Save the document, applying the Bates numbering
doc.Save(outputPath, batesOptions);
```

**Why this matters:** The overload `Save(string, BatesNumberingOptions)` combines the rendering step with the numbering process, ensuring that the output file contains the visible identifiers.

## Full example – everything together

Below is a single, self‑contained program you can copy, paste, and run. It demonstrates **how to add bates numbering** from start to finish.

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

### Expected output

Running the program produces `output.pdf` where each page displays a label similar to:

```
CASE01-1
CASE01-2
CASE01-3
...
```

The numbers appear in the footer by default, but you can move them by adjusting the `Margin` property in `BatesNumberingOptions`.

## Edge cases and common variations

| Situation | What to adjust |
|-----------|----------------|
| **Different prefix per batch** | Change `Prefix` before calling `Save`. You can loop over multiple documents with distinct prefixes. |
| **Continue numbering from a previous file** | Set `StartNumber` to the last used number + 1. |
| **Place numbers in the header** | Use `batesOptions.Margin = new Margin(20, 0, 0, 0);` (top margin) or customize `batesOptions.Position`. |
| **Custom font or color** | Assign `Font`, `FontSize`, and `Color` properties as shown in the commented section. |
| **Large PDFs (1000+ pages)** | The operation is memory‑efficient; however, you may want to enable `doc.OptimizeResources()` before saving to reduce file size. |

**Pro tip:** If your workflow requires different numbering schemes per document, encapsulate the logic in a helper method:

```csharp
static void ApplyBatesNumbering(string src, string dst, string prefix, int start)
{
    var doc = new Document(src);
    var opts = new BatesNumberingOptions { Prefix = prefix, StartNumber = start };
    doc.Save(dst, opts);
}
```

## Conclusion

You now know **how to add bates numbering** to any PDF using Aspose.PDF in C#. The tutorial covered loading the PDF document, configuring the numbering options, and saving the final file—all in a single, executable program.  

From here you can explore related topics such as **adding watermarks**, **merging multiple PDFs**, or **extracting text** with Aspose.PDF. Experiment with different fonts, colors, and positions to match your organization’s formatting standards.

Ready to automate your legal document workflow? Add the code to your build pipeline, run it against batches of files, and let Aspose.PDF handle the heavy lifting. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create PDF Document C# – Add Bates Numbering](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/)
- [Add Bates Numbering PDF – Step‑by‑Step Guide to Number PDF Pages](/pdf/english/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/)
- [Aspose PDF Tutorial – Insert a Blank Page and Update Bates Numbering](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}