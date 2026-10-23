---
category: general
date: 2026-10-23
description: How to change PDF opacity using Aspose.Pdf in C#. Learn to edit ExtGState,
  set stroke/fill opacity, and apply blend modes in just a few lines of code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to change PDF opacity
- Aspose.Pdf opacity
- PDF graphics state
- ExtGState dictionary
- C# PDF manipulation
- PDF blend mode
language: en
lastmod: 2026-10-23
og_description: How to change PDF opacity using Aspose.Pdf in C#. Follow this concise
  guide to modify stroke and fill opacity, set blend modes, and save the updated document.
og_image_alt: Screenshot of a PDF page with semi‑transparent graphics created by Aspose.Pdf
  in C#
og_title: How to change PDF opacity in C# – complete Aspose.Pdf tutorial
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: How to change PDF opacity using Aspose.Pdf in C#. Learn to edit ExtGState,
    set stroke/fill opacity, and apply blend modes in just a few lines of code.
  headline: How to change PDF opacity in C# with Aspose.Pdf – step‑by‑step guide
  type: TechArticle
- description: How to change PDF opacity using Aspose.Pdf in C#. Learn to edit ExtGState,
    set stroke/fill opacity, and apply blend modes in just a few lines of code.
  name: How to change PDF opacity in C# with Aspose.Pdf – step‑by‑step guide
  steps:
  - name: Load the PDF document
    text: '```csharp using Aspose.Pdf;'
  - name: Get the first page and its resource dictionary
    text: '```csharp // Step 2: Get the first page and its resource dictionary var
      firstPage = pdfDocument.Pages[1]; var resourcesEditor = new DictionaryEditor(firstPage.Resources);
      ```'
  - name: Retrieve (or create) the ExtGState dictionary
    text: '```csharp // Step 3: Retrieve the ExtGState dictionary from the page resources
      // If ExtGState does not exist, create an empty one. CosPdfDictionary extGStateDict;
      if (resourcesEditor.ContainsKey("ExtGState")) { extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
      } else { extGStateDic'
  - name: Create a new graphics state dictionary and define opacity entries
    text: '```csharp // Step 4: Create a new graphics state dictionary and define
      its entries var graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
      var graphicsStateEntries = new[] { new KeyValuePair<string, ICosPdfPrimitive>("CA",
      new CosPdfNumber(1.0)), // Stroke opacity (fully opaque)'
  - name: Add the new graphics state to the ExtGState dictionary
    text: '```csharp // Step 5: Add the new graphics state to the ExtGState dictionary
      (named "GS0") extGStateDict.Add("GS0", graphicsStateDict); ```'
  - name: Save the updated PDF document
    text: '```csharp // Step 6: Save the updated PDF document pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
      } ```'
  type: HowTo
tags:
- PDF
- C#
- Aspose.Pdf
- Opacity
- GraphicsState
title: How to change PDF opacity in C# with Aspose.Pdf – step‑by‑step guide
url: /net/programming-with-operators/how-to-change-pdf-opacity-in-c-with-aspose-pdf-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to change PDF opacity in C# with Aspose.Pdf – step‑by‑step guide

If you need to **how to change PDF opacity** for specific elements, this tutorial shows a complete, runnable solution. You’ll see how to edit the ExtGState dictionary, set both stroke and fill opacity, and choose a blend mode—all with a few clear lines of C# code.

Changing PDF opacity is useful when you want watermarks, overlay graphics, or subtle visual effects without rebuilding the whole document. The guide assumes you have a basic C# environment and the Aspose.Pdf for .NET library installed.

![how to change PDF opacity using Aspose.Pdf in C#](https://example.com/og-image.png)

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 or later (the code also works with .NET Framework 4.7+)
* A licensed copy of **Aspose.Pdf for .NET** (the free trial works for testing)
* An input PDF file located in a folder you can reference from code
* Visual Studio 2022 or any C# editor you prefer

No additional NuGet packages are required—Aspose.Pdf contains all the types used in this tutorial.

## Understanding the PDF graphics state

A PDF page stores drawing parameters in a **graphics state** object. The **ExtGState** dictionary holds entries such as:

* **CA** – stroke opacity (0 = transparent, 1 = opaque)
* **ca** – fill opacity
* **BM** – blend mode (e.g., *Normal*, *Multiply*, *Screen*)

By creating a new graphics state dictionary and adding it to the page’s ExtGState collection, you can reference the state later in content streams. This approach avoids rewriting the entire page content and works with any existing PDF.

## How to change PDF opacity with Aspose.Pdf

The following six steps cover the entire process—from loading the document to saving the modified file. Each step includes the exact code you need and an explanation of why the step matters.

### Step 1: Load the PDF document

```csharp
using Aspose.Pdf;

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

**Why this matters** – Opening the file with `Aspose.Pdf.Document` gives you full access to the internal PDF structure, including page resources where the **ExtGState** dictionary lives.

### Step 2: Get the first page and its resource dictionary

```csharp
// Step 2: Get the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

**Why this matters** – Every page has a *Resources* dictionary that groups fonts, images, and graphics states. `DictionaryEditor` provides convenient read/write access to that collection.

### Step 3: Retrieve (or create) the ExtGState dictionary

```csharp
// Step 3: Retrieve the ExtGState dictionary from the page resources
// If ExtGState does not exist, create an empty one.
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
```

**Why this matters** – Some PDFs already contain an **ExtGState** entry; others do not. The conditional logic ensures the tutorial works for both cases, making it robust for real‑world files.

### Step 4: Create a new graphics state dictionary and define opacity entries

```csharp
// Step 4: Create a new graphics state dictionary and define its entries
var graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // Fill opacity (50 % transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

**Why this matters** – The three key entries control how drawing commands are rendered:

* `CA = 1.0` keeps stroke lines fully visible.
* `ca = 0.5` makes filled shapes semi‑transparent.
* `BM = Normal` uses the default blend mode; you can replace `"Normal"` with `"Multiply"` or `"Screen"` for creative effects.

### Step 5: Add the new graphics state to the ExtGState dictionary

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary (named "GS0")
extGStateDict.Add("GS0", graphicsStateDict);
```

**Why this matters** – Naming the entry `"GS0"` creates a reference you can later use in a content stream (`/GS0 gs`). If you need multiple opacity variations, add additional entries (`"GS1"`, `"GS2"`, …) with different `CA`/`ca` values.

### Step 6: Save the updated PDF document

```csharp
// Step 6: Save the updated PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

**Why this matters** – Persisting the changes writes the modified **ExtGState** dictionary back to the file. The resulting PDF now contains a reusable graphics state that any drawing command can invoke.

## Applying the new graphics state to page content

The steps above only create the graphics state; you still need to reference it in the page’s content stream. Here’s a quick example that draws a semi‑transparent rectangle using the state we just added:

```csharp
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    var page = pdfDocument.Pages[1];
    var content = new PageContentEditor(page);
    // Begin the graphics state GS0
    content.InsertContent(0, "q /GS0 gs\n"); // Save graphics state and apply GS0
    // Draw a rectangle (100,100) to (300,300)
    content.InsertContent(0, "0.2 0.6 0.8 rg\n"); // Set fill color (light blue)
    content.InsertContent(0, "100 100 200 200 re\n");
    content.InsertContent(0, "f\n"); // Fill rectangle with current fill opacity
    // Restore graphics state
    content.InsertContent(0, "Q\n");
    pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

**Explanation** – The `q` operator saves the current graphics state, `/GS0 gs` applies the opacity settings, the rectangle is drawn, and `Q` restores the original state. You can place this snippet anywhere on the page, before or after existing content, depending on the visual layering you need.

## Common pitfalls and how to avoid them

| Symptom | Cause | Fix |
|---------|-------|-----|
| Opacity appears unchanged | The page has no ExtGState entry or the content does not reference the new state. | Verify that `ExtGState` exists and that the content stream contains `/GS0 gs` (or the name you chose). |
| Blend mode has no effect | Using an incompatible color space or PDF version. | Ensure the PDF version is at least 1.4 (required for transparency) and that you are not mixing spot colors with blend modes. |
| Document fails to open in older viewers | Transparency not supported in PDF 1.3 or earlier. | Set `pdfDocument.Version = 1.4;` before saving, or upgrade the PDF version explicitly. |

## Testing the result

Open `output.pdf` in Adobe Acrobat Reader, Foxit, or any modern PDF viewer. You should see the rectangle rendered with 50 % fill opacity while its border remains fully opaque. Use the *Edit → Preferences → Accessibility* options to toggle “Use high‑contrast colors” and confirm that the semi‑transparent effect persists.

If you need to verify programmatically, Aspose.Pdf lets you read back the graphics state:

```csharp
var gs = pdfDocument.Pages[1].Resources["ExtGState"]["GS0"].ToCosPdfDictionary();
var fillOpacity = ((CosPdfNumber)gs["ca"]).Value; // Should be 0.5
```

## Extending the technique

* **Multiple opacity levels** – Add more entries (`"GS1"`, `"GS2"`) with different `ca` values and reference them where needed.
* **Different blend modes** – Replace `"Normal"` with `"Multiply"` or `"Screen"` to achieve artistic overlays.
* **Applying to images** – Use the same graphics state before an `Do` operator that draws an XObject image.

These variations let you build watermarks, highlight sections, or create complex visual designs without rasterizing the PDF.

## Conclusion

You now know **how to change PDF opacity** in C# using Aspose.Pdf. By creating a custom graphics state, adding it to the page’s ExtGState dictionary, and invoking the state in a content stream, you gain fine‑grained control over stroke and fill transparency as well as blend modes. The complete example is ready to copy, run, and adapt to any PDF manipulation scenario you encounter.

Ready for the next challenge? Try combining this technique with **Aspose.Pdf opacity** on images, or explore **PDF blend mode** effects to produce professional‑grade overlays. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Change PDF Opacity with Aspose.PDF – Complete C# Guide](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Change opacity PDF in C# with Aspose.Pdf – step‑by‑step guide](/pdf/english/net/programming-with-pdf-pages/change-opacity-pdf-in-c-with-aspose-pdf-step-by-step-guide/)
- [How to change PDF transparency in C# using Aspose.Pdf](/pdf/english/net/programming-with-operators/how-to-change-pdf-transparency-in-c-using-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}