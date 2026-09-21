---
category: general
date: 2026-03-03
description: Create PDF Document C# with Bates numbering – learn how to add bates,
  add sequential page numbers, and generate bates in just a few steps.
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- how to generate bates
language: en
og_description: Create PDF Document C# with Bates numbering. This guide shows how
  to add bates, add sequential page numbers, and generate bates quickly.
og_title: Create PDF Document C# – Add Bates Numbering
tags:
- C#
- PDF
- Bates numbering
title: Create PDF Document C# – Add Bates Numbering
url: /net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create PDF Document C# – Add Bates Numbering

Ever needed to **create PDF document C#** and then tag each page with a unique identifier for legal or archival purposes? You're not the only one—law firms, courts, and even large corporations constantly ask, “How do I add Bates numbers to my PDFs automatically?” The good news is that with a few lines of code you can generate a PDF, sprinkle Bates numbers across every page, and save the result without ever opening an editor.

In this tutorial we’ll walk through a practical, end‑to‑end example that shows **how to add Bates**, how to **add sequential page numbers**, and even how to **generate Bates** with custom prefixes. By the end you’ll have a reusable snippet that you can drop into any .NET project.

## What You’ll Need

- **.NET 6+** (the code works on .NET Framework 4.6+ as well)
- **Aspose.Pdf for .NET** – a commercial library that offers a clean API for PDF manipulation. A free evaluation works fine for testing.
- A basic understanding of C# (you’re probably already comfortable with `using` statements and objects).

No additional NuGet packages are required beyond `Aspose.Pdf`. If you haven’t installed it yet, run:

```bash
dotnet add package Aspose.Pdf
```

> **Pro tip:** Keep your Aspose version up‑to‑date; the latest 23.x release adds performance tweaks for large documents.

## Step 1: Open (or Create) the Source PDF Document

First we need a PDF to work with. In many real‑world scenarios you already have an input file—say a scanned contract. For the sake of the example we’ll open an existing file called `input.pdf`.

```csharp
using Aspose.Pdf;

// Step 1 – Load the PDF you want to number
var pdfPath = @"C:\Docs\input.pdf";
using var pdfDocument = new Document(pdfPath);
```

> **Why this matters:** Opening the document inside a `using` block guarantees the file handle is released promptly, avoiding file‑lock issues when you later try to overwrite the same file.

## Step 2: Define Your Bates Numbering Options

Bates numbers consist of a **prefix** (often a case identifier) and a **starting number**. You can also control the number of digits, the placement on the page, and the font style. Here we’ll use the secondary keyword **add bates numbering pdf** by configuring a `BatesNumberingOptions` object.

```csharp
// Step 2 – Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    // Primary keyword in action: create pdf document c# with custom settings
    Prefix = "CASE-",
    Start = 1000,
    // Optional: set zero‑padding to 6 digits (e.g., CASE-001000)
    NumberOfDigits = 6,
    // Optional: define where the number appears (bottom‑right corner)
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Optional: choose a readable font
    Font = FontRepository.FindFont("Arial")
};
```

> **How to add bates:** By tweaking `Prefix` and `Start` you control the exact string that will appear on each page. The `NumberOfDigits` property ensures consistent width, which is handy for legal filings.

## Step 3: Apply Bates Numbering to Every Page

Now comes the core operation—adding the numbers. The `AddBatesNumbering` method walks through each page, draws the text, and respects the options we defined.

```csharp
// Step 3 – Apply Bates numbering to all pages
pdfDocument.AddBatesNumbering(batesOptions);
```

Under the hood Aspose renders the text as a *content* element, meaning the numbers become part of the PDF and cannot be turned off in a viewer. This is exactly what you need when you want **add sequential page numbers** that are immutable.

### Edge Cases & Variations

- **Multiple prefixes:** If you need different prefixes per section, create separate `BatesNumberingOptions` and call `AddBatesNumbering` on a page range (`pdfDocument.Pages[1..5]`).
- **Zero‑padding control:** Omit `NumberOfDigits` for a variable‑length number, or set it to a higher value for leading zeros.
- **Custom positioning:** Use `Margin` to offset the number from the edge, or switch `HorizontalAlignment` to `Center` for a footer style.

## Step 4: Save the Modified PDF

Finally, write the updated document to disk. You can overwrite the original or create a brand‑new file.

```csharp
// Step 4 – Save the PDF with Bates numbers applied
var outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
```

After this line runs, `output.pdf` contains the original content plus a visible Bates tag on every page—exactly what you’d expect when you **how to generate bates** for a case file.

## Full, Runnable Example

Putting it all together, here’s the complete snippet you can copy‑paste into a console app:

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Open the source PDF
        var inputFile = @"C:\Docs\input.pdf";
        using var pdf = new Document(inputFile);

        // 2️⃣ Configure Bates numbering (add bates numbering pdf)
        var options = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 1000,
            NumberOfDigits = 6,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = FontRepository.FindFont("Arial")
        };

        // 3️⃣ Apply the numbering (how to add bates)
        pdf.AddBatesNumbering(options);

        // 4️⃣ Save the result (add sequential page numbers)
        var outputFile = @"C:\Docs\output.pdf";
        pdf.Save(outputFile);

        Console.WriteLine("Bates numbering applied successfully!");
    }
}
```

### Expected Result

Open `output.pdf` in any viewer (Adobe Reader, Edge, etc.). You’ll see each page stamped with something like **CASE-001000**, **CASE-001001**, … up to the last page. The numbers sit snugly at the bottom‑right, matching the options we set.

## Common Questions & Troubleshooting

- **“What if my PDF is password‑protected?”**  
  Load it with the password: `new Document(inputFile, new LoadOptions { Password = "secret" })`.

- **“Can I add Bates numbers to a newly created PDF?”**  
  Absolutely. Just create the document first (`var doc = new Document();`) then follow Steps 2‑4 before saving.

- **“Is the font always embedded?”**  
  Aspose automatically embeds the font if it isn’t already in the PDF. If you need a specific font family, set `options.Font` accordingly.

- **“What about performance on 10,000‑page files?”**  
  The library streams pages, so memory usage stays modest. However, you might want to increase the `PdfSaveOptions.CompressionMode` for faster I/O.

## Pro Tips for Production Use

1. **Batch processing:** Wrap the above logic in a loop that iterates over a folder of PDFs. Use `Directory.GetFiles("*.pdf")` and process each file individually.
2. **Logging:** Emit the first and last Bates numbers to a log file—helps auditors verify that numbering was continuous.
3. **Error handling:** Enclose the whole block in a `try/catch` and surface a clear message if the source PDF is missing or corrupted.
4. **Zero‑padding flexibility:** If you need a dynamic digit count based on total pages, calculate `NumberOfDigits = (pdf.Pages.Count + options.Start).ToString().Length`.

## Conclusion

We’ve just shown how to **create PDF document C#** and seamlessly **add Bates numbering**—covering everything from the initial load to the final save. The short example demonstrates **how to add bates**, **add sequential page numbers**, and **how to generate bates** with custom prefixes and zero‑padding. With a few tweaks you can adapt this pattern to batch jobs, different layouts, or even integrate it into a web API that returns a freshly‑numbered PDF on demand.

Ready for the next step? Try combining this with Aspose’s **watermark** feature, or generate a summary index that lists each Bates number alongside a brief description of the page’s content. The possibilities are endless, and the code you now have is a solid foundation for any document‑automation workflow.

Happy coding, and may your PDFs always be perfectly numbered! 

![Screenshot of a PDF viewer showing create pdf document c# with Bates numbers applied](image-placeholder.png "create pdf document c# with Bates numbers")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}