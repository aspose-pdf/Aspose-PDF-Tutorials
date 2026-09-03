---
category: general
date: 2026-02-20
description: Add Bates Numbering to your documents and convert DOCX to PDF with custom
  page numbers in C#. Learn how to add sequential page numbers and save document as
  PDF.
draft: false
keywords:
- add bates numbering
- convert docx to pdf
- add custom page numbers
- save document as pdf
- add sequential page numbers
language: en
og_description: Add Bates Numbering to your DOCX files and convert them to PDF with
  custom page numbers using C#. This guide walks you through every step.
og_title: Add Bates Numbering to DOCX and Convert to PDF – C# Tutorial
tags:
- C#
- PDF
- Document Automation
title: Add Bates Numbering to DOCX and Convert to PDF – Complete C# Guide
url: /net/document-conversion/add-bates-numbering-to-docx-and-convert-to-pdf-complete-c-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Bates Numbering to DOCX and Convert to PDF – Complete C# Guide

Ever needed to **add bates numbering** to a legal brief but weren’t sure how to automate it? You’re not the only one. In many firms the manual process of stamping each page is a real time‑suck, and the risk of a missed number can be costly.  

The good news? With a few lines of C# you can **add bates numbering**, **convert docx to pdf**, and **save document as pdf** in one smooth flow. Below you’ll find a self‑contained solution that works today, plus the “why” behind each choice so you can tweak it for your own workflow.

---

## What This Tutorial Covers

In the next sections we’ll:

1. Load a DOCX file from disk.  
2. Define **custom page numbers** (prefix, start value, and optional formatting).  
3. Apply **add bates numbering** to every page of the source.  
4. **Convert docx to pdf** while preserving the numbering.  
5. **Save document as pdf** to a location of your choosing.  

No external services, no hidden settings—just plain C# and a popular document‑processing library (e.g., GroupDocs.Conversion). By the end you’ll have a ready‑to‑run console app that produces a PDF with sequential page numbers exactly where you need them.

---

## Prerequisites

- **.NET 6.0** or later (the code compiles on .NET Framework 4.7+ as well).  
- The **GroupDocs.Conversion** NuGet package (or any library that exposes `Document`, `BatesNumberingOptions`, and `Pages.AddBatesNumbering`). Install with:  

```bash
dotnet add package GroupDocs.Conversion
```

- A DOCX file you want to process (place it in `YOUR_DIRECTORY/input.docx`).  
- Basic familiarity with C# console projects.

---

## Step‑by‑Step Implementation

### ## Add Bates Numbering – Preparing the Project

First, create a new console project and pull in the required namespaces:

```csharp
using System;
using GroupDocs.Conversion;               // Core document handling
using GroupDocs.Conversion.Options;       // Options like BatesNumberingOptions
using GroupDocs.Conversion.Options.Pdf;   // PDF‑specific options (if needed)

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill the body in the next steps
        }
    }
}
```

> **Why this matters:** Importing the correct namespaces gives you access to the `Document` class (the entry point) and the **BatesNumberingOptions** object that controls the numbering format. Skipping this step throws a compile‑time error, which is why we start here.

### ## Load the Source DOCX File

Now we read the Word file. The `Document` constructor takes a path, so keep your paths absolute or relative to the executable.

```csharp
// Step 1: Load the source document
string inputPath = @"YOUR_DIRECTORY/input.docx";
Document document = new Document(inputPath);
```

> **Pro tip:** If the file might be missing, wrap this in a `try/catch` and show a friendly message. It prevents the whole app from crashing and improves the user experience.

### ## Define Custom Page Numbers (Bates Options)

Here’s where we set up **add custom page numbers**. You can change the `Prefix`, `Start`, and even the number format (e.g., leading zeros).

```csharp
// Step 2: Define Bates numbering options (prefix and starting number)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC",      // Anything you need – legal firms love prefixes
    Start = 1000,        // First number in the sequence
    // Optional: NumberFormat = "0000" // forces four‑digit padding
};
```

> **Why you need a prefix:** In many jurisdictions the prefix identifies the case file or client. The library will prepend it to every page number automatically.

### ## Apply Bates Numbering to Every Page

With the options ready, we tell the document to stamp each page:

```csharp
// Step 3: Apply Bates numbering to every page in the document
document.Pages.AddBatesNumbering(batesOptions);
```

> **Edge case:** If your DOCX already contains footers, the library will overlay the numbers by default. Some libraries let you specify the placement (top‑right, bottom‑center, etc.) via additional properties on `BatesNumberingOptions`.

### ## Convert to PDF and Save

Finally, we output a PDF that contains the newly added numbers. The `Save` method automatically infers the format from the file extension.

```csharp
// Step 4: Save the document with the new Bates numbers as PDF
string outputPath = @"YOUR_DIRECTORY/output.pdf";
document.Save(outputPath);
Console.WriteLine($"✅ PDF saved with Bates numbering at: {outputPath}");
```

> **Why we save as PDF:** PDFs preserve layout, fonts, and the exact positioning of the numbers, making them ideal for legal filings and archival.

---

## Full Working Example

Putting it all together, here’s the complete program you can copy‑paste into `Program.cs` and run:

```csharp
using System;
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source DOCX
            string inputPath = @"YOUR_DIRECTORY/input.docx";
            Document document = new Document(inputPath);

            // 2️⃣ Set up Bates numbering (custom prefix & start)
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC",
                Start = 1000
                // NumberFormat = "0000" // Uncomment for zero‑padded numbers
            };

            // 3️⃣ Apply the numbering to every page
            document.Pages.AddBatesNumbering(batesOptions);

            // 4️⃣ Convert and save as PDF
            string outputPath = @"YOUR_DIRECTORY/output.pdf";
            document.Save(outputPath);

            Console.WriteLine($"✅ Done! PDF with Bates numbers saved to {outputPath}");
        }
    }
}
```

### Expected Result

Open `output.pdf` in any viewer. You’ll see each page numbered like **ABC‑1000**, **ABC‑1001**, … continuing to the last page. The numbers appear in the default location (bottom‑right) unless you altered the options.

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| **Can I change the placement of the numbers?** | Yes. Most libraries expose `Position` or `Margin` properties on `BatesNumberingOptions`. Set `batesOptions.Position = BatesNumberingPosition.BottomLeft;` for a different corner. |
| **What if the DOCX has existing footers?** | The library usually overwrites the area where it draws the number. If you need to keep existing footers, look for an `OverwriteExisting` flag or add the numbers manually via a custom footer template. |
| **Do I need to worry about Unicode characters?** | The prefix can contain any Unicode text, but make sure the font used in the PDF supports those characters; otherwise they’ll appear as squares. |
| **How do I add leading zeros?** | Set `NumberFormat = "0000"` (or any pattern) in `BatesNumberingOptions`. This forces numbers like 0010, 0011, etc. |
| **Can I batch‑process many DOCX files?** | Absolutely. Wrap the logic in a `foreach (var file in Directory.GetFiles(..., "*.docx"))` loop and reuse the same `batesOptions` object or vary it per file. |

---

## Pro Tips & Best Practices

- **Performance:** If you’re processing hundreds of files, reuse a single `Document` instance where possible and call `document.Dispose()` after each save to free unmanaged resources.  
- **Version control:** Keep the `Prefix` and `Start` values in a config file (`appsettings.json`). That way you can change them without recompiling.  
- **Testing:** Run the program against a 1‑page DOCX first. Verify the number appears where you expect before scaling up to massive contracts.  
- **Compliance:** Some jurisdictions require the Bates number to be at least 8 characters long. Adjust `Prefix` and `NumberFormat` accordingly.  

---

## Next Steps – Expand Your Automation

Now that you’ve mastered **add bates numbering**, consider these related enhancements:

- **Convert docx to pdf** while preserving hyperlinks and bookmarks.  
- **Add custom page numbers** to existing PDFs using a PDF‑specific library (e.g., iTextSharp).  
- **Save document as pdf** with different quality settings for web vs. print.  
- **Add sequential page numbers** to scanned images by OCR‑processing each page first.  

Each of these topics builds on the same core concepts—loading a document, configuring options, and saving the result—so you’ll feel right at home.

---

## Conclusion

We’ve walked through a complete, end‑to‑end solution for **add bates numbering** to a DOCX file, **convert docx to pdf**, and **save document as pdf** with custom, sequential page numbers. The code is short, the dependencies are minimal, and the approach is flexible enough for both small law‑firm projects and large‑scale enterprise pipelines.

Give it a spin, tweak the prefix, experiment with number formats, and you’ll have a robust tool in your developer toolbox. If you run into quirks or have ideas for further automation, drop a comment below—happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}