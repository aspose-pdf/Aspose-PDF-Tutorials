---
category: general
date: 2026-10-13
description: 了解如何使用 Aspose.Pdf for C# 在 PDF 中设置透明度。还可以查看如何保存修改后的 PDF 并更改填充透明度。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set transparency
- save modified pdf
- change fill alpha
- set fill opacity
- edit pdf resources
language: zh
lastmod: 2026-10-13
og_description: 如何在使用 Aspose.Pdf for C# 的 PDF 中设置透明度。请按照本指南编辑 PDF 资源、更改填充透明度，并保存修改后的
  PDF 文件。
og_image_alt: Screenshot of a PDF page showing transparent graphics applied with Aspose.Pdf
  in C#
og_title: 使用 Aspose.Pdf C# 在 PDF 中设置透明度 – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  headline: How to set transparency in a PDF with Aspose.Pdf C#
  type: TechArticle
- description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  name: How to set transparency in a PDF with Aspose.Pdf C#
  steps:
  - name: Load the PDF document
    text: '```csharp using Aspose.Pdf; using System.Collections.Generic;'
  - name: Edit PDF resources to add a graphics state
    text: '```csharp // Get the first page (pages are 1‑based) Page firstPage = pdfDocument.Pages[1];'
  - name: Change fill alpha and set fill opacity
    text: '```csharp // Create an empty graphics state dictionary CosPdfDictionary
      newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);'
  - name: Add the new graphics state to the ExtGState dictionary
    text: '```csharp // Register the new state under the name "GS0" extGStateDict.Add("GS0",
      newGraphicsState); ```'
  - name: (Optional) Apply the graphics state in a content stream
    text: 'If you want to draw a rectangle using the new fill opacity, add the following
      after the previous steps:'
  - name: Save modified PDF
    text: '```csharp // Persist the changes to a new file pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
      ```'
  - name: Next steps
    text: '* Explore other blend modes (`Multiply`, `Screen`, etc.) by changing the
      `BM` entry. * Adjust stroke alpha (`CA`) to create semi‑transparent outlines.
      * Combine multiple graphics states to build a library of reusable visual effects.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- Transparency
title: 如何使用 Aspose.Pdf C# 在 PDF 中设置透明度
url: /zh/net/images-graphics/how-to-set-transparency-in-a-pdf-with-aspose-pdf-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 PDF 中使用 Aspose.Pdf C# 设置透明度

如果您需要在使用 C# 的 PDF 中设置透明度，本教程将展示具体步骤。您还将学习如何在不离开 Aspose.Pdf 环境的情况下保存修改后的 PDF 文件并更改填充透明度。

本指南将演示加载文档、编辑 PDF 资源、创建定义填充不透明度的图形状态以及持久化更改的全过程。无需外部工具；所有操作均在标准 .NET 项目中完成。

## 前置条件

在开始之前，请确保您已具备：

* 已安装 .NET 6.0 或更高版本  
* 有效的 Aspose.Pdf for .NET 许可证（或免费评估密钥）  
* 已知目录中的输入 PDF 文件  

您可以通过 NuGet 添加 Aspose.Pdf 包：

```bash
dotnet add package Aspose.Pdf
```

## 如何在 PDF 中设置透明度

本节包含核心实现。每一步都会解释 **为什么** 需要该代码，而不仅仅是 **做了什么**。

### 步骤 1：加载 PDF 文档

```csharp
using Aspose.Pdf;
using System.Collections.Generic;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*为什么这一步？*  
`Document` 表示内存中的整个 PDF 文件。打开文件后，您即可访问页面、资源以及将要修改的底层对象。

### 步骤 2：编辑 PDF 资源以添加图形状态

```csharp
// Get the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];

// Create an editor for the page's resource dictionary
DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);

// Retrieve the ExtGState dictionary; it holds graphics state objects
CosPdfDictionary extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
```

*为什么这一步？*  
PDF 页面在资源字典中存储可复用对象——字体、图像和图形状态。`ExtGState` 条目包含透明度设置。通过编辑此字典，您可以引入页面可以引用的新状态。

### 步骤 3：更改填充 alpha 并设置填充不透明度

```csharp
// Create an empty graphics state dictionary
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the graphics state entries
var graphicsStateEntries = new[]
{
    // Stroke alpha (CA) – fully opaque
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    // Fill alpha (ca) – 50 % transparent
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // Blend mode (BM) – normal composition
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

// Populate the new graphics state
foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*为什么这一步？*  
`ca` 控制 **填充不透明度**，而 `CA` 控制 **描边不透明度**。将 `ca` 设置为 `0.5` 可使填充形状的透明度为 50 %。`BM` 条目选择混合模式；`"Normal"` 是标准透明度最常用的选择。

### 步骤 4：将新图形状态添加到 ExtGState 字典

```csharp
// Register the new state under the name "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

*为什么这一步？*  
为图形状态命名（`"GS0"`）后，页面内容流即可使用 `gs` 操作符引用它。完成注册后，页面即可应用您刚定义的透明度。

### 步骤 5：（可选）在内容流中应用图形状态

如果您想使用新填充不透明度绘制矩形，请在前面的步骤之后添加以下代码：

```csharp
// Create a content stream that uses the new graphics state
string cs = @"
q               % Save graphics state
/GS0 gs         % Apply the graphics state defined earlier
0 0 200 100 re  % Define a rectangle (x, y, width, height)
0.2 0.6 0.8 rg  % Set fill color (RGB)
f               % Fill the rectangle using the current graphics state
Q               % Restore graphics state
";

firstPage.Contents.Add(new Aspose.Pdf.Operator.GsContent(cs));
```

*为什么这一步？*  
`q`/`Q` 操作符用于保存和恢复图形状态，确保透明度仅影响预期的绘图指令。`gs` 操作符切换到名为 `"GS0"` 的图形状态。

### 步骤 6：保存修改后的 PDF

```csharp
// Persist the changes to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*为什么这一步？*  
保存操作会将更新后的资源字典和任何新内容流写入磁盘。生成的文件（`output.pdf`）包含前一步定义的透明矩形。

## 完整可运行示例

将上述代码组合起来，下面是一个可以编译运行的完整程序：

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using System.Collections.Generic;

class SetTransparencyDemo
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Access the first page and its resources
        Page firstPage = pdfDocument.Pages[1];
        var resourceEditor = new DictionaryEditor(firstPage.Resources);
        var extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();

        // Create a new graphics state with 50 % fill opacity
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var graphicsStateEntries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke alpha
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill alpha
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var entry in graphicsStateEntries)
            newGraphicsState.Add(entry);

        // Register the graphics state as "GS0"
        extGStateDict.Add("GS0", newGraphicsState);

        // Optional: draw a rectangle using the new transparency
        string cs = @"
q
/GS0 gs
0 0 200 100 re
0.2 0.6 0.8 rg
f
Q
";
        firstPage.Contents.Add(new GsContent(cs));

        // Save the modified PDF
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

**预期结果** – `output.pdf` 显示一个填充淡紫色、透明度为 50 % 的矩形，背景内容可以部分可见。

## 常见问题与边缘情况

* **我可以更改描边不透明度而不是填充不透明度吗？**  
  将 `CA`（大写）设置为 `0`（完全透明）到 `1`（完全不透明）之间的数值。示例中已将 `CA` 设置为 `1`，因此描边保持不透明。

* **如果页面尚未拥有 ExtGState 字典怎么办？**  
  `resourceEditor["ExtGState"]` 会自动创建一个空字典。向其中添加 `"GS0"` 的方式相同。

* **图形状态可以在多个页面之间复用吗？**  
  可以。只要将条目添加到文档的资源字典，任何引用 `"GS0"` 的页面都会继承相同的透明度设置。

* **这种方式与使用高级 `Graphics` API 有何不同？**  
  编辑底层资源字典可让您精确控制 PDF 内部结构，并且由于避免嵌入额外对象，生成的文件更小。

## 结论

现在您已经掌握了使用 Aspose.Pdf for C# **在 PDF 中设置透明度** 的方法。教程涵盖了编辑 PDF 资源、修改填充 alpha、设置填充不透明度以及保存修改后的 PDF。基于此，您可以尝试不同的混合模式、对文本应用透明度，或为复杂文档创建可复用的图形状态。

### 后续步骤

* 通过更改 `BM` 条目探索其他混合模式（`Multiply`、`Screen` 等）。  
* 调整描边 alpha（`CA`）以创建半透明轮廓。  
* 组合多个图形状态，构建可复用的视觉效果库。  

欢迎在评论区分享您的成果或提问。祝编码愉快！

## 接下来应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式，每篇资源均提供完整可运行的代码示例和逐步说明。

- [如何使用 Aspose.PDF for .NET 定制 PDF：设置页面边距并绘制线条](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [如何使用 Aspose-PDF for .NET 在 PDF 中设置图像大小](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [如何使用 Aspose.PDF for .NET 设置 PDF 权限：完整指南](/pdf/english/net/security-permissions/set-pdf-privileges-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}