---
category: general
date: 2026-06-08
description: Create multi page form in C# using Aspose.Pdf. Learn how to add textbox
  to pdf, create pdf form field, and save updated pdf with clear code examples.
draft: false
keywords:
- create multi page form
- add textbox to pdf
- create pdf form field
- how to save pdf
- save updated pdf
language: en
og_description: Create multi page form in C# with Aspose.Pdf. This guide shows how
  to add textbox to pdf, create pdf form field, and save updated pdf in minutes.
og_title: Create Multi Page Form in C# – Complete Aspose.Pdf Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create multi page form in C# using Aspose.Pdf. Learn how to add textbox
    to pdf, create pdf form field, and save updated pdf with clear code examples.
  headline: Create Multi Page Form in C# with Aspose.Pdf – Step‑by‑Step Guide
  type: TechArticle
- description: Create multi page form in C# using Aspose.Pdf. Learn how to add textbox
    to pdf, create pdf form field, and save updated pdf with clear code examples.
  name: Create Multi Page Form in C# with Aspose.Pdf – Step‑by‑Step Guide
  steps:
  - name: '**Load** the existing PDF.'
    text: '**Load** the existing PDF.'
  - name: '**Create** a `TextBoxField` on the first page – this is our form field.'
    text: '**Create** a `TextBoxField` on the first page – this is our form field.'
  - name: '**Add** a widget annotation on the second page so the same field appears
      there too.'
    text: '**Add** a widget annotation on the second page so the same field appears
      there too.'
  - name: '**Save** the modified document as a new file.'
    text: '**Save** the modified document as a new file.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF Forms
title: Create Multi Page Form in C# with Aspose.Pdf – Step‑by‑Step Guide
url: /net/programming-with-forms/create-multi-page-form-in-c-with-aspose-pdf-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Multi Page Form in C# with Aspose.Pdf – Complete Guide

Ever wondered how to **create multi page form** in C# without wrestling with low‑level PDF specs? You're not the only one. Whether you're building a job‑application portal or a tax‑return wizard, a multi‑page PDF form can make data collection feel slick and professional.

In this tutorial we’ll walk through a real‑world example that **adds textbox to pdf**, **creates pdf form field**, and finally **saves updated pdf**. By the end you’ll have a fully functional two‑page form you can drop into any .NET project.

> **Pro tip:** Aspose.Pdf works on .NET 6+, .NET Framework 4.6+ and even .NET Core, so you’re covered whether you’re on Windows or Linux.

## What You’ll Need

- **Aspose.Pdf for .NET** (NuGet package `Aspose.Pdf`).  
- A simple PDF file (`input.pdf`) that already has at least two pages.  
- Visual Studio 2022 or any editor that supports C#.  
- A folder you can read/write to – we’ll reference it as `YOUR_DIRECTORY`.

No other dependencies. Ready? Let’s dive in.

![Create multi page form example in C# using Aspose.Pdf](image.png "Create multi page form example")

## Create Multi Page Form – Overview

Before we start typing code, let’s outline the high‑level flow:

1. **Load** the existing PDF.  
2. **Create** a `TextBoxField` on the first page – this is our form field.  
3. **Add** a widget annotation on the second page so the same field appears there too.  
4. **Save** the modified document as a new file.

Each step is deliberately isolated so you can swap out pieces (e.g., change the rectangle size or add more pages) without breaking the whole thing.

## Step 1 – Load the PDF Document

The first thing you do when working with any PDF library is open the source file. Aspose.Pdf makes this a one‑liner.

```csharp
// Step 1: Load the PDF document from disk
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document(@"YOUR_DIRECTORY\input.pdf");
```

*Why this matters:* Loading the document gives you access to the `Pages` collection, which is where we’ll attach our form field and widget later. If the file isn’t found an exception is thrown, so make sure the path is correct.

## Step 2 – Create a TextBox Form Field (add textbox to pdf)

Now we actually **create pdf form field** – a `TextBoxField`. Think of it as the data container that will hold whatever the user types.

```csharp
// Step 2: Instantiate a TextBoxField on page 1
Aspose.Pdf.Forms.TextBoxField commentsField = new Aspose.Pdf.Forms.TextBoxField(
    pdfDocument.Pages[1],                                   // target page (1‑based index)
    new Aspose.Pdf.Rectangle(100, 100, 300, 120));         // position & size (LLX, LLY, URX, URY)
```

A few notes:

- The rectangle coordinates are expressed in points (1 pt = 1/72 in). Adjust them to fit your layout.
- `pdfDocument.Pages[1]` refers to the **first** page because Aspose uses a 1‑based collection.
- By creating the field on page 1 we also give it a default appearance, which we’ll reuse on page 2.

## Step 3 – Set the Field’s Name and Initial Value

Every form field needs an identifier. This is the string you’ll later reference when extracting user input.

```csharp
// Step 3: Assign a name and an empty default value
commentsField.Name = "Comments";   // unique field name
commentsField.Value = "";          // start with a blank textbox
```

*Why name it “Comments”?* It’s descriptive, but you can call it anything (`"Address"`, `"PhoneNumber"`). Just keep it unique across the whole PDF; duplicate names cause data collisions when the form is submitted.

## Step 4 – Add a Widget Annotation on the Second Page

A *widget* is the visual representation of a form field on a particular page. By default the field we created lives only on page 1. To make the same textbox appear on page 2 we add a widget annotation.

```csharp
// Step 4: Place the same TextBoxField on page 2 via a widget
commentsField.Widgets.Add(
    new Aspose.Pdf.Forms.WidgetAnnotation(
        pdfDocument.Pages[2],                               // second page
        new Aspose.Pdf.Rectangle(50, 50, 250, 70)));       // widget rectangle
```

Why a widget? Because PDF forms separate **field definition** (the data) from **widget appearance** (what the user sees). Adding a widget lets the user fill the same field on multiple pages—a classic requirement for multi‑page forms.

### Edge‑Case Tip

If your source PDF has more than two pages and you want the textbox on every page, loop over `pdfDocument.Pages` and add a widget for each one. Just remember to keep the rectangle size appropriate for each page’s layout.

## Step 5 – Save the Updated PDF (how to save pdf)

Finally we persist our changes. Aspose.Pdf offers a straightforward `Save` method that overwrites or creates a new file.

```csharp
// Step 5: Save the updated PDF to a new file
pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
```

*Why not overwrite `input.pdf`?* Keeping the original untouched makes debugging easier and lets you compare before/after results. If you truly need to replace the source, just call `Save` with the same path.

## Full Working Example

Putting it all together, here’s the complete, ready‑to‑run program.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // Load the existing PDF (make sure the file exists)
        Document pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // Create a TextBoxField on the first page
        TextBoxField commentsField = new TextBoxField(
            pdfDocument.Pages[1],
            new Rectangle(100, 100, 300, 120));

        // Configure the field
        commentsField.Name = "Comments";
        commentsField.Value = ""; // blank by default

        // Add a widget on the second page so the same field appears there
        commentsField.Widgets.Add(
            new WidgetAnnotation(
                pdfDocument.Pages[2],
                new Rectangle(50, 50, 250, 70)));

        // Save the modified PDF
        pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");

        // Optional: inform the user
        System.Console.WriteLine("Multi‑page form created successfully!");
    }
}
```

### Expected Output

When you open `output.pdf` in Adobe Acrobat Reader:

- Page 1 shows an empty textbox at coordinates (100, 100)‑(300, 120).  
- Page 2 shows the same textbox at (50, 50)‑(250, 70).  
- Both boxes share the **field name** `Comments`, meaning the data entered on either page syncs automatically.

## Common Questions & Gotchas

| Question | Answer |
|----------|--------|
| *Can I add more than one textbox?* | Absolutely. Just repeat steps 2‑4 with a new `TextBoxField` instance and a unique `Name`. |
| *What if the PDF has no second page?* | The code will throw an `ArgumentOutOfRangeException`. Guard it with `if (pdfDocument.Pages.Count >= 2) { … }`. |
| *Do I need to set fonts?* | Aspose uses the default Helvetica. For custom fonts, set `commentsField.DefaultAppearance.Font` before saving. |
| *Is the field printable?* | Yes – Aspose marks widgets as printable by default. You can toggle `WidgetAnnotation.Flags` if needed. |
| *How to extract the entered value later?* | After users fill the form and you receive the PDF, call `pdfDocument.Form["Comments"].Value` to read the data. |

## Next Steps

Now that you know **how to save pdf** after adding a textbox, you might want to explore:

- Adding **checkboxes** or **radio buttons** (`CheckBoxField`, `RadioButtonField`).  
- Using **JavaScript** actions for client‑side validation (`commentsField.Actions.OnMouseUp = "…"`).  
- **Flattening** the form to prevent further edits (`pdfDocument.Form.Flatten()`).  

All of these build on the same concepts we covered while **creating multi page form**.

---

**Bottom line:** You’ve just learned how to **create multi page form** in C# with Aspose.Pdf, how to **add textbox to pdf**, how to **create pdf form field**, and the exact steps to **save updated pdf**. Feel free to tweak the rectangles, add more fields, or loop over all pages for a truly dynamic solution.

Got a twist you’d like to share? Drop a comment below, and happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create PDF with Aspose – Add Form Field and Pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Create PDF Document with Aspose – Add Page, Text Box, and Form](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)
- [How to Add and Extract PDF Form Fields Using Aspose.PDF for .NET: A Comprehensive Guide](/pdf/english/net/forms-annotations/manage-pdf-form-fields-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}