---
category: general
date: 2026-06-21
description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
  black rectangle annotation, and save modified PDF efficiently.
draft: false
keywords:
- draw rectangle on pdf
- load pdf document
- add black rectangle
- create black rectangle
- save modified pdf
language: en
og_description: Draw rectangle on PDF in C# by loading a PDF document, creating a
  black rectangle annotation, and saving the modified PDF. Full code included.
og_title: Draw Rectangle on PDF with C# – Complete Programming Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
    black rectangle annotation, and save modified PDF efficiently.
  headline: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
  type: TechArticle
- description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
    black rectangle annotation, and save modified PDF efficiently.
  name: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
  steps:
  - name: .NET 6.0 SDK (or any recent .NET version) installed
    text: .NET 6.0 SDK (or any recent .NET version) installed
  - name: 'A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package
      Aspose.PDF`)'
    text: 'A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package
      Aspose.PDF`)'
  - name: An existing PDF file (`input.pdf`) placed in a folder you can read/write
    text: An existing PDF file (`input.pdf`) placed in a folder you can read/write
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
title: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
url: /net/annotations/draw-rectangle-on-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Draw Rectangle on PDF with C# – Complete Programming Tutorial

Ever needed to **draw rectangle on PDF** files from a .NET app but weren’t sure where to start? You’re not the only one. Whether it’s highlighting a section, redacting sensitive data, or simply adding a visual cue, learning how to *draw rectangle on PDF* programmatically can save you hours of manual editing.

In this guide we’ll walk through a practical example that **loads a PDF document**, **creates a black rectangle**, and then **saves the modified PDF**. By the end you’ll have a reusable snippet you can drop into any C# project—no mystery, just clear code and explanations.

## What This Tutorial Covers

- How to **load pdf document** using the Aspose.PDF for .NET library  
- Defining a rectangle’s coordinates and ensuring it stays inside page bounds  
- Using the **add black rectangle** method to annotate the page  
- **Save modified pdf** to a new file location  
- Edge‑case handling (multiple pages, out‑of‑bounds rectangles, custom colors)  

No external tools, no vague references—just a complete, runnable example you can copy‑paste.

---

## Prerequisites

Before we dive in, make sure you have:

1. .NET 6.0 SDK (or any recent .NET version) installed  
2. A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package Aspose.PDF`)  
3. An existing PDF file (`input.pdf`) placed in a folder you can read/write  

That’s it. If you’re comfortable with basic C# syntax, you’ll be good to go.

---

## Step 1: Load PDF Document

The first thing we need is a **load pdf document** call. Aspose.PDF’s `Document` class takes the file path and reads the whole file into memory.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing;

// Load the source PDF
Document pdfDocument = new Document(@"C:\MyFiles\input.pdf");
```

*Why this matters*: Loading the PDF gives you access to its pages, metadata, and drawing surface. Without this step you can’t place any shapes.

---

## Step 2: Pick the Target Page

PDF pages are 1‑based in Aspose, so the first page is index 1. Grab the page you want to annotate—usually the first one for a quick demo.

```csharp
// Get the first page (pages are 1‑based)
Page targetPage = pdfDocument.Pages[1];
```

If you need to work on a different page, just change the index. Remember to validate that the index exists to avoid `ArgumentOutOfRangeException`.

---

## Step 3: Define the Rectangle Geometry

A rectangle is defined by its lower‑left (X,Y) and upper‑right (X,Y) coordinates. The `Rectangle` struct stores these as `LLX`, `LLY`, `URX`, `URY`.

```csharp
// Define the rectangle (lower‑left X,Y and upper‑right X,Y)
Rectangle boundingRect = new Rectangle(100, 100, 300, 300);
```

Feel free to adjust those numbers—`100,100` places the lower‑left corner 100 points from the left and bottom edges, while `300,300` sets the upper‑right corner 300 points from the edges.

---

## Step 4: Verify the Rectangle Fits Inside the Page

Attempting to draw outside the page bounds will either be ignored or cause an exception, depending on the library version. A quick check keeps your code robust.

```csharp
// Ensure the rectangle fits within the page dimensions
if (targetPage.PageInfo.Width >= boundingRect.URX &&
    targetPage.PageInfo.Height >= boundingRect.URY)
{
    // Rectangle is safe to add
}
else
{
    throw new InvalidOperationException("Rectangle exceeds page dimensions.");
}
```

*Pro tip*: If you plan to support PDFs of varying sizes, you might calculate the rectangle based on a percentage of the page width/height instead of absolute points.

---

## Step 5: Add Black Rectangle Annotation

Now the fun part—**add black rectangle** to the page. Aspose provides `AddRectangle` which takes the geometry and a `Color`. We’ll use `Color.Black` to **create black rectangle**.

```csharp
// Add a black rectangle annotation to the page
targetPage.AddRectangle(boundingRect, Color.Black);
```

That single line does the heavy lifting: it creates an annotation object, sets its border color to black, and inserts it into the page’s annotation collection.

If you ever need a different fill or border style, explore the overload that accepts an `Annotation` object where you can tweak line width, dash pattern, or even opacity.

---

## Step 6: Save Modified PDF

Finally, persist your changes with **save modified pdf**. You can overwrite the original or write to a new file—here we’ll create an output file.

```csharp
// Save the updated PDF to a new location
pdfDocument.Save(@"C:\MyFiles\output.pdf");
```

That’s the whole workflow. Run the program and open `output.pdf`; you should see a solid black rectangle where you defined it.

---

## Full Working Example

Below is a self‑contained console application that puts all the steps together. Copy it into a new `.csproj` and hit **Run**.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load PDF document
            Document pdfDocument = new Document(@"C:\MyFiles\input.pdf");

            // 2️⃣ Get the first page (pages are 1‑based)
            Page firstPage = pdfDocument.Pages[1];

            // 3️⃣ Define the rectangle geometry
            Rectangle rect = new Rectangle(100, 100, 300, 300);

            // 4️⃣ Verify bounds
            if (firstPage.PageInfo.Width < rect.URX || firstPage.PageInfo.Height < rect.URY)
            {
                Console.WriteLine("Rectangle does not fit on the page.");
                return;
            }

            // 5️⃣ Add a black rectangle annotation
            firstPage.AddRectangle(rect, Color.Black);

            // 6️⃣ Save modified PDF
            pdfDocument.Save(@"C:\MyFiles\output.pdf");

            Console.WriteLine("Successfully drew rectangle on PDF and saved the file.");
        }
    }
}
```

**Expected output** in the console:

```
Successfully drew rectangle on PDF and saved the file.
```

Open `output.pdf` and you’ll see a black rectangle positioned at the coordinates you specified.

---

## Handling Common Variations

| Situation | What to Change | Why |
|-----------|----------------|-----|
| **Multiple pages** | Loop through `pdfDocument.Pages` and apply the same logic to each `Page` object. | Allows batch annotation across a whole document. |
| **Different colors** | Replace `Color.Black` with `Color.Red` or any `System.Drawing.Color`. | Useful for highlighting rather than redacting. |
| **Transparent fill** | Use `new Annotation(rect) { Color = Color.Black, Opacity = 0.5 }`. | Gives a semi‑transparent overlay instead of a solid block. |
| **Dynamic rectangle size** | Compute `URX` and `URY` based on `PageInfo.Width * 0.5` etc. | Makes the rectangle adapt to various page dimensions. |
| **Error handling** | Wrap the whole block in `try…catch` and log `Aspose.Pdf.IOException`. | Prevents crashes when the source file is missing or locked. |

These tweaks illustrate how you can **create black rectangle** annotations in many contexts without rewriting the core logic.

---

## Pro Tips & Pitfalls

- **Dispose the Document**: Although Aspose.PDF implements `IDisposable`, the `using` pattern isn’t strictly required for short‑lived console apps. In long‑running services, wrap `Document` in a `using` block to free native resources promptly.  
- **Coordinate System**: PDF coordinates start at the lower‑left corner. If you’re used to top‑left origin (like WinForms), you’ll need to invert the Y‑axis: `pageHeight - y`.  
- **Performance**: Adding annotations to very large PDFs can be memory‑intensive. Consider processing pages in chunks or using `PdfFileEditor` for more lightweight edits.  
- **Legal**: Ensure you have rights to modify the source PDF—some documents are protected against editing.

---

## Conclusion

We’ve just demonstrated how to **draw rectangle on PDF** using C#—starting from **load pdf document**, defining geometry, **add black rectangle**, and finally **save modified pdf**. The example is complete, runnable, and adaptable to real‑world scenarios like batch processing or custom styling.

Next, you might explore adding other annotation types (text, highlights) or merging multiple PDFs after annotation. Both **load pdf document** and **save modified pdf** steps remain the same, so you can extend this pattern with confidence.

Got a twist you tried? Share it in the comments, and happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Filled Rectangle Object in PDF using Java](/pdf/english/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)
- [Create Filled Rectangle Object In Pdf Using Java](/pdf/german/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)
- [Create Filled Rectangle Object In Pdf Using Java](/pdf/french/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}