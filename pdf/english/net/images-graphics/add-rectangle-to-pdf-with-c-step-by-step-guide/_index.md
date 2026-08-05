---
category: general
date: 2026-08-04
description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
  Aspose.Pdf in a clear, complete example.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to pdf
- how to draw shape in pdf c#
language: en
lastmod: 2026-08-04
og_description: Add rectangle to PDF using C#. This tutorial shows how to draw shape
  in PDF C# quickly and reliably.
og_image_alt: Screenshot of a PDF page with a blue rectangle drawn by C# code
og_title: Add rectangle to PDF with C# – complete programming guide
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  headline: Add rectangle to PDF with C# – step‑by‑step guide
  type: TechArticle
- description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  name: Add rectangle to PDF with C# – step‑by‑step guide
  steps:
  - name: '**Create a new console project**'
    text: '**Create a new console project**'
  - name: '**Add the Aspose.Pdf package**'
    text: '**Add the Aspose.Pdf package**'
  - name: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
    text: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Add rectangle to PDF with C# – step‑by‑step guide
url: /net/images-graphics/add-rectangle-to-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add rectangle to PDF with C# – step‑by‑step guide

If you need to **add rectangle to PDF** files from a C# application, this guide shows you exactly how to do it. You’ll see a complete, runnable example that draws a shape in PDF C# using the Aspose.Pdf library, and you’ll understand why each line of code matters.

Drawing shapes in PDFs is a common requirement for report generators, invoice templates, and custom document branding. By the end of this tutorial you can insert any rectangular annotation, change its size, color, or position, and save the modified document without losing existing content.

**What you’ll learn**

* How to load an existing PDF with Aspose.Pdf.
* How to define rectangle bounds and create a rectangle shape.
* How to add the rectangle to a page’s paragraph collection.
* How to save the updated PDF and verify the result.
* Variations for multiple pages, transparency, and custom line styles.

**Prerequisites**

* .NET 6.0 or later (the code also works with .NET Framework 4.7+).
* Visual Studio 2022 or any C# IDE.
* A NuGet reference to `Aspose.Pdf` (free trial or licensed version).
* An input PDF file named `input.pdf` placed in a folder you control.

---

## How to draw shape in PDF C# – set up the project

1. **Create a new console project**  

   ```bash
   dotnet new console -n PdfRectangleDemo
   cd PdfRectangleDemo
   ```

2. **Add the Aspose.Pdf package**  

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. **Place `input.pdf`** in the project directory (or any folder you reference later).

The project is now ready to compile code that will **add rectangle to PDF** files.

---

## Step 1: Load the PDF document

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // Load the existing PDF file.
        Document pdfDoc = new Document("input.pdf");
```

*The `Document` class parses the file and exposes a `Pages` collection. Loading is the first required operation before any drawing can occur.*

---

## Step 2: Choose the target page

```csharp
        // Get the first page (pages are 1‑based).
        Page firstPage = pdfDoc.Pages[1];
```

*If you need to add the rectangle to a different page, replace the index with the desired page number. The library throws an exception when the index is out of range, so ensure the PDF contains enough pages.*

---

## Step 3: Define rectangle bounds

```csharp
        // Define the rectangle's position and size (points).
        // (left, bottom, right, top) – origin is bottom‑left.
        Rectangle bounds = new Rectangle(50, 700, 300, 800);
```

*The coordinate system uses points (1 pt = 1/72 inch). The example creates a 250 pt wide by 100 pt high rectangle near the top of the page. Adjust the numbers to fit your layout.*

---

## Step 4: Create the rectangle shape

```csharp
        // Create a rectangle shape with the defined bounds.
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            // Optional styling – a semi‑transparent blue fill.
            FillColor = Color.FromRgb(0, 120, 215),
            FillOpacity = 0.4,

            // Optional border – 2 pt thick, dark gray.
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };
```

*The `Rectangle` class inherits from `GraphicalObject`. Setting `FillColor` and `Border` is optional, but it demonstrates how to control appearance when you **how to draw shape in PDF C#** beyond a plain outline.*

---

## Step 5: Add the rectangle to the page

```csharp
        // Add the rectangle shape to the page's paragraph collection.
        firstPage.Paragraphs.Add(rectangleShape);
```

*Paragraphs are the container for any drawable object. By inserting the shape into `Paragraphs`, Aspose.Pdf renders it when the document is saved.*

---

## Step 6: Save the modified PDF

```csharp
        // Save the updated PDF to a new file.
        pdfDoc.Save("output.pdf");

        // Inform the user.
        Console.WriteLine("Rectangle added and saved to output.pdf");
    }
}
```

*Saving creates a new file so the original `input.pdf` remains unchanged. You can overwrite the source file by passing the same path, but keeping a backup is a best practice.*

---

## Full source code (runnable)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color struct

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document
        Document pdfDoc = new Document("input.pdf");

        // Step 2: Get the first page (pages are 1‑based)
        Page firstPage = pdfDoc.Pages[1];

        // Step 3: Define rectangle bounds (left, bottom, right, top)
        Rectangle bounds = new Rectangle(50, 700, 300, 800);

        // Step 4: Create a rectangle shape with optional styling
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            FillColor = Color.FromArgb(102, 0, 120, 215), // 40 % opacity blue
            FillOpacity = 0.4,
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };

        // Step 5: Add the rectangle shape to the page
        firstPage.Paragraphs.Add(rectangleShape);

        // Step 6: Save the modified PDF
        pdfDoc.Save("output.pdf");

        Console.WriteLine("Rectangle added to PDF successfully.");
    }
}
```

**Expected output** – Open `output.pdf` in any PDF viewer. You should see a blue‑filled rectangle near the top‑right corner of the first page, outlined with a dark gray border.

---

## How to draw shape in PDF C# on multiple pages

If you need to **add rectangle to PDF** on every page, loop through the `Pages` collection:

```csharp
foreach (Page page in pdfDoc.Pages)
{
    Rectangle rect = new Rectangle(50, 700, 300, 800);
    Rectangle shape = new Rectangle(rect)
    {
        FillColor = Color.FromArgb(80, 255, 0, 0), // semi‑transparent red
        Border = new Border { Width = 1, Color = Color.Black }
    };
    page.Paragraphs.Add(shape);
}
```

*This pattern reuses the same bounds on each page. Adjust the coordinates per page if you need different positions.*

---

## Common pitfalls and best‑practice tips

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| Rectangle appears off‑page | Coordinates are measured from the bottom‑left; using a top‑oriented coordinate system can cause confusion. | Remember that the Y‑axis grows upward. Use values that fit within the page size (`page.PageInfo.Width`, `page.PageInfo.Height`). |
| Shape is invisible | Fill opacity set to `0` or border width set to `0`. | Ensure `FillOpacity` is greater than `0` and `Border.Width` is at least `0.5`. |
| Saving throws `AccessDeniedException` | Output file is open in another program. | Close any viewers before running the code, or save to a different path. |
| Rectangle overlaps existing content | No layering control was set. | Use `ZIndex` property (higher values render on top) if you need to control layering. |

---

## Extending the rectangle – gradients, rotation, and transparency

Aspose.Pdf supports advanced graphics. To create a rotated rectangle with a linear gradient:

```csharp
Rectangle gradientRect = new Rectangle(bounds)
{
    // Gradient fill from left (blue) to right (green)
    FillColor = Color.Blue,
    FillColor2 = Color.Green,
    FillMode = FillMode.LinearGradient,
    // Rotate 45 degrees around the rectangle's center
    Rotation = 45
};
firstPage.Paragraphs.Add(gradientRect);
```

*The same code pattern demonstrates **how to draw shape in PDF C#** with richer visual effects.*

---

## Verify the result programmatically

You can confirm that the rectangle was added by checking the page’s paragraph count:

```csharp
int shapeCount = firstPage.Paragraphs.Count;
Console.WriteLine($"Page 1 now contains {shapeCount} paragraph objects.");
```

If the count increased by one after the insertion, the operation succeeded.

---

## Conclusion

You now know how to **add rectangle to PDF** files using C#. The tutorial covered loading a document, defining bounds, creating a rectangle shape, inserting it into a page, and saving the result. You also saw how to handle multiple pages, avoid common errors, and apply advanced styling.

Next, explore related topics such as **how to draw shape in PDF C#** for circles, polygons, or free‑form paths, and learn to combine shapes with text and images to build fully‑featured PDF reports.

Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds Guide](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)
- [How to Add an Image Stamp to a PDF Using Aspose.PDF for .NET: A Comprehensive Guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [How to Add a Rotating Image Watermark to PDFs Using Aspose.PDF for .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}