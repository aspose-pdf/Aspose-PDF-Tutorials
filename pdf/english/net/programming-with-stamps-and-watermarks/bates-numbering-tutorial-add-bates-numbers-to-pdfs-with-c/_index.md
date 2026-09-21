---
category: general
date: 2026-02-25
description: bates numbering tutorial – learn how to add page numbers pdf and apply
  custom Bates numbering using Aspose.Pdf in C#. Step‑by‑step guide with full code.
draft: false
keywords:
- bates numbering tutorial
- add page numbers pdf
- how to add bates
- add bates numbering
language: en
og_description: bates numbering tutorial shows you how to add page numbers pdf and
  custom Bates numbering in C#. Complete code, explanations, and tips.
og_title: bates numbering tutorial – Add Bates Numbers to PDFs with C#
tags:
- PDF
- C#
- Aspose.Pdf
title: 'bates numbering tutorial: Add Bates Numbers to PDFs with C#'
url: /net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-bates-numbers-to-pdfs-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# bates numbering tutorial – Adding Bates Numbers to PDFs in C#

Ever wondered how to add page numbers pdf while also embedding a legal‑style Bates number? You're not alone. In this **bates numbering tutorial** we’ll walk through everything you need to know to stamp every page of a PDF with a custom prefix, leading zeros, and precise positioning—using Aspose.Pdf for .NET.

The good news? It’s pretty straightforward once you grasp the core concepts. By the end of this guide you’ll have a runnable program that takes *input.pdf* and spits out *bates_out.pdf* with a neat “ABC‑01000” style label on each page. Let’s dive in.

## What You’ll Need

- **Aspose.Pdf for .NET** (version 23.10 or later). The library is commercial, but a free trial works just fine for learning.
- .NET 6+ SDK (any recent version will do).
- A basic C# development environment—Visual Studio, VS Code, or Rider.
- An input PDF to experiment with (any multi‑page document will illustrate the effect).

No extra NuGet packages beyond Aspose.Pdf are required, and the code runs on Windows, Linux, or macOS without modification.

## Step 1: Load the Source PDF Document (bates numbering tutorial – initialization)

First we create a `Document` object that represents the PDF we want to modify. Think of it as loading a blank canvas that you can draw on.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF – replace the path with your actual file location
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// Quick sanity check – make sure the document actually has pages
if (pdfDocument.Pages.Count == 0)
{
    throw new InvalidOperationException("The PDF you provided contains no pages.");
}
```

**Why this matters:** Without loading the file, there’s nothing to annotate. The sanity check prevents a silent failure later when you try to add artifacts to a non‑existent page collection.

## Step 2: Define the Bates Numbering Artifact (how to add bates)

A *BatesNumberingArtifact* tells Aspose where and how to draw the identifier. You can control the prefix, start number, zero padding, font size, and exact X/Y coordinates.

```csharp
// Configure the Bates numbering artifact
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
{
    Prefix = "ABC",          // Text that appears before the number
    Start = 1000,            // First number in the sequence
    LeadingZeros = 5,        // Pad the number with zeros (e.g., 01000)
    FontSize = 9,            // Small enough to sit in the margin
    Position = new Position   // Position measured from the lower‑left corner
    {
        X = 50,               // Horizontal offset (points)
        Y = 30                // Vertical offset (points)
    }
};
```

**Why this matters:** The `LeadingZeros` property ensures every label has the same length, which is crucial for legal documents where alignment matters. Adjust `X` and `Y` to move the stamp to the top‑right, bottom‑left, or wherever your workflow demands.

## Step 3: Attach the Artifact to Every Page (add page numbers pdf)

Now we loop through each page and attach the same artifact. This is where the *add page numbers pdf* requirement is fulfilled—each page gets its own sequential label automatically.

```csharp
// Iterate over each page and add the Bates artifact
foreach (Page page in pdfDocument.Pages)
{
    // The artifact is added to the page's Artifacts collection.
    // Aspose will handle the incrementing of the number for us.
    page.Artifacts.Add(batesArtifact);
}
```

**Why this matters:** By adding the artifact to the `Artifacts` collection rather than drawing text manually, we let Aspose manage the numbering logic, leading zeros, and rendering. This reduces bugs and keeps the code concise.

## Step 4: Save the Modified PDF (add bates numbering)

Finally, we persist the changes to a new file. It’s a good habit to write to a different filename so you keep the original untouched.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");

// Optional: let the user know we succeeded
Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
```

**Why this matters:** The `Save` method writes the entire PDF, embedding the artifacts as part of the page content stream. The resulting file can be opened in any PDF viewer and will display the Bates numbers exactly as specified.

## Full Working Example (All Steps Combined)

Below is the complete, ready‑to‑run program. Copy‑paste it into a console app project, replace the placeholder paths, and hit **F5**.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
            if (pdfDocument.Pages.Count == 0)
                throw new InvalidOperationException("The PDF you provided contains no pages.");

            // 2️⃣ Configure the Bates numbering artifact
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                Start = 1000,
                LeadingZeros = 5,
                FontSize = 9,
                Position = new Position { X = 50, Y = 30 }
            };

            // 3️⃣ Attach the artifact to every page
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesArtifact);
            }

            // 4️⃣ Save the modified PDF
            pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");
            Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
        }
    }
}
```

### Expected Result

Open *bates_out.pdf* in Adobe Reader, Foxit, or any viewer. You should see a label like **ABC‑01000** on the first page, **ABC‑01001** on the second, and so forth, positioned 50 pts from the left edge and 30 pts from the bottom. The numbers are right‑aligned because of the leading zeros, giving the document a clean, professional look.

## Common Variations & Edge Cases

| Scenario | How to Adjust |
|----------|---------------|
| **Different prefix** | Change `Prefix = "XYZ"` in the artifact definition. |
| **Start at a custom number** | Set `Start = 5000` (or any integer). |
| **Place the number in the top‑right corner** | Use `Position = new Position { X = pdfDocument.PageInfo.Width - 50, Y = pdfDocument.PageInfo.Height - 30 }`. |
| **Change font size for larger documents** | Modify `FontSize = 12` (or any size). |
| **Add a background rectangle** | Create a `RectangleArtifact` and add it before the `BatesNumberingArtifact`. |
| **Skip certain pages** | Inside the `foreach` loop, add an `if (page.Number % 2 == 0) continue;` to skip even pages. |

**Pro tip:** Always test with a short PDF first. It’s faster to verify positioning before you run the script on a 200‑page case file.

## Frequently Asked Questions

- **Does this work with encrypted PDFs?**  
  Aspose.Pdf can open password‑protected files if you provide the password via `Document(string, string)`. The Bates artifact will still be applied after decryption.

- **Can I add both Bates numbers and regular page numbers?**  
  Yes. Add a `PageNumberArtifact` alongside the `BatesNumberingArtifact`. Each artifact maintains its own counter.

- **What if my PDF has different page sizes?**  
  The `Position` values are absolute points. For mixed‑size documents, compute the position per page inside the loop using `page.PageInfo.Width` and `page.PageInfo.Height`.

## Next Steps & Related Topics

Now that you’ve mastered the **bates numbering tutorial**, you might want to explore:

- **Adding watermarks** – similar artifact approach with `TextArtifact`.
- **Merging multiple PDFs** – use `Document.AppendDocument`.
- **Extracting text for search indexing** – `TextAbsorber` class.
- **Automating batch processing** – loop over a folder of PDFs and apply the same artifact.

All of these topics build on the same concepts you just learned, so you’re well‑positioned to expand your PDF automation toolkit.

---

*Happy coding! If you hit any snags or have ideas for further customization, feel free to drop a comment below. The world of PDF manipulation is vast, but with a solid **bates numbering tutorial** under your belt, you’re already ahead of the curve.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}