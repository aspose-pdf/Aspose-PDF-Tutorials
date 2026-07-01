---
category: general
date: 2026-06-30
description: Add Bates numbering to PDF using Aspose.PDF in C#. Learn how to number
  PDF pages, set a custom prefix, and create a reliable Bates numbering document.
draft: false
keywords:
- add bates numbering
- how to add bates
- number pdf pages
- how to number pdf
- bates numbering document
language: en
og_description: Add Bates numbering to PDF with Aspose.PDF. This guide shows how to
  number PDF pages and create a Bates numbering document in C#.
og_title: Add Bates Numbering to PDF – Aspose.PDF Guide
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add Bates numbering to PDF using Aspose.PDF in C#. Learn how to number
    PDF pages, set a custom prefix, and create a reliable Bates numbering document.
  headline: Add Bates Numbering to PDF with Aspose.PDF – Complete Guide
  type: TechArticle
- description: Add Bates numbering to PDF using Aspose.PDF in C#. Learn how to number
    PDF pages, set a custom prefix, and create a reliable Bates numbering document.
  name: Add Bates Numbering to PDF with Aspose.PDF – Complete Guide
  steps:
  - name: Customizing Appearance (Optional)
    text: 'If you need a different font, size, or placement, you can tweak the `BatesNumbering`
      properties:'
  - name: Expected Output
    text: Open `bates_numbered.pdf` in any PDF viewer. You’ll see a label like **CASE‑1000**
      on the first page, **CASE‑1001** on the second, and so on. The numbers appear
      in the bottom‑left corner by default (or wherever you set `XIndent`/`YIndent`).
  - name: 1. What if the PDF is huge (hundreds of MB)?
    text: 'Aspose.PDF streams pages to disk by default, so memory consumption stays
      low. However, you can explicitly enable **compression**:'
  - name: 2. Need a different numbering format (e.g., suffix instead of prefix)?
    text: 'Set the `Suffix` property:'
  - name: 3. How to restart numbering for a new section?
    text: Call `bates.StartNumber = 1;` before processing the next batch, or create
      a second `BatesNumbering` instance.
  - name: 4. The PDF already contains watermarks—will the numbers overlap?
    text: 'Adjust `XIndent` and `YIndent` to move the numbers away from existing elements.
      You can also change the `Position` enum (`BatesNumberingPosition.TopRight`,
      etc.):'
  - name: 5. Does this work with encrypted PDFs?
    text: 'If the source PDF is password‑protected, open it like this:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF processing
- Bates numbering
title: Add Bates Numbering to PDF with Aspose.PDF – Complete Guide
url: /net/programming-with-pdf-pages/add-bates-numbering-to-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Bates Numbering to PDF with Aspose.PDF – Complete Guide

Ever needed to **add bates numbering** to a PDF but weren’t sure where to start? You’re not the only one—legal teams, auditors, and even developers often ask *how to add bates* for tracking large document sets. In this tutorial we’ll walk through a complete, ready‑to‑run solution that numbers PDF pages, applies a custom prefix, and saves a fresh **bates numbering document**. No fluff, just the code you can copy‑paste today.

We’ll cover everything from setting up Aspose.PDF, choosing a start number, handling edge cases like huge files, and even tweaking the format if you need something beyond the default. By the end you’ll be able to **number pdf pages** automatically, and you’ll understand why this approach is both robust and easy to maintain.

## Prerequisites

Before we dive in, make sure you have:

- .NET 6.0 or later (the example uses .NET 6 but works with .NET Core 3.1+)
- An Aspose.PDF for .NET license (the free evaluation works for testing)
- A PDF file you want to process (named `source.pdf` in the example)
- Visual Studio 2022 or any C# editor you prefer

That’s it—no extra NuGet packages beyond Aspose.PDF.

## Step 1: Install Aspose.PDF for .NET

Open your terminal or Package Manager Console and run:

```bash
dotnet add package Aspose.PDF
```

or, inside Visual Studio:

```
Tools → NuGet Package Manager → Manage NuGet Packages for Solution…
Search “Aspose.PDF” and click Install.
```

> **Pro tip:** If you plan to process thousands of pages, enable **Aspose.PDF’s memory‑saving mode** by setting `PdfConversion.SaveOptions.UseObjectPooling = true;` later on.

## Step 2: Create a Simple Console App Skeleton

Let’s scaffold a minimal console app so you can run the code instantly:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in the next steps.
        }
    }
}
```

Save the file as `Program.cs`. This skeleton gives us a clean place to drop the **bates numbering** logic.

## Step 3: Open the Source PDF Document

The first real operation is opening the PDF you want to stamp. We’ll use a `using` block so the file handle is released automatically:

```csharp
// Step 3: Open the source PDF document
using (var doc = new Document("YOUR_DIRECTORY/source.pdf"))
{
    // Subsequent steps go here.
}
```

> **Why a `using` block?** It guarantees the underlying file stream is closed, preventing file‑locking issues when you later try to overwrite the same file.

## Step 4: Set Up the BatesNumbering Facade

Aspose.PDF provides a convenient façade called `BatesNumbering`. It hides the low‑level page‑by‑page handling and lets you focus on the numbering itself.

```csharp
// Step 4: Create a Bates numbering facade
var bates = new BatesNumbering
{
    // Step 4a: Choose the starting number
    StartNumber = 1000,

    // Step 4b: Add an optional prefix (e.g., CASE-)
    Prefix = "CASE-"
    
    // You can also set a suffix, font size, or position if needed.
};
```

### Customizing Appearance (Optional)

If you need a different font, size, or placement, you can tweak the `BatesNumbering` properties:

```csharp
bates.FontSize = 10;               // Smaller than the default 12
bates.TextColor = Color.Black;    // Ensure high contrast
bates.XIndent = 20;               // Move number 20 points from the left edge
bates.YIndent = 30;               // Move number 30 points from the bottom edge
```

These settings are handy when the default placement interferes with existing content.

## Step 5: Apply the Bates Numbering to the Document

Now we actually stamp the numbers onto each page:

```csharp
// Step 5: Apply the Bates numbering to the document
bates.AddBatesNumbering(doc);
```

Behind the scenes Aspose.PDF iterates over every page, inserts the formatted string (e.g., `CASE-1000`, `CASE-1001`, …), and respects any layout options you set earlier.

## Step 6: Save the Newly Numbered PDF

Finally, write the result to disk. You can overwrite the original file or create a fresh one—here we’ll keep both for safety:

```csharp
// Step 6: Save the newly numbered PDF
doc.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering applied successfully!");
```

Running the program should produce a file named `bates_numbered.pdf` with each page clearly labeled.

### Expected Output

Open `bates_numbered.pdf` in any PDF viewer. You’ll see a label like **CASE‑1000** on the first page, **CASE‑1001** on the second, and so on. The numbers appear in the bottom‑left corner by default (or wherever you set `XIndent`/`YIndent`).

## Full Working Example

Putting all the pieces together, here’s the complete code you can copy‑paste:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to match your environment
            const string sourcePath = "YOUR_DIRECTORY/source.pdf";
            const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";

            // Open the source PDF
            using (var doc = new Document(sourcePath))
            {
                // Configure Bates numbering
                var bates = new BatesNumbering
                {
                    StartNumber = 1000,
                    Prefix = "CASE-",
                    // Optional customizations:
                    // FontSize = 10,
                    // TextColor = Color.Black,
                    // XIndent = 20,
                    // YIndent = 30
                };

                // Apply numbering
                bates.AddBatesNumbering(doc);

                // Save the result
                doc.Save(outputPath);
                Console.WriteLine($"Bates numbering added. Saved to: {outputPath}");
            }
        }
    }
}
```

Run `dotnet run` from the project folder, and you’ll see the console message confirming success.

## Edge Cases & Common Questions

### 1. What if the PDF is huge (hundreds of MB)?

Aspose.PDF streams pages to disk by default, so memory consumption stays low. However, you can explicitly enable **compression**:

```csharp
doc.Compress();
```

### 2. Need a different numbering format (e.g., suffix instead of prefix)?

Set the `Suffix` property:

```csharp
bates.Suffix = "-2026";
```

You can combine both:

```csharp
bates.Prefix = "CASE-";
bates.Suffix = "-2026";
```

Result: `CASE-1000-2026`.

### 3. How to restart numbering for a new section?

Call `bates.StartNumber = 1;` before processing the next batch, or create a second `BatesNumbering` instance.

### 4. The PDF already contains watermarks—will the numbers overlap?

Adjust `XIndent` and `YIndent` to move the numbers away from existing elements. You can also change the `Position` enum (`BatesNumberingPosition.TopRight`, etc.):

```csharp
bates.Position = BatesNumberingPosition.TopRight;
```

### 5. Does this work with encrypted PDFs?

If the source PDF is password‑protected, open it like this:

```csharp
var doc = new Document(sourcePath, new LoadOptions { Password = "yourPassword" });
```

The rest of the workflow remains unchanged.

## Tips for Production‑Ready Implementations

- **License early**: Insert `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` at the start of `Main` to avoid the evaluation watermark.
- **Parallel processing**: For batch operations on many files, wrap the per‑file logic in a `Parallel.ForEach` loop—just be mindful of I/O limits.
- **Logging**: Use `Ser


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Add Page Number Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add a Text Stamp to PDF Using Aspose.PDF .NET: Comprehensive Guide](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}