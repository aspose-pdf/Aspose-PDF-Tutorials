---
category: general
date: 2026-07-20
description: 'Create PDF document C# with Aspose.Pdf: position text in PDF and add
  structural tree for accessibility. Follow this step‑by‑step guide.'
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document c#
- position text in pdf
- add structural tree
- Aspose.Pdf tagging
- PDF/A‑2b generation
language: en
lastmod: 2026-07-20
og_description: Create PDF document C# instantly. Learn how to position text in PDF
  and add structural tree using Aspose.Pdf for PDF/A‑2b compliance.
og_image_alt: Screenshot showing positioned text inside a PDF generated with Aspose.Pdf
  in C#
og_title: Create PDF Document C# – Full Guide to Position Text & Tag Structure
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: 'Create PDF document C# with Aspose.Pdf: position text in PDF and add
    structural tree for accessibility. Follow this step‑by‑step guide.'
  headline: Create PDF Document C# – Position Text and Add Structural Tree
  type: TechArticle
- description: 'Create PDF document C# with Aspose.Pdf: position text in PDF and add
    structural tree for accessibility. Follow this step‑by‑step guide.'
  name: Create PDF Document C# – Position Text and Add Structural Tree
  steps:
  - name: Can I use other units (mm, cm) for positioning?
    text: Aspose.Pdf works natively with points. If you prefer millimeters, convert
      using `1 mm ≈ 2.83465 pt`. For example, `Position(25.4, 254)` places the paragraph
      1 cm from the left and 9 cm from the bottom.
  - name: What if I need to add multiple tags (headings, tables)?
    text: Simply create additional `StructureElement` objects with tags like `"H1"`
      for headings or `"Table"` for tables, and add the corresponding content as kids.
      Nesting works the same way—children inherit the parent’s logical order.
  - name: Does this approach work for PDF/A‑1b or PDF/A‑3b?
    text: Yes. Replace `SaveFormat.PdfA2b` with `SaveFormat.PdfA1b` or `SaveFormat.PdfA3b`.
      Keep in mind that each PDF/A version has its own set of required metadata; Aspose.Pdf
      will prompt you if something is missing.
  type: HowTo
tags:
- C#
- PDF
- Aspose.Pdf
title: Create PDF Document C# – Position Text and Add Structural Tree
url: /net/programming-with-tagged-pdf/create-pdf-document-c-position-text-and-add-structural-tree/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create PDF Document C# – Position Text and Add Structural Tree

Ever needed to **create PDF document C#** that not only places text exactly where you want it, but also embeds a proper structural tree for accessibility? You're not the only one—developers building invoices, reports, or e‑books hit this need all the time. In this tutorial we’ll walk through a complete, ready‑to‑run example that does exactly that, using the powerful Aspose.Pdf library.

We'll cover how to **position text in PDF**, attach a semantic tag via the **add structural tree** step, and finally save the file as a PDF/A‑2b compliant document. By the end you’ll have a reusable snippet you can drop into any .NET project.

---

## What You’ll Need

- **.NET 6.0** or later (the code works with .NET Framework 4.6+ as well)  
- **Aspose.Pdf for .NET** NuGet package (`Install-Package Aspose.Pdf`)  
- A basic C# development environment (Visual Studio, Rider, or VS Code)  

No additional third‑party tools are required; the library handles everything from page layout to PDF/A compliance.

---

## Step 1: Initialize the PDF Document (Create PDF Document C#)

The first thing we do is spin up a fresh `Document` object. Think of it as a clean canvas—nothing on it yet, but ready to receive pages, text, and structural metadata.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Struct;

// Create a new PDF document – this is the core of our create pdf document c# workflow
Document pdfDoc = new Document();

// Add a blank page to the document; the page will host our positioned text
Page pdfPage = pdfDoc.Pages.Add();
```

> **Why this matters:** The `Document` class is the entry point for all Aspose.Pdf operations. Adding a page early gives us a surface to attach both visual content and the structural tree later on.

---

## Step 2: Define a Paragraph and Position It (Position Text in PDF)

Now we create a `Paragraph` object and tell Aspose exactly where on the page it should appear. PDF coordinates are measured in points (1 inch = 72 pt), so we use `Position(72, 720)` to place the paragraph 1 inch from the left edge and 10 inches up from the bottom.

```csharp
// Define a paragraph positioned 1 inch from the left and 10 inches from the bottom
Paragraph positionedParagraph = new Paragraph
{
    // Position(x, y) – X is horizontal, Y is vertical from the bottom-left corner
    Position = new Position(72, 720) // 72 pt = 1 inch, 720 pt = 10 inch
};

// Add the actual text we want to display
positionedParagraph.Segments.Add(
    new TextFragment("Tagged paragraph at a specific location.")
);
```

> **Pro tip:** If you need to position multiple lines, adjust the `Y` coordinate for each subsequent paragraph, or use a `TextBuilder` for finer control.

---

## Step 3: Create a Structural Element (Add Structural Tree)

Accessibility‑aware PDFs rely on a *structure tree* that describes the logical order of content. Here we create a `StructureElement` with the tag `"P"` (paragraph) and attach our positioned paragraph as its child.

```csharp
// Create a structural element (tag) for the paragraph – this is the add structural tree step
StructureElement structElement = new StructureElement("P");

// Attach the paragraph as a child of the structural element
structElement.AddKid(positionedParagraph);
```

> **Why we add a structural tree:** Screen readers and other assistive technologies use these tags to navigate the document. Without them, your PDF might be visually perfect but inaccessible.

---

## Step 4: Hook the Structural Element to the Page

Each page maintains its own collection of structural elements. By adding our `structElement` to `pdfPage.StructElements`, we integrate the logical hierarchy with the visual layout.

```csharp
// Attach the structural element to the page's structure tree
pdfPage.StructElements.Add(structElement);
```

> **Common pitfall:** Forgetting this step means the tag exists in memory but isn’t linked to any page, rendering the accessibility information invisible to readers.

---

## Step 5: Save as PDF/A‑2b (Ensuring Long‑Term Preservation)

PDF/A‑2b is a subset of PDF designed for archiving. Aspose.Pdf can produce this format with a single call. Replace `"YOUR_DIRECTORY"` with an actual path on your machine.

```csharp
// Save the document as a PDF/A‑2b file – ideal for long‑term storage and compliance
pdfDoc.Save("YOUR_DIRECTORY/TaggedWithPosition.pdf", SaveFormat.PdfA2b);
```

> **Result:** You now have a PDF where the text sits exactly where you placed it, and the document includes a proper structural tree for accessibility tools.

---

## Full Working Example

Below is the complete program you can copy‑paste into a console app. It compiles and runs as‑is (once you add the Aspose.Pdf NuGet reference).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Struct;

namespace PdfPositioningDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Initialize the document
            Document pdfDoc = new Document();
            Page pdfPage = pdfDoc.Pages.Add();

            // Step 2: Define and position the paragraph
            Paragraph positionedParagraph = new Paragraph
            {
                Position = new Position(72, 720) // 1 inch left, 10 inches up
            };
            positionedParagraph.Segments.Add(
                new TextFragment("Tagged paragraph at a specific location.")
            );

            // Step 3: Create the structural element (tag)
            StructureElement structElement = new StructureElement("P");
            structElement.AddKid(positionedParagraph);

            // Step 4: Attach the structural element to the page
            pdfPage.StructElements.Add(structElement);

            // Step 5: Save as PDF/A‑2b
            string outputPath = @"C:\Temp\TaggedWithPosition.pdf";
            pdfDoc.Save(outputPath, SaveFormat.PdfA2b);

            Console.WriteLine($"PDF created successfully at: {outputPath}");
        }
    }
}
```

**Expected output:** After running, open `TaggedWithPosition.pdf`. You’ll see the sentence “Tagged paragraph at a specific location.” sitting near the bottom‑right corner of the first page. If you inspect the PDF’s tags (e.g., with Adobe Acrobat’s “Tags” pane), you’ll find a `<P>` element linked to that paragraph.

---

![Screenshot of positioned text in a PDF generated with Aspose.Pdf](/images/pdf-positioned.png){: .align-center }

*Image alt text:* **create pdf document c#** – screenshot showing positioned text inside a PDF generated with Aspose.Pdf.

---

## Common Questions & Edge Cases

### Can I use other units (mm, cm) for positioning?

Aspose.Pdf works natively with points. If you prefer millimeters, convert using `1 mm ≈ 2.83465 pt`. For example, `Position(25.4, 254)` places the paragraph 1 cm from the left and 9 cm from the bottom.

### What if I need to add multiple tags (headings, tables)?

Simply create additional `StructureElement` objects with tags like `"H1"` for headings or `"Table"` for tables, and add the corresponding content as kids. Nesting works the same way—children inherit the parent’s logical order.

### Does this approach work for PDF/A‑1b or PDF/A‑3b?

Yes. Replace `SaveFormat.PdfA2b` with `SaveFormat.PdfA1b` or `SaveFormat.PdfA3b`. Keep in mind that each PDF/A version has its own set of required metadata; Aspose.Pdf will prompt you if something is missing.

---

## Recap

We’ve walked through a **create pdf document c#** scenario that:

1. Instantiates a new PDF using Aspose.Pdf.  
2. **Position text in PDF** by setting exact coordinates.  
3. **Add structural tree** elements for accessibility.  
4. Saves the result as a standards‑compliant PDF/A‑2b file.

All steps are fully self‑contained, and you can adapt the snippet for more complex layouts, multiple pages, or different tag types.

---

## What’s Next?

- **Styling text** – explore `TextState` to change fonts, colors, and sizes.  
- **Embedding images** – use `ImageFragment` and position it alongside the paragraph.  
- **Generating tables** – create `Table` objects and tag them with `"Table"` for richer semantics.  
- **Automation pipelines** – integrate this code into a background service that generates invoices nightly.

Feel free to experiment, and let us know which variations you find most useful. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Tagged PDFs with Aspose.PDF for .NET&#58; A Complete Guide to Enhancing Accessibility and Document Structure](/pdf/english/net/advanced-features/create-tagged-pdfs-aspose-pdf-net/)
- [Create PDF Document with Aspose.PDF – Step‑by‑Step Guide](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Create & Rotate Text in PDFs Using Aspose.PDF .NET&#58; A Comprehensive Guide for Developers](/pdf/english/net/text-operations/create-rotate-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}