---
category: general
date: 2026-06-24
description: Add bates numbering to PDF files using C# and Aspose.PDF. Learn custom
  page numbers, sequential page numbers, and header footer numbering in minutes.
draft: false
keywords:
- add bates numbering
- custom page numbers
- sequential page numbers
- bates numbering pdf
- header footer numbering
language: en
og_description: Add bates numbering to PDF files using C# and Aspose.PDF. Master custom
  page numbers and header footer numbering in a few easy steps.
og_title: Add Bates Numbering to PDFs with C# – Complete Guide
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Add bates numbering to PDF files using C# and Aspose.PDF. Learn custom
    page numbers, sequential page numbers, and header footer numbering in minutes.
  headline: Add Bates Numbering to PDFs with C# – Complete Guide
  type: TechArticle
- description: Add bates numbering to PDF files using C# and Aspose.PDF. Learn custom
    page numbers, sequential page numbers, and header footer numbering in minutes.
  name: Add Bates Numbering to PDFs with C# – Complete Guide
  steps:
  - name: Load the Source PDF Document
    text: First we need a `Document` object that represents the file we want to modify.
  - name: Configure Bates Numbering Options (custom page numbers)
    text: Now we set up a `BatesNumberingOptions` object. This is where you define
      **custom page numbers**, the font, colors, and margins.
  - name: Apply the Bates Numbering to the Entire Document
    text: With the options prepared, the actual insertion is a single method call.
  - name: Save the PDF with Bates Numbers Applied
    text: Finally, write the modified document back to disk.
  - name: Limiting the Page Range
    text: 'Sometimes you only want to number a subset, such as pages 3‑10 of a 25‑page
      contract. Adjust `StartingPage` and `EndingPage` accordingly:'
  - name: Changing the Placement to Footer
    text: 'If your workflow requires **header footer numbering** at the bottom left,
      tweak the `Margin`:'
  - name: Using a Different Format
    text: 'Legal teams sometimes use “2024‑A‑001”. Just change the format string:'
  - name: Handling Transparent Backgrounds
    text: The `BackgroundColor = Color.Transparent` ensures the number doesn’t obscure
      existing content. If you need a light gray box behind the text for readability,
      replace it with `Color.LightGray`.
  type: HowTo
- questions:
  - answer: Yes—load the document with the password first (`pdfDocument = new Document("file.pdf",
      new LoadOptions { Password = "pwd" })`) then apply the same steps.
    question: Will this work with password‑protected PDFs?
  - answer: You can run `AddBatesNumbering` twice with two separate `BatesNumberingOptions`,
      each targeting either odd (`StartingPage = 1; EndingPage = pdfDocument.Pages.Count;
      PageSequence = PageSequence.Odd`) or even pages.
    question: Can I add different numbers to odd and even pages?
  - answer: A trial works for evaluation, but the trial adds a watermark. For production
      use you’ll need a valid license to get a clean **bates numbering pdf**.
    question: Do I need a license for Aspose.PDF?
  type: FAQPage
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Add Bates Numbering to PDFs with C# – Complete Guide
url: /net/programming-with-pdf-pages/add-bates-numbering-to-pdfs-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Bates Numbering to PDFs with C# – Complete Guide

Add bates numbering to your PDF files in C# with just a few lines of code. If you’ve ever needed custom page numbers for legal briefs or want sequential page numbers across a contract bundle, this tutorial has you covered.

In the next few minutes we’ll walk through everything you need to know: loading a PDF, configuring the numbering style, applying the numbers, and finally saving the updated file. By the end you’ll be able to generate a **bates numbering pdf** that looks professional, whether you’re processing a single file or an entire folder of documents.

## What You’ll Need

Before we dive in, make sure you have the following prerequisites:

- **.NET 6.0 or later** – the code targets .NET 6, but earlier versions of .NET Framework work as well.
- **Aspose.PDF for .NET** – a commercial library (free trial available) that provides the `Document` and `BatesNumberingOptions` classes used in this guide.
- A **C# IDE** (Visual Studio, Rider, or VS Code) – any editor that can compile .NET projects will do.
- An input PDF named `input.pdf` placed in a folder you can reference from your code.

Got everything? Great—let’s get started.

## Add Bates Numbering – Overview

The core idea behind **add bates numbering** is to treat the PDF as a canvas and then paint a string (like “DOC‑001”) onto each page’s header or footer. Aspose.PDF does the heavy lifting: you simply describe the format, the page range, and the visual style, and the library writes the numbers for you.

Below is the full, runnable example that you can copy‑paste into a console app. Every line is explained, so you’ll understand not only *what* to write, but *why* each piece matters.

### Step 1: Load the Source PDF Document

First we need a `Document` object that represents the file we want to modify.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Drawing;

// Load the source PDF (replace the path with your actual folder)
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Why this matters:** The `Document` class is the entry point for all PDF operations. It loads the file into memory, giving you access to the `Pages` collection, which we’ll later iterate over when adding numbers.

### Step 2: Configure Bates Numbering Options (custom page numbers)

Now we set up a `BatesNumberingOptions` object. This is where you define **custom page numbers**, the font, colors, and margins.

```csharp
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    NumberingFormat = "DOC-{0:D3}",          // e.g., DOC-001, DOC-002 …
    StartNumber = 1,
    StartingPage = 1,
    EndingPage = pdfDocument.Pages.Count,
    Font = new Font(FontFamily.Helvetica, 12, FontStyle.Bold),
    ForegroundColor = Color.Black,
    BackgroundColor = Color.Transparent,
    Margin = new Margin(0, 20, 20, 0)        // top, right, bottom, left (points)
};
```

- **NumberingFormat** – the `{0:D3}` placeholder tells Aspose to pad numbers with three digits.
- **StartNumber** – where the sequence begins; change it if you’re appending to an existing bundle.
- **StartingPage / EndingPage** – define the page range; you could limit it to 2‑5 for a subset, giving you **sequential page numbers** only where you need them.
- **Font & Colors** – visual style for the **header footer numbering**; Helvetica works well for legal documents because it’s clean and readable.
- **Margin** – positions the text 20 pts from the top and right edges; tweak these values to move the number to the bottom or left if desired.

> **Pro tip:** If you need the numbers in the footer instead of the header, swap the `Margin` values to something like `new Margin(0, 0, 20, 20)` (bottom, left).

### Step 3: Apply the Bates Numbering to the Entire Document

With the options prepared, the actual insertion is a single method call.

```csharp
// Apply the numbering to every page in the defined range
pdfDocument.AddBatesNumbering(batesOptions);
```

Behind the scenes Aspose iterates over the selected pages, formats each number according to `NumberingFormat`, and draws the string onto the page canvas. This is the heart of **add bates numbering**—no manual looping required.

### Step 4: Save the PDF with Bates Numbers Applied

Finally, write the modified document back to disk.

```csharp
// Save the output file (choose a different name to avoid overwriting the source)
pdfDocument.Save("YOUR_DIRECTORY/BatesNumbered.pdf");
```

When you open `BatesNumbered.pdf` you’ll see “DOC‑001”, “DOC‑002”, … printed in the top‑right corner of each page. That’s a fully functional **bates numbering pdf** ready for filing or e‑discovery.

## Expected Result

| Page | Header (example) |
|------|------------------|
| 1    | DOC‑001 |
| 2    | DOC‑002 |
| …    | … |
| N    | DOC‑00N |

The numbers appear exactly where the `Margin` placed them, using the Helvetica Bold 12‑pt font. If you opened the file in Adobe Acrobat, you’d notice the numbers are part of the page content—not a separate annotation—so they survive printing and flattening.

## Edge Cases & Variations

### Limiting the Page Range

Sometimes you only want to number a subset, such as pages 3‑10 of a 25‑page contract. Adjust `StartingPage` and `EndingPage` accordingly:

```csharp
batesOptions.StartingPage = 3;
batesOptions.EndingPage = 10;
batesOptions.StartNumber = 1; // reset numbering for the subset
```

### Changing the Placement to Footer

If your workflow requires **header footer numbering** at the bottom left, tweak the `Margin`:

```csharp
batesOptions.Margin = new Margin(20, 0, 0, 20); // top, right, bottom, left
```

### Using a Different Format

Legal teams sometimes use “2024‑A‑001”. Just change the format string:

```csharp
batesOptions.NumberingFormat = "2024-A-{0:D3}";
```

### Handling Transparent Backgrounds

The `BackgroundColor = Color.Transparent` ensures the number doesn’t obscure existing content. If you need a light gray box behind the text for readability, replace it with `Color.LightGray`.

## Common Questions (Answered)

- **Will this work with password‑protected PDFs?**  
  Yes—load the document with the password first (`pdfDocument = new Document("file.pdf", new LoadOptions { Password = "pwd" })`) then apply the same steps.

- **Can I add different numbers to odd and even pages?**  
  You can run `AddBatesNumbering` twice with two separate `BatesNumberingOptions`, each targeting either odd (`StartingPage = 1; EndingPage = pdfDocument.Pages.Count; PageSequence = PageSequence.Odd`) or even pages.

- **Do I need a license for Aspose.PDF?**  
  A trial works for evaluation, but the trial adds a watermark. For production use you’ll need a valid license to get a clean **bates numbering pdf**.

## Full Working Example (Copy‑Paste Ready)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Set up numbering options (custom page numbers, sequential page numbers)
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            NumberingFormat = "DOC-{0:D3}",
            StartNumber = 1,
            StartingPage = 1,
            EndingPage = pdfDocument.Pages.Count,
            Font = new Font(FontFamily.Helvetica, 12, FontStyle.Bold),
            ForegroundColor = Color.Black,
            BackgroundColor = Color.Transparent,
            Margin = new Margin(0, 20, 20, 0) // top, right, bottom, left
        };

        // 3️⃣ Apply the numbering (header footer numbering)
        pdfDocument.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the result
        pdfDocument.Save("YOUR_DIRECTORY/BatesNumbered.pdf");

        System.Console.WriteLine("Bates numbering added successfully!");
    }
}
```

Run the program, open the output file, and you’ll see the numbers exactly where the code told Aspose to put them. No extra loops, no manual drawing—just **add bates numbering** in four concise steps.

## Conclusion

You now have a solid, production‑ready way to **add bates numbering** to any PDF using C# and Aspose.PDF. From loading the document to configuring **custom page numbers**, applying **sequential page numbers**, and saving a clean **bates numbering pdf**, the entire workflow fits in a single method call.

What’s next? Try mixing this technique with other Aspose features—like stamping a logo, merging multiple PDFs, or extracting pages based on the numbers you just added. Exploring **header footer numbering** together with watermarks can give


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Aspose.PDF .NET&#58; Add Page Numbers to PDFs Using FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Add Images & Page Numbers to PDFs Using Aspose.PDF for .NET&#58; A Complete Guide](/pdf/english/net/document-manipulation/enhance-pdfs-images-page-numbers-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}