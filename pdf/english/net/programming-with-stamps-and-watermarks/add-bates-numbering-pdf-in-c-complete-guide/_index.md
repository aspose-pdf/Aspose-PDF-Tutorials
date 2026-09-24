---
category: general
date: 2026-03-14
description: Add Bates Numbering PDF using Aspose.Pdf in C#. Learn how to add bates
  and add sequential page numbers automatically for legal or archival documents.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- Aspose PDF Bates artifact
- C# PDF automation
language: en
og_description: Add Bates Numbering PDF step‑by‑step. This tutorial shows how to add
  bates and add sequential page numbers using Aspose.Pdf for .NET.
og_title: Add Bates Numbering PDF in C# – Complete Guide
tags:
- Aspose.Pdf
- C#
- PDF
- Bates numbering
title: Add Bates Numbering PDF in C# – Complete Guide
url: /net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Bates Numbering PDF – Full Walkthrough

Ever needed to **add bates numbering pdf** to a massive legal bundle but weren’t sure where to start? Adding Bates numbers is a routine, yet surprisingly fiddly, part of document‑review workflows. The good news? With Aspose.Pdf for .NET you can automate the whole thing in a handful of lines.

In this guide we’ll walk through **how to add bates** to every page of a PDF, discuss the **add sequential page numbers** options, and show you a ready‑to‑run code sample. By the end you’ll have a self‑contained solution that you can drop into any C# project—no extra scripts, no manual stamping.

## What You’ll Need

- **Aspose.Pdf for .NET** (version 23.10 or newer). The library is commercial, but a free evaluation works just fine for testing.
- A .NET development environment (Visual Studio, Rider, or the `dotnet` CLI).
- An input PDF (`input.pdf`) you want to tag.
- A little patience for the occasional edge‑case (we’ll cover those).

If you already have those, great—let’s jump in.

![Add Bates Numbering PDF example](/images/bates-numbering-example.png "Screenshot showing a PDF with add bates numbering pdf applied")

## Step 1: Set Up the Project and Install Aspose.Pdf

To keep things tidy, start a fresh console app:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

The `dotnet add package` command pulls the latest Aspose.Pdf assembly from NuGet, so you’re ready to code.

### Why a console app?

A console app is lightweight, runs anywhere, and lets you focus on the PDF logic without UI distractions. Of course, you can later migrate the code into a web API or a background service—nothing in the core logic ties you to the console.

## Step 2: Load the Source PDF

Opening the document is straightforward. We’ll use a `using` block so the file handle is released automatically.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing;   // Required for Color

class Program
{
    static void Main()
    {
        // Adjust these paths to match your environment
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string outputPdfPath = @"C:\Docs\output.pdf";

        // Load the PDF – this is where the “add bates numbering pdf” process begins
        using (var pdfDocument = new Document(sourcePdfPath))
        {
            // Next steps go here...
        }
    }
}
```

**What’s happening?** The `Document` class represents the entire PDF file. By wrapping it in `using`, we guarantee that `Dispose` runs, flushing any pending changes to disk.

## Step 3: Define a Bates Number Artifact (The “how to add bates” Core)

Aspose.Pdf treats Bates numbers as *artifacts*—metadata that can be rendered on‑screen or printed, but doesn’t become a permanent content stream unless you flatten the PDF. Here’s the object we’ll attach to each page:

```csharp
var batesArtifact = new BatesNumberArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    Increment = 1,
    X = 36,               // 0.5 inch from the left edge (points)
    Y = 36,               // 0.5 inch from the bottom edge (points)
    FontSize = 9,
    FontColor = Color.Black
};
```

### Why use an artifact?

- **Performance:** The number is rendered on‑the‑fly, so you can change the prefix or start number without rewriting the whole PDF.
- **Flexibility:** You can later flatten the PDF if you need a “hard‑coded” stamp for legal submission.
- **Precision:** Positioning uses points (1/72 inch), giving you pixel‑perfect control.

If you need a different prefix or a larger font, just tweak the properties. The `Increment` field determines how the number steps from page to page—perfect for the **add sequential page numbers** requirement.

## Step 4: Attach the Artifact to Every Page

Now we loop through the `Pages` collection and add the artifact. This is the actual “add bates numbering pdf” action.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

### Edge‑Case Note

If your PDF already contains Bates artifacts, you might end up with duplicates. A quick guard can prevent that:

```csharp
foreach (Page page in pdfDocument.Pages)
{
    bool alreadyHasBates = page.Artifacts.Any(a => a is BatesNumberArtifact);
    if (!alreadyHasBates)
        page.Artifacts.Add(batesArtifact);
}
```

That tiny check saves you from a messy double‑stamp situation, especially when processing batches of documents that have been pre‑tagged.

## Step 5: Save the Updated PDF

Finally, write the file back to disk. You can either overwrite the original or create a new file—here we’ll produce a fresh copy:

```csharp
pdfDocument.Save(outputPdfPath);
Console.WriteLine($"Bates numbers added successfully. Output saved to {outputPdfPath}");
```

When you open `output.pdf` in any viewer, you’ll see “CASE‑1000”, “CASE‑1001”, etc., at the lower‑left corner of each page.

### Optional: Flatten the PDF

If the recipient requires a non‑editable PDF (common in court filings), flatten the pages:

```csharp
pdfDocument.FlattenAllPages();   // Turns artifacts into permanent content
pdfDocument.Save(outputPdfPath);
```

Flattening is a one‑time operation; after it, the Bates numbers become part of the page content stream and can’t be altered without re‑processing.

## Full Working Example

Below is the complete program you can copy‑paste into `Program.cs`. It includes the optional flatten step commented out for easy toggling.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System;
using System.Drawing;
using System.Linq;

class Program
{
    static void Main()
    {
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string outputPdfPath = @"C:\Docs\output.pdf";

        using (var pdfDocument = new Document(sourcePdfPath))
        {
            var batesArtifact = new BatesNumberArtifact
            {
                Prefix = "CASE-",
                StartNumber = 1000,
                Increment = 1,
                X = 36,
                Y = 36,
                FontSize = 9,
                FontColor = Color.Black
            };

            foreach (Page page in pdfDocument.Pages)
            {
                // Prevent duplicate artifacts if the PDF was processed before
                bool alreadyHasBates = page.Artifacts.Any(a => a is BatesNumberArtifact);
                if (!alreadyHasBates)
                    page.Artifacts.Add(batesArtifact);
            }

            // Uncomment the next line if you need a flattened PDF for legal submission
            // pdfDocument.FlattenAllPages();

            pdfDocument.Save(outputPdfPath);
        }

        Console.WriteLine($"Bates numbers added successfully. Output saved to {outputPdfPath}");
    }
}
```

Run it with `dotnet run` and watch the console confirm the operation.

## Common Questions & Pro Tips

| Question | Answer |
|----------|--------|
| **Can I change the position per page?** | Yes. Instead of a single `batesArtifact`, create a new one inside the loop and set `X`/`Y` based on page size. |
| **What if the PDF is password‑protected?** | Load it with `new Document(sourcePdfPath, new LoadOptions { Password = "mySecret" })`. The rest of the workflow stays unchanged. |
| **Do I need to worry about performance on huge files?** | Adding artifacts is O(N) where N = page count, and memory usage stays low because Aspose streams pages. For PDFs >10 000 pages, consider processing in batches to avoid long GC pauses. |
| **Is the numbering resettable per section?** | Absolutely. Set `StartNumber` to a new value before you hit the first page of the next section, or create a second `BatesNumberArtifact` with a different `Prefix`. |
| **Will this work on .NET Core?** | Yes. Aspose.Pdf supports .NET Framework, .NET Core, and .NET 5/6+. Just target the appropriate runtime in your csproj. |

### Pro tip

When you’re dealing with **add sequential page numbers** for a multi‑volume set, store the last used number in a small JSON file. Read it before you start, increment accordingly, then write it back. This tiny persistence layer prevents accidental number reuse across runs.

## Verifying the Result

Open `output.pdf` in Adobe Reader, Foxit, or even Chrome. You should see something like:

```
CASE-1000   (Page 1)
CASE-1001   (Page 2)
…
CASE-1015   (Page 16)
```

If you flattened the PDF, the numbers become part of the page graphics—right‑click → “Inspect” will show them as ordinary text objects.

## Conclusion

We’ve just covered how to **add bates numbering pdf** using Aspose.Pdf, explored the **how to add bates** mechanics, and demonstrated a clean way to **add sequential page numbers** across an entire document. The snippet is production‑ready, handles duplicate artifacts, and even offers an optional flatten step for legal compliance.

Next, you might want to explore:

- Merging multiple PDFs while preserving Bates continuity (use `Document.AppendDocument` and adjust `StartNumber` on the fly).
- Adding a QR code alongside the Bates number for automated tracking.
- Integrating this logic into an ASP.NET Core API so your web service can tag PDFs on demand.

Give it a spin, tweak the prefix, play with fonts, and let the automation take the grunt work out of your document‑review pipeline. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}