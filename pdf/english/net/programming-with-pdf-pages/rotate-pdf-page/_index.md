---
title: Rotate a Single PDF Page 180 Degrees with Aspose.PDF for .NET
weight: 260
limit:
description: Learn how to rotate the third page of a PDF 180° using Aspose.PDF for .NET.
keywords: [rotate pdf page, Aspose.PDF for .NET, PDF page rotation .NET, rotate third page pdf, PDF SDK rotate page]
url: /net/programming-with-pdf-pages/rotate-pdf-page/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Learn how to rotate the third page of a PDF 180° using Aspose.PDF for
    .NET.
  headline: Rotate a Single PDF Page 180 Degrees with Aspose.PDF for .NET
  type: TechArticle
- description: Learn how to rotate the third page of a PDF 180° using Aspose.PDF for
    .NET.
  name: Rotate a Single PDF Page 180 Degrees with Aspose.PDF for .NET
  steps:
  - name: The file contains only explanatory comments and no executable code, serving
      as a placeholder for the original example.
    text: The file contains only explanatory comments and no executable code, serving
      as a placeholder for the original example.
  type: HowTo
- questions:
  - answer: Use the SDK’s page collection with zero‑based indexing, e.g., `pdfDocument.Pages[2]`,
      because index 2 corresponds to the third page.
    question: How do I target the third page of the PDF for rotation?
  - answer: The rotation property only accepts the four standard values 0, 90, 180,
      and 270 degrees; any other value is rounded to the nearest allowed angle.
    question: Can I rotate a page by an angle other than 180 degrees?
  - answer: The rotation is applied only to the in‑memory `PdfDocument`; you must
      call `pdfDocument.Save("output.pdf")` (or a similar save method) to write the
      changes to a new file, leaving the source unchanged.
    question: Does rotating the page modify the original file automatically?
  - answer: The SDK automatically recalculates the positions of annotations and form
      fields so they stay correctly aligned with the new orientation.
    question: What happens to annotations or form fields after the page is rotated?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/rotate-pdf-page/og-image.png
og_title: Rotate a PDF Page 180° with Aspose.PDF
og_description: Quickly flip the third page of your PDF upside‑down with a few lines of Aspose.PDF for .NET code.
og_image_alt: Guide showing code that rotates the third page of a PDF 180 degrees using Aspose.PDF for .NET.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Rotate a Single PDF Page 180 Degrees with Aspose.PDF
In this tutorial you’ll learn how to rotate the third page of a PDF document by 180 degrees using Aspose.PDF for .NET. The example walks through loading a PDF, selecting page 3, applying the rotation, and saving the updated file. This approach lets you flip a specific page without altering the orientation of the remaining pages.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/rotate-pdf-page" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: How do I target the third page of the PDF for rotation?**  
A: Use the SDK’s page collection with zero‑based indexing, e.g., `pdfDocument.Pages[2]`, because index 2 corresponds to the third page.

**Q: Can I rotate a page by an angle other than 180 degrees?**  
A: The rotation property only accepts the four standard values 0, 90, 180, and 270 degrees; any other value is rounded to the nearest allowed angle.

**Q: Does rotating the page modify the original file automatically?**  
A: The rotation is applied only to the in‑memory `PdfDocument`; you must call `pdfDocument.Save("output.pdf")` (or a similar save method) to write the changes to a new file, leaving the source unchanged.

**Q: What happens to annotations or form fields after the page is rotated?**  
A: The SDK automatically recalculates the positions of annotations and form fields so they stay correctly aligned with the new orientation.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}