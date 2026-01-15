---
category: general
date: 2026-01-15
description: Add bates numbers to your PDF quickly with Aspose.Pdf. Learn how to add
  footer to pdf, add page numbers pdf, and add custom page numbering.
draft: false
keywords:
- add bates numbers
- bates numbering pdf
- add footer to pdf
- add page numbers pdf
- add custom page numbering
language: en
og_description: Add bates numbers to your PDF quickly with Aspose.Pdf. Learn how to
  add footer to pdf, add page numbers pdf, and add custom page numbering.
og_title: Add Bates Numbers to PDF – bates numbering pdf
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Add Bates Numbers to PDF – bates numbering pdf
url: /net/programming-with-text/add-bates-numbers-to-pdf-bates-numbering-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Bates Numbers to PDF – Complete Guide

Ever needed to **add bates numbers** to a PDF but weren’t sure where to start? You’re not alone—legal teams, auditors, and anyone dealing with massive document sets hit this snag daily. The good news? With Aspose.Pdf for .NET you can sprinkle those numbers onto every page in just a handful of lines.

In this tutorial we’ll walk through the whole process: from pulling in the Aspose.Pdf library, loading your source file, configuring a *BatesNumberingArtifact*, attaching it as a footer, and finally saving the result. By the end you’ll also know how to **add footer to pdf**, **add page numbers pdf**, and even **add custom page numbering** for those tricky edge‑cases.

## What You’ll Need

- .NET 6+ (or .NET Framework 4.8 if you’re still on the classic stack)  
- A reference to the **Aspose.Pdf** NuGet package (`Install-Package Aspose.Pdf`)  
- A PDF file you want to stamp (we’ll call it `source.pdf`)  

That’s it—no extra tools, no heavyweight PDF editors. Let’s dive in.

![add bates numbers example](https://example.com/images/add-bates-numbers.png "add bates numbers example")

## Step 1: Add Bates Numbers – Load the PDF Document

First, we need a `Document` object that represents the PDF we’re about to modify. Think of this as opening a Word document before you start typing.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the PDF you want to add bates numbers to
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // The rest of the steps go here...
    }
}
```

> **Why this matters:** Loading the file gives you access to its `Pages` collection, which is where we’ll attach the Bates numbering artifact later. If the file can’t be found, Aspose will throw a clear `FileNotFoundException`, so double‑check the path.

## Step 2: Configure bates numbering pdf Settings

Now we define *how* the numbers should look. The `BatesNumberingArtifact` lets you set a prefix, start number, digit padding, suffix, and placement. This is the core of **bates numbering pdf**.

```csharp
// Step 2: Create and configure the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    NumberDigits = 5,          // forces 5 digits, e.g., 01000
    Suffix = "-A",
    Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
};
```

> **Pro tip:** If you need the numbers to appear in the header instead, swap `BottomCenter` for `TopCenter`. The placement enum also supports `BottomLeft`, `BottomRight`, etc., giving you flexibility for different **add footer to pdf** styles.

## Step 3: Add page numbers pdf – Attach the Artifact to Every Page

With the artifact ready, we loop through each page and add it to the `Artifacts` collection. This is the step that actually **adds page numbers pdf**.

```csharp
// Step 3: Attach the artifact to each page
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

> **What’s happening under the hood?** The `Artifacts` collection is rendered after the page’s main content, ensuring the Bates number sits on top of any existing text but below annotations. If you need the number to be behind the content (rare), you’d use `page.Artifacts.Insert(0, batesArtifact)`.

## Step 4: Add custom page numbering – Save the Updated PDF

Finally, we write the modified document out to disk. The output file will contain the Bates numbers as a permanent part of each page.

```csharp
// Step 4: Save the PDF with the new numbering
pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
```

> **Verification tip:** Open `bates_out.pdf` in any viewer. You should see something like `CASE-01000-A` centered at the bottom of every page. If the numbers are missing, double‑check that the `Placement` property matches your intended location.

## Full Working Example

Putting it all together, here’s the complete, ready‑to‑run program:

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the source PDF
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // Configure Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            NumberDigits = 5,
            Suffix = "-A",
            Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
        };

        // Attach artifact to each page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.Artifacts.Add(batesArtifact);
        }

        // Save the new PDF (adds footer to pdf)
        pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

        Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
    }
}
```

### Expected Result

- **File:** `bates_out.pdf` in the same folder as `source.pdf`
- **Visual:** Bottom‑center text `CASE-01000-A`, `CASE-01001-A`, … for each subsequent page
- **Behaviour:** Numbers are permanently embedded; they survive printing, flattening, and further editing.

## Common Variations & Edge Cases

| Situation | How to Adjust |
|-----------|---------------|
| **Different starting number** | Change `StartNumber` to any integer (e.g., `StartNumber = 500`). |
| **Letter suffixes per volume** | Use a loop to modify `Suffix` per page, or create multiple artifacts with different suffixes. |
| **Right‑aligned numbering** | Set `Placement = BatesNumberingArtifact.PlacementLocation.BottomRight`. |
| **Large documents (10k+ pages)** | Consider batching pages or increasing `NumberDigits` to avoid overflow. |
| **Need to hide numbers on certain pages** | Skip those pages in the `foreach` loop (e.g., `if (page.Number != 1) page.Artifacts.Add(batesArtifact);`). |

> **Watch out for:** Using a `Prefix` or `Suffix` that contains illegal filename characters (e.g., `*` or `?`). Aspose will still embed them, but they may cause issues when you later extract the text.

## Pro Tips for Production Use

- **Cache the artifact** if you’re processing many PDFs in a row; creating it once saves a few milliseconds per file.  
- **Thread‑safety:** The `BatesNumberingArtifact` instance is not thread‑safe, so give each thread its own copy.  
- **Performance:** For massive batches, disable PDF compression (`pdfDocument.Compress = false`) before saving, then re‑enable if needed.  
- **Testing:** Always run a quick visual check on the first generated PDF to ensure placement matches your legal team’s standards.

## Conclusion

You now have a solid, end‑to‑end recipe for how to **add bates numbers** to any PDF using Aspose.Pdf, complete with options to **add footer to pdf**, **add page numbers pdf**, and **add custom page numbering**. The code is fully self‑contained, works with .NET 6 and later, and can be dropped into any existing automation pipeline.

What’s next? Try swapping the `BottomCenter` placement for a header style, experiment with dynamic prefixes (e.g., case IDs from a database), or combine this with Aspose’s text‑extraction features to generate a searchable index of your newly‑numbered documents. The sky’s the limit, and you’ve just earned a powerful tool for document control.

Happy coding, and may your PDFs always stay perfectly numbered!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}