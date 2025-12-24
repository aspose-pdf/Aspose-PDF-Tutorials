---
category: general
date: 2025-12-23
description: Crop image in PDF using C# and Aspose.Pdf – learn how to create PDF from
  image, add image to PDF, and save PDF document in a few easy steps.
draft: false
keywords:
- crop image in pdf
- create pdf from image
- add image to pdf
- save pdf document
- convert jpg to pdf
language: en
og_description: Crop image in PDF using C# and Aspose.Pdf. This guide shows how to
  create PDF from image, add image to PDF, and save PDF document quickly.
og_title: Crop image in PDF with C# – Create PDF from Image, Add Image to PDF
tags:
- pdf
- csharp
- aspose
- image-processing
title: Crop image in PDF with C# – Create PDF from Image, Add Image to PDF, and Save
  PDF Document
url: /net/programming-with-images/crop-image-in-pdf-with-c-create-pdf-from-image-add-image-to/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crop image in PDF with C# – Complete Step‑by‑Step Guide

Ever needed to **crop image in PDF** but didn't know which API call would actually do the job? You're not alone. Many developers hit a wall when they try to trim a picture while converting a JPEG into a PDF, especially when they want only a specific quadrant of the original.  

In this tutorial we'll solve that problem together: you'll learn how to **create PDF from image**, place the picture on a page, apply a crop box, and finally **save PDF document** on disk. By the end you’ll also know how to **convert JPG to PDF** with the exact portion you need—no extra post‑processing required.

## What You'll Build

- A C# console application that reads `input.jpg` from a folder you specify.  
- A PDF file (`output.pdf`) that contains only the top‑left quarter of that JPEG.  
- A reusable pattern you can adapt to crop any region, change the image format, or generate multi‑page PDFs.

### Prerequisites

- .NET 6.0 or later (the code works on .NET Framework 4.7+ as well).  
- Aspose.Pdf for .NET installed via NuGet (`Install-Package Aspose.Pdf`).  
- Basic familiarity with C# syntax—if you can write a `Console.WriteLine`, you’re good to go.

> **Pro tip:** If you don’t have a license, Aspose.Pdf works in evaluation mode with a watermark; the API calls remain identical.

## Step 1: Set Up the Project and Import Namespaces

First things first—create a new console project and pull in the required namespaces. This step is the foundation for any **create PDF from image** workflow.

```csharp
using System;
using System.IO;
using Aspose.Pdf;          // Core Aspose.Pdf classes
using Aspose.Pdf.Text;    // For optional text handling
```

> *Why this matters:* Importing `Aspose.Pdf` gives you access to `Document`, `Page`, and `Rectangle`—the three building blocks you’ll use to **add image to PDF** and define a crop area.

## Step 2: Define Paths and Open the Source Image

Next, tell the program where to find the JPEG and where to drop the resulting PDF. Using a `FileStream` ensures the image is read in a read‑only, memory‑efficient way.

```csharp
// Step 2: Point to your working folder
string folderPath = @"C:\MyImages";   // <-- change this to your own folder

// Open the JPEG as a read‑only stream
using FileStream imageStream = File.OpenRead(Path.Combine(folderPath, "input.jpg"));
```

> *Edge case:* If the file doesn't exist, `File.OpenRead` throws a `FileNotFoundException`. In production code you might wrap this in a `try/catch` and log a friendly error.

## Step 3: Create a New PDF Document

Now we spin up a blank PDF. Think of this as an empty canvas where we’ll later **add image to PDF** and crop it.

```csharp
using Document pdfDocument = new Document();   // Auto‑disposable in C# 8+
```

> *Why we use `using`*: It guarantees that the underlying file handles are released as soon as we finish saving, preventing file‑lock issues on Windows.

## Step 4: Calculate the Full Image Rectangle and the Crop Box

Aspose.Pdf works with points (1 point = 1/72 inch). In the original snippet the rectangle starts at `(17.62, 65.25)` and stretches to `(602.62, 767.25)`. We'll keep those numbers, then compute a crop box that captures only the top‑left quarter.

```csharp
// Full image area on the PDF page (you can adjust these numbers)
Rectangle fullImageRect = new Rectangle(17.62, 65.25, 602.62, 767.25);

// Compute half‑width and half‑height for the top‑left quarter
double halfWidth  = fullImageRect.Width  / 2;
double halfHeight = fullImageRect.Height / 2;

// Crop box that shows only the top‑left quarter
Rectangle cropBox = new Rectangle(
    fullImageRect.LLX,                 // left (LLX)
    fullImageRect.LLY,                 // bottom (LLY)
    fullImageRect.LLX + halfWidth,    // right
    fullImageRect.LLY + halfHeight);  // top
```

> *Why a crop box?* The PDF spec distinguishes between the **MediaBox** (full page size) and the **CropBox** (visible region). By feeding both rectangles to `AddImage`, Aspose.Pdf draws the image at its full size but clips it to the CropBox you defined.

## Step 5: Add a Page and Place the Cropped Image

With our rectangles ready, we add a page to the document and insert the image. This is the moment where the **crop image in PDF** actually happens.

```csharp
// Add a new page to the PDF
Page pdfPage = pdfDocument.Pages.Add();

// Place the image using both the full rectangle and the crop box
pdfPage.AddImage(imageStream, fullImageRect, cropBox);
```

> *What if you need a different region?* Just change the coordinates when you build `cropBox`. For example, to get the bottom‑right quarter, start at `fullImageRect.LLX + halfWidth` and `fullImageRect.LLY`.

## Step 6: Save the PDF to Disk

Finally, we persist the result. This step completes the **save PDF document** portion of our guide.

```csharp
string outputPath = Path.Combine(folderPath, "output.pdf");
pdfDocument.Save(outputPath);

Console.WriteLine($"✅ PDF saved to: {outputPath}");
```

When you open `output.pdf` in any viewer, you’ll see only the top‑left quarter of `input.jpg` rendered at the size you specified in `fullImageRect`.

## Full Working Example

Putting it all together, here’s the complete program you can copy‑paste into `Program.cs` and run.

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Define folder and open the source image
        // -------------------------------------------------
        string folderPath = @"C:\MyImages"; // <-- update this path
        using FileStream imageStream = File.OpenRead(Path.Combine(folderPath, "input.jpg"));

        // -------------------------------------------------
        // Step 2: Create a new PDF document
        // -------------------------------------------------
        using Document pdfDocument = new Document();

        // -------------------------------------------------
        // Step 3: Define full image rectangle and crop box
        // -------------------------------------------------
        Rectangle fullImageRect = new Rectangle(17.62, 65.25, 602.62, 767.25);
        double halfWidth  = fullImageRect.Width  / 2;
        double halfHeight = fullImageRect.Height / 2;
        Rectangle cropBox = new Rectangle(
            fullImageRect.LLX,
            fullImageRect.LLY,
            fullImageRect.LLX + halfWidth,
            fullImageRect.LLY + halfHeight);

        // -------------------------------------------------
        // Step 4: Add a page and insert the cropped image
        // -------------------------------------------------
        Page pdfPage = pdfDocument.Pages.Add();
        pdfPage.AddImage(imageStream, fullImageRect, cropBox);

        // -------------------------------------------------
        // Step 5: Save the PDF (convert JPG to PDF)
        // -------------------------------------------------
        string outputPath = Path.Combine(folderPath, "output.pdf");
        pdfDocument.Save(outputPath);
        Console.WriteLine($"✅ PDF saved to: {outputPath}");
    }
}
```

### Expected Result

- **File created:** `output.pdf` in the same folder as `input.jpg`.  
- **Visual outcome:** The PDF page shows only the top‑left quarter of the original JPEG, scaled to fit the rectangle you defined.  
- **File size:** Typically a few hundred kilobytes, depending on JPEG compression.

## Frequently Asked Questions & Edge Cases

### Can I crop a different quadrant?

Absolutely. Change the `cropBox` coordinates. For the bottom‑right quarter:

```csharp
Rectangle cropBox = new Rectangle(
    fullImageRect.LLX + halfWidth,
    fullImageRect.LLY + halfHeight,
    fullImageRect.URX,
    fullImageRect.URY);
```

### What if my image is a PNG or BMP?

Aspose.Pdf supports any image format that .NET can read. Just replace `"input.jpg"` with `"input.png"` (or `.bmp`) and the same code works. No extra conversion step needed.

### How do I add multiple pages, each with a different crop?

Wrap the page‑creation logic in a loop. For each iteration create a new `Rectangle` for the crop box, add a fresh page, and call `AddImage`. Example:

```csharp
for (int i = 0; i < 4; i++)
{
    Page page = pdfDocument.Pages.Add();
    Rectangle box = GetCropBoxForQuadrant(i, fullImageRect);
    page.AddImage(imageStream, fullImageRect, box);
}
```

### What about high‑resolution images that exceed PDF page size?

You can either scale the `fullImageRect` to fit the page or set the PDF page size explicitly:

```csharp
pdfPage.PageInfo.Width = 595;   // A4 width in points
pdfPage.PageInfo.Height = 842;  // A4 height in points
```

Then adjust `fullImageRect` accordingly.

### Is there a way to remove the watermark in evaluation mode?

You need a commercial license from Aspose. Once you apply the license (`License license = new License(); license.SetLicense("Aspose.Pdf.lic");`) the watermark disappears and you can use the API without restrictions.

## Wrap‑Up

We’ve just walked through a complete, production‑ready example that **crop image in PDF** using C# and Aspose.Pdf. From opening

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}