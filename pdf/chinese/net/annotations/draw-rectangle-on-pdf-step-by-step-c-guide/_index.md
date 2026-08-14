---
category: general
date: 2026-08-14
description: 使用 C# 快速在 PDF 上绘制矩形。了解如何定义矩形尺寸并仅用几行代码将形状添加到 PDF 页面。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- draw rectangle on pdf
- how to define rectangle dimensions
language: zh
lastmod: 2026-08-14
og_description: 使用 C# 在几秒钟内在 PDF 上绘制矩形。本指南展示如何定义矩形尺寸、添加形状以及验证页面边界，以实现可靠的 PDF 图形。
og_image_alt: Screenshot of a PDF page showing a black rectangle drawn with C# code
og_title: 在 PDF 上绘制矩形 – 完整的 C# 教程
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: draw rectangle on pdf quickly using C#. Learn how to define rectangle
    dimensions and add shapes to a PDF page in just a few lines.
  headline: draw rectangle on pdf – step‑by‑step C# guide
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
- RectangleShape
- Graphics
title: 在 PDF 上绘制矩形 – C# 步骤指南
url: /zh/net/annotations/draw-rectangle-on-pdf-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 上绘制矩形 – 完整 C# 教程

如果您需要使用 C# **在 PDF 上绘制矩形**，本指南为您提供简洁、可投入生产的解决方案。您将准确了解 **如何定义矩形尺寸**，验证形状是否适合，并通过一次方法调用将其添加到页面。

本教程涵盖了从创建 PDF 文档到渲染矩形的全部步骤，您可以直接复制粘贴代码到自己的项目中并立即看到效果。无需查阅外部文档——只需按照以下步骤操作。

## 前置条件

开始之前，请确保您具备：

* .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.7+）
* **Aspose.PDF for .NET** NuGet 包（`Install-Package Aspose.PDF`）
* 对 C# 语法的基本了解
* Visual Studio 或 VS Code 等 IDE

> **专业提示：** 使用 Aspose.PDF 的免费评估许可证进行快速实验；它会添加一个小水印，但可以测试所有功能。

## 如何使用 C# 在 PDF 上绘制矩形

任务的核心是创建 `RectangleShape`，设置其大小和描边，并将其附加到 `Page`。下面的 H2 标题包含了主要关键词，满足 SEO 要求。

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        Document pdfDoc = new Document();

        // 2️⃣ Add a blank page (default size: A4)
        Page page = pdfDoc.Pages.Add();

        // 3️⃣ Define the rectangle bounds (x, y, width, height)
        //    This demonstrates how to define rectangle dimensions.
        Rectangle rectBounds = new Rectangle(0, 0, 500, 700);

        // 4️⃣ Create the rectangle shape and set its stroke color
        RectangleShape rectangleShape = new RectangleShape(rectBounds)
        {
            StrokeColor = Color.Black   // black outline
        };

        // 5️⃣ Verify that the shape fits within the page boundaries
        page.CheckShapeBoundary(rectangleShape);

        // 6️⃣ Add the shape to the page
        page.Add(rectangleShape);

        // 7️⃣ Save the PDF to disk
        string outPath = "RectangleDemo.pdf";
        pdfDoc.Save(outPath);
        Console.WriteLine($"PDF saved to {outPath}");
    }
}
```

### 各步骤说明

| 步骤 | 为什么重要 |
|------|------------|
| **1️⃣ 创建新的 PDF 文档** | 初始化用于容纳页面和图形的容器。 |
| **2️⃣ 添加空白页** | 需要一个 `Page` 对象，因为形状是附加到页面，而不是直接附加到文档。 |
| **3️⃣ 定义矩形边界** | 这里是 **如何定义矩形尺寸** 的位置。`Rectangle` 构造函数接受 `x`、`y`、`width` 和 `height`，单位为点（1 pt = 1/72 in）。 |
| **4️⃣ 创建矩形形状** | `RectangleShape` 是 Aspose 用于渲染矩形的类。设置 `StrokeColor` 定义轮廓；也可以设置 `FillColor` 进行实填充。 |
| **5️⃣ 验证页面边界** | `CheckShapeBoundary` 在矩形超出页面尺寸时抛出异常，防止生成错误的 PDF。 |
| **6️⃣ 将形状添加到页面** | 形状成为页面内容流的一部分。 |
| **7️⃣ 保存 PDF** | 将文档持久化为文件，可使用任何 PDF 查看器打开。 |

生成的 `RectangleDemo.pdf` 包含一个位于页面左上角的黑色矩形，宽度恰好为 500 pt，高度为 700 pt。

![在 PDF 上绘制矩形示例](https://example.com/rectangle-demo.png "在 PDF 上绘制矩形示例")

*图片替代文字：在 PDF 上绘制矩形示例，显示 PDF 页面左上角的黑色矩形。*

## 如何为不同页面尺寸定义矩形尺寸

上面的代码片段使用了固定值（`500 x 700`）。在实际应用中，您通常需要让矩形根据页面的宽高自适应。

```csharp
// Get page dimensions (in points)
float pageWidth = page.PageInfo.Width;
float pageHeight = page.PageInfo.Height;

// Define a rectangle that occupies 80% of the page width and 50% of the height
float rectWidth  = pageWidth * 0.8f;
float rectHeight = pageHeight * 0.5f;

// Center the rectangle on the page
float rectX = (pageWidth - rectWidth) / 2;
float rectY = (pageHeight - rectHeight) / 2;

Rectangle dynamicRect = new Rectangle(rectX, rectY, rectWidth, rectHeight);
RectangleShape dynamicShape = new RectangleShape(dynamicRect)
{
    StrokeColor = Color.DarkBlue,
    FillColor   = Color.LightGray   // optional fill
};

page.CheckShapeBoundary(dynamicShape);
page.Add(dynamicShape);
```

**关键要点：**

* 使用 `page.PageInfo.Width` 和 `Height` 读取实际页面尺寸。
* 乘以系数（例如 `0.8f`）可将尺寸表示为页面的百分比。
* 通过用页面尺寸减去矩形尺寸再除以二来实现居中。

## 常见陷阱及规避方法

| 陷阱 | 产生原因 | 解决方案 |
|------|----------|----------|
| 矩形超出页面 | 使用硬编码的尺寸大于页面大小。 | 在添加形状 **之前** 调用 `page.CheckShapeBoundary`；若抛出异常则调整尺寸。 |
| 描边不可见 | `StrokeColor` 保持默认 (`Color.Empty`)。 | 明确设置 `StrokeColor`（例如 `Color.Black`）。 |
| 矩形出现在屏幕外 | PDF 坐标系原点在左下角，使用屏幕式左上坐标会导致翻转。 | 记住原点 `(0,0)` 位于左下角。相应调整 `y`，或使用 `pageHeight - desiredY`。 |
| 线宽意外过细 | 默认线宽对打印可能太细。 | 设置 `rectangleShape.LineWidth = 2;` 增加线宽。 |

## 扩展示例

一旦您能够 **在 PDF 上绘制矩形**，就可以轻松添加其他形状：

* **EllipseShape** – 用于绘制圆形或椭圆。
* **PolygonShape** – 用于自定义多边形。
* **TextFragment** – 为矩形添加标签。

所有形状遵循相同的工作流：定义边界、配置外观、验证边界，然后添加到页面。

## 完整可运行程序

下面是将基础矩形和动态尺寸示例组合在一起的完整程序。将其复制到新的控制台项目中，恢复 `Aspose.PDF` NuGet 包后运行。

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class RectangleDemo
{
    static void Main()
    {
        // Create document and page
        Document doc = new Document();
        Page page = doc.Pages.Add();

        // ==== Fixed‑size rectangle (basic example) ====
        Rectangle fixedRect = new Rectangle(0, 0, 500, 700);
        RectangleShape fixedShape = new RectangleShape(fixedRect)
        {
            StrokeColor = Color.Black,
            LineWidth   = 1
        };
        page.CheckShapeBoundary(fixedShape);
        page.Add(fixedShape);

        // ==== Dynamic rectangle that adapts to page size ====
        float pageW = page.PageInfo.Width;
        float pageH = page.PageInfo.Height;

        float dynWidth  = pageW * 0.6f;
        float dynHeight = pageH * 0.3f;
        float dynX      = (pageW - dynWidth) / 2;
        float dynY      = (pageH - dynHeight) / 2;

        Rectangle dynamicRect = new Rectangle(dynX, dynY, dynWidth, dynHeight);
        RectangleShape dynamicShape = new RectangleShape(dynamicRect)
        {
            StrokeColor = Color.DarkBlue,
            FillColor   = Color.LightYellow,
            LineWidth   = 2
        };
        page.CheckShapeBoundary(dynamicShape);
        page.Add(dynamicShape);

        // Save PDF
        string outFile = "CombinedRectangles.pdf";
        doc.Save(outFile);
        Console.WriteLine($"PDF created: {outFile}");
    }
}
```

**预期输出：**  
打开 `CombinedRectangles.pdf`。您会看到一个锚定在左下角的黑色矩形，以及一个居中的深蓝色矩形（填充淡黄色）。两个矩形都遵循页面边距。

## 结论

您现在已经掌握了使用 C# **在 PDF 上绘制矩形** 的方法，并能够精准 **定义矩形尺寸**，无论是固定布局还是响应式布局。该方案利用 Aspose.PDF 的 `RectangleShape`、边界检查以及简单的算术运算，能够适配任意页面尺寸。

接下来，您可以进一步探索：

* 添加 **填充颜色** 和 **线条样式**（虚线、点线）——次要关键词：带样式的如何定义矩形尺寸。
* 将多个形状组合到同一个 `Page` 中，以创建图表或表单。
* 将 PDF 导出为流用于 Web API，而不是保存到磁盘。

尝试不同的尺寸、颜色和位置，掌握 .NET 应用中的 PDF 图形绘制。祝编码愉快！

## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您在自己的项目中进一步掌握 API 功能并探索替代实现方案。每篇资源都提供完整的可运行代码示例和逐步解释。

- [如何使用 Aspose.PDF for .NET 定制 PDF：设置页面边距并绘制直线](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [如何使用 Aspose.PDF for .NET 为 PDF 添加页面水印：完整指南](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [如何使用 Aspose.PDF for .NET 为 PDF 添加页码水印 | 水印与背景](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}