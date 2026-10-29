---
title: 使用 Aspose.Pdf for .NET 在忽略特定区域的情况下比较 PDF
weight: 201
limit:
description: 学习使用 Aspose.Pdf for .NET 并排比较 PDF 并忽略选定区域。
keywords: [Aspose.Pdf for .NET, pdf comparison, exclude areas pdf, ignore regions pdf diff, side-by-side pdf comparison, pdf diff highlighting]
url: /net/document-manipulation/exclude-areas/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: 学习使用 Aspose.Pdf for .NET 并排比较 PDF 并忽略选定区域。
  headline: 使用 Aspose.Pdf for .NET 在忽略特定区域的情况下比较 PDF
  type: TechArticle
- description: 学习使用 Aspose.Pdf for .NET 并排比较 PDF 并忽略选定区域。
  name: 使用 Aspose.Pdf for .NET 在忽略特定区域的情况下比较 PDF
  steps:
  - name: 为两个源 PDF 和输出差异 PDF 定义文件路径。
    text: 为两个源 PDF 和输出差异 PDF 定义文件路径。
  - name: 检查两个源 PDF 文件是否存在，如果任一缺失则中止并显示错误信息。
    text: 检查两个源 PDF 文件是否存在，如果任一缺失则中止并显示错误信息。
  - name: 创建一个数组，包含要在第一个 PDF 中忽略的矩形区域。
    text: 创建一个数组，包含要在第一个 PDF 中忽略的矩形区域。
  - name: 创建一个数组，包含要在第二个 PDF 中忽略的矩形区域。
    text: 创建一个数组，包含要在第二个 PDF 中忽略的矩形区域。
  - name: 配置并排比较，将忽略区域数组分配给相应的属性。
    text: 配置并排比较，将忽略区域数组分配给相应的属性。
  - name: 加载两个 PDF 并运行并排比较，在指定路径生成差异文件。
    text: 加载两个 PDF 并运行并排比较，在指定路径生成差异文件。
  - name: 打印确认信息，指示比较已完成以及差异 PDF 保存的位置。
    text: 打印确认信息，指示比较已完成以及差异 PDF 保存的位置。
  type: HowTo
- questions:
  - answer: 坐标采用点（1/72 英寸）为单位，原点位于页面左下角，因此前两个数字是左下角的 X/Y，后两个数字是右上角的 X/Y。
    question: 在定义忽略区时，`Rectangle` 值使用的坐标系是什么？
  - answer: 可以——在 `ExcludeAreas1`（或 `ExcludeAreas2`）数组中提供多个 `Aspose.Pdf.Rectangle`
      对象；每个矩形将在比较过程中独立被排除。
    question: 我可以在同一文档中忽略多个矩形区域吗？
  - answer: 不。`ExcludeAreas1` 适用于第一个 PDF，`ExcludeAreas2` 适用于第二个，因此可以为每个文档指定不同的坐标。
    question: 忽略的矩形必须在两个 PDF 中完全相同吗？
  - answer: Aspose.Pdf 会静默地忽略完全位于页面之外的矩形；它们对比较结果没有影响。
    question: 如果矩形定义在页面边界之外会怎样？
  - answer: '`ExcludeAreas` 数组按页应用，因此需要将相同的 `Rectangle` 添加到每页的集合中（例如遍历 `pdf.Pages`
      并分配数组），然后再调用 `SideBySidePdfComparer.Compare`。'
    question: 如何在 PDF 的每一页上排除相同的区域？
  type: FAQPage
images:
- /net/document-manipulation/exclude-areas/og-image.png
og_title: 比较 PDF 时忽略区域
og_description: 了解如何在并排 PDF 比较中跳过选定区域并获得干净的差异 PDF。
og_image_alt: 使用 Aspose.Pdf for .NET 的并排 PDF 比较指南，支持排除矩形区域
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Pdf for .NET 在忽略特定区域的情况下比较 PDF
本教程演示了如何使用 Aspose.Pdf for .NET 对两个 PDF 文档进行并排比较，同时排除指定的矩形区域。通过在每个文件中定义排除区域，生成的差异 PDF 只突出显示重要的更改，便于聚焦相关差异。

---

{{< tutorial-widget sourcePath="pdf/net/document-manipulation/exclude-areas" >}}


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

**Q: 在定义忽略区时，`Rectangle` 值使用的坐标系是什么？**  
A: 坐标采用点（1/72 英寸）为单位，原点位于页面左下角，因此前两个数字是左下角的 X/Y，后两个数字是右上角的 X/Y。

**Q: 我可以在同一文档中忽略多个矩形区域吗？**  
A: 可以——在 `ExcludeAreas1`（或 `ExcludeAreas2`）数组中提供多个 `Aspose.Pdf.Rectangle` 对象；每个矩形将在比较过程中独立被排除。

**Q: 忽略的矩形必须在两个 PDF 中完全相同吗？**  
A: 不。`ExcludeAreas1` 适用于第一个 PDF，`ExcludeAreas2` 适用于第二个，因此可以为每个文档指定不同的坐标。

**Q: 如果矩形定义在页面边界之外会怎样？**  
A: Aspose.Pdf 会静默地忽略完全位于页面之外的矩形；它们对比较结果没有影响。

**Q: 如何在 PDF 的每一页上排除相同的区域？**  
A: `ExcludeAreas` 数组按页应用，因此需要将相同的 `Rectangle` 添加到每页的集合中（例如遍历 `pdf.Pages` 并分配数组），然后再调用 `SideBySidePdfComparer.Compare`。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}