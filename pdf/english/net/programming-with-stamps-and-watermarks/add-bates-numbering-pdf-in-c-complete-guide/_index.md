---
category: general
date: 2026-05-27
description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
  numbering quickly, customize format, and automate legal document tagging.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbering
language: en
og_description: Add Bates numbering PDF with Aspose.Pdf in C#. This guide shows how
  to add Bates numbering, configure prefixes, and save the result.
og_title: Add Bates Numbering PDF in C# – Step‑by‑Step Tutorial
schemas:
- author: Aspose
  dateModified: '2026-05-27'
  description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  headline: Add Bates Numbering PDF in C# – Complete Guide
  type: TechArticle
- description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  name: Add Bates Numbering PDF in C# – Complete Guide
  steps:
  - name: Expected Output
    text: 'When you run the program, the console prints:'
  - name: Can I position the Bates number elsewhere?
    text: Yes. Use the `BatesNumberingArtifact`’s `Location` property (e.g., `Location
      = new Position(10, 10)`) to place the number at custom X/Y coordinates. You
      can also set `HorizontalAlignment` and `VerticalAlignment` for more control.
  - name: What if my PDF has thousands of pages?
    text: Aspose.Pdf streams pages efficiently, but it’s still a good idea to process
      in batches if you hit memory limits. The `Document` class also supports `PdfConverter`
      for incremental saving.
  - name: How do I change the font or color?
    text: 'Wrap the artifact in a `TextState` object:'
  - name: Do I need a license for production use?
    text: A licensed version removes evaluation watermarks and unlocks full performance.
      The free trial works fine for testing and proof‑of‑concepts.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- Bates numbering
- PDF automation
title: Add Bates Numbering PDF in C# – Complete Guide
url: /net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Bates Numbering PDF in C# – Complete Guide

Ever wondered **how to add Bates numbering** to a PDF without spending hours fiddling with manual tools? You're not alone—legal teams, auditors, and e‑discovery specialists all need a reliable way to **add Bates numbering PDF** files programmatically.  

In this tutorial we’ll walk through a concise, end‑to‑end solution using Aspose.Pdf for .NET, so you can drop Bates numbers onto any document with just a few lines of C# code.

## What You’ll Learn

- How to open an existing PDF with Aspose.Pdf  
- How to create a Bates numbering artifact and fine‑tune its format  
- How to attach the artifact to every page (or just the first)  
- How to save the updated file and verify the result  

No prior experience with Aspose is required—just a basic understanding of C# and .NET. By the end, you’ll have a reusable snippet you can copy‑paste into any project.

## Prerequisites

- .NET 6.0 or later (the code also works on .NET Framework 4.7+)
- Aspose.Pdf for .NET NuGet package (`Install-Package Aspose.Pdf`)
- A source PDF file you want to tag (place it in a folder you can reference)

> **Pro tip:** If you don’t have a license yet, Aspose offers a free temporary key that removes evaluation watermarks.

## Step 1 – Open the Source PDF Document  

First we need a `Document` object that represents the file on disk. Think of this as loading a blank canvas that we’ll later paint Bates numbers onto.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Adjust the path to point at your source PDF
        string sourcePath = @"C:\Docs\source.pdf";

        // Load the PDF – this is where we start to add Bates numbering
        using (var pdfDocument = new Document(sourcePath))
        {
            // The rest of the logic lives inside this using block
        }
    }
}
```

**Why this matters:** Opening the document inside a `using` block ensures all unmanaged resources are released promptly, which is especially important for large PDFs.

## Step 2 – Create a Bates Numbering Artifact  

A *BatesNumberingArtifact* is Aspose’s way of describing how the numbers should look. You can set a prefix, starting number, increment, and even a custom format string.

```csharp
// Step 2: Define the Bates numbering artifact
var batesNumbering = new BatesNumberingArtifact
{
    Prefix = "ABC",            // Text that appears before each number
    StartNumber = 1000,        // First number in the sequence
    Increment = 1,             // Step between consecutive numbers
    Format = "{0:D5}"          // Zero‑padded 5‑digit number (e.g., 01000)
};
```

**Why you might change these values:**  
- **Prefix** is useful for case IDs (“CASE‑”, “DOC‑”).  
- **StartNumber** lets you continue a previous series.  
- **Increment** can be set to 2 if you need odd/even numbering.  
- **Format** supports any .NET composite format; `{0:D5}` guarantees five digits with leading zeros.

## Step 3 – Attach the Artifact to the Desired Pages  

You can add the artifact to a single page, a range, or the whole document. For most legal workflows we attach it to *every* page, but the example below shows the minimal case—adding it to the first page.

```csharp
// Step 3: Attach the artifact to the first page (index is 1‑based)
pdfDocument.Pages[1].Artifacts.Add(batesNumbering);
```

If you need to cover all pages, loop through them:

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesNumbering);
}
```

**Why this step is crucial:** Artifacts are rendered *after* the page content, so the numbers appear on top of existing text without altering the original layout.

## Step 4 – Save the Modified PDF  

Finally, write the changes back to disk. You can overwrite the original or create a new file—here we’ll generate a fresh copy called `bates.pdf`.

```csharp
// Step 4: Persist the changes
string outputPath = @"C:\Docs\bates.pdf";
pdfDocument.Save(outputPath);

Console.WriteLine($"Bates numbering added successfully. File saved to: {outputPath}");
```

When you open `bates.pdf` you’ll see “ABC01000” (or whatever format you chose) stamped in the default location—usually the bottom‑right corner.

## Full Working Example  

Putting it all together, here’s the complete program you can compile and run:

```csharp
using Aspose.Pdf;
using System;

class AddBatesNumbering
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Open the source PDF
        // -----------------------------------------------------------------
        string sourcePath = @"C:\Docs\source.pdf";
        using (var pdfDocument = new Document(sourcePath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Create and configure the Bates numbering artifact
            // -----------------------------------------------------------------
            var batesNumbering = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                StartNumber = 1000,
                Increment = 1,
                Format = "{0:D5}"
            };

            // -----------------------------------------------------------------
            // 3️⃣ Attach the artifact to each page (or a specific page)
            // -----------------------------------------------------------------
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesNumbering);
            }

            // -----------------------------------------------------------------
            // 4️⃣ Save the new PDF
            // -----------------------------------------------------------------
            string outputPath = @"C:\Docs\bates.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbers added. Output: {outputPath}");
        }
    }
}
```

### Expected Output

When you run the program, the console prints:

```
Bates numbers added. Output: C:\Docs\bates.pdf
```

Opening `bates.pdf` shows the prefix “ABC” followed by a zero‑padded five‑digit sequence on every page—exactly what you asked the code to do.

## Common Questions & Edge Cases

### Can I position the Bates number elsewhere?

Yes. Use the `BatesNumberingArtifact`’s `Location` property (e.g., `Location = new Position(10, 10)`) to place the number at custom X/Y coordinates. You can also set `HorizontalAlignment` and `VerticalAlignment` for more control.

### What if my PDF has thousands of pages?

Aspose.Pdf streams pages efficiently, but it’s still a good idea to process in batches if you hit memory limits. The `Document` class also supports `PdfConverter` for incremental saving.

### How do I change the font or color?

Wrap the artifact in a `TextState` object:

```csharp
batesNumbering.TextState = new TextState
{
    FontSize = 12,
    Font = FontRepository.FindFont("Arial"),
    ForegroundColor = Color.FromRgb(255, 0, 0) // red
};
```

### Do I need a license for production use?

A licensed version removes evaluation watermarks and unlocks full performance. The free trial works fine for testing and proof‑of‑concepts.

## Verification – Quick Visual Check  

If you prefer an automated verification, Aspose can extract the text of a page and confirm the presence of the prefix:

```csharp
string pageText = pdfDocument.Pages[1].ExtractText();
bool hasBates = pageText.Contains("ABC01000");
Console.WriteLine(hasBates ? "Bates number verified." : "Number missing!");
```

Running this after the save step will print `Bates number verified.` if everything went smoothly.

## Conclusion  

You now know **how to add Bates numbering PDF** files using Aspose.Pdf in C#. From opening the document to configuring the artifact, attaching it to pages, and saving the result, the process is straightforward and fully scriptable.  

Next steps? Try experimenting with:

- Different `Prefix` values for multiple case batches  
- Custom `Location` and `TextState` for branding  
- Adding page‑specific prefixes (e.g., “VOL‑1‑”, “VOL‑2‑”) by adjusting `StartNumber` per loop iteration  

These tweaks let you tailor the solution to almost any legal or archival workflow.  

Got more questions about **how to add Bates numbering** for multi‑language PDFs or encrypted files? Drop a comment below, and happy coding!


## Related Tutorials

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add Different Headers in PDF Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-different-headers-aspose-pdf-net/)
- [How to Add a Text Stamp Footer in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}