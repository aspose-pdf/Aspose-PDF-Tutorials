---
category: general
date: 2026-03-22
description: Add Bates numbering PDF quickly with Aspose.Pdf. Learn how to add bates,
  add sequential page numbers, add custom footer pdf, and add artifact to pdf in minutes.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- add custom footer pdf
- add artifact to pdf
language: en
og_description: Add Bates numbering PDF using Aspose.Pdf. This guide shows how to
  add bates, add sequential page numbers, add custom footer pdf, and add artifact
  to pdf.
og_title: Add Bates Numbering PDF – Step‑by‑Step C# Tutorial
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Add Bates Numbering PDF – Complete C# Guide
url: /net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Bates Numbering PDF – Complete C# Guide

Ever needed to **add bates numbering pdf** to a batch of legal documents but weren’t sure where to start? You’re not the first—many developers hit that wall when building case‑management tools. The good news? With Aspose.Pdf you can **add bates**, **add sequential page numbers**, and even **add custom footer pdf** elements in just a few lines of code.  

In this tutorial we’ll walk through the whole process, from installing the library to saving the final file, and we’ll sprinkle in tips on how to **add artifact to pdf** files without breaking existing content. By the end you’ll have a ready‑to‑run snippet that you can drop into any .NET project.

## What You’ll Need

- .NET 6+ (the code works on .NET Core and .NET Framework alike)  
- A valid Aspose.Pdf for .NET license (you can start with a free evaluation)  
- An input PDF (`input.pdf`) placed in a folder you can reference  
- Visual Studio, Rider, or any C# editor you prefer  

That’s it—no extra NuGet packages besides Aspose.Pdf.

## Step 1: Install Aspose.Pdf via NuGet

First things first—let’s get the library onto your machine. Open a terminal in your project folder and run:

```bash
dotnet add package Aspose.Pdf
```

Or, if you’re using Visual Studio’s Package Manager Console:

```powershell
Install-Package Aspose.Pdf
```

*Pro tip:* After installation, double‑check that the `Aspose.Pdf` folder appears under `Dependencies → Packages` in your solution explorer.

## Step 2: Load the Source PDF Document

Now we create a `Document` object that represents the PDF we want to stamp. Using the `using` statement ensures the file handle is released automatically.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing; // For Color

// Step 2: Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

Why use `using var`? It guarantees disposal even if an exception occurs, preventing file‑locking issues later when you try to overwrite the same file.

## Step 3: Create and Configure a Bates Numbering Artifact

A Bates number is essentially a text artifact that lives in the PDF’s logical structure. You can treat it like a **custom footer pdf** because it appears on every page without being part of the page’s content stream.

```csharp
// Step 3: Define the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "INV-",          // Optional prefix – change as needed
    Start = 1000,             // Starting number
    Format = "0000",          // Zero‑padded format (e.g., 1000 → 1000)
    X = 500,                  // Horizontal position (points from left)
    Y = 20,                   // Vertical position (points from bottom)
    FontSize = 10,
    FontColor = Color.Black
};
```

### Why These Settings Matter

- **Prefix**: Useful for distinguishing document types (e.g., “INV‑” for invoices).  
- **Start**: Sets the first number; you can feed this from a database if you need continuity across files.  
- **Format**: `"0000"` forces a four‑digit display, ensuring alignment when numbers grow.  
- **X/Y**: Coordinates are measured from the bottom‑left corner, so `Y = 20` places the text just above the page margin. Adjust `X` if you want the number left‑aligned or centered.

If you need to **add sequential page numbers** instead of Bates numbers, simply omit `Prefix` and adjust `Format` to `"###"` or any pattern you prefer.

## Step 4: Apply the Artifact to All Pages

Aspose.Pdf lets you attach an artifact to the entire document in a single call. This is the most efficient way to **add artifact to pdf** without looping through each page manually.

```csharp
// Step 4: Apply the artifact to the whole document
pdfDocument.Pages.AddArtifact(batesArtifact);
```

Behind the scenes, Aspose adds the artifact to the page dictionary of every page, which means the numbering becomes part of the PDF’s logical structure—perfect for later extraction or search.

## Step 5: Save the Updated PDF

Finally, write the changes back to disk. You can overwrite the original or save to a new file; the latter is safer during development.

```csharp
// Step 5: Save the PDF with Bates numbers
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

When you open `output.pdf` in a viewer, you’ll see “INV‑1000”, “INV‑1001”, … at the bottom‑right of each page.

### Verifying the Result

Open the PDF in Adobe Acrobat or any viewer and look for the numbers. If you need to confirm programmatically, you can read back the artifact:

```csharp
foreach (var page in pdfDocument.Pages)
{
    foreach (var artifact in page.Artifacts)
    {
        Console.WriteLine($"Page {page.Number}: {artifact.Text}");
    }
}
```

That snippet prints each page’s Bates label—handy for automated tests.

## Edge Cases & Common Questions

### What if My PDF Already Has a Footer?

Adding an artifact won’t overwrite existing footers because artifacts sit in a separate layer. However, if the visual overlap is a concern, tweak the `Y` coordinate or increase the `X` offset to move the Bates number out of the way.

### Can I Use a Different Font or Color?

Absolutely. The `BatesNumberingArtifact` inherits from `Artifact`, so you can set `Font`, `FontColor`, and even `Opacity`. Example:

```csharp
batesArtifact.Font = FontRepository.FindFont("Arial");
batesArtifact.FontColor = Color.FromArgb(255, 0, 0); // Red
```

### How Do I Reset the Counter for a New Document?

Just change `Start` before calling `AddArtifact`. If you generate many PDFs in a loop, keep a running counter in your application logic.

### Is This Approach Compatible with Encrypted PDFs?

Aspose.Pdf can open encrypted PDFs if you supply the password:

```csharp
var loadOptions = new LoadOptions { Password = "mySecret" };
using var pdfDocument = new Document("encrypted.pdf", loadOptions);
```

After decryption, the same artifact‑adding steps work flawlessly.

## Full Working Example

Below is the complete, ready‑to‑run program. Paste it into a console app, adjust the paths, and hit **F5**.

```csharp
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Create the Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "INV-",
            Start = 1000,
            Format = "0000",
            X = 500,
            Y = 20,
            FontSize = 10,
            FontColor = Color.Black
        };

        // Apply the artifact to every page
        pdfDocument.Pages.AddArtifact(batesArtifact);

        // Save the result
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Expected output:** The console prints “Bates numbering added successfully!” and `output.pdf` contains sequential labels like `INV‑1000`, `INV‑1001`, etc., positioned at the bottom‑right of each page.

## Quick Recap

- **Primary goal:** **add bates numbering pdf** using Aspose.Pdf.  
- We covered **how to add bates**, **add sequential page numbers**, and **add custom footer pdf** elements through a single artifact.  
- The tutorial showed how to **add artifact to pdf**, handle edge cases, and verify the result.  

## What’s Next?

- **Dynamic prefixes:** Pull values from a database to generate “CASE‑2023‑001”, “CASE‑2023‑002”, …  
- **Conditional placement:** Use page size detection (`page.MediaBox`) to center numbers on landscape pages.  
- **Combine with watermarks:** Add a semi‑transparent logo alongside the Bates number for branding.  

Feel free to experiment—maybe you’ll discover a smarter way to batch‑process thousands of files. If you run into trouble, drop a comment or check Aspose’s official docs (they’re surprisingly clear). Happy coding!  

![add bates numbering pdf example](https://example.com/bates-numbering-screenshot.png "Screenshot showing add bates numbering pdf in a PDF viewer")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}