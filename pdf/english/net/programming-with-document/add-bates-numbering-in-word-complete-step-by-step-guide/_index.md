---
category: general
date: 2026-06-21
description: Add Bates numbering in Word quickly. Learn how to add Bates, apply Bates
  numbering for legal docs, and automate numbering with C#.
draft: false
keywords:
- add bates numbering
- how to add bates
- bates numbering in word
- bates numbering for legal
- apply bates numbering
language: en
og_description: Add Bates numbering in Word using C#. This guide shows how to add
  Bates, apply Bates numbering for legal documents, and automate the process.
og_title: Add Bates Numbering in Word – Full Programming Walkthrough
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  headline: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  name: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: '| Page | Bates Number | |------|--------------| | 1 | ABC-1000 | | 2 |
      ABC-1001 | | … | … | | N | ABC‑(1000 + N‑1) |'
  - name: What if the document already contains page numbers?
    text: The `AddBatesNumbering` method will **not** overwrite existing page number
      fields; it simply adds a new field. If you want to replace the existing numbers,
      remove them first or set `batesOptions.Position` to the same location as the
      current page numbers.
  - name: Can I skip pages (e.g., exclude a cover page)?
    text: 'Yes. Use the overload that accepts a `PageRange`:'
  - name: How do I change the numbering format (Roman numerals, letters)?
    text: 'The `BatesNumberingOptions` class supports a `NumberFormat` property:'
  - name: What about performance on huge files?
    text: Loading a 2‑GB Word file can consume a lot of RAM. To mitigate, process
      the document in chunks using the `DocumentSplitter` utility, apply Bates numbering
      to each chunk, then merge the parts back together. This pattern keeps memory
      usage under control while still letting you **apply bates numbering*
  type: HowTo
tags:
- document‑automation
- csharp
- legal‑tech
title: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
url: /net/programming-with-document/add-bates-numbering-in-word-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Bates Numbering in Word – Complete Step‑by‑Step Guide

Ever wondered how to add Bates numbering to a Word file without manually typing each number? You’re not alone. Many lawyers, paralegals, and e‑discovery specialists need a reliable way to **add Bates numbering** to hundreds of pages, and doing it by hand is a nightmare.

In this tutorial we’ll walk through a clean C# solution that **applies Bates numbering** to a `.docx` file, explains why each line matters, and shows you how to tweak the code for legal‑specific needs. By the end you’ll be able to generate a perfectly numbered document in seconds—no extra plugins required.

## What You’ll Learn

- The exact code required to **add Bates numbering** to a Word document.
- How the `BatesNumberingOptions` class works and why you might adjust the prefix or start value.
- Tips for using this approach on large case files, including memory‑wise considerations.
- A quick rundown of prerequisites so you can copy‑paste the solution and run it today.

**Prerequisites**  
- .NET 6+ (or .NET Framework 4.7.2+ if you prefer the older runtime).  
- A reference to the Aspose.Words for .NET library (or any similar API that exposes `AddBatesNumbering`).  
- Basic familiarity with C# and Visual Studio (or your favourite IDE).

If you’re comfortable with those, let’s dive in.

## Step 1: Set Up the Project and Import the Library

First, create a new console app (or integrate into an existing service). Then add the Aspose.Words NuGet package:

```bash
dotnet add package Aspose.Words
```

> **Pro tip:** Use the free evaluation license for testing; it adds a small watermark but otherwise works exactly like the full version.

```csharp
using Aspose.Words;
using Aspose.Words.BatesNumbering;
```

These `using` statements bring the `Document` and `BatesNumberingOptions` classes into scope, which are essential for the **apply bates numbering** step later on.

## Step 2: Load the Source Document

You’ll need a Word file to work on. The code below loads `input.docx` from a folder you specify. Replace `"YOUR_DIRECTORY"` with the actual path on your machine.

```csharp
// Step 1: Load the source document
var document = new Document("YOUR_DIRECTORY/input.docx");
```

Why load the file first? The `Document` object parses the entire Word package into memory, allowing us to manipulate headers, footers, and page layouts before saving. If the file is massive (think 10,000 pages), consider using `LoadOptions` with `LoadFormat.Docx` to stream sections instead of loading everything at once.

## Step 3: Configure Bates Numbering Options

This is where the magic happens. You tell the library what prefix to use (`"ABC-"` in the example) and where to start counting (`1000`). Both values are fully customizable.

```csharp
// Step 2: Define Bates numbering options (prefix and starting number)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",
    Start = 1000,
    // Optional: set the position, alignment, and font if you need legal‑specific styling
    // Position = BatesNumberingPosition.Footer,
    // Alignment = BatesNumberingAlignment.Right,
    // Font = new Font("Times New Roman", 10, FontStyle.Bold)
};
```

**Why a prefix?** In legal practice, prefixes often identify the case or the producing party (`"ABC-"` could stand for *Acme Bank Corp.*). Starting at `1000` is common because many firms reserve the first 999 numbers for internal drafts.

If you’re dealing with **Bates numbering for legal** documents, you might also want to set `batesOptions.Position` to `Header` or `Footer` and adjust the alignment to match court rules. The library supports these tweaks out of the box.

## Step 4: Apply Bates Numbering to the Entire Document

Now we actually inject the numbers. The `AddBatesNumbering` method walks through every page, inserts the formatted string, and updates the document’s internal page count.

```csharp
// Step 3: Apply Bates numbering to the entire document
document.AddBatesNumbering(batesOptions);
```

Behind the scenes, Aspose.Words creates a hidden field on each page that renders as `ABC-1000`, `ABC-1001`, and so on. Because it’s a field, you can later edit the prefix or start number without regenerating the whole file—handy for **how to add bates** after a discovery request changes.

## Step 5: Save the Modified Document

Finally, write the output to a new file. Keeping the original untouched is a best practice, especially when dealing with evidence that must remain pristine.

```csharp
// Step 4: Save the modified document
document.Save("YOUR_DIRECTORY/output.docx");
```

You now have `output.docx` with sequential Bates numbers appended to every page. Open it in Word, and you’ll see the numbers exactly where you specified (footer by default). The file size may increase slightly because of the extra fields, but it’s negligible compared to the benefits.

### Expected Output

| Page | Bates Number |
|------|--------------|
| 1    | ABC-1000     |
| 2    | ABC-1001     |
| …    | …            |
| N    | ABC‑(1000 + N‑1) |

If you open the document’s “Field Codes” view (`Alt+F9` in Word), you’ll see something like `{ BATES \* MERGEFORMAT ABC-1000 }` on each page.

## Edge Cases & Common Questions

### What if the document already contains page numbers?

The `AddBatesNumbering` method will **not** overwrite existing page number fields; it simply adds a new field. If you want to replace the existing numbers, remove them first or set `batesOptions.Position` to the same location as the current page numbers.

### Can I skip pages (e.g., exclude a cover page)?

Yes. Use the overload that accepts a `PageRange`:

```csharp
var range = new PageRange(2, document.PageCount); // start at page 2
document.AddBatesNumbering(batesOptions, range);
```

This is useful when you need **bates numbering for legal** briefs that start after a title page.

### How do I change the numbering format (Roman numerals, letters)?

The `BatesNumberingOptions` class supports a `NumberFormat` property:

```csharp
batesOptions.NumberFormat = BatesNumberFormat.RomanUpper;
```

Set it before calling `AddBatesNumbering`. This flexibility helps when a court mandates a specific style.

### What about performance on huge files?

Loading a 2‑GB Word file can consume a lot of RAM. To mitigate, process the document in chunks using the `DocumentSplitter` utility, apply Bates numbering to each chunk, then merge the parts back together. This pattern keeps memory usage under control while still letting you **apply bates numbering** efficiently.

## Full Working Example

Putting everything together, here’s a ready‑to‑run console program:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.BatesNumbering;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            var inputPath = @"C:\Docs\input.docx";
            var document = new Document(inputPath);

            // 2️⃣ Define Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                // Optional styling for legal compliance
                Position = BatesNumberingPosition.Footer,
                Alignment = BatesNumberingAlignment.Right,
                Font = new Font("Times New Roman", 9, FontStyle.Bold)
            };

            // 3️⃣ Apply Bates numbering across all pages
            document.AddBatesNumbering(batesOptions);

            // 4️⃣ Save the result
            var outputPath = @"C:\Docs\output.docx";
            document.Save(outputPath);

            Console.WriteLine($"✅ Bates numbering applied! Saved to {outputPath}");
        }
    }
}
```

Run the program, open `output.docx`, and you’ll see a clean series of numbers ready for filing, discovery, or court submission.

## Conclusion

You now know exactly **how to add Bates** to a Word document using C#. The steps—load, configure, apply, and save—are straightforward, yet flexible enough to satisfy **Bates numbering for legal** workflows, custom prefixes, and even large‑scale batch processing. 

If you’re ready to take this further, consider:

- Integrating the code into a web API so colleagues can upload files and receive numbered PDFs instantly.  
- Adding error handling for missing files or permission issues (a quick `try/catch` around `Document.Load`).  
- Exploring other Aspose.Words features like watermarks or redaction for a full‑suite e‑discovery toolkit.

Feel free to experiment with different prefixes, start numbers, or even combine multiple numbering schemes in the same document. The world of **apply bates numbering** is surprisingly versatile once you have the core logic under your belt.

Got questions or a tricky scenario? Drop a comment below, and we’ll troubleshoot together. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Apply Numbering Style in Heading of PDF using Java](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/french/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}