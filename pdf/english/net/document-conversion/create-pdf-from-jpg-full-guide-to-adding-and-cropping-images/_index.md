---
category: general
date: 2025-12-25
description: Create PDF from JPG quickly using Aspose.PDF. Learn how to add image
  pdf page, crop image pdf, and create pdf with image programmatically.
draft: false
keywords:
- create pdf from jpg
- create pdf with image
- crop image pdf
- add image pdf page
- crop image programmatically
language: en
og_description: Create PDF from JPG in C# with Aspose.PDF. This tutorial shows how
  to add image pdf page, crop image pdf, and programmatically generate PDFs with images.
og_title: Create PDF from JPG – Step‑by‑Step Image Cropping Guide
tags:
- Aspose.PDF
- C#
- ImageProcessing
title: Create PDF from JPG – Full Guide to Adding and Cropping Images
url: /net/document-conversion/create-pdf-from-jpg-full-guide-to-adding-and-cropping-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create PDF from JPG – Full Guide to Adding and Cropping Images

Ever needed to **create PDF from JPG** but weren’t sure how to keep only the part of the picture you actually want? You’re not alone. Many developers hit that wall when they try to generate reports that include product photos, scanned forms, or screenshots. The good news is that with a few lines of C# and Aspose.PDF you can add an image to a PDF page, crop it on the fly, and save the result—all without touching Photoshop.

In this tutorial we’ll walk through everything you need to know to **create PDF with image**, **crop image pdf**, and even **add image pdf page** programmatically. By the end you’ll have a ready‑to‑run snippet that takes a JPEG, crops the top‑left quarter, and writes a brand‑new PDF file to disk. No external tools, no manual steps.

## What You’ll Learn

- How to set up the Aspose.PDF library in a .NET project.  
- The exact code required to **create PDF from JPG** while cropping it.  
- Why we calculate a *crop box* instead of resizing the image.  
- Common pitfalls such as coordinate systems and page size mismatches.  
- Tips for extending the solution to multiple pages or different crop regions.

> **Prerequisites** – You should have .NET 6+ (or .NET Framework 4.7+) installed, a basic understanding of C#, and access to the Aspose.PDF NuGet package. If you’re new to Aspose, just run `dotnet add package Aspose.PDF` and you’re good to go.

---

## Step 1 – Install Aspose.PDF and Prepare Your Project

First things first: you need the Aspose.PDF library. Open a terminal in your project folder and run:

```bash
dotnet add package Aspose.PDF
```

That single command pulls in all the assemblies you’ll need to **create PDF with image**. After the install, open your IDE (Visual Studio, Rider, or VS Code) and create a new C# console app if you don’t already have one:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
```

> **Pro tip:** Keep your `using` statements at the top; it makes the code easier to scan and helps AI models locate the dependencies quickly.

---

## Step 2 – Define Input/Output Paths and Load the JPEG

We’ll store the source JPG in a folder called `Images` inside the project’s root. The output PDF will land in the same directory for simplicity.

```csharp
// Step 2: Define the base directory for input and output files
string dataDir = Path.Combine(Directory.GetCurrentDirectory(), "Data");

// Ensure the directory exists
Directory.CreateDirectory(dataDir);

// Path to the source JPEG
string jpgPath = Path.Combine(dataDir, "Images", "Sample-01.jpg");

// Path for the resulting PDF
string pdfPath = Path.Combine(dataDir, "AddCroppedImageMender_out.pdf");
```

If the file isn’t there, the program will throw a `FileNotFoundException`. That’s intentional—better to fail fast than to generate an empty PDF.

---

## Step 3 – Create a New PDF Document and Open the Image Stream

Now we instantiate a fresh PDF document (think of it as a blank canvas) and open a read‑only stream to the JPEG. Using `using` statements guarantees that the file handles are released even if an exception occurs.

```csharp
// Step 3: Create a new PDF document and open the source image
using (var pdfDocument = new Document())
using (var imageStream = File.OpenRead(jpgPath))
{
    // The rest of the logic lives inside this block
```

At this point we have a `pdfDocument` object ready to receive pages, and `imageStream` points to the raw bytes of our JPG.

---

## Step 4 – Calculate the Full Image Rectangle and the Crop Box

Aspose.PDF works with points (1 point = 1/72 inch). The `Rectangle` class defines the area where the image will be placed on the page. In this example we use a rectangle that roughly matches an A4‑sized page, but you can adjust the numbers to fit your layout.

```csharp
    // Step 4: Define the rectangle that represents the full image area on the page
    var fullRect = new Rectangle(17.62, 65.25, 602.62, 767.25);

    // Calculate a smaller rectangle (crop box) that keeps only the top‑left quarter
    double halfWidth = fullRect.Width / 2;
    double halfHeight = fullRect.Height / 2;
    var cropBox = new Rectangle(
        fullRect.LLX,
        fullRect.LLY,
        fullRect.LLX + halfWidth,
        fullRect.LLY + halfHeight);
```

Why do we need a *crop box*? The `AddImage` overload we’ll use accepts both the destination rectangle (`fullRect`) and a source rectangle (`cropBox`). The source rectangle tells Aspose which part of the JPEG to copy—effectively cropping the image without creating a temporary file.

> **Note:** The coordinate system starts at the lower‑left corner. If you’re used to top‑left origin (like in WinForms), you’ll need to flip the Y‑axis yourself.

---

## Step 5 – Add a New Page and Place the Cropped Image

With the geometry ready, we add a fresh page to the PDF and drop the cropped image onto it. The `AddImage` method does the heavy lifting: it reads the bytes from `imageStream`, extracts the region defined by `cropBox`, scales it to `fullRect`, and embeds it.

```csharp
    // Step 5: Add a new page and place the cropped image onto it
    var page = pdfDocument.Pages.Add();
    page.AddImage(imageStream, fullRect, cropBox);
```

If you ever need to add **multiple images** on the same page, just call `page.AddImage` again with a different `fullRect`. The same `cropBox` logic can be reused for each picture.

---

## Step 6 – Save the PDF and Verify the Result

Finally, we persist the document to disk. The `Save` method writes a fully‑compliant PDF that any viewer (Adobe Reader, Chrome, etc.) can open.

```csharp
    // Step 6: Save the resulting PDF
    pdfDocument.Save(pdfPath);
}
```

When you run the program, you should see `AddCroppedImageMender_out.pdf` inside the `Data` folder. Opening it will reveal a single page where only the top‑left quarter of `Sample-01.jpg` is visible—exactly what our **crop image pdf** logic intended.

---

## Full Working Example (Copy‑Paste Ready)

Below is the complete, self‑contained program. Paste it into `Program.cs`, adjust the `dataDir` path if you like, and hit **Run**.

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // Step 1: Define the base directory for input and output files
        string dataDir = Path.Combine(Directory.GetCurrentDirectory(), "Data");
        Directory.CreateDirectory(dataDir);

        // Paths
        string jpgPath = Path.Combine(dataDir, "Images", "Sample-01.jpg");
        string pdfPath = Path.Combine(dataDir, "AddCroppedImageMender_out.pdf");

        // Verify source image exists
        if (!File.Exists(jpgPath))
        {
            Console.WriteLine($"Source image not found: {jpgPath}");
            return;
        }

        // Step 2‑6: Create PDF, crop image, and save
        using (var pdfDocument = new Document())
        using (var imageStream = File.OpenRead(jpgPath))
        {
            // Full rectangle (page area where the image will be placed)
            var fullRect = new Rectangle(17.62, 65.25, 602.62, 767.25);

            // Crop box – keep top‑left quarter
            double halfWidth = fullRect.Width / 2;
            double halfHeight = fullRect.Height / 2;
            var cropBox = new Rectangle(
                fullRect.LLX,
                fullRect.LLY,
                fullRect.LLX + halfWidth,
                fullRect.LLY + halfHeight);

            // Add a page and the cropped image
            var page = pdfDocument.Pages.Add();
            page.AddImage(imageStream, fullRect, cropBox);

            // Save the PDF
            pdfDocument.Save(pdfPath);
        }

        Console.WriteLine($"PDF created successfully: {pdfPath}");
    }
}
```

**Expected output:**  

```
PDF created successfully: C:\YourProject\Data\AddCroppedImageMender_out.pdf
```

Open the PDF and you’ll see the cropped portion of the original JPEG occupying the page.

---

## Frequently Asked Questions (FAQ)

### 1. Can I crop a different region (e.g., bottom‑right)?
Absolutely. Just adjust the `cropBox` coordinates. For bottom‑right, start from `fullRect.URX - halfWidth` and `fullRect.URY - halfHeight`.

### 2. Does this work with PNG or BMP files?
Yes. `AddImage` accepts any format that Aspose.PDF can decode, which includes PNG, BMP, GIF, and even multi‑page TIFFs.

### 3. What if I need to *scale* the image instead of cropping?
Replace the `cropBox` with `fullRect` for both parameters, then set the `ImageScale` property on the `Image` object (or adjust `fullRect` dimensions).

### 4. How do I add **multiple images** on separate pages?
Loop over your image collection, call `pdfDocument.Pages.Add()` for each iteration, and repeat the `AddImage` call with a fresh `fullRect` each time.

### 5. Is there a way to **add image pdf page** without cropping?
Sure—just omit the `cropBox` argument and use the overload `page.AddImage(imageStream, fullRect)`.

---

## Extending the Solution

- **Dynamic page size:** Use `page.SetPageSize(PageSize.A4.Width, PageSize.A4.Height)` before adding the image.  
- **Metadata:** Set `pdfDocument.Info.Title = "Cropped Image PDF"` to improve searchability.  
- **Encryption:** Call `pdfDocument.Encrypt("ownerPwd", "userPwd", EncryptionAlgorithms.RC4_128)` if you need to protect the file.  

All of these tweaks keep the core idea of **create PDF from JPG** intact while giving you a production‑ready toolkit.

---

## Conclusion

We’ve just shown you how to **create PDF from JPG**, **add image pdf page**, and **crop image pdf** using Aspose.PDF in a clean, single‑file C# program. The key takeaways are:

- Use a *full rectangle* for placement and a *crop box* for the region you actually want.  
- The `AddImage` overload that accepts both rectangles does the cropping for you—no extra image‑processing library required.  
- The same pattern scales to multiple pages, different image formats, and even encrypted PDFs.

Now that you’ve mastered the basics, try swapping the crop region, stacking several images, or generating a multi‑page

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}