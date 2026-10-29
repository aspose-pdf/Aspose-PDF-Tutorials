---
category: general
date: 2026-08-04
description: Create new PDF document in C# and add Bates numbering pdf quickly using
  Aspose.Pdf – learn to add blank page pdf and custom page numbers.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new pdf document
- add bates numbering pdf
- how to add bates
- add blank page pdf
- add custom page numbers
language: en
lastmod: 2026-08-04
og_description: Create new PDF document in C# and automatically add Bates numbering
  pdf for legal case management – full code example included.
og_image_alt: Screenshot of a C# program creating a PDF document with Bates numbers
  applied
og_title: Create new PDF document with Bates numbering in C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create new PDF document in C# and add Bates numbering pdf quickly using
    Aspose.Pdf – learn to add blank page pdf and custom page numbers.
  headline: Create new PDF document with Bates numbering in C#
  type: TechArticle
tags:
- C#
- PDF
- Aspose.Pdf
- Bates numbering
title: Create new PDF document with Bates numbering in C#
url: /net/document-creation/create-new-pdf-document-with-bates-numbering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create new PDF document with Bates numbering in C#

If you need to **create new PDF document** in C#, this guide shows you how to **add Bates numbering pdf** using Aspose.Pdf. You’ll learn to **add blank page pdf**, configure **add custom page numbers**, and save the final file.

The tutorial covers every step from installing the library to generating a PDF that complies with legal case‑file standards. By the end you can generate a PDF, insert a blank page, apply Bates numbers, and customize the numbering format—all with a single, runnable program.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 SDK or later installed  
* Visual Studio 2022 (or any C# IDE)  
* An active Aspose.Pdf for .NET license or a free evaluation key  

You do not need any additional NuGet packages; the tutorial installs everything automatically.

## Step 1: Install Aspose.Pdf via NuGet

Open a terminal in your project folder and run:

```bash
dotnet add package Aspose.Pdf
```

The command adds the latest stable version of Aspose.Pdf to your project, which provides the `Document`, `BatesNumbering`, and other PDF‑manipulation classes you’ll use.

## Step 2: Create new PDF document – initial setup

Creating the PDF file is the foundation for every later operation. The `Document` class represents the entire PDF container.

```csharp
using Aspose.Pdf;

// Step 2: Create a new PDF document
using var doc = new Document();
```

*Why this matters*: Instantiating `Document` allocates the internal structures required for pages, fonts, and graphics. Using `using var` ensures the file is properly disposed after saving.

## Step 3: Add blank page pdf

A PDF must contain at least one page before you can place content on it. Adding a blank page gives you a clean canvas for Bates numbers.

```csharp
// Step 3: Add a blank page to the document
Page page = doc.Pages.Add();
```

The `Pages.Add()` method appends a new, empty page at the end of the document’s page collection. You can repeat this call to add more pages if you later need to **add custom page numbers** across multiple pages.

## Step 4: Configure Bates numbering – how to add bates

Bates numbering is a sequential identifier commonly used in legal documents. You configure it through the `BatesNumbering` class.

```csharp
// Step 4: Set up Bates numbering options
var bates = new BatesNumbering
{
    StartNumber = 1000,      // Starting number for the sequence
    Prefix = "CaseA-",       // Text to prepend to each number
    Increment = 1,           // Increment between consecutive numbers
    // Optional: Set the location, font size, etc.
};
```

*Why this matters*: `StartNumber` defines the first number, `Prefix` adds a readable label, and `Increment` controls the step size. You can also adjust `HorizontalAlignment`, `VerticalAlignment`, `FontSize`, and `Margins` to control the appearance of the number on each page.

## Step 5: Apply the Bates numbering pdf to the page

Now that the numbering options are ready, apply them to the page (or to the whole document).

```csharp
// Step 5: Apply the Bates numbering to the page
bates.Apply(page);
```

Calling `Apply` inserts the formatted number into the page’s footer by default. If you need the number elsewhere, set `bates.Position` before calling `Apply`.

## Step 6: Save the PDF with Bates numbers applied

Finally, write the in‑memory document to disk.

```csharp
// Step 6: Save the PDF with Bates numbers applied
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumbered.pdf");

doc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

The saved file now contains a single page with the Bates number **CaseA-1000** displayed at the bottom. Open the PDF in any viewer to verify the numbering.

## Expected output

When you open `BatesNumbered.pdf`, you should see:

* One blank page (or more if you added additional pages)  
* The text **CaseA-1000** positioned at the bottom of the page (default location)  

If you add more pages and reuse the same `BatesNumbering` instance, the numbers will increment automatically (CaseA-1001, CaseA-1002, …).

## Pro tip: Adding custom page numbers in addition to Bates numbers

Sometimes you need both Bates numbers and traditional page numbers. You can combine them by adding a `TextFragment` after applying Bates numbering:

```csharp
// Add a traditional page number in the header
var pageNumber = new TextFragment($"Page {page.Number}")
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Top,
    FontSize = 12,
    Font = FontRepository.FindFont("Arial")
};
page.Paragraphs.Add(pageNumber);
```

This snippet demonstrates **add custom page numbers** while preserving the Bates label.

## Edge case: Applying Bates numbering to multiple pages

If your document contains several pages, you can apply the same `BatesNumbering` instance to each page in a loop:

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    bates.Apply(doc.Pages[i]);
}
```

The loop ensures every page receives a sequential number based on the `StartNumber` and `Increment` you defined.

## Common pitfalls and how to avoid them

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| Numbers appear off‑center | Default alignment may not match your layout | Set `bates.HorizontalAlignment` and `bates.VerticalAlignment` explicitly |
| Numbers overlap existing content | No margin is defined | Adjust `bates.Margin` or use `bates.Position` to move the number |
| License exception at runtime | Evaluation version limits output | Apply a valid Aspose.Pdf license before creating the document (`License license = new License(); license.SetLicense("Aspose.Pdf.lic");`) |

## Full working example

Below is a self‑contained program you can copy, paste, and run.

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1. Create a new PDF document
        using var doc = new Document();

        // 2. Add a blank page pdf
        Page page = doc.Pages.Add();

        // 3. Configure Bates numbering – how to add bates
        var bates = new BatesNumbering
        {
            StartNumber = 1000,
            Prefix = "CaseA-",
            Increment = 1,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(20, 20, 20, 20),
            FontSize =


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF .NET&#58; Add Page Numbers to PDFs Using FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}