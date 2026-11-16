---
category: general
date: 2026-11-16
description: Learn how to create PDF graphics state in C# using Aspose.Pdf. This guide
  covers opacity, blend mode, and full code example.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf graphics state
- Aspose.Pdf ExtGState
- PDF opacity
- C# PDF manipulation
- PDF blend mode
- Aspose.Pdf graphics state
language: en
lastmod: 2026-11-16
og_description: Create PDF graphics state in C# with Aspose.Pdf. Follow this complete
  tutorial to set opacity and blend mode programmatically.
og_image_alt: Illustration of how to create PDF graphics state with Aspose.Pdf in
  C#
og_title: Create PDF graphics state in C# – step‑by‑step Aspose.Pdf guide
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to create PDF graphics state in C# using Aspose.Pdf. This
    guide covers opacity, blend mode, and full code example.
  headline: How to create PDF graphics state in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF
title: How to create PDF graphics state in C# with Aspose.Pdf
url: /net/images-graphics/how-to-create-pdf-graphics-state-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create PDF graphics state in C# with Aspose.Pdf

If you need to **create PDF graphics state** in a .NET project, this tutorial shows you exactly how to do it with Aspose.Pdf. Whether you want to control opacity, change blend mode, or reuse a custom graphics state across pages, the steps below give you a complete, ready‑to‑run solution.

In this guide you’ll learn how to access the page resources, add an **ExtGState** entry, and persist the changes to a new file. The example works with Aspose.Pdf 23.12 (or later) and targets .NET 6+, but the concepts apply to earlier versions as well.

## Prerequisites

Before you start, make sure you have:

* Visual Studio 2022 (or any C# IDE) with .NET 6 SDK installed.  
* An Aspose.Pdf for .NET license or a temporary evaluation key.  
* A PDF file named `input.pdf` placed in a folder you can reference from code.  

No additional NuGet packages are required beyond `Aspose.Pdf`.

## What the tutorial covers

* Loading an existing PDF document.  
* Navigating to the first page’s resources dictionary.  
* Creating a new graphics state dictionary that defines stroke opacity (`CA`), fill opacity (`ca`), and blend mode (`BM`).  
* Adding the new graphics state to the **ExtGState** collection with a custom name (`GS0`).  
* Saving the updated PDF so that subsequent drawing commands can reference the new state.

By the end of the tutorial you’ll be able to **create PDF graphics state** objects programmatically and reuse them in any drawing operation.

## Step 1: Set up the project and import namespaces

Create a new console application (or integrate the code into an existing project). Add the Aspose.Pdf reference and include the required namespaces:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Generator;
```

> **Pro tip:** If you’re using the free evaluation version, add `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` before loading the document to avoid watermark messages.

## Step 2: Load the PDF document

Opening the file is straightforward. The `Document` class represents the entire PDF and gives you access to its pages and resources.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";

using (var document = new Document(inputPath))
{
    // All subsequent steps run inside this using block
```

Placing the code inside a `using` block guarantees that the file handle is released after the operation, which is essential for **C# PDF manipulation** in production services.

## Step 3: Retrieve the first page’s resources dictionary

Every PDF page has a *Resources* dictionary that stores fonts, images, and graphics states. We need a `DictionaryEditor` to edit that structure.

```csharp
    // Step 3: Get the first page and its resources dictionary
    var page = document.Pages[1];
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

If the PDF already contains an `ExtGState` entry, `resourcesEditor["ExtGState"]` will return it; otherwise, Aspose.Pdf creates an empty dictionary for us when we add the first entry.

## Step 4: Access or create the ExtGState dictionary

The **ExtGState** dictionary holds named graphics state objects. We either fetch an existing one or create a new container.

```csharp
    // Step 4: Access (or create) the ExtGState dictionary within the resources
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

When `ExtGState` does not exist, `resourcesEditor["ExtGState"]` returns a new empty dictionary automatically, ensuring the code works for any PDF.

## Step 5: Build the new graphics state dictionary

A graphics state is a `CosPdfDictionary` with specific keys:

* `CA` – stroke opacity (0‑1)  
* `ca` – fill opacity (0‑1)  
* `BM` – blend mode (`Normal`, `Multiply`, etc.)

We create an empty dictionary, populate it, and then add it to `ExtGState`.

```csharp
    // Step 5: Create a new graphics state dictionary with desired parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (50% transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };

    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

You can change `0.5` to any value between `0` and `1` to adjust fill opacity, or replace `"Normal"` with `"Multiply"` for a different **PDF blend mode**. This flexibility is why creating a custom graphics state is a powerful technique in **Aspose.Pdf graphics state** handling.

## Step 6: Register the graphics state with a name

PDF content streams refer to graphics states by name. Here we use `GS0`, but any unique name works.

```csharp
    // Step 6: Add the new graphics state to the ExtGState dictionary with a name (e.g., GS0)
    extGState.Add("GS0", newGraphicsState);
```

If you need multiple states, repeat the creation step with different parameters and add them as `GS1`, `GS2`, etc. This pattern scales well for complex documents that require varied opacity or blend settings on different layers.

## Step 7: Save the modified PDF

Finally, write the updated document to a new file. Keeping the original intact makes debugging easier.

```csharp
    // Step 7: Save the updated PDF document
    string outputPath = @"YOUR_DIRECTORY\output.pdf";
    document.Save(outputPath);
}
```

After execution, `output.pdf` contains an `ExtGState` entry named `GS0`. Any subsequent drawing operator can reference it using the `gs` operator (e.g., `GS0 gs` in a content stream).  

> **Why this matters:** By creating a reusable graphics state you avoid repeating opacity and blend settings for each drawing command, which improves both performance and maintainability.

## Using the new graphics state in a content stream (optional)

If you want to see the effect immediately, you can add a simple rectangle that uses the state we just created:

```csharp
using (var document = new Document(outputPath))
{
    var page = document.Pages[1];
    var content = page.Contents[1]; // Get the first content stream

    // Insert graphics state selection and a semi‑transparent rectangle
    var operators = new List<Operator>
    {
        new Operator("GS0", "gs"),                     // Select our custom graphics state
        new Operator("0.5", "w"),                      // Set line width (optional)
        new Operator("100", "100", "200", "150", "re"), // Rectangle (x, y, width, height)
        new Operator("B")                              // Stroke the rectangle
    };

    foreach (var op in operators)
        content.Operators.Add(op);

    document.Save(@"YOUR_DIRECTORY\final_output.pdf");
}
```

The rectangle will be drawn with 50 % fill opacity while the stroke remains fully opaque, exactly as defined in the **create PDF graphics state** dictionary.

## Common pitfalls and how to avoid them

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| `ExtGState` entry not found | Some PDFs omit the dictionary entirely. | The `DictionaryEditor` automatically creates it when you add the first entry, so no extra check is needed. |
| Opacity values > 1 or < 0 | PDF spec limits opacity to the range `[0,1]`. | Clamp values before creating `CosPdfNumber`. |
| Blend mode typo | PDF blend mode names are case‑sensitive. | Use exact names like `"Normal"`, `"Multiply"`, `"Screen"`. |
| License watermark | Evaluation version adds a watermark on the first page. | Apply a valid license file before opening the document. |

Addressing these edge cases ensures your **create PDF graphics state** implementation works reliably across different PDF sources.

## Full, runnable example

Below is a self‑contained program you can copy, paste, and run. Replace `YOUR_DIRECTORY` with an actual folder path on your machine.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;

class Program
{
    static void Main()
    {
        // Optional: apply license to remove evaluation watermark
        // var license = new Aspose.Pdf.License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        using (var document = new Document(inputPath))
        {
            // 1️⃣ Get first page and its resources
            var page = document.Pages[1];
            var resourcesEditor = new DictionaryEditor(page.Resources);

            // 2️⃣ Access (or create) ExtGState dictionary
            var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // 3️⃣ Build new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // 4️⃣ Register the state with a name (GS0)
            extGState.Add("


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create custom graphics state in PDF using Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Add graphics state to PDF using Aspose.PDF for .NET (C#)](/pdf/english/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/)
- [How to create empty graphics state in a PDF with C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}