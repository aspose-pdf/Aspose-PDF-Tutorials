---
title: 使用 Aspose.Pdf for .NET 在第十页后拆分 PDF
weight: 360
limit:
description: 使用 Aspose.Pdf for .NET 在第十页后拆分 PDF 文档的逐步代码示例。
keywords: [pdf split, Aspose.Pdf for .NET, split PDF after page, extract pages from PDF, c# pdf split, pdf pagination]
url: /net/programming-with-pdf-pages/split-pdf/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: 使用 Aspose.Pdf for .NET 在第十页后拆分 PDF 文档的逐步代码示例。
  headline: 使用 Aspose.Pdf for .NET 在第十页后拆分 PDF
  type: TechArticle
- description: 使用 Aspose.Pdf for .NET 在第十页后拆分 PDF 文档的逐步代码示例。
  name: 使用 Aspose.Pdf for .NET 在第十页后拆分 PDF
  steps:
  - name: 头部注释说明了示例的目的，指出完整代码已被移至其他位置，并提供了指向最新源代码的链接。
    text: 头部注释说明了示例的目的，指出完整代码已被移至其他位置，并提供了指向最新源代码的链接。
  - name: 此存根行不执行任何操作，仅用于保持原始 URL 的可用性。
    text: 此存根行不执行任何操作，仅用于保持原始 URL 的可用性。
  type: HowTo
- questions:
  - answer: Aspose.Pdf 不会抛出错误；`Split` 方法只会返回原始文档且保持不变，因为第十页之后没有页面可用于开始新部分。
    question: 如果源 PDF 少于十页会怎样？
  - answer: 在 `PdfDocument` 实例上调用 `PdfDocument.Split(pageNumber)`，并将 `10` 作为 `pageNumber`
      传入，以创建两个独立的文档。
    question: 使用哪个类和方法在第十页拆分 PDF？
  - answer: 是的，Aspose.Pdf 会在拆分后的文档中保留所有页面级对象（书签、注释、表单字段等），并保持它们附着在原始所在的页面上。
    question: 拆分后，书签、注释和表单字段会保持在原始页面上吗？
  - answer: 调用 `Split` 后会得到两个 `PdfDocument` 对象；您需要在第一个对象上调用 `Save("FirstPart.pdf")`，在第二个对象上调用
      `Save("SecondPart.pdf")`，自行提供不同的文件名。
    question: 拆分后生成的两个部分的输出文件应如何命名？
  type: FAQPage
images:
- /net/programming-with-pdf-pages/split-pdf/og-image.png
og_title: 在第10页后拆分 PDF
og_description: 使用 Aspose.Pdf for .NET 在第10页拆分 PDF 的快速教程。
og_image_alt: 展示如何使用 Aspose.Pdf for .NET 在第十页后拆分 PDF 的指南
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Pdf for .NET 在第十页后拆分 PDF
将 PDF 拆分为多个文档可以简化分发和处理。本教程指导您使用 Aspose.Pdf for .NET 在第十页后拆分 PDF，生成两个独立文件。按照逐步代码，仅用几行 C# 即可提取前十页和其余页面。

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

**Q: 如果源 PDF 少于十页会怎样？**  
A: Aspose.Pdf 不会抛出错误；`Split` 方法只会返回原始文档且保持不变，因为第十页之后没有页面可用于开始新部分。

**Q: 使用哪个类和方法在第十页拆分 PDF？**  
A: 在 `PdfDocument` 实例上调用 `PdfDocument.Split(pageNumber)`，并将 `10` 作为 `pageNumber` 传入，以创建两个独立的文档。

**Q: 拆分后，书签、注释和表单字段会保持在原始页面上吗？**  
A: 是的，Aspose.Pdf 会在拆分后的文档中保留所有页面级对象（书签、注释、表单字段等），并保持它们附着在原始所在的页面上。

**Q: 拆分后生成的两个部分的输出文件应如何命名？**  
A: 调用 `Split` 后会得到两个 `PdfDocument` 对象；您需要在第一个对象上调用 `Save("FirstPart.pdf")`，在第二个对象上调用 `Save("SecondPart.pdf")`，自行提供不同的文件名。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}