---
category: general
date: 2026-08-14
description: draw rectangle on pdf quickly using C#. Learn how to define rectangle
  dimensions and add shapes to a PDF page in just a few lines.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- draw rectangle on pdf
- how to define rectangle dimensions
language: en
lastmod: 2026-08-14
og_description: draw rectangle on pdf with C# in seconds. This guide shows how to
  define rectangle dimensions, add a shape, and verify page boundaries for reliable
  PDF graphics.
og_image_alt: Screenshot of a PDF page showing a black rectangle drawn with C# code
og_title: draw rectangle on pdf – complete C# tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: draw rectangle on pdf quickly using C#. Learn how to define rectangle
    dimensions and add shapes to a PDF page in just a few lines.
  headline: draw rectangle on pdf – step‑by‑step C# guide
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
- RectangleShape
- Graphics
title: draw rectangle on pdf – step‑by‑step C# guide
url: /net/annotations/draw-rectangle-on-pdf-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# draw rectangle on pdf – complete C# tutorial

If you need to **draw rectangle on pdf** using C#, this guide shows you a concise, production‑ready solution. You’ll see exactly **how to define rectangle dimensions**, verify that the shape fits, and add it to a page with a single method call.

The tutorial covers everything from creating a PDF document to rendering the rectangle, so you can copy‑paste the code into your own project and see results instantly. No external documentation is required—just the steps below.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 or later (the code also works with .NET Framework 4.7+)
* The **Aspose.PDF for .NET** NuGet package (`Install-Package Aspose.PDF`)
* A basic understanding of C# syntax
* An IDE such as Visual Studio or VS Code

> **Pro tip:** Use the free evaluation license of Aspose.PDF for quick experiments; it adds a small watermark but lets you test all features.

## How to draw rectangle on PDF with C#

The core of the task is creating a `RectangleShape`, setting its size and stroke, and attaching it to a `Page`. The following H2 header contains the primary keyword, satisfying SEO requirements.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        Document pdfDoc = new Document();

        // 2️⃣ Add a blank page (default size: A4)
        Page page = pdfDoc.Pages.Add();

        // 3️⃣ Define the rectangle bounds (x, y, width, height)
        //    This demonstrates how to define rectangle dimensions.
        Rectangle rectBounds = new Rectangle(0, 0, 500, 700);

        // 4️⃣ Create the rectangle shape and set its stroke color
        RectangleShape rectangleShape = new RectangleShape(rectBounds)
        {
            StrokeColor = Color.Black   // black outline
        };

        // 5️⃣ Verify that the shape fits within the page boundaries
        page.CheckShapeBoundary(rectangleShape);

        // 6️⃣ Add the shape to the page
        page.Add(rectangleShape);

        // 7️⃣ Save the PDF to disk
        string outPath = "RectangleDemo.pdf";
        pdfDoc.Save(outPath);
        Console.WriteLine($"PDF saved to {outPath}");
    }
}
```

### Explanation of each step

| Step | Why it matters |
|------|----------------|
| **1️⃣ Create a new PDF document** | Initializes the container that will hold pages and graphics. |
| **2️⃣ Add a blank page** | You need a `Page` object because shapes are attached to a page, not directly to the document. |
| **3️⃣ Define the rectangle bounds** | This is where you **how to define rectangle dimensions**. The `Rectangle` constructor takes `x`, `y`, `width`, and `height` in points (1 pt = 1/72 in). |
| **4️⃣ Create the rectangle shape** | `RectangleShape` is the Aspose class that renders a rectangle. Setting `StrokeColor` defines the outline; you could also set `FillColor` for a solid fill. |
| **5️⃣ Verify page boundaries** | `CheckShapeBoundary` throws an exception if the rectangle exceeds the page size, preventing malformed PDFs. |
| **6️⃣ Add the shape to the page** | The shape becomes part of the page’s content stream. |
| **7️⃣ Save the PDF** | Persists the document to a file you can open with any PDF viewer. |

The resulting `RectangleDemo.pdf` contains a black rectangle positioned at the top‑left corner of the page, exactly 500 pt wide and 700 pt tall.

![draw rectangle on pdf example](https://example.com/rectangle-demo.png "draw rectangle on pdf example")

*Image alt text: draw rectangle on pdf example showing a black rectangle in the upper left corner of a PDF page.*

## How to define rectangle dimensions for different page sizes

The snippet above uses fixed values (`500 x 700`). In real applications you often need the rectangle to adapt to the page’s width and height.

```csharp
// Get page dimensions (in points)
float pageWidth = page.PageInfo.Width;
float pageHeight = page.PageInfo.Height;

// Define a rectangle that occupies 80% of the page width and 50% of the height
float rectWidth  = pageWidth * 0.8f;
float rectHeight = pageHeight * 0.5f;

// Center the rectangle on the page
float rectX = (pageWidth - rectWidth) / 2;
float rectY = (pageHeight - rectHeight) / 2;

Rectangle dynamicRect = new Rectangle(rectX, rectY, rectWidth, rectHeight);
RectangleShape dynamicShape = new RectangleShape(dynamicRect)
{
    StrokeColor = Color.DarkBlue,
    FillColor   = Color.LightGray   // optional fill
};

page.CheckShapeBoundary(dynamicShape);
page.Add(dynamicShape);
```

**Key points:**

* Use `page.PageInfo.Width` and `Height` to read the actual page size.
* Multiplying by a factor (e.g., `0.8f`) lets you express dimensions as a percentage of the page.
* Centering is achieved by subtracting the rectangle size from the page size and halving the remainder.

## Common pitfalls and how to avoid them

| Pitfall | Why it happens | Fix |
|---------|----------------|-----|
| Rectangle extends beyond the page | Hard‑coded dimensions larger than the page size. | Call `page.CheckShapeBoundary` **before** adding the shape; adjust dimensions if an exception is thrown. |
| Stroke not visible | `StrokeColor` left at default (`Color.Empty`). | Explicitly set `StrokeColor` (e.g., `Color.Black`). |
| Rectangle appears off‑screen | Coordinates start at the bottom‑left in PDF space; using screen‑style top‑left coordinates causes a flip. | Remember that the origin `(0,0)` is the lower‑left corner. Adjust `y` accordingly or use `pageHeight - desiredY`. |
| Unexpected line thickness | The default line width may be too thin for printing. | Set `rectangleShape.LineWidth = 2;` to increase thickness. |

## Extending the example

Once you can **draw rectangle on pdf**, you can easily add other shapes:

* **EllipseShape** – for circles or ovals.
* **PolygonShape** – for custom polygons.
* **TextFragment** – to label your rectangles.

All shapes share the same workflow: define bounds, configure appearance, verify boundaries, then add to the page.

## Complete, runnable program

Below is the full program that combines the basic rectangle and the dynamic sizing example. Copy it into a new console project, restore the `Aspose.PDF` NuGet package, and run.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class RectangleDemo
{
    static void Main()
    {
        // Create document and page
        Document doc = new Document();
        Page page = doc.Pages.Add();

        // ==== Fixed‑size rectangle (basic example) ====
        Rectangle fixedRect = new Rectangle(0, 0, 500, 700);
        RectangleShape fixedShape = new RectangleShape(fixedRect)
        {
            StrokeColor = Color.Black,
            LineWidth   = 1
        };
        page.CheckShapeBoundary(fixedShape);
        page.Add(fixedShape);

        // ==== Dynamic rectangle that adapts to page size ====
        float pageW = page.PageInfo.Width;
        float pageH = page.PageInfo.Height;

        float dynWidth  = pageW * 0.6f;
        float dynHeight = pageH * 0.3f;
        float dynX      = (pageW - dynWidth) / 2;
        float dynY      = (pageH - dynHeight) / 2;

        Rectangle dynamicRect = new Rectangle(dynX, dynY, dynWidth, dynHeight);
        RectangleShape dynamicShape = new RectangleShape(dynamicRect)
        {
            StrokeColor = Color.DarkBlue,
            FillColor   = Color.LightYellow,
            LineWidth   = 2
        };
        page.CheckShapeBoundary(dynamicShape);
        page.Add(dynamicShape);

        // Save PDF
        string outFile = "CombinedRectangles.pdf";
        doc.Save(outFile);
        Console.WriteLine($"PDF created: {outFile}");
    }
}
```

**Expected output:**  
Open `CombinedRectangles.pdf`. You’ll see a black rectangle anchored at the lower‑left corner and a centered dark‑blue rectangle with a light‑yellow fill. Both rectangles respect the page margins.

## Conclusion

You now know how to **draw rectangle on pdf** with C# and precisely **how to define rectangle dimensions** for both fixed and responsive layouts. The approach uses Aspose.PDF’s `RectangleShape`, boundary checking, and simple arithmetic to adapt to any page size.

Next, you might explore:

* Adding **fill colors** and **line styles** (dashed, dotted) – secondary keyword: how to define rectangle dimensions with style.
* Combining multiple shapes into a single `Page` to create charts or forms.
* Exporting the PDF to a stream for web APIs instead of saving to disk.

Experiment with different sizes, colors, and positions to master PDF graphics in your .NET applications. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Customize PDFs with Aspose.PDF for .NET&#58; Set Page Margins and Draw Lines](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET&#58; A Complete Guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [How to Add Page Number Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}