---
category: general
date: 2026-09-24
description: 学习如何在 C# 中使用 Aspose.Pdf 更改 PDF 透明度。本分步指南涵盖 PDF 不透明度、混合模式和图形状态编辑。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.Pdf graphics state
- PDF opacity
- C# PDF manipulation
- blend mode PDF
- modify PDF resources
language: zh
lastmod: 2026-09-24
og_description: 使用 Aspose.Pdf 在 C# 中更改 PDF 透明度。遵循本指南编辑 PDF 的不透明度、混合模式和图形状态，以实现专业文档输出。
og_image_alt: Screenshot showing C# code that changes PDF transparency
og_title: 在 C# 中更改 PDF 透明度 – 完整的 Aspose.Pdf 指南
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Learn how to change PDF transparency in C# with Aspose.Pdf. This step‑by‑step
    guide covers PDF opacity, blend mode and graphics state editing.
  headline: How to change PDF transparency in C# using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- C#
- Aspose.Pdf
- Transparency
title: 如何使用 Aspose.Pdf 在 C# 中更改 PDF 的透明度
url: /zh/net/programming-with-operators/how-to-change-pdf-transparency-in-c-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.Pdf 更改 PDF 透明度

如果您需要在 .NET 项目中**更改 PDF 透明度**，本指南将向您展示如何使用 Aspose.Pdf 完成此操作。您将看到一个完整的可运行示例，修改 PDF 不透明度、设置混合模式，并更新页面的图形状态字典。

当您需要水印、叠加图形或自定义视觉效果时，更改 PDF 透明度是常见需求。在本教程中，您将学习编辑 **Aspose.Pdf graphics state**、调整 **PDF opacity**，以及使用 **blend mode PDF** 设置——全部使用简洁的 C# 代码。

## 前提条件

* .NET 6.0 或更高版本已安装  
* Aspose.Pdf for .NET 许可证（或临时评估密钥）  
* 一个名为 `input.pdf` 的 PDF 文件，位于您可以引用为 `YOUR_DIRECTORY` 的文件夹中  
* 对 C# 和 Visual Studio（任何 IDE 均可）有基本了解  

除了 `Aspose.Pdf` 外，无需其他 NuGet 包。由于 Aspose.Pdf 跨平台，代码可在 Windows、Linux 或 macOS 上运行。

## 更改 PDF 透明度 – 步骤 1：打开 PDF 文档

第一步是加载源 PDF。使用 `using` 块可自动释放文件句柄。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System.Collections.Generic;

string inputPath  = @"YOUR_DIRECTORY\input.pdf";
string outputPath = @"YOUR_DIRECTORY\output.pdf";

using (var document = new Document(inputPath))
{
    // The document is now ready for manipulation.
```

打开文档是任何 **C# PDF manipulation** 任务的基础。如果找不到文件，Aspose.Pdf 会抛出 `FileNotFoundException`，因此在运行代码前请再次确认路径。

## 使用 Aspose.Pdf graphics state 访问页面资源

接下来，获取第一页及其资源字典。资源字典包含字体、图像以及控制图形参数的 **ExtGState** 条目等对象。

```csharp
    // Step 2: Get the first page of the document
    var page = document.Pages[1];

    // Step 3: Access the page's resource dictionary for editing
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

`DictionaryEditor` 类提供了一个便捷的包装器，用于读取和写入 PDF 字典。这里我们关注 **ExtGState** 字典，因为它存储透明度设置。

## 为 PDF 不透明度创建并配置新的 graphics state

现在我们构建一个全新的 graphics state 字典。该字典将保存定义描边不透明度 (`CA`)、填充不透明度 (`ca`) 和混合模式 (`BM`) 的参数。

```csharp
    // Step 4: Retrieve the existing ExtGState dictionary (graphics states)
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

    // Step 5: Create a new empty graphics state dictionary
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

    // Step 6: Define graphics state parameters (stroke opacity, fill opacity, blend mode)
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),            // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),          // Fill opacity (50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))       // Blend mode PDF (standard normal blending)
    };

    // Step 7: Add each parameter to the new graphics state dictionary
    foreach (var param in parameters)
        newGraphicsState.Add(param);
```

* **`CA`** 控制描边操作（线条、边框）的不透明度。  
* **`ca`** 控制填充操作（填充形状、文本）的不透明度。  
* **`BM`** 选择混合模式；默认是 `"Normal"`，但您可以使用 `"Multiply"` 或 `"Screen"` 来实现艺术效果。  

这些设置是 **PDF opacity** 操作的核心。根据您的视觉设计调整数值——`0` 表示完全透明，`1` 表示完全不透明。

## 插入 graphics state 并保存文档

构建新状态后，我们将其以唯一名称 (`GS0`) 添加到现有的 **ExtGState** 字典中。最后，保存修改后的 PDF。

```csharp
    // Step 8: Insert the new graphics state into the ExtGState dictionary with a name
    extGState.Add("GS0", newGraphicsState);

    // Step 9: Save the modified PDF document
    document.Save(outputPath);
}
```

当在查看器中打开 PDF 时，任何引用 `GS0` 的内容都会以定义的透明度渲染。您以后可以使用绘图命令的 `GraphicsState` 属性将此 graphics state 应用于特定对象（例如 `page.Contents.Add(new TextFragment(...){ GraphicsState = "GS0" })`）。

## 验证结果

在 Adobe Acrobat Reader、Foxit 或任何支持透明度的 PDF 查看器中打开 `output.pdf`。您应该看到第一页的填充元素以 50 % 不透明度渲染，而描边保持完全不透明。如果未看到变化，请确保页面实际使用了新的 graphics state——否则，您可以显式将 `GS0` 分配给想要影响的对象。

![在 C# 中更改 PDF 透明度的代码示例](path/to/image.png){: .img-responsive alt="在 C# 中更改 PDF 透明度的代码示例"}

*上图展示了更改 PDF 透明度的完整 C# 源代码。*

## 常见变体和边缘情况

| 情况 | 如何调整代码 |
|-----------|-----------------------|
| **多页** | 遍历 `document.Pages`，对每页重复步骤 2‑8。 |
| **不同的混合模式** | 将 `"Normal"` 替换为 `"Multiply"`、`"Screen"` 或任何 PDF 标准的混合模式名称。 |
| **更高的填充不透明度** | 将 `new CosPdfNumber(0.5)` 更改为介于 `0` 和 `1` 之间的值。 |
| **不存在的 ExtGState** | 如果 `resourcesEditor["ExtGState"]` 返回 `null`，则创建新字典：`var extGState = CosPdfDictionary.CreateEmptyDictionary(document); resourcesEditor["ExtGState"] = extGState;` |

这些变体展示了使用 Aspose.Pdf **modify PDF resources** 的灵活性。通过调整参数，您可以在 PDF 中生成水印、半透明叠加层或自定义 UI 元素。

## 完整、可运行的示例

下面是完整的程序，您可以将其复制粘贴到新的控制台应用项目中。它包含所有必要的 `using` 指令、错误处理和注释。



## 接下来您应该学习什么？

以下教程涵盖与本指南技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能，并在自己的项目中探索替代实现方案。

- [使用 Aspose.PDF 更改 PDF 不透明度 – 完整 C# 指南](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [在 C# 中更改 PDF 不透明度 – 完整 Aspose 指南](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-in-c-complete-aspose-guide/)
- [使用 Aspose 为 PDF 添加透明度 – 完整 C# 指南](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}