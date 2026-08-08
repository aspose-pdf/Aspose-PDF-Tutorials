---
category: general
date: 2026-03-27
description: Add Bates numbering in C# quickly. Learn how to add custom page numbers,
  add sequential page numbers, and add custom numbers to Word docs.
draft: false
keywords:
- add bates numbering
- how to add bates
- add custom page numbers
- add sequential page numbers
- add custom numbers
language: en
og_description: Add Bates numbering in C# with a clear example. This guide shows how
  to add custom page numbers, add sequential page numbers, and more.
og_title: Add Bates Numbering in C# – Complete Tutorial
tags:
- C#
- Document Processing
- Bates Numbering
title: Add Bates Numbering in C# – Step‑by‑Step Guide
url: /net/programming-with-pdf-pages/add-bates-numbering-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Bates Numbering in C# – Step‑by‑Step Guide

Ever wondered how to **add bates numbering** to a Word document without pulling your hair out? You're not the only one. In many legal or compliance projects, every page needs a unique identifier, and doing it by hand is a nightmare.  

In this tutorial we’ll walk through a complete, runnable example that **adds bates numbering**, shows you **how to add bates** in a few lines, and even covers how to **add custom page numbers** and **add sequential page numbers** when you need them. By the end you’ll have a .docx file stamped with the numbers you choose—no third‑party tools required.

## What You’ll Learn

- Load a DOCX file with the Aspose.Words for .NET API (or any compatible library).  
- Configure **add custom numbers** such as a prefix, a start value, and a font size.  
- Apply the numbering to every page in one call.  
- Save the result and verify that the numbers appear as expected.  

No prior experience with Bates numbering is required; just a basic C# setup and a copy of the source document. Let’s dive in.

## Prerequisites

- .NET 6+ (the code works on .NET Core and .NET Framework alike).  
- Aspose.Words for .NET installed via NuGet (`Install-Package Aspose.Words`).  
- A Word document named `input.docx` placed in a folder you can reference (`YOUR_DIRECTORY`).  
- Visual Studio, VS Code, or any C# IDE you like.

> **Pro tip:** If you’re using a different library (e.g., Open XML SDK), the concepts stay the same—just swap the API calls.

## Step 1: Load the Source Document

First we need to bring the Word file into memory.

```csharp
using Aspose.Words;

// Step 1: Load the source document
Document document = new Document("YOUR_DIRECTORY/input.docx");
```

*Why this matters:* Loading the file creates a `Document` object that gives you access to pages, sections, and the low‑level node tree. Without it you can’t attach any numbering.

## Step 2: Configure Bates Numbering Options

Now we define exactly how the numbers should look. This is where you **add custom page numbers** or **add sequential page numbers**.

```csharp
// Step 2: Define Bates numbering options (prefix, start number, font size)
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Prefix that appears before every number, e.g., "ABC"
    Prefix = "ABC",
    // The first number in the sequence; change to 1 if you prefer
    Start = 1000,
    // Font size in points; 9 works well for most legal docs
    FontSize = 9
};
```

*Why this matters:* The `Prefix` lets you **add custom numbers** like a case ID, while `Start` determines the initial counter. Changing `FontSize` ensures the numbers don’t swallow the page margins.

## Step 3: Apply Bates Numbering to Every Page

With the options ready, we tell the library to stamp each page.

```csharp
// Step 3: Apply Bates numbering to all pages of the document
document.Pages.AddBatesNumbering(batesOptions);
```

*Why this matters:* The `AddBatesNumbering` method walks through the internal page collection and injects a text box at the bottom‑right corner (the default location). It’s the core of **how to add bates** without writing a loop yourself.

## Step 4: Save the Updated Document

Finally, we write the modified file back to disk.

```csharp
// Step 4: Save the updated document
document.Save("YOUR_DIRECTORY/output.docx");
```

*Why this matters:* Saving creates a new `output.docx` that you can open in Word, LibreOffice, or any viewer to confirm the numbers appear.

## Expected Result

Open `output.docx`. Every page should display something like:

```
ABC‑1000   (on page 1)
ABC‑1001   (on page 2)
ABC‑1002   (on page 3)
...
```

If you open the document’s print preview you’ll see the numbers in the lower‑right corner, matching the font size you set.

## Edge Cases & Variations

| Situation | What to Change | Why |
|-----------|----------------|-----|
| **No prefix needed** | `Prefix = string.Empty` | Removes the “ABC‑” part, leaving only the numeric sequence. |
| **Start at 1** | `Start = 1` | Useful for simple **add sequential page numbers** without a custom prefix. |
| **Large documents (>10,000 pages)** | Increase `FontSize` or adjust `Location` (use overloads of `AddBatesNumbering`) | Prevents overlap with footers or headers. |
| **Read‑only source file** | Open with `LoadOptions` that allow write access, or copy the file first | Otherwise `document.Save` will throw an exception. |
| **Different placement** | Use `batesOptions.Position = BatesNumberingPosition.TopLeft` (or other enum) | Some firms require numbers at the top of the page. |

> **Note:** Not all libraries expose a `BatesNumberingOptions` class. With Open XML SDK you’d insert a `TextBox` manually—same principle, more code.

## Full Working Example

Here’s the entire program in one place. Copy‑paste it into a console app and run.

```csharp
using System;
using Aspose.Words;

class Program
{
    static void Main()
    {
        // Load the source document
        Document document = new Document("YOUR_DIRECTORY/input.docx");

        // Define Bates numbering options
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC",      // custom prefix
            Start = 1000,        // starting number
            FontSize = 9         // font size in points
        };

        // Apply numbering to every page
        document.Pages.AddBatesNumbering(batesOptions);

        // Save the result
        document.Save("YOUR_DIRECTORY/output.docx");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

Run the program, open `output.docx`, and you’ll see the numbering exactly where you expected. 🎉

## Frequently Asked Questions

**Q: Can I change the color of the numbers?**  
A: Yes. After calling `AddBatesNumbering`, you can retrieve the generated `Shape` objects and set their `FillColor` property.

**Q: What if I need the numbers on the left side instead of the right?**  
A: Use `batesOptions.Position = BatesNumberingPosition.BottomLeft` (or `TopLeft`, `TopRight`). The API supports all four corners.

**Q: Does this work with PDF output?**  
A: Absolutely. After adding the numbering, call `document.Save("output.pdf")`. The numbers are rendered into the PDF just like in Word.

## Conclusion

You now know **how to add bates numbering** to a Word file using C#. The tutorial covered loading a document, configuring **add custom numbers**, applying **add sequential page numbers**, and saving the final result. With the full code sample, you can drop this into any project and start stamping documents instantly.

Ready for the next challenge? Try combining this with a batch processor that loops through a folder of files, or explore **add custom page numbers** in the header/footer for a more polished look. Either way, you’ve got a solid foundation for any legal‑tech or compliance automation task.

Got questions or a cool use‑case? Leave a comment below, and happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}