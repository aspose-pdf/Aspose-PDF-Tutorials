---
category: general
date: 2026-09-12
description: Learn how to add transparency to PDF, draw a rectangle on PDF, and save
  PDF with transparency using Aspose.PDF in C# – step‑by‑step guide.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- draw rectangle on pdf
- save pdf with transparency
language: en
lastmod: 2026-09-12
og_description: Add transparency to PDF, draw a rectangle on PDF, and save PDF with
  transparency using Aspose.PDF in C#. Follow this complete tutorial.
og_image_alt: Screenshot of a PDF page showing a semi‑transparent rectangle drawn
  with Aspose.PDF
og_title: Add transparency to PDF and draw a rectangle on PDF – complete C# guide
schemas:
- author: Aspose
  dateModified: '2026-09-12'
  description: Learn how to add transparency to PDF, draw a rectangle on PDF, and
    save PDF with transparency using Aspose.PDF in C# – step‑by‑step guide.
  headline: How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF
url: /net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF

If you need to **add transparency to PDF** files, this guide shows you exactly how to do it in C#. You’ll also learn how to **draw rectangle on PDF** and finally **save PDF with transparency** so the result can be reused in reports, invoices, or any document‑automation workflow.

In this tutorial you will:

* Load an existing PDF document.
* Create a custom graphics state that defines stroke and fill opacity.
* Apply that graphics state to the canvas and draw a rectangle.
* Save the modified file while preserving the transparency settings.

No external tools are required beyond the Aspose.PDF for .NET library, and every line of code is explained so you understand *why* each step matters.

## Prerequisites

* .NET 6.0 or later (the code also works with .NET Framework 4.7+).
* A licensed or evaluation copy of **Aspose.PDF for .NET**. Install it via NuGet:

```bash
dotnet add package Aspose.Pdf
```

* An input PDF (`input.pdf`) placed in a folder you can reference from your project.

## Step 1: Load the PDF document

The first operation is to open the source file. Using the `using` statement guarantees that the document is disposed properly, which prevents file‑locking issues later when you try to save.

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";
using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

*Why this matters*: Loading the document gives you access to the page collection, resource dictionaries, and canvas objects required for drawing.

## Step 2: Access the first page’s resource dictionary

Every PDF page has a **resource dictionary** that stores objects such as fonts, images, and graphics states. To introduce a new transparency setting we need to edit the `ExtGState` entry.

```csharp
// Step 2: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

*Why this matters*: The `DictionaryEditor` lets us read and modify low‑level PDF objects without breaking the document structure.

## Step 3: Create a custom graphics state with transparency values

A graphics state (`ExtGState`) controls how drawing operations are rendered. We define two opacity parameters:

* **CA** – stroke opacity (the outline of shapes).
* **ca** – fill opacity (the interior of shapes).

We also set the blend mode (`BM`) to “Normal”, which is the most common compositing operation.

```csharp
// Step 3: Create a custom graphics state (ExtGState) with transparency settings
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
var customGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "CA", new Aspose.Pdf.Cos.CosPdfNumber(1)),          // stroke opacity = 100 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),        // fill opacity = 50 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))      // normal blend mode
};

foreach (var p in parameters)
    customGs.Add(p);

// Register the new graphics state under the name "GS0"
extGStateDict.Add("GS0", customGs);
```

*Why this matters*: By adding `GS0` to the `ExtGState` dictionary we create a reusable reference that the canvas can activate before drawing. The fill opacity of `0.5` makes the rectangle semi‑transparent, achieving the **add transparency to PDF** goal.

## Step 4: Apply the graphics state and draw a rectangle

Now we tell the page’s canvas to use the graphics state we just created, then we draw a rectangle. The coordinates follow the PDF coordinate system (origin at the lower‑left corner).

```csharp
// Step 4: Apply the custom graphics state and draw a rectangle
var canvas = firstPage.Canvas;

// Activate the transparency graphics state
canvas.SetGraphicsState("GS0");

// Draw a rectangle from (100, 500) to (200, 600)
canvas.Rectangle(100, 500, 200, 600);

// Render the rectangle outline using the current graphics state
canvas.Stroke();
```

*Why this matters*: `SetGraphicsState("GS0")` switches the drawing context to the transparency settings defined earlier. The `Rectangle` method defines the shape, and `Stroke` renders the outline with the specified opacity. If you also want a filled rectangle, replace `Stroke()` with `FillAndStroke()`.

## Step 5: Save the modified PDF while preserving transparency

Finally, write the document back to disk. The output file contains the new graphics state, the drawn rectangle, and the transparency information.

```csharp
// Step 5: Save the modified PDF
string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
pdfDocument.Save(outputPath);
```

*Why this matters*: Saving the document finalizes all changes. The resulting file can be opened in any PDF viewer, and the rectangle will appear with 50 % fill opacity.

### Expected result

When you open `output_with_extgstate.pdf` you should see a rectangle whose border is fully opaque and whose interior is semi‑transparent, allowing any underlying page content to show through.

## Edge cases and practical tips

| Situation | Recommended adjustment |
|-----------|------------------------|
| **Multiple pages** | Loop over `pdfDocument.Pages` and repeat steps 2‑4 for each target page. |
| **Different opacity values** | Change the `CosPdfNumber` values for `CA` (stroke) and `ca` (fill) to any number between `0` (fully transparent) and `1` (fully opaque). |
| **Custom blend modes** | Replace `"Normal"` with `"Multiply"`, `"Screen"`, or any PDF‑standard blend mode supported by your viewer. |
| **Filled rectangle** | Call `canvas.FillAndStroke()` instead of `canvas.Stroke()` to apply both fill and outline. |
| **Re‑using the same graphics state** | You can call `canvas.SetGraphicsState("GS0")` before drawing any number of shapes on the same page. |

**Pro tip:** Always inspect the resource dictionary after adding a new `ExtGState`. If the dictionary does not exist, create it first:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
    resourcesEditor.Add("ExtGState", new Aspose.Pdf.Cos.CosPdfDictionary(pdfDocument));
```

## Full, runnable example

Below is a self‑contained program that you can copy into a console application and run immediately (replace `YOUR_DIRECTORY` with an actual path).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF document
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Access the first page’s resources
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        if (!resourcesEditor.ContainsKey("ExtGState"))
            resourcesEditor.Add("ExtGState", new CosPdfDictionary(pdfDocument));

        // 3️⃣ Create a custom graphics state with transparency
        var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        var customGs = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };

        foreach (var p in parameters)
            customGs.Add(p);

        extGStateDict.Add("GS0", customGs);

        // 4️⃣ Apply the graphics state and draw a rectangle
        var canvas = firstPage.Canvas;
        canvas.SetGraphicsState("GS0");
        canvas.Rectangle(100, 500, 200, 600);
        canvas.Stroke(); // use FillAndStroke() for a filled shape

        // 5️⃣ Save the PDF with transparency
        string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine("PDF saved with a transparent rectangle at: " + outputPath);
    }
}
```

Running the program produces `output_with_extgstate.pdf`, which demonstrates **add transparency to PDF**, **draw rectangle on PDF**, and **save PDF with transparency** all in one flow.

## Conclusion

You now know how to **add transparency to PDF** files, **draw rectangle on PDF**, and **save PDF with transparency** using Aspose.PDF for .NET. The process revolves around creating a custom `ExtGState`, applying it to the canvas, and persisting the changes. With these building blocks you can extend the technique to other shapes, multiple pages, or dynamic opacity values.

**Next steps**

* Explore other drawing primitives such as `canvas.Ellipse`, `canvas.Path`, or `canvas.TextFragment` while reusing the same graphics state.
* Combine transparency with image overlays to create watermarks (`canvas.Image` + custom `ExtGState`).
* Review the Aspose.PDF documentation on **graphics state parameters** for advanced compositing effects.

Happy coding, and enjoy the visual flexibility that transparency brings to your PDF workflows!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [How to Add a Line Object in PDF Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Add Image Stamps to PDFs Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}