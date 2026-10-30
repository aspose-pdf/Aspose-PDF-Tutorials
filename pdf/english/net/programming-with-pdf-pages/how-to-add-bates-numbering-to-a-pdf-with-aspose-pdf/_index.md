---
category: general
date: 2026-10-07
description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
  guide also covers pdf page numbering and other numbering tricks.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- pdf page numbering
- number pdf pages
- how to add bates
- bates numbering pdf
language: en
lastmod: 2026-10-07
og_description: Add bates numbering to a PDF quickly. Follow this tutorial to master
  pdf page numbering, number pdf pages, and automate document tracking.
og_image_alt: Screenshot of a PDF with Bates numbers added using Aspose.Pdf
og_title: Add bates numbering to PDFs in C# – complete Aspose guide
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  headline: How to add bates numbering to a PDF with Aspose.Pdf
  type: TechArticle
- description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  name: How to add bates numbering to a PDF with Aspose.Pdf
  steps:
  - name: 1. Can I change the location of the numbers?
    text: Yes. Set `batesOptions.Position = new Position(10, 10, 10, 10);` where the
      four values represent margins from the top, bottom, left, and right edges. Aspose
      also provides predefined enums such as `BatesNumberingPosition.BottomCenter`.
  - name: 2. What if my PDF already contains page numbers?
    text: Adding Bates numbers will **stack** on top of existing numbers. To avoid
      visual clutter, either hide the original numbers (if they are part of a text
      layer) or adjust the `batesOptions` font size and position.
  - name: 3. Does this work with encrypted PDFs?
    text: 'Aspose can open password‑protected PDFs if you supply the password:'
  - name: 4. How do I **number pdf pages** with a simple sequential counter (no prefix/suffix)?
    text: 'Just set `Prefix = string.Empty` and `Suffix = string.Empty`:'
  - name: 5. Can I use this approach in ASP.NET Core to serve PDFs on‑the‑fly?
    text: 'Absolutely. Load the document, apply the numbering, then write the stream
      to the HTTP response:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: How to add bates numbering to a PDF with Aspose.Pdf
url: /net/programming-with-pdf-pages/how-to-add-bates-numbering-to-a-pdf-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to add bates numbering to a PDF with Aspose.Pdf

If you need to **add bates numbering** to a PDF, this guide shows you exactly how to do it in C#. Whether you are preparing legal bundles, managing case files, or just want reliable **pdf page numbering**, the steps below give you a complete, runnable solution.

In this tutorial you will learn how to:

* Load an existing PDF file.
* Configure Bates numbering options such as prefix, start number, digit padding, separator, and suffix.
* Apply the numbering to every page.
* Save the updated document.

No external tools are required beyond the Aspose.Pdf for .NET library, and the code works with .NET 6+ as well as .NET Framework 4.7.2+.  

---

## Prerequisites

Before you start, make sure you have:

| Requirement | Why it matters |
|-------------|----------------|
| **Aspose.Pdf for .NET** (NuGet package `Aspose.Pdf`) | Provides the `Document` and `BatesNumberingOptions` classes used in the code. |
| **.NET SDK** (6.0 or later recommended) | Enables you to compile and run the C# console application. |
| **A source PDF** you want to number | The tutorial uses `source.pdf` as an example; replace the path with your own file. |
| **Write permission** to the output folder | The `Save` call needs to write the new file. |

You can install the library with the following CLI command:

```bash
dotnet add package Aspose.Pdf
```

---

## Step 1: Create a new console project

Open a terminal and run:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
```

This creates a minimal C# project that we will fill with the code needed to **add bates numbering**.

---

## Step 2: Add the required `using` directives

Open `Program.cs` and add the namespaces at the top of the file:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

* `Aspose.Pdf` gives you access to the `Document` class for loading and saving PDFs.  
* `Aspose.Pdf.Text` contains `BatesNumberingOptions`, the object that defines how the numbers appear.

---

## Step 3: Load the source PDF

The first actionable line loads the PDF you want to number. Replace `"YOUR_DIRECTORY/source.pdf"` with the actual path to your file.

```csharp
// Load the source PDF
Document pdf = new Document("YOUR_DIRECTORY/source.pdf");
```

If the file cannot be found, Aspose throws a `FileNotFoundException`. To avoid this, you may want to validate the path beforehand:

```csharp
if (!System.IO.File.Exists("YOUR_DIRECTORY/source.pdf"))
{
    Console.WriteLine("Source PDF not found.");
    return;
}
```

---

## Step 4: Define Bates numbering options

`BatesNumberingOptions` lets you control every visual element of the numbering. The example below shows a typical configuration for legal case files:

```csharp
// Define Bates numbering options
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",          // Text before the numeric part
    StartNumber = 1000,       // First number to use
    Digits = 6,               // Pad with leading zeros (e.g., 001000)
    Separator = "-",          // Character between prefix, number, and suffix
    Suffix = "-2025"          // Text after the numeric part
};
```

**Why each property matters**

| Property | Purpose |
|----------|---------|
| `Prefix` | Helps you group documents by project, client, or case. |
| `StartNumber` | Sets the initial counter; useful when you already have existing numbered files. |
| `Digits` | Guarantees a uniform width, making sorting easier. |
| `Separator` | Improves readability, especially when combining prefix and suffix. |
| `Suffix` | Allows you to add a year, version, or any trailing identifier. |

You can also control the placement (top, bottom, left, right) and font style by accessing `batesOptions.Position` and `batesOptions.Font`. For most scenarios the defaults (bottom‑right, 12‑pt Times New Roman) work well.

---

## Step 5: Apply the numbering to every page

Calling `pdf.BatesNumbering.Add` inserts the numbers on each page in the order they appear.

```csharp
// Apply Bates numbering to every page
pdf.BatesNumbering.Add(batesOptions);
```

If you need to **number pdf pages** only on a subset (e.g., skip the cover page), you can pass a `PageCollection` instead:

```csharp
// Example: skip the first page
pdf.BatesNumbering.Add(batesOptions, pdf.Pages.Skip(1));
```

---

## Step 6: Save the updated PDF

Finally, write the modified document to disk. The file name usually reflects that the PDF now contains Bates numbers.

```csharp
// Save the PDF with Bates numbers applied
pdf.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering added successfully.");
```

If the output folder does not exist, Aspose creates it automatically. However, you should ensure you have write permissions to avoid a `UnauthorizedAccessException`.

---

## Full, runnable example

Putting all the pieces together, here is a complete program you can copy, paste, and run:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source PDF
        // -------------------------------------------------
        const string inputPath = "YOUR_DIRECTORY/source.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        Document pdf = new Document(inputPath);

        // -------------------------------------------------
        // 2️⃣ Configure Bates numbering
        // -------------------------------------------------
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            Digits = 6,
            Separator = "-",
            Suffix = "-2025"
        };

        // -------------------------------------------------
        // 3️⃣ Apply the numbering to every page
        // -------------------------------------------------
        pdf.BatesNumbering.Add(batesOptions);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";
        pdf.Save(outputPath);
        Console.WriteLine($"Bates numbering added. Saved to {outputPath}");
    }
}
```

**Expected output** (console):

```
Bates numbering added. Saved to YOUR_DIRECTORY/bates_numbered.pdf
```

Open `bates_numbered.pdf` and you will see each page labeled something like `CASE-001000-2025`, `CASE-001001-2025`, etc., positioned in the default bottom‑right corner.

---

## Frequently asked questions (FAQ)

### 1. Can I change the location of the numbers?
Yes. Set `batesOptions.Position = new Position(10, 10, 10, 10);` where the four values represent margins from the top, bottom, left, and right edges. Aspose also provides predefined enums such as `BatesNumberingPosition.BottomCenter`.

### 2. What if my PDF already contains page numbers?
Adding Bates numbers will **stack** on top of existing numbers. To avoid visual clutter, either hide the original numbers (if they are part of a text layer) or adjust the `batesOptions` font size and position.

### 3. Does this work with encrypted PDFs?
Aspose can open password‑protected PDFs if you supply the password:

```csharp
Document pdf = new Document("source.pdf", new LoadOptions { Password = "mySecret" });
```

Bates numbering is then applied in the same way.

### 4. How do I **number pdf pages** with a simple sequential counter (no prefix/suffix)?
Just set `Prefix = string.Empty` and `Suffix = string.Empty`:

```csharp
BatesNumberingOptions simple = new BatesNumberingOptions
{
    StartNumber = 1,
    Digits = 4   // 0001, 0002, …
};
pdf.BatesNumbering.Add(simple);
```

### 5. Can I use this approach in ASP.NET Core to serve PDFs on‑the‑fly?
Absolutely. Load the document, apply the numbering, then write the stream to the HTTP response:

```csharp
using (var ms = new MemoryStream())
{
    pdf.Save(ms);
    ms.Position = 0;
    return File(ms, "application/pdf", "bates_numbered.pdf");
}
```

---

## Edge cases and best‑practice tips

| Situation | Recommended approach |
|-----------|----------------------|
| **Large PDFs (hundreds of pages)** | Call `pdf.BatesNumbering.Add` **after** you have performed any page‑level transformations to avoid re‑processing the same pages multiple times. |
| **Custom fonts** | Set `batesOptions.Font = FontRepository.FindFont("Arial")` and adjust `batesOptions.FontSize` for better readability on scanned documents. |
| **Performance‑critical batch jobs** | Reuse a single `Document` instance when processing many files in a loop; dispose of it after each iteration to free memory. |
| **International characters** | Use Unicode‑compatible fonts (e.g., `Times New Roman Unicode`) to ensure the prefix or suffix displays correctly. |
| **Version compatibility** | The code works with Aspose.Pdf 23.10 and newer. If you target an older version, check the API reference for any property name changes. |

---

## Conclusion

You now know how to **add bates numbering** to a PDF using Aspose.Pdf for .NET. The tutorial covered loading a PDF, configuring `BatesNumberingOptions`, applying the numbers to each page, and saving the result. With these building blocks you can also implement generic **pdf page numbering**, **number pdf pages** with custom formats, and integrate the process into larger automation pipelines.

**Next steps**

* Explore the **bates numbering pdf** API further to customize font, color, and placement.  
* Combine this technique with **digital signatures** to create tamper‑evident legal bundles.  
* Look into Aspose’s **PDF merging** capabilities if you need to concatenate multiple case files before numbering.

Feel free to experiment with different prefixes, suffixes, and digit lengths to match your organization’s filing standards. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create PDF Document C# – Add Bates Numbering Guide](/pdf/english/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/)
- [How to Add Bates Numbering in PDF with C# – Complete Guide](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-c-complete-guide/)
- [Aspose PDF Tutorial – Insert a Blank Page and Update Bates Numbering](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}