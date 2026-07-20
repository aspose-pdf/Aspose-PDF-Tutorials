---
category: general
date: 2026-07-20
description: How to add bates numbering to a PDF using Aspose.Pdf. Learn to add bates
  numbers pdf and add stamp to each page quickly and reliably.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to add bates numbering
- add bates numbers pdf
- add stamp to each page
language: en
lastmod: 2026-07-20
og_description: How to add bates numbering to a PDF with Aspose.Pdf. This guide shows
  you how to add bates numbers pdf and stamp each page in just a few lines of C#.
og_image_alt: Screenshot of a PDF page displaying Bates numbering added by Aspose.Pdf
og_title: How to Add Bates Numbering in PDF – Complete Aspose.Pdf Tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: How to add bates numbering to a PDF using Aspose.Pdf. Learn to add
    bates numbers pdf and add stamp to each page quickly and reliably.
  headline: How to Add Bates Numbering in PDF with Aspose – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: Yes. Load the document with a `PdfLoadOptions` object that supplies the
      password, then proceed exactly as shown.
    question: Does this work with password‑protected PDFs?
  - answer: Create multiple `BatesNumberingStamp` instances, configure each with its
      own `Prefix`, and apply them only to the appropriate page ranges.
    question: What if I need different prefixes per case?
  - answer: 'Aspose.Pdf offers a 30‑day trial. For production use you’ll need a license,
      but the API surface remains identical. --- ## Conclusion We’ve just covered
      **how to add bates numbering** to any PDF using Aspose.Pdf, demonstrated how
      to **add bates numbers pdf** in a clean, repeatable fashion, and showed'
    question: Is the library free?
  type: FAQPage
tags:
- Aspose.Pdf
- Bates numbering
- PDF automation
title: How to Add Bates Numbering in PDF with Aspose – Step‑by‑Step Guide
url: /net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-aspose-step-by-step-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Add Bates Numbering in PDF with Aspose – Step‑by‑Step Guide

Ever wondered **how to add bates numbering** to a legal document without spending hours in a GUI? You're not the only one. In many law firms, government agencies, and even large enterprises, stamping every page with a unique identifier is a daily chore—yet a single line of C# can make it a piece of cake.

In this tutorial we'll walk through a complete, runnable example that shows you exactly **how to add bates numbering** using the Aspose.Pdf library. By the end you’ll also know how to **add bates numbers pdf** files and **add stamp to each page** with just a few lines of code. No magic, just clear reasoning and practical tips.

## What You’ll Learn

- Load an existing PDF with Aspose.Pdf.
- Create a `BatesNumberingStamp` and customize its look.
- Loop through every page and **add stamp to each page** automatically.
- Save the result as a new PDF that carries a professional Bates number on every sheet.

### Prerequisites

- .NET 6.0 or later (the code works on .NET Framework 4.7+ as well).
- A valid Aspose.Pdf for .NET license (or a temporary evaluation key).
- An original PDF file you want to number (we’ll call it `Original.pdf`).

If you meet those three items, you’re ready to dive in.

---

## Step 1: Set Up Your Project and Install Aspose.Pdf

First, create a new console project (or add the code to an existing one). Then pull the NuGet package:

```bash
dotnet add package Aspose.Pdf
```

> **Pro tip:** If you’re on a corporate network, make sure your NuGet source is configured to reach `https://www.nuget.org`.

## Step 2: Load the Source PDF Document

Loading a PDF is as simple as pointing Aspose at the file path. The `Document` class represents the whole file.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the source PDF (replace the path with your own)
var document = new Document(@"C:\Temp\Original.pdf");

// Quick sanity check – how many pages are we dealing with?
Console.WriteLine($"Document contains {document.Pages.Count} pages.");
```

Why do we log the page count? Because Bates numbering must be sequential across *all* pages, and it’s nice to verify you’re not accidentally loading a different file.

## Step 3: Create a Bates Numbering Stamp

The heart of the operation is the `BatesNumberingStamp`. It lets you define prefix, separator, digit padding, and even whether the stamp should be treated as an *artifact* (i.e., invisible to text extraction tools).

```csharp
var batesStamp = new BatesNumberingStamp
{
    // Starting number – change this to whatever your workflow requires
    StartingNumber = 1000,

    // A human‑readable prefix, often a case or project code
    Prefix = "ABC-",

    // Separator between the running number and the total page count
    Separator = "/",

    // Pad the number with leading zeros to a fixed width (5 digits here)
    NumberOfDigits = 5,

    // Mark the stamp as an artifact so it won’t be indexed by search
    Artifact = true
};
```

**Why these settings?**  
- `StartingNumber = 1000` mimics a typical legal docket that already has a backlog.  
- `NumberOfDigits = 5` guarantees numbers like `01000`, `01001`, etc., line up nicely.  
- `Artifact = true` is essential when the PDF will be fed into OCR or e‑discovery pipelines; the numbers stay visible to humans but are ignored by text‑search engines.

## Step 4: Add the Stamp to Every Page

Now we loop over `document.Pages` and apply the same stamp to each page. Aspose automatically increments the number for you.

```csharp
foreach (Page page in document.Pages)
{
    // The AddStamp method clones the stamp for the current page,
    // updates the running number, and positions it at the default location.
    page.AddStamp(batesStamp);
}
```

> **Common question:** *Can I control where the stamp appears?*  
> Absolutely. The `BatesNumberingStamp` inherits from `Stamp`, so you can set properties like `HorizontalAlignment`, `VerticalAlignment`, `XIndent`, and `YIndent` before the loop. For brevity we’ll stick with the default bottom‑right corner.

## Step 5: Save the Modified PDF

Finally, persist the changes. You can overwrite the original file or write to a new location—here we’ll keep both copies.

```csharp
// Save the new PDF with Bates numbers
document.Save(@"C:\Temp\BatesNumbered.pdf");

// Inform the user
Console.WriteLine("Bates numbering added successfully!");
```

When you open `BatesNumbered.pdf`, each page will display a stamp similar to:

```
ABC-01000/00123
ABC-01001/00123
…
ABC-01122/00123
```

where `00123` is the total page count, and the prefix `ABC-` stays constant.

---

## Full Working Example

Copy the entire block below into a fresh `Program.cs` file and run it. Adjust the file paths to match your environment.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            var srcPath = @"C:\Temp\Original.pdf";
            var document = new Document(srcPath);
            Console.WriteLine($"Loaded '{srcPath}' with {document.Pages.Count} pages.");

            // 2️⃣ Configure the Bates numbering stamp
            var batesStamp = new BatesNumberingStamp
            {
                StartingNumber = 1000,
                Prefix = "ABC-",
                Separator = "/",
                NumberOfDigits = 5,
                Artifact = true,
                // Optional: change alignment if you need a different location
                // HorizontalAlignment = HorizontalAlignment.Left,
                // VerticalAlignment = VerticalAlignment.Top,
                // XIndent = 20,
                // YIndent = 20
            };

            // 3️⃣ Apply the stamp to every page
            foreach (Page page in document.Pages)
            {
                page.AddStamp(batesStamp);
            }

            // 4️⃣ Save the new PDF
            var outPath = @"C:\Temp\BatesNumbered.pdf";
            document.Save(outPath);
            Console.WriteLine($"Saved Bates‑numbered PDF to '{outPath}'.");
        }
    }
}
```

**Expected output in the console:**

```
Loaded 'C:\Temp\Original.pdf' with 12 pages.
Saved Bates-numbered PDF to 'C:\Temp\BatesNumbered.pdf'.
```

Open the saved file and you’ll see the sequential numbers on each page—exactly what you’d expect when you **add bates numbers pdf**.

---

## Advanced Tweaks (Optional)

| Goal | How to achieve it |
|------|-------------------|
| **Change stamp color** | Set `batesStamp.Color = Color.FromRgb(255, 0, 0);` before the loop. |
| **Place stamp in the header** | Adjust `HorizontalAlignment` and `VerticalAlignment` properties as shown in the commented code. |
| **Skip certain pages** | Add an `if (page.Number % 2 == 0) continue;` condition inside the `foreach`. |
| **Use a custom font** | Assign `batesStamp.Font = FontRepository.FindFont("Arial");`. |
| **Make the stamp visible to OCR** | Set `Artifact = false`. |

These variations let you **add stamp to each page** while still keeping the core logic tidy.

---

## Frequently Asked Questions

**Q: Does this work with password‑protected PDFs?**  
A: Yes. Load the document with a `PdfLoadOptions` object that supplies the password, then proceed exactly as shown.

**Q: What if I need different prefixes per case?**  
A: Create multiple `BatesNumberingStamp` instances, configure each with its own `Prefix`, and apply them only to the appropriate page ranges.

**Q: Is the library free?**  
A: Aspose.Pdf offers a 30‑day trial. For production use you’ll need a license, but the API surface remains identical.

---

## Conclusion

We’ve just covered **how to add bates numbering** to any PDF using Aspose.Pdf, demonstrated how to **add bates numbers pdf** in a clean, repeatable fashion, and showed you the simplest way to **add stamp to each page** with a single loop. The code is fully self‑contained, runs in seconds, and can be dropped into larger document‑processing pipelines without modification.

Ready for the next challenge? Try generating a cover page that lists the Bates range, or embed a QR code alongside each stamp. The possibilities are endless, and the same pattern you learned today will serve you well wherever you need to automate PDF metadata.

If you found this guide helpful, give it a share, leave a comment, or explore our other tutorials on PDF merging, watermarking, and digital signatures. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET&#58; A Complete Guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [How to Add Page Number Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}