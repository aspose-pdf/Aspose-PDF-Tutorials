---
category: general
date: 2026-09-24
description: Learn how to change PDF transparency in C# with Aspose.Pdf. This step‑by‑step
  guide covers PDF opacity, blend mode and graphics state editing.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.Pdf graphics state
- PDF opacity
- C# PDF manipulation
- blend mode PDF
- modify PDF resources
language: en
lastmod: 2026-09-24
og_description: Change PDF transparency in C# using Aspose.Pdf. Follow this guide
  to edit PDF opacity, blend mode, and graphics state for professional document output.
og_image_alt: Screenshot showing C# code that changes PDF transparency
og_title: Change PDF transparency in C# – complete Aspose.Pdf guide
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Learn how to change PDF transparency in C# with Aspose.Pdf. This step‑by‑step
    guide covers PDF opacity, blend mode and graphics state editing.
  headline: How to change PDF transparency in C# using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- C#
- Aspose.Pdf
- Transparency
title: How to change PDF transparency in C# using Aspose.Pdf
url: /net/programming-with-operators/how-to-change-pdf-transparency-in-c-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to change PDF transparency in C# using Aspose.Pdf

If you need to **change PDF transparency** in a .NET project, this guide shows you exactly how to do it with Aspose.Pdf. You’ll see a complete, runnable example that modifies PDF opacity, sets a blend mode, and updates the page’s graphics state dictionary.

Changing PDF transparency is a common requirement when you want watermarks, overlay graphics, or custom visual effects. In this tutorial you’ll learn to edit the **Aspose.Pdf graphics state**, adjust **PDF opacity**, and work with **blend mode PDF** settings—all using clean C# code.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 or later installed  
* An Aspose.Pdf for .NET license (or a temporary evaluation key)  
* A PDF file named `input.pdf` in a folder you can reference as `YOUR_DIRECTORY`  
* Basic familiarity with C# and Visual Studio (any IDE works)

No additional NuGet packages are required beyond `Aspose.Pdf`. The code runs on Windows, Linux, or macOS because Aspose.Pdf is cross‑platform.

## Change PDF transparency – step 1: open the PDF document

The first operation is to load the source PDF. Using a `using` block guarantees that the file handle is released automatically.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System.Collections.Generic;

string inputPath  = @"YOUR_DIRECTORY\input.pdf";
string outputPath = @"YOUR_DIRECTORY\output.pdf";

using (var document = new Document(inputPath))
{
    // The document is now ready for manipulation.
```

Opening the document is the foundation for any **C# PDF manipulation** task. If the file cannot be found, Aspose.Pdf throws a `FileNotFoundException`, so double‑check the path before running the code.

## Access the page resources with Aspose.Pdf graphics state

Next, retrieve the first page and its resource dictionary. The resource dictionary holds objects like fonts, images, and **ExtGState** entries that control graphics parameters.

```csharp
    // Step 2: Get the first page of the document
    var page = document.Pages[1];

    // Step 3: Access the page's resource dictionary for editing
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

The `DictionaryEditor` class provides a convenient wrapper for reading and writing PDF dictionaries. Here we focus on the **ExtGState** dictionary because it stores transparency settings.

## Create and configure a new graphics state for PDF opacity

Now we build a fresh graphics state dictionary. This dictionary will hold the parameters that define stroke opacity (`CA`), fill opacity (`ca`), and the blend mode (`BM`).

```csharp
    // Step 4: Retrieve the existing ExtGState dictionary (graphics states)
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

    // Step 5: Create a new empty graphics state dictionary
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

    // Step 6: Define graphics state parameters (stroke opacity, fill opacity, blend mode)
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),            // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),          // Fill opacity (50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))       // Blend mode PDF (standard normal blending)
    };

    // Step 7: Add each parameter to the new graphics state dictionary
    foreach (var param in parameters)
        newGraphicsState.Add(param);
```

* **`CA`** controls the opacity of stroke operations (lines, borders).  
* **`ca`** controls the opacity of fill operations (filled shapes, text).  
* **`BM`** selects the blend mode; `"Normal"` is the default, but you could use `"Multiply"` or `"Screen"` for artistic effects.

These settings are the core of **PDF opacity** manipulation. Adjust the numeric values to suit your visual design—`0` means fully transparent, `1` means fully opaque.

## Insert the graphics state and save the document

After constructing the new state, we add it to the existing **ExtGState** dictionary under a unique name (`GS0`). Finally, we save the altered PDF.

```csharp
    // Step 8: Insert the new graphics state into the ExtGState dictionary with a name
    extGState.Add("GS0", newGraphicsState);

    // Step 9: Save the modified PDF document
    document.Save(outputPath);
}
```

When the PDF is opened in a viewer, any content that references `GS0` will render with the defined transparency. You can later apply this graphics state to specific objects using the `GraphicsState` property of drawing commands (e.g., `page.Contents.Add(new TextFragment(...){ GraphicsState = "GS0" })`).

## Verify the result

Open `output.pdf` in Adobe Acrobat Reader, Foxit, or any PDF viewer that supports transparency. You should see the first page’s fill elements rendered at 50 % opacity while strokes remain fully opaque. If you don’t notice a change, ensure that the page actually uses the new graphics state—otherwise, you can explicitly assign `GS0` to the objects you want to affect.

![Change PDF transparency in C# code example](path/to/image.png){: .img-responsive alt="Change PDF transparency in C# code example"}

*The image above shows the complete C# source that changes PDF transparency.*

## Common variations and edge cases

| Situation | How to adapt the code |
|-----------|-----------------------|
| **Multiple pages** | Loop over `document.Pages` and repeat steps 2‑8 for each page. |
| **Different blend mode** | Replace `"Normal"` with `"Multiply"`, `"Screen"`, or any PDF‑standard blend name. |
| **Higher fill opacity** | Change `new CosPdfNumber(0.5)` to a value between `0` and `1`. |
| **No existing ExtGState** | If `resourcesEditor["ExtGState"]` returns `null`, create a new dictionary: `var extGState = CosPdfDictionary.CreateEmptyDictionary(document); resourcesEditor["ExtGState"] = extGState;` |

These variations demonstrate the flexibility of **modify PDF resources** using Aspose.Pdf. By adjusting the parameters, you can produce watermarks, semi‑transparent overlays, or custom UI elements inside a PDF.

## Full, runnable example

Below is the complete program you can copy‑paste into a new Console App project. It contains all necessary `using` directives, error handling, and comments.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;

namespace PdfTransparencyDemo
{
    class Program
    {
        static void Main()
        {
            // Paths – replace YOUR_DIRECTORY with an actual folder on your machine
            string inputPath  = @"YOUR_DIRECTORY\input.pdf";
            string outputPath = @"YOUR_DIRECTORY\output.pdf";

            try
            {
                // Step 1: Open the PDF document
                using (var document = new Document(inputPath))
                {
                    // Step 2: Get the first page
                    var page = document.Pages[1];

                    // Step 3: Edit the page's resources
                    var resourcesEditor = new DictionaryEditor(page.Resources);

                    // Step 4: Get or create the ExtGState dictionary
                    CosPdfDictionary extGState;
                    if (resourcesEditor.ContainsKey("ExtGState"))
                        extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
                    else
                    {
                        extGState = CosPdfDictionary.CreateEmptyDictionary(document);
                        resourcesEditor["ExtGState"] = extGState;
                    }

                    // Step 5: Create a new graphics state
                    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

                    // Step 6: Define opacity and blend mode
                    var parameters = new[]
                    {
                        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
                    };

                    // Step 7: Populate the graphics state
                    foreach (var param in parameters)
                        newGraphicsState.Add(param);

                    // Step 8: Add the new state to ExtGState with a unique name
                    extGState.Add("GS0", newGraphicsState);

                    // Optional: Apply the graphics state to existing content
                    // Example: make all text use the new transparency
                    // var textFragment = new TextFragment("Sample text") { GraphicsState = "GS0" };
                    // page.Paragraphs.Add(text


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Change PDF Opacity with Aspose.PDF – Complete C# Guide](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Change PDF Opacity in C# – Complete Aspose Guide](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-in-c-complete-aspose-guide/)
- [Add Transparency to PDF using Aspose – Complete C# Guide](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}