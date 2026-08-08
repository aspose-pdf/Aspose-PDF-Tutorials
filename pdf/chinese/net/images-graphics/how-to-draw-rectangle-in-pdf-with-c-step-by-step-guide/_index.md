---
category: general
date: 2026-03-27
description: 学习如何使用 Aspose.Pdf for C# 在 PDF 中绘制矩形。向 PDF 添加矩形，向 PDF 添加形状，并使用清晰的代码示例在
  PDF 上绘制形状。
draft: false
keywords:
- how to draw rectangle
- add rectangle to pdf
- add shape to pdf
- draw shape on pdf
- draw rectangle in pdf
language: zh
og_description: 掌握使用 Aspose.Pdf 在 PDF 中绘制矩形的方法。本教程一步步演示如何向 PDF 添加矩形、添加形状以及在 PDF 上绘制形状。
og_title: 使用 C# 在 PDF 中绘制矩形 – 完整指南
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: 如何使用 C# 在 PDF 中绘制矩形 – 步骤指南
url: /zh/net/images-graphics/how-to-draw-rectangle-in-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 C# 在 PDF 中绘制矩形 – 步骤指南

是否曾想过 **如何在 PDF 中绘制矩形** 而不必纠结于底层的 PDF 语法？你并不孤单。许多开发者在需要可视化边界框、突出显示区域或在生成的文档中添加简单装饰元素时都会卡住。好消息是？使用 Aspose.Pdf for .NET，这个过程轻而易举。

在本教程中，我们将逐步演示如何 **向 PDF 添加矩形**、**向 PDF 添加形状**，以及最终 **在 PDF 中绘制矩形**，全部使用简洁、符合惯用法的 C#。完成后，你将拥有一个可运行的程序，生成的 PDF 文件中包含一个清晰的矩形——无需任何外部工具。

## 前置条件

- .NET 6.0 或更高版本（代码同样适用于 .NET Core 和 .NET Framework）
- Aspose.Pdf for .NET NuGet 包（`Install-Package Aspose.Pdf`）
- 基本的 C# 开发环境（Visual Studio、VS Code、Rider 等）

不需要其他库；其余全部由 Aspose.Pdf 自身处理。

## 第一步：创建项目并导入命名空间

首先，新建一个控制台应用程序并引入 Aspose.Pdf 命名空间。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the rest of the code here.
        }
    }
}
```

**为什么重要：** 导入 `Aspose.Pdf.Drawing` 可让你使用 `Rectangle` 形状类来 **在 PDF 上绘制形状**。保持入口代码整洁有助于后续步骤的阅读。

## 第二步：创建新 PDF 文档并添加页面

没有页面的 PDF 是没有意义的，所以我们先创建文档对象并添加一页。

```csharp
// Step 2: Initialize a new PDF document
Document pdfDoc = new Document();

// Add a blank page to the document (size defaults to A4)
Page page = pdfDoc.Pages.Add();
```

**说明：** `Document` 类代表整个文件，而 `Pages.Add()` 返回一个全新的 `Page` 对象，随后我们将在其上 **向 PDF 添加矩形**。默认的 A4 大小适用于大多数场景，如需自定义画布可传入宽高参数。

## 第三步：定义矩形形状

下面进入 **如何绘制矩形** 的核心——设置位置和尺寸。

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
// Coordinates are measured from the lower‑left corner of the page.
var rectangleShape = new Rectangle(100, 500, 300, 200)
{
    // Optional: set line color and fill color
    BorderColor = Color.Black,
    BorderWidth = 2,
    FillColor = Color.LightGray
};
```

**为何要设置这些属性：**  
- `BorderColor` 和 `BorderWidth` 控制轮廓，使矩形可见。  
- `FillColor` 为其提供淡背景，适用于需要高亮区域的情况。  
- 构造函数 `(x, y, width, height)` 让你能够精准 **在 PDF 中绘制矩形**。

## 第四步：将矩形添加到页面

形状准备好后，我们通过将其加入页面的 `Annotations` 集合来 **向 PDF 添加形状**。Aspose.Pdf 会自动验证边界，无需担心溢出。

```csharp
// Step 4: Add the rectangle shape to the page
page.Annotations.Add(rectangleShape);
```

**内部原理：** `Annotations` 集合将矩形视为矢量图形。PDF 渲染时，库会把我们的坐标转换为 PDF 内容流。

## 第五步：保存文档

最后，将 PDF 写入磁盘，以便在任意阅读器中打开。

```csharp
// Step 5: Save the PDF file
string outputPath = "RectangleDemo.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

**结果：** 打开 `RectangleDemo.pdf`，你会看到一个浅灰色矩形，黑色边框位于页面左侧 100 pt、底部 500 pt 处。这就是使用 C# **绘制矩形** 的完整解决方案。

## 完整可运行示例

将所有代码片段组合起来，即可得到完整、可直接运行的程序：

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize a new PDF document
            Document pdfDoc = new Document();

            // Add a blank page (A4 by default)
            Page page = pdfDoc.Pages.Add();

            // Define a rectangle shape (x, y, width, height)
            var rectangleShape = new Rectangle(100, 500, 300, 200)
            {
                BorderColor = Color.Black,
                BorderWidth = 2,
                FillColor = Color.LightGray
            };

            // Add the rectangle to the page
            page.Annotations.Add(rectangleShape);

            // Save the document
            string outputPath = "RectangleDemo.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved to {outputPath}");
        }
    }
}
```

**预期输出：** 生成名为 `RectangleDemo.pdf` 的文件，包含单页居中的浅灰色矩形，黑色轮廓。可使用 Adobe Reader、Chrome 或任意 PDF 阅读器打开。

## 常见变体与边界情况

### 1. 绘制多个矩形

如果需要 **向 PDF 多次添加矩形**，只需创建更多 `Rectangle` 对象并逐个加入 `page.Annotations`。对坐标集合进行循环即可轻松实现。

```csharp
foreach (var rectInfo in rectangles)
{
    var rect = new Rectangle(rectInfo.X, rectInfo.Y, rectInfo.Width, rectInfo.Height)
    {
        BorderColor = Color.Blue,
        BorderWidth = 1,
        FillColor = Color.Transparent
    };
    page.Annotations.Add(rect);
}
```

### 2. 使用不同单位

Aspose.Pdf 使用点（1 pt = 1/72 英寸）。如果更喜欢使用毫米，可先进行转换：

```csharp
double mmToPt = 72.0 / 25.4;
float x = (float)(20 * mmToPt); // 20 mm from left
float y = (float)(150 * mmToPt);
```

### 3. 将矩形作为表单字段添加

当需要交互式矩形（例如可点击区域）时，使用 `LinkAnnotation` 替代普通 `Rectangle`。代码类似，只是会添加 URL 或 JavaScript 动作。

### 4. 兼容性注意

Aspose.Pdf 23.9 版（2026 年初发布）完全支持上述 API。旧版本可能需要使用 `page.AddAnnotation(rectangleShape)` 而非 `page.Annotations.Add`。遇到编译错误时，请查阅发行说明。

## 专业技巧与常见坑点

- **技巧：** 若只需轮廓，可将 `FillColor = Color.Transparent`，可略微减小文件体积。  
- **注意：** 使用超出页面尺寸的坐标。Aspose.Pdf 会默默裁剪形状，调试时可能会产生困惑。  
- **性能提示：** 添加成千上万个矩形是可行的，但若生成大型报告，考虑将形状批量写入单个 `Graphics` 对象，以降低开销。

## 可视化参考

下面是一张生成的 PDF 截图（矩形以浅灰色高亮）。alt 文本已包含主要关键词以利 SEO。

![在 PDF 中绘制矩形示例](https://example.com/images/rectangle-demo.png "在 PDF 中绘制矩形示例")

## 结论

我们已经介绍了如何使用 Aspose.Pdf for C# **在 PDF 中绘制矩形**。通过创建 `Document`、添加 `Page`、定义 `Rectangle` 形状，最后 **向 PDF 添加形状**，即可仅用几行代码生成矢量图形。无论是用于高亮、布局调试还是 UI 覆盖，**向 PDF 添加矩形** 的方法都具备良好的可扩展性。

接下来，你可以探索 **在 PDF 上绘制其他形状**——如圆形、多段线，甚至自定义 SVG 路径。亦可深入文本渲染、图像插入以及 PDF 表单操作，构建功能完整的报表。Aspose.Pdf 提供了丰富的 API，掌握了本文的基础后，你已准备好尽情实验。

祝编码愉快，愿你的 PDF 总是呈现出你设想的样子！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}