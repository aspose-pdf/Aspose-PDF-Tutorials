---
category: general
date: 2026-02-14
description: 快速使用 C# 创建 PDF 文档：向 PDF 添加页面，绘制矩形形状，并使用 Aspose.Pdf 通过几行代码将 PDF 保存到文件。
draft: false
keywords:
- create pdf document c#
- add page to pdf
- how to draw rectangle
- add shape to pdf
- save pdf to file
language: zh
og_description: 在几分钟内使用 C# 创建 PDF 文档。学习如何向 PDF 添加页面、绘制矩形、添加形状，并使用清晰的代码示例将 PDF 保存到文件。
og_title: 使用 C# 创建 PDF 文档 – 步骤指南
tags:
- Aspose.Pdf
- C#
- PDF generation
title: 创建 PDF 文档 C# – 添加页面、绘制矩形并保存
url: /zh/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建 PDF 文档 C# – 添加页面、绘制矩形并保存

是否曾经需要 **create PDF document C#** 并且不知从何入手？你并不是唯一的开发者——很多人在首次进行编程式 PDF 生成时都会遇到同样的难题。好消息是，只需几行 Aspose.Pdf 代码，你就可以向 PDF 添加页面、绘制矩形，并 **save PDF to file**，轻松搞定。

在本教程中，我们将逐步演示所有必需的操作：初始化 PDF、插入新页面、绘制矩形形状，最后将文件持久化到磁盘。完成后，你将拥有一个可运行的控制台应用程序，它会在全新 PDF 页面中生成一个带蓝色边框的矩形。

## 你需要准备的环境

- **.NET 6 或更高**（示例使用顶级语句，但任何近期的 .NET 版本均可）
- **Aspose.Pdf for .NET** NuGet 包  
  ```bash
  dotnet add package Aspose.Pdf
  ```
- 一个拥有写入权限的文件夹——教程会将文件保存到 `YOUR_DIRECTORY/shapes.pdf`。

无需额外配置、无需 XML，仅需纯 C#。

## 创建 PDF 文档 C# – 概览

第一步是实例化一个 `Document` 对象。可以把它看作你的空白画布，之后添加的所有内容——页面、文本、图形——都会附着在这个实例上。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document (the canvas)
using var pdfDocument = new Document();
```

> **为什么使用 `using var`？**  
> `Document` 类实现了 `IDisposable`。将其放在 `using` 语句中可以确保所有非托管资源（文件句柄、原生缓冲区）在使用完毕后立即释放，这在长时间运行的服务中尤为重要。

## 向 PDF 添加页面

没有页面的 PDF 就像一本没有页码的书——毫无用处。添加页面只需一次方法调用，同时会返回一个 `Page` 对象，供后续操作使用。

```csharp
// Step 2: Add a fresh page to the document
var pdfPage = pdfDocument.Pages.Add();
```

> **提示：** 新添加的页面会自动采用默认尺寸（A4）。如果需要自定义尺寸，可在添加任何内容之前设置 `pdfPage.PageInfo.Width` 和 `Height`。

## 如何绘制矩形

接下来是有趣的部分：绘制矩形。Aspose.Pdf 使用 `RectangleShape` 类，它需要一个 `Rectangle`（x、y、宽、高）来定义边界。坐标系起点位于页面的左下角。

```csharp
// Step 3: Define the rectangle bounds (x, y, width, height)
// This will be validated – an exception is thrown if the rectangle is out of bounds
var rectangleBounds = new Rectangle(50, 50, 200, 150);
```

> **边缘情况：** 如果 `x + width` 超过页面宽度或 `y + height` 超过页面高度，Aspose 会抛出 `ArgumentException`。在为不同页面尺寸生成 PDF 时，请务必再次确认尺寸参数。

## 向 PDF 添加形状

准备好边界后，我们创建形状、设置蓝色描边，然后将其加入页面的段落集合中。

```csharp
// Step 4: Create a rectangle shape with a blue stroke and add it to the page
var rectangleShape = new RectangleShape(rectangleBounds)
{
    StrokeColor = Color.Blue,   // Outline color
    // FillColor = Color.LightGray, // Uncomment to add a fill
    // LineWidth = 2                // Adjust border thickness if needed
};
pdfPage.Paragraphs.Add(rectangleShape);
```

> **为什么要加入 `Paragraphs`？**  
> 在 Aspose.Pdf 中，视觉元素（如形状）被视为“段落”，因为它们占据页面上的矩形区域。这种设计使得布局引擎在处理文本和图形时保持一致。

## 将 PDF 保存到文件

最后一步是持久化文档。提供完整路径后，Aspose 会自动完成压缩、对象流和交叉引用表等繁重工作。

```csharp
// Step 5: Save the PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/shapes.pdf");
```

> **专业技巧：** 如果希望文件与可执行文件位于同一目录，可使用 `Path.Combine(Environment.CurrentDirectory, "shapes.pdf")`；若担心目录不存在，可提前调用 `Directory.CreateDirectory`，以避免 `DirectoryNotFoundException`。

### 预期结果

使用任意 PDF 查看器打开 `shapes.pdf`。你应该会看到一页 A4 大小的 PDF，页面左侧和底部各留 50 点距离，呈现一个 **蓝色边框矩形**，尺寸为 200 × 150 点。页面中没有文字，仅有该形状——非常适合作为水印、表单字段或视觉占位符。

![PDF document with a blue rectangle created using create pdf document c#](https://example.com/images/pdf-rectangle.png "使用 create pdf document c# 创建的带蓝色矩形的 PDF 文档")

*Alt text:* *使用 create pdf document c# 创建的带蓝色矩形的 PDF 文档。*

## 完整可运行示例

下面是完整的、可直接复制粘贴的程序代码。它可以作为控制台应用（`dotnet new console`）编译运行，除 NuGet 包外无需其他配置。

```csharp
// Program.cs
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

using var pdfDocument = new Document();               // Create PDF document
var pdfPage = pdfDocument.Pages.Add();                // Add a page

// Define rectangle bounds (x, y, width, height)
// Aspose validates the rectangle – out‑of‑bounds throws an exception
var rectangleBounds = new Rectangle(50, 50, 200, 150);

// Create the rectangle shape (blue stroke) and add it to the page
var rectangleShape = new RectangleShape(rectangleBounds)
{
    StrokeColor = Color.Blue
};
pdfPage.Paragraphs.Add(rectangleShape);

// Save the document to disk
pdfDocument.Save("YOUR_DIRECTORY/shapes.pdf");

// Inform the user
Console.WriteLine("PDF created successfully at YOUR_DIRECTORY/shapes.pdf");
```

运行程序，打开生成的文件，你会看到形状正好出现在我们定义的位置。

## 常见问题与注意事项

- **问：** *如果需要填充矩形该怎么办？*  
  **答：** 在 `RectangleShape` 初始化器中取消注释 `FillColor` 行。Aspose 支持纯色、渐变乃至图像填充。

- **问：** *可以在同一页面上绘制多个形状吗？*  
  **答：** 当然可以。只需创建额外的 `RectangleShape`、`Ellipse` 或 `Polygon` 对象，并逐一添加到 `pdfPage.Paragraphs`。

- **问：** *坐标系是否始终是左下角为原点？*  
  **答：** 是的，Aspose 遵循 PDF 规范，原点 (0,0) 位于左下角。如果你更习惯左上角为原点，需要自行计算 `y = pageHeight - desiredY`。

- **问：** *如果目标文件夹不存在会怎样？*  
  **答：** `pdfDocument.Save` 会抛出 `DirectoryNotFoundException`。请使用 `Directory.CreateDirectory` 预先创建文件夹。

## 后续步骤

既然已经掌握了 **add page to PDF**、**draw rectangle**、**add shape to PDF** 以及 **save PDF to file**，你可以在此基础上进一步扩展：

- 在形状旁插入文本、图像或表格。  
- 使用 `Graphics` 进行自由绘制（线条、弧线、自定义路径）。  
- 若有安全需求，可探索 PDF 加密或数字签名。

上述所有主题都直接基于我们刚才的代码实现，尽情实验吧。

---

**结论：** 你刚刚学习了使用 Aspose.Pdf **create PDF document C#** 的完整工作流——初始化、添加页面、绘制矩形形状并持久化文件。这是生成发票、报告、证书或任何自动化文档的坚实基石。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}