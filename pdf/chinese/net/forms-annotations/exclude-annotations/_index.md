---
title: 使用 Aspose.Pdf for .NET 的并排 PDF 比较（排除批注）
weight: 101
limit:
description: 使用 Aspose.Pdf for .NET 对 PDF 进行比较并排除批注区域的分步指南。
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: 使用 Aspose.Pdf for .NET 对 PDF 进行比较并排除批注区域的分步指南。
  headline: 使用 Aspose.Pdf for .NET 的并排 PDF 比较（排除批注）
  type: TechArticle
- description: 使用 Aspose.Pdf for .NET 对 PDF 进行比较并排除批注区域的分步指南。
  name: 使用 Aspose.Pdf for .NET 的并排 PDF 比较（排除批注）
  steps:
  - name: 定义主 PDF、次要 PDF 和输出差异 PDF 的文件路径。
    text: 定义主 PDF、次要 PDF 和输出差异 PDF 的文件路径。
  - name: 检查两个输入 PDF 文件是否存在，如果任意一个缺失则中止并显示错误信息。
    text: 检查两个输入 PDF 文件是否存在，如果任意一个缺失则中止并显示错误信息。
  - name: 在 using 块中将两个 PDF 文件打开为 Document 对象（pdfA 和 pdfB），以便自动释放资源。
    text: 在 using 块中将两个 PDF 文件打开为 Document 对象（pdfA 和 pdfB），以便自动释放资源。
  - name: 收集 pdfA 中每个批注的边界矩形，并将其存入 ignoredRectsA。
    text: 收集 pdfA 中每个批注的边界矩形，并将其存入 ignoredRectsA。
  - name: 收集 pdfB 中每个批注的边界矩形，并将其存入 ignoredRectsB。
    text: 收集 pdfB 中每个批注的边界矩形，并将其存入 ignoredRectsB。
  - name: 创建 SideBySideComparisonOptions 对象，并将先前收集的批注矩形分别赋给 ExcludeAreas1 和 ExcludeAreas2，以便在比较时忽略这些区域。
    text: 创建 SideBySideComparisonOptions 对象，并将先前收集的批注矩形分别赋给 ExcludeAreas1 和 ExcludeAreas2，以便在比较时忽略这些区域。
  - name: 使用这两个 Document 对象和已配置的选项运行并排 PDF 比较，并将结果写入 outputPdf。
    text: 使用这两个 Document 对象和已配置的选项运行并排 PDF 比较，并将结果写入 outputPdf。
  - name: 释放 Document 对象并退出 using 块。
    text: 释放 Document 对象并退出 using 块。
  - name: 打印确认信息，指示比较已完成以及差异 PDF 保存的位置。
    text: 打印确认信息，指示比较已完成以及差异 PDF 保存的位置。
  type: HowTo
- questions:
  - answer: 是的。代码仅不向相应的 `ignoredRects` 列表添加矩形，因此 `ExcludeAreas1`/`ExcludeAreas2` 会收到空数组，比较器会处理整页。
    question: 如果 PDF 页面没有批注会怎样——比较仍然会工作吗？
  - answer: 将 `ExcludeAreas1`（或 `ExcludeAreas2`）设置为收集的矩形，并将另一个属性保持为空数组；比较器只会忽略指定文档中的区域。
    question: 我能只排除一个文档的批注，而在差异中保留另一个文档的批注吗？
  - answer: 比较器会在内部合并重叠的矩形，因此重叠的批注边界会安全地被排除，不会出现重复计数。
    question: 重叠的批注矩形会对 `ExcludeAreas` 产生任何问题吗？
  - answer: 是的，设置 `compareOpts.ExcludeTables = true;`——此标志与 `ExcludeAreas1`/`ExcludeAreas2`
      一起工作，以同样方式排除表格区域。
    question: 是否可以使用同一个选项对象在排除批注的同时排除表格？
  - answer: 代码在添加之前会检查 `if (a != null && a.Rect != null)`，因此会直接跳过空矩形，不会抛出异常。
    question: 如果批注的 `Rect` 属性为 null 会怎样——代码会抛出异常吗？
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: 比较不含批注的 PDF
og_description: 运行并排 PDF 差异比较，跳过所有批注标记。
og_image_alt: 展示使用 Aspose.Pdf for .NET 排除批注区域的并排 PDF 比较的指南
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Pdf for .NET 的并排 PDF 比较（排除批注）
本教程展示了如何使用 Aspose.Pdf for .NET 对两个 PDF 文件进行比较，同时忽略所有批注内容。它从每个文档中提取所有批注的边界框，将这些区域传入 SideBySideComparisonOptions，然后运行并排比较。结果是一个仅突出显示非批注更改的差异 PDF。

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

**Q: 如果 PDF 页面没有批注会怎样——比较仍然会工作吗？**  
A: 是的。代码仅不向相应的 `ignoredRects` 列表添加矩形，因此 `ExcludeAreas1`/`ExcludeAreas2` 会收到空数组，比较器会处理整页。

**Q: 我能只排除一个文档的批注，而在差异中保留另一个文档的批注吗？**  
A: 将 `ExcludeAreas1`（或 `ExcludeAreas2`）设置为收集的矩形，并将另一个属性保持为空数组；比较器只会忽略指定文档中的区域。

**Q: 重叠的批注矩形会对 `ExcludeAreas` 产生任何问题吗？**  
A: 比较器会在内部合并重叠的矩形，因此重叠的批注边界会安全地被排除，不会出现重复计数。

**Q: 是否可以使用同一个选项对象在排除批注的同时排除表格？**  
A: 是的，设置 `compareOpts.ExcludeTables = true;`——此标志与 `ExcludeAreas1`/`ExcludeAreas2` 一起工作，以同样方式排除表格区域。

**Q: 如果批注的 `Rect` 属性为 null 会怎样——代码会抛出异常吗？**  
A: 代码在添加之前会检查 `if (a != null && a.Rect != null)`，因此会直接跳过空矩形，不会抛出异常。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}