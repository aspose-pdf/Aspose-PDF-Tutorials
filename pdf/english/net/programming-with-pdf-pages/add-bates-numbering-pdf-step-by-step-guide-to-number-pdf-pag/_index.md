---
category: general
date: 2026-03-03
description: Add Bates numbering PDF quickly and learn how to number PDF pages or
  add sequential PDF numbers using Aspose.Pdf in C#.
draft: false
keywords:
- add bates numbering pdf
- number pdf pages
- add sequential pdf numbers
- pdf bates numbering tutorial
- aspnet pdf automation
language: en
og_description: Add Bates numbering PDF in C# to number PDF pages and add sequential
  PDF numbers. Full code, explanations, and best practices.
og_title: Add Bates Numbering PDF – Complete C# Tutorial
tags:
- PDF
- C#
- Aspose.Pdf
- Document Automation
title: Add Bates Numbering PDF – Step‑by‑Step Guide to Number PDF Pages
url: /net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Bates Numbering PDF – Complete C# Tutorial

Ever needed to **add bates numbering pdf** files but weren’t sure where to start? You’re not the only one—legal teams, auditors, and archivists all wrestle with the same problem. The good news? With a few lines of C# and the Aspose.Pdf library you can **number pdf pages** automatically, and you’ll even get the flexibility to **add sequential pdf numbers** with custom prefixes, suffixes, and placement.

In this guide we’ll walk through a real‑world example, explain why each setting matters, and show you how to tweak the code for edge cases like different page sizes or custom digit counts. By the end you’ll have a ready‑to‑run snippet that adds Bates numbers to any PDF you throw at it, and you’ll understand the “why” behind every option.

## Prerequisites

Before we dive in, make sure you have:

- .NET 6.0 or later (the code works with .NET Framework 4.6+ as well)
- A valid Aspose.Pdf for .NET license (or a free evaluation key)
- Visual Studio 2022 (or any C# editor you prefer)
- A source PDF named `source.pdf` in a folder you can reference

That’s it—no extra NuGet packages beyond Aspose.Pdf.

## Step 1 – Open the Source PDF Document

The first thing you need to do is load the PDF you want to stamp. Using a `using` block guarantees the file handle is released correctly, which prevents locking issues later on.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the original PDF
using (var pdfDocument = new Document(@"C:\MyDocs\source.pdf"))
{
    // The rest of the steps will go inside this block.
}
```

> **Why this matters:** Opening the document inside a `using` statement ensures deterministic disposal. If you skip it, the file may stay locked, and subsequent attempts to save or delete the PDF will fail—something I’ve seen cause headaches in production pipelines.

## Step 2 – Configure Bates Numbering Options

Now we tell Aspose how we want the Bates numbers to look. Every property maps directly to a visual element on the page.

```csharp
// Step 2: Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    Prefix = "2025-",               // Text before the number
    Suffix = "-A",                  // Text after the number
    Start = 5000,                   // First number in the sequence
    NumberOfDigits = 5,             // Pads with leading zeros (e.g., 05000)
    Placement = BatesNumberPlacement.BottomRight // Where the number appears
};
```

### Quick tips for the options

| Property | What it does | When to change it |
|----------|--------------|-------------------|
| **Prefix / Suffix** | Adds static text before/after the numeric part. | Use a case ID, project code, or “CONF‑” for confidential docs. |
| **Start** | The first number in the series. | If you’re continuing a numbering scheme from a previous batch, set this accordingly. |
| **NumberOfDigits** | Controls zero‑padding. | For legal filings you often need exactly 6 digits; set to `6`. |
| **Placement** | BottomRight, BottomLeft, TopRight, TopLeft, Center. | Choose based on your document layout; BottomRight is the most common for Bates numbers. |

> **Pro tip:** If you need to **number pdf pages** in multiple columns, you can call `pdfDocument.AddBatesNumbering` twice with different `Placement` values and distinct `Prefix` strings.

## Step 3 – Apply the Bates Numbering to the Document

With the options ready, the actual stamping is a single method call. Aspose handles pagination, rotation, and margin calculations internally.

```csharp
// Step 3: Apply the numbering to every page
pdfDocument.AddBatesNumbering(batesOptions);
```

> **Why a single call works:** Under the hood Aspose iterates over `pdfDocument.Pages`, creates a `TextFragment` for each page, and positions it based on the `Placement` you chose. This abstraction saves you from writing a manual loop and dealing with coordinate transforms.

## Step 4 – Save the Updated PDF

Finally, write the modified file to disk. You can overwrite the original or create a new file; the example below creates a fresh copy.

```csharp
// Step 4: Persist the changes
pdfDocument.Save(@"C:\MyDocs\bates_numbered.pdf");
```

If you need to **add sequential pdf numbers** to a stream (e.g., when sending the file over an API), replace the file path with a `MemoryStream`:

```csharp
using var output = new MemoryStream();
pdfDocument.Save(output);
output.Position = 0; // Reset for downstream consumption
```

## Full Working Example

Putting it all together, here’s the complete, ready‑to‑run program:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Open the source PDF
        using (var pdfDocument = new Document(@"C:\MyDocs\source.pdf"))
        {
            // Configure Bates numbering
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "2025-",
                Suffix = "-A",
                Start = 5000,
                NumberOfDigits = 5,
                Placement = BatesNumberPlacement.BottomRight
            };

            // Apply the numbering
            pdfDocument.AddBatesNumbering(batesOptions);

            // Save the result
            pdfDocument.Save(@"C:\MyDocs\bates_numbered.pdf");
        }

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

### Expected Output

- A new file `bates_numbered.pdf` appears in `C:\MyDocs`.
- Each page shows something like `2025-05000-A`, `2025-05001-A`, … in the bottom‑right corner.
- The numbers are zero‑padded to five digits, matching the `NumberOfDigits` setting.

## Handling Common Variations

### 1. Different Page Sizes

If your PDF mixes portrait and landscape pages, you may notice the number being clipped on the wider side. To fix this, enable the `AutoFit` property:

```csharp
batesOptions.AutoFit = true; // Adjusts font size to fit within page margins
```

### 2. Custom Font or Color

Bates numbers default to black, 12‑pt Times New Roman. Change the appearance by accessing the `TextState`:

```csharp
batesOptions.TextState = new TextState
{
    FontSize = 10,
    Font = FontRepository.FindFont("Courier New"),
    ForegroundColor = Color.GetBlue()
};
```

### 3. Skipping Pages

Suppose you want to **number pdf pages** but skip the title page. Use a page range:

```csharp
pdfDocument.AddBatesNumbering(batesOptions, new PageNumbering { Start = 2 });
```

### 4. Adding Multiple Numbering Schemes

Legal teams sometimes require both a Bates number and a confidential watermark. Run two separate `AddBatesNumbering` calls with different `Placement` values:

```csharp
// First scheme – bottom right
pdfDocument.AddBatesNumbering(batesOptions);

// Second scheme – top left, different prefix
var confidentialOptions = new BatesNumberingOptions
{
    Prefix = "CONF-",
    Start = 1,
    NumberOfDigits = 4,
    Placement = BatesNumberPlacement.TopLeft,
    TextState = new TextState { FontSize = 8, ForegroundColor = Color.GetRed() }
};
pdfDocument.AddBatesNumbering(confidentialOptions);
```

## Frequently Asked Questions

**Q: Does this work with PDFs that already have existing text?**  
A: Yes. Aspose adds the Bates number as a separate layer, so existing content stays untouched. If you need the numbers to appear *behind* existing text (rare), you’d have to manipulate the page’s content streams manually.

**Q: What if the PDF is password‑protected?**  
A: Load it with the password first: `new Document(path, new LoadOptions { Password = "secret" })`. After stamping, you can re‑apply encryption via `pdfDocument.Encrypt(...)`.

**Q: Can I use this in a .NET Core console app?**  
A: Absolutely. The same code works in .NET Core, .NET 5+, and .NET Framework. Just reference the appropriate Aspose.Pdf NuGet package.

## Conclusion

We’ve just covered how to **add bates numbering pdf** files, how to **number pdf pages**, and how to **add sequential pdf numbers** with full control over formatting, placement, and edge‑case handling. The short snippet above does the heavy lifting, while the extra options let you adapt the solution to any legal, archival, or compliance workflow.

Ready for the next step? Try combining this approach with:

- **Batch processing** – loop over a folder of PDFs and apply the same numbering scheme.
- **Dynamic prefixes** – pull case IDs from a database and inject them per document.
- **PDF/A compliance** – after numbering, call `pdfDocument.Convert(..., PdfFormat.PdfA2b)` to ensure long‑term preservation.

Feel free to experiment, share your findings, or ask questions in the comments. Happy coding, and may your PDFs always stay perfectly indexed! 

![Screenshot of a PDF page with Bates numbers in the bottom‑right corner](https://example.com/images/bates-numbered.png "add bates numbering pdf example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}