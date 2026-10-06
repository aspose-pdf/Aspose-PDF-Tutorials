---
category: general
date: 2026-03-24
description: Create PDF document and learn how to set absolute position for tagged
  text. This tutorial shows how to add span element, how to add tagged content and
  position text on page.
draft: false
keywords:
- create pdf document
- set absolute position
- add span element
- how to add tagged
- position text on page
language: en
og_description: Create PDF document and instantly see how to set absolute position,
  add span element, and position text on page with tagged PDF content.
og_title: Create PDF Document – Absolute Positioning of Tagged Text
tags:
- Aspose.Pdf
- C#
- PDF Tagging
title: Create PDF Document – Set Absolute Position for Tagged Text
url: /net/programming-with-tagged-pdf/create-pdf-document-set-absolute-position-for-tagged-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create PDF Document – Set Absolute Position for Tagged Text

Ever needed to **create pdf document** that contains accessible, tagged text positioned exactly where you want it? Maybe you’re building a form‑like PDF where the label must sit at a precise coordinate, or you’re generating a certificate and the name has to align perfectly with a background image.  

In this guide we’ll walk through a complete, runnable example that shows **how to add tagged** content, **set absolute position**, and **add span element** so you can **position text on page** without guessing. No external references—just the code you can copy‑paste, plus explanations of the “why” behind each line.

## Prerequisites

- .NET 6+ (or .NET Framework 4.6+) with a C# compiler  
- Aspose.Pdf for .NET (latest version at the time of writing, 23.12) installed via NuGet  
- Basic familiarity with C# syntax  

If you’ve got those, let’s get started.

---

## Create PDF Document – Setting the Absolute Position

The first thing we do is instantiate an empty `Document`. This object represents the whole PDF file and gives us access to the tagged‑content tree.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();
```

**Why this matters:**  
`Document` is the root of the PDF structure. By creating it first we ensure there’s a canvas for both visual elements (pages, graphics) and logical structure (tags). The `using` statement guarantees the file is properly disposed, which prevents file‑handle leaks on Windows.

---

## Enable Tagged Content (How to Add Tagged)

Before we can insert any tagged elements, the document must be marked as *tagged*. Aspose.Pdf automatically creates a `TaggedContent` object, but you still need to turn the flag on.

```csharp
// Step 2: Mark the document as tagged (required for accessibility)
pdfDocument.TaggedContent = true;
```

**What happens under the hood?**  
Setting `TaggedContent` to `true` tells PDF readers that the file contains a logical structure tree. This is crucial for screen readers and for the `SetPosition` method to work correctly on a span element.

---

## Get the Root Element of the Tagged‑Content Tree

The root element is the entry point for all structural tags (like `<Document>`, `<Section>`, `<Span>`). Think of it as the invisible “body” of the PDF.

```csharp
// Step 3: Retrieve the root element of the tag tree
var rootElement = pdfDocument.TaggedContent.RootElement;
```

**Why we need the root:**  
All subsequent tags must be attached somewhere in the tree; otherwise they won’t appear in the accessibility hierarchy.

---

## Add a Span Element – The Building Block for Inline Text

A *span* is the PDF equivalent of an HTML `<span>`—perfect for short pieces of text that you want to position precisely.

```csharp
// Step 4: Create a span element that will hold the text
var spanElement = rootElement.CreateSpanElement();
```

**Design note:**  
If you need richer formatting (bold, italic, hyperlinks), you can wrap the span in a `<Paragraph>` or use `TextFragment` objects later. For absolute positioning, a plain span is the lightest weight.

---

## Set Absolute Position – X=100, Y=200

Now comes the fun part: placing the span at an exact location on the page. The coordinate system starts at the bottom‑left corner (0,0) and uses points (1 pt ≈ 1/72 in).

```csharp
// Step 5: Position the span at an absolute location (X=100, Y=200)
spanElement.SetPosition(100, 200);
```

**Why absolute positioning?**  
When you need pixel‑perfect layout—think certificates, invoices, or forms—relative flow (like left‑to‑right text) isn’t enough. `SetPosition` bypasses the normal text flow and pins the element where you specify.

---

## Add Text to the Span

With the span positioned, we now inject the actual string.

```csharp
// Step 6: Add the desired text to the span
spanElement.AddText("Positioned tagged text");
```

**Tip:**  
If you need Unicode characters or right‑to‑left scripts, just pass the string; Aspose.Pdf handles the encoding automatically.

---

## Append the Span to the Root Element

Finally, we attach the span to the document’s logical tree so that it becomes part of the final PDF.

```csharp
// Step 7: Append the span to the root so it becomes part of the PDF structure
rootElement.AppendChild(spanElement);
```

**What if you forget this step?**  
The span would exist in memory but never be serialized into the file, so you’d see no text and the accessibility tree would be incomplete.

---

## Complete, Runnable Example

Below is the full program you can drop into a console app. It creates a one‑page PDF, adds a tagged span at (100, 200), and saves the file as `TaggedPositioned.pdf`.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Enable tagging for accessibility
        pdfDocument.TaggedContent = true;

        // 3️⃣ Add a blank page (required for visual placement)
        var page = pdfDocument.Pages.Add();

        // 4️⃣ Get the root element of the tagged‑content tree
        var rootElement = pdfDocument.TaggedContent.RootElement;

        // 5️⃣ Create a span element that will hold the text
        var spanElement = rootElement.CreateSpanElement();

        // 6️⃣ Position the span at an absolute location on the page (X=100, Y=200)
        spanElement.SetPosition(100, 200);

        // 7️⃣ Add the desired text to the span
        spanElement.AddText("Positioned tagged text");

        // 8️⃣ Append the span to the root so it becomes part of the PDF structure
        rootElement.AppendChild(spanElement);

        // 9️⃣ Save the document
        pdfDocument.Save("TaggedPositioned.pdf");

        Console.WriteLine("PDF created successfully – check TaggedPositioned.pdf");
    }
}
```

**Expected output:**  
Open `TaggedPositioned.pdf` in any viewer (Adobe Acrobat, Foxit, etc.). You’ll see the phrase **“Positioned tagged text”** exactly 100 pt from the left edge and 200 pt from the bottom edge of the page. If you inspect the *Tags* panel, a `<Span>` element will be listed under the document’s root, confirming that the content is properly tagged.

---

## Common Questions & Edge Cases

### What if I need to position text on a specific page other than the first?

Add the page you want (`var page = pdfDocument.Pages[3];`) before calling `SetPosition`. The span will automatically attach to the active page context.

### Can I set the position in inches or centimeters?

`SetPosition` accepts points. Convert using the formulas:  
- **Inches → points:** `points = inches * 72`  
- **Centimeters → points:** `points = cm * 28.3465`

### How do I change the font or color of the span?

After creating the span, you can retrieve its `TextState` and modify it:

```csharp
var textState = spanElement.TextState;
textState.Font = FontRepository.FindFont("Arial");
textState.FontSize = 12;
textState.ForegroundColor = Color.GetBlack();
```

### What if the document already has existing tags?

You can still create a new span and append it to any existing element (`rootElement`, a specific `<Section>`, etc.). Just make sure you maintain a logical hierarchy—screen readers expect a well‑structured tree.

### Does this work with PDF/A or PDF/UA compliance?

Yes. Tagged PDFs are a core requirement for PDF/UA. If you need PDF/A, set `pdfDocument.Convert(new PdfAConversionOptions(PdfAStandard.PdfA_1b));` after building the content.

---

## Pro Tips & Pitfalls

- **Pro tip:** Always add a page before positioning content. Without a page, `SetPosition` silently fails because there’s nowhere to render.
- **Watch out for units:** Mixing pixels from a UI design with PDF points will misplace your text. Double‑check your conversion.
- **Performance hint:** If you’re generating thousands of PDFs, reuse a single `Document` instance and call `pdfDocument.Pages.Clear()` between runs to avoid excessive memory allocation.
- **Accessibility reminder:** Tagging isn’t just a nice‑to‑have; many regulations (Section 508, EN 301 549) require it. Using `CreateSpanElement` ensures the text is discoverable by assistive technologies.

---

## Conclusion

We’ve just **created pdf document** from scratch, **set absolute position**, **added span element**, and demonstrated **how to add tagged** content so you can **position text on page** with pixel‑perfect accuracy. The complete example is ready to run, and the explanation covered both the *how* and the *why*—exactly what developers (and AI assistants) look for when they need a reliable solution.

Next, you might explore:

- Adding images behind the positioned text for watermarked certificates.  
- Using `CreateParagraphElement` for multi‑line blocks that still need absolute placement.  
- Exporting to PDF/UA to satisfy strict accessibility audits.  

Feel free to tweak the coordinates, fonts, or colors—experimentation is the fastest way to master tagged PDF generation. If you hit a snag, drop a comment below; happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}