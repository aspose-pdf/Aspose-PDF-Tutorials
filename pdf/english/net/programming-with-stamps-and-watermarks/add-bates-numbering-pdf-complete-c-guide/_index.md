---
category: general
date: 2026-03-03
description: Learn how to add bates numbering PDF and also discover how to add bates,
  create PDF form field, and how to convert PDFX4 in one clear tutorial.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- create pdf form field
- how to convert pdfx4
language: en
og_description: Add Bates numbering PDF, learn how to add bates, create PDF form field,
  and how to convert PDFX4 with practical C# code.
og_title: Add Bates Numbering PDF – Complete C# Guide
tags:
- PDF
- CSharp
- DocumentAutomation
title: Add Bates Numbering PDF – Complete C# Guide
url: /net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Bates Numbering PDF – Complete C# Guide

Ever wondered **how to add bates** to a PDF without pulling your hair out? You’re not alone. In many legal or archival projects, **add bates numbering pdf** is the first line on the to‑do list, and if you miss a step the whole filing system can fall apart.  

In this tutorial we’ll walk through four real‑world tasks: detecting a compromised signature, **add bates numbering pdf**, converting a file **how to convert pdfx4**, and finally **create PDF form field** with two widget annotations. By the end you’ll have a single, runnable C# program that does all of this, plus tips on pitfalls you might hit along the way.

## Prerequisites

- .NET 6 SDK or later (the code uses the latest language features, but .NET 5 works too)
- A PDF processing library that exposes `Document`, `BatesNumberingOptions`, `PdfFormatConversionOptions`, `TextBoxField`, etc. (the examples are based on a typical commercial SDK; replace the namespaces if you use a different one)
- A folder called `YOUR_DIRECTORY` with a few sample PDFs (`signed.pdf`, `input.pdf`, `source.pdf`) so you can see the output files appear next to them
- Visual Studio 2022 or any IDE you prefer

Now that we’ve set the stage, let’s dive in.

## Step 1 – Detect if a PDF Signature Is Compromised

Before you start stamping or converting, it’s good practice to verify that any existing digital signatures are still valid. A compromised signature could mean the document was altered after signing, and blindly adding Bates numbers would invalidate legal compliance.

```csharp
using System;
using YourPdfLibrary;   // replace with the actual namespace of your PDF SDK

// Load the signed PDF
Document signedDoc = new Document("YOUR_DIRECTORY/signed.pdf");

// Check the signature status
bool isCompromised = signedDoc.IsSignatureCompromised();

// Output the result – true means the signature is no longer trustworthy
Console.WriteLine($"Signature compromised? {isCompromised}");
```

**Why this matters:**  
If `isCompromised` returns `true`, you should either reject the file or request a fresh signature before proceeding. Adding Bates numbers to a tampered document could be considered fraud in a courtroom.

**Pro tip:** Some SDKs let you retrieve *why* the signature failed (e.g., altered content, expired certificate). Log that information for audit trails.

## Step 2 – Add Bates Numbering PDF

Now for the star of the show: **add bates numbering pdf**. Bates numbers are sequential identifiers that usually appear in the header or footer of each page. The SDK’s `AddBatesNumbering` method does the heavy lifting, but you still need to decide on a prefix, start number, and placement.

```csharp
// Load the source PDF you want to number
Document batesSource = new Document("YOUR_DIRECTORY/input.pdf");

// Configure Bates numbering options
var batesOptions = new BatesNumberingOptions
{
    Prefix = "2025-",    // optional text before the numeric part
    Start = 1000,        // first number in the sequence
    // You can also set Font, FontSize, Color, Position, etc.
};

// Apply the numbering to every page
batesSource.AddBatesNumbering(batesOptions);

// Save the newly numbered PDF
batesSource.Save("YOUR_DIRECTORY/bates.pdf");

// Verify quickly – the console will show the file path
Console.WriteLine("Bates‑numbered PDF saved as bates.pdf");
```

**How to add bates** correctly:  

- **Placement:** Most lawyers want the number in the bottom‑right corner. If the SDK defaults elsewhere, set `batesOptions.Position = BatesNumberPosition.BottomRight;`.
- **Zero‑padding:** To keep sorting easy, use `batesOptions.NumberFormat = "D6";` (produces `001000`, `001001`, …).
- **Multiple prefixes:** If you have several document batches, concatenate a batch code to the prefix (`"2025-AB-"`).

**Edge case:** If the source PDF already contains a footer, the new number might overlap. Test on a sample page and adjust `Margin` or `Offset` values accordingly.

![Screenshot of a PDF with Bates numbers added – demonstrating add bates numbering pdf](add-bates-numbering-pdf.png "add bates numbering pdf")

*Image alt text: “Screenshot showing add bates numbering pdf in C# with visible sequential numbers.”*

## Step 3 – How to Convert PDFX4

The PDF/X‑4 format is a subset of PDF designed for reliable printing and archiving. Converting to PDF/X‑4 strips out unsupported features and enforces color‑profile consistency. Here’s **how to convert pdfx4** using the same `Document` class.

```csharp
// Load the original PDF you wish to convert
Document pdfSource = new Document("YOUR_DIRECTORY/source.pdf");

// Set up conversion options – we want PDF/X‑4 and we’ll delete any pages that cause errors
var conversionOptions = new PdfFormatConversionOptions(
    PdfFormat.PDF_X_4,               // target format
    ConvertErrorAction.Delete);     // action on conversion errors

// Perform the conversion
pdfSource.Convert(conversionOptions);

// Persist the new PDF/X‑4 file
pdfSource.Save("YOUR_DIRECTORY/pdfx4.pdf");

// Quick confirmation
Console.WriteLine("Converted to PDF/X‑4 and saved as pdfx4.pdf");
```

**Why PDF/X‑4?**  
- Guarantees that all fonts are embedded.  
- Preserves transparency, unlike older PDF/X‑1a.  
- Ideal for high‑end presses that demand a strict workflow.

**Common pitfalls when you ask “how to convert pdfx4”:**  

- **Unsupported color spaces:** If the source uses DeviceCMYK, the conversion may fail unless you embed an ICC profile.  
- **Large images:** The conversion process can inflate file size; consider down‑sampling (`conversionOptions.ImageResolution = 300;`).  
- **Form fields:** Some PDF/X flavors strip interactive elements. If you need to keep them, double‑check the SDK’s compliance level.

## Step 4 – Create PDF Form Field (Two Widget Annotations)

Finally, let’s **create PDF form field** that appears on two different pages. A single logical field can have multiple visual representations (widgets). This is perfect for “Notes” sections that need to be accessible throughout the document.

```csharp
// Start with a fresh document
Document formDoc = new Document();

// Add the first page and place the field there
Page firstPage = formDoc.Pages.Add();
var notesField = new TextBoxField(firstPage,
    new Rectangle(50, 700, 300, 750))   // left, bottom, right, top
{
    Name = "Notes",
    Value = "Enter your comments here..."
};

// Add a second page and attach a second widget to the same field
Page secondPage = formDoc.Pages.Add();
notesField.AddWidgetAnnotation(secondPage, new Rectangle(50, 500, 300, 550));

// Register the field with the document’s form collection
formDoc.Form.Add(notesField, notesField.Name);

// Save the result
formDoc.Save("YOUR_DIRECTORY/twoWidgets.pdf");
Console.WriteLine("PDF with two widget annotations saved as twoWidgets.pdf");
```

**What’s happening under the hood:**  

- The `TextBoxField` object holds the *data* (the actual text) and a *default appearance* (font, size).  
- `AddWidgetAnnotation` creates a visual representation on another page but points back to the same underlying field, so whatever the user types on page 1 appears on page 2 automatically.  
- By adding the field to `formDoc.Form`, the PDF becomes **interactive** and can be filled in any PDF viewer.

**Tips for reliable form fields:**  

- **Set a proper font** (`notesField.Font = FontTimesRoman;`) to avoid substitution warnings.  
- **Enable JavaScript validation** if your workflow demands it (`notesField.Actions.OnBlur = "if (this.value.length > 200) app.alert('Too long');"`).  
- **Flatten the form** (`formDoc.Form.Flatten();`) when you finally need a read‑only version for archiving.

## Full Working Example

Putting everything together, here’s a single program you can copy‑paste, compile, and run. It demonstrates **add bates numbering pdf**, **how to convert pdfx4**, and **create PDF form field** in one cohesive flow.

```csharp
using System;
using YourPdfLibrary;   // Replace with your actual PDF SDK namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Detect compromised signature
        Document signedDoc = new Document("YOUR_DIRECTORY/signed.pdf");
        bool compromised = signedDoc.IsSignatureCompromised();
        Console.WriteLine($"Signature compromised? {compromised}");

        // 2️⃣ Add Bates numbering – this is the core “add bates numbering pdf” step
        Document batesSource = new Document("YOUR_DIRECTORY/input.pdf");
        var batesOpts = new BatesNumberingOptions
        {
            Prefix = "2025-",
            Start = 1000,
            NumberFormat = "D6",
            Position = BatesNumberPosition.BottomRight,
            Margin = 20
        };
        batesSource.AddBatesNumbering(batesOpts);
        batesSource.Save("YOUR_DIRECTORY/bates.pdf");
        Console.WriteLine("Bates‑numbered PDF saved.");

        // 3️⃣ Convert to PDF/X‑4 – “how to convert pdfx4”
        Document pdfSource = new Document("YOUR_DIRECTORY/source.pdf");
        var convOpts = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_4,
            ConvertErrorAction.Delete);
        pdfSource.Convert(convOpts);
        pdfSource.Save("YOUR_DIRECTORY/pdfx4.pdf");
        Console.WriteLine("Converted to PDF/X‑4.");

        // 4️⃣ Create a form field with two widgets – “create PDF form field”
        Document formDoc = new Document();
        Page p1 = formDoc.Pages.Add();
        var notes = new TextBoxField(p1,
            new Rectangle(50, 700, 300, 750))
        {
            Name = "Notes",
            Value = "Enter your comments here..."
        };
        Page p2 = formDoc.Pages.Add();
        notes.AddWidgetAnnotation(p2, new Rectangle(50, 500, 300, 550));
        formDoc.Form.Add(notes, notes.Name);
        formDoc.Save("YOUR_DIRECTORY/twoWidgets.pdf");
        Console.WriteLine("Form PDF with two widgets saved.");
    }
}
```

**Expected output:**  

```
Signature compromised? False

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}