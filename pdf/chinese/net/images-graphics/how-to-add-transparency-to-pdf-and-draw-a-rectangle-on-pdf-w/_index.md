---
category: general
date: 2026-09-12
description: 学习如何在 PDF 中添加透明度、在 PDF 上绘制矩形，并使用 Aspose.PDF 在 C# 中保存具有透明度的 PDF——一步一步的指南。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- draw rectangle on pdf
- save pdf with transparency
language: zh
lastmod: 2026-09-12
og_description: 使用 Aspose.PDF 在 C# 中为 PDF 添加透明度、在 PDF 上绘制矩形，并保存带透明度的 PDF。请参阅完整教程。
og_image_alt: Screenshot of a PDF page showing a semi‑transparent rectangle drawn
  with Aspose.PDF
og_title: 为 PDF 添加透明度并在 PDF 上绘制矩形 – 完整 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-09-12'
  description: Learn how to add transparency to PDF, draw a rectangle on PDF, and
    save PDF with transparency using Aspose.PDF in C# – step‑by‑step guide.
  headline: How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: 如何在 PDF 中添加透明度并使用 Aspose.PDF 绘制矩形
url: /zh/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 PDF 中添加透明度并使用 Aspose.PDF 绘制矩形

如果您需要 **向 PDF 添加透明度**，本指南将向您展示如何在 C# 中实现。您还将学习如何 **在 PDF 上绘制矩形**，以及最终 **保存带有透明度的 PDF**，以便在报告、发票或任何文档自动化工作流中重复使用。

在本教程中，您将：

* 加载现有的 PDF 文档。
* 创建自定义图形状态，以定义描边和填充的不透明度。
* 将该图形状态应用到画布并绘制矩形。
* 保存修改后的文件，同时保留透明度设置。

无需任何外部工具，只需使用 Aspose.PDF for .NET 库，并且每行代码都有解释，让您了解每一步的 *原因*。

## 前提条件

* .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.7+）。
* 已授权或评估版的 **Aspose.PDF for .NET**。通过 NuGet 安装：

```bash
dotnet add package Aspose.Pdf
```

* 将输入 PDF（`input.pdf`）放置在项目可以引用的文件夹中。

## 步骤 1：加载 PDF 文档

第一步是打开源文件。使用 `using` 语句可确保文档被正确释放，避免在后续保存时出现文件锁定问题。

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";
using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

*Why this matters*: 加载文档后，您即可访问页面集合、资源字典以及绘图所需的画布对象。

## 步骤 2：访问第一页的资源字典

每个 PDF 页面都有一个 **资源字典**，用于存储字体、图像和图形状态等对象。要引入新的透明度设置，需要编辑 `ExtGState` 条目。

```csharp
// Step 2: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

*Why this matters*: `DictionaryEditor` 让我们能够读取和修改底层 PDF 对象，而不会破坏文档结构。

## 步骤 3：创建带有透明度值的自定义图形状态

图形状态（`ExtGState`）控制绘图操作的渲染方式。我们定义两个不透明度参数：

* **CA** – 描边不透明度（形状的轮廓）。
* **ca** – 填充不透明度（形状的内部）。

我们还将混合模式（`BM`）设置为 “Normal”，这是最常用的合成操作。

```csharp
// Step 3: Create a custom graphics state (ExtGState) with transparency settings
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
var customGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "CA", new Aspose.Pdf.Cos.CosPdfNumber(1)),          // stroke opacity = 100 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),        // fill opacity = 50 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))      // normal blend mode
};

foreach (var p in parameters)
    customGs.Add(p);

// Register the new graphics state under the name "GS0"
extGStateDict.Add("GS0", customGs);
```

*Why this matters*: 将 `GS0` 添加到 `ExtGState` 字典后，我们创建了一个可复用的引用，画布在绘制前可以激活它。`0.5` 的填充不透明度使矩形半透明，从而实现 **向 PDF 添加透明度** 的目标。

## 步骤 4：应用图形状态并绘制矩形

现在我们让页面的画布使用刚才创建的图形状态，然后绘制矩形。坐标遵循 PDF 坐标系（原点位于左下角）。

```csharp
// Step 4: Apply the custom graphics state and draw a rectangle
var canvas = firstPage.Canvas;

// Activate the transparency graphics state
canvas.SetGraphicsState("GS0");

// Draw a rectangle from (100, 500) to (200, 600)
canvas.Rectangle(100, 500, 200, 600);

// Render the rectangle outline using the current graphics state
canvas.Stroke();
```

*Why this matters*: `SetGraphicsState("GS0")` 将绘图上下文切换到之前定义的透明度设置。`Rectangle` 方法定义形状，`Stroke` 使用指定的不透明度渲染轮廓。如果还需要填充矩形，请将 `Stroke()` 替换为 `FillAndStroke()`。

## 步骤 5：保存修改后的 PDF 并保留透明度

最后，将文档写回磁盘。输出文件包含新的图形状态、绘制的矩形以及透明度信息。

```csharp
// Step 5: Save the modified PDF
string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
pdfDocument.Save(outputPath);
```

*Why this matters*: 保存文档会最终确定所有更改。生成的文件可在任何 PDF 查看器中打开，矩形将以 50 % 填充不透明度显示。

### 预期结果

打开 `output_with_extgstate.pdf` 时，您应看到一个矩形，其边框完全不透明，而内部半透明，能够透视底层页面内容。

## 边缘情况和实用技巧

| 情况 | 推荐的调整 |
|-----------|------------------------|
| **多页文档** | 对 `pdfDocument.Pages` 进行循环，并对每个目标页重复步骤 2‑4。 |
| **不同的不透明度值** | 将 `CA`（描边）和 `ca`（填充）的 `CosPdfNumber` 值改为 `0`（完全透明）到 `1`（完全不透明）之间的任意数值。 |
| **自定义混合模式** | 将 `"Normal"` 替换为 `"Multiply"`、`"Screen"` 或任何 PDF 标准支持的混合模式。 |
| **填充矩形** | 调用 `canvas.FillAndStroke()` 而不是 `canvas.Stroke()`，以同时应用填充和轮廓。 |
| **重复使用同一图形状态** | 在同一页面上绘制任意数量的形状前，都可以调用 `canvas.SetGraphicsState("GS0")`。 |

**专业提示：** 在添加新的 `ExtGState` 后，务必检查资源字典。如果字典不存在，请先创建它：

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
    resourcesEditor.Add("ExtGState", new Aspose.Pdf.Cos.CosPdfDictionary(pdfDocument));
```

## 完整、可运行的示例

下面是一个独立的程序示例，您可以直接复制到控制台应用程序中运行（将 `YOUR_DIRECTORY` 替换为实际路径）。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF document
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Access the first page’s resources
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        if (!resourcesEditor.ContainsKey("ExtGState"))
            resourcesEditor.Add("ExtGState", new CosPdfDictionary(pdfDocument));

        // 3️⃣ Create a custom graphics state with transparency
        var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        var customGs = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };

        foreach (var p in parameters)
            customGs.Add(p);

        extGStateDict.Add("GS0", customGs);

        // 4️⃣ Apply the graphics state and draw a rectangle
        var canvas = firstPage.Canvas;
        canvas.SetGraphicsState("GS0");
        canvas.Rectangle(100, 500, 200, 600);
        canvas.Stroke(); // use FillAndStroke() for a filled shape

        // 5️⃣ Save the PDF with transparency
        string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine("PDF saved with a transparent rectangle at: " + outputPath);
    }
}
```

运行程序后会生成 `output_with_extgstate.pdf`，演示了 **向 PDF 添加透明度**、**在 PDF 上绘制矩形**以及**保存带透明度的 PDF**的完整流程。

## 结论

现在，您已经掌握了使用 Aspose.PDF for .NET **向 PDF 添加透明度**、**在 PDF 上绘制矩形**以及**保存带透明度的 PDF**的技巧。整个过程围绕创建自定义 `ExtGState`、将其应用到画布并持久化更改展开。凭借这些基础，您可以将该技术扩展到其他形状、多页文档或动态不透明度值。

**后续步骤**

* 探索其他绘图原语，如 `canvas.Ellipse`、`canvas.Path` 或 `canvas.TextFragment`，并复用相同的图形状态。
* 将透明度与图像叠加相结合，创建水印（`canvas.Image` + 自定义 `ExtGState`）。
* 查阅 Aspose.PDF 文档中关于 **graphics state parameters** 的章节，了解高级合成效果。

祝编码愉快，尽情享受透明度为 PDF 工作流带来的视觉灵活性！

## 接下来应该学习什么？

以下教程涵盖了与本指南技术密切相关的主题，可帮助您进一步掌握 API 功能并在项目中探索替代实现方案。每个资源都提供完整的可运行代码示例和逐步解释。

- [如何在 C# 中创建 PDF – 添加页面、绘制矩形并保存](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [使用 Aspose.PDF for .NET 在 PDF 中添加线对象的分步指南](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [使用 Aspose.PDF for .NET 向 PDF 添加图像水印的分步指南](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}