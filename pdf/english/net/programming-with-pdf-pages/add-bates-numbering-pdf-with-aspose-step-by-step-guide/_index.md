---
category: general
date: 2026-08-08
description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also shows
  how to add blank page pdf and generate pdf programmatically.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering pdf
- add blank page pdf
- generate pdf programmatically
- create pdf aspose
language: en
lastmod: 2026-08-08
og_description: Add bates numbering pdf with Aspose.Pdf in C#. Learn to add blank
  page pdf, generate pdf programmatically, and save the final document in minutes.
og_image_alt: Screenshot of C# code adding Bates numbering and a blank page to a PDF
  using Aspose.Pdf
og_title: Add bates numbering pdf with Aspose – complete C# guide
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  headline: Add bates numbering pdf with Aspose – step‑by‑step guide
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  name: Add bates numbering pdf with Aspose – step‑by‑step guide
  steps:
  - name: What if I need a different font or position?
    text: 'The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`,
      `HorizontalAlignment`, and `VerticalAlignment`. For example:'
  - name: How do I exclude a specific page from numbering?
    text: Create a separate `BatesNumberingArtifact` for the pages you want to number
      and add it only to those pages. Pages without an attached artifact will remain
      unnumbered.
  - name: Does this work with existing PDFs?
    text: 'Yes. Instead of `new Document()`, load an existing file:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF generation
- Bates numbering
title: Add bates numbering pdf with Aspose – step‑by‑step guide
url: /net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add bates numbering pdf with Aspose – step‑by‑step guide

Add bates numbering pdf with Aspose.Pdf is straightforward once you understand the core steps. If you also need to add blank page pdf or generate pdf programmatically, this guide covers everything you need.

In this tutorial you will:

* Create a new PDF document from scratch.  
* Add a blank page pdf that will host the Bates numbers.  
* Configure the Bates numbering artifact with a custom prefix.  
* Save the PDF so the numbers appear on the generated file.  

By the end you will have a fully functional C# console application that produces a PDF containing Bates numbers like **CASE‑1000**, **CASE‑1001**, … – a common requirement for legal and e‑discovery workflows.

## Prerequisites

* .NET 6.0 SDK or later (the code also works with .NET Framework 4.8).  
* Visual Studio 2022 or any C#‑compatible IDE.  
* A valid Aspose.Pdf for .NET license (or a free evaluation key).  
* Basic familiarity with C# syntax.

> **Pro tip:** If you run the code without a license, Aspose will add a small watermark to the output PDF.

## Step 1: Set up the project and import Aspose.Pdf

Create a new console project and add the Aspose.Pdf NuGet package:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

The `using` directives required for the example are:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
```

These namespaces give you access to the `Document`, `Page`, and `BatesNumberingArtifact` classes used later.

## Step 2: Add a blank page pdf

A Bates number must be attached to a page, so we first create a blank page that will receive the numbering artifact.

```csharp
// Step 2: Add a blank page pdf
Document pdfDocument = new Document();          // creates an empty PDF
Page pdfPage = pdfDocument.Pages.Add();         // adds the first (blank) page
```

The `Document` class represents the whole PDF file, while `Pages.Add()` inserts a new, empty page at the end of the document’s page collection. Because the document starts empty, this call also creates the first page.

## Step 3: Configure the Bates numbering artifact

Now we define how the Bates numbers should look. The `BatesNumberingArtifact` lets you set the start number, prefix, suffix, and formatting options.

```csharp
// Step 3: Define Bates numbering settings
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
{
    StartNumber = 1000,          // first number in the sequence
    Prefix = "CASE-",            // custom prefix before each number
    // Optional: you can also set Suffix, FontSize, FontColor, etc.
};
```

**Why this matters:**  
Setting `StartNumber` to **1000** matches typical legal case file conventions. The `Prefix` ensures each number appears as **CASE‑1000**, **CASE‑1001**, … which is easier to search and sort.

## Step 4: Attach the artifact to the page

The artifact must be added to the page’s `Artifacts` collection so that Aspose renders it on every page during saving.

```csharp
// Step 4: Attach the Bates numbering artifact to the PDF page
pdfPage.Artifacts.Add(batesArtifact);
```

When the document is saved, Aspose automatically repeats the artifact on all pages, incrementing the number for each subsequent page.

## Step 5: (Optional) Add additional pages

If you need more pages, simply repeat `pdfDocument.Pages.Add()`. The Bates numbering artifact you attached in the previous step will automatically appear on each new page.

```csharp
// Example: add two more pages
pdfDocument.Pages.Add();
pdfDocument.Pages.Add();
```

## Step 6: Save the PDF – generate pdf programmatically

Finally, persist the document to disk. This is the point where the Bates numbers are rendered onto the pages.

```csharp
// Step 6: Save the PDF – generate pdf programmatically
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumberedDocument.pdf");

// Ensure the directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);

pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to: {outputPath}");
```

**Expected result:**  
Open *BatesNumberedDocument.pdf* and you will see a three‑page PDF. Each page displays a Bates number in the bottom‑right corner:

* Page 1 → **CASE‑1000**  
* Page 2 → **CASE‑1001**  
* Page 3 → **CASE‑1002**

The numbers are automatically incremented because the artifact is attached to the page collection.

## Full, runnable example

Putting everything together, here is a complete console program you can copy, paste, and run:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new PDF document
            Document pdfDocument = new Document();

            // Add a blank page pdf
            Page pdfPage = pdfDocument.Pages.Add();

            // Define Bates numbering settings (add bates numbering pdf)
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
            {
                StartNumber = 1000,
                Prefix = "CASE-"
            };

            // Attach the artifact to the page
            pdfPage.Artifacts.Add(batesArtifact);

            // (Optional) add more pages to see incremented numbers
            pdfDocument.Pages.Add(); // page 2
            pdfDocument.Pages.Add(); // page 3

            // Save the PDF – generate pdf programmatically
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "BatesNumberedDocument.pdf");

            Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);
            pdfDocument.Save(outputPath);

            Console.WriteLine($"PDF saved to: {outputPath}");
        }
    }
}
```

Run the program with `dotnet run`. After execution, locate the file on your desktop and verify the Bates numbers.

![Add bates numbering pdf example](/images/bates-numbering.png "Add bates numbering pdf example")

## Common questions and edge cases

### What if I need a different font or position?

The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`, `HorizontalAlignment`, and `VerticalAlignment`. For example:

```csharp
batesArtifact.FontSize = 12;
batesArtifact.FontColor = Color.Blue;
batesArtifact.HorizontalAlignment = HorizontalAlignment.Left;
batesArtifact.VerticalAlignment = VerticalAlignment.Top;
```

### How do I exclude a specific page from numbering?

Create a separate `BatesNumberingArtifact` for the pages you want to number and add it only to those pages. Pages without an attached artifact will remain unnumbered.

### Does this work with existing PDFs?

Yes. Instead of `new Document()`, load an existing file:

```csharp
Document pdfDocument = new Document("input.pdf");
```

Then attach the artifact to the desired pages and save.

## Conclusion

You now know how to **add bates numbering pdf** using Aspose.Pdf, how to **add blank page pdf**, and how to **generate pdf programmatically** in a clean, reusable C# solution. The approach works with any number of pages, custom prefixes, and styling options, giving you full control over the final document.

Next steps you might explore:

* Use **create pdf as


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add an Empty Page at the End of a PDF Using Aspose.PDF for .NET | Step-by-Step Guide](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)
- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}