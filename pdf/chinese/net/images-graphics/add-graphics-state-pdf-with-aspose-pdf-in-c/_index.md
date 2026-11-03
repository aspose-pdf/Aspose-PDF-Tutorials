---
category: general
date: 2026-10-07
description: 使用 Aspose.Pdf 在 C# 中添加图形状态 PDF，以修改 PDF 透明度。请按照本分步指南嵌入自定义图形状态并控制不透明度。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- modify pdf transparency
language: zh
lastmod: 2026-10-07
og_description: 使用 Aspose.Pdf 在 C# 中添加图形状态 PDF。了解如何通过创建自定义图形状态字典来修改 PDF 的透明度。
og_image_alt: Screenshot showing the add graphics state pdf code editor in Visual
  Studio
og_title: 使用 Aspose.Pdf 添加图形状态 PDF – 控制 PDF 透明度
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Add graphics state pdf using Aspose.Pdf in C# to modify PDF transparency.
    Follow this step‑by‑step guide to embed custom graphics states and control opacity.
  headline: Add graphics state pdf with Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: 在 C# 中使用 Aspose.Pdf 添加图形状态 PDF
url: /zh/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Pdf 在 C# 中添加图形状态 PDF

如果您需要在文档中**添加图形状态 PDF**，本教程将向您展示如何使用 Aspose.Pdf for .NET 完成此操作。完成本指南后，您还将了解如何**修改 PDF 透明度**，从而能够为任何绘图操作设置自定义的不透明度值。

使用 PDF 图形状态可以控制诸如线宽、混合模式等参数，本文最重要的就是内容的透明度。以下步骤面向熟悉 C# 的开发者，提供一个可直接运行的解决方案，无需深入官方 SDK 文档。

## 您将学到

* 如何创建一个新的图形状态字典并使用 `CA`、`ca` 和 `BM` 条目进行填充。  
* 如何将该字典插入页面的 `ExtGState` 资源，使 PDF 能识别它。  
* `ca`（描边）和 `CA`（填充）值如何影响后续绘图指令的**修改 PDF 透明度**。  
* 常见陷阱，如命名冲突和版本兼容性，以及后续扩展图形状态的专业技巧。

**先决条件**

* .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.7+）。  
* 有效的 Aspose.Pdf for .NET 许可证（免费评估版可用于测试）。  
* Visual Studio 2022 或您喜欢的任何 C# IDE。  

---

## 步骤 1：安装 Aspose.Pdf for .NET

将 NuGet 包添加到您的项目中：

```bash
dotnet add package Aspose.Pdf
```

该包包含 `Aspose.Pdf` 命名空间，提供后续使用的 `Document`、`DictionaryEditor` 和 `CosPdfDictionary` 类。

> **专业提示：** 如果您计划批量处理大量 PDF，请在 `Program.cs` 中尽早启用 **License**，以避免评估水印。

```csharp
// Apply your license (optional for evaluation)
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Aspose.Pdf.lic");
```

## 步骤 2：定义输入和输出路径

您必须将 SDK 指向已有的 PDF（`input.pdf`），并指定修改后文件的保存位置（`output.pdf`）。

```csharp
// Define input and output PDF file paths
string inputPath = @"C:\MyPdfs\input.pdf";
string outputPath = @"C:\MyPdfs\output.pdf";
```

> **原因说明：** 使用绝对路径可防止 SDK 在错误的工作目录中查找，这是导致 `FileNotFoundException` 的常见原因。

## 步骤 3：打开 PDF 并定位第一页的资源

`ExtGState` 字典位于每页的资源字典中。为简化演示，我们将编辑第一页，但相同方法适用于任何页面索引。

```csharp
using (var pdfDocument = new Aspose.Pdf.Document(inputPath))
{
    // Get the first page (pages are 1‑based)
    var firstPage = pdfDocument.Pages[1];

    // Access the page’s resource dictionary via DictionaryEditor
    var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);

    // Retrieve (or create) the ExtGState entry
    var extGStateDict = resourcesEditor["ExtGState"]
        .ToCosPdfDictionary(); // Throws if ExtGState does not exist
```

**边缘情况：** 如果页面没有 `ExtGState` 条目，需要创建它：

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
{
    var emptyDict = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", emptyDict);
    extGStateDict = emptyDict;
}
```

## 步骤 4：构建新的图形状态字典

图形状态是一组键/值对，用于描述绘图操作的行为。实现透明度我们需要以下三个键：

| Key | 含义 | 典型值 |
|-----|------|--------|
| `CA` | 填充不透明度 (0 = 透明, 1 = 不透明) | `1`（完全不透明） |
| `ca` | 描边不透明度（相同尺度） | `0.5`（50 % 透明） |
| `BM` | 混合模式（例如 `Normal`, `Multiply`） | `Normal` |

```csharp
    // Create an empty dictionary that will hold the graphics state
    var newGraphicsState = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Populate the dictionary with transparency and blend mode entries
    var graphicsStateEntries = new[]
    {
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "CA", new Aspose.Pdf.CosPdfNumber(1)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "ca", new Aspose.Pdf.CosPdfNumber(0.5)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "BM", new Aspose.Pdf.CosPdfName("Normal"))
    };

    foreach (var entry in graphicsStateEntries)
        newGraphicsState.Add(entry);
```

**为什么使用这些值？**  
`ca = 0.5` 使任何描边路径（线条、边框）以 50 % 不透明度显示，而 `CA = 1` 则保持填充形状完全不透明。根据需要调整这两个数值，以实现精确的**修改 PDF 透明度**效果。

## 步骤 5：将图形状态插入 ExtGState 字典

您必须为新状态指定唯一名称（例如 `GS0`）。如果该名称已存在，Aspose.Pdf 将覆盖已有条目，可能导致依赖该状态的其他内容出错。

```csharp
    // Add the new graphics state under a custom name
    const string stateName = "GS0";

    // Ensure we don’t clash with an existing entry
    if (extGStateDict.ContainsKey(stateName))
        extGStateDict.Remove(stateName);

    extGStateDict.Add(stateName, newGraphicsState);
```

现在页面资源已包含 `GS0`。若要实际使用它，需要在内容流中通过 `gs` 操作符引用该图形状态（例如 `GS0 gs`）。如果需要绘制自定义形状，Aspose.Pdf 允许您注入原始 PDF 操作符。

## 步骤 6：保存修改后的 PDF

```csharp
    // Persist the changes to a new file
    pdfDocument.Save(outputPath);
}
```

生成的 `output.pdf` 与原文件在视觉内容上保持一致，但随后选择 `GS0` 的任何绘图指令都会遵循您定义的透明度设置。

### 预期结果

在 Adobe Acrobat 或任意 PDF 查看器中打开 `output.pdf`。如果使用 `GS0` 图形状态添加新的描边线（例如通过 `pdfDocument.Pages[1].Contents.Add(...)`），该线条将呈现半透明效果，而填充仍保持不透明。这表明您已成功**添加图形状态 PDF**并**修改 PDF 透明度**。

---

## 完整可运行示例

下面是完整的程序示例，您可以复制粘贴到控制台应用中。示例包括许可证加载、错误处理以及解释每个非显而易见步骤的注释。



## 接下来您应该学习什么？

以下教程涵盖与本指南技术密切相关的主题，帮助您进一步学习。每篇资源都提供完整的可运行代码示例和逐步说明，助您掌握更多 API 功能并在项目中探索替代实现方案。

- [使用 Aspose PDF 在 C# 中为 PDF 添加透明度 – 步骤指南](/pdf/english/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [使用 Aspose 为 PDF 添加透明度 – 完整 C# 指南](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [使用 Aspose.PDF for .NET 为 PDF 添加图像水印的完整指南](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}