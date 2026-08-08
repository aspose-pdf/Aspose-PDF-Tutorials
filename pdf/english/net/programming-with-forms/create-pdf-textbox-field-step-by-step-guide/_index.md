---
category: general
date: 2026-06-21
description: Create PDF textbox field with C# and learn how to duplicate PDF form
  field or add textbox to PDF form in just a few lines of code.
draft: false
keywords:
- create pdf textbox field
- duplicate pdf form field
- add textbox to pdf form
- pdf form automation
- c# pdf library
language: en
og_description: Create PDF textbox field quickly. This guide shows how to duplicate
  PDF form field and add textbox to PDF form using a modern C# PDF library.
og_title: Create PDF Textbox Field – Complete C# Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  headline: Create PDF Textbox Field – Step‑by‑Step Guide
  type: TechArticle
- description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  name: Create PDF Textbox Field – Step‑by‑Step Guide
  steps:
  - name: What if I need the field on *more* than two pages?
    text: Just repeat the clone‑and‑add steps for each additional page. The underlying
      data object stays the same, so all widgets stay in sync.
  - name: How do I change the appearance (font, border, background)?
    text: Each `Widget` has a `SetBorderColor`, `SetBorderWidth`, and `SetBackgroundColor`
      method. You can also assign a default appearance string (`DA`) to control the
      font and size.
  - name: Can I make the field read‑only after the user fills it?
    text: Yes. Set the `ReadOnly` flag on the field after you’ve collected the data,
      or toggle it based on your workflow.
  - name: What about PDFs that already contain a form?
    text: If the document already has an AcroForm, `doc.GetForm()` simply returns
      it. You can then add new fields without disturbing existing ones. Just be careful
      to use unique field names.
  type: HowTo
tags:
- PDF
- C#
- FormFields
title: Create PDF Textbox Field – Step‑by‑Step Guide
url: /net/programming-with-forms/create-pdf-textbox-field-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create PDF Textbox Field – Complete C# Tutorial

Ever needed to **create PDF textbox field** but weren’t sure which API calls to use? You’re not alone. Whether you’re building a contract‑signing portal or a simple data‑capture sheet, adding interactive text boxes to a PDF is a core skill for any form‑automation developer.  

In this guide we’ll walk through a practical example that not only **adds textbox to PDF form**, but also shows how to **duplicate PDF form field** so the same input appears on multiple pages. By the end you’ll have a runnable program you can drop into any .NET project.

## What You’ll Need

- .NET 6.0 or later (the code works with .NET Core as well)  
- A modern C# PDF library – the snippet below uses **PDFTron SDK**, but the concepts translate to iText 7, PdfSharp, or other libraries.  
- Visual Studio 2022 (or any IDE you like)  

That’s it – no extra services, no obscure dependencies. If you already have a PDF you want to augment, just point the code at it.

---

## Step 1: Set Up the Project and Import the SDK

First, create a console app:

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
```

Add the PDFTron NuGet package:

```bash
dotnet add package PDFTron.NET
```

Now open `Program.cs` and pull in the namespaces we’ll need:

```csharp
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;
```

> **Pro tip:** If you’re using a different library, replace the `using` statements with the equivalents (e.g., `iText.Kernel.Pdf` for iText 7).

## Step 2: Initialize the PDF Document and Form

We’ll start with a fresh PDF that contains two pages – the source page for the original textbox and a target page for the duplicate.

```csharp
PDFNet.Initialize();                     // Initialize the PDFTron runtime

// Create a new PDF document
using (PDFDoc doc = new PDFDoc())
{
    // Add two blank pages (letter size)
    Page sourcePage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(sourcePage);
    Page targetPage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(targetPage);

    // Get (or create) the AcroForm object
    Form form = doc.GetForm();
```

The `Form` object is where all interactive fields live. If the document didn’t have a form already, `GetForm()` creates one for us.

## Step 3: **Create PDF Textbox Field** on the First Page

Now comes the core of our tutorial – creating a textbox field. The rectangle coordinates are expressed in points (1 inch = 72 points). The example places the box near the top‑center of the first page.

```csharp
    // Step 1: Create a text box field on the first page and set its initial value
    TextBoxField textBoxField = new TextBoxField(sourcePage, new Rect(100, 500, 300, 520))
    {
        Value = "Sample"
    };
```

Why do we set `Value` right away? Pre‑populating the field gives users a hint about the expected input, and it also demonstrates that the field is fully functional.

## Step 4: Add the Field to the Form – **Add Textbox to PDF Form**

Next, we register the field with the form using a logical name. This name is what you’ll reference later when you need to read or modify the field’s data programmatically.

```csharp
    // Step 2: Add the field to the form with a logical name
    form.Add(textBoxField, "multiBox");
```

Choosing a clear name (like `"multiBox"`) makes later code easier to understand, especially when you have dozens of fields.

## Step 5: **Duplicate PDF Form Field** on Another Page

A common requirement is to show the same field on multiple pages – think of a “Customer Name” box that appears on every invoice page. PDFTron lets us clone the widget annotation, which is the visual representation of the field.

```csharp
    // Step 3: Clone the field's widget annotation so it can appear on another page
    Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

    // Step 4: Place the cloned widget on the second page
    targetPage.Annotations.Add(clonedWidget);
```

The cloned widget shares the same underlying data as the original textbox. When a user types into one instance, the other updates automatically – that’s the magic of **duplicate PDF form field**.

## Step 6: Save the Document and Clean Up

Finally, write the PDF to disk and shut down the PDFNet runtime.

```csharp
    // Save the resulting PDF
    doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
    Console.WriteLine("PDF created: output.pdf");
}

// Shut down PDFNet (optional but good practice)
PDFNet.Terminate();
```

Running the program produces a two‑page PDF (`output.pdf`). Open it in Adobe Acrobat Reader, click the textbox on page 1, type something, then switch to page 2 – the same text appears instantly. That’s a fully functional **create pdf textbox field** example with a duplicated field.

---

## Full Working Example (Copy‑Paste Ready)

```csharp
// Program.cs
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;

class Program
{
    static void Main()
    {
        PDFNet.Initialize();

        using (PDFDoc doc = new PDFDoc())
        {
            // Create two pages
            Page sourcePage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(sourcePage);
            Page targetPage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(targetPage);

            // Get the form (creates one if missing)
            Form form = doc.GetForm();

            // Step 1: Create a text box field on the first page
            TextBoxField textBoxField = new TextBoxField(sourcePage,
                new Rect(100, 500, 300, 520))
            {
                Value = "Sample"
            };

            // Step 2: Add the field to the form
            form.Add(textBoxField, "multiBox");

            // Step 3: Clone the widget so it appears on page 2
            Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

            // Step 4: Attach the cloned widget to the second page
            targetPage.Annotations.Add(clonedWidget);

            // Save the file
            doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
            Console.WriteLine("PDF created: output.pdf");
        }

        PDFNet.Terminate();
    }
}
```

**Expected output:** A file named `output.pdf` containing two pages. Both pages display the same editable textbox labeled “Sample”. Editing one updates the other instantly.

---

## Common Questions & Edge Cases

### What if I need the field on *more* than two pages?

Just repeat the clone‑and‑add steps for each additional page. The underlying data object stays the same, so all widgets stay in sync.

```csharp
Widget anotherClone = textBoxField.CreateWidgetAnnotation();
thirdPage.Annotations.Add(anotherClone);
```

### How do I change the appearance (font, border, background)?

Each `Widget` has a `SetBorderColor`, `SetBorderWidth`, and `SetBackgroundColor` method. You can also assign a default appearance string (`DA`) to control the font and size.

```csharp
textBoxField.SetBorderColor(new ColorPt(0, 0, 1), 3); // blue border
textBoxField.SetBackgroundColor(new ColorPt(0.9, 0.9, 0.9), 3); // light gray fill
textBoxField.SetDefaultAppearance("Helvetica 12 Tf 0 g");
```

### Can I make the field read‑only after the user fills it?

Yes. Set the `ReadOnly` flag on the field after you’ve collected the data, or toggle it based on your workflow.

```csharp
textBoxField.SetFlag(Field.Flag.e_readonly, true);
```

### What about PDFs that already contain a form?

If the document already has an AcroForm, `doc.GetForm()` simply returns it. You can then add new fields without disturbing existing ones. Just be careful to use unique field names.

---

## Tips for Real‑World Projects

- **Naming convention:** Prefix field names with the page or section (e.g., `invoice_customer_name`) to avoid collisions.  
- **Validation:** Use JavaScript actions (`field.SetAction(Field.Action.e_keystroke, "event.rc = /^[A-Za-z]+$/.test(event.change);")`) if you need client‑side validation.  
- **Performance:** When working with large PDFs, call `doc.Lock()` before bulk operations to reduce I/O overhead.  
- **Accessibility:** Set the `AlternateName` property so screen readers can describe the field.

---

## Conclusion

We’ve just **created a PDF textbox field**, shown how to **duplicate PDF form field** across pages, and demonstrated the simplest way to **add textbox to PDF form** using C#. The full, runnable code lives above, and you can extend it with styling, validation, or additional pages as needed.

Ready for the next step? Try embedding a dropdown (`ChoiceField`) or a signature widget, or explore how to flatten the form after data entry for archival purposes. The PDFTron SDK (or any comparable library) gives you the building blocks—your imagination decides the final shape.

If you hit a snag, drop a comment below or check the library’s official docs; they’re packed with examples that complement what we covered here. Happy coding, and may your forms always stay in sync!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create PDF with Aspose – Add Form Field and Pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Add Form Field in PDF Document using Java](/pdf/english/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)
- [Add Form Field In Pdf Document Using Java](/pdf/german/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}