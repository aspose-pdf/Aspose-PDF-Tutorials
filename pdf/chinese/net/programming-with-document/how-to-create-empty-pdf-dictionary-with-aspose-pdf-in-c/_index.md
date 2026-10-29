---
category: general
date: 2026-09-18
description: 学习如何在 C# 中使用 Aspose.PDF 创建空的 PDF 字典。本分步指南涵盖 ExtGState、图形状态以及 CosPdfDictionary
  的操作。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.PDF
- ExtGState dictionary
- graphics state
- CosPdfDictionary
- PDF manipulation C#
language: zh
lastmod: 2026-09-18
og_description: 使用 Aspose.PDF 在 C# 中创建空的 PDF 字典。请参阅本综合教程，了解如何编辑 ExtGState 和图形状态字典。
og_image_alt: Screenshot showing creation of an empty PDF dictionary in C#
og_title: 在 C# 中创建空 PDF 字典 – 完整的 Aspose.PDF 指南
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn to create empty PDF dictionary in C# using Aspose.PDF. This step‑by‑step
    guide covers ExtGState, graphics state, and CosPdfDictionary manipulation.
  headline: How to create empty PDF dictionary with Aspose.PDF in C#
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: 如何在 C# 中使用 Aspose.PDF 创建空 PDF 字典
url: /zh/net/programming-with-document/how-to-create-empty-pdf-dictionary-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.PDF 创建空 PDF 字典

如果您在处理 PDF 文件时需要 **创建空 PDF 字典**，本指南将向您展示如何使用 Aspose.PDF for .NET 完成此操作。无论是调整透明度、混合模式，还是任何自定义图形状态，下面的步骤都能帮助您安全、高效地编辑 `ExtGState` 字典。

在本教程中，您将学习：

* 使用 Aspose.PDF 加载 PDF 文档。
* 访问第一页的资源以及现有的 `ExtGState` 字典。
* 构建一个新的空 `CosPdfDictionary` 并填充图形状态条目。
* 在不丢失原始内容的情况下保存修改后的 PDF。

该方案适用于任何至少包含一页的 PDF，并仅需 Aspose.PDF 库（版本 23.10 或更高）。

## 前置条件

* .NET 6.0 或更高（代码同样适用于 .NET Framework 4.8）。
* 引入 **Aspose.PDF** NuGet 包的引用。
* 输入 PDF 文件位于 `YOUR_DIRECTORY/input.pdf`。
* 对 C# 和 PDF 概念（如资源和图形状态）有基本了解。

> **专业提示：** 处理大型 PDF 时，建议将 `Document` 对象放在 `using` 块中，以确保及时释放所有文件句柄。

## 步骤 1：加载 PDF 文档

第一步打开源文件。Aspose.PDF 会将整个文档读取到内存中，便于您编辑内部对象。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

*为什么这很重要*：加载文档会创建可变的对象模型。没有这一步，您无法访问用于字典操作的页面资源。

## 步骤 2：获取第一页的资源

每页都有一个 `Resources` 字典，存放字体、图像和图形状态。访问它会得到一个 `DictionaryEditor`，简化读写操作。

```csharp
// Step 2: Get the resources of the first page
Page firstPage = pdfDocument.Pages[1];
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*为什么这很重要*：`ExtGState` 字典位于页面资源内部。编辑错误的字典不会对渲染产生任何影响。

## 步骤 3：定位已有的 ExtGState 字典

`ExtGState` 条目可能已经包含图形状态对象。我们将其获取为 `CosPdfDictionary`，以便后续添加新条目。

```csharp
// Step 3: Access the existing ExtGState dictionary
CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

如果 `ExtGState` 条目不存在，稍后为其分配新字典时，Aspose.PDF 会自动创建一个空字典。

## 步骤 4：**创建空 PDF 字典** 用于新的图形状态

这里我们构建一个全新的 `CosPdfDictionary`——即 **创建空 PDF 字典** 操作的核心。随后我们使用标准图形状态键填充它：

* `CA` – 描边不透明度。
* `ca` – 填充不透明度。
* `BM` – 混合模式。

```csharp
// Step 4: Create a new graphics state dictionary and define its entries
CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

KeyValuePair<string, ICosPdfPrimitive>[] graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),          // Stroke opacity
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),       // Fill opacity
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))    // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

*为什么这很重要*：通过显式定义每个条目，您可以控制页面对象的混合和渲染方式。该字典在添加这些键之前是 **空的**，这正满足了 **创建空 PDF 字典** 的要求。

## 步骤 5：将新图形状态添加到 ExtGState 字典

每个图形状态必须拥有唯一名称（例如 `GS0`）。我们将在该名称下插入刚构建好的字典。

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary with a unique name
extGStateDict.Add("GS0", graphicsStateDict);
```

如果需要多个状态，可继续添加 `GS1`、`GS2` 等条目，确保每个名称在 `ExtGState` 字典中唯一。

## 步骤 6：保存更新后的 PDF 文档

最后，将修改写回磁盘。原始文件保持不变，因为我们保存到了新路径。

```csharp
// Step 6: Save the updated PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

生成的 `output.pdf` 现在包含一个额外的图形状态（`GS0`），您可以在任意页面内容流中使用 `/GS0` 操作符进行引用。

## 完整工作示例

将所有步骤组合在一起，即可得到一个可直接运行的完整程序。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources
            Page firstPage = pdfDocument.Pages[1];
            DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Get (or create) ExtGState dictionary
            CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Build a new empty PDF dictionary for graphics state
            CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var entry in entries)
                graphicsStateDict.Add(entry);

            // Insert the new graphics state with a unique name
            extGStateDict.Add("GS0", graphicsStateDict);

            // Save the modified document
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

**预期输出**：运行程序后，`output.pdf` 的视觉内容与 `input.pdf` 相同。使用 Adobe Acrobat 或 PDF‑Tron 等工具检查 PDF 时，您会在第一页的 `ExtGState` 字典下看到新条目 `GS0`。

## 常见变体和边缘情况

| 情形 | 需要调整的内容 |
|-----------|----------------|
| **不存在 ExtGState 条目** | 将 `resourcesEditor["ExtGState"]` 替换为 `new CosPdfDictionary(pdfDocument)`，并重新赋值给 `firstPage.Resources["ExtGState"]`。 |
| **多个页面需要相同状态** | 将相同的 `GS0` 条目添加到每个页面的 `ExtGState` 字典，或从共享资源对象引用该字典。 |
| **不同的混合模式** | 将 `CosPdfName` 的值从 `"Normal"` 改为 `"Multiply"`、`"Screen"` 等，依据所需效果选择。 |
| **更高的不透明度值** | 使用 `new CosPdfNumber(0.8)` 为 `ca` 或 `CA` 提高填充或描边不透明度。 |
| **使用流操作符** | 在内容流中，在绘制操作之前写入 `"/GS0 gs"`，以应用新的图形状态。 |

## 性能考虑

* **内存使用** – 加载非常大的 PDF 时，内存占用会随页数线性增长。如果只需编辑第一页，处理完后可使用 `pdfDocument.Pages.Delete(pageNumber)` 释放资源。
* **线程安全** – Aspose.PDF 对象并非线程安全。请在单线程上进行字典编辑，或为每个线程创建独立的 `Document` 实例。

## 结论

现在，您已经掌握了如何使用 Aspose.PDF **创建空 PDF 字典**，并向其中填充图形状态条目，再将其附加到页面的 `ExtGState` 字典中。这一技术让您能够在 C# 中直接控制不透明度、混合模式以及其他渲染参数。

接下来，您可以进一步探索 **PDF manipulation C#**、为高级透明效果添加自定义 **ExtGState dictionary** 条目，或使用 **CosPdfDictionary** 修改字体、XObject 等其他资源类型。尝试创建多个图形状态，以在 PDF 中实现更复杂的视觉效果。

## 接下来您应该学习什么？

以下教程涵盖与本指南技术密切相关的主题，帮助您进一步掌握 API 功能并在项目中尝试不同实现方式。

- [使用 Aspose.PDF for .NET 创建并填充 PDF 矩形：分步指南](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)
- [使用 Aspose.PDF for .NET 创建虚线：分步指南](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [使用 Aspose.PDF for .NET 在 PDF 末尾添加空白页：分步指南](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}