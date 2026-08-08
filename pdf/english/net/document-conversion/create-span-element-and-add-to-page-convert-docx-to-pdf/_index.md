---
category: general
date: 2026-03-27
description: Create span element in C# and learn how to add span to a page while converting
  DOCX to PDF and saving as PDF. Step‑by‑step guide for developers.
draft: false
keywords:
- create span element
- how to add span
- convert docx to pdf
- add element to page
- save as pdf
language: en
og_description: Create span element in C# and learn how to add span to a page while
  converting DOCX to PDF, then save as PDF. Complete code example included.
og_title: Create span element and add to page – Convert DOCX to PDF
tags:
- C#
- DocumentProcessing
- PDFConversion
title: Create span element and add to page – Convert DOCX to PDF
url: /net/document-conversion/create-span-element-and-add-to-page-convert-docx-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create span element and add to page – Convert DOCX to PDF

Create **span element** in a DOCX file is a common task when you need precise layout control. In this tutorial we’ll show you **how to add span** to a page, **convert DOCX to PDF**, and **save as PDF**—all in a few tidy steps.  

If you’ve ever stared at a Word document and thought, “I wish I could drop a tiny text box at an exact coordinate,” you’re in the right place. We’ll walk through the entire workflow, from loading the source file to getting a polished PDF output.

## What you’ll accomplish

By the end of this guide you’ll be able to:

* Load a `.docx` file using the document library’s `Document` class.  
* **Create span element** with the `TaggedContent` API.  
* Position that span at exact X/Y coordinates on a chosen page.  
* **Add element to page** reliably, even when the page isn’t the first one.  
* **Convert DOCX to PDF** and **save as PDF** with a single `Save` call.

No external tools, no mysterious settings—just plain C# code you can copy‑paste into your project.

## Prerequisites

* .NET 6+ (or any recent .NET runtime that your library supports).  
* The document processing SDK that provides `Document`, `TaggedContent`, `Position`, etc.  
* A basic understanding of C# syntax—if you can write a `Console.WriteLine`, you’re good.

> **Pro tip:** Keep your SDK version up‑to‑date; the latest release (v3.2 as of March 2026) includes performance tweaks for page‑level operations.

---

![Diagram illustrating how to create span element and place it on a PDF page](https://example.com/images/create-span-element.png "Create span element placement diagram")

## Create span element – Position and Add to Page

Below is the full, runnable code that does everything from loading the source DOCX to writing the final PDF. Feel free to drop it into a console app, adjust the paths, and run it.

```csharp
using DocumentProcessing;   // Replace with the actual namespace of your SDK
using DocumentProcessing.Models;

class Program
{
    static void Main()
    {
        // Step 1: Load the DOCX you want to modify
        // -------------------------------------------------
        // The constructor takes a file path; make sure the file exists.
        Document doc = new Document(@"C:\Docs\input.docx");

        // Step 2: Create a new span element using the TaggedContent API
        // -------------------------------------------------
        // A span is a lightweight container for inline content.
        var span = doc.TaggedContent.CreateSpanElement();
        // Optional: add some text inside the span
        span.Text = "Hello, world!";

        // Step 3: Position the span at the desired coordinates (X = 50, Y = 750)
        // -------------------------------------------------
        // Position uses points (1/72 inch). Adjust as needed.
        span.Position = new Position(50, 750);

        // Step 4: Add the span to the target page (page index 1 = second page)
        // -------------------------------------------------
        // Pages are zero‑based; index 1 means the second page in the document.
        doc.Pages[1].Add(span);

        // Step 5: Convert the modified DOCX to PDF and save the result
        // -------------------------------------------------
        // The Save method automatically detects the output format from the extension.
        doc.Save(@"C:\Docs\output.pdf");

        // Confirmation output
        Console.WriteLine("Span added, document converted, and PDF saved successfully.");
    }
}
```

### Step‑by‑step explanation

#### Step 1 – Load the DOCX document  
We instantiate a `Document` object pointing at `input.docx`. This object represents the whole Word file in memory, giving us access to pages, content, and metadata.  

#### Step 2 – Create a span element  
The `TaggedContent.CreateSpanElement()` call returns a lightweight inline container. Think of it as a tiny, invisible box that can hold text, images, or other inline elements. Adding text (`span.Text`) is optional but useful for debugging.

#### Step 3 – Position the span  
`new Position(50, 750)` sets the top‑left corner of the span 50 pts from the left margin and 750 pts from the top of the page. These values are absolute, so you can place the span anywhere—perfect for precise layouts.

#### Step 4 – Add span to the target page  
`doc.Pages[1].Add(span)` injects the span into the second page. The API uses zero‑based indexing, so page 0 is the first page. If you need to add it to the first page, simply use `doc.Pages[0]`.

#### Step 5 – Convert DOCX to PDF and save as PDF  
Calling `doc.Save("output.pdf")` does two things: it writes the modified document to disk **and** converts the content to PDF because of the `.pdf` extension. No extra conversion step is required—this is the easiest way to **save as PDF**.

---

## How to add span on a different page (advanced)

Sometimes you don’t know the page index ahead of time. You can locate a page by its number (human‑friendly) or by searching for a specific keyword.

```csharp
// Find the page that contains the word "Summary"
int targetIndex = doc.Pages
    .Select((p, i) => new { Page = p, Index = i })
    .FirstOrDefault(x => x.Page.Text.Contains("Summary"))?.Index ?? 0;

// Fallback to first page if not found
targetIndex = Math.Max(targetIndex, 0);

// Add the span to the discovered page
doc.Pages[targetIndex].Add(span);
```

**Why this matters:** In reports where the number of pages varies, hard‑coding `Pages[1]` can break the layout. This snippet shows a robust pattern for **how to add span** dynamically.

---

## Common pitfalls and how to avoid them

| Issue | What happens | Fix |
|-------|--------------|-----|
| **Span not visible** | Coordinates are off‑page or the span has zero width/height. | Double‑check `Position` values; use a ruler in your PDF viewer. |
| **Wrong page index** | You add to page 0 but expect it on page 2. | Remember the API is zero‑based; add 1 to the human page number. |
| **Saving overwrites source** | `doc.Save("input.docx")` replaces the original file. | Always save to a new path (`output.pdf`) when converting. |
| **Missing SDK reference** | Compilation error on `Document` class. | Install the NuGet package: `dotnet add package DocumentProcessing.SDK`. |

---

## Verifying the result

After running the program, open `output.pdf` in any PDF viewer. You should see the text “Hello, world!” positioned exactly at (50, 750) on the second page. If the text appears elsewhere, adjust the `Position` values and re‑run.  

For automated testing, you can use a PDF parser (e.g., iTextSharp) to assert the text’s coordinates programmatically.

```csharp
// Example using iTextSharp to verify position (pseudo‑code)
var pdfReader = new PdfReader(@"C:\Docs\output.pdf");
var page = pdfReader.GetPageContent(2);
Debug.Assert(page.Contains("Hello, world!"));
```

---

## Next steps

* **Style the span** – explore `span.Font`, `span.Color`, and other styling properties.  
* **Add images** – use `CreateImageElement()` instead of a span for graphics.  
* **Batch processing** – loop over a folder of DOCX files

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}