---
category: general
date: 2026-02-14
description: Add Bates numbering PDF to your documents effortlessly. Learn how to
  add footer page numbers and add sequential numbers PDF with Aspose.Pdf in minutes.
draft: false
keywords:
- add bates numbering pdf
- add footer page numbers
- how to add bates numbers
- add sequential numbers pdf
language: en
og_description: Add Bates numbering PDF quickly. This guide shows how to add footer
  page numbers and sequential numbers PDF using Aspose.Pdf, with full code and tips.
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

Ever needed to **add Bates numbering PDF** files but weren’t sure where to start? You're not alone. Legal teams, auditors, and any folks handling large document sets constantly ask, “How do I add Bates numbers without breaking the layout?” The good news is that with Aspose.Pdf for .NET you can inject those numbers as a simple footer—no manual editing required.

In this tutorial we’ll walk through a practical, end‑to‑end solution that not only **adds footer page numbers** but also lets you **add sequential numbers PDF** files with a custom prefix, font size, and alignment. By the end you’ll have a ready‑to‑run C# program, a clear understanding of why each setting matters, and a few pro tips to avoid the most common pitfalls.

## What You’ll Learn

- How to load an existing PDF and prepare it for Bates numbering.  
- Which **BatesNumberingOptions** properties control appearance and placement.  
- How to apply numbering to every page in one call.  
- Ways to customize the prefix, start number, and margins for different legal formats.  
- Edge‑case handling—what to do with encrypted PDFs or documents that already contain footers.

**Prerequisites**: .NET 6+ (or .NET Framework 4.7+), a recent version of Aspose.Pdf (the example uses 23.10), and an input PDF you own the rights to modify. No other third‑party libraries are needed.

---

## Step 1 – Load the PDF You Want to Number

The first thing we do is create a `Document` instance that points to the source file. Using the `using var` pattern ensures the file handle is released automatically.

```csharp
using Aspose.Pdf;

// Replace with the path to your source PDF
using var doc = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Why this matters:** Aspose.Pdf reads the entire PDF structure into memory, allowing us to manipulate pages, annotations, and metadata without touching the original file on disk. If the PDF is password‑protected, you can pass the password to the constructor—see the “Encrypted PDFs” note at the end.

---

## Step 2 – Define Your Bates Numbering Options

Bates numbers are essentially page footers with a configurable prefix and a sequential counter. The `BatesNumberingOptions` class lets you fine‑tune every visual aspect.

```csharp
var batesOptions = new BatesNumberingOptions
{
    // The text that will appear before the numeric part
    Prefix = "ABC-",

    // Starting number; the library will increment this automatically
    StartNumber = 1000,

    // Font size of the footer text (points)
    FontSize = 12,

    // Align the number to the right side of the page
    HorizontalAlignment = HorizontalAlignment.Right,

    // Place the number at the bottom of the page
    VerticalAlignment = VerticalAlignment.Bottom,

    // Margins: left, top, right, bottom (in points)
    Margin = new MarginInfo(0, 20, 0, 0)
};
```

### Quick tip

- **Prefix**: Use a short, unique identifier (e.g., case number) to keep the footer readable.  
- **StartNumber**: Legal firms often start at `1` or a custom offset; pick whatever matches your filing system.  
- **Margins**: The bottom margin of `20` points keeps the text clear of footnotes or signatures that might already sit near the page edge.

---

## Step 3 – Apply the Numbering to All Pages

With the options configured, the actual injection is a one‑liner. Aspose.Pdf handles pagination, updates existing content streams, and respects the page rotation automatically.

```csharp
doc.Pages.AddBatesNumbering(batesOptions);
```

> **What’s happening under the hood?** The library iterates over each `Page` object, creates a `TextFragment` that incorporates the prefix and current counter, then draws it using the page’s coordinate system. Because we set `HorizontalAlignment.Right` and `VerticalAlignment.Bottom`, the text snaps to the lower‑right corner regardless of page size.

---

## Step 4 – Save the Modified PDF

Finally, write the result to a new file. Overwriting the original is possible, but keeping a copy helps with version control.

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

If you need to preserve the original metadata (author, creation date), Aspose.Pdf copies it by default. You can also specify a `SaveOptions` object for PDF/A compliance or compression.

---

## Full Working Example

Below is the complete, ready‑to‑run program. Paste it into a console app project, adjust the file paths, and hit **F5**.

```csharp
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using var doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Configure Bates numbering options
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC-",
            StartNumber = 1000,
            FontSize = 12,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(0, 20, 0, 0)
        };

        // 3️⃣ Apply numbering to every page
        doc.Pages.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the output PDF
        doc.Save("YOUR_DIRECTORY/output.pdf");

        System.Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Expected result:** Each page of `output.pdf` now displays a footer like `ABC-1000`, `ABC-1001`, … anchored to the lower‑right corner. Open the file in any PDF reader to verify.

---

## Handling Common Variations

### Adding Footer Page Numbers Only

If you only need simple page numbers without a prefix, set `Prefix = ""` and perhaps adjust the margin to avoid colliding with existing footers.

```csharp
batesOptions.Prefix = "";
batesOptions.StartNumber = 1; // classic page numbering
```

### Using a Different Alignment

Legal documents sometimes require the number centered at the bottom. Switch the alignment:

```csharp
batesOptions.HorizontalAlignment = HorizontalAlignment.Center;
```

### Dealing with Encrypted PDFs

When the source PDF is password‑protected, supply the password like this:

```csharp
using var doc = new Document("secure.pdf", new LoadOptions { Password = "mySecret" });
```

The rest of the workflow stays identical.

### Skipping Existing Footers

If a document already contains a footer that you don’t want to overwrite, you can prepend a custom string that makes the new number distinct, or you could iterate pages manually and add a `TextFragment` only where the footer is absent. The library’s `Page` class exposes `Annotations` and `Contents` collections for fine‑grained control.

---

## Pro Tips & Pitfalls

- **Avoid clipping**: Very small bottom margins can cause the text to be cut off on printers. Test with a physical print if you’ll be distributing hard copies.  
- **Performance**: Adding Bates numbers to a 500‑page PDF takes under a second on a modern laptop, but large batches benefit from parallel processing—just remember that `Document` isn’t thread‑safe, so each thread needs its own instance.  
- **Version compatibility**: The code works with Aspose.Pdf 23.10 and newer. If you’re on an older version, the property names are the same but the `MarginInfo` constructor might require `float` arguments.  
- **Legal compliance**: Some jurisdictions require the Bates number to be placed in a specific location (e.g., bottom‑left). Adjust the `HorizontalAlignment` accordingly.  

---

## Conclusion

We’ve just demonstrated how to **add Bates numbering PDF** files using Aspose.Pdf for .NET, covering everything from loading the document to saving the final version with a clean footer. By tweaking a handful of properties you can also **add footer page numbers**, **add sequential numbers PDF**, or customize the appearance to meet any legal standard.

Ready for the next step? Try combining this technique with OCR text extraction to embed searchable keywords alongside your Bates numbers, or automate the process for entire folders using `Directory.GetFiles`. The possibilities are endless, and the foundation you now have will make those extensions painless.

Happy coding, and may your PDFs always be perfectly numbered!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}