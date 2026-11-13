---
category: general
date: 2026-11-12
description: Learn how to change PDF opacity using Aspose.Pdf, add transparency, set
  blend mode, and save modified PDF in C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF opacity
- how to add transparency
- save modified PDF
- how to set blend mode
- set fill opacity
language: en
lastmod: 2026-11-12
og_description: Change PDF opacity with Aspose.Pdf, learn how to add transparency,
  set blend mode, and save modified PDF files in C#.
og_image_alt: Screenshot of a PDF page with altered opacity using Aspose.Pdf
og_title: Change PDF opacity with Aspose.Pdf – add transparency and save
schemas:
- author: Aspose
  dateModified: '2026-11-12'
  description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  headline: Change PDF opacity with Aspose.Pdf and save the file
  type: TechArticle
- description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  name: Change PDF opacity with Aspose.Pdf and save the file
  steps:
  - name: Load the PDF document
    text: Start by creating a `Document` instance that points to your source file.
      The constructor reads the entire PDF into memory, allowing you to manipulate
      its internal objects.
  - name: Access the first page’s resources
    text: Each PDF page stores a *resource dictionary* that holds objects such as
      fonts, images, and graphics states. You need to edit this dictionary to inject
      a new `ExtGState` entry.
  - name: Ensure an ExtGState dictionary exists
    text: The `ExtGState` dictionary holds custom graphics states. If it does not
      exist, the code creates one automatically.
  - name: Define a new graphics state (ExtGState)
    text: A graphics state defines how drawing operations behave. The following dictionary
      sets stroke opacity (`CA`), fill opacity (`ca`), and blend mode (`BM`).
  - name: Register the graphics state in the resource dictionary
    text: Give the new state a name (e.g., `GS0`) and add it to the `ExtGState` dictionary.
      This name will be referenced later in the page content stream.
  - name: Apply the graphics state to page content
    text: To actually see the opacity effect, insert the `/GS0 gs` operator before
      the drawing commands you want to affect. The example below draws a semi‑transparent
      rectangle.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The `Save` method overwrites
      the target file or creates a new one if it does not exist.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Change PDF opacity with Aspose.Pdf and save the file
url: /net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-and-save-the-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Change PDF opacity with Aspose.Pdf and save the file

If you need to **change PDF opacity** in a document, Aspose.Pdf provides a straightforward API to adjust both stroke and fill transparency. This tutorial shows exactly **how to add transparency**, **how to set blend mode**, and **save modified PDF** files with just a few lines of C# code.

You’ll walk through every step—from loading an existing PDF to defining a new graphics state and persisting the changes. By the end of this guide you can:

* Reduce the visibility of vector graphics or images.
* Apply a custom blend mode such as *Normal* or *Multiply*.
* Export the updated file without losing any other content.

The only prerequisite is a working .NET development environment and a reference to the Aspose.Pdf library (version 23.9 or later). No external tools are required.

## Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 SDK or later | Guarantees compatibility with the latest Aspose.Pdf APIs. |
| Aspose.Pdf for .NET NuGet package | Supplies the `Document`, `CosPdfDictionary`, and related classes used in the code. |
| A PDF file to edit (e.g., `input.pdf`) | Serves as the source for opacity changes. |

Install the NuGet package with:

```bash
dotnet add package Aspose.Pdf
```

## Change PDF opacity with Aspose.Pdf

### Step 1: Load the PDF document

Start by creating a `Document` instance that points to your source file. The constructor reads the entire PDF into memory, allowing you to manipulate its internal objects.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;

// Load the existing PDF
var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");
```

> **Why this step?** Loading the file creates a manipulable object model. All subsequent changes operate on this in‑memory representation, ensuring the original file stays untouched until you explicitly save.

### Step 2: Access the first page’s resources

Each PDF page stores a *resource dictionary* that holds objects such as fonts, images, and graphics states. You need to edit this dictionary to inject a new `ExtGState` entry.

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor simplifies access to the page's resource dictionary
var resourcesEditor = new DictionaryEditor(page.Resources);
```

> **Tip:** If your PDF contains multiple pages that need the same opacity, repeat this step for each page or share a single `ExtGState` across pages.

### Step 3: Ensure an ExtGState dictionary exists

The `ExtGState` dictionary holds custom graphics states. If it does not exist, the code creates one automatically.

```csharp
// Get or create the ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                     ?? new CosPdfDictionary(pdfDoc);
resourcesEditor["ExtGState"] = extGStateDict;
```

> **Why this step?** Without an `ExtGState` container, any attempt to reference a new graphics state would fail, resulting in a PDF that ignores your opacity settings.

### Step 4: Define a new graphics state (ExtGState)

A graphics state defines how drawing operations behave. The following dictionary sets stroke opacity (`CA`), fill opacity (`ca`), and blend mode (`BM`).

```csharp
// Create an empty dictionary for the new graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Set desired parameters
var parameters = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (1 = opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (0.5 = 50% transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var param in parameters)
    newGraphicsState.Add(param);
```

> **How to set fill opacity:** The `ca` entry controls the opacity of filled shapes (text, paths). Adjust the numeric value between `0` (fully transparent) and `1` (fully opaque) to meet your design requirements.

> **How to set blend mode:** The `BM` entry selects the compositing algorithm. Common values include `Normal`, `Multiply`, `Screen`, and `Overlay`. Choose the one that matches your visual intent.

### Step 5: Register the graphics state in the resource dictionary

Give the new state a name (e.g., `GS0`) and add it to the `ExtGState` dictionary. This name will be referenced later in the page content stream.

```csharp
// Add the graphics state with a symbolic name
extGStateDict.Add("GS0", newGraphicsState);
```

> **Pro tip:** Use a naming convention like `GS0`, `GS1`, … when you create multiple states. It prevents name collisions and makes debugging easier.

### Step 6: Apply the graphics state to page content

To actually see the opacity effect, insert the `/GS0 gs` operator before the drawing commands you want to affect. The example below draws a semi‑transparent rectangle.

```csharp
// Build a content stream that uses the new graphics state
var content = new MemoryStream();
var writer = new StreamWriter(content);

// Activate the graphics state
writer.WriteLine("q");                 // Save graphics state
writer.WriteLine("/GS0 gs");           // Apply custom ExtGState
writer.WriteLine("0.2 0.5 0.8 rg");    // Set fill color (RGB)
writer.WriteLine("100 500 200 100 re"); // Rectangle (x y width height)
writer.WriteLine("f");                 // Fill rectangle
writer.WriteLine("Q");                 // Restore graphics state
writer.Flush();

content.Position = 0;
page.Contents.Add(new ContentStream(content));
```

> **Why the `q` and `Q` operators?** They push and pop the graphics state stack, ensuring that the opacity change only affects the rectangle and not the rest of the page.

### Step 7: Save the modified PDF

Finally, write the updated document to disk. The `Save` method overwrites the target file or creates a new one if it does not exist.

```csharp
// Persist the changes
pdfDoc.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **How to save modified PDF:** The `Save` call writes all in‑memory modifications, including the new `ExtGState`, to the specified path. You can also stream the result to a `MemoryStream` for web responses.

## Full working example

Below is a single, self‑contained program that incorporates every step described above. Copy it into a console application and run it to verify the opacity change.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Operators;

class ChangePdfOpacityDemo
{
    static void Main()
    {
        // 1. Load the PDF
        var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");

        // 2. Get first page and its resources
        var page = pdfDoc.Pages[1];
        var resourcesEditor = new DictionaryEditor(page.Resources);

        // 3. Ensure ExtGState dictionary exists
        var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                             ?? new CosPdfDictionary(pdfDoc);
        resourcesEditor["Ext


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to save modified PDF with Aspose.Pdf and add transparency](/pdf/english/net/document-manipulation/how-to-save-modified-pdf-with-aspose-pdf-and-add-transparenc/)
- [How to add transparency to PDF using Aspose.PDF in C#](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [How to add graphics state pdf and control transparency with Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}