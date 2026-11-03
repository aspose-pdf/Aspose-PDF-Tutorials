---
category: general
date: 2026-10-10
description: 了解如何使用 Aspose.PDF 向 PDF 添加矩形、在 PDF 上绘制形状并保存修改后的 PDF。包括逐步指南，帮助访问特定的 PDF
  页面。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to PDF
- draw shape on PDF
- save modified PDF
- add shape to PDF
- access specific PDF page
language: zh
lastmod: 2026-10-10
og_description: 使用 Aspose.PDF 在 C# 中向 PDF 添加矩形。本教程展示了如何在 PDF 上绘制形状、访问特定的 PDF 页面以及保存修改后的
  PDF。
og_image_alt: Screenshot of a PDF page with a blue rectangle overlay created by Aspose.PDF
og_title: 使用 Aspose.PDF 向 PDF 添加矩形 – 完整 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  headline: How to add rectangle to PDF with Aspose.PDF in C#
  type: TechArticle
- description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  name: How to add rectangle to PDF with Aspose.PDF in C#
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: What if the PDF has only one page?
    text: Attempting to access `pdfDocument.Pages[1]` throws an `ArgumentOutOfRangeException`.
      Guard against this by checking `pdfDocument.Pages.Count` before indexing.
  - name: How to add multiple rectangles on different pages?
    text: Repeat Steps 2‑4 for each target page, adjusting the rectangle’s coordinates
      as needed. You can place the logic inside a loop that iterates over `pdfDocument.Pages`.
  - name: Can I use other shapes such as circles or polygons?
    text: Yes. Aspose.PDF provides `Ellipse`, `Polygon`, and `Polyline` classes that
      follow the same pattern as `Rectangle`. Replace the `new Aspose.Pdf.Drawing.Rectangle`
      call with the desired shape class.
  - name: Does the library support PDFs with rotated pages?
    text: Aspose.PDF automatically respects page rotation when rendering shapes. The
      rectangle’s coordinates are interpreted in the page’s native coordinate system,
      so no extra transformation is required.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: 如何在 C# 中使用 Aspose.PDF 向 PDF 添加矩形
url: /zh/net/images-graphics/how-to-add-rectangle-to-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.PDF 向 PDF 添加矩形

如果您需要 **向 PDF 添加矩形**，本指南将手把手教您实现。您将学习 **在 PDF 上绘制形状**、定位特定页面以及 **安全保存修改后的 PDF**。

在报告、发票或文档批注等场景中，处理 PDF 文档是常见需求。完成本教程后，您可以自信地 **向 PDF 添加形状**，处理越界错误，并将该方案集成到任何 .NET 项目中。

## 前置条件

开始之前，请确保您拥有：

* 已安装 .NET 6.0 SDK 或更高版本  
* Visual Studio 2022（或任意 C# IDE）  
* Aspose.PDF for .NET 许可证或免费评估密钥——两种模式下 API 行为相同  
* 一个名为 `input.pdf` 的 PDF 文件，放置在代码可引用的文件夹中  

上述即为示例唯一的外部依赖。

## 步骤 1：安装 Aspose.PDF NuGet 包

Aspose.PDF 库提供了 `Document`、`Rectangle` 等绘图类。

```bash
dotnet add package Aspose.PDF
```

运行此命令会将最新稳定版的 Aspose.PDF 添加到项目中，使 PDF 类可用于编译。

## 步骤 2：加载 PDF 文档

首个操作是加载源文件。这会在内存中创建可供修改的表示。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;

class PdfRectangleExample
{
    static void Main()
    {
        // Load the PDF document from disk
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

*为什么重要*：加载文档后，您即可访问其页面集合，为后续 **访问特定 PDF 页面** 做准备。

## 步骤 3：访问第二页（零基索引）

PDF 页面从 `0` 开始索引。要在第二页放置矩形，需获取索引为 `1` 的页面。

```csharp
        // Access the second page (pages are zero‑based)
        var page = pdfDocument.Pages[1];
```

如果文档页数少于两页，将抛出 `ArgumentOutOfRangeException`，提示您在生产代码中加入防护判断。

## 步骤 4：创建矩形形状

使用 `Rectangle` 结构定义矩形的位置和大小，然后将其包装为 Aspose 绘图对象。

```csharp
        // Define rectangle bounds: (x, y, width, height)
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            // Optional visual styling
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };
```

*为什么重要*：`BorderInfo` 和 `FillColor` 属性让您 **在 PDF 上绘制形状** 时拥有可见的轮廓和可选填充，使矩形在阅读时更醒目。

## 步骤 5：将矩形添加到页面的段落集合

Aspose.PDF 将绘图对象视为段落元素。将矩形加入页面的 `Paragraphs` 集合即可在页面上渲染。

```csharp
        // Add the rectangle shape to the page
        page.Paragraphs.Add(rectangleShape);
```

此时内存中的 PDF 文档已包含新形状，但磁盘上的文件仍保持不变，直至您保存它。

## 步骤 6：保存修改后的 PDF 并处理越界错误

调用 `Save` 将更新后的文档写入新文件。如果矩形超出页面尺寸，Aspose 会抛出 `PdfException`。捕获该异常可让您优雅地报告问题。

```csharp
        try
        {
            // Save the altered PDF to a new file
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            // Handle shape that does not fit on the page
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

*为什么重要*：`try/catch` 代码块确保您的应用 **安全保存修改后的 PDF**，错误信息还能帮助您调整矩形坐标。

## 完整工作示例

将所有步骤组合起来，下面是可直接运行的完整程序：

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;
using System.Drawing; // Required for Color

class PdfRectangleExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // Step 2: Access the second page (zero‑based)
        var page = pdfDocument.Pages[1];

        // Step 3: Create a rectangle shape positioned at (100,100) with width 300 and height 200
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };

        // Step 4: Add the rectangle shape to the page's paragraph collection
        page.Paragraphs.Add(rectangleShape);

        // Step 5: Save the modified PDF, handling out‑of‑bounds cases
        try
        {
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

### 预期输出

运行程序后会打印：

```
PDF saved successfully with rectangle added.
```

并生成 `output.pdf`，其中原始内容上会在第二页的指定坐标处显示一个蓝色矩形。

如果矩形尺寸超过页面，则会看到：

```
Shape out of bounds: The shape exceeds page margins.
```

## 常见问题和边缘情况

### 如果 PDF 只有一页怎么办？

访问 `pdfDocument.Pages[1]` 会抛出 `ArgumentOutOfRangeException`。在索引前先检查 `pdfDocument.Pages.Count` 以防止此类错误。

```csharp
if (pdfDocument.Pages.Count < 2)
{
    Console.WriteLine("Document does not contain a second page.");
    return;
}
```

### 如何在不同页面上添加多个矩形？

对每个目标页面重复步骤 2‑4，并相应调整矩形坐标。您可以将逻辑放入遍历 `pdfDocument.Pages` 的循环中。

### 能否使用其他形状，如圆形或多边形？

可以。Aspose.PDF 提供 `Ellipse`、`Polygon`、`Polyline` 等类，使用方式与 `Rectangle` 相同。只需将 `new Aspose.Pdf.Drawing.Rectangle` 替换为相应的形状类即可。

### 库是否支持带旋转的页面？

Aspose.PDF 在渲染形状时会自动遵循页面旋转。矩形坐标会按照页面的本地坐标系解释，无需额外变换。

## 性能考虑

* **内存使用** – 加载大型 PDF（数百 MB）会占用相应的内存。如果只需修改单页，可使用 `PdfFileInfo` 提取该页，修改后再合并回去。  
* **批量处理** – 为大量文档添加形状时，复用单个 `License` 实例可避免重复的许可证验证开销。

## 接下来的步骤

现在您已经掌握了 **向 PDF 添加矩形**，可以进一步探索以下相关主题：

* **在 PDF 上绘制形状** – 学习覆盖文本、图像和水印  
* **向 PDF 添加形状** – 将多个形状组合成单一注释层  
* **保存修改后的 PDF** – 使用流 (`MemoryStream`) 直接从 Web API 返回 PDF  
* **访问特定 PDF 页面** – 实现页面范围提取以生成自定义报告  

尝试不同的颜色、线型和透明度，以匹配您的品牌规范。

---

*祝编码愉快！如果本教程帮助您 **向 PDF 添加矩形**，请与团队分享或将改进贡献回社区。*

## 接下来应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式。

- [如何在 C# 中使用 Aspose.PDF 添加形状 – 步骤指南](/pdf/english/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [如何在 PDF 中使用 Aspose.PDF for .NET 添加线对象 – 步骤指南](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [如何在 C# 中创建 PDF – 添加页面、绘制矩形并保存](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}