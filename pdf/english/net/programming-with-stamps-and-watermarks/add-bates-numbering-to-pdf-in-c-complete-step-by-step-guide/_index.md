---
category: general
date: 2026-06-18
description: Add Bates numbering to PDF in C# quickly. Learn how to load PDF, set
  a bates numbering prefix, and add sequential page numbers using a simple C# library.
draft: false
keywords:
- add bates numbering
- add sequential page numbers
- load pdf c#
- apply bates numbering
- bates numbering prefix
language: en
og_description: Add Bates numbering to PDF in C# in the first sentence. Follow this
  guide to load a PDF, configure a prefix, and apply sequential page numbers automatically.
og_title: Add Bates Numbering to PDF in C# – Full Programming Walkthrough
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Add Bates numbering to PDF in C# quickly. Learn how to load PDF, set
    a bates numbering prefix, and add sequential page numbers using a simple C# library.
  headline: Add Bates Numbering to PDF in C# – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- PDF
- C#
- Document Processing
title: Add Bates Numbering to PDF in C# – Complete Step‑by‑Step Guide
url: /net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdf-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Bates Numbering to PDF in C# – Complete Step‑by‑Step Guide

Ever needed to **add bates numbering** to a PDF but weren’t sure where to start in C#? You’re not alone. In many legal, medical, or archival workflows, stamping each page with a unique identifier is a must, and doing it programmatically saves endless manual effort.

In this tutorial you’ll see exactly how to **load pdf c#**, configure a **bates numbering prefix**, and **apply bates numbering** so that every page gets a sequential number. By the end you’ll have a ready‑to‑run snippet that adds sequential page numbers with a custom prefix—no mystery, just clear code.

## What You’ll Learn

- How to open an existing PDF file using a popular .NET PDF library.  
- How to set up **bates numbering options** (prefix, start number, padding).  
- How to invoke the library’s `AddBatesNumbering` method to **add bates numbering** automatically.  
- How to save the modified document without breaking existing content.  

No external tools, no command‑line hacks—just straight C# code you can drop into any .NET project.

![Diagram showing Bates numbering applied to PDF pages](/images/bates-numbering-flow.png){: .align-center alt="Add Bates Numbering flow diagram"}

## Prerequisites

- .NET 6.0 or later (the code works with .NET Core and .NET Framework 4.6+).  
- A PDF manipulation library that supports Bates numbering (e.g., **Aspose.PDF**, **iText7**, or **PdfSharp** with an extension). The example below uses a generic API that mirrors Aspose.PDF’s syntax, but you can adapt it to your favorite library.  
- Basic C# knowledge—if you can write a `Console.WriteLine`, you’re good to go.  

Got those? Great—let’s dive in.

## Add Bates Numbering – Overview

Before we start coding, let’s clarify why **add bates numbering** matters. A Bates number is a unique identifier that appears on every page, usually in the format `PREFIX-####`. Courts, law firms, and government agencies rely on it to reference documents precisely. Automating this step eliminates human error, ensures consistent formatting, and speeds up batch processing of hundreds of files.

Now that the “why” is clear, let’s see the “how”.

## Step 1: Load PDF in C#

First, we need to bring the source PDF into memory. Most libraries expose a `Document` constructor that takes a file path.

```csharp
// Step 1: Load the PDF document from disk
// Replace YOUR_DIRECTORY with the actual folder path.
Document doc = new Document("YOUR_DIRECTORY/input.pdf");

// Quick sanity check – ensure the file was loaded.
if (doc.Pages.Count == 0)
{
    throw new InvalidOperationException("The PDF appears to be empty or could not be read.");
}
```

*Why this step?* Loading the PDF gives us a manipulable object model. Without it, we can’t attach a **bates numbering prefix** or any other metadata.

> **Pro tip:** If you’re processing many files, consider reusing a single `PdfLoadOptions` instance to improve performance.

## Step 2: Configure Bates Numbering Prefix

Next, we define how the numbering should look. The `BatesNumberingOptions` class lets you specify a prefix, a starting number, and even padding (how many digits to reserve).

```csharp
// Step 2: Set up Bates numbering options
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // The prefix that will appear before every number.
    Prefix = "ABC",          // <-- this is the bates numbering prefix
    // The first number in the series.
    Start = 1000,
    // Optional: pad numbers to 5 digits (e.g., 01000, 01001)
    Padding = 5
};
```

*Why this matters:* The **bates numbering prefix** helps categorize documents (e.g., “ABC” for a specific case). Adjust `Start` and `Padding` to match your organization’s conventions.

## Step 3: Apply Bates Numbering to the Document

Now the core action: tell the library to embed the numbers on each page. The method name varies by library, but the concept stays the same.

```csharp
// Step 3: Apply the Bates numbering to every page
doc.AddBatesNumbering(batesOptions);
```

Behind the scenes the library iterates over `doc.Pages`, draws the text (usually in the footer), and respects any existing page margins. If you need the numbers in a different location, most APIs let you tweak `BatesNumberingOptions.Position`.

> **What if the PDF already has page numbers?** Most libraries will overlay the new Bates number on top of existing content. If you want to replace them, you may need to clear the existing footer first—check your library’s documentation for `RemovePageNumbers()` or similar.

## Step 4: Save the Updated PDF

Finally, write the modified document back to disk. You can overwrite the original or write to a new file; the latter is safer for batch jobs.

```csharp
// Step 4: Save the PDF with Bates numbers applied
doc.Save("YOUR_DIRECTORY/output.pdf");

// Confirmation message
Console.WriteLine("Bates numbering added successfully! Output saved to output.pdf");
```

That’s it—four concise steps and you’ve **add bates numbering** to any PDF file.

## Full Working Example

Putting it all together, here’s a self‑contained console app you can copy‑paste into Visual Studio:

```csharp
using System;
using Aspose.Pdf;               // Replace with your PDF library namespace
using Aspose.Pdf.Facades;       // For Bates numbering support

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF
        Document doc = new Document("YOUR_DIRECTORY/input.pdf");
        if (doc.Pages.Count == 0)
        {
            Console.WriteLine("Error: PDF is empty or unreadable.");
            return;
        }

        // 2️⃣ Configure Bates numbering
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC",
            Start = 1000,
            Padding = 5,
            // Optional: change position to top‑right
            // Position = new Position(0, 0, 0, 0) // customize as needed
        };

        // 3️⃣ Apply the numbering
        doc.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the result
        doc.Save("YOUR_DIRECTORY/output.pdf");
        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Expected output:** Open `output.pdf` and you’ll see each page labeled something like `ABC-01000`, `ABC-01001`, … up to the last page. The numbers appear in the default footer location unless you changed the `Position`.

## Handling Edge Cases

| Situation | Recommended Approach |
|-----------|----------------------|
| **Large documents (1000+ pages)** | Increase `Padding` to accommodate the highest number, e.g., `Padding = 7`. |
| **Existing watermarks** | Apply Bates numbering *after* adding watermarks to avoid overlap. |
| **Different prefixes per batch** | Loop through files and set `batesOptions.Prefix` dynamically based on folder name or metadata. |
| **Unicode characters in prefix** | Ensure your PDF library supports UTF‑8; some older versions may require ASCII only. |

## Pro Tips & Common Pitfalls

- **Pro tip:** Use `doc.Optimize()` (if available) after numbering to compress the file and keep size manageable.  
- **Watch out for:** PDFs with encrypted pages—most libraries need the password before you can add numbers.  
- **Typical mistake:** Forgetting to set `Padding`. Without it, numbers like `1000` will become `1000` (no leading zeros), which can break sorting in some systems.  
- **Performance tip:** For batch processing, instantiate the `BatesNumberingOptions` once and reuse it across documents; only change `Start` if you need a continuous series.

## Conclusion

You now have a clear, reproducible way to **add bates numbering** to PDFs using C#. From loading the file to configuring a **bates numbering prefix**, applying the numbers, and finally saving the result, every step is covered with both *how* and *why* explanations. This solution works for any .NET project and can be extended to handle bulk operations, custom positions, or integration with document management systems.

Ready for the next challenge? Try experimenting with **add sequential page numbers** in a different style, or combine Bates numbers with QR codes for even richer metadata. The same pattern—load, configure, apply, save—holds for most PDF automation tasks.

If you’ve got questions about customizing the layout, handling encrypted PDFs, or integrating this into an ASP.NET API, drop a comment below. Happy coding, and may your PDFs always be perfectly numbered!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Add page numbers pdf with C# – Full Step‑by‑Step Guide](/pdf/english/net/programming-with-pdf-pages/add-page-numbers-pdf-with-c-full-step-by-step-guide/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Add Images & Page Numbers to PDFs Using Aspose.PDF for .NET: A Complete Guide](/pdf/english/net/document-manipulation/enhance-pdfs-images-page-numbers-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}