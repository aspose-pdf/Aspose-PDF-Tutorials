---
category: general
date: 2025-12-22
description: Create PDF document C# with a full example that shows how to add table
  of contents to PDF, how to insert PDF page, and customize PDF page numbers—all in
  one guide.
draft: false
keywords:
- create pdf document c#
- add table of contents to pdf
- how to insert pdf page
- customize pdf page numbers
- how to add toc pdf
language: en
og_description: Create PDF document C# and learn how to add a table of contents, insert
  PDF pages, and customize page numbers in a clear step‑by‑step tutorial.
og_title: Create PDF Document C# – Table of Contents & Page Numbers
tags:
- Aspose.Pdf
- C#
- PDF generation
title: Create PDF Document C# – Add a Table of Contents, Insert Pages & Customize
  Page Numbers
url: /net/programming-with-pdf-pages/create-pdf-document-c-add-a-table-of-contents-insert-pages-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create PDF Document C# – Full Guide to TOC, Page Insertion & Number Customization

Ever wondered how to **create PDF document C#** that already contains a polished Table of Contents? Maybe you’ve tried inserting a page only to end up with mis‑aligned numbers, or you’re scratching your head over how to customize PDF page numbers for a professional look. You’re not alone—many developers hit these roadblocks when automating reports, contracts, or e‑books.

In this tutorial we’ll solve all of that in one go. You’ll see a complete, runnable example that **adds a table of contents to a PDF**, shows **how to insert PDF page** at the beginning, and demonstrates **customize PDF page numbers** with a prefix. By the end you’ll have a single method that produces a clean, navigable PDF, ready for distribution.

> **What you’ll need**  
> • .NET 6+ (or .NET Framework 4.6+).  
> • Aspose.Pdf for .NET (free trial or licensed version).  
> • A basic C# project (Console App works perfectly).  

Let’s dive in and build the solution step by step.

---

## Step 1: Set Up the Project & Load the Source PDF

Before we can modify anything we must reference Aspose.Pdf and load the original file. This is the foundation for **how to insert PDF page** later on.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Path to the source PDF you want to enhance
        string sourcePath = @"YOUR_DIRECTORY\CustomizePageNumbersAddingToC.pdf";

        // Load the document – this is where we start to create PDF document C#
        using (var pdfDocument = new Document(sourcePath))
        {
            // The rest of the logic lives inside this using block
            AddTableOfContents(pdfDocument);
            pdfDocument.Save(@"YOUR_DIRECTORY\CustomizePageNumbersAddingToC_out.pdf");
        }
    }
}
```

*Why this matters*: Loading the file gives us a `Document` object that represents the entire PDF in memory. All subsequent operations—page insertion, TOC creation, and number customization—are performed on this object.

---

## Step 2: Insert a Blank Page for the Table of Contents

A Table of Contents needs its own page, typically at the very front. Here’s **how to insert PDF page** at index 1 (the first position).

```csharp
static void AddTableOfContents(Document pdfDocument)
{
    // Insert a new blank page as the first page – this will hold the TOC
    Page tocPage = pdfDocument.Pages.Insert(1);

    // Prepare TOC metadata (title, page‑number prefix, etc.)
    var tocInfo = new TocInfo
    {
        Title = new TextFragment("Table Of Contents")
        {
            TextState = { FontSize = 20, FontStyle = FontStyles.Bold }
        },
        PageNumbersPrefix = "P"   // Prefix for page numbers in the TOC
    };

    tocPage.TocInfo = tocInfo;
```

*Explanation*: `Pages.Insert(1)` pushes all existing pages one slot forward, making room for the new TOC page. Setting `TocInfo` tells Aspose how to render the heading and which prefix to apply—this is the core of **customize PDF page numbers**.

---

## Step 3: Populate the TOC with Entries for Each Real Page

Now we need to create a heading for every page *except* the TOC itself. Each heading becomes a clickable entry that points to its destination page.

```csharp
    // Loop through the original pages (skip the TOC page we just added)
    for (int i = 1; i < pdfDocument.Pages.Count; i++)
    {
        // Create a heading level – 1 works fine for a simple flat TOC
        var tocEntry = new Heading(1);
        var textSegment = new TextSegment
        {
            Text = $"Page {i}"
        };

        // Link the heading to the correct destination page
        tocEntry.DestinationPage = pdfDocument.Pages[i + 1]; // +1 because of the inserted TOC page
        tocEntry.Top = pdfDocument.Pages[i + 1].Rect.Height; // Position at the top of the page
        tocEntry.Segments.Add(textSegment);
        tocEntry.TocPage = tocPage; // Associate entry with the TOC page

        // Add the heading to the TOC page's paragraph collection
        tocPage.Paragraphs.Add(tocEntry);
    }
}
```

*Why this works*: `Heading` objects are special Aspose elements that automatically generate TOC entries when the document is saved. By setting `DestinationPage` we tell the PDF where to jump when the user clicks the entry. The loop runs `pdfDocument.Pages.Count - 1` times, ensuring we never reference the TOC itself.

---

## Step 4: Save the Updated PDF

The final step is straightforward—just persist the changes to disk.

```csharp
// Inside Main(), after AddTableOfContents(pdfDocument);
pdfDocument.Save(@"YOUR_DIRECTORY\CustomizePageNumbersAddingToC_out.pdf");
```

When you open the resulting file, you’ll see a nicely formatted “Table Of Contents” page at the front, each entry prefixed with **“P”** (our custom page‑number prefix), and clicking any entry jumps to the corresponding page.

---

## Full Working Example (All Pieces Together)

Below is the complete program you can copy‑paste into a console app. No piece is missing, so you can run it immediately after installing Aspose.Pdf via NuGet.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        string sourcePath = @"YOUR_DIRECTORY\CustomizePageNumbersAddingToC.pdf";
        string outputPath = @"YOUR_DIRECTORY\CustomizePageNumbersAddingToC_out.pdf";

        using (var pdfDocument = new Document(sourcePath))
        {
            AddTableOfContents(pdfDocument);
            pdfDocument.Save(outputPath);
        }

        Console.WriteLine("PDF with TOC created successfully!");
    }

    static void AddTableOfContents(Document pdfDocument)
    {
        // Insert TOC page at the beginning
        Page tocPage = pdfDocument.Pages.Insert(1);

        // Configure TOC appearance and page number prefix
        var tocInfo = new TocInfo
        {
            Title = new TextFragment("Table Of Contents")
            {
                TextState = { FontSize = 20, FontStyle = FontStyles.Bold }
            },
            PageNumbersPrefix = "P"
        };
        tocPage.TocInfo = tocInfo;

        // Add an entry for each original page (skip the TOC itself)
        for (int i = 1; i < pdfDocument.Pages.Count; i++)
        {
            var tocEntry = new Heading(1);
            var textSegment = new TextSegment { Text = $"Page {i}" };

            tocEntry.DestinationPage = pdfDocument.Pages[i + 1];
            tocEntry.Top = pdfDocument.Pages[i + 1].Rect.Height;
            tocEntry.Segments.Add(textSegment);
            tocEntry.TocPage = tocPage;

            tocPage.Paragraphs.Add(tocEntry);
        }
    }
}
```

**Expected outcome**:  

- First page: “Table Of Contents” title, entries like “Page 1 … P1”, “Page 2 … P2”, etc.  
- Remaining pages: unchanged content, but now reachable via the TOC links.  

If you open the PDF in Adobe Reader, the bookmarks pane will also list the same entries, giving you two navigation methods.

---

## Common Questions & Edge Cases

### 1. What if my source PDF already has a TOC?
You can still insert a new one, but you might want to remove the old bookmarks first. Use `pdfDocument.Outlines.Delete()` before adding the new headings.

### 2. How do I change the prefix from “P” to something else?
Just modify `tocInfo.PageNumbersPrefix = "YourPrefix"` in Step 2. The same property works for any string, even an empty one if you don’t want a prefix.

### 3. Can I add sub‑levels (e.g., chapters and sections)?
Absolutely. Use `new Heading(2)` for a second‑level entry, and adjust `textSegment.Text` accordingly. Aspose will automatically indent and number them.

### 4. What about PDFs that are password‑protected?
Load the document with `new Document(sourcePath, new LoadOptions { Password = "secret" })`. After manipulation, you can re‑apply the password via `pdfDocument.Encrypt`.

### 5. Is the approach compatible with .NET Core?
Yes. Aspose.Pdf for .NET supports .NET Standard 2.0+, so you can run this code in .NET 5/6/7 console apps, ASP.NET Core services, or even Azure Functions.

---

## Pro Tips & Pitfalls

- **Pro tip**: If you need a fancy TOC layout (dots, right‑aligned page numbers), customize the `TextFragment` style or build a table manually—Aspose lets you draw lines and set tab stops.
- **Watch out for**: Off‑by‑one errors when inserting pages. Remember that after you insert the TOC, every original page’s index shifts by +1.
- **Performance note**: For PDFs with hundreds of pages, consider disabling `pdfDocument.Compress` temporarily to speed up the insertion loop, then re‑enable it before saving.
- **Testing**: Always open the generated PDF in more than one viewer (Adobe Reader, Foxit, Chrome) to verify that the links work across platforms.

---

## Conclusion

We’ve just walked through a complete, end‑to‑end solution that shows **how to create PDF document C#**, **add table of contents to PDF**, **how to insert PDF page**, and **customize PDF page numbers**—all in a single, easy‑to‑read tutorial. By loading the source file, inserting a dedicated TOC page, populating it with heading entries, and finally saving the document, you end up with a professional‑looking PDF ready for distribution.

From here you can experiment with multi‑level headings, different page‑number prefixes, or even generate the source PDF on the fly instead of loading an existing one. The same pattern works for invoices, manuals, e‑books, and any scenario where navigation matters.

Feel free to drop a comment if you hit a snag, or share how you extended the example in your own projects. Happy coding, and enjoy the smoother PDF workflow!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}