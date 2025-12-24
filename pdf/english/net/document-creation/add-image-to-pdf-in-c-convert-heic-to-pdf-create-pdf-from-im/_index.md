---
category: general
date: 2025-12-23
description: Add image to PDF in C# quickly – learn how to convert HEIC to PDF, create
  PDF from image, and set PDF page size in a few lines of code.
draft: false
keywords:
- add image to pdf
- convert heic to pdf
- create pdf from image
- set pdf page size
- how to convert heic to pdf
language: en
og_description: Add image to PDF in C# with step‑by‑step code. Convert HEIC to PDF,
  create PDF from image, and set PDF page size easily.
og_title: Add image to PDF in C# – Fast HEIC Conversion & Page Sizing
tags:
- aspnet
- csharp
- pdf-generation
title: Add image to PDF in C# – Convert HEIC to PDF, Create PDF from Image, and Set
  PDF Page Size
url: /net/document-creation/add-image-to-pdf-in-c-convert-heic-to-pdf-create-pdf-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add image to PDF in C# – Complete Guide

Add image to PDF in C# is a common task for many developers who need to embed pictures into reports, invoices, or e‑books. If you’ve ever wrestled with a HEIC photo and wondered how to convert it to a PDF without a heavyweight GUI, you’re in the right place.  

In this tutorial we’ll walk through the entire workflow: loading a HEIC file, extracting raw RGB24 data, creating a PDF page that exactly matches the image dimensions, and finally saving the result. By the end you’ll know **how to convert HEIC to PDF**, how to **create PDF from image**, and how to **set PDF page size** programmatically.

## What You’ll Need

- **.NET 6+** (the code works on .NET Framework 4.7+ as well)  
- **Aspose.Pdf for .NET** – a commercial library that supports bitmap‑based image insertion.  
- **FileFormat.Heic.Decoder** – a NuGet package that can read HEIC containers.  
- A basic C# IDE (Visual Studio, Rider, or VS Code).  

No additional tools, no external command‑line utilities. Just the two NuGet packages and a few lines of C#.

---

![add image to pdf example](image.png "add image to pdf example")

*Figure: The resulting PDF page perfectly matches the original HEIC image.*

## Step 1: Install the Required Packages

Open your project folder in a terminal and run:

```bash
dotnet add package Aspose.Pdf
dotnet add package FileFormat.Heic.Decoder
```

These commands pull the latest stable versions (as of December 2025) and add them to your `.csproj`. If you prefer the Package Manager Console inside Visual Studio, use `Install-Package Aspose.Pdf` and `Install-Package FileFormat.Heic.Decoder`.

## Step 2: Define File Paths and Load the HEIC Image

First we point the program at the source HEIC and decide where the PDF will land. Then we use the HEIC decoder to pull out raw pixel data.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Devices;
using FileFormat.Heic.Decoder;

class HeicToPdf
{
    static void Main()
    {
        // ---- 2.1: Set input and output locations ---------------------------------
        string inputHeicPath = @"C:\Images\sample.heic";
        string outputPdfPath = @"C:\Images\sample.pdf";

        // ---- 2.2: Load HEIC and get raw RGB24 bytes ------------------------------
        using (FileStream heicStream = new FileStream(inputHeicPath, FileMode.Open, FileAccess.Read))
        {
            // The HeicImage class handles decoding internally.
            HeicImage heicImage = HeicImage.Load(heicStream);

            // Extract pixel data in 24‑bit RGB format.
            byte[] pixelData = heicImage.GetByteArray(PixelFormat.Rgb24);

            // Image dimensions – we’ll reuse these for the PDF page size.
            int width  = (int)heicImage.Width;
            int height = (int)heicImage.Height;

            // ---- 2.3: Create the PDF and embed the image -------------------------
            CreatePdfFromRawPixels(pixelData, width, height, outputPdfPath);
        }
    }

    // Helper method kept separate for readability.
    private static void CreatePdfFromRawPixels(byte[] pixelData, int width, int height, string pdfPath)
    {
        // This method contains the core "add image to pdf" logic.
        using (Document pdfDocument = new Document())
        {
            // ---- 2.3.1: Add a page sized exactly to the image -----------------
            Page page = pdfDocument.Pages.Add();
            page.PageInfo.Width  = width;   // set pdf page size
            page.PageInfo.Height = height;  // matches the HEIC dimensions

            // ---- 2.3.2: Build an Aspose.Pdf.Image from the raw buffer ---------
            Image pdfImage = new Image
            {
                BitmapInfo = new BitmapInfo(
                    pixelData, width, height, BitmapInfo.PixelFormat.Rgb24)
            };

            // ---- 2.3.3: Place the image on the page ----------------------------
            page.Paragraphs.Add(pdfImage);

            // ---- 2.3.4: Save the document --------------------------------------
            pdfDocument.Save(pdfPath);
        }
    }
}
```

### Why This Works

- **Raw pixel buffer**: By feeding the RGB24 byte array directly into `BitmapInfo`, we avoid the overhead of writing a temporary PNG or JPEG.  
- **Exact page sizing**: Setting `page.PageInfo.Width/Height` to the image dimensions means the PDF page has no white margins – the image fills the page edge‑to‑edge. This satisfies the **set pdf page size** requirement.  
- **Single responsibility**: The helper method `CreatePdfFromRawPixels` isolates the PDF creation logic, making the code easier to test and reuse.

## Step 3: Run the Application and Verify the Output

Compile and run:

```bash
dotnet run --project HeicToPdf.csproj
```

If everything is wired correctly, you’ll find `sample.pdf` beside your HEIC file. Opening it in any PDF viewer should show a page that looks identical to the original photo—no distortion, no extra margins.

### Quick Validation Checklist

- ✅ The PDF page dimensions equal the HEIC width × height.  
- ✅ The image appears crisp (RGB24 preserves full color depth).  
- ✅ No temporary files are left on disk.  

If you notice a blank page, double‑check that `pixelData.Length` matches `width * height * 3`. A mismatch usually means the decoder returned a different pixel format; in that case, switch to `PixelFormat.Rgba32` and adjust the `BitmapInfo` accordingly.

## Step 4: Common Variations and Edge Cases

### Converting Multiple HEIC Files in a Batch

```csharp
string[] heicFiles = Directory.GetFiles(@"C:\Images", "*.heic");
foreach (var heicPath in heicFiles)
{
    string pdfPath = Path.ChangeExtension(heicPath, ".pdf");
    // Reuse the same loading/creation logic from Step 2.
}
```

### Handling Transparency

HEIC can contain an alpha channel. If you need to preserve transparency, decode to `PixelFormat.Rgba32` and use `BitmapInfo.PixelFormat.Rgba32`. Keep in mind that many PDF viewers flatten transparent layers against a white background.

### Setting DPI for High‑Resolution PDFs

If you want the PDF to report a specific DPI (dots per inch), adjust the page size like this:

```csharp
float dpi = 300f;
page.PageInfo.Width  = width  * 72f / dpi;   // 72 points = 1 inch
page.PageInfo.Height = height * 72f / dpi;
```

Now the image is scaled correctly for printing at 300 DPI.

## Pro Tips & Pitfalls

- **Pro tip:** Reuse a single `Document` instance when converting many images; it reduces memory churn.  
- **Watch out for:** Very large HEIC files (above 30 MP) can consume gigabytes of RAM when expanded to raw RGB24. In such cases, consider streaming the image in tiles instead of loading the whole buffer at once.  
- **Version check:** Aspose.Pdf 23.10+ introduced better support for bitmap images; using an older version may throw `NotSupportedException` for certain pixel formats.  

---

## Conclusion

You now have a complete, production‑ready solution for **add image to pdf** using C#. The tutorial covered everything from installing the right NuGet packages, **convert HEIC to PDF**, **create PDF from image**, and precisely **set PDF page size**. With just a few lines of code you can embed any HEIC (or other bitmap) into a PDF that matches the original dimensions, making the process fast and reliable.

What’s next? Try mixing multiple images on a single page, add text annotations with Aspose.Pdf’s `TextFragment`, or generate a multi‑page report that pulls images from a cloud storage bucket. The same principles apply, so you’re well‑equipped to expand this pattern.

Feel free to drop a comment if you hit any snags, or share how you adapted the code for your own project. Happy coding, and enjoy the simplicity of turning HEIC photos into polished PDFs!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}