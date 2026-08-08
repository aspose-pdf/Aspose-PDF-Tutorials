---
category: general
date: 2026-04-10
description: Create PDF document C# with a clear example. Learn how to add multiple
  pages PDF, add text box field, how to add widget, and save PDF with form.
draft: false
keywords:
- create pdf document c#
- add multiple pages pdf
- save pdf with form
- how to add widget
- add text box field
language: en
og_description: Create PDF document C# quickly. This guide shows how to add multiple
  pages PDF, add text box field, how to add widget, and save PDF with form.
og_title: Create PDF Document C# – Complete Multi‑Page Form Tutorial
tags:
- C#
- PDF
- Form handling
title: Create PDF Document C# – Step‑by‑Step Guide to Multi‑Page Forms
url: /net/programming-with-forms/create-pdf-document-c-step-by-step-guide-to-multi-page-forms/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create PDF Document C# – Step‑by‑Step Guide to Multi‑Page Forms

Ever wondered how to **create PDF document C#** that spans several pages and contains interactive fields? Maybe you’re building an invoice generator, a registration form, or a simple report that users can fill out later. In this tutorial we’ll walk through the whole process—from initializing a PDF, adding multiple pages, inserting a text box field, attaching a widget annotation, to finally **save PDF with form** data. No fluff, just a hands‑on example you can copy‑paste and run today.

We'll also sprinkle in practical tips like *how to add widget* correctly and why you might want to reuse a field across pages. By the end you’ll have a working `multibox.pdf` that demonstrates a shared text box across two pages.

## Prerequisites

- .NET 6+ (or .NET Framework 4.7 or higher) – any recent runtime works.
- A PDF manipulation library that provides `Document`, `TextBoxField`, and `WidgetAnnotation` classes. The code below uses the popular **Aspose.PDF for .NET**, but the concepts translate to iTextSharp, PdfSharp, or other libraries.
- Visual Studio 2022 or any IDE you prefer.
- Basic C# familiarity – you don’t need deep PDF internals, just the API calls.

> **Pro tip:** If you haven’t installed the library yet, run `dotnet add package Aspose.PDF` from the terminal.

## Step 1: Create PDF Document C# – Initialize the Document

First things first, we need a blank canvas. The `Document` object represents the whole PDF file.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Create a new PDF document
using (var document = new Document())
{
    // The rest of the code lives inside this using block
}
```

Why wrap the document in a `using` statement? It guarantees that all unmanaged resources are released, and the file gets flushed to disk when we call `Save`. This pattern is the recommended way to work with PDFs in C#.

## Step 2: Add Multiple Pages PDF

A PDF without pages is, well, invisible. Let’s add two pages—one will host the field itself, the other will hold a widget that points to the same field.

```csharp
// Step 2: Add two pages – one for the field, one for the widget
var firstPage = document.Pages.Add();
var secondPage = document.Pages.Add();
```

> **Why two pages?** When you want the same input to appear on several pages, you create a *field* once and then reference it with *widget annotations* on the other pages. This keeps the data synchronized automatically.

Below is a simple diagram that visualizes the relationship (alt text includes the primary keyword for accessibility).

![Create PDF document C# diagram showing field on page 1 and widget on page 2](image.png)

*Alt text: create pdf document c# diagram illustrating a shared text box field across two pages.*

## Step 3: Add Text Box Field to Your PDF

Now we place a text box on the first page. The rectangle defines its position and size (coordinates are in points, 72 pts = 1 inch).

```csharp
// Step 3: Create a text box field on the first page and give it a shared name and value
var sharedTextBox = new TextBoxField(firstPage, new Rectangle(100, 600, 300, 620));
sharedTextBox.PartialName = "MultiBox";
sharedTextBox.Value = "Shared value";
```

- **PartialName** is the identifier that both the field and any widget will share.
- Setting `Value` here gives the field a default appearance, which will also show up on the widget page.

## Step 4: How to Add Widget – Reference the Same Field on Another Page

A widget is essentially a visual placeholder that points back to the original field. By reusing the same rectangle, the widget looks identical to the field, but lives on a different page.

```csharp
// Step 4: Create a widget annotation on the second page that references the same field rectangle
var sharedWidget = new WidgetAnnotation(secondPage, sharedTextBox.Rect);
sharedWidget.PartialName = sharedTextBox.PartialName;
secondPage.Annotations.Add(sharedWidget);
```

> **Common pitfall:** Forgetting to add the widget to `secondPage.Annotations`. Without that line the widget never appears, even though the object exists.

## Step 5: Register the Field and Save PDF with Form

Now we tell the document’s form collection about our new field. The `Add` method takes the field instance and its name. Finally, we write the file to disk.

```csharp
// Step 5: Register the field with the document form
document.Form.Add(sharedTextBox, "MultiBox");

// Step 6: Save the PDF containing the multi‑page field
document.Save("YOUR_DIRECTORY/multibox.pdf");
```

When you open `multibox.pdf` in Adobe Acrobat or any PDF viewer that supports forms, you’ll see the same text box on both pages. Editing it on one page instantly updates the other because they share the same underlying field.

## Full Working Example

Putting everything together, here’s the complete, ready‑to‑run program:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Step 1: Create a new PDF document
        using (var document = new Document())
        {
            // Step 2: Add two pages – one for the field, one for the widget
            var firstPage = document.Pages.Add();
            var secondPage = document.Pages.Add();

            // Step 3: Create a text box field on the first page and give it a shared name and value
            var sharedTextBox = new TextBoxField(firstPage, new Rectangle(100, 600, 300, 620));
            sharedTextBox.PartialName = "MultiBox";
            sharedTextBox.Value = "Shared value";

            // Step 4: Create a widget annotation on the second page that references the same field rectangle
            var sharedWidget = new WidgetAnnotation(secondPage, sharedTextBox.Rect);
            sharedWidget.PartialName = sharedTextBox.PartialName;
            secondPage.Annotations.Add(sharedWidget);

            // Step 5: Register the field with the document form
            document.Form.Add(sharedTextBox, "MultiBox");

            // Step 6: Save the PDF containing the multi‑page field
            document.Save("multibox.pdf");
        }

        Console.WriteLine("PDF created successfully! Check the file 'multibox.pdf'.");
    }
}
```

### Expected Result

- **Two pages**: Page 1 shows a text box with the default text “Shared value”.  
- **Page 2** mirrors the same box. Typing in one updates the other instantly.  
- The file size is modest (a few kilobytes) because we only added simple form objects.

## Frequently Asked Questions & Edge Cases

### Can I add more than one widget for the same field?

Absolutely. Just repeat the widget creation step for each additional page, reusing the same `PartialName`. This is handy for multi‑page contracts where the same signature field appears at the bottom of each page.

### What if I need a different size or position on the second page?

You can create a new `Rectangle` for the widget while keeping the same `PartialName`. The field’s value will still sync, but the visual layout can differ per page.

### Does this work with password‑protected PDFs?

Yes, but you must open the document with the correct password first:

```csharp
var document = new Document("protected.pdf", "ownerPassword");
```

Then proceed with the same steps. The library will preserve encryption when you call `Save`.

### How do I retrieve the entered value programmatically?

After a user fills the form and you load the PDF again:

```csharp
var loaded = new Document("multibox.pdf");
var field = loaded.Form["MultiBox"] as TextBoxField;
Console.WriteLine("User entered: " + field.Value);
```

### What if I want to flatten the form (make fields non‑editable)?

Call `document.Form.Flatten()` before saving. This converts the interactive fields into static content, which can be useful for final invoices.

## Wrap‑Up

We’ve just **created PDF document C#** that spans multiple pages, added a reusable text box field, demonstrated **how to add widget** annotations, and finally **save PDF with form** data. The key takeaway is that a single field can be visualized on any number of pages through widgets, keeping user input consistent across the whole document.

Ready for the next challenge? Try:

- Adding a **checkbox** or **dropdown** using the same pattern.  
- Populating the PDF with data from a database instead of a hard‑coded value.  
- Exporting the filled PDF to a byte array for HTTP download in an ASP.NET Core API.

Feel free to experiment, break things, and then fix them—that’s how you truly master PDF generation in C#. If you run into hiccups, drop a comment below or check the library’s official docs for deeper nuances.

Happy coding, and enjoy building smarter PDFs!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}