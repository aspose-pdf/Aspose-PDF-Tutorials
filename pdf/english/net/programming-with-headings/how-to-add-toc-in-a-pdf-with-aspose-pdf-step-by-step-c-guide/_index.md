---
category: general
date: 2025-12-23
description: How to add TOC to a PDF quickly. Learn to add table of contents, format
  it, and save PDF document using Aspose.PDF in C#.
draft: false
keywords:
- how to add toc
- add table of contents
- how to create pdf
- save pdf document
- how to format toc
language: en
og_description: How to add TOC to a PDF using Aspose.PDF. This guide shows you how
  to create PDF, format the table of contents, and save the document.
og_title: How to Add TOC in a PDF – Complete C# Tutorial
tags:
- Aspose.PDF
- C#
- PDF generation
title: How to Add TOC in a PDF with Aspose.PDF – Step‑by‑Step C# Guide
url: /net/programming-with-headings/how-to-add-toc-in-a-pdf-with-aspose-pdf-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Add TOC in a PDF with Aspose.PDF – Complete C# Tutorial

Ever wondered **how to add TOC** to a PDF without spending hours fiddling with low‑level PDF objects? You're not alone. Many developers need a clean, clickable Table of Contents (TOC) for reports, manuals, or e‑books, and Aspose.PDF makes it surprisingly straightforward.

In this tutorial we’ll walk through **how to add a table of contents**, **how to format the TOC**, and **how to create PDF** files that you can later **save PDF document** to disk. By the end you’ll have a fully functional PDF with a multi‑level TOC, ready for distribution.

## Prerequisites – What You’ll Need Before You Start

- **Aspose.PDF for .NET** (latest version; the API shown targets 23.x but works with earlier 20.x releases)
- **.NET 6.0** or later (any recent .NET runtime will do)
- A **C# IDE** such as Visual Studio 2022 (or VS Code with the C# extension)
- Basic familiarity with C# syntax (if you’ve written a “Hello World” before, you’re good)

No additional NuGet packages are required beyond `Aspose.Pdf`. If you haven’t installed it yet, run:

```bash
dotnet add package Aspose.Pdf
```

Now that the groundwork is laid, let’s dive into the code.

## Step 1: Create a New PDF Document (How to Create PDF)

The first thing you must do is instantiate a fresh `Document` object. Think of it as opening a blank notebook where every page you add will later become part of the final PDF.

```csharp
// Step 1: Create a new PDF document
using (var pdfDoc = new Aspose.Pdf.Document())
{
    // All further operations happen inside this using block
```

> **Why this matters:** The `Document` class is the entry point for every Aspose.PDF operation. By wrapping it in a `using` statement we guarantee that all unmanaged resources are released once we’re done, which is especially important when **saving PDF document** to disk.

## Step 2: Add a TOC Page and Set Its Title

A TOC needs its own dedicated page. Here we add a page to the document and configure a `TocInfo` object that holds the title and visual style of the TOC.

```csharp
    // Step 2: Add a page for the Table of Contents (TOC) and set its title
    var tocPage = pdfDoc.Pages.Add();
    var tocInfo = new Aspose.Pdf.TocInfo
    {
        LineDash = Aspose.Pdf.Text.TabLeaderType.Solid,
        Title = new Aspose.Pdf.Text.TextFragment("Table Of Contents")
        {
            TextState = { FontSize = 30 }
        }
    };
    tocPage.TocInfo = tocInfo;
```

> **Pro tip:** Setting `LineDash` to `Solid` makes the dotted leader lines appear between entry text and page numbers. You can change it later when we **format the TOC**.

## Step 3: Define Custom Formatting for Four TOC Levels (How to Format TOC)

Most documents have hierarchical headings. Aspose.PDF lets you define up to 10 levels; we’ll configure four, each with its own margin, font style, and leader type.

```csharp
    // Step 3: Define custom formatting for four TOC levels
    tocInfo.FormatArrayLength = 4;

    // Level 1
    tocInfo.FormatArray[0].Margin.Left = 0;
    tocInfo.FormatArray[0].Margin.Right = 30;
    tocInfo.FormatArray[0].LineDash = Aspose.Pdf.Text.TabLeaderType.Dot;
    tocInfo.FormatArray[0].TextState.FontStyle = Aspose.Pdf.Text.FontStyles.Bold |
                                                  Aspose.Pdf.Text.FontStyles.Italic;

    // Level 2
    tocInfo.FormatArray[1].Margin.Left = 10;
    tocInfo.FormatArray[1].Margin.Right = 30;
    tocInfo.FormatArray[1].LineDash = Aspose.Pdf.Text.TabLeaderType.None;
    tocInfo.FormatArray[1].TextState.FontSize = 10;

    // Level 3
    tocInfo.FormatArray[2].Margin.Left = 20;
    tocInfo.FormatArray[2].Margin.Right = 30;
    tocInfo.FormatArray[2].TextState.FontStyle = Aspose.Pdf.Text.FontStyles.Bold;

    // Level 4
    tocInfo.FormatArray[3].Margin.Left = 30;
    tocInfo.FormatArray[3].Margin.Right = 30;
    tocInfo.FormatArray[3].LineDash = Aspose.Pdf.Text.TabLeaderType.Solid;
    tocInfo.FormatArray[3].TextState.FontStyle = Aspose.Pdf.Text.FontStyles.Bold;
```

> **Why we set margins:** Indentation makes the hierarchy obvious to readers. The `LineDash` property controls the leader line (dots, solid line, or none). Adjust these values to match your branding guidelines.

## Step 4: Add Content Pages and Create Headings That Populate the TOC

Now we add a regular content page and sprinkle headings of various levels. Each heading automatically registers itself with the TOC page we created earlier.

```csharp
    // Step 4: Add a content page and create headings that will appear in the TOC
    var contentPage = pdfDoc.Pages.Add();

    for (int level = 1; level <= 4; level++)
    {
        var heading = new Aspose.Pdf.Heading(level);
        var segment = new Aspose.Pdf.Text.TextSegment { Text = $"Sample Heading {level}" };
        heading.Segments.Add(segment);
        heading.IsAutoSequence = true;          // Auto‑number the heading
        heading.TocPage = tocPage;             // Link to the TOC page
        heading.TextState.Font = Aspose.Pdf.Text.FontRepository.FindFont("Arial Unicode MS");
        heading.IsInList = true;               // Makes it appear as a list item in the TOC
        contentPage.Paragraphs.Add(heading);
    }
```

> **What’s happening under the hood:** The `Heading` class not only renders the text on the page but also registers an entry in the `TocInfo` we set up earlier. By assigning `TocPage`, you tell Aspose where to collect these entries.

## Step 5: Save the PDF Document (Save PDF Document)

Finally, we persist the document to disk. Change the path to match your environment.

```csharp
    // Step 5: Save the PDF with the custom TOC
    pdfDoc.Save("YOUR_DIRECTORY/TOC_out.pdf");
}
```

> **Tip for production:** Use `pdfDoc.Save("output.pdf", SaveFormat.PdfA_1b)` if you need PDF/A compliance for archival purposes.

---

### Full Working Example

Below is the complete, copy‑and‑paste‑ready code that implements every step we discussed. No pieces are missing, so you can run it immediately after adding the Aspose.PDF NuGet package.

```csharp
// Full example: how to add toc, add table of contents, and save pdf document
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Step 1: Create a new PDF document
        using (var pdfDoc = new Document())
        {
            // Step 2: Add a page for the Table of Contents (TOC) and set its title
            var tocPage = pdfDoc.Pages.Add();
            var tocInfo = new TocInfo
            {
                LineDash = TabLeaderType.Solid,
                Title = new TextFragment("Table Of Contents")
                {
                    TextState = { FontSize = 30 }
                }
            };
            tocPage.TocInfo = tocInfo;

            // Step 3: Define custom formatting for four TOC levels
            tocInfo.FormatArrayLength = 4;

            // Level 1
            tocInfo.FormatArray[0].Margin.Left = 0;
            tocInfo.FormatArray[0].Margin.Right = 30;
            tocInfo.FormatArray[0].LineDash = TabLeaderType.Dot;
            tocInfo.FormatArray[0].TextState.FontStyle = FontStyles.Bold | FontStyles.Italic;

            // Level 2
            tocInfo.FormatArray[1].Margin.Left = 10;
            tocInfo.FormatArray[1].Margin.Right = 30;
            tocInfo.FormatArray[1].LineDash = TabLeaderType.None;
            tocInfo.FormatArray[1].TextState.FontSize = 10;

            // Level 3
            tocInfo.FormatArray[2].Margin.Left = 20;
            tocInfo.FormatArray[2].Margin.Right = 30;
            tocInfo.FormatArray[2].TextState.FontStyle = FontStyles.Bold;

            // Level 4
            tocInfo.FormatArray[3].Margin.Left = 30;
            tocInfo.FormatArray[3].Margin.Right = 30;
            tocInfo.FormatArray[3].LineDash = TabLeaderType.Solid;
            tocInfo.FormatArray[3].TextState.FontStyle = FontStyles.Bold;

            // Step 4: Add a content page and create headings that will appear in the TOC
            var contentPage = pdfDoc.Pages.Add();

            for (int level = 1; level <= 4; level++)
            {
                var heading = new Heading(level);
                var segment = new TextSegment { Text = $"Sample Heading {level}" };
                heading.Segments.Add(segment);
                heading.IsAutoSequence = true;
                heading.TocPage = tocPage;
                heading.TextState.Font = FontRepository.FindFont("Arial Unicode MS");
                heading.IsInList = true;
                contentPage.Paragraphs.Add(heading);
            }

            // Step 5: Save the PDF with the custom TOC
            pdfDoc.Save("TOC_out.pdf");
        }
    }
}
```

**Expected output:**  
- Page 1: “Table Of Contents” title with four entries (`Sample Heading 1` … `Sample Heading 4`).  
- Page 2: The four headings, each styled according to the level‑specific formatting we defined.

![how to add toc example](toc-example.png){alt="how to add toc example"}

---

## Common Questions & Edge Cases

### Can I add more than four levels?

Absolutely. `TocInfo.FormatArrayLength` can be set up to 10. Just remember to configure each `FormatArray[i]` entry; otherwise the default style will be applied.

### What if I need a clickable TOC (hyperlinks)?

Aspose.PDF automatically creates internal links when you set `heading.TocPage`. If you want external URLs, use `TextFragment.Action = new GoToAction(pageNumber)` or `UriAction`.

### How do I change the TOC title after it’s been created?

Simply modify `tocInfo.Title.Text` before saving:

```csharp
tocInfo.Title.Text = "Contents";
```

### Is there a way to export the TOC as a separate PDF?

Yes. After the document is built, you can extract `tocPage` and save it alone:

```csharp
var tocOnly = new Document();
tocOnly.Pages.Add(tocPage);
tocOnly.Save("TOC_only.pdf");
```

### What about PDF/A compliance?

When you call `pdfDoc.Save`, pass a `PdfSaveOptions` object with `PdfCompliance = PdfCompliance.PdfA1b`. The TOC will still work, and the file will meet archival standards.

---

## Recap – What We Covered

- **How to add TOC**: Created a dedicated TOC page and linked headings.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}