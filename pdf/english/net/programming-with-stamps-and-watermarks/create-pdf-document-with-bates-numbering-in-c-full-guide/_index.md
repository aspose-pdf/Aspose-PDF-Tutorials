---
category: general
date: 2026-03-06
description: Create PDF document in C# and add bates number easily. Learn how to add
  blank page pdf, place stamp on page, and implement bates numbering.
draft: false
keywords:
- create pdf document
- add bates number
- add blank page pdf
- how to add bates numbering
- place stamp on page
language: en
og_description: Create PDF document in C# and add bates number. This guide shows how
  to add blank page pdf, place stamp on page, and apply bates numbering.
og_title: Create PDF Document with Bates Numbering – C# Tutorial
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Create PDF Document with Bates Numbering in C# – Full Guide
url: /net/programming-with-stamps-and-watermarks/create-pdf-document-with-bates-numbering-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create PDF Document with Bates Numbering in C#

Ever needed to **create PDF document** in C# and wondered how to add a Bates number without pulling your hair out? You're not the only one—law firms, courts, and even some corporate compliance teams face exactly this puzzle every day. The good news? With a few lines of Aspose.Pdf code you can spin up a brand‑new PDF, tack on a blank page, and stamp a proper Bates number in one smooth flow.

In this tutorial we’ll walk through the entire process: from setting up the project, to adding a blank page PDF, to figuring out **how to add bates numbering**, and finally to **place stamp on page** and save the result. By the end you’ll have a ready‑to‑use snippet you can drop into any .NET app. No vague references, just a complete, runnable example.

## What You’ll Need

- **.NET 6+** (or .NET Framework 4.6+ – Aspose.Pdf works with both)
- **Aspose.Pdf for .NET** NuGet package (`Install-Package Aspose.Pdf`)
- A decent IDE (Visual Studio, Rider, or VS Code with C# extension)

That’s it. No extra DLLs, no external services. Let’s dive in.

## Step 1: Create PDF Document – Initial Setup

First things first, we need a fresh `Document` object. Think of it as the empty canvas where everything else will live.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Initialize a new PDF document
Document pdfDocument = new Document();
```

> **Why this matters:** The `Document` class is the entry point for every Aspose operation. Instantiating it gives you access to the `Pages` collection, metadata, and security settings—all the building blocks for a professional PDF.

## Step 2: Add Blank Page PDF

A PDF without pages is like a book with no pages—pretty useless. Adding a blank page is straightforward, and it gives us a surface to stamp the Bates number onto.

```csharp
// Add a single blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **Pro tip:** If you need multiple pages, just call `pdfDocument.Pages.Add()` in a loop. Each call returns a fresh `Page` object you can customise independently.

## Step 3: How to Add Bates Numbering – Create the TextStamp

Now comes the heart of the matter: the **Bates number**. In Aspose.Pdf it’s just a `TextStamp` with a special artifact flag.

```csharp
// Create a text stamp that will serve as a Bates number
TextStamp batesStamp = new TextStamp("Bates-001")
{
    // Mark the stamp as a Bates‑numbering artifact (helps PDF viewers treat it specially)
    Artifact = ArtifactType.BatesNumbering,
    // Align the stamp to the bottom‑right corner of the page
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Add a small margin so the number isn’t glued to the edge
    Margin = new Margin { Bottom = 10, Right = 10 }
};
```

> **Why we set `Artifact`**: Some PDF readers expose Bates numbers as searchable metadata. Flagging the stamp as a `BatesNumbering` artifact ensures that downstream tools can recognise it automatically.

## Step 4: Place Stamp on Page

With the stamp ready, we now **place stamp on page**. This is the step where the visual number actually appears in the PDF.

```csharp
// Add the Bates number stamp to the previously created page
page.AddStamp(batesStamp);
```

> **Edge case:** If you need the number to increment on each page, you’d loop through `pdfDocument.Pages` and update `batesStamp.Value` before calling `AddStamp`. The example here keeps it simple with a static “Bates‑001”.

## Step 5: Save and Verify the Result

Finally, we persist the PDF to disk. Choose a folder you have write access to; otherwise, you’ll hit a `UnauthorizedAccessException`.

```csharp
// Save the stamped PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/BatesStamped.pdf");
```

When you open `BatesStamped.pdf` in any viewer you should see a tiny “Bates‑001” tucked neatly in the lower‑right corner of the blank page.

> **Expected output:**  
> ![PDF with Bates number stamp](image-placeholder.png "PDF with Bates number stamp")  
> *Alt text: PDF with Bates number stamp on the bottom‑right corner.*

If the number isn’t showing, double‑check the margin values and make sure the page size isn’t too small (default A4 works fine). Also confirm that the `Artifact` flag isn’t being stripped by any post‑processing tools.

## Full Working Example

Below is the complete, copy‑paste‑ready program. It includes all the `using` directives and comments to keep you oriented.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize a new PDF document
        Document pdfDocument = new Document();

        // 2️⃣ Add a blank page – this is where we’ll put the Bates number
        Page page = pdfDocument.Pages.Add();

        // 3️⃣ Create a TextStamp for the Bates number
        TextStamp batesStamp = new TextStamp("Bates-001")
        {
            Artifact = ArtifactType.BatesNumbering,          // Marks it as a Bates‑numbering artifact
            HorizontalAlignment = HorizontalAlignment.Right, // Align right
            VerticalAlignment = VerticalAlignment.Bottom,    // Align bottom
            Margin = new Margin { Bottom = 10, Right = 10 }  // Small margin from edges
        };

        // 4️⃣ Place the stamp on the page
        page.AddStamp(batesStamp);

        // 5️⃣ Save the PDF to disk
        string outputPath = @"C:\Temp\BatesStamped.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"PDF created successfully: {outputPath}");
    }
}
```

Run the program, pop open the PDF, and you’ll see the Bates number exactly where we told it to go. 🎉

## Common Variations & Gotchas

| Scenario | What to Change | Why |
|----------|----------------|-----|
| **Multiple pages, incrementing numbers** | Loop through `pdfDocument.Pages`, set `batesStamp.Value = $"Bates-{i:D3}"` before `AddStamp` | Gives each page a unique identifier, typical for legal bundles |
| **Different placement (top‑left)** | Change `HorizontalAlignment = HorizontalAlignment.Left` and `VerticalAlignment = VerticalAlignment.Top` | Some organizations prefer the number in the header instead of the footer |
| **Custom font or color** | Set `batesStamp.TextState.Font = FontRepository.FindFont("Arial"); batesStamp.TextState.FontSize = 12; batesStamp.TextState.ForegroundColor = Color.Red;` | Improves readability or meets branding guidelines |
| **Adding an existing PDF as a background** | Load the source PDF with `Document src = new Document("source.pdf"); pdfDocument.Pages.Add(src.Pages[1]);` | Useful when you need to stamp over a pre‑generated form |

## Wrapping Up

We’ve just shown how to **create PDF document**, **add blank page pdf**, and **add bates number** using Aspose.Pdf for .NET, then **place stamp on page** and save the file. The code is deliberately compact so you can adapt it to larger workflows—whether you’re batching dozens of files or integrating into a web service.

If you’re ready to take this further, consider:

- Automating the increment logic for large case files.
- Embedding the PDF generation into an ASP.NET Core API.
- Adding security (password protection) with `pdfDocument.Encrypt(...)`.

Feel free to experiment, break things, and ask questions in the comments. Happy coding, and may your PDFs always be perfectly stamped!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}