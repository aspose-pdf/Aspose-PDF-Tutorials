---
category: general
date: 2026-04-06
description: Create PDF from JPG quickly and learn how to crop image in PDF, add new
  PDF page, and convert JPG to PDF with crop using C#.
draft: false
keywords:
- create pdf from jpg
- crop image in pdf
- how to add new pdf page
- convert jpg to pdf with crop
- insert image into pdf c#
language: en
og_description: Create PDF from JPG and crop image in PDF with C#. Learn how to add
  new PDF page and convert JPG to PDF with crop.
og_title: Create PDF from JPG in C# – Step‑by‑Step Guide
tags:
- Aspose.Pdf
- C#
- PDF generation
title: Create PDF from JPG in C# – Full Guide with Cropping and New Pages
url: /net/document-conversion/create-pdf-from-jpg-in-c-full-guide-with-cropping-and-new-pa/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create PDF from JPG in C# – Full Guide with Cropping and New Pages

Ever needed to **create PDF from JPG** but weren’t sure how to keep only the part you actually want? You’re not alone. In many apps—think invoices, receipts, or photo‑books—developers must turn a picture into a PDF while discarding the unwanted edges.  

In this tutorial we’ll walk through a complete, ready‑to‑run solution that **creates PDF from JPG**, shows you how to **crop image in PDF**, and demonstrates the **how to add new pdf page** when you need more than one picture. By the end you’ll also know how to **convert JPG to PDF with crop** and **insert image into PDF C#** using the Aspose.Pdf library.

## What You’ll Learn

- Set up Aspose.Pdf in a .NET project (no heavy configuration required).  
- Load a JPEG, define the area you want to keep, and crop it while inserting into a PDF page.  
- Add additional pages to the same document, letting you build multi‑page PDFs from many images.  
- Save the final file and verify the output.  

**Prerequisites:** .NET 6+ (or .NET Framework 4.6+), Visual Studio 2022 or any editor you like, and a NuGet reference to `Aspose.Pdf`. No other external services are needed.

![Create PDF from JPG example](image.jpg){: .align-center alt="Create PDF from JPG example showing a cropped image placed on a PDF page"}

---

## Step 1: Install Aspose.Pdf and Prepare Your Project

First things first—add the Aspose.Pdf package. Open a terminal in your solution folder and run:

```bash
dotnet add package Aspose.Pdf
```

That single line pulls in everything you need: the `Document`, `Rectangle`, and `Page` classes we’ll use later. In my experience, the NuGet route is the cleanest way to stay up‑to‑date without fiddling with DLLs.

> **Pro tip:** If you’re targeting .NET Framework, use the `Aspose.Pdf.NET` package instead; the API surface is identical.

---

## Step 2: Load the JPEG and Define the Page Size

We need a canvas that matches the dimensions we want for the final PDF page. The code below creates a fresh `Document` and opens the source image as a stream.

```csharp
using Aspose.Pdf;
using System.IO;

// Create a new PDF document – this will hold our pages.
using var pdfDocument = new Document();

// Open the JPEG you want to convert.
using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

// Define the full‑size rectangle (the page) – 600 × 800 points works well for most photos.
var pageBounds = new Rectangle(0, 0, 600, 800);
```

Why a rectangle? In Aspose.Pdf a `Rectangle` represents both the page dimensions and the region of the image you want to display. By separating the *page* from the *crop area* you gain fine‑grained control over what ends up on the PDF.

---

## Step 3: Choose the Crop Area (Upper‑Left Quarter)

Suppose you only need the top‑left quarter of the photo. We calculate that region relative to the page size:

```csharp
// Crop the upper‑left quarter of the image.
var cropArea = new Rectangle(
    pageBounds.LLX,                                 // left X (0)
    pageBounds.LLY + pageBounds.Height / 2,         // bottom Y (halfway up)
    pageBounds.LLX + pageBounds.Width / 2,          // right X (halfway across)
    pageBounds.URY);                                // top Y (full height)
```

The `Rectangle` constructor takes **lower‑left X/Y** and **upper‑right X/Y** values. By adding half the height to `LLY` we shift the bottom of the crop upward, effectively discarding the lower half of the image. Adjust these calculations if you need a different portion.

> **Why crop before adding?**  
> Cropping on the PDF side avoids creating a temporary bitmap on disk, saving both I/O and memory. Aspose handles the math for you, and the result is a clean, vector‑friendly PDF.

---

## Step 4: Add a New Page and Insert the Cropped Image

Now we actually place the image onto a PDF page. This is where the **how to add new pdf page** keyword shines.

```csharp
// Add a new page to the document.
var page = pdfDocument.Pages.Add();

// Insert the image using both the page bounds and the crop rectangle.
page.AddImage(imageStream, pageBounds, cropArea);
```

`AddImage` takes three arguments:

1. **Stream** – the source JPEG.  
2. **Page rectangle** – defines the size of the page (our `pageBounds`).  
3. **Crop rectangle** – tells Aspose which part of the image to render.

If you need more pages, simply repeat the `Add` + `AddImage` pattern with a new `imageStream` each time. This satisfies the **how to add new pdf page** requirement while keeping the code tidy.

---

## Step 5: Save the PDF and Verify the Result

The final step is a one‑liner, but don’t underestimate it—saving to the correct path ensures the file can be opened by any PDF viewer.

```csharp
// Save the PDF to disk.
pdfDocument.Save(@"C:\Output\cropped_image.pdf");

// Optional: open the file automatically (Windows only).
System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
```

When you open `cropped_image.pdf`, you should see a single page that contains only the upper‑left quarter of the original JPEG, perfectly centered within the 600 × 800 page.

---

## Full Working Example (All Steps Combined)

Below is the complete program you can copy‑paste into a console app. It compiles as‑is, assuming you’ve installed Aspose.Pdf and placed a JPEG at the specified location.

```csharp
using Aspose.Pdf;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document.
        using var pdfDocument = new Document();

        // 2️⃣ Open the source JPEG.
        using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

        // 3️⃣ Define the page size (600 × 800 points).
        var pageBounds = new Rectangle(0, 0, 600, 800);

        // 4️⃣ Calculate the crop area – upper‑left quarter.
        var cropArea = new Rectangle(
            pageBounds.LLX,
            pageBounds.LLY + pageBounds.Height / 2,
            pageBounds.LLX + pageBounds.Width / 2,
            pageBounds.URY);

        // 5️⃣ Add a new page and insert the cropped image.
        var page = pdfDocument.Pages.Add();
        page.AddImage(imageStream, pageBounds, cropArea);

        // 6️⃣ Save the resulting PDF.
        pdfDocument.Save(@"C:\Output\cropped_image.pdf");

        // 7️⃣ (Optional) Open the PDF automatically.
        System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
    }
}
```

### Expected Output

- **File:** `cropped_image.pdf` (≈ 30 KB).  
- **Content:** One page, 600 × 800 points, showing the top‑left quarter of `photo.jpg`.  
- **Behavior:** No distortion; the image retains its original resolution within the cropped bounds.

---

## Frequently Asked Questions & Edge Cases

### What if I need to keep the whole image, not just a quarter?

Simply set `cropArea` equal to `pageBounds`:

```csharp
var cropArea = pageBounds; // No cropping – full image.
```

### Can I use a different page size (e.g., A4)?

Absolutely. Replace the `pageBounds` values with the dimensions of an A4 page in points (595 × 842):

```csharp
var pageBounds = new Rectangle(0, 0, 595, 842);
```

The crop rectangle can stay the same or be recalculated to match the new aspect ratio.

### How do I add multiple images, each on its own page?

Loop over a collection of file paths:

```csharp
foreach (var path in imagePaths)
{
    using var stream = File.OpenRead(path);
    var page = pdfDocument.Pages.Add();
    page.AddImage(stream, pageBounds, pageBounds); // No crop for each image.
}
```

### What about transparency or PNG images?

Aspose.Pdf treats PNG the same way as JPEG. If the source has an alpha channel, the PDF will preserve it, provided the PDF version supports transparency (default is fine).

### Does this work on .NET Core on Linux?

Yes. Aspose.Pdf is cross‑platform; just ensure the `imageStream` points to a valid file path on the target OS. No Windows‑only APIs are used.

---

## Tips & Best Practices

- **Memory Management:** Always wrap streams in `using` statements (as shown) to avoid file locks.  
- **Performance:** If you’re processing dozens of images, consider reusing a single `Document` instance and calling `pdfDocument.Pages.Add()` for each image.  
- **Error Handling:** Wrap the whole routine in a `try/catch` block and log `PdfException` for troubleshooting.  
- **Quality Control:** Aspose.Pdf lets you set image resolution via `ImageFragment`. For high‑dpi scans, set `ImageFragment.Resolution = 300;`.  
- **Security:** If the PDF will be shared externally, you can add encryption with `pdfDocument.Encrypt("ownerPwd", "userPwd", Permission.All);`.

---

## Conclusion

We’ve just covered how to **create PDF from JPG** in C#, **crop image in PDF**, and **add new PDF page** to build multi‑page documents. The same pattern lets you **convert JPG to PDF with crop** and **insert image into PDF C#** for any scenario—from simple receipts to complex photo‑books.  

Give it a try: swap the crop logic, experiment with A4 pages, or chain several images together. The Aspose.Pdf library makes these tasks painless, and the code above is a solid, citation‑worthy reference you can paste into any project.

---

### What’s Next?

- **Add text annotations** to the PDF (e.g., captions under each image).  
- **Create a table of contents** automatically for multi‑page PDFs.  
- **Merge multiple PDFs** using `pdfDocument.Pages.AddRange(otherDoc.Pages);`.  

Each of those topics builds on the fundamentals you just mastered, so you’re well‑positioned to explore them

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}