---
category: general
date: 2026-07-03
description: Bates numbering tutorial showing how to add bates numbering pdf files
  using Aspose.PDF. Includes prefix bates number setup and a complete bates numbering
  example.
draft: false
keywords:
- bates numbering tutorial
- add bates numbering pdf
- bates numbering example
- prefix bates number
language: en
og_description: Bates numbering tutorial that walks you through adding bates numbering
  pdf files, setting a prefix bates number, and delivering a full working example.
og_title: 'Bates Numbering Tutorial: Add Numbers to PDF with Aspose'
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Bates numbering tutorial showing how to add bates numbering pdf files
    using Aspose.PDF. Includes prefix bates number setup and a complete bates numbering
    example.
  headline: 'Bates Numbering Tutorial: Add Numbers to PDF with Aspose'
  type: TechArticle
- description: Bates numbering tutorial showing how to add bates numbering pdf files
    using Aspose.PDF. Includes prefix bates number setup and a complete bates numbering
    example.
  name: 'Bates Numbering Tutorial: Add Numbers to PDF with Aspose'
  steps:
  - name: What if I need to reset the counter for each section?
    text: You can call `pdfDocument.BatesNumbering.Reset()` before processing a new
      range of pages. Combine it with a loop over `pdfDocument.Pages` and set `Start`
      again for each section.
  - name: How do I apply different prefixes to different page ranges?
    text: 'Create multiple `BatesNumbering` objects—one per range—by cloning the document
      or by using the `Add` method (available in newer Aspose versions). Here’s a
      quick sketch:'
  - name: Does the library support Unicode prefixes?
    text: Absolutely. Pass any Unicode string (e.g., `"案件‑"`). Aspose.PDF handles
      right‑to‑left scripts and special symbols without extra configuration.
  - name: What about PDF security—will Bates numbering break encryption?
    text: If the source PDF is encrypted, you must provide the password before accessing
      `BatesNumbering`. The numbering process respects the original encryption settings—your
      output will stay encrypted unless you explicitly change it.
  type: HowTo
tags:
- Aspose.PDF
- PDF processing
- Bates numbering
title: 'Bates Numbering Tutorial: Add Numbers to PDF with Aspose'
url: /net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-numbers-to-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates Numbering Tutorial – Adding Bates Numbers to PDFs with Aspose

Ever needed a **bates numbering tutorial** because you had to tag thousands of pages for litigation? You're not alone. In many legal and compliance workflows, a reliable way to *add bates numbering pdf* files is a non‑negotiable requirement. Fortunately, Aspose.PDF makes the whole process a piece of cake, and in this guide we’ll walk through a complete **bates numbering example** that you can drop straight into your project.

> **What you’ll get:** a runnable code snippet that sets the starting number, applies a **prefix bates number**, and saves the result—all in under 30 lines of C#.

## Prerequisites

Before we dive in, make sure you have:

- .NET 6.0 or later (the API works the same on .NET Framework 4.6+)
- A valid Aspose.PDF for .NET license (or you can use the free evaluation mode)
- An input PDF named `input.pdf` placed in a folder you control
- Visual Studio 2022 or any editor that understands C# projects

No extra NuGet packages beyond `Aspose.Pdf` are required.

## Step 1: Install Aspose.PDF for .NET

Open your terminal (or Package Manager Console) and run:

```bash
dotnet add package Aspose.Pdf
```

Or, if you prefer the UI, right‑click **Dependencies → Manage NuGet Packages**, search for *Aspose.Pdf*, and click **Install**. This pulls in the latest stable version (as of July 2026, version 23.12).

## Step 2: Open the Source PDF Document

The first line of any **add bates numbering pdf** workflow is to load the file you want to stamp. We’ll wrap the operation in a `using` block so the document is disposed automatically.

```csharp
using Aspose.Pdf;

// Step 2: Load the PDF you want to number
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here...
}
```

> **Pro tip:** If your PDF lives in a cloud bucket, you can feed a `Stream` instead of a file path—Aspose.PDF handles both seamlessly.

## Step 3: Set the Starting Number and Prefix

Now comes the heart of the **bates numbering example**: telling Aspose where to start and what text should precede each number. The `BatesNumbering` property exposes both `Start` and `Prefix`.

```csharp
    // Step 3a: Define where the numbering begins
    pdfDocument.BatesNumbering.Start = 1000;   // you can start anywhere

    // Step 3b: Add a custom prefix – this is the prefix bates number you asked for
    pdfDocument.BatesNumbering.Prefix = "ABC-";
```

Why bother with a prefix? In many legal cases the prefix identifies the case file, the department, or the production batch. Using `"ABC-"` as a placeholder, you could change it to `"CASE42-"` or any string that fits your naming convention.

## Step 4: Choose Where the Numbers Appear (Optional)

Aspose defaults to placing the number in the lower‑right corner, but you can move it anywhere by tweaking the `Location` property. This step isn’t mandatory for a basic **add bates numbering pdf** operation, yet it’s handy to know.

```csharp
    // Optional: Move the number to the top‑left corner
    pdfDocument.BatesNumbering.Location = new Location(10, pdfDocument.Pages[1].PageInfo.Height - 30);
```

The `Location` takes X and Y coordinates measured in points (1 pt ≈ 1/72 in). Adjust as needed for your page layout.

## Step 5: Save the Updated PDF

Finally, persist the changes. The `Save` method on `BatesNumbering` writes a new file while preserving the original untouched.

```csharp
    // Step 5: Write the output file with numbering applied
    pdfDocument.BatesNumbering.Save("YOUR_DIRECTORY/output.pdf");
}
```

When you open `output.pdf`, each page will show something like `ABC-1000`, `ABC-1001`, … up to the last page.

## Full Working Example

Putting it all together, here’s the **bates numbering example** you can copy‑paste into a console app’s `Main` method:

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // Path configuration – adjust to your environment
        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        // Load the PDF
        using (var pdfDocument = new Document(inputPath))
        {
            // Set start number and prefix
            pdfDocument.BatesNumbering.Start = 1000;
            pdfDocument.BatesNumbering.Prefix = "ABC-";

            // (Optional) Change location – comment out if default is fine
            // pdfDocument.BatesNumbering.Location = new Location(10, pdfDocument.Pages[1].PageInfo.Height - 30);

            // Save the numbered PDF
            pdfDocument.BatesNumbering.Save(outputPath);
        }

        Console.WriteLine($"Bates numbering applied! Check: {outputPath}");
    }
}
```

**Expected output** (in the console):

```
Bates numbering applied! Check: YOUR_DIRECTORY\output.pdf
```

Open the generated PDF and you’ll see sequential numbers prefixed with `ABC-` starting at `1000`.

## Common Questions & Edge Cases

### What if I need to reset the counter for each section?

You can call `pdfDocument.BatesNumbering.Reset()` before processing a new range of pages. Combine it with a loop over `pdfDocument.Pages` and set `Start` again for each section.

### How do I apply different prefixes to different page ranges?

Create multiple `BatesNumbering` objects—one per range—by cloning the document or by using the `Add` method (available in newer Aspose versions). Here’s a quick sketch:

```csharp
// Number first 10 pages with "PRE‑"
pdfDocument.BatesNumbering.Start = 1;
pdfDocument.BatesNumbering.Prefix = "PRE-";
pdfDocument.BatesNumbering.Save(outputPath, new PageRange(1, 10));

// Number the rest with "POST‑"
pdfDocument.BatesNumbering.Start = 1;
pdfDocument.BatesNumbering.Prefix = "POST-";
pdfDocument.BatesNumbering.Save(outputPath, new PageRange(11, pdfDocument.Pages.Count));
```

### Does the library support Unicode prefixes?

Absolutely. Pass any Unicode string (e.g., `"案件‑"`). Aspose.PDF handles right‑to‑left scripts and special symbols without extra configuration.

### What about PDF security—will Bates numbering break encryption?

If the source PDF is encrypted, you must provide the password before accessing `BatesNumbering`. The numbering process respects the original encryption settings—your output will stay encrypted unless you explicitly change it.

```csharp
pdfDocument.Encrypt(new DocumentEncryption("ownerPwd", "userPwd"));
```

## Tips & Best Practices

- **Batch processing:** Wrap the whole routine in a `foreach` loop to handle dozens of files automatically.
- **Logging:** Emit the start number, prefix, and output path to a log file; this eases audit trails for legal teams.
- **Performance:** For huge PDFs (500 + pages), consider enabling **memory optimization** via `pdfDocument.OptimizeMemory = true;`.
- **Testing:** Always keep a copy of the original PDF; Bates numbering is irreversible once saved.

## Conclusion

In this **bates numbering tutorial** we’ve covered everything you need to **add bates numbering pdf** files with Aspose.PDF:

1. Install the library.
2. Load your source document.
3. Set the starting number and a **prefix bates number**.
4. (Optionally) adjust the placement.
5. Save the result.

You now have a solid **bates numbering example** that you can adapt to any legal, archival, or compliance workflow. Want to go further? Try combining Bates numbers with watermarks, or generate a CSV manifest that maps each page to its identifier. The sky’s the limit, and Aspose gives you the tools to get there.

---

*Ready to put this into production? Drop a comment if you hit any snags, and happy coding!*


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Apply Numbering Style in Heading of PDF using Java](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Aspose Pdf Net Floatingbox Page Numbering](/pdf/german/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}