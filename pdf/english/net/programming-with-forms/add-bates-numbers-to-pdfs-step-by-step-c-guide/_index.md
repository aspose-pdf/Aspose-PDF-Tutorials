---
category: general
date: 2026-02-12
description: Add Bates numbers to PDF files quickly. Learn how to add text field PDF,
  add form field PDF, and add page numbers PDF using Aspose.PDF.
draft: false
keywords:
- add bates numbers
- add text field pdf
- add form field pdf
- add page numbers pdf
- how to add bates
language: en
og_description: Add Bates numbers to PDF documents in C#. This guide shows how to
  add text field PDF, add form field PDF, and add page numbers PDF with Aspose.PDF.
og_title: Add Bates Numbers to PDFs – Complete C# Tutorial
tags:
- PDF
- C#
- Aspose.PDF
title: Add Bates Numbers to PDFs – Step‑by‑Step C# Guide
url: /net/programming-with-forms/add-bates-numbers-to-pdfs-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Bates Numbers to PDFs – Complete C# Guide

Ever needed to **add bates numbers** to a stack of legal PDFs but weren’t sure where to start? You’re not alone. In many law firms and e‑discovery projects, stamping every page with a unique identifier is a daily chore, and doing it manually is a nightmare.  

The good news? With a few lines of C# and Aspose.PDF you can automate the whole thing. In this tutorial we’ll walk through **how to add bates** numbers, sprinkle a text field on each page, and save a clean, searchable PDF—all without breaking a sweat.

> **What you’ll get:** a fully runnable code sample, explanations of why each line matters, tips for edge cases, and a quick checklist to verify your output.  

We’ll also touch on related tasks like **add text field pdf**, **add form field pdf**, and **add page numbers pdf**, so you’ll have a toolbox ready for any document‑automation challenge.

---

## Prerequisites

- .NET 6.0 or later (the code works with .NET Framework 4.6+ as well)  
- Visual Studio 2022 (or any IDE you prefer)  
- A valid Aspose.PDF for .NET license (the free trial works for testing)  
- A source PDF named `source.pdf` placed in a folder you can reference  

If any of these sound unfamiliar, just pause and install the missing piece before moving on. The steps below assume you’ve already added the Aspose.PDF NuGet package:

```bash
dotnet add package Aspose.Pdf
```

---

## How to add bates numbers to a PDF with Aspose.PDF

Below is the complete, copy‑paste‑ready program. It loads a PDF, creates a **text box field** on every page, writes a formatted Bates number, and finally writes the modified file out.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 👉 Step 1: Load the source PDF document
        using (var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf"))
        {
            // 👉 Step 2: Add a Bates number text field to each page
            for (int pageNumber = 1; pageNumber <= pdfDocument.Pages.Count; pageNumber++)
            {
                // Define the rectangle where the field will appear (10,10) = lower‑left corner
                var fieldRect = new Rectangle(10, 10, 150, 30);

                // Create the TextBoxField – this is the “add text field pdf” part
                var batesField = new TextBoxField(pdfDocument.Pages[pageNumber], fieldRect)
                {
                    // Format the number: BATES-00001, BATES-00002, …
                    Value = $"BATES-{pageNumber:D5}"
                };

                // Register the field with the form collection – “add form field pdf”
                pdfDocument.Form.Add(batesField, $"Bates_{pageNumber}", pageNumber);
            }

            // 👉 Step 3: Save the modified PDF with Bates numbers
            pdfDocument.Save(@"YOUR_DIRECTORY\bates.pdf");
        }

        Console.WriteLine("✅ Bates numbers added successfully!");
    }
}
```

### Why this works

- **`Document`** is the entry point; it represents the whole PDF file.  
- **`Rectangle`** defines where the field lives on the page. The numbers are in points (1 pt ≈ 1/72 in). Adjust the coordinates if you need the number in a different corner.  
- **`TextBoxField`** is a *form field* that can hold any string. By assigning `Value` we effectively **add page numbers pdf** with a custom prefix.  
- **`pdfDocument.Form.Add`** registers the field with the PDF’s AcroForm, making it visible in viewers like Adobe Acrobat.  

If you ever need to change the appearance (font, color, size) you can tweak the `TextBoxField` properties—see the Aspose docs for `DefaultAppearance` and `Border`.

---

## Adding a text field to each PDF page (the “add text field pdf” step)

Sometimes you only want a visible label, not an interactive form field. In that case you can replace the `TextBoxField` with a `TextFragment` and add it directly to the page’s `Paragraphs` collection. Here’s a quick alternative:

```csharp
var fragment = new TextFragment($"BATES-{pageNumber:D5}")
{
    // Position the text using a TextState (font, size, color)
    TextState = new TextState
    {
        Font = FontRepository.FindFont("Arial"),
        FontSize = 12,
        ForegroundColor = Color.Black
    }
};

// Set the fragment’s rectangle (same coordinates as before)
fragment.Position = new Position(10, 10);
pdfDocument.Pages[pageNumber].Paragraphs.Add(fragment);
```

The **add text field pdf** approach is useful when the final document will be read‑only, while the **add form field pdf** method keeps the numbers editable later on.

---

## Saving the PDF with Bates numbers (the “add page numbers pdf” moment)

After the loop finishes, calling `pdfDocument.Save` writes everything to disk. If you need to preserve the original file, simply change the output path or use `pdfDocument.Save` overloads to stream the result directly to a response in a web API.

```csharp
// Example: stream to HTTP response (ASP.NET Core)
Response.ContentType = "application/pdf";
pdfDocument.Save(Response.Body);
```

That’s the neat part—no temporary files, no extra libraries, just Aspose handling the heavy lifting.

---

## Expected Result & Quick Verification

Open `bates.pdf` in any PDF viewer. You should see a small box in the lower‑left corner of every page reading:

```
BATES-00001
BATES-00002
…
```

If you inspect the document properties, you’ll notice an AcroForm containing fields named `Bates_1`, `Bates_2`, etc. That confirms the **add form field pdf** step succeeded.

---

## Common Pitfalls & Pro Tips

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| Numbers appear off‑center | Rectangle coordinates are relative to the page’s lower‑left corner. | Flip the Y‑value (`pageHeight - marginTop`) or use `page.PageInfo.Height` to calculate a top‑margin placement. |
| Fields are invisible in Adobe Reader | The default border is set to “No”. | Set `batesField.Border = new Border { Width = 0.5f, Color = Color.Black };` |
| Large PDFs cause memory pressure | `using` disposes the document only after the loop finishes. | Process pages in chunks or use `pdfDocument.Save` with `SaveOptions` that enable streaming. |
| License not applied | Aspose prints a watermark on the first page. | Register your license early: `License lic = new License(); lic.SetLicense("Aspose.Pdf.lic");` |

---

## Extending the Solution

- **Custom prefixes:** Replace `"BATES-"` with any string (`"DOC-"`, `"CASE-"`, …).  
- **Zero‑padding length:** Change `{pageNumber:D5}` to `{pageNumber:D3}` for three digits.  
- **Dynamic placement:** Use `pdfDocument.Pages[pageNumber].PageInfo.Width` to position the field on the right‑hand side.  
- **Conditional numbering:** Skip blank pages by checking `pdfDocument.Pages[pageNumber].IsBlank`.

All these variations keep the core pattern of **add bates numbers**, **add text field pdf**, and **add form field pdf** intact.

---

## Full Working Example (All‑in‑One)

Below is the final, ready‑to‑run program that incorporates the tips above. Copy it into a new console app and hit F5.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;

class AddBatesNumbers
{
    static void Main()
    {
        // Register your license here (optional for trial)
        // var license = new License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        using (var pdfDocument = new Document(inputPath))
        {
            int totalPages = pdfDocument.Pages.Count;

            for (int i = 1; i <= totalPages; i++)
            {
                // Position the field 10 pts from left and 10 pts from bottom
                var rect = new Rectangle(10, 10, 150, 30);

                var batesField = new TextBoxField(pdfDocument.Pages[i], rect)
                {
                    Value = $"BATES-{i:D5}"
                };

                // Optional: make the field look nicer
                batesField.Border = new Border
                {
                    Width = 0.5f,
                    Color = Color.Gray
                };
                batesField.DefaultAppearance = new DefaultAppearance
                {
                    Font = FontRepository.FindFont("Arial"),
                    FontSize = 10,
                    ForegroundColor = Color.DarkBlue
                };

                pdfDocument.Form.Add(batesField, $"Bates_{i}", i);
            }

            pdfDocument.Save(outputPath);
        }

        Console.WriteLine($"✅ Finished! Bates numbers saved to: {outputPath}");
    }
}
```

Run it, open the result, and you’ll see a professional‑looking identifier on every page—exactly what a litigation support specialist would expect.

---

## Conclusion

We just demonstrated **how to add bates numbers** to any PDF using C# and Aspose.PDF. By creating a **text box field** on each page we simultaneously **add text field pdf**, **add form field pdf**, and **add page numbers pdf** in a single pass. The approach is fast, scalable, and easy to tweak for custom prefixes, different layouts, or conditional logic.

Ready for the next challenge? Try embedding a QR code that links to the original case file, or generate a separate index page that lists all Bates numbers with their corresponding page titles. The same API lets you merge PDFs, extract pages, and even redact sensitive data—so the sky’s the limit.

If you hit a snag, drop a comment below or check Aspose’s official documentation for deeper dives. Happy coding, and may your PDFs always stay perfectly numbered!  

---  

![add bates numbers screenshot](https://example.com/images/add-bates-numbers.png "add bates numbers example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}