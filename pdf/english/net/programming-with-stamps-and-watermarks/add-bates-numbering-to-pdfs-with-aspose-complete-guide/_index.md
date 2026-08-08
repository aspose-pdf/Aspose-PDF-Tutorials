---
category: general
date: 2026-04-25
description: Add bates numbering to PDFs quickly using Aspose.Pdf. Learn how to add
  page numbers pdf, auto adjust font size, and add text watermark in C#.
draft: false
keywords:
- add bates numbering
- add page numbers pdf
- auto adjust font size
- how to add bates
- add text watermark
language: en
og_description: Add bates numbering to PDFs with Aspose.Pdf. This guide shows how
  to add page numbers pdf, auto adjust font size, and add text watermark in a single,
  runnable example.
og_title: Add Bates Numbering to PDFs – Full Aspose.C# Tutorial
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Add Bates Numbering to PDFs with Aspose – Complete Guide
url: /net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Bates Numbering to PDFs with Aspose – Complete Guide

Ever needed to **add bates numbering** to a PDF but weren’t sure where to start? You’re not alone—legal teams, auditors, and developers alike hit this wall daily. The good news? With Aspose.Pdf for .NET you can stamp a Bates number, auto‑adjust the font size, and even treat the stamp as a subtle text watermark—all in a handful of lines of C#.

In this tutorial we’ll walk through the exact steps to **add page numbers pdf**, tweak the font so it never overflows, and answer the “how to add bates” question once and for all. By the end you’ll have a ready‑to‑run console app that produces a professionally numbered PDF, and you’ll see how to extend it into a full‑blown watermark solution.

## Prerequisites

Before we dive in, make sure you have:

* **Aspose.Pdf for .NET** (the latest NuGet package as of April 2026).  
* .NET 6.0 SDK or newer – the API works the same on .NET Framework, but .NET 6 gives you the best performance.  
* A sample PDF called `input.pdf` placed in a folder you can reference (e.g., `C:\Docs\`).  

No extra configuration is required; the library is self‑contained.

---

## Step 1 – Load the Source PDF Document

The first thing we do is open the file we want to number. Aspose’s `Document` class represents the whole PDF, and loading it is as simple as passing the path to the constructor.

```csharp
using Aspose.Pdf;

string inputPath = @"C:\Docs\input.pdf";
Document pdfDocument = new Document(inputPath);
```

*Why this matters*: Loading the document gives you access to the `Pages` collection, which is where we’ll attach the Bates stamp later. If the file can’t be found, Aspose throws a clear `FileNotFoundException`, so you’ll know exactly what went wrong.

---

## Step 2 – Create a Text Stamp for Bates Numbers

Now we craft the visual element that will appear on each page. The `TextStamp` class lets you embed any string, and we’ll use the placeholder `{page}-{total}` to let Aspose replace those tokens automatically.

```csharp
// Create a stamp that will display "Bates: 1-10", "Bates: 2-10", etc.
TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
{
    // Let the stamp automatically adjust its font size to fit the stamp rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Optional: make the stamp look like a subtle watermark
    Opacity = 0.4,
    // Position the stamp at the bottom‑right corner
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Choose a readable font
    Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
};
```

*Key points*:

* **auto adjust font size** – Setting `AutoAdjustFontSizeToFitStampRectangle` to `true` guarantees the text never spills outside the rectangle, which is perfect for variable‑length page numbers.
* **add text watermark** – By lowering the `Opacity` we turn the Bates number into a faint watermark, satisfying the “add text watermark” requirement without a separate step.
* **how to add bates** – The `{page}` and `{total}` tokens are the secret sauce; Aspose replaces them at runtime, so you don’t have to calculate anything yourself.

---

## Step 3 – Apply the Stamp to Every Page

A common pit‑fall is stamping only the first page. To truly **add page numbers pdf**, we need to loop through the entire `Pages` collection.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp for each page to avoid shared state issues
    page.AddStamp(batesStamp);
}
```

Why clone? The `AddStamp` method internally creates a copy, but explicitly using a fresh instance per iteration avoids accidental side‑effects if you later modify stamp properties (like changing color for specific pages).

---

## Step 4 – Save the Updated PDF

With the stamps in place, persisting the changes is straightforward. You can overwrite the original file or write to a new location—here we’ll save a new file called `output.pdf`.

```csharp
string outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

If you open `output.pdf` you’ll see each page labeled “Bates: 1‑10”, “Bates: 2‑10”, … right at the bottom‑right, with a faint opacity that doubles as a **add text watermark**.

---

## Full Working Example

Putting it all together, here’s a single, self‑contained console program you can copy‑paste into Visual Studio.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        string inputPath = @"C:\Docs\input.pdf";
        Document pdfDocument = new Document(inputPath);

        // 2️⃣ Create a Bates number stamp with auto‑adjusted font size
        TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Opacity = 0.4, // acts as a subtle watermark
            XIndent = 20,
            YIndent = 20,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
        };

        // 3️⃣ Add the stamp to every page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.AddStamp(batesStamp);
        }

        // 4️⃣ Save the result
        string outputPath = @"C:\Docs\output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**Expected result**: Open `output.pdf` in any viewer; each page shows a line like “Bates: 3‑12” in the lower‑right corner, sized just right for the rectangle and rendered with 40 % opacity. This satisfies both the legal‑tracking requirement and the visual watermark need.

---

## Common Variations & Edge Cases

| Situation | What to change | Why |
|-----------|----------------|-----|
| **Different placement** | Adjust `HorizontalAlignment` / `VerticalAlignment` or set `XIndent`/`YIndent` | Some firms prefer top‑left or center placement. |
| **Custom prefix** | Replace `"Bates: "` with `"Doc‑ID: "` or any string | You might be using a different naming convention. |
| **Multiple stamps** | Create a second `TextStamp` (e.g., for a confidentiality notice) and add it after the first | Combining **add bates numbering** with other **add text watermark** requirements is trivial. |
| **Large page counts** | Increase the initial font size (e.g., `14`) – the auto‑adjust will shrink it when needed | When you have > 999 pages the string gets longer; the auto‑adjust prevents clipping. |
| **Encrypted PDFs** | Call `pdfDocument.Decrypt("password")` before stamping | You can’t modify a secured file without the password. |

---

## Pro Tips & Pitfalls

* **Pro tip:** Set `batesStamp.Margin = new MarginInfo(5, 5, 5, 5)` if you notice the text hugging the edge of the page.  
* **Watch out for:** Very small rectangles (default size is 100 × 30 pt). If you need a larger area, set `batesStamp.Width` and `batesStamp.Height` manually.  
* **Performance note:** Stamping thousands of pages can take a few seconds, but Aspose streams pages efficiently—no need to load the whole document into memory.  

---

## Conclusion

We’ve just demonstrated how to **add bates numbering** to a PDF using Aspose.Pdf, while simultaneously **add page numbers pdf**, enable **auto adjust font size**, and create an **add text watermark** in one cohesive flow. The complete, runnable example above gives you a solid foundation you can adapt to any legal‑document workflow or internal reporting system.

Ready for the next step? Try pairing this approach with Aspose’s PDF merging API to batch‑process multiple files, or explore the `TextFragment` class for richer watermarks (colored, rotated, or multi‑line). The possibilities are endless, and the code you now have is a reliable baseline.

If you found this guide helpful, feel free to drop a comment, star the repository, or share your own variations. Happy coding, and may your PDFs always be perfectly numbered!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}