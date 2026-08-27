---
category: general
date: 2026-02-14
description: 'Create PDF document C# quickly: add page to PDF, draw a rectangle shape,
  and save PDF to file using Aspose.Pdf in a few lines of code.'
draft: false
keywords:
- create pdf document c#
- add page to pdf
- how to draw rectangle
- add shape to pdf
- save pdf to file
language: en
og_description: Create PDF document C# in minutes. Learn how to add page to PDF, draw
  rectangle, add shape to PDF, and save PDF to file with clear code examples.
og_title: Create PDF Document C# – Step‑by‑Step Guide
tags:
- Aspose.Pdf
- C#
- PDF generation
title: Create PDF Document C# – Add Page, Draw Rectangle & Save
url: /net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create PDF Document C# – Add Page, Draw Rectangle & Save

Ever needed to **create PDF document C#** from scratch and wondered where to start? You're not the only one—many developers hit that same wall when they first tackle programmatic PDF generation. The good news? With a few lines of Aspose.Pdf code you can add a page to PDF, draw a rectangle, and **save PDF to file** without breaking a sweat.

In this tutorial we’ll walk through everything you need: initializing the PDF, inserting a new page, drawing a rectangle shape, and finally persisting the file on disk. By the end you’ll have a runnable console app that produces a crisp blue‑bordered rectangle inside a fresh PDF page.

## What You’ll Need

- **.NET 6 or later** (the sample uses top‑level statements, but any recent .NET version works)
- **Aspose.Pdf for .NET** NuGet package  
  ```bash
  dotnet add package Aspose.Pdf
  ```
- A folder where you have write permission – the tutorial will save the file to `YOUR_DIRECTORY/shapes.pdf`.

No extra configuration, no XML, just plain C#.

## Create PDF Document C# – Overview

The first step is to spin up a `Document` object. Think of this as your blank canvas; everything you add later—pages, text, shapes—gets attached to this single instance.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document (the canvas)
using var pdfDocument = new Document();
```

> **Why `using var`?**  
> The `Document` class implements `IDisposable`. Wrapping it in a `using` statement guarantees that all unmanaged resources (file handles, native buffers) are released as soon as we’re done, which is especially important in long‑running services.

## Add Page to PDF

A PDF without pages is like a book with no pages—pretty useless. Adding a page is a single method call, but it also gives you a `Page` object you can later manipulate.

```csharp
// Step 2: Add a fresh page to the document
var pdfPage = pdfDocument.Pages.Add();
```

> **Tip:** The newly added page automatically adopts the default size (A4). If you need a custom size, you can set `pdfPage.PageInfo.Width` and `Height` before adding any content.

## How to Draw Rectangle

Now for the fun part: drawing a rectangle. Aspose.Pdf uses the `RectangleShape` class, which expects a `Rectangle` (x, y, width, height) defining the bounds. The coordinates start from the bottom‑left corner of the page.

```csharp
// Step 3: Define the rectangle bounds (x, y, width, height)
// This will be validated – an exception is thrown if the rectangle is out of bounds
var rectangleBounds = new Rectangle(50, 50, 200, 150);
```

> **Edge case:** If `x + width` exceeds the page width or `y + height` exceeds the page height, Aspose throws an `ArgumentException`. Always double‑check your dimensions, especially when generating PDFs for different page sizes.

## Add Shape to PDF

With the bounds ready, we create the shape, give it a blue stroke, and drop it onto the page’s paragraph collection.

```csharp
// Step 4: Create a rectangle shape with a blue stroke and add it to the page
var rectangleShape = new RectangleShape(rectangleBounds)
{
    StrokeColor = Color.Blue,   // Outline color
    // FillColor = Color.LightGray, // Uncomment to add a fill
    // LineWidth = 2                // Adjust border thickness if needed
};
pdfPage.Paragraphs.Add(rectangleShape);
```

> **Why add it to `Paragraphs`?**  
> In Aspose.Pdf, visual elements like shapes are treated as “paragraphs” because they occupy a rectangular area on the page. This design keeps the layout engine consistent across text and graphics.

## Save PDF to File

The final act is persisting the document. Provide a full path, and Aspose handles the heavy lifting—compression, object streams, and cross‑reference tables are all taken care of automatically.

```csharp
// Step 5: Save the PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/shapes.pdf");
```

> **Pro tip:** Use `Path.Combine(Environment.CurrentDirectory, "shapes.pdf")` if you want the file next to your executable, or `Directory.CreateDirectory` beforehand to avoid a `DirectoryNotFoundException`.

### Expected Result

Open `shapes.pdf` with any PDF viewer. You should see a single A4‑sized page with a **blue‑bordered rectangle** positioned 50 points from the left and bottom edges, measuring 200 × 150 points. No text, just the shape—perfect for watermarks, form fields, or visual placeholders.

![PDF document with a blue rectangle created using create pdf document c#](https://example.com/images/pdf-rectangle.png "PDF document with a blue rectangle created using create pdf document c#")

*Alt text:* *PDF document with a blue rectangle created using create pdf document c#.*

## Full Working Example

Below is the complete, copy‑and‑paste‑ready program. It compiles as a console app (`dotnet new console`) and runs without any extra configuration beyond the NuGet package.

```csharp
// Program.cs
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

using var pdfDocument = new Document();               // Create PDF document
var pdfPage = pdfDocument.Pages.Add();                // Add a page

// Define rectangle bounds (x, y, width, height)
// Aspose validates the rectangle – out‑of‑bounds throws an exception
var rectangleBounds = new Rectangle(50, 50, 200, 150);

// Create the rectangle shape (blue stroke) and add it to the page
var rectangleShape = new RectangleShape(rectangleBounds)
{
    StrokeColor = Color.Blue
};
pdfPage.Paragraphs.Add(rectangleShape);

// Save the document to disk
pdfDocument.Save("YOUR_DIRECTORY/shapes.pdf");

// Inform the user
Console.WriteLine("PDF created successfully at YOUR_DIRECTORY/shapes.pdf");
```

Run the program, open the generated file, and you’ll see the shape exactly where we defined it.

## Common Questions & Gotchas

- **Q:** *What if I need a filled rectangle?*  
  **A:** Uncomment the `FillColor` line in the `RectangleShape` initializer. Aspose supports solid colors, gradients, and even image fills.

- **Q:** *Can I draw multiple shapes on the same page?*  
  **A:** Absolutely. Just create additional `RectangleShape`, `Ellipse`, or `Polygon` objects and add each to `pdfPage.Paragraphs`.

- **Q:** *Is the coordinate system always bottom‑left?*  
  **A:** Yes, Aspose follows the PDF specification where the origin (0,0) is at the lower‑left corner. If you prefer a top‑left origin, you’ll need to calculate `y = pageHeight - desiredY`.

- **Q:** *What happens if the target folder doesn’t exist?*  
  **A:** `pdfDocument.Save` will throw a `DirectoryNotFoundException`. Pre‑create the folder with `Directory.CreateDirectory`.

## Next Steps

Now that you know how to **add page to PDF**, **how to draw rectangle**, **add shape to PDF**, and **save PDF to file**, you can expand this foundation:

- Insert text, images, or tables alongside shapes.  
- Use `Graphics` for free‑form drawing (lines, arcs, custom paths).  
- Explore PDF encryption or digital signatures if security is a concern.  

Each of those topics builds directly on the code we just covered, so feel confident experimenting.

---

**Bottom line:** You’ve just learned the complete workflow to **create PDF document C#** with Aspose.Pdf—initialize, add a page, draw a rectangle shape, and persist the file. It’s a solid building block for invoices, reports, certificates, or any automated document you need to generate on the fly. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}