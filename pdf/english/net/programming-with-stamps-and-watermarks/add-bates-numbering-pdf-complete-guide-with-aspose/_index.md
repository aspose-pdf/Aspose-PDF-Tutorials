---
category: general
date: 2026-06-08
description: Add bates numbering pdf using Aspose.Pdf in C#. Learn how to add bates,
  add page numbers pdf, add sequential numbers pdf, and see a bates number pdf example.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add page numbers pdf
- add sequential numbers pdf
- bates number pdf example
language: en
og_description: Add bates numbering pdf in C#. This tutorial shows how to add bates,
  add page numbers pdf, and add sequential numbers pdf with a full bates number pdf
  example.
og_title: Add Bates Numbering PDF – Complete Guide with Aspose
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. Learn how to add bates,
    add page numbers pdf, add sequential numbers pdf, and see a bates number pdf example.
  headline: Add Bates Numbering PDF – Complete Guide with Aspose
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. Learn how to add bates,
    add page numbers pdf, add sequential numbers pdf, and see a bates number pdf example.
  name: Add Bates Numbering PDF – Complete Guide with Aspose
  steps:
  - name: Install the Aspose.Pdf NuGet Package
    text: 'First, add the library to your project. Open the Package Manager Console
      and run:'
  - name: Open the Source PDF Document
    text: Now we load the PDF we want to stamp. The `using` statement ensures the
      file is closed properly even if an exception occurs.
  - name: Create a Bates Numbering Facade
    text: 'The *facade* pattern hides the complexity of the underlying PDF structure.
      Here’s how we instantiate it:'
  - name: Configure the Starting Number and Prefix
    text: Bates numbers often include a case‑specific prefix. You can also control
      the number of digits, the separator, and the placement on the page.
  - name: Apply the Bates Numbering to the Document
    text: 'With the facade configured, we now stamp every page:'
  - name: Save the Modified PDF
    text: 'Finally, write the output to disk:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF processing
title: Add Bates Numbering PDF – Complete Guide with Aspose
url: /net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-guide-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Bates Numbering PDF – Complete Programming Guide

Ever needed to **add bates numbering pdf** but weren’t sure where to start? If you’ve ever wondered *how to add bates* to a legal document, you’re in the right place. In this tutorial we’ll walk through a hands‑on, end‑to‑end example that not only adds Bates numbers but also shows you how to **add page numbers pdf**, **add sequential numbers pdf**, and even provides a ready‑to‑run **bates number pdf example**.

We’ll be using the Aspose.Pdf library for .NET, because it abstracts away the low‑level PDF internals while giving you fine‑grained control. By the end of this guide you’ll have a reusable snippet you can drop into any C# project, and you’ll understand why each line matters.

## What You’ll Need

- **.NET 6.0** or later (the code also works on .NET Framework 4.6+).  
- A **license** for Aspose.Pdf or a free temporary evaluation key.  
- A sample PDF called `input.pdf` placed in a folder you can reference.  
- Visual Studio, Rider, or any C# editor you prefer.

That’s it—no extra tools, no command‑line gymnastics. Ready? Let’s dive in.

## Add Bates Numbering PDF – Step‑by‑Step Implementation

Below we break the process into six logical steps. Each step includes a short code snippet, an explanation of *why* we do it, and a tip you might find handy.

### Step 1: Install the Aspose.Pdf NuGet Package

First, add the library to your project. Open the Package Manager Console and run:

```powershell
Install-Package Aspose.Pdf
```

> **Pro tip:** If you’re on .NET Core, you can also use `dotnet add package Aspose.Pdf`.

Installing the package gives you access to the `Aspose.Pdf.Facades.BatesNumbering` class, which is the workhorse for **add bates numbering pdf**.

### Step 2: Open the Source PDF Document

Now we load the PDF we want to stamp. The `using` statement ensures the file is closed properly even if an exception occurs.

```csharp
using (var doc = new Aspose.Pdf.Document(@"C:\MyPdfs\input.pdf"))
{
    // All further steps happen inside this block.
}
```

Why use `Aspose.Pdf.Document`? It represents the entire PDF in memory, allowing us to manipulate pages, fonts, and metadata without touching the original file on disk.

### Step 3: Create a Bates Numbering Facade

The *facade* pattern hides the complexity of the underlying PDF structure. Here’s how we instantiate it:

```csharp
var bates = new Aspose.Pdf.Facades.BatesNumbering();
```

This object will later be configured with a prefix, start number, and formatting options. Think of it as the “engine” that will **add page numbers pdf** in a Bates‑compliant way.

### Step 4: Configure the Starting Number and Prefix

Bates numbers often include a case‑specific prefix. You can also control the number of digits, the separator, and the placement on the page.

```csharp
bates.StartNumber = 1000;          // First number in the sequence
bates.Prefix = "CASE-";            // Prefix that appears before each number
bates.NumberOfDigits = 5;          // Pads numbers with leading zeros (e.g., 01000)
bates.Separator = "-";             // Optional separator between prefix and number
bates.Location = new Aspose.Pdf.Rectangle(0, 0, 200, 20); // Bottom‑left corner
bates.FontSize = 12;
bates.FontColor = System.Drawing.Color.Blue;
```

**Why these settings?**  
- `StartNumber` lets you continue a previous series.  
- `NumberOfDigits` guarantees uniform length, which is crucial for legal indexing.  
- `Location` defines where the **add sequential numbers pdf** will appear; you can move it to the top‑right if you prefer.

### Step 5: Apply the Bates Numbering to the Document

With the facade configured, we now stamp every page:

```csharp
bates.AddBatesNumbering(doc);
```

Under the hood, Aspose iterates through each page, draws the text at the specified location, and respects any existing content. This single line is what actually **add bates numbering pdf** to your file.

### Step 6: Save the Modified PDF

Finally, write the output to disk:

```csharp
doc.Save(@"C:\MyPdfs\output.pdf");
```

You now have a PDF where every page carries a unique Bates identifier, ready for discovery or courtroom submission.

#### Full Working Example (Bates Number PDF Example)

Putting it all together, here’s a complete, self‑contained program you can compile and run:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using (var doc = new Document(@"C:\MyPdfs\input.pdf"))
        {
            // 2️⃣ Create the Bates numbering facade
            var bates = new BatesNumbering();

            // 3️⃣ Configure prefix, start number, and formatting
            bates.StartNumber = 1000;
            bates.Prefix = "CASE-";
            bates.NumberOfDigits = 5;
            bates.Separator = "-";
            bates.Location = new Rectangle(0, 0, 200, 20); // Bottom‑left
            bates.FontSize = 12;
            bates.FontColor = Color.Blue;

            // 4️⃣ Apply the numbering to every page
            bates.AddBatesNumbering(doc);

            // 5️⃣ Save the result
            doc.Save(@"C:\MyPdfs\output.pdf");
        }

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

> **Expected output:** Open `output.pdf` and you’ll see “CASE‑01000”, “CASE‑01001”, … at the bottom‑left of each page.

![Screenshot of a PDF page with Bates numbers at the bottom-left corner – add bates numbering pdf example](https://example.com/bates-numbering-screenshot.png "add bates numbering pdf example")

*(Image alt text: *add bates numbering pdf example* – shows the Bates numbers applied to a sample PDF.)*

## How to Add Bates – Understanding the Facade

You might wonder **how to add bates** without the Aspose facade. The alternative is to manually draw text on each page using low‑level PDF operators, but that approach is error‑prone and requires deep knowledge of the PDF spec. The facade abstracts those details, letting you focus on *what* you want (a prefix, a start number) rather than *how* to render it.

If you ever need to **add page numbers pdf** in a non‑Bates style (e.g., “Page 3 of 12”), you can reuse the same `BatesNumbering` class—just change the `Prefix` to an empty string and adjust the `Location`. The underlying engine is the same, which means you get consistent rendering across both use cases.

## Add Page Numbers PDF – Customizing Placement and Style

Legal teams often request the page number in the header, while litigation support staff prefers it in the footer. Here’s a quick tweak:

```csharp
bates.Location = new Rectangle(0, doc.Pages[1].PageInfo.Height - 20, 200, 20); // Top‑right
bates.Prefix = "";               // No prefix for plain page numbers
bates.StartNumber = 1;           // Start from 1
bates.NumberOfDigits = 0;        // No padding
bates.FontColor = Color.Black;
```

The same `AddBatesNumbering` call will now **add page numbers pdf** to the top of each page. Because the facade works on the document object, you can switch between Bates and plain page numbering with a few property changes—no need to rewrite the loop.

## Add Sequential Numbers PDF – Advanced Formatting

Suppose you need a format like `2023-CASE-00123`. You can combine a date prefix with the existing settings:

```csharp
bates.Prefix = $"{DateTime.Now:yyyy}-CASE-";
bates.NumberOfDigits = 5;
bates.Separator = "-";
```

Now every page will read `2023-CASE-00123`, `2023-CASE-00124`, etc. This demonstrates how easily you can **add sequential numbers pdf** that satisfy complex naming conventions.

## Edge Cases and Common Pitfalls

| Situation | What to watch out for | Suggested fix |
|-----------|----------------------|---------------|
| **Very large PDFs ( > 500 MB )** | Memory consumption can spike because the whole document is loaded into RAM. | Use `Document` with `MemoryManagement` settings or process the file in chunks with `PdfFileEditor`. |
| **Existing page numbers**


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add Page Number Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [Aspose.PDF .NET: Add Page Numbers to PDFs Using FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}