---
category: general
date: 2026-08-04
description: 使用 C# 向 PDF 添加矩形。通过清晰、完整的示例，学习如何在 C# 中使用 Aspose.Pdf 绘制 PDF 形状。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to pdf
- how to draw shape in pdf c#
language: zh
lastmod: 2026-08-04
og_description: 使用 C# 向 PDF 添加矩形。本教程展示了如何快速可靠地在 PDF 中使用 C# 绘制形状。
og_image_alt: Screenshot of a PDF page with a blue rectangle drawn by C# code
og_title: 使用 C# 向 PDF 添加矩形 – 完整编程指南
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  headline: Add rectangle to PDF with C# – step‑by‑step guide
  type: TechArticle
- description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  name: Add rectangle to PDF with C# – step‑by‑step guide
  steps:
  - name: '**Create a new console project**'
    text: '**Create a new console project**'
  - name: '**Add the Aspose.Pdf package**'
    text: '**Add the Aspose.Pdf package**'
  - name: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
    text: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: 使用 C# 向 PDF 添加矩形 – 步骤指南
url: /zh/net/images-graphics/add-rectangle-to-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 向 PDF 添加矩形 – 步骤指南

如果您需要在 C# 应用程序中 **向 PDF 添加矩形**，本指南将准确展示如何操作。您将看到一个完整、可运行的示例，使用 Aspose.Pdf 库在 PDF C# 中绘制形状，并了解每行代码的作用。

在 PDF 中绘制形状是报表生成器、发票模板和自定义文档品牌化的常见需求。完成本教程后，您可以插入任意矩形批注，修改其大小、颜色或位置，并在不丢失现有内容的情况下保存修改后的文档。

**您将学习**

* 如何使用 Aspose.Pdf 加载已有的 PDF。
* 如何定义矩形边界并创建矩形形状。
* 如何将矩形添加到页面的段落集合中。
* 如何保存更新后的 PDF 并验证结果。
* 多页、透明度和自定义线条样式的变体。

**先决条件**

* .NET 6.0 或更高（代码同样适用于 .NET Framework 4.7+）。
* Visual Studio 2022 或任意 C# IDE。
* 对 `Aspose.Pdf` 的 NuGet 引用（免费试用版或正式授权版）。
* 一个名为 `input.pdf` 的输入 PDF 文件，放置在您可控制的文件夹中。

---

## 如何在 PDF C# 中绘制形状 – 项目设置

1. **创建一个新的控制台项目**  

   ```bash
   dotnet new console -n PdfRectangleDemo
   cd PdfRectangleDemo
   ```

2. **添加 Aspose.Pdf 包**  

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. **将 `input.pdf` 放置在项目目录中**（或放在后续引用的任意文件夹）。

项目现在已经准备好编译能够 **向 PDF 添加矩形** 的代码。

---

## 第 1 步：加载 PDF 文档

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // Load the existing PDF file.
        Document pdfDoc = new Document("input.pdf");
```

*`Document` 类解析文件并公开 `Pages` 集合。加载是进行任何绘制操作的首要步骤。*

---

## 第 2 步：选择目标页面

```csharp
        // Get the first page (pages are 1‑based).
        Page firstPage = pdfDoc.Pages[1];
```

*如果需要在其他页面添加矩形，请将索引替换为目标页码。当索引超出范围时，库会抛出异常，请确保 PDF 包含足够的页面。*

---

## 第 3 步：定义矩形边界

```csharp
        // Define the rectangle's position and size (points).
        // (left, bottom, right, top) – origin is bottom‑left.
        Rectangle bounds = new Rectangle(50, 700, 300, 800);
```

*坐标系使用点（1 pt = 1/72 英寸）。示例在页面顶部附近创建一个宽 250 pt、高 100 pt 的矩形。根据您的布局自行调整数值。*

---

## 第 4 步：创建矩形形状

```csharp
        // Create a rectangle shape with the defined bounds.
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            // Optional styling – a semi‑transparent blue fill.
            FillColor = Color.FromRgb(0, 120, 215),
            FillOpacity = 0.4,

            // Optional border – 2 pt thick, dark gray.
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };
```

*`Rectangle` 类继承自 `GraphicalObject`。设置 `FillColor` 和 `Border` 是可选的，但它演示了在 **如何在 PDF C# 中绘制形状** 时如何控制外观，而不仅仅是普通轮廓。*

---

## 第 5 步：将矩形添加到页面

```csharp
        // Add the rectangle shape to the page's paragraph collection.
        firstPage.Paragraphs.Add(rectangleShape);
```

*段落是任何可绘制对象的容器。通过将形状插入 `Paragraphs`，Aspose.Pdf 在文档保存时会渲染它。*

---

## 第 6 步：保存修改后的 PDF

```csharp
        // Save the updated PDF to a new file.
        pdfDoc.Save("output.pdf");

        // Inform the user.
        Console.WriteLine("Rectangle added and saved to output.pdf");
    }
}
```

*保存会创建一个新文件，原始的 `input.pdf` 保持不变。您可以通过传入相同路径来覆盖源文件，但保留备份是最佳实践。*

---

## 完整源代码（可运行）

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color struct

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document
        Document pdfDoc = new Document("input.pdf");

        // Step 2: Get the first page (pages are 1‑based)
        Page firstPage = pdfDoc.Pages[1];

        // Step 3: Define rectangle bounds (left, bottom, right, top)
        Rectangle bounds = new Rectangle(50, 700, 300, 800);

        // Step 4: Create a rectangle shape with optional styling
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            FillColor = Color.FromArgb(102, 0, 120, 215), // 40 % opacity blue
            FillOpacity = 0.4,
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };

        // Step 5: Add the rectangle shape to the page
        firstPage.Paragraphs.Add(rectangleShape);

        // Step 6: Save the modified PDF
        pdfDoc.Save("output.pdf");

        Console.WriteLine("Rectangle added to PDF successfully.");
    }
}
```

**预期输出** – 在任意 PDF 查看器中打开 `output.pdf`。您应当看到第一页右上角附近有一个蓝色填充、深灰色边框的矩形。

---

## 如何在 PDF C# 中对多页绘制形状

如果需要在每一页 **向 PDF 添加矩形**，可以遍历 `Pages` 集合：

```csharp
foreach (Page page in pdfDoc.Pages)
{
    Rectangle rect = new Rectangle(50, 700, 300, 800);
    Rectangle shape = new Rectangle(rect)
    {
        FillColor = Color.FromArgb(80, 255, 0, 0), // semi‑transparent red
        Border = new Border { Width = 1, Color = Color.Black }
    };
    page.Paragraphs.Add(shape);
}
```

*此模式在每页使用相同的边界。如果需要不同位置，请根据页面自行调整坐标。*

---

## 常见陷阱与最佳实践提示

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| 矩形显示在页面之外 | 坐标是相对于左下角测量的；使用顶部为基准的坐标系会导致混淆。 | 记住 Y 轴向上增长。使用适合页面尺寸的值（`page.PageInfo.Width`、`page.PageInfo.Height`）。 |
| 形状不可见 | 填充不透明度设为 `0` 或边框宽度设为 `0`。 | 确保 `FillOpacity` 大于 `0`，且 `Border.Width` 至少为 `0.5`。 |
| 保存时抛出 `AccessDeniedException` | 输出文件被其他程序占用。 | 运行代码前关闭所有查看器，或保存到其他路径。 |
| 矩形覆盖已有内容 | 未设置层级控制。 | 如需控制层级，可使用 `ZIndex` 属性（数值越大越在上层）。 |

---

## 扩展矩形 – 渐变、旋转与透明度

Aspose.Pdf 支持高级图形。创建带线性渐变的旋转矩形：

```csharp
Rectangle gradientRect = new Rectangle(bounds)
{
    // Gradient fill from left (blue) to right (green)
    FillColor = Color.Blue,
    FillColor2 = Color.Green,
    FillMode = FillMode.LinearGradient,
    // Rotate 45 degrees around the rectangle's center
    Rotation = 45
};
firstPage.Paragraphs.Add(gradientRect);
```

*相同的代码模式演示了 **如何在 PDF C# 中绘制形状** 并实现更丰富的视觉效果。*

---

## 以编程方式验证结果

您可以通过检查页面的段落计数来确认矩形是否已添加：

```csharp
int shapeCount = firstPage.Paragraphs.Count;
Console.WriteLine($"Page 1 now contains {shapeCount} paragraph objects.");
```

如果插入后计数增加了一个，则操作成功。

---

## 结论

现在您已经掌握了使用 C# **向 PDF 添加矩形** 的方法。教程涵盖了加载文档、定义边界、创建矩形形状、将其插入页面以及保存结果的全过程。您还了解了多页处理、常见错误的规避以及高级样式的应用。

接下来，探索相关主题，如 **如何在 PDF C# 中绘制圆形、 多边形 或自由路径**，并学习将形状与文本、图像结合，构建功能完整的 PDF 报表。

祝编码愉快！


## 接下来您应该学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助您在项目中进一步使用这些技术。每个资源都提供完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并探索替代实现方案。

- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds Guide](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)
- [How to Add an Image Stamp to a PDF Using Aspose.PDF for .NET: A Comprehensive Guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [How to Add a Rotating Image Watermark to PDFs Using Aspose.PDF for .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}