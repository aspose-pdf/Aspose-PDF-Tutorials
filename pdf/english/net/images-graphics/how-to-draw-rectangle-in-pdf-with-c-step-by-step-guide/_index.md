---
category: general
date: 2026-03-27
description: Learn how to draw rectangle in PDF using Aspose.Pdf for C#. Add rectangle
  to PDF, add shape to PDF and draw shape on PDF with clear code examples.
draft: false
keywords:
- how to draw rectangle
- add rectangle to pdf
- add shape to pdf
- draw shape on pdf
- draw rectangle in pdf
language: en
og_description: Master how to draw rectangle in PDF using Aspose.Pdf. This tutorial
  shows you how to add rectangle to PDF, add shape to PDF, and draw shape on PDF step
  by step.
og_title: How to Draw Rectangle in PDF with C# – Complete Guide
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: How to Draw Rectangle in PDF with C# – Step‑by‑Step Guide
url: /net/images-graphics/how-to-draw-rectangle-in-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Draw Rectangle in PDF with C# – Step‑by‑Step Guide

Ever wondered **how to draw rectangle** in a PDF without wrestling with low‑level PDF syntax? You're not the only one. Many developers hit a wall when they need to visualise a bounding box, a highlight area, or a simple decorative element inside a generated document. The good news? With Aspose.Pdf for .NET the process is a piece of cake.

In this tutorial we’ll walk through everything you need to **add rectangle to PDF**, **add shape to PDF**, and ultimately **draw rectangle in PDF** using clean, idiomatic C#. By the end you’ll have a runnable program that produces a PDF file containing a crisp rectangle—no external tools required.

## Prerequisites

- .NET 6.0 or later (the code works with .NET Core and .NET Framework as well)
- Aspose.Pdf for .NET NuGet package (`Install-Package Aspose.Pdf`)
- A basic C# development environment (Visual Studio, VS Code, Rider, etc.)

No other libraries are needed; everything else is handled by Aspose.Pdf itself.

## Step 1: Set Up the Project and Import Namespaces

First, create a new console application and pull in the Aspose.Pdf namespace.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the rest of the code here.
        }
    }
}
```

**Why this matters:** Importing `Aspose.Pdf.Drawing` gives you access to the `Rectangle` shape class we’ll use to **draw shape on PDF**. Keeping the entry point tidy makes the later steps easier to follow.

## Step 2: Create a New PDF Document and a Page

A PDF without pages is meaningless, so we start by creating a document object and adding a single page.

```csharp
// Step 2: Initialize a new PDF document
Document pdfDoc = new Document();

// Add a blank page to the document (size defaults to A4)
Page page = pdfDoc.Pages.Add();
```

**Explanation:** The `Document` class represents the whole file, while `Pages.Add()` returns a fresh `Page` object where we’ll later **add rectangle to PDF**. The default A4 size works for most cases, but you can pass width/height if you need a custom canvas.

## Step 3: Define the Rectangle Shape

Now comes the core of **how to draw rectangle**—defining its position and dimensions.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
// Coordinates are measured from the lower‑left corner of the page.
var rectangleShape = new Rectangle(100, 500, 300, 200)
{
    // Optional: set line color and fill color
    BorderColor = Color.Black,
    BorderWidth = 2,
    FillColor = Color.LightGray
};
```

**Why we set these properties:**  
- `BorderColor` and `BorderWidth` control the outline, making the rectangle visible.  
- `FillColor` gives it a subtle background, useful when you want to highlight a region.  
- The constructor `(x, y, width, height)` lets you **draw rectangle in PDF** precisely where you need it.

## Step 4: Add the Rectangle to the Page

With the shape ready, we now **add shape to PDF** by attaching it to the page’s `Annotations` collection. Aspose.Pdf validates the bounds automatically, so you don’t have to worry about overflow.

```csharp
// Step 4: Add the rectangle shape to the page
page.Annotations.Add(rectangleShape);
```

**What happens under the hood:** The `Annotations` collection treats the rectangle as a vector graphic. When the PDF is rendered, the library translates our coordinates into the PDF content stream.

## Step 5: Save the Document

Finally, write the PDF to disk so you can open it in any viewer.

```csharp
// Step 5: Save the PDF file
string outputPath = "RectangleDemo.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

**Result:** Opening `RectangleDemo.pdf` shows a light‑gray rectangle with a black border positioned 100 pts from the left and 500 pts from the bottom of the page. That’s the complete solution for **how to draw rectangle** in a PDF using C#.

## Full Working Example

Putting all the pieces together, here’s the complete, ready‑to‑run program:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize a new PDF document
            Document pdfDoc = new Document();

            // Add a blank page (A4 by default)
            Page page = pdfDoc.Pages.Add();

            // Define a rectangle shape (x, y, width, height)
            var rectangleShape = new Rectangle(100, 500, 300, 200)
            {
                BorderColor = Color.Black,
                BorderWidth = 2,
                FillColor = Color.LightGray
            };

            // Add the rectangle to the page
            page.Annotations.Add(rectangleShape);

            // Save the document
            string outputPath = "RectangleDemo.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved to {outputPath}");
        }
    }
}
```

**Expected output:** A file named `RectangleDemo.pdf` containing a single page with a centered light‑gray rectangle outlined in black. You can open it with Adobe Reader, Chrome, or any PDF viewer.

## Common Variations & Edge Cases

### 1. Drawing Multiple Rectangles

If you need to **add rectangle to PDF** more than once, simply create additional `Rectangle` objects and add each to `page.Annotations`. Looping over a collection of coordinates makes this trivial.

```csharp
foreach (var rectInfo in rectangles)
{
    var rect = new Rectangle(rectInfo.X, rectInfo.Y, rectInfo.Width, rectInfo.Height)
    {
        BorderColor = Color.Blue,
        BorderWidth = 1,
        FillColor = Color.Transparent
    };
    page.Annotations.Add(rect);
}
```

### 2. Using Different Units

Aspose.Pdf works in points (1 pt = 1/72 inch). If you prefer millimeters, convert them first:

```csharp
double mmToPt = 72.0 / 25.4;
float x = (float)(20 * mmToPt); // 20 mm from left
float y = (float)(150 * mmToPt);
```

### 3. Adding a Rectangle as a Form Field

When you need an interactive rectangle (e.g., a clickable area), use a `LinkAnnotation` instead of a plain `Rectangle`. The code is similar but adds a URL or JavaScript action.

### 4. Compatibility Concerns

Aspose.Pdf version 23.9 (released early 2026) fully supports the APIs shown above. Older versions may require `page.AddAnnotation(rectangleShape)` instead of `page.Annotations.Add`. Always check the release notes if you encounter compile errors.

## Pro Tips & Pitfalls

- **Pro tip:** Set `FillColor = Color.Transparent` if you only need an outline. This reduces file size slightly.
- **Watch out for:** Using coordinates that exceed the page dimensions. Aspose.Pdf will silently clip the shape, which can be confusing when debugging.
- **Performance note:** Adding thousands of rectangles is fine, but if you’re generating large reports consider batching shapes into a single `Graphics` object to reduce overhead.

## Visual Reference

Below is a quick screenshot of the generated PDF (the rectangle is highlighted in light gray). The alt text includes the primary keyword for SEO.

![how to draw rectangle in PDF example](https://example.com/images/rectangle-demo.png "how to draw rectangle in PDF example")

## Conclusion

We’ve covered **how to draw rectangle** in a PDF using Aspose.Pdf for C#. By creating a `Document`, adding a `Page`, defining a `Rectangle` shape, and finally **adding shape to PDF**, you can generate vector‑based graphics with just a handful of lines. Whether you need to **add rectangle to pdf** for highlighting, layout debugging, or UI overlays, the approach scales nicely.

Next, you might explore **draw shape on pdf** beyond rectangles—think circles, polylines, or even custom SVG paths. Or dive into text rendering, image insertion, and PDF form manipulation to build full‑featured reports. The Aspose.Pdf library offers a rich API, and with the fundamentals covered here you’re ready to experiment.

Happy coding, and may your PDFs always look exactly how you envision!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}