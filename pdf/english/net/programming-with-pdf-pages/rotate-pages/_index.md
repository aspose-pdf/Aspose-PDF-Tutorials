---
title: Rotate Every PDF Page 180° Using Aspose.Pdf for .NET
weight: 260
limit:
description: Step‑by‑step guide to rotate all pages of a PDF 180 degrees with Aspose.Pdf for .NET.
keywords: [rotate pdf pages .net, Aspose.Pdf for .NET, rotate all pages 180 degrees, pdf page rotation, c# pdf manipulation]
url: /net/programming-with-pdf-pages/rotate-pages/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Step‑by‑step guide to rotate all pages of a PDF 180 degrees with Aspose.Pdf
    for .NET.
  headline: Rotate Every PDF Page 180° Using Aspose.Pdf for .NET
  type: TechArticle
- description: Step‑by‑step guide to rotate all pages of a PDF 180 degrees with Aspose.Pdf
    for .NET.
  name: Rotate Every PDF Page 180° Using Aspose.Pdf for .NET
  steps:
  - name: Declare the source and destination file paths for the PDF.
    text: Declare the source and destination file paths for the PDF.
  - name: Check that the source file exists and abort with an error message if it
      does not.
    text: Check that the source file exists and abort with an error message if it
      does not.
  - name: Create a Document object for the source PDF inside a using block to manage
      resources.
    text: Create a Document object for the source PDF inside a using block to manage
      resources.
  - name: Iterate through each Page in pdfDoc.Pages and set its Rotate property to
      Rotation.on180, turning every page upside‑down.
    text: Iterate through each Page in pdfDoc.Pages and set its Rotate property to
      Rotation.on180, turning every page upside‑down.
  - name: Save the modified Document to the destination file, persisting the rotations.
    text: Save the modified Document to the destination file, persisting the rotations.
  - name: Write a confirmation message to the console indicating the operation completed.
    text: Write a confirmation message to the console indicating the operation completed.
  type: HowTo
- questions:
  - answer: The code checks `File.Exists(sourceFile)` and writes an error to `Console.Error`
      before returning, so no exception is thrown and the program exits gracefully.
    question: What happens if the source PDF file does not exist?
  - answer: Yes, replace `Rotation.on180` with another enum value such as `Rotation.on90`
      (clockwise) or `Rotation.on270` (counter‑clockwise) to apply a different rotation.
    question: Can I rotate the pages by a different angle, e.g., 90° clockwise?
  - answer: Aspose.Pdf’s `Pages` collection is 1‑based, but the `foreach` iterator
      abstracts that away, iterating over each `Page` object regardless of the underlying
      index.
    question: Is the page collection zero‑based? How does the `foreach` loop work?
  - answer: Calling `pdfDoc.Save(destinationFile)` will overwrite any existing file
      with that name, so use a different filename or back up the original if you need
      to keep it.
    question: Will the original PDF be overwritten if I use the same filename for
      `destinationFile`?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/rotate-pages/og-image.png
og_title: Rotate Every PDF Page 180°
og_description: Learn how to flip all pages of a PDF upside‑down in just a few lines of C# code.
og_image_alt: Guide showing how to rotate every page of a PDF by 180 degrees using Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Rotate Every PDF Page 180° Using Aspose.Pdf
This tutorial shows how to rotate each page of an existing PDF document by 180 degrees with the Aspose.Pdf Document class. By applying a full‑page rotation you can quickly correct upside‑down scans or re‑orient documents without recreating them. The example is written in C# and works on the .NET platform.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/rotate-pages" >}}


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

**Q: What happens if the source PDF file does not exist?**  
A: The code checks `File.Exists(sourceFile)` and writes an error to `Console.Error` before returning, so no exception is thrown and the program exits gracefully.

**Q: Can I rotate the pages by a different angle, e.g., 90° clockwise?**  
A: Yes, replace `Rotation.on180` with another enum value such as `Rotation.on90` (clockwise) or `Rotation.on270` (counter‑clockwise) to apply a different rotation.

**Q: Is the page collection zero‑based? How does the `foreach` loop work?**  
A: Aspose.Pdf’s `Pages` collection is 1‑based, but the `foreach` iterator abstracts that away, iterating over each `Page` object regardless of the underlying index.

**Q: Will the original PDF be overwritten if I use the same filename for `destinationFile`?**  
A: Calling `pdfDoc.Save(destinationFile)` will overwrite any existing file with that name, so use a different filename or back up the original if you need to keep it.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}