---
category: general
date: 2025-12-22
description: Add image to pdf quickly with C#. This tutorial shows how to convert
  HEIC to PDF, create PDF from image, set PDF page size and save the PDF document
  in just a few steps.
draft: false
keywords:
- add image to pdf
- convert heic to pdf
- create pdf from image
- set pdf page size
- save pdf document
language: en
og_description: Add image to pdf with C#. Learn to convert HEIC to PDF, create PDF
  from image, set PDF page size, and save the PDF document efficiently.
og_title: Add image to pdf in C# – Full step‑by‑step guide
tags:
- C#
- Aspose.Pdf
- HEIC
- Document Generation
title: Add image to pdf in C# – Complete guide to convert HEIC, set page size & save
  document
url: /net/programming-with-images/add-image-to-pdf-in-c-complete-guide-to-convert-heic-set-pag/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add image to pdf in C# – Complete guide

Ever needed to **add image to pdf** but weren’t sure where to start? You’re not alone. Whether you’re processing photos from a mobile app or automating report generation, the ability to **convert HEIC to PDF** and control the final layout is a real game‑changer.

In this tutorial we’ll walk through a hands‑on solution that takes a HEIC file, extracts its raw pixels, sizes the PDF page to match the image, and finally **save pdf document** to disk. By the end you’ll have a single, runnable program you can drop into any .NET project. No fluff, just the exact steps you need.

We’ll also cover a few “what if” scenarios—like handling large images, tweaking DPI, or swapping out Aspose.Pdf for another library. All you need is a recent version of .NET (4.7+ or .NET 6) and the two NuGet packages shown below.

---

## Prerequisites

- **Aspose.Pdf for .NET** – provides the `Document`, `Page`, and `Image` classes.  
- **FileFormat.Heic** – a lightweight decoder that can read HEIC files into a byte buffer.  
- Visual Studio (or any C# editor) and basic familiarity with .NET streams.  

You can install the packages via the NuGet console:

```powershell
Install-Package Aspose.Pdf
Install-Package FileFormat.Heic
```

Once those are in place, we’re ready to dive in.

---

## Step 1: Load the HEIC file and extract raw pixels

The first thing we have to do is read the source image. The HEIC format isn’t natively supported by .NET, so we rely on `FileFormat.Heic` to decode it into a simple RGB24 byte array.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using FileFormat.Heic.Decoder;

class HeicToPdfConverter
{
    static void Main()
    {
        // Define input and output paths – adjust to your environment
        string inputFolder = @"YOUR_DIRECTORY\";
        string heicPath = Path.Combine(inputFolder, "HEICtoPDF.heic");
        string pdfPath  = Path.Combine(inputFolder, "HEICtoPDF_out.pdf");

        // Open a file stream for the HEIC image
        using (FileStream heicStream = new FileStream(heicPath, FileMode.Open, FileAccess.Read))
        {
            // Decode the HEIC image into an object we can query
            HeicImage heicImage = HeicImage.Load(heicStream);

            // Grab the raw pixel data in 24‑bit RGB format
            byte[] pixelData = heicImage.GetByteArray(PixelFormat.Rgb24);
            int width  = (int)heicImage.Width;
            int height = (int)heicImage.Height;

            // Continue to PDF creation...
```

> **Why this matters:** By pulling the pixel buffer directly we avoid any intermediate file writes, which keeps the conversion fast and memory‑friendly. The `Rgb24` format is the sweet spot for Aspose.Pdf’s `BitmapInfo` constructor.

---

## Step 2: **Add image to pdf** – create a PDF document and size the page

Now that we have the image data, we need a PDF canvas that matches its dimensions. This is where the **set pdf page size** keyword shines—if the page were larger or smaller, the image would be stretched or letterboxed.

```csharp
            // Create a new PDF document
            using (var pdfDoc = new Document())
            {
                // Add a fresh page; we’ll adjust its size to the image dimensions
                var page = pdfDoc.Pages.Add();
                page.PageInfo.Width  = width;   // width in points (1 point = 1/72 inch)
                page.PageInfo.Height = height;  // height in points

                // Build an Aspose.Pdf.Image from the raw pixel buffer
                var pdfImage = new Image
                {
                    BitmapInfo = new BitmapInfo(
                        pixelData, width, height, BitmapInfo.PixelFormat.Rgb24)
                };

                // Place the image onto the page
                page.Paragraphs.Add(pdfImage);

                // Finally, **save pdf document** to disk
                pdfDoc.Save(pdfPath);
            }
        }

        Console.WriteLine("✅ Conversion complete! PDF saved to: " + pdfPath);
    }
}
```

> **Key insight:** `PageInfo.Width` and `Height` accept values in points. Because we use the same pixel count for both the image and the page, the visual result is a 1:1 pixel‑to‑point mapping—no scaling, no distortion.

---

## Step 3: Verify the output and handle common edge cases

A quick sanity check is always worthwhile. Open the resulting PDF in any viewer; you should see the original HEIC image filling the page edge‑to‑edge.

### What if the image is huge?

If the source picture exceeds typical screen dimensions (e.g., a 6000 × 4000 photo), the PDF page will be equally large. Some viewers might struggle, and the file size can balloon. To mitigate this:

1. **Downscale before conversion** – use a library like `ImageSharp` to resize the pixel buffer.  
2. **Adjust DPI** – multiply width/height by a factor (e.g., 0.5) and set `page.PageInfo` accordingly; the visual size shrinks while the pixel data stays intact.

### What about transparency?

HEIC can contain an alpha channel, but `Rgb24` discards it. If you need to preserve transparency, switch to `PixelFormat.Rgba32` and use the corresponding `BitmapInfo.PixelFormat.Rgba32`. Keep in mind not all PDF viewers render alpha correctly.

---

## Step 4: Extend the solution – batch processing & alternative libraries

The pattern we just built scales nicely to batch jobs. Wrap the inner conversion logic in a method, loop over a directory, and you’ll have a **convert HEIC to PDF** pipeline in minutes.

```csharp
static void ConvertFolder(string folderPath)
{
    foreach (var file in Directory.GetFiles(folderPath, "*.heic"))
    {
        string outFile = Path.ChangeExtension(file, ".pdf");
        // Re‑use the conversion code from Main, passing file & outFile
        ConvertSingleHeicToPdf(file, outFile);
    }
}
```

If you prefer an open‑source PDF engine, `PdfSharpCore` can replace Aspose.Pdf. The only change is how you embed the image—`XImage.FromStream` works with a `MemoryStream` built from `pixelData`.

---

## Full source code (ready to copy)

Below is the complete, self‑contained program. Paste it into a new console app, restore NuGet packages, and hit **Run**.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using FileFormat.Heic.Decoder;

class HeicToPdfConverter
{
    static void Main()
    {
        string inputFolder = @"YOUR_DIRECTORY\";
        string heicPath = Path.Combine(inputFolder, "HEICtoPDF.heic");
        string pdfPath  = Path.Combine(inputFolder, "HEICtoPDF_out.pdf");

        using (FileStream heicStream = new FileStream(heicPath, FileMode.Open, FileAccess.Read))
        {
            // Load HEIC image
            HeicImage heicImage = HeicImage.Load(heicStream);
            byte[] pixelData = heicImage.GetByteArray(PixelFormat.Rgb24);
            int width  = (int)heicImage.Width;
            int height = (int)heicImage.Height;

            // Create PDF and set page size
            using (var pdfDoc = new Document())
            {
                var page = pdfDoc.Pages.Add();
                page.PageInfo.Width  = width;
                page.PageInfo.Height = height;

                // Build PDF image from raw bytes
                var pdfImage = new Image
                {
                    BitmapInfo = new BitmapInfo(
                        pixelData, width, height, BitmapInfo.PixelFormat.Rgb24)
                };

                page.Paragraphs.Add(pdfImage);
                pdfDoc.Save(pdfPath);
            }
        }

        Console.WriteLine("✅ Conversion complete! PDF saved to: " + pdfPath);
    }
}
```

> **Expected result:** A one‑page PDF named `HEICtoPDF_out.pdf` that displays the original HEIC picture without any scaling artifacts.

---

## Visual summary

![add image to pdf example](add-image-to-pdf.png "add image to pdf – HEIC conversion result")

*The screenshot shows the PDF opened in Adobe Reader, perfectly matching the source image dimensions.*

---

## Conclusion

You’ve just learned **how to add image to pdf** using C#, how to **convert HEIC to PDF**, how to **create PDF from image**, how to **set PDF page size** to the exact dimensions of the source, and finally how to **save PDF document** reliably. The code is compact, dependency‑light, and ready for production.

From here you might:

- Integrate the converter into a web API that accepts uploads.  
- Add compression options to shrink the final PDF size.  
- Swap the HEIC decoder for a multi‑format library if you need to support JPEG, PNG, or WebP as well.

Feel free to experiment—change the DPI, add multiple images per page, or even embed text captions. The sky’s the limit when you control the PDF generation pipeline yourself.

Got questions or a tricky edge case? Drop a comment below, and I’ll help you sort it out. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}