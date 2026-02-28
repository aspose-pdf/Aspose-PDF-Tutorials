---
category: general
date: 2026-02-28
description: Create PDF document C# with Bates numbering. Learn how to add bates numbering
  pdf, set prefixes, and generate sequential PDF numbers in a single walkthrough.
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add document identification numbers
- add sequential pdf numbers
language: en
og_description: Create PDF document C# with Bates numbering. This tutorial shows how
  to add bates numbering pdf, set custom prefixes, and produce sequential PDF numbers.
og_title: Create PDF Document C# – Add Bates Numbering
tags:
- Aspose.PDF
- C#
- PDF automation
title: Create PDF Document C# – Add Bates Numbering Guide
url: /net/document-creation/create-pdf-document-c-add-bates-numbering-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create PDF Document C# – Add Bates Numbering Guide

Ever wondered how to **create PDF document C#** that already carries a unique identifier on every page? That’s a common pain point when you need to track legal files, court filings, or any batch of PDFs that must be searchable by a number. The good news? With Aspose.PDF you can add Bates numbers in just a few lines of code—no manual editing required.

In this guide we’ll walk through the entire process: loading an existing PDF, configuring **add bates numbering pdf**, applying the numbers, and finally saving the result. By the end you’ll be able to **add document identification numbers** and even **add sequential PDF numbers** automatically, all from C#.

## Prerequisites

- .NET 6.0 or later (the API works with .NET Framework 4.5+ as well)
- A licensed copy of **Aspose.PDF for .NET** (the free trial works for testing)
- An input PDF file you want to number (we’ll call it `input.pdf`)
- Visual Studio 2022 (or any IDE you prefer)

No extra NuGet packages beyond Aspose.PDF are needed.

![Create PDF Document C# with Bates numbering](https://example.com/image.png "Create PDF Document C# example")

## Step 1: Load the Source PDF Document

Before you can **add bates numbering pdf**, you need a `Document` object that represents the file on disk.

```csharp
using Aspose.Pdf;

// Load the source PDF document
var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*Why this matters*: The `Document` class is the entry point for every operation in Aspose.PDF. It abstracts the file system, so you can work with pages, annotations, and metadata without touching the raw bytes.

> **Pro tip:** If you’re processing many files in a loop, reuse the same `Document` instance only when the source is identical; otherwise, instantiate a fresh object for each file to avoid memory leaks.

## Step 2: Define Bates Numbering Options

Here’s where the **how to add bates** part becomes concrete. You configure a `BatesNumberingOptions` object to tell Aspose what the prefix should be, where to start, and how big the font must appear.

```csharp
// Define Bates numbering options (prefix, start number, font size)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",   // You can change this to any string you need
    Start = 1000,      // Starting number – useful for continuous numbering across batches
    FontSize = 9       // Small enough to fit in the margin but still readable
};
```

*Why this matters*: The `Prefix` lets you embed a case identifier (e.g., “ABC-”). The `Start` property is essential when you’re **adding sequential PDF numbers** across multiple documents—just keep incrementing it. And `FontSize` ensures the numbers don’t obstruct existing content.

## Step 3: Apply Bates Numbering to the Entire Document

Now we actually stamp the numbers onto each page. The `BatesNumbering` class does all the heavy lifting.

```csharp
// Apply Bates numbering to the entire document
var bates = new BatesNumbering();
bates.AddBatesNumbering(pdfDocument, batesOptions);
```

*Why this matters*: Under the hood, Aspose walks through every page, calculates the appropriate number (Prefix + (Start + pageIndex)), and draws it in the bottom‑right corner by default. You can customize the position later, but the default works for most legal‑style documents.

> **Common question:** *What if I only need to number a subset of pages?*  
> Use the overload `AddBatesNumbering(Document, BatesNumberingOptions, int startPage, int endPage)` to limit the range.

## Step 4: Save the PDF with Bates Numbers Applied

The final step is to write the modified document back to disk.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*Why this matters*: The `Save` method respects the original file format, so you end up with a standard PDF that any viewer can open—complete with **add document identification numbers** on each page.

## Full Working Example

Putting it all together, here’s a self‑contained program you can paste into a new console app and run immediately.

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

**Expected result:** Open `output.pdf` in any viewer; you’ll see “ABC‑1000”, “ABC‑1001”, … printed on each page’s lower‑right corner. The numbers are selectable text, so they’re searchable and can be copied—exactly what you’d expect from a proper **add sequential PDF numbers** implementation.

## Edge Cases & Variations

### Custom Positioning

If the default corner collides with existing footers, you can shift the placement:

```csharp
batesOptions.Position = new Position(10, 10); // X, Y from the bottom‑left
```

### Different Number Formats

Want zero‑padded numbers (e.g., 001000)? Use `NumberFormat`:

```csharp
batesOptions.NumberFormat = "D6"; // Pads to 6 digits
```

### Multiple Files in a Batch

When processing many PDFs, maintain a running counter:

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

### Handling Password‑Protected PDFs

If the source PDF is encrypted, pass the password when creating the `Document`:

```csharp
var pdfDocument = new Document("protected.pdf", new LoadOptions { Password = "mySecret" });
```

## Frequently Asked Questions

| Question | Answer |
|----------|--------|
| **Can I use a different library?** | Yes, libraries like iTextSharp or PdfSharp also support page‑level text insertion, but Aspose.PDF offers the most straightforward API for Bates numbering. |
| **Does this affect file size?** | Adding a few bytes of text per page is negligible; the output size typically grows by less than 1 KB per page. |
| **Is the numbering searchable?** | Absolutely. Aspose writes the numbers as text objects, not as images, so they’re indexed by PDF readers. |
| **What if I need a different font?** | Set `batesOptions.Font` to a `Font` object (e.g., `FontRepository.FindFont("Arial")`). |

## Conclusion

We’ve just demonstrated how to **create PDF document C#** and instantly **add bates numbering pdf** using Aspose.PDF. The process is simple, reliable, and fully programmable—perfect for legal firms, government agencies, or any organization that must **add document identification numbers** and **add sequential PDF numbers** to large batches of files.

Take this foundation and experiment: try different prefixes for different departments, chain the numbering across multiple files, or embed QR codes alongside the Bates numbers for extra traceability. The sky’s the limit once you have the core workflow nailed down.

If you found this tutorial useful, give it a share, leave a comment, or explore our other guides on PDF manipulation with C#. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}