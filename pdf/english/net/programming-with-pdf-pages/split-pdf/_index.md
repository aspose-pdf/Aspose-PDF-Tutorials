---
title: Split PDF After Page Ten Using Aspose.Pdf for .NET
weight: 360
limit:
description: Step‑by‑step code to split a PDF document right after the tenth page with Aspose.Pdf for .NET.
keywords: [pdf split, Aspose.Pdf for .NET, split PDF after page, extract pages from PDF, c# pdf split, pdf pagination]
url: /net/programming-with-pdf-pages/split-pdf/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Step‑by‑step code to split a PDF document right after the tenth page
    with Aspose.Pdf for .NET.
  headline: Split PDF After Page Ten Using Aspose.Pdf for .NET
  type: TechArticle
- description: Step‑by‑step code to split a PDF document right after the tenth page
    with Aspose.Pdf for .NET.
  name: Split PDF After Page Ten Using Aspose.Pdf for .NET
  steps:
  - name: The header comments explain the purpose of the example, note that the full
      code has been moved, and provide a link to the up‑to‑date source.
    text: The header comments explain the purpose of the example, note that the full
      code has been moved, and provide a link to the up‑to‑date source.
  - name: The stub line performs no action and exists only to keep the original URL
      functional.
    text: The stub line performs no action and exists only to keep the original URL
      functional.
  type: HowTo
- questions:
  - answer: Aspose.Pdf will not throw an error; the `Split` method will simply return
      the original document unchanged because there is no page after the tenth to
      start a new part.
    question: What happens if the source PDF has fewer than ten pages?
  - answer: You call `PdfDocument.Split(pageNumber)` on a `PdfDocument` instance,
      passing `10` as the `pageNumber` to create two separate documents.
    question: Which class and method are used to split the PDF at page ten?
  - answer: Yes, Aspose.Pdf preserves all page‑level objects (bookmarks, annotations,
      form fields, etc.) in the resulting split documents, keeping them attached to
      the pages they originated from.
    question: Do bookmarks, annotations, and form fields stay with their original
      pages after the split?
  - answer: After calling `Split`, you receive two `PdfDocument` objects; you must
      call `Save("FirstPart.pdf")` on the first and `Save("SecondPart.pdf")` on the
      second, providing distinct file names yourself.
    question: How should I name the output files for the two parts created by the
      split?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/split-pdf/og-image.png
og_title: Split PDF after page 10
og_description: Quick tutorial to split a PDF at page 10 using Aspose.Pdf for .NET.
og_image_alt: Guide showing how to split a PDF after the tenth page using Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Split PDF After Page Ten Using Aspose.Pdf
Splitting a PDF into separate documents can simplify distribution and processing. This tutorial walks you through using Aspose.Pdf for .NET to split a PDF right after the tenth page, creating two distinct files. Follow the step‑by‑step code to extract the first ten pages and the remaining pages with just a few lines of C#.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/split-pdf" >}}


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

**Q: What happens if the source PDF has fewer than ten pages?**  
A: Aspose.Pdf will not throw an error; the `Split` method will simply return the original document unchanged because there is no page after the tenth to start a new part.

**Q: Which class and method are used to split the PDF at page ten?**  
A: You call `PdfDocument.Split(pageNumber)` on a `PdfDocument` instance, passing `10` as the `pageNumber` to create two separate documents.

**Q: Do bookmarks, annotations, and form fields stay with their original pages after the split?**  
A: Yes, Aspose.Pdf preserves all page‑level objects (bookmarks, annotations, form fields, etc.) in the resulting split documents, keeping them attached to the pages they originated from.

**Q: How should I name the output files for the two parts created by the split?**  
A: After calling `Split`, you receive two `PdfDocument` objects; you must call `Save("FirstPart.pdf")` on the first and `Save("SecondPart.pdf")` on the second, providing distinct file names yourself.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}