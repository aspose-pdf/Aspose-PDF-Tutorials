---
category: general
date: 2026-08-20
description: Create custom graphics state in PDF with Aspose.Pdf. Learn how to edit
  PDF resources and add transparency PDF in just a few steps.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom graphics state
- edit pdf resources
- add transparency pdf
- Aspose.Pdf graphics state
- PDF resource dictionary
language: en
lastmod: 2026-08-20
og_description: Create custom graphics state in PDF with Aspose.Pdf. This tutorial
  shows how to edit PDF resources and add transparency PDF quickly.
og_image_alt: Screenshot of C# code that creates a custom graphics state in a PDF
og_title: Create custom graphics state in PDF – Aspose.Pdf guide
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create custom graphics state in PDF with Aspose.Pdf. Learn how to edit
    PDF resources and add transparency PDF in just a few steps.
  headline: Create custom graphics state in PDF using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- Aspose.Pdf
- C#
- Graphics state
title: Create custom graphics state in PDF using Aspose.Pdf
url: /net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create custom graphics state in PDF using Aspose.Pdf

If you need to **create custom graphics state** in a PDF, this guide shows you exactly how to do it with Aspose.Pdf for .NET. By the end of the tutorial you will be able to **edit PDF resources**, inject a new graphics‑state dictionary, and **add transparency PDF** content without leaving your C# project.

You’ll see a complete, runnable example, an explanation of why each line matters, and tips for handling multi‑page documents or different blend modes. No external tools are required—just the Aspose.Pdf library and a basic .NET development environment.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 or later (the code also works with .NET Framework 4.7+)
* A licensed copy of **Aspose.Pdf for .NET** (the free trial works for testing)
* An input PDF file named `input.pdf` placed in a folder you can reference from code
* Visual Studio 2022 or any IDE that supports C# development

The tutorial assumes you are familiar with basic C# syntax and the concept of PDF pages.

## Step 1: Load the source PDF and access the first page

The first operation is to open the PDF file and retrieve the page whose resources you want to modify. Aspose.Pdf represents each page as a `Page` object, and every page contains a **resource dictionary** that stores graphics states, fonts, XObjects, and more.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

// Load the PDF you want to edit
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Get the first page (pages are 1‑based in Aspose.Pdf)
    Page firstPage = pdfDocument.Pages[1];
```

*Why this matters:* The `Document` class loads the file into memory, and `Pages[1]` gives you direct access to the first page’s resource dictionary, which is where a graphics state lives.

## Step 2: Open the resource dictionary for editing

Aspose.Pdf provides a `DictionaryEditor` helper that lets you treat a resource dictionary like a regular .NET `Dictionary`. This makes it straightforward to read, add, or replace entries such as `ExtGState`.

```csharp
    // Create an editor for the page’s resources
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Why this matters:* `DictionaryEditor` abstracts the low‑level COS objects, letting you work with familiar key/value pairs while still preserving PDF compliance.

## Step 3: Retrieve (or create) the ExtGState dictionary

The **ExtGState** entry holds all external graphics‑state objects for the page. If the dictionary does not exist, Aspose.Pdf will create an empty one for you.

```csharp
    // Ensure the ExtGState dictionary exists
    var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
        ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
        : new CosPdfDictionary(pdfDocument);
```

*Why this matters:* A missing `ExtGState` entry would cause a `KeyNotFoundException` later. This guard lets the code work on PDFs that have never defined a custom graphics state before—an essential part of **edit PDF resources** robustness.

## Step 4: Build the custom graphics state dictionary

A graphics state describes how drawing operations are rendered. To **add transparency PDF**, you need to set the `ca` (fill opacity) and `CA` (stroke opacity) entries, and optionally a blend mode (`BM`). The following code builds a new dictionary with those parameters.

```csharp
    // Create an empty dictionary that will become the new graphics state
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Define the parameters you want for the custom state
    var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
    {
        // Stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        // Fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        // Blend mode – "Normal" is the default, but you can use "Multiply", "Screen", etc.
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };

    // Populate the dictionary with the parameters
    foreach (var param in graphicsStateParams)
        newGraphicsState.Add(param);
```

*Why this matters:* The `ca` and `CA` entries control transparency for fill and stroke operations, respectively. Setting `BM` lets you experiment with different compositing effects, which is useful when you later **add transparency PDF** content such as semi‑transparent shapes or images.

## Step 5: Register the new graphics state under a unique name

Every graphics state in the `ExtGState` dictionary must have a unique name (e.g., `GS0`, `GS1`). You can choose any name that does not clash with existing entries.

```csharp
    // Choose a name that is unlikely to collide with existing states
    const string graphicsStateName = "GS0";

    // Add the new graphics state to the ExtGState dictionary
    extGStateDict.Add(graphicsStateName, newGraphicsState);

    // If the ExtGState entry was missing, attach it back to the page resources
    if (!resourcesEditor.ContainsKey("ExtGState"))
        resourcesEditor["ExtGState"] = extGStateDict;
```

*Why this matters:* By inserting the new dictionary under `GS0`, you make the state addressable from page content streams. The conditional block ensures the `ExtGState` entry is present even for PDFs that started without one—another **edit PDF resources** safeguard.

## Step 6: Use the custom graphics state in the page content (optional)

The previous steps only *define* the graphics state. To actually see the effect, you must reference it in the page’s content stream. Below is a quick example that draws a semi‑transparent rectangle using the state we just created.

```csharp
    // Get the page’s content stream (or create a new one if empty)
    var content = firstPage.Contents[1];
    var graphics = new ContentWriter(content);

    // Save current graphics state
    graphics.WriteOperator(OperatorName.SaveState);
    // Set the custom graphics state we just defined
    graphics.WriteOperand($"/{graphicsStateName}");
    graphics.WriteOperator(OperatorName.SetExtGState);
    // Draw a rectangle (coordinates are in points)
    graphics.WriteOperand(100);   // lower‑left x
    graphics.WriteOperand(500);   // lower‑left y
    graphics.WriteOperand(200);   // width
    graphics.WriteOperand(100);   // height
    graphics.WriteOperator(OperatorName.Rectangle);
    // Fill the rectangle using the current fill opacity (ca = 0.5)
    graphics.WriteOperator(OperatorName.Fill);
    // Restore the previous graphics state
    graphics.WriteOperator(OperatorName.RestoreState);
```

*Why this matters:* The `SetExtGState` operator (`gs`) tells the PDF renderer to apply the parameters defined in `GS0`. The rectangle will appear with 50 % fill opacity while its stroke remains fully opaque.

## Step 7: Save the modified PDF

Finally, write the changes back to disk. You can overwrite the original file or create a new one.

```csharp
    // Save the updated PDF
    pdfDocument.Save("YOUR_DIRECTORY/output_with_custom_gs.pdf");
}
```

When you open `output_with_custom_gs.pdf` in a PDF viewer, you should see a semi‑transparent rectangle on the first page. This confirms that you successfully **create custom graphics state**, **edit PDF resources**, and **add transparency PDF** content.

## Common variations and edge cases

| Situation | What to adjust |
|-----------|----------------|
| **Multiple pages need the same state** | Register the graphics state once (steps 1‑5) and reference `GS0` on any page’s content stream. |
| **Different opacity per element** | Define additional states (`GS1`, `GS2`, …) with different `ca`/`CA` values and switch between them using `SetExtGState`. |
| **Blend mode other than Normal** | Replace `"Normal"` with `"Multiply"`, `"Screen"`, or any PDF‑standard blend mode in the `BM` entry. |
| **Name collision** | Before adding, check `extGStateDict.ContainsKey(yourName)` and pick a unique suffix if needed. |
| **PDF already contains an ExtGState dictionary** | The code in Step 3 already re‑uses the existing dictionary, so no extra handling is required. |

**Pro tip:** When working with large PDFs, wrap the `Document` usage in a `using` block (as shown) to release native resources promptly. Also, consider enabling Aspose.Pdf’s `PdfCompliance` property if you need to guarantee PDF/A or PDF/X conformance after editing resources.

## Full working example

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Load the PDF you want to edit
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 1: Get the first page
            Page firstPage = pdfDocument.Pages[1];

            // Step 2: Open the page resources for editing
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 3: Retrieve or create the ExtGState dictionary
            var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
                ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
                : new CosPdfDictionary(pdfDocument);

            // Step 4: Build a custom graphics state (50 % fill opacity, 100 % stroke opacity)
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var param in graphicsStateParams)
                newGraphicsState.Add(param);

            // Step 5: Register the graphics state under the name GS0
            const string graphicsStateName = "GS0";
            extGStateDict.Add(graphicsStateName, newGraphics


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create PDF with Aspose – Add Form Field and Pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [How to Create Custom Tables in PDFs Using Aspose.PDF .NET](/pdf/english/net/tables-lists/create-custom-tables-in-pdfs-aspose-pdf-dot-net/)
- [Create Custom Pdf Stamps Aspose Pdf Net](/pdf/hongkong/net/images-graphics/create-custom-pdf-stamps-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}