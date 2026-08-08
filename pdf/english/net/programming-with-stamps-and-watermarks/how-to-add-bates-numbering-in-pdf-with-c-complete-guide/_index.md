---
category: general
date: 2026-06-05
description: How to add bates numbering in PDF using C#. Learn to load a PDF document,
  update pagination, and add bates stamps quickly.
draft: false
keywords:
- how to add bates numbering
- add bates numbers pdf
- load pdf document c#
- add bates stamps to pdf
- update pagination pdf
language: en
og_description: How to add bates numbering in PDF using C#. This guide shows loading
  a PDF, updating pagination, and saving the stamped document.
og_title: How to Add Bates Numbering in PDF with C# – Step‑by‑Step
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: How to add bates numbering in PDF using C#. Learn to load a PDF document,
    update pagination, and add bates stamps quickly.
  headline: How to Add Bates Numbering in PDF with C# – Complete Guide
  type: TechArticle
- description: How to add bates numbering in PDF using C#. Learn to load a PDF document,
    update pagination, and add bates stamps quickly.
  name: How to Add Bates Numbering in PDF with C# – Complete Guide
  steps:
  - name: Load PDF Document in C#
    text: Before any numbering can happen, the PDF must be loaded into memory. Aspose.Pdf’s
      `Document` class does the heavy lifting, handling everything from encryption
      to page streams.
  - name: Add Bates Stamps to PDF
    text: The real hero of the library is `UpdatePagination()`. When you call it without
      parameters, Aspose automatically inserts Bates numbers on every page, using
      the default format `Page 1 of N`. If you need a custom prefix (e.g., “ABC‑2023‑”),
      you can supply a `PaginationInfo` object.
  - name: Save the Updated PDF
    text: After stamping, you simply persist the modified document. You can overwrite
      the original or write to a new file—both are safe as long as you respect file
      locks.
  - name: Full Working Example
    text: 'Putting the three pieces together yields a compact, production‑ready program:'
  type: HowTo
- questions:
  - answer: 'Pass the password to the `Document` constructor:'
    question: What if my PDF is password‑protected?
  - answer: 'Embed the font when you save: `pdf.FontEmbeddingMode = FontEmbeddingMode.Always;`.'
    question: Fonts missing on the target machine?
  - answer: The free evaluation works but adds a watermark. For production, acquire
      a license to remove it and unlock full pagination features.
    question: Do I need a license for Aspose.Pdf?
  type: FAQPage
tags:
- PDF
- C#
- Aspose.Pdf
title: How to Add Bates Numbering in PDF with C# – Complete Guide
url: /net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Add Bates Numbering in PDF with C# – Complete Guide

Ever wondered **how to add bates numbering** to a PDF without spending hours fiddling with manual tools? You’re not alone. In many legal, forensic, or compliance workflows, stamping a document with sequential Bates numbers is a non‑negotiable step, and doing it programmatically in C# can save you a ton of time.

In this tutorial we’ll walk through a clean, end‑to‑end solution that shows you exactly how to **load a PDF document in C#**, refresh the pagination, and **add bates stamps to PDF** files using the Aspose.Pdf library. By the end you’ll have a ready‑to‑run code sample, a handful of practical tips, and a clear idea of how to tweak the process for your own projects.

## What You’ll Learn

- How to reference and configure Aspose.Pdf for .NET.
- The three‑step pattern: load → update pagination → save.
- Why `UpdatePagination()` is the magic behind **add bates numbers pdf** automatically.
- Customization options for Bates number format, position, and style.
- Common pitfalls (e.g., missing fonts, large files) and how to avoid them.

> **Prerequisites** – You need .NET 6+ (or .NET Framework 4.6+), a licensed copy of Aspose.Pdf for .NET, and a basic understanding of C#. No other external tools are required.

![how to add bates numbering in PDF using C#](image.png "how to add bates numbering in PDF using C#")

## How to Add Bates Numbering – Step‑by‑Step

Below we break the process into three logical steps. Each step is wrapped in its own **H2** header so you can jump straight to the part you need.

### Load PDF Document in C#

Before any numbering can happen, the PDF must be loaded into memory. Aspose.Pdf’s `Document` class does the heavy lifting, handling everything from encryption to page streams.

```csharp
using System;
using Aspose.Pdf;          // Make sure the Aspose.Pdf namespace is referenced

class BatesNumberingDemo
{
    static void Main()
    {
        // 👉 Step 1: Load the source PDF
        // Replace YOUR_DIRECTORY with the actual folder path on your machine.
        var inputPath = @"YOUR_DIRECTORY\input.pdf";

        // The `using` block ensures the document is properly disposed.
        using (var pdf = new Document(inputPath))
        {
            // The rest of the workflow continues inside this block.
            // ...
        }
    }
}
```

**Why this matters:**  
- The `using` statement guarantees that file handles are released, preventing “file in use” errors later when you try to save.  
- Loading the file once keeps memory usage low, even for multi‑hundred‑page PDFs.

### Add Bates Stamps to PDF

The real hero of the library is `UpdatePagination()`. When you call it without parameters, Aspose automatically inserts Bates numbers on every page, using the default format `Page 1 of N`. If you need a custom prefix (e.g., “ABC‑2023‑”), you can supply a `PaginationInfo` object.

```csharp
using Aspose.Pdf.Text;

// Inside the using block from the previous step:
{
    // 👉 Step 2: Configure and apply Bates numbering
    var pagination = new PaginationInfo
    {
        // Example: "ABC-2023-" will be prepended to each page number.
        Prefix = "ABC-2023-",
        // Suffix can be left empty or used for things like "-END".
        Suffix = string.Empty,
        // Choose where the stamp appears. Bottom‑right is common.
        HorizontalAlignment = HorizontalAlignment.Right,
        VerticalAlignment = VerticalAlignment.Bottom,
        // Font settings ensure the numbers are legible.
        Font = new FontRepository().FindFont("Arial"),
        FontSize = 10,
        // Optional: Add a border or background if you need a stamp look.
        // Border = new BorderInfo(BorderSide.All, 0.5f, Color.Black)
    };

    // This call adds the stamps to every page.
    pdf.Pages.UpdatePagination(pagination);
}
```

**Why this works:**  
- `PaginationInfo` gives you fine‑grained control over **add bates stamps to pdf** without writing a loop yourself.  
- The library automatically handles page count, zero‑padding, and even right‑to‑left languages if needed.

### Save the Updated PDF

After stamping, you simply persist the modified document. You can overwrite the original or write to a new file—both are safe as long as you respect file locks.

```csharp
// 👉 Step 3: Save the output PDF
var outputPath = @"YOUR_DIRECTORY\output.pdf";
pdf.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

**Tip:** If you’re processing many files in a batch, consider using `pdf.Save(outputPath, SaveFormat.PdfA_1b)` to produce a PDF/A‑compliant archive, which is often required for legal evidence.

### Full Working Example

Putting the three pieces together yields a compact, production‑ready program:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class BatesNumberingDemo
{
    static void Main()
    {
        var inputPath = @"YOUR_DIRECTORY\input.pdf";
        var outputPath = @"YOUR_DIRECTORY\output.pdf";

        using (var pdf = new Document(inputPath))
        {
            var pagination = new PaginationInfo
            {
                Prefix = "ABC-2023-",
                HorizontalAlignment = HorizontalAlignment.Right,
                VerticalAlignment = VerticalAlignment.Bottom,
                Font = new FontRepository().FindFont("Arial"),
                FontSize = 10
            };

            // Add or refresh Bates numbers
            pdf.Pages.UpdatePagination(pagination);

            // Persist the changes
            pdf.Save(outputPath);
        }

        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**Expected output:**  
Open `output.pdf` in any viewer and you’ll see a sequence like `ABC-2023-001`, `ABC-2023-002`, … at the bottom‑right of each page. The numbers are automatically incremented, even if you later insert or delete pages and re‑run `UpdatePagination()`.

## Customizing Bates Number Appearance (Optional)

If the default settings don’t fit your workflow, you can tweak a few more properties:

| Property | What it controls | Example |
|----------|------------------|---------|
| `StartNumber` | First number in the series | `StartNumber = 1000` |
| `NumberStyle` | Numeric, Roman, or alphanumeric | `NumberStyle = NumberStyle.AlphaNumeric` |
| `Margin` | Distance from page edges (in points) | `Margin = new MarginInfo(10, 10, 10, 10)` |
| `Color` | Text color for the stamp | `Color = Color.Red` |

```csharp
pagination.StartNumber = 1000;
pagination.NumberStyle = NumberStyle.AlphaNumeric;
pagination.Margin = new MarginInfo(5, 5, 5, 5);
pagination.Color = Color.Red;
```

These tweaks are especially handy when you need to **add bates numbers pdf** for court filings that require a specific format.

## Common Questions & Edge Cases

- **What if my PDF is password‑protected?**  
  Pass the password to the `Document` constructor:  
  `new Document(inputPath, new LoadOptions { Password = "secret" })`.

- **Large PDFs (>500 MB) cause OutOfMemoryException.**  
  Enable streaming: `var pdf = new Document(inputPath) { EnableMemoryOptimization = true };`.

- **Fonts missing on the target machine?**  
  Embed the font when you save: `pdf.FontEmbeddingMode = FontEmbeddingMode.Always;`.

- **Do I need a license for Aspose.Pdf?**  
  The free evaluation works but adds a watermark. For production, acquire a license to remove it and unlock full pagination features.

## Recap

We’ve covered **how to add bates numbering** to a PDF using C# from start to finish. The core steps—**load pdf document c#**, call `UpdatePagination()` (the heart of **add bates stamps to pdf**), and **save**—are simple yet powerful. By customizing `PaginationInfo`, you can satisfy almost any legal or forensic requirement, and the built‑in safeguards keep your code robust for large or protected files.

## What’s Next?

- Dive deeper into **add bates numbers pdf** by generating separate index pages that list each stamp.  
- Combine this approach with OCR to embed searchable text alongside Bates numbers.  
- Explore other Aspose.Pdf features like watermarking, digital signatures, or PDF/A conversion.

Feel free to experiment, break things, and then fix them—that’s how you truly master PDF automation. If you hit a snag or have a clever use‑case, drop a comment below. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add Page Number Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET&#58; A Complete Guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}