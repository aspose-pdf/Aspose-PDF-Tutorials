---
category: general
date: 2025-12-25
description: Create PDF document and learn how to add toc, format toc, and set toc
  using Aspose.PDF in C#. Step‑by‑step code and tips.
draft: false
keywords:
- create pdf document
- how to create pdf
- how to add toc
- how to format toc
- how to set toc
language: en
og_description: Create PDF document and see how to add toc, format toc, and set toc
  in C#. Full example and best practices.
og_title: Create PDF Document with Table of Contents – Aspose.PDF Tutorial
tags:
- Aspose.PDF
- C#
- PDF generation
title: Create PDF Document with Table of Contents – Complete Aspose.PDF Guide
url: /net/programming-with-bookmarks/create-pdf-document-with-table-of-contents-complete-aspose-p/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create PDF Document with Table of Contents – Complete Aspose.PDF Guide

Ever needed to **create PDF document** programmatically and also provide a neat table of contents? You’re not the only one scratching your head over that. Whether you’re building a reporting engine or an e‑book generator, a searchable TOC makes your PDF feel professional and user‑friendly.

In this tutorial we’ll walk through **how to create pdf** files with Aspose.PDF, then show **how to add toc**, **how to format toc**, and finally explain **how to set toc** properties for multi‑level headings. By the end you’ll have a single, runnable C# file that spits out a polished PDF with a custom‑styled TOC.

## What You’ll Need

- **Aspose.PDF for .NET** (any recent version, e.g., 23.12).  
- A .NET development environment (Visual Studio, Rider, or VS Code).  
- Basic C# knowledge – nothing fancy, just the ability to run a console app.  

No extra NuGet packages are required beyond Aspose.PDF, and the code works on .NET 6+ as well as .NET Framework 4.7.2.

---

## Create PDF Document – Project Setup

First, create a new console project and add the Aspose.PDF package:

```bash
dotnet new console -n PdfTocDemo
cd PdfTocDemo
dotnet add package Aspose.PDF
```

Now open `Program.cs`. At the top, bring in the namespaces we’ll use:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

> **Pro tip:** Keep your `using` statements tidy; it helps the compiler and makes the file easier to scan.

---

## Step 1: Initialize the PDF Document

Creating the PDF document is the foundation of **how to create pdf** files with Aspose. Think of the `Document` object as a blank canvas.

```csharp
// Step 1: Create a new PDF document
using (var pdfDocument = new Document())
{
    // All further operations happen inside this using block.
```

The `using` ensures the file is flushed and resources are released automatically.  

---

## Step 2: Add a Table of Contents Page and Set Its Title

A TOC page lives like any other page, but we give it special metadata (`TocInfo`). This is where **how to add toc** really starts.

```csharp
    // Step 2: Add a page for the Table of Contents and set its title
    var tocPage = pdfDocument.Pages.Add();
    var tocInfo = new TocInfo();

    var titleFragment = new TextFragment("Table Of Contents");
    titleFragment.TextState.FontSize = 20;
    titleFragment.TextState.FontStyle = FontStyles.Bold;
    tocInfo.Title = titleFragment;
    tocPage.TocInfo = tocInfo;
```

The title appears at the top of the TOC page, styled in 20‑point bold text. You can swap the string for any language or branding you need.

---

## Step 3: Configure TOC Appearance – How to Format TOC

Aspose lets you hide page numbers, set margins, and assign distinct styles per outline level. Here’s a compact yet flexible configuration that answers **how to format toc** for four hierarchy levels.

```csharp
    // Step 3: Configure TOC to hide page numbers and define formatting for 4 levels
    tocInfo.IsShowPageNumbers = false;   // we’ll hide numbers for a cleaner look
    tocInfo.FormatArrayLength = 4;       // we support up to 4 heading levels

    // Level 1 formatting – bold & italic, no right margin
    tocInfo.FormatArray[0].Margin.Right = 0;
    tocInfo.FormatArray[0].TextState.FontStyle = FontStyles.Bold | FontStyles.Italic;

    // Level 2 formatting – left indent, underline, smaller font
    tocInfo.FormatArray[1].Margin.Left = 30;
    tocInfo.FormatArray[1].TextState.Underline = true;
    tocInfo.FormatArray[1].TextState.FontSize = 10;

    // Level 3 formatting – just bold
    tocInfo.FormatArray[2].TextState.FontStyle = FontStyles.Bold;

    // Level 4 formatting – also bold (you could change color here)
    tocInfo.FormatArray[3].TextState.FontStyle = FontStyles.Bold;
```

Feel free to tweak `Margin.Left`, `FontSize`, or add `TextState.FontColor` for extra flair. The key is that each level can look completely different, which is the essence of **how to format toc**.

---

## Step 4: Insert Content Pages and Headings – How to Set TOC

Now we add a regular content page and populate it with headings that will automatically appear in the TOC. This demonstrates **how to set toc** references.

```csharp
    // Step 4: Add a regular content page
    var contentPage = pdfDocument.Pages.Add();

    // Step 5: Insert headings of levels 1‑4, linking each to the TOC page
    for (int level = 1; level <= 4; level++)
    {
        var heading = new Heading(level);
        var textSegment = new TextSegment();

        heading.TocPage = tocPage;               // associate with TOC
        heading.Segments.Add(textSegment);
        heading.IsAutoSequence = true;           // automatic numbering (1., 1.1., etc.)
        textSegment.Text = $"this is heading of level {level}";
        heading.IsInList = true;                 // include in TOC list

        contentPage.Paragraphs.Add(heading);
    }
```

Each `Heading` object knows its level (`1`‑`4`) and automatically registers itself in the TOC because we set `IsInList = true`. The `IsAutoSequence` flag gives you hierarchical numbering without extra code—perfect for large documents.

---

## Step 5: Save the PDF

Finally, write the file to disk. Change the path to a folder you have write access to.

```csharp
    // Step 6: Save the PDF with the generated Table of Contents
    pdfDocument.Save("TOC_out.pdf");
}
```

When you open `TOC_out.pdf`, you’ll see a first page titled **Table Of Contents**, followed by four headings styled according to the rules we set earlier. No page numbers appear beside the entries because we disabled them in `tocInfo.IsShowPageNumbers`.

---

## Expected Result & Quick Verification

| Page | Content |
|------|---------|
| **1** | “Table Of Contents” header, four entries (Level 1‑4) with custom styles. |
| **2** | Four headings, each numbered automatically (e.g., “1 this is heading of level 1”). |

Open the PDF in any viewer; clicking a TOC entry should jump to the corresponding heading. If it doesn’t, double‑check that `heading.TocPage = tocPage;` is set correctly.

---

## Common Questions & Edge Cases

### What if I need more than four levels?
Increase `tocInfo.FormatArrayLength` and add extra `FormatArray` entries. Just remember that very deep hierarchies can become unreadable—keep it under six levels for most use‑cases.

### Can I show page numbers for some levels only?
Set `tocInfo.IsShowPageNumbers = true` globally, then override per‑level using `tocInfo.FormatArray[i].IsShowPageNumbers = false` for the levels you want to hide.

### How do I change the TOC font family?
Add `tocInfo.FormatArray[i].TextState.Font = FontRepository.FindFont("Arial");` for each level you wish to customize.

### Is it possible to generate the TOC after adding all content?
Yes. Aspose lets you call `pdfDocument.GenerateToc();` after the document is fully built. In this tutorial we used the *inline* approach, which is more straightforward for small examples.

---

## Full Working Example (Copy‑Paste Ready)

```csharp
// ---------------------------------------------------------------
// Full example: Create PDF Document with a custom Table of Contents
// ---------------------------------------------------------------
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Step 1: Create a new PDF document
        using (var pdfDocument = new Document())
        {
            // Step 2: Add TOC page and set title
            var tocPage = pdfDocument.Pages.Add();
            var tocInfo = new TocInfo();

            var titleFragment = new TextFragment("Table Of Contents");
            titleFragment.TextState.FontSize = 20;
            titleFragment.TextState.FontStyle = FontStyles.Bold;
            tocInfo.Title = titleFragment;
            tocPage.TocInfo = tocInfo;

            // Step 3: Configure TOC formatting (4 levels)
            tocInfo.IsShowPageNumbers = false;
            tocInfo.FormatArrayLength = 4;

            // Level 1
            tocInfo.FormatArray[0].Margin.Right = 0;
            tocInfo.FormatArray[0].TextState.FontStyle = FontStyles.Bold | FontStyles.Italic;

            // Level 2
            tocInfo.FormatArray[1].Margin.Left = 30;
            tocInfo.FormatArray[1].TextState.Underline = true;
            tocInfo.FormatArray[1].TextState.FontSize = 10;

            // Level 3
            tocInfo.FormatArray[2].TextState.FontStyle = FontStyles.Bold;

            // Level 4
            tocInfo.FormatArray[3].TextState.FontStyle = FontStyles.Bold;

            // Step 4: Add a regular content page
            var contentPage = pdfDocument.Pages.Add();

            // Step 5: Insert headings (levels 1‑4) linked to TOC
            for (int level = 1; level <= 4; level++)
            {
                var heading = new Heading(level);
                var textSegment = new TextSegment();

                heading.TocPage = tocPage;      // associate with TOC
                heading.Segments.Add(textSegment);
                heading.IsAutoSequence = true;  // automatic numbering
                textSegment.Text = $"this is heading of level {level}";
                heading.IsInList = true;        // include in TOC

                contentPage.Paragraphs.Add(heading);
            }

            // Step 6: Save the PDF
            pdfDocument.Save("TOC_out.pdf");
        }

        Console.WriteLine("PDF generated successfully – see TOC_out.pdf");
    }
}
```

Run the program (`dotnet run`) and open `TOC_out.pdf`. You should see the fully styled table of contents followed by the four headings.

---

## Next Steps & Related Topics

- **How to add images to a PDF** – embed charts or logos alongside your text.  
- **How to create bookmarks** – complement the TOC with PDF bookmarks for better navigation.  
- **How to set PDF metadata** – title, author, and keywords for searchable archives.  

Experiment with those features to turn a simple report into a polished, publishing‑ready document.

---

## Wrap‑Up

We’ve just shown how to **create PDF document** using Aspose.PDF, then walked through **how to add toc**, **how to format toc**, and **how to set toc** for multi‑level headings. The complete, copy‑paste example should work out‑

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}