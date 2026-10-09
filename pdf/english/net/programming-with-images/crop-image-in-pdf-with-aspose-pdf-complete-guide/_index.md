---
category: general
date: 2026-06-08
description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
  image, save PDF with image, and add image to PDF in just a few lines.
draft: false
keywords:
- crop image in pdf
- create pdf with image
- save pdf with image
- how to add image to pdf
- how to crop image pdf
language: en
og_description: Crop image in PDF using Aspose.PDF in C#. This tutorial shows how
  to create PDF with image, save PDF with image, and add image to PDF quickly.
og_title: Crop Image in PDF with Aspose.PDF – Complete Guide
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  headline: Crop Image in PDF with Aspose.PDF – Complete Guide
  type: TechArticle
- description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  name: Crop Image in PDF with Aspose.PDF – Complete Guide
  steps:
  - name: '**Image stream** – the raw bytes of your picture.'
    text: '**Image stream** – the raw bytes of your picture.'
  - name: '**Placement rectangle** – where on the page the image lives.'
    text: '**Placement rectangle** – where on the page the image lives.'
  - name: '**Crop rectangle** – the portion of the image you actually want to render.'
    text: '**Crop rectangle** – the portion of the image you actually want to render.'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
- Image processing
title: Crop Image in PDF with Aspose.PDF – Complete Guide
url: /net/programming-with-images/crop-image-in-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crop Image in PDF with Aspose.PDF – Complete Guide

Ever wondered how to **crop image in PDF** without pulling out a graphics editor? You're not the only one. In many reports, invoices, or e‑books you need just a slice of a picture—maybe the logo corner or a chart fragment—and you want it straight inside the PDF.  

This guide shows you exactly that: we’ll **create PDF with image**, **add image to PDF**, and then **crop image in PDF** using the Aspose.PDF library for C#. By the end you’ll also know how to **save PDF with image** so you can ship the file to anyone.

---

## What You’ll Need

- .NET 6.0 or later (the code works with .NET Framework 4.6+ as well)  
- A licensed or trial copy of **Aspose.PDF for .NET** (install via NuGet `Install-Package Aspose.PDF`)  
- An image file (JPEG/PNG) on disk – we’ll call it `image.jpg`  
- Any IDE you like (Visual Studio, Rider, VS Code)

That’s it. No extra services, no external tools.

---

## Step 1: Set Up the Project and Imports

First, spin up a console app and bring in the namespaces we’ll use. The `using` statements keep the code tidy and make the later steps easier to read.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;   // for text fragments if you want captions later
```

> **Pro tip:** If you’re using Visual Studio, right‑click the project → *Manage NuGet Packages* → search “Aspose.PDF” and install. The library handles both image placement and cropping internally, so you won’t need any third‑party image libs.

---

## Step 2: Create PDF with Image

Now we actually **create pdf with image**. The snippet below builds a fresh `Document`, adds a blank page, and prepares an image stream.

```csharp
// Initialize a new PDF document
Document pdf = new Document();

// Add a blank page – think of it as a clean canvas
Page page = pdf.Pages.Add();

// Open the source image file
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // We'll place the whole image first; cropping comes next
    // Define where the image should sit on the page (in points; 1 point = 1/72 inch)
    Rectangle placement = new Rectangle(0, 0, 600, 800); // width=600pt, height=800pt

    // Add the image without cropping yet – just to see the full picture
    page.AddImage(imgStream, placement);
}
```

Running this code will give you a PDF with the entire picture stretched to the dimensions you specified. It’s a good sanity check before you start trimming.

---

## Step 3: How to Add Image to PDF (and Prepare for Cropping)

If you already know the exact region you want, you can skip the full‑size step and go straight to the **how to add image to pdf** part. The `AddImage` method accepts three parameters:

1. **Image stream** – the raw bytes of your picture.  
2. **Placement rectangle** – where on the page the image lives.  
3. **Crop rectangle** – the portion of the image you actually want to render.

Below is the compact version that does both placement **and** cropping in one call.

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Full‑size placement rectangle (you can adjust X/Y if you need margins)
    Rectangle placement = new Rectangle(0, 0, 600, 800);

    // Crop area: upper‑left quarter of the original image
    Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

    // This single line both adds the image and crops it
    page.AddImage(imgStream, placement, crop);
}
```

> **Why this works:** Aspose.PDF internally maps the crop rectangle to the image’s pixel dimensions, then renders only that slice inside the `placement` area. No extra bitmap processing required, which means you keep the PDF size small.

---

## Step 4: How to Crop Image PDF – Advanced Options

Sometimes the quarter‑crop isn’t enough. Maybe you need a custom rectangle or you want to preserve the image’s aspect ratio. Here’s a more flexible approach:

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Placement on the page (centered, 300pt wide, keep original height)
    Rectangle placement = new Rectangle(150, 400, 450, 1200);

    // Suppose you want a 200 × 150 pixel region starting at (50, 30) in the source image
    // First, convert pixel coordinates to points (assuming 72 DPI)
    float dpi = 72f;
    float left   = 50  / dpi * 72; // = 50 points
    float bottom = 30  / dpi * 72; // = 30 points
    float width  = 200 / dpi * 72; // = 200 points
    float height = 150 / dpi * 72; // = 150 points

    Rectangle crop = new Rectangle(left, bottom, left + width, bottom + height);

    page.AddImage(imgStream, placement, crop);
}
```

**Edge case handling:**  
- **Null streams** – always wrap the `FileStream` in a `using` block, as shown, to avoid leaks.  
- **Large images** – if the source image is huge, consider scaling the `placement` rectangle down; Aspose will downsample automatically.  
- **Transparent PNGs** – the library respects alpha channels, so your cropped area will keep transparency.

---

## Step 5: Save PDF with Image (and Verify)

Finally, we **save pdf with image**. The `Save` method writes the document to disk. You can also stream it back to a web client if you’re building an API.

```csharp
// Save the final PDF to the output folder
pdf.Save("YOUR_DIRECTORY/output.pdf");

// Optional: Open the file automatically (only works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/output.pdf",
    UseShellExecute = true
});
```

When you open `output.pdf`, you should see only the cropped portion of `image.jpg` positioned exactly where you defined it. If the image looks stretched, adjust the `placement` rectangle’s width/height to match the aspect ratio of the crop rectangle.

---

## Common Questions & Gotchas

| Question | Answer |
|----------|--------|
| **Can I crop multiple images on the same page?** | Absolutely. Call `page.AddImage` for each image with its own placement and crop rectangles. |
| **What if my image is in a different format (e.g., BMP)?** | Aspose.PDF supports JPEG, PNG, BMP, GIF, and TIFF out of the box. Just change the file extension. |
| **Do I need a license for production use?** | A trial works for up to 5 pages. For real deployments, purchase a license to remove the watermark. |
| **How do I rotate the cropped image?** | After adding the image, retrieve the `Image` object and set its `Rotate` property (`Rotate = RotationAngle.Rotate90`). |
| **Is there a way to crop using percentages instead of absolute points?** | Yes—calculate the rectangle dimensions based on `image.Width * 0.25` etc., then convert to points as shown in Step 4. |

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using System;
using System.IO;
using Aspose.Pdf;

namespace CropImageInPdfDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new PDF document and add a blank page
            Document pdf = new Document();
            Page page = pdf.Pages.Add();

            // 2️⃣ Open the image that will be placed on the page
            using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
            {
                // 3️⃣ Define where the image will sit on the page (points)
                Rectangle placement = new Rectangle(0, 0, 600, 800);

                // 4️⃣ Define the crop area – upper‑left quarter of the image
                Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

                // 5️⃣ Add the image using both placement and crop rectangles
                page.AddImage(imgStream, placement, crop);
            }

            // (Optional) Save the PDF to verify the result
            pdf.Save("YOUR_DIRECTORY/output.pdf");

            Console.WriteLine("PDF created and image cropped successfully!");
        }
    }
}
```

Run the program, open `output.pdf`, and you’ll see only the top‑left quarter of `image.jpg` rendered at the top‑left corner of the page. Change the `crop` rectangle values to experiment with different slices.

---

## Conclusion

We’ve walked through the entire process of **crop image in pdf** using Aspose.PDF for C#. Starting from a fresh document, we **create pdf with image**, demonstrate the **how to add image to pdf**, apply a custom **how to crop image pdf** rectangle, and finally **save pdf with image**.  

Now you can embed precisely‑cropped pictures into any PDF you generate—perfect for invoices, marketing brochures, or automated reports. Next up, consider adding text captions (`TextFragment`) or drawing shapes around the cropped image to highlight it further.  

Got more scenarios you’re curious about? Drop a comment, and happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Set Image Size in a PDF Using Aspose.PDF for .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [How to Add an Image Stamp to a PDF Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [How to Extract Image Information from PDFs Using Aspose.PDF for .NET](/pdf/english/net/images-graphics/extract-image-info-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}