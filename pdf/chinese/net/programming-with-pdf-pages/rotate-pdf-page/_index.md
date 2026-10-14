---
title: 使用 Aspose.PDF for .NET 将单个 PDF 页面旋转 180 度
weight: 260
limit:
description: 了解如何使用 Aspose.PDF for .NET 将 PDF 的第三页旋转 180°。
keywords: [rotate pdf page, Aspose.PDF for .NET, PDF page rotation .NET, rotate third page pdf, PDF SDK rotate page]
url: /net/programming-with-pdf-pages/rotate-pdf-page/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: 了解如何使用 Aspose.PDF for .NET 将 PDF 的第三页旋转 180°。
  headline: 使用 Aspose.PDF for .NET 将单个 PDF 页面旋转 180 度
  type: TechArticle
- description: 了解如何使用 Aspose.PDF for .NET 将 PDF 的第三页旋转 180°。
  name: 使用 Aspose.PDF for .NET 将单个 PDF 页面旋转 180 度
  steps:
  - name: 该文件仅包含说明性注释，没有可执行代码，用作原始示例的占位符。
    text: 该文件仅包含说明性注释，没有可执行代码，用作原始示例的占位符。
  type: HowTo
- questions:
  - answer: 使用 SDK 的页面集合并采用从零开始的索引，例如 `pdfDocument.Pages[2]`，因为索引 2 对应第三页。
    question: 如何定位 PDF 的第三页进行旋转？
  - answer: rotation 属性仅接受四个标准值 0、90、180 和 270 度；任何其他值都会四舍五入为最近的允许角度。
    question: 我可以将页面旋转为除 180 度以外的角度吗？
  - answer: 旋转仅作用于内存中的 `PdfDocument`；您必须调用 `pdfDocument.Save("output.pdf")`（或类似的保存方法）将更改写入新文件，原文件保持不变。
    question: 旋转页面会自动修改原始文件吗？
  - answer: SDK 会自动重新计算注释和表单字段的位置，使其在新方向下保持正确对齐。
    question: 页面旋转后，注释或表单字段会怎样？
  type: FAQPage
images:
- /net/programming-with-pdf-pages/rotate-pdf-page/og-image.png
og_title: 使用 Aspose.PDF 将 PDF 页面旋转 180°
og_description: 只需几行 Aspose.PDF for .NET 代码，即可快速将 PDF 的第三页倒置翻转。
og_image_alt: 指南展示了使用 Aspose.PDF for .NET 将 PDF 的第三页旋转 180 度的代码。
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.PDF for .NET 将单个 PDF 页面旋转 180 度
在本教程中，您将学习如何使用 Aspose.PDF for .NET 将 PDF 文档的第三页旋转 180 度。示例演示了加载 PDF、选择第 3 页、应用旋转并保存更新后的文件的过程。此方法可让您翻转特定页面，而不影响其余页面的方向。

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

**Q: 如何定位 PDF 的第三页进行旋转？**  
A: 使用 SDK 的页面集合并采用从零开始的索引，例如 `pdfDocument.Pages[2]`，因为索引 2 对应第三页。

**Q: 我可以将页面旋转为除 180 度以外的角度吗？**  
A: rotation 属性仅接受四个标准值 0、90、180 和 270 度；任何其他值都会四舍五入为最近的允许角度。

**Q: 旋转页面会自动修改原始文件吗？**  
A: 旋转仅作用于内存中的 `PdfDocument`；您必须调用 `pdfDocument.Save("output.pdf")`（或类似的保存方法）将更改写入新文件，原文件保持不变。

**Q: 页面旋转后，注释或表单字段会怎样？**  
A: SDK 会自动重新计算注释和表单字段的位置，使其在新方向下保持正确对齐。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}