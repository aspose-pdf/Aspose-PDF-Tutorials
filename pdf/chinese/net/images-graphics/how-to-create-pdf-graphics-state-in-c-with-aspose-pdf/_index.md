---
category: general
date: 2026-11-16
description: 学习如何在 C# 中使用 Aspose.Pdf 创建 PDF 图形状态。本指南涵盖不透明度、混合模式以及完整代码示例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf graphics state
- Aspose.Pdf ExtGState
- PDF opacity
- C# PDF manipulation
- PDF blend mode
- Aspose.Pdf graphics state
language: zh
lastmod: 2026-11-16
og_description: 使用 Aspose.Pdf 在 C# 中创建 PDF 图形状态。请遵循本完整教程，以编程方式设置不透明度和混合模式。
og_image_alt: Illustration of how to create PDF graphics state with Aspose.Pdf in
  C#
og_title: 在 C# 中创建 PDF 图形状态 – Aspose.Pdf 分步指南
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to create PDF graphics state in C# using Aspose.Pdf. This
    guide covers opacity, blend mode, and full code example.
  headline: How to create PDF graphics state in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF
title: 如何在 C# 中使用 Aspose.Pdf 创建 PDF 图形状态
url: /zh/net/images-graphics/how-to-create-pdf-graphics-state-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.Pdf 创建 PDF 图形状态

如果您需要在 .NET 项目中 **创建 PDF 图形状态**，本教程将向您展示如何使用 Aspose.Pdf 完成此操作。无论是控制不透明度、修改混合模式，还是在页面之间复用自定义图形状态，下面的步骤都提供了一个完整、可直接运行的解决方案。

在本指南中，您将学习如何访问页面资源、添加 **ExtGState** 条目，并将更改持久化到新文件。示例适用于 Aspose.Pdf 23.12（或更高版本），目标为 .NET 6+，但概念同样适用于更早的版本。

## 前置条件

在开始之前，请确保您具备以下条件：

* 已安装 .NET 6 SDK 的 Visual Studio 2022（或任意 C# IDE）。  
* 拥有 Aspose.Pdf for .NET 授权或临时评估密钥。  
* 将名为 `input.pdf` 的 PDF 文件放置在代码可引用的文件夹中。  

除 `Aspose.Pdf` 之外，无需其他 NuGet 包。

## 本教程涵盖的内容

* 加载已有的 PDF 文档。  
* 访问第一页的资源字典。  
* 创建一个定义描边不透明度（`CA`）、填充不透明度（`ca`）和混合模式（`BM`）的新图形状态字典。  
* 使用自定义名称（`GS0`）将新图形状态添加到 **ExtGState** 集合。  
* 保存更新后的 PDF，以便后续绘图指令能够引用该新状态。

完成本教程后，您将能够以编程方式 **创建 PDF 图形状态** 对象，并在任何绘图操作中复用它们。

## 步骤 1：设置项目并导入命名空间

创建一个新的控制台应用程序（或将代码集成到现有项目中）。添加 Aspose.Pdf 引用并包含所需的命名空间：

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Generator;
```

> **小贴士：** 如果使用免费评估版，请在加载文档之前添加 `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` 以避免出现水印提示。

## 步骤 2：加载 PDF 文档

打开文件非常直接。`Document` 类代表整个 PDF，并提供对其页面和资源的访问。

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";

using (var document = new Document(inputPath))
{
    // All subsequent steps run inside this using block
```

将代码放在 `using` 块中可确保在操作完成后释放文件句柄，这对于生产环境中的 **C# PDF 操作** 至关重要。

## 步骤 3：获取第一页的资源字典

每个 PDF 页面都有一个 *Resources* 字典，用于存储字体、图像和图形状态。我们需要一个 `DictionaryEditor` 来编辑该结构。

```csharp
    // Step 3: Get the first page and its resources dictionary
    var page = document.Pages[1];
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

如果 PDF 已经包含 `ExtGState` 条目，`resourcesEditor["ExtGState"]` 将返回它；否则，当我们添加第一个条目时，Aspose.Pdf 会为我们创建一个空字典。

## 步骤 4：访问或创建 ExtGState 字典

**ExtGState** 字典保存具名的图形状态对象。我们要么获取已有的字典，要么创建一个新的容器。

```csharp
    // Step 4: Access (or create) the ExtGState dictionary within the resources
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

当 `ExtGState` 不存在时，`resourcesEditor["ExtGState"]` 会自动返回一个新的空字典，确保代码对任何 PDF 都有效。

## 步骤 5：构建新的图形状态字典

图形状态是一个带有特定键的 `CosPdfDictionary`：

* `CA` – 描边不透明度（0‑1）  
* `ca` – 填充不透明度（0‑1）  
* `BM` – 混合模式（`Normal`、`Multiply` 等）

我们创建一个空字典，填充后再将其添加到 `ExtGState`。

```csharp
    // Step 5: Create a new graphics state dictionary with desired parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (50% transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };

    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

您可以将 `0.5` 改为 0 到 1 之间的任意值以调整填充不透明度，或将 `"Normal"` 替换为 `"Multiply"` 以使用不同的 **PDF 混合模式**。正是这种灵活性，使得创建自定义图形状态成为 **Aspose.Pdf 图形状态** 处理中的强大技巧。

## 步骤 6：使用名称注册图形状态

PDF 内容流通过名称引用图形状态。这里我们使用 `GS0`，但任何唯一名称都可以。

```csharp
    // Step 6: Add the new graphics state to the ExtGState dictionary with a name (e.g., GS0)
    extGState.Add("GS0", newGraphicsState);
```

如果需要多个状态，只需使用不同的参数重复创建步骤，并分别命名为 `GS1`、`GS2` 等。这种模式在需要对不同图层设置不同不透明度或混合模式的复杂文档中表现良好。

## 步骤 7：保存修改后的 PDF

最后，将更新后的文档写入新文件。保留原始文件有助于调试。

```csharp
    // Step 7: Save the updated PDF document
    string outputPath = @"YOUR_DIRECTORY\output.pdf";
    document.Save(outputPath);
}
```

执行后，`output.pdf` 将包含名为 `GS0` 的 `ExtGState` 条目。任何后续的绘图操作都可以使用 `gs` 操作符引用它（例如，在内容流中使用 `GS0 gs`）。  

> **为何重要：** 通过创建可复用的图形状态，您可以避免在每个绘图指令中重复设置不透明度和混合模式，从而提升性能并降低维护成本。

## 在内容流中使用新图形状态（可选）

如果想立即看到效果，可以添加一个使用刚才创建的状态的简单矩形：

```csharp
using (var document = new Document(outputPath))
{
    var page = document.Pages[1];
    var content = page.Contents[1]; // Get the first content stream

    // Insert graphics state selection and a semi‑transparent rectangle
    var operators = new List<Operator>
    {
        new Operator("GS0", "gs"),                     // Select our custom graphics state
        new Operator("0.5", "w"),                      // Set line width (optional)
        new Operator("100", "100", "200", "150", "re"), // Rectangle (x, y, width, height)
        new Operator("B")                              // Stroke the rectangle
    };

    foreach (var op in operators)
        content.Operators.Add(op);

    document.Save(@"YOUR_DIRECTORY\final_output.pdf");
}
```

该矩形将在填充时使用 50 % 不透明度，而描边保持完全不透明，正如 **创建 PDF 图形状态** 字典中所定义的那样。

## 常见陷阱及规避方法

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| 未找到 `ExtGState` 条目 | 某些 PDF 完全省略了该字典。 | 当您添加第一个条目时，`DictionaryEditor` 会自动创建它，无需额外检查。 |
| 不透明度值大于 1 或小于 0 | PDF 规范将不透明度限制在 `[0,1]` 范围。 | 在创建 `CosPdfNumber` 前对数值进行截断。 |
| 混合模式拼写错误 | PDF 混合模式名称区分大小写。 | 使用精确名称，如 `"Normal"`、`"Multiply"`、`"Screen"`。 |
| 许可证水印 | 评估版会在首页添加水印。 | 在打开文档前加载有效的许可证文件。 |

处理好这些边界情况，可确保您的 **创建 PDF 图形状态** 实现能够在各种 PDF 源上可靠运行。

## 完整、可运行的示例

下面是一个完整的自包含程序，您可以直接复制、粘贴并运行。请将 `YOUR_DIRECTORY` 替换为您机器上的实际文件夹路径。

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;

class Program
{
    static void Main()
    {
        // Optional: apply license to remove evaluation watermark
        // var license = new Aspose.Pdf.License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        using (var document = new Document(inputPath))
        {
            // 1️⃣ Get first page and its resources
            var page = document.Pages[1];
            var resourcesEditor = new DictionaryEditor(page.Resources);

            // 2️⃣ Access (or create) ExtGState dictionary
            var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // 3️⃣ Build new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // 4️⃣ Register the state with a name (GS0)
            extGState.Add("


## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并探索在项目中的替代实现方式。每篇资源都提供完整的可运行代码示例和逐步解释。

- [使用 Aspose.Pdf 在 PDF 中创建自定义图形状态](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [使用 Aspose.PDF for .NET (C#) 向 PDF 添加图形状态](/pdf/english/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/)
- [如何在 C# 中创建空的 PDF 图形状态](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}