---
category: general
date: 2026-09-05
description: 在 C# 中创建 PDF 文档，添加空白页，绘制矩形，并保存 PDF 文件。遵循一步一步的 Aspose.PDF 示例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add blank page pdf
- draw rectangle pdf
- save pdf file
- how to add rectangle
language: zh
lastmod: 2026-09-05
og_description: 在 C# 中创建 PDF 文档，添加空白页，绘制矩形，并保存 PDF 文件。请参阅使用 Aspose.PDF 的完整示例。
og_image_alt: Screenshot showing a PDF document with a drawn rectangle on a blank
  page
og_title: 创建带空白页和矩形的 PDF 文档 – C# 指南
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  headline: How to create PDF document with a blank page and rectangle
  type: TechArticle
- description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  name: How to create PDF document with a blank page and rectangle
  steps:
  - name: 'Edge case: custom page size'
    text: 'If your layout requires a 6 × 9 inch page, replace the default call with:'
  - name: 'Pro tip: styling the rectangle'
    text: 'You can change the stroke color and line width:'
  - name: 'Edge case: overwriting existing files'
    text: 'Aspose.PDF overwrites an existing file by default. To protect previous
      outputs, check for file existence first:'
  - name: Expected output
    text: Running the program creates a single‑page PDF. When you open `output.pdf`
      you will see a blank white page with a red rectangle positioned 100 points from
      the left and bottom edges, measuring 200 × 200 points.
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
- PDF generation
title: 如何创建包含空白页和矩形的 PDF 文档
url: /zh/net/document-creation/how-to-create-pdf-document-with-a-blank-page-and-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用空白页和矩形创建 PDF 文档

如果您需要以编程方式 **create PDF document**，本指南展示了在 C# 中的完整解决方案。您将学习如何添加空白页、在该页上绘制矩形，最后保存 PDF 文件。示例使用 Aspose.PDF 库，支持 .NET 6+ 和 .NET Framework 4.5+。

添加空白页和绘制形状是发票、证书或自定义报告的常见需求。完成本教程后，您将拥有一个可运行的项目，生成的 PDF 包含一个位于 (100, 100)、大小为 200 × 200 点的矩形。

## 前提条件

在开始之前，请确保您具备：

* Visual Studio 2022（或任何 C# IDE）
* .NET 6 SDK 或 .NET Framework 4.5+
* Aspose.PDF for .NET NuGet 包  
  ```bash
  dotnet add package Aspose.PDF
  ```
* 对输出目录的写入权限

无需额外配置；代码开箱即用。

## 创建 PDF 文档 – 概览

整个过程由四个逻辑步骤组成：

1. **Instantiate** 一个 `Document` 对象 – 该对象代表 PDF 文件。
2. **Add a blank page** – 页面提供绘图画布。
3. **Draw a rectangle** – `Path` 对象定义形状。
4. **Save the PDF file** – 将文档持久化到磁盘。

每个步骤都在独立的章节中阐述，便于根据需要复用或替换。

![Diagram of a PDF with a rectangle on a blank page](https://example.com/placeholder-image.png){.img-fluid alt="显示在空白页上绘制矩形的 PDF 文档的截图"}

## 添加空白页 PDF

在放置任何图形之前，PDF 必须至少包含一页。`Pages.Add()` 方法会创建一个默认尺寸（A4）的空白页。如果需要不同尺寸，请传入 `PageSize` 参数。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();

// Step 2: Add a blank page to the document
Page pdfPage = pdfDocument.Pages.Add();   // adds an A4 page by default
```

*Why this step matters* – 页面对象保存文本、图像和矢量图形的集合。没有页面，任何尝试添加矩形的操作都会抛出异常。

### 边缘情况：自定义页面尺寸

如果您的布局需要 6 × 9 英寸的页面，请使用以下调用替代默认方法：

```csharp
var pageSize = new Size(432, 648); // 72 points per inch
Page pdfPage = pdfDocument.Pages.Add(pageSize);
```

## 绘制矩形 PDF

绘制矩形只需创建一个 `Rectangle` 几何体并将其包装在 `Path` 中。`ValidateBounds()` 调用确保形状位于页面边距内，防止被裁剪。

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

// Step 4: Add the rectangle to the page contents
Path rectanglePath = new Path(shapeRect).ValidateBounds();
pdfPage.Contents.Add(rectanglePath);
```

*Why this step matters* – `Path` 对象是 Aspose.PDF 使用的底层矢量原语。通过验证边界，可避免矩形超出页面限制时的运行时错误。

### 专业提示：矩形样式

您可以更改描边颜色和线宽：

```csharp
rectanglePath.GraphInfo = new GraphInfo
{
    StrokeColor = Color.Red,
    LineWidth = 2
};
```

这将产生一个红色轮廓，线宽为 2 点。

## 保存 PDF 文件

持久化文档会在磁盘上生成文件。`Save` 方法接受文件路径或流。提供绝对路径可以明确位置，对自动化脚本非常有用。

```csharp
// Step 5: Save the PDF to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

*Why this step matters* – 保存是唯一一次将内存中的表示转化为物理文件的时机。如果需要从 Web API 返回 PDF，请将文件路径替换为 `MemoryStream`。

### 边缘情况：覆盖已有文件

Aspose.PDF 默认会覆盖已有文件。为保护之前的输出，请先检查文件是否存在：

```csharp
if (File.Exists(outputPath))
{
    File.Delete(outputPath);
}
pdfDocument.Save(outputPath);
```

## 添加矩形的最佳实践

* **Keep coordinates within the page margins** – 使用 `ValidateBounds()` 或手动计算边距。
* **Reuse `GraphInfo` objects** 在绘制多个形状时复用，可减少内存分配。
* **Dispose of the `Document` object**（如示例中的 `using var`）以及时释放本机资源。
* **Test with different DPI settings** 若后续嵌入光栅图像；矢量形状（如矩形）在任何分辨率下都保持清晰。

## 完整可运行示例

下面是完整程序，可直接复制到控制台应用中。无需修改即可编译，并在项目文件夹生成 `output.pdf`。

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using var pdfDocument = new Document();

        // Add a blank page to the document
        Page pdfPage = pdfDocument.Pages.Add();

        // Define a rectangle shape (x, y, width, height)
        Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

        // Create a path for the rectangle and validate its bounds
        Path rectanglePath = new Path(shapeRect).ValidateBounds();

        // Optional: style the rectangle (red outline, 2‑pt width)
        rectanglePath.GraphInfo = new GraphInfo
        {
            StrokeColor = Color.Red,
            LineWidth = 2
        };

        // Add the rectangle to the page contents
        pdfPage.Contents.Add(rectanglePath);

        // Determine output path
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");

        // Ensure no leftover file blocks the save operation
        if (File.Exists(outputPath))
        {
            File.Delete(outputPath);
        }

        // Save the PDF to a file
        pdfDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

### 预期输出

运行程序后会生成单页 PDF。打开 `output.pdf` 时，您会看到一页白色空白页，左侧和底部各留 100 点的距离处有一个红色矩形，尺寸为 200 × 200 点。

## 结论

您现在已经掌握了使用 Aspose.PDF 在 C# 中 **create PDF document**、**add blank page pdf**、**draw rectangle pdf** 和 **save pdf file** 的方法。示例涵盖了关键 API 调用，解释了每一步的必要性，并提供了自定义页面尺寸或矩形样式等常见变体的技巧。

接下来，您可以探索 **adding text**、**embedding images** 或 **creating multi‑page reports** 等相关主题。相同的模式——实例化 `Document`、操作页面、添加矢量或光栅内容，然后 `Save`——适用于所有这些场景。欢迎尝试不同的形状、颜色和页面布局，以满足项目需求。

## 接下来您应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，构建在本教程演示的技巧之上。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [Create PDF Document C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)
- [Create PDF Document with Aspose.PDF – Step‑by‑Step Guide](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Create PDF Document with Aspose – Add Page, Text Box, and Form](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}