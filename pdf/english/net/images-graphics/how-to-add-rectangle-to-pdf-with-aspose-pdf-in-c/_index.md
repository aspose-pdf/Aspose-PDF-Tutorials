---
category: general
date: 2026-10-10
description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
  PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to PDF
- draw shape on PDF
- save modified PDF
- add shape to PDF
- access specific PDF page
language: en
lastmod: 2026-10-10
og_description: Add rectangle to PDF using Aspose.PDF in C#. This tutorial shows how
  to draw shape on PDF, access a specific PDF page, and save modified PDF.
og_image_alt: Screenshot of a PDF page with a blue rectangle overlay created by Aspose.PDF
og_title: Add rectangle to PDF with Aspose.PDF – complete C# guide
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  headline: How to add rectangle to PDF with Aspose.PDF in C#
  type: TechArticle
- description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  name: How to add rectangle to PDF with Aspose.PDF in C#
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: What if the PDF has only one page?
    text: Attempting to access `pdfDocument.Pages[1]` throws an `ArgumentOutOfRangeException`.
      Guard against this by checking `pdfDocument.Pages.Count` before indexing.
  - name: How to add multiple rectangles on different pages?
    text: Repeat Steps 2‑4 for each target page, adjusting the rectangle’s coordinates
      as needed. You can place the logic inside a loop that iterates over `pdfDocument.Pages`.
  - name: Can I use other shapes such as circles or polygons?
    text: Yes. Aspose.PDF provides `Ellipse`, `Polygon`, and `Polyline` classes that
      follow the same pattern as `Rectangle`. Replace the `new Aspose.Pdf.Drawing.Rectangle`
      call with the desired shape class.
  - name: Does the library support PDFs with rotated pages?
    text: Aspose.PDF automatically respects page rotation when rendering shapes. The
      rectangle’s coordinates are interpreted in the page’s native coordinate system,
      so no extra transformation is required.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: How to add rectangle to PDF with Aspose.PDF in C#
url: /net/images-graphics/how-to-add-rectangle-to-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to add rectangle to PDF with Aspose.PDF in C#

If you need to **add rectangle to PDF** files programmatically, this guide shows you exactly how. You’ll learn to **draw shape on PDF**, target a particular page, and **save modified PDF** without errors.

Working with PDF documents is a common requirement for reporting, invoicing, or document annotation. By the end of this tutorial you can confidently **add shape to PDF** files, handle out‑of‑bounds errors, and integrate the solution into any .NET project.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 SDK or later installed  
* Visual Studio 2022 (or any C# IDE)  
* An Aspose.PDF for .NET license or a free evaluation key – the API works the same way in both modes  
* A PDF file named `input.pdf` placed in a folder you can reference from your code  

These items are the only external dependencies for the example.

## Step 1: Install the Aspose.PDF NuGet package

The Aspose.PDF library provides the `Document`, `Rectangle`, and other drawing classes you need.

```bash
dotnet add package Aspose.PDF
```

Running this command adds the latest stable version of Aspose.PDF to your project, making the PDF classes available for compilation.

## Step 2: Load the PDF document

The first operation is to load the source file. This creates an in‑memory representation that you can modify.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;

class PdfRectangleExample
{
    static void Main()
    {
        // Load the PDF document from disk
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

*Why this matters*: Loading the document gives you access to its pages collection, which is required to **access specific PDF page** later.

## Step 3: Access the second page (zero‑based index)

PDF pages are indexed from `0`. To place a rectangle on the second page, retrieve the page at index `1`.

```csharp
        // Access the second page (pages are zero‑based)
        var page = pdfDocument.Pages[1];
```

If the document has fewer than two pages, an `ArgumentOutOfRangeException` will be thrown, alerting you to the need for a guard clause in production code.

## Step 4: Create the rectangle shape

Define the rectangle’s position and size using the `Rectangle` structure, then wrap it in an Aspose drawing object.

```csharp
        // Define rectangle bounds: (x, y, width, height)
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            // Optional visual styling
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };
```

*Why this matters*: The `BorderInfo` and `FillColor` properties let you **draw shape on PDF** with a visible outline and optional fill, making the rectangle stand out for readers.

## Step 5: Add the rectangle to the page’s paragraph collection

Aspose.PDF treats drawing objects as paragraph elements. Adding the rectangle to the page’s `Paragraphs` collection renders it on the page.

```csharp
        // Add the rectangle shape to the page
        page.Paragraphs.Add(rectangleShape);
```

At this point the PDF document in memory contains the new shape, but the file on disk is unchanged until you save it.

## Step 6: Save the modified PDF and handle out‑of‑bounds errors

Calling `Save` writes the updated document to a new file. If the rectangle exceeds the page dimensions, Aspose throws a `PdfException`. Catching this exception lets you report the problem cleanly.

```csharp
        try
        {
            // Save the altered PDF to a new file
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            // Handle shape that does not fit on the page
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

*Why this matters*: The `try/catch` block ensures your application **save modified PDF** safely, and the error message helps you adjust the rectangle’s coordinates if needed.

## Full working example

Putting all steps together, here’s the complete, ready‑to‑run program:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;
using System.Drawing; // Required for Color

class PdfRectangleExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // Step 2: Access the second page (zero‑based)
        var page = pdfDocument.Pages[1];

        // Step 3: Create a rectangle shape positioned at (100,100) with width 300 and height 200
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };

        // Step 4: Add the rectangle shape to the page's paragraph collection
        page.Paragraphs.Add(rectangleShape);

        // Step 5: Save the modified PDF, handling out‑of‑bounds cases
        try
        {
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

### Expected output

Running the program prints:

```
PDF saved successfully with rectangle added.
```

and creates `output.pdf` that shows the original content plus a blue rectangle at the specified coordinates on the second page.

If the rectangle were larger than the page, you would see:

```
Shape out of bounds: The shape exceeds page margins.
```

## Common questions and edge cases

### What if the PDF has only one page?

Attempting to access `pdfDocument.Pages[1]` throws an `ArgumentOutOfRangeException`. Guard against this by checking `pdfDocument.Pages.Count` before indexing.

```csharp
if (pdfDocument.Pages.Count < 2)
{
    Console.WriteLine("Document does not contain a second page.");
    return;
}
```

### How to add multiple rectangles on different pages?

Repeat Steps 2‑4 for each target page, adjusting the rectangle’s coordinates as needed. You can place the logic inside a loop that iterates over `pdfDocument.Pages`.

### Can I use other shapes such as circles or polygons?

Yes. Aspose.PDF provides `Ellipse`, `Polygon`, and `Polyline` classes that follow the same pattern as `Rectangle`. Replace the `new Aspose.Pdf.Drawing.Rectangle` call with the desired shape class.

### Does the library support PDFs with rotated pages?

Aspose.PDF automatically respects page rotation when rendering shapes. The rectangle’s coordinates are interpreted in the page’s native coordinate system, so no extra transformation is required.

## Performance considerations

* **Memory usage** – Loading a large PDF (hundreds of megabytes) consumes proportional memory. If you only need to modify a single page, consider using `PdfFileInfo` to extract that page, modify it, and then merge it back.
* **Batch processing** – When adding shapes to many documents, reuse a single `License` instance to avoid repeated license validation overhead.

## Next steps

Now that you can **add rectangle to PDF**, explore these related topics:

* **draw shape on PDF** – learn to overlay text, images, and watermarks  
* **add shape to PDF** – combine multiple shapes into a single annotation layer  
* **save modified PDF** – use streams (`MemoryStream`) to return PDFs directly from web APIs  
* **access specific PDF page** – implement page‑range extraction for custom reports  

Experiment with different colors, line styles, and transparency levels to match your branding guidelines.

---

*Happy coding! If this tutorial helped you **add rectangle to PDF**, consider sharing it with teammates or contributing improvements back to the community.*


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide](/pdf/english/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [How to Add a Line Object in PDF Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}