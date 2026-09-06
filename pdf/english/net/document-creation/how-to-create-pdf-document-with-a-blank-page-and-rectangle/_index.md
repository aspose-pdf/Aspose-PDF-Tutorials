---
category: general
date: 2026-09-05
description: Create PDF document in C# by adding a blank page, drawing a rectangle,
  and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add blank page pdf
- draw rectangle pdf
- save pdf file
- how to add rectangle
language: en
lastmod: 2026-09-05
og_description: Create PDF document in C# by adding a blank page, drawing a rectangle,
  and saving the PDF file. Follow this complete example with Aspose.PDF.
og_image_alt: Screenshot showing a PDF document with a drawn rectangle on a blank
  page
og_title: Create PDF document with blank page and rectangle – C# guide
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  headline: How to create PDF document with a blank page and rectangle
  type: TechArticle
- description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  name: How to create PDF document with a blank page and rectangle
  steps:
  - name: 'Edge case: custom page size'
    text: 'If your layout requires a 6 × 9 inch page, replace the default call with:'
  - name: 'Pro tip: styling the rectangle'
    text: 'You can change the stroke color and line width:'
  - name: 'Edge case: overwriting existing files'
    text: 'Aspose.PDF overwrites an existing file by default. To protect previous
      outputs, check for file existence first:'
  - name: Expected output
    text: Running the program creates a single‑page PDF. When you open `output.pdf`
      you will see a blank white page with a red rectangle positioned 100 points from
      the left and bottom edges, measuring 200 × 200 points.
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
- PDF generation
title: How to create PDF document with a blank page and rectangle
url: /net/document-creation/how-to-create-pdf-document-with-a-blank-page-and-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create PDF document with a blank page and rectangle

If you need to **create PDF document** programmatically, this guide shows a complete solution in C#. You will learn how to add a blank page, draw a rectangle on that page, and finally save the PDF file. The example uses the Aspose.PDF library, which works with .NET 6+ and .NET Framework 4.5+.

Adding a blank page and drawing shapes is a common requirement for invoices, certificates, or custom reports. By the end of this tutorial you will have a runnable project that produces a PDF containing a single rectangle positioned at (100, 100) with a size of 200 × 200 points.

## Prerequisites

Before you start, make sure you have:

* Visual Studio 2022 (or any C# IDE)
* .NET 6 SDK or .NET Framework 4.5+
* Aspose.PDF for .NET NuGet package  
  ```bash
  dotnet add package Aspose.PDF
  ```
* Write permission to the output directory

No additional configuration is required; the code runs out‑of‑the‑box.

## Create PDF document – overview

The whole process consists of four logical steps:

1. **Instantiate** a `Document` object – this represents the PDF file.
2. **Add a blank page** – the page provides a canvas for drawing.
3. **Draw a rectangle** – a `Path` object defines the shape.
4. **Save the PDF file** – persists the document to disk.

Each step is isolated in its own section so you can reuse or replace parts as needed.

![Diagram of a PDF with a rectangle on a blank page](https://example.com/placeholder-image.png){.img-fluid alt="Screenshot showing a PDF document with a drawn rectangle on a blank page"}

## Add blank page pdf

A PDF must contain at least one page before any graphics can be placed. The `Pages.Add()` method creates an empty page with default dimensions (A4). If you need a different size, pass a `PageSize` argument.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();

// Step 2: Add a blank page to the document
Page pdfPage = pdfDocument.Pages.Add();   // adds an A4 page by default
```

*Why this step matters* – The page object holds collections for text, images, and vector graphics. Without a page, any attempt to add a rectangle would raise an exception.

### Edge case: custom page size

If your layout requires a 6 × 9 inch page, replace the default call with:

```csharp
var pageSize = new Size(432, 648); // 72 points per inch
Page pdfPage = pdfDocument.Pages.Add(pageSize);
```

## Draw rectangle pdf

Drawing a rectangle is a matter of creating a `Rectangle` geometry and wrapping it in a `Path`. The `ValidateBounds()` call ensures the shape fits inside the page margins, preventing clipping.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

// Step 4: Add the rectangle to the page contents
Path rectanglePath = new Path(shapeRect).ValidateBounds();
pdfPage.Contents.Add(rectanglePath);
```

*Why this step matters* – The `Path` object is the low‑level vector primitive used by Aspose.PDF. By validating bounds you avoid runtime errors when the rectangle exceeds page limits.

### Pro tip: styling the rectangle

You can change the stroke color and line width:

```csharp
rectanglePath.GraphInfo = new GraphInfo
{
    StrokeColor = Color.Red,
    LineWidth = 2
};
```

This produces a red outline with a 2‑point thickness.

## Save pdf file

Persisting the document finalizes the file on disk. The `Save` method accepts a file path or a stream. Providing an absolute path makes the location explicit, which is useful for automation scripts.

```csharp
// Step 5: Save the PDF to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

*Why this step matters* – Saving is the only point where the in‑memory representation becomes a physical file. If you need to return the PDF from a web API, replace the file path with a `MemoryStream`.

### Edge case: overwriting existing files

Aspose.PDF overwrites an existing file by default. To protect previous outputs, check for file existence first:

```csharp
if (File.Exists(outputPath))
{
    File.Delete(outputPath);
}
pdfDocument.Save(outputPath);
```

## How to add rectangle – best practices

* **Keep coordinates within the page margins** – use `ValidateBounds()` or calculate margins manually.
* **Reuse `GraphInfo` objects** when drawing multiple shapes; this reduces memory allocation.
* **Dispose of the `Document` object** (as shown with `using var`) to free native resources promptly.
* **Test with different DPI settings** if you later embed raster images; vector shapes like rectangles remain crisp at any resolution.

## Complete working example

Below is the full program you can copy into a console application. It compiles without modification and produces `output.pdf` in the project folder.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using var pdfDocument = new Document();

        // Add a blank page to the document
        Page pdfPage = pdfDocument.Pages.Add();

        // Define a rectangle shape (x, y, width, height)
        Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

        // Create a path for the rectangle and validate its bounds
        Path rectanglePath = new Path(shapeRect).ValidateBounds();

        // Optional: style the rectangle (red outline, 2‑pt width)
        rectanglePath.GraphInfo = new GraphInfo
        {
            StrokeColor = Color.Red,
            LineWidth = 2
        };

        // Add the rectangle to the page contents
        pdfPage.Contents.Add(rectanglePath);

        // Determine output path
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");

        // Ensure no leftover file blocks the save operation
        if (File.Exists(outputPath))
        {
            File.Delete(outputPath);
        }

        // Save the PDF to a file
        pdfDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

### Expected output

Running the program creates a single‑page PDF. When you open `output.pdf` you will see a blank white page with a red rectangle positioned 100 points from the left and bottom edges, measuring 200 × 200 points.

## Conclusion

You now know how to **create PDF document**, **add blank page pdf**, **draw rectangle pdf**, and **save pdf file** using Aspose.PDF in C#. The example covers the essential API calls, explains why each call is required, and provides tips for common variations such as custom page sizes or rectangle styling. 

Next, explore related topics like **adding text**, **embedding images**, or **creating multi‑page reports**. The same pattern—instantiate a `Document`, manipulate pages, add vector or raster content, then `Save`—applies to all of those scenarios. Feel free to experiment with different shapes, colors, and page layouts to fit your project's needs.


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create PDF Document C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)
- [Create PDF Document with Aspose.PDF – Step‑by‑Step Guide](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Create PDF Document with Aspose – Add Page, Text Box, and Form](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}