---
category: general
date: 2025-12-25
description: How to add TOC to a PDF using Aspose.PDF in ASP.NET. Learn to add pdf
  table of contents, create toc, generate pdf asp.net and create pdf with toc.
draft: false
keywords:
- how to add toc
- add pdf table of contents
- how to create toc
- generate pdf asp.net
- create pdf with toc
language: en
og_description: How to add TOC to a PDF using Aspose.PDF. This tutorial shows how
  to add pdf table of contents, create toc, generate pdf asp.net and create pdf with
  toc.
og_title: How to Add TOC in PDF with Aspose.PDF – Complete Guide
tags:
- Aspose.PDF
- C#
- PDF generation
title: How to Add TOC in PDF with Aspose.PDF – Step‑by‑Step Guide
url: /net/programming-with-bookmarks/how-to-add-toc-in-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Add TOC in PDF with Aspose.PDF – Complete Guide

Ever wondered **how to add TOC** to a PDF without spending hours fiddling with low‑level PDF objects? You're not the only one. In many reporting or documentation projects the lack of a clickable table of contents is a real pain point, especially when the output is meant for end users who need to jump around quickly.  

Good news: Aspose.PDF makes it surprisingly easy to **add pdf table of contents**, and you can do it right from your ASP.NET code‑behind. In this tutorial we'll walk through the entire process—starting from a blank document, customizing each heading level, and finally saving a polished PDF that already contains a functional TOC. By the end you’ll also see how to **generate pdf asp.net** projects that **create pdf with toc** automatically.

## What This Tutorial Covers

* Setting up an Aspose.PDF `Document` and a dedicated TOC page.  
* Defining custom formatting for heading levels 1‑4.  
* Adding headings that automatically link back to the TOC.  
* Saving the final file and verifying the clickable entries.  

No external libraries beyond Aspose.PDF are required, and the code works with .NET 6+ as well as classic .NET Framework projects. If you’ve already got Aspose.PDF installed via NuGet, you’re ready to copy‑paste.

---

## Prerequisites

| Requirement | Why It Matters |
|-------------|----------------|
| **Aspose.PDF for .NET** (latest version) | Provides the `Document`, `Heading`, `TocInfo` classes we’ll use. |
| **Visual Studio 2022** (or any C# IDE) | Makes it easy to test the snippet in a console or ASP.NET project. |
| **Basic C# knowledge** | You’ll need to understand namespaces and loops, but the tutorial explains every line. |

If you need to add the package, run:

```bash
dotnet add package Aspose.PDF
```

Now let’s dive into the code.

---

## Step 1 – Create the PDF Document and a Dedicated TOC Page

The first thing you do when you **how to add toc** is to create an empty `Document` object and then reserve a page that will hold the table of contents. This page is separate from the content pages so the TOC stays at the beginning, just like in a printed book.

```csharp
// Step 1: Initialize a new PDF document and add a blank page for the TOC
var pdf = new Aspose.Pdf.Document();
var tocPage = pdf.Pages.Add();   // This will become the TOC page
```

*Why a separate page?*  
Aspose.PDF treats the TOC as a regular page, which means you can style it, add a title, and later insert page numbers automatically. Keeping it separate also prevents the TOC from being mixed with your main content.

---

## Step 2 – Configure TOC Information and Custom Formatting

Aspose.PDF gives you a `TocInfo` object where you can set the title, the leader style (dots, dashes, or solid lines), and an array of formatting rules—one for each heading level you plan to use.

```csharp
// Step 2: Set up TOC metadata and formatting for each heading level
var tocInfo = new Aspose.Pdf.TocInfo
{
    LineDash = Aspose.Pdf.Text.TabLeaderType.Solid,
    Title = new Aspose.Pdf.Text.TextFragment("Table Of Contents")
    {
        TextState = { FontSize = 30 }
    },
    FormatArrayLength = 4          // We will define 4 heading levels
};
tocPage.TocInfo = tocInfo;

// Level‑1 formatting (big, bold, dotted leader)
tocInfo.FormatArray[0].Margin.Left = 0;
tocInfo.FormatArray[0].Margin.Right = 30;
tocInfo.FormatArray[0].LineDash = Aspose.Pdf.Text.TabLeaderType.Dot;
tocInfo.FormatArray[0].TextState.FontStyle = Aspose.Pdf.Text.FontStyles.Bold | Aspose.Pdf.Text.FontStyles.Italic;

// Level‑2 formatting (smaller, no leader)
tocInfo.FormatArray[1].Margin.Left = 10;
tocInfo.FormatArray[1].Margin.Right = 30;
tocInfo.FormatArray[1].LineDash = Aspose.Pdf.Text.TabLeaderType.None;
tocInfo.FormatArray[1].TextState.FontSize = 10;

// Level‑3 formatting (indented, bold)
tocInfo.FormatArray[2].Margin.Left = 20;
tocInfo.FormatArray[2].Margin.Right = 30;
tocInfo.FormatArray[2].TextState.FontStyle = Aspose.Pdf.Text.FontStyles.Bold;

// Level‑4 formatting (most indented, solid leader)
tocInfo.FormatArray[3].Margin.Left = 30;
tocInfo.FormatArray[3].Margin.Right = 30;
tocInfo.FormatArray[3].LineDash = Aspose.Pdf.Text.TabLeaderType.Solid;
tocInfo.FormatArray[3].TextState.FontStyle = Aspose.Pdf.Text.FontStyles.Bold;
```

**Explanation of the key properties**

* `LineDash` – Determines what appears between the heading text and the page number (dots, solid line, or nothing).  
* `Margin.Left/Right` – Controls indentation, letting you visually nest headings.  
* `FontStyle` – You can combine `Bold`, `Italic`, `Underline`, etc., to make each level distinct.  

Feel free to tweak the values; they affect the visual hierarchy of the final TOC.

---

## Step 3 – Add a Content Page for Your Headings

Now we need somewhere to place the actual headings that the TOC will reference. In a real‑world report you’d probably have many pages, but for this demo a single page is enough.

```csharp
// Step 3: Add a page that will hold the main content headings
var contentPage = pdf.Pages.Add();
```

If you later want to generate a multi‑page report, just keep calling `pdf.Pages.Add()` wherever you need a new page.

---

## Step 4 – Create Headings, Link Them to the TOC, and Populate the Content Page

Aspose.PDF’s `Heading` class automatically registers itself with the TOC page when you set the `TocPage` property. The loop below creates four headings (levels 1‑4), assigns a sample text, and marks them as part of a list so page numbers are calculated correctly.

```csharp
// Step 4: Generate headings for levels 1‑4 and add them to the content page
for (int level = 1; level <= 4; level++)
{
    var heading = new Aspose.Pdf.Heading(level);
    var segment = new Aspose.Pdf.Text.TextSegment { Text = $"Sample Heading {level}" };
    heading.Segments.Add(segment);
    heading.IsAutoSequence = true;               // Automatic numbering (1., 1.1, etc.)
    heading.TocPage = tocPage;                   // Link this heading to the TOC page
    heading.TextState.Font = Aspose.Pdf.Text.FontRepository.FindFont("Arial Unicode MS");
    heading.IsInList = true;                     // Makes the heading part of a list for numbering
    contentPage.Paragraphs.Add(heading);
}
```

**Why use `IsAutoSequence`?**  
It automatically prefixes each heading with a number that reflects its hierarchy (e.g., “1 Sample Heading 1”, “1.1 Sample Heading 2”). This mirrors what you’d see in a Word document table of contents.

---

## Step 5 – Save the PDF and Verify the Result

The final step is a one‑liner, but it’s the moment you’ll see the fruits of your labor. The PDF will be saved to the folder you specify; just make sure the path exists and your application has write permissions.

```csharp
// Step 5: Persist the PDF to disk
pdf.Save("C:/Temp/TOC_out.pdf");
```

Open the resulting file in any PDF viewer (Adobe Reader, Edge, Chrome). You should see:

1. A **Table Of Contents** page at the very beginning, with four entries, each using the formatting you defined.  
2. Clickable links: clicking on “Sample Heading 2” takes you straight to the corresponding heading on the next page.  

If you need to embed the PDF in an ASP.NET MVC view, simply return the file stream with `FileResult`.

---

## Full Working Example (Copy‑Paste Ready)

Below is the complete, self‑contained program you can drop into a console app or an ASP.NET controller action. No other code is required.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Initialize document and TOC page
        var pdf = new Document();
        var tocPage = pdf.Pages.Add();

        // Configure TOC metadata
        var tocInfo = new TocInfo
        {
            LineDash = TabLeaderType.Solid,
            Title = new TextFragment("Table Of Contents")
            {
                TextState = { FontSize = 30 }
            },
            FormatArrayLength = 4
        };
        tocPage.TocInfo = tocInfo;

        // Level‑1 formatting
        tocInfo.FormatArray[0].Margin.Left = 0;
        tocInfo.FormatArray[0].Margin.Right = 30;
        tocInfo.FormatArray[0].LineDash = TabLeaderType.Dot;
        tocInfo.FormatArray[0].TextState.FontStyle = FontStyles.Bold | FontStyles.Italic;

        // Level‑2 formatting
        tocInfo.FormatArray[1].Margin.Left = 10;
        tocInfo.FormatArray[1].Margin.Right = 30;
        tocInfo.FormatArray[1].LineDash = TabLeaderType.None;
        tocInfo.FormatArray[1].TextState.FontSize = 10;

        // Level‑3 formatting
        tocInfo.FormatArray[2].Margin.Left = 20;
        tocInfo.FormatArray[2].Margin.Right = 30;
        tocInfo.FormatArray[2].TextState.FontStyle = FontStyles.Bold;

        // Level‑4 formatting
        tocInfo.FormatArray[3].Margin.Left = 30;
        tocInfo.FormatArray[3].Margin.Right = 30;
        tocInfo.FormatArray[3].LineDash = TabLeaderType.Solid;
        tocInfo.FormatArray[3].TextState.FontStyle = FontStyles.Bold;

        // Add a content page
        var contentPage = pdf.Pages.Add();

        // Create headings (levels 1‑4)
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

        // Save the PDF
        pdf.Save("C:/Temp/TOC_out.pdf");
    }
}
```

### Expected Output

When you open `TOC_out.pdf`, the first page reads **Table Of Contents** in 30‑pt font, followed by four entries:

```
Sample Heading 1 ........................................... 2
Sample Heading 2 ........................................... 2
Sample Heading 3 ........................................... 2
Sample Heading 4 ........................................... 2
```

Each line is a clickable link that jumps to the respective heading on page 2. The headings themselves are numbered automatically (1, 1.1, 1.1.1,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}