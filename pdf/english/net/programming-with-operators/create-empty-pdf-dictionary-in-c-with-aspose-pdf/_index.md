---
category: general
date: 2026-08-14
description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
  a graphics state to the ExtGState collection and modify PDFs programmatically.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.Pdf Document
- PDF graphics state
- ExtGState dictionary
- CosPdfDictionary usage
language: en
lastmod: 2026-08-14
og_description: Create empty PDF dictionary in C# with Aspose.Pdf. Follow this complete
  guide to add a custom graphics state to a PDF’s ExtGState collection.
og_image_alt: Screenshot showing C# code that creates an empty PDF dictionary with
  Aspose.Pdf
og_title: Create empty PDF dictionary in C# – Aspose.Pdf step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  headline: Create empty PDF dictionary in C# with Aspose.Pdf
  type: TechArticle
- description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  name: Create empty PDF dictionary in C# with Aspose.Pdf
  steps:
  - name: Create a new **Console App** project in Visual Studio.
    text: Create a new **Console App** project in Visual Studio.
  - name: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
    text: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
  - name: 'Add the following `using` directives at the top of `Program.cs`:'
    text: 'Add the following `using` directives at the top of `Program.cs`:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Create empty PDF dictionary in C# with Aspose.Pdf
url: /net/programming-with-operators/create-empty-pdf-dictionary-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create empty PDF dictionary in C# with Aspose.Pdf

If you need to **create empty PDF dictionary** objects while working with PDF files, this guide shows you exactly how to do it in C# using the Aspose.Pdf library. Whether you are building a custom graphics state, adding a new resource, or preparing a template for later use, the steps below give you a complete, runnable solution.

You’ll learn how to load a PDF, access the first page’s resource dictionary, build a brand‑new `CosPdfDictionary`, and insert it into the `ExtGState` collection. By the end of the tutorial you will have a working `output.pdf` that contains the newly created dictionary.

## Prerequisites

Before you start, make sure you have:

- .NET 6.0 or later (the code also works with .NET Framework 4.6+)
- Visual Studio 2022 or any C# IDE you prefer
- An Aspose.Pdf for .NET license (or a temporary evaluation key)
- A sample PDF named **input.pdf** placed in a folder you control (the folder path will be used as `dataDir`)

No additional NuGet packages are required beyond `Aspose.Pdf`.

## Step 1: Set up the project and reference Aspose.Pdf

1. Create a new **Console App** project in Visual Studio.  
2. Open the **NuGet Package Manager** and install `Aspose.Pdf`:

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. Add the following `using` directives at the top of `Program.cs`:

   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Text;
   using Aspose.Pdf.Operators;
   using Aspose.Pdf.Facades;
   using Aspose.Pdf.InteractiveFeatures;
   using Aspose.Pdf.Xmp;
   using Aspose.Pdf.Operators.Filters;
   using Aspose.Pdf.Operators.Gfx;
   ```

   *Why these namespaces?* `Aspose.Pdf` contains the core `Document` class, while `Aspose.Pdf.Operators.Gfx` provides `CosPdfDictionary`, `CosPdfNumber`, and related low‑level PDF objects needed to **create empty PDF dictionary** structures.

## Step 2: Load the source PDF

The first operation is to load the existing PDF file into a `Document` instance. This gives you access to all pages, resources, and low‑level dictionaries.

```csharp
// Step 2: Load the PDF document
string dataDir = @"C:\MyPdfFolder\";               // Change to your folder
using var pdfDocument = new Document(dataDir + "input.pdf");
```

*Explanation*: `Document` reads the file into memory and prepares internal structures. The `using` statement ensures the file handle is released after we finish processing.

## Step 3: Access the first page’s resource dictionary

Every PDF page has a **Resources** dictionary that groups fonts, images, ExtGState objects, and other shared resources. To insert a new graphics state we need to edit this dictionary.

```csharp
// Step 3: Get the first page and its Resources dictionary
Page firstPage = pdfDocument.Pages[1];                     // PDF pages are 1‑based
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` is a helper class that lets you treat a PDF dictionary like a C# `Dictionary<string, object>`.

## Step 4: Retrieve (or create) the ExtGState collection

`ExtGState` holds graphics state objects such as opacity, blend mode, and line width. If the source PDF already contains an `ExtGState` entry, we reuse it; otherwise we create a new empty dictionary.

```csharp
// Step 4: Ensure an ExtGState dictionary exists
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a brand‑new ExtGState dictionary and add it to Resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*Why this check?* Some PDFs omit the `ExtGState` entry altogether. By handling both cases, the tutorial remains robust for any input file.

## Step 5: **Create empty PDF dictionary** for a new graphics state

Now we actually **create empty PDF dictionary** objects that define the graphics state parameters. The dictionary starts empty, and we add the required keys:

```csharp
// Step 5: Build a new graphics state dictionary (empty PDF dictionary + entries)
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Stroke opacity (CA) – 1 means fully opaque strokes
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes semi‑transparent fills
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default compositing mode
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

### What each entry does

| Key | Type | Meaning |
|-----|------|---------|
| **CA** | `CosPdfNumber` | Stroke opacity (range 0‑1). |
| **ca** | `CosPdfNumber` | Fill opacity (range 0‑1). |
| **BM** | `CosPdfName`   | Blend mode; `"Normal"` is the most common. |

Because we started with an **empty PDF dictionary**, we have full control over which entries are added. You can extend this dictionary with additional graphics state parameters such as `LW` (line width) or `LC` (line cap) whenever needed.

## Step 6: Insert the new graphics state into ExtGState

The `ExtGState` dictionary works like a map where each entry is identified by a name (e.g., `GS0`, `GS1`). We add our freshly built dictionary under a unique key.

```csharp
// Step 6: Add the graphics state to the ExtGState collection
extGStateDict.Add("GS0", newGraphicsState);
```

If you plan to add multiple states, increment the suffix (`GS1`, `GS2`, …) to avoid name collisions.

## Step 7: Save the modified PDF

Finally, write the changes back to disk. The `Save` method automatically serializes the updated dictionaries.

```csharp
// Step 7: Persist the changes
pdfDocument.Save(dataDir + "output.pdf");
```

Open `output.pdf` in any PDF viewer and inspect the **Resources → ExtGState** entry (most viewers hide this, but tools like Adobe Acrobat Preflight or PDF‑Tron can reveal it). You should see a `GS0` entry containing the opacity and blend mode values you defined.

## Complete working example

Putting all the pieces together, here is the full program you can copy‑paste into `Program.cs` and run:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators.Gfx;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string dataDir = @"C:\MyPdfFolder\"; // <-- change to your folder
        using var pdfDocument = new Document(dataDir + "input.pdf");

        // -----------------------------------------------------------------
        // 2️⃣ Access the first page’s Resources dictionary
        // -----------------------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // -----------------------------------------------------------------
        // 3️⃣ Retrieve or create the ExtGState dictionary
        // -----------------------------------------------------------------
        CosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourcesEditor["ExtGState"] = extGStateDict;
        }

        // -----------------------------------------------------------------
        // 4️⃣ **Create empty PDF dictionary** for a new graphics state
        // -----------------------------------------------------------------
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode

        // -----------------------------------------------------------------
        // 5️⃣ Add the graphics state to ExtGState
        // -----------------------------------------------------------------
        extGStateDict.Add("GS0", newGraphicsState);

        // -----------------------------------------------------------------
        // 6️⃣ Save the modified PDF
        // -----------------------------------------------------------------
        pdfDocument.Save(dataDir + "output.pdf");

        Console.WriteLine("PDF saved with new empty dictionary at: " + dataDir + "output.pdf");
    }
}
```

**Expected output** – The console prints a confirmation line, and `output.pdf` contains the new `GS0` entry under `ExtGState`. When you render a page that references `GS0` (e.g., via a content stream operator `gs`), strokes will be fully opaque while fills are 50 % transparent.

## Common questions and edge‑case handling

| Question | Answer |
|----------|--------|
| *What if the PDF has multiple pages?* | The example targets the first page (`Pages[1]`). To affect all pages, loop through `pdfDocument.Pages` and repeat steps 3‑5 for each page’s resources. |
| *Can I add the dictionary to a page that already has an ExtGState entry named “GS0”?* | Yes, but you must use a different key (`GS1`, `GS2`, …) to avoid overwriting the existing entry. |
| *Is it safe to modify the dictionary after saving?* | Once you call `Save`, the in‑memory representation is detached from the file. You can continue editing the `Document` object and call `Save` again if needed. |
| *Do I need a license for Aspose.Pdf to use `


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [How to Remove Graphics from PDFs Using Aspose.PDF .NET&#58; A Complete Guide](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [How to Create Multi-Layer PDFs Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/advanced-features/create-multi-layer-pdfs-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}