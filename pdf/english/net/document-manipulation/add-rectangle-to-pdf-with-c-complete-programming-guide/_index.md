---
category: general
date: 2026-06-05
description: Add rectangle to PDF using Aspose.Pdf in C#. Learn how to load existing
  PDF, edit PDF page, and insert shape into PDF in minutes.
draft: false
keywords:
- add rectangle to pdf
- draw rectangle on pdf
- load existing pdf
- edit pdf page
- insert shape into pdf
language: en
og_description: Add rectangle to PDF quickly. This tutorial shows how to load existing
  PDF, edit PDF page, and draw rectangle on PDF using Aspose.Pdf.
og_title: Add Rectangle to PDF with C# – Step‑by‑Step Guide
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Add rectangle to PDF using Aspose.Pdf in C#. Learn how to load existing
    PDF, edit PDF page, and insert shape into PDF in minutes.
  headline: Add Rectangle to PDF with C# – Complete Programming Guide
  type: TechArticle
- description: Add rectangle to PDF using Aspose.Pdf in C#. Learn how to load existing
    PDF, edit PDF page, and insert shape into PDF in minutes.
  name: Add Rectangle to PDF with C# – Complete Programming Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.6+). - Aspose.Pdf
      for .NET NuGet package (`Install-Package Aspose.Pdf`). - Basic familiarity with
      C# syntax (no deep PDF knowledge required).'
  - name: Why loading matters
    text: Before you can draw anything, the PDF must be in memory. The `Document`
      constructor reads the file, parses its internal structure, and gives you an
      object model to work with. If the file is locked or corrupted, Aspose will throw
      a descriptive exception—so you know exactly what went wrong.
  - name: Code
    text: '```csharp Document doc = new Document("YOUR_DIRECTORY/input.pdf"); ```'
  - name: Why page selection is crucial
    text: PDFs are page‑oriented; each page has its own coordinate system. Aspose
      uses a **1‑based** index, which trips up developers coming from 0‑based collections.
      Selecting the wrong page either throws an `ArgumentOutOfRangeException` or modifies
      an unintended page.
  - name: Code
    text: '```csharp Page page = doc.Pages[1]; // First page ```'
  - name: Understanding the rectangle coordinates
    text: A rectangle in Aspose.Pdf is defined by its lower‑left (`xLL`, `yLL`) and
      upper‑right (`xUR`, `yUR`) corners. The coordinate system starts at the **bottom‑left**
      of the page, with X increasing to the right and Y increasing upward. This is
      opposite of many UI frameworks, so keep an eye on the axes.
  - name: Code to add the shape
    text: '```csharp Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500,
      700); page.AddRectangle(rect); ```'
  - name: Why saving is the final step
    text: All manipulations stay in memory until you persist them. `Document.Save`
      writes the new content to disk (or stream). Overwriting the original file is
      possible, but keeping a backup (`output.pdf`) is safer.
  - name: Code
    text: '```csharp doc.Save("YOUR_DIRECTORY/output.pdf"); ```'
  type: HowTo
- questions:
  - answer: Yes—loop through `doc.Pages` and repeat the `AddRectangle` call for each
      `Page` object.
    question: Can I add the rectangle to every page automatically?
  - answer: Aspose provides `AddCircle`, `AddPolygon`, and `AddPolyline` methods.
      The same rectangle logic applies for bounding boxes.
    question: What if I need to draw a circle or a polygon?
  - answer: 'Compute the center coordinates:'
    question: Is there a way to position the rectangle relative to the page center?
  - answer: Aspose loads pages lazily, but if you’re processing thousands of pages,
      consider using `PdfExtractor` to work on subsets or stream the file to reduce
      memory footprint.
    question: Performance concerns for large PDFs?
  type: FAQPage
tags:
- pdf
- csharp
- aspose
- shape-manipulation
title: Add Rectangle to PDF with C# – Complete Programming Guide
url: /net/document-manipulation/add-rectangle-to-pdf-with-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Rectangle to PDF with C# – Complete Programming Guide

Ever needed to **add rectangle to pdf** but weren’t sure which API call to use? You’re not alone—many developers hit that wall when they first try to edit a PDF programmatically. The good news? With a few lines of C# and the powerful Aspose.Pdf library, you can draw a rectangle on any page of an existing document in a flash.

In this guide we’ll walk through loading an existing PDF, selecting the right page, defining a rectangle that fits, and finally inserting the shape into the PDF. By the end you’ll have a reusable snippet that you can drop into any .NET project. Oh, and we’ll also touch on **draw rectangle on pdf** nuances you might not have considered.

## What You’ll Gain

- A clear, step‑by‑step solution that works out‑of‑the‑box.
- Understanding of how **load existing pdf** files safely.
- Tips for **edit pdf page** without corrupting the document.
- Strategies to **insert shape into pdf** beyond just rectangles.
- Ready‑to‑run C# code you can copy‑paste immediately.

### Prerequisites

- .NET 6.0 or later (the code also works on .NET Framework 4.6+).
- Aspose.Pdf for .NET NuGet package (`Install-Package Aspose.Pdf`).
- Basic familiarity with C# syntax (no deep PDF knowledge required).

If you have those, let’s dive in.

![Add rectangle to PDF example](add-rectangle-to-pdf.png "Screenshot showing a rectangle added to a PDF page – add rectangle to pdf")

## Add Rectangle to PDF – Step‑by‑Step Overview

Below is the full, runnable example that follows the exact order we’ll discuss:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the existing PDF file
        Document doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Select the first page (pages are 1‑based)
        Page page = doc.Pages[1];

        // 3️⃣ Define a rectangle that fits inside the page bounds
        //    (xLL, yLL, xUR, yUR) – lower‑left & upper‑right corners
        Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500, 700);

        // 4️⃣ Add the rectangle to the page – this draws the shape
        page.AddRectangle(rect);

        // 5️⃣ Save the modified PDF to a new file
        doc.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

Now let’s unpack each line so you understand **why** we do what we do, not just **what**.

## Load Existing PDF Document

### Why loading matters

Before you can draw anything, the PDF must be in memory. The `Document` constructor reads the file, parses its internal structure, and gives you an object model to work with. If the file is locked or corrupted, Aspose will throw a descriptive exception—so you know exactly what went wrong.

### Code

```csharp
Document doc = new Document("YOUR_DIRECTORY/input.pdf");
```

- Replace `YOUR_DIRECTORY` with the absolute or relative path to your source file.
- The path can be a URL if you enable Aspose’s remote loading (advanced scenario).
- **Tip:** Wrap this in a `try/catch` block to handle `FileNotFoundException` or `PdfException` gracefully.

```csharp
try
{
    Document doc = new Document("input.pdf");
}
catch (Exception ex)
{
    Console.WriteLine($"Failed to load PDF: {ex.Message}");
    return;
}
```

## Select and Prepare the Page

### Why page selection is crucial

PDFs are page‑oriented; each page has its own coordinate system. Aspose uses a **1‑based** index, which trips up developers coming from 0‑based collections. Selecting the wrong page either throws an `ArgumentOutOfRangeException` or modifies an unintended page.

### Code

```csharp
Page page = doc.Pages[1]; // First page
```

If you need to work on page 3, simply change the index to `3`. For dynamic scenarios, you can loop:

```csharp
foreach (Page pg in doc.Pages)
{
    // Apply rectangle to every page
}
```

## Define and Draw Rectangle on PDF

### Understanding the rectangle coordinates

A rectangle in Aspose.Pdf is defined by its lower‑left (`xLL`, `yLL`) and upper‑right (`xUR`, `yUR`) corners. The coordinate system starts at the **bottom‑left** of the page, with X increasing to the right and Y increasing upward. This is opposite of many UI frameworks, so keep an eye on the axes.

- `0,0` is the bottom‑left corner of the page.
- Width = `xUR - xLL`; Height = `yUR - yLL`.

If you accidentally set a rectangle larger than the page, `AddRectangle` will throw an exception. To avoid that, you can query the page size:

```csharp
double pageWidth  = page.PageInfo.Width;
double pageHeight = page.PageInfo.Height;
```

Then clamp your rectangle:

```csharp
double rectWidth  = Math.Min(500, pageWidth);
double rectHeight = Math.Min(700, pageHeight);
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, rectWidth, rectHeight);
```

### Code to add the shape

```csharp
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500, 700);
page.AddRectangle(rect);
```

- `AddRectangle` automatically draws a thin black border.
- Want a filled rectangle? Use `page.AddAnnotation(new SquareAnnotation(page, rect) { FillColor = Color.Yellow });`.
- Need a different line thickness? Set `rect.LineWidth = 2;` before adding.

#### Edge case: multiple rectangles

If you call `AddRectangle` repeatedly, each call adds another shape. To avoid overlapping, offset subsequent rectangles:

```csharp
for (int i = 0; i < 3; i++)
{
    var offset = i * 20;
    var r = new Aspose.Pdf.Rectangle(offset, offset, 500 + offset, 700 + offset);
    page.AddRectangle(r);
}
```

## Save the Modified PDF

### Why saving is the final step

All manipulations stay in memory until you persist them. `Document.Save` writes the new content to disk (or stream). Overwriting the original file is possible, but keeping a backup (`output.pdf`) is safer.

### Code

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

- You can also save to a `MemoryStream` if you need to send the PDF over HTTP:

```csharp
using var ms = new MemoryStream();
doc.Save(ms);
byte[] pdfBytes = ms.ToArray();
// return File(pdfBytes, "application/pdf");
```

## Full Working Example (Copy‑Paste Ready)

Putting everything together, here’s the final program you can run right now:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

class AddRectangleDemo
{
    static void Main()
    {
        const string inputPath  = "input.pdf";
        const string outputPath = "output.pdf";

        // Load the existing PDF
        Document doc;
        try
        {
            doc = new Document(inputPath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error loading PDF: {ex.Message}");
            return;
        }

        // Ensure the document has at least one page
        if (doc.Pages.Count == 0)
        {
            Console.WriteLine("PDF contains no pages.");
            return;
        }

        // Select the first page (1‑based index)
        Page page = doc.Pages[1];

        // Get page dimensions to avoid overflow
        double pageW = page.PageInfo.Width;
        double pageH = page.PageInfo.Height;

        // Define rectangle size (clamp to page bounds)
        double rectW = Math.Min(500, pageW);
        double rectH = Math.Min(700, pageH);
        Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, rectW, rectH);

        // Optional: set line width and color
        rect.LineWidth = 2;
        rect.Color = Color.Blue;

        // Add rectangle to the page
        page.AddRectangle(rect);

        // Save the result
        doc.Save(outputPath);
        Console.WriteLine($"Rectangle added and saved to {outputPath}");
    }
}
```

**Expected output:** Open `output.pdf` and you’ll see a blue‑bordered rectangle anchored at the bottom‑left corner of the first page, sized up to 500 × 700 points (or smaller if the page is tiny).

## Common Questions & Pro Tips

- **Can I add the rectangle to every page automatically?**  
  Yes—loop through `doc.Pages` and repeat the `AddRectangle` call for each `Page` object.

- **What if I need to draw a circle or a polygon?**  
  Aspose provides `AddCircle`, `AddPolygon`, and `AddPolyline` methods. The same rectangle logic applies for bounding boxes.

- **Is there a way to position the rectangle relative to the page center?**  
  Compute the center coordinates:  
  ```csharp
  double centerX = pageW / 2;
  double centerY = pageH / 2;
  double halfW = rectW / 2;
  double halfH = rectH / 2;
  var centeredRect = new Aspose.Pdf.Rectangle(centerX - halfW, centerY - halfH,
                                              centerX + halfW, centerY + halfH);
  page.AddRectangle(centeredRect);
  ```

- **Performance concerns for large PDFs?**  
  Aspose loads pages lazily, but if you’re processing thousands of pages, consider using `PdfExtractor` to work on subsets or stream the file to reduce memory footprint.

## Conclusion

You now know **how to add rectangle


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET: A Complete Guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Add Images & Page Numbers to PDFs Using Aspose.PDF for .NET: A Complete Guide](/pdf/english/net/document-manipulation/enhance-pdfs-images-page-numbers-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}