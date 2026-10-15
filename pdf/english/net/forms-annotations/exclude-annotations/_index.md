---
title: Side‑by‑Side PDF Comparison Excluding Annotations with Aspose.Pdf for .NET
weight: 101
limit:
description: Step‑by‑step guide to compare PDFs and exclude annotation areas using Aspose.Pdf for .NET.
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Step‑by‑step guide to compare PDFs and exclude annotation areas using
    Aspose.Pdf for .NET.
  headline: Side‑by‑Side PDF Comparison Excluding Annotations with Aspose.Pdf for
    .NET
  type: TechArticle
- description: Step‑by‑step guide to compare PDFs and exclude annotation areas using
    Aspose.Pdf for .NET.
  name: Side‑by‑Side PDF Comparison Excluding Annotations with Aspose.Pdf for .NET
  steps:
  - name: Define the file paths for the primary PDF, the secondary PDF, and the output
      diff PDF.
    text: Define the file paths for the primary PDF, the secondary PDF, and the output
      diff PDF.
  - name: Check that both input PDF files exist and abort with an error message if
      either is missing.
    text: Check that both input PDF files exist and abort with an error message if
      either is missing.
  - name: Open the two PDF files as Document objects (pdfA and pdfB) within a using
      block so they are disposed automatically.
    text: Open the two PDF files as Document objects (pdfA and pdfB) within a using
      block so they are disposed automatically.
  - name: Collect the bounding rectangles of every annotation in pdfA and store them
      in ignoredRectsA.
    text: Collect the bounding rectangles of every annotation in pdfA and store them
      in ignoredRectsA.
  - name: Collect the bounding rectangles of every annotation in pdfB and store them
      in ignoredRectsB.
    text: Collect the bounding rectangles of every annotation in pdfB and store them
      in ignoredRectsB.
  - name: Create a SideBySideComparisonOptions object and assign the previously gathered
      annotation rectangles to ExcludeAreas1 and ExcludeAreas2 so those regions are
      ignored during comparison.
    text: Create a SideBySideComparisonOptions object and assign the previously gathered
      annotation rectangles to ExcludeAreas1 and ExcludeAreas2 so those regions are
      ignored during comparison.
  - name: Run the side‑by‑side PDF comparison using the two Document objects and the
      configured options, writing the result to outputPdf.
    text: Run the side‑by‑side PDF comparison using the two Document objects and the
      configured options, writing the result to outputPdf.
  - name: Dispose the Document objects and exit the using block.
    text: Dispose the Document objects and exit the using block.
  - name: Print a confirmation message indicating that the comparison is complete
      and where the diff PDF was saved.
    text: Print a confirmation message indicating that the comparison is complete
      and where the diff PDF was saved.
  type: HowTo
- questions:
  - answer: Yes. The code simply adds no rectangles to the corresponding `ignoredRects`
      list, so `ExcludeAreas1`/`ExcludeAreas2` receive an empty array and the comparer
      processes the whole page.
    question: What happens if a PDF page has no annotations – will the comparison
      still work?
  - answer: Set `ExcludeAreas1` (or `ExcludeAreas2`) to the collected rectangles and
      leave the other property as an empty array; the comparer will ignore regions
      only in the specified document.
    question: Can I exclude only annotations from one document while keeping the other's
      annotations in the diff?
  - answer: Overlapping rectangles are merged internally by the comparer, so overlapping
      annotation bounds are safely excluded without double‑counting.
    question: Do overlapping annotation rectangles cause any issues with `ExcludeAreas`?
  - answer: Yes, set `compareOpts.ExcludeTables = true;` – this flag works alongside
      `ExcludeAreas1`/`ExcludeAreas2` to ignore table regions as well.
    question: Is there a way to exclude tables in addition to annotations using the
      same options object?
  - answer: The code checks `if (a != null && a.Rect != null)` before adding to the
      list, so null rectangles are simply skipped and no exception is thrown.
    question: What if an annotation’s `Rect` property is null – will the code throw
      an exception?
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: Compare PDFs Without Annotations
og_description: Run a side‑by‑side PDF diff that skips all annotation marks.
og_image_alt: Guide showing a side‑by‑side PDF comparison that excludes annotation regions using Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Side‑by‑Side PDF Comparison Excluding Annotations with Aspose.Pdf
This tutorial shows how to compare two PDF files using Aspose.Pdf for .NET while ignoring any annotation content. It extracts the bounding boxes of all annotations from each document, feeds those regions into SideBySideComparisonOptions, and then runs a side‑by‑side comparison. The result is a diff PDF that highlights only the non‑annotation changes.

---

{{< tutorial-widget sourcePath="pdf/net/forms-annotations/exclude-annotations" >}}


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

**Q: What happens if a PDF page has no annotations – will the comparison still work?**  
A: Yes. The code simply adds no rectangles to the corresponding `ignoredRects` list, so `ExcludeAreas1`/`ExcludeAreas2` receive an empty array and the comparer processes the whole page.

**Q: Can I exclude only annotations from one document while keeping the other's annotations in the diff?**  
A: Set `ExcludeAreas1` (or `ExcludeAreas2`) to the collected rectangles and leave the other property as an empty array; the comparer will ignore regions only in the specified document.

**Q: Do overlapping annotation rectangles cause any issues with `ExcludeAreas`?**  
A: Overlapping rectangles are merged internally by the comparer, so overlapping annotation bounds are safely excluded without double‑counting.

**Q: Is there a way to exclude tables in addition to annotations using the same options object?**  
A: Yes, set `compareOpts.ExcludeTables = true;` – this flag works alongside `ExcludeAreas1`/`ExcludeAreas2` to ignore table regions as well.

**Q: What if an annotation’s `Rect` property is null – will the code throw an exception?**  
A: The code checks `if (a != null && a.Rect != null)` before adding to the list, so null rectangles are simply skipped and no exception is thrown.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}