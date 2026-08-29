---
category: general
date: 2026-08-17
description: 使用 C# 和 Aspose.Pdf 在 PDF 中创建空的图形状态。请按照本分步指南安全地编辑 ExtGState 资源。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty graphics state
- Aspose PDF graphics state
- C# modify PDF resources
- add ExtGState dictionary
- PDF page resources editing
language: zh
lastmod: 2026-08-17
og_description: 使用 C# 在 PDF 中创建空的图形状态。本教程展示了如何使用 Aspose.Pdf 编辑 ExtGState 资源，以实现可靠的
  PDF 修改。
og_image_alt: Screenshot of C# code that adds an empty graphics state to a PDF document
og_title: 使用 C# 在 PDF 中创建空图形状态 – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Create empty graphics state in a PDF using C# and Aspose.Pdf. Follow
    this step‑by‑step guide to edit ExtGState resources safely.
  headline: How to create empty graphics state in a PDF with C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: 如何在 PDF 中使用 C# 创建空图形状态
url: /zh/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 PDF 中使用 C# 创建空的图形状态

如果您需要在 PDF 中**创建空的图形状态**，本指南将向您展示如何使用 C# 和 Aspose.Pdf 完成此操作。您将看到一个完整、可运行的示例，它向页面的 ExtGState 字典添加一个新条目，而不会影响现有内容。

在 PDF 图形状态上工作是一个常见需求，当您想要在每个对象层面控制透明度、混合模式或其他渲染参数时。下面的代码演示了推荐的做法，解释了每一步的原因，并涵盖了您可能遇到的典型变体。

## 前置条件

在开始之前，请确保您拥有：

* .NET 6.0 或更高版本（示例同样可以在 .NET Core 下编译）。
* Aspose.Pdf for .NET 许可证（或临时评估密钥）。
* 包含您想要修改的 `input.pdf` 文件的文件夹。
* 对 C# 语法以及 PDF 资源字典等概念有基本了解。

## 第 1 步：设置项目并导入命名空间

创建一个新的控制台应用程序，或将代码集成到现有项目中。添加 Aspose.Pdf NuGet 包：

```bash
dotnet add package Aspose.Pdf
```

然后导入所需的命名空间：

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
```

这些导入让您能够访问 `Document`、`DictionaryEditor` 以及用于**创建空的图形状态**条目的 PDF 原始类。

## 第 2 步：定义保存 PDF 文件的文件夹

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfSamples\";
```

将路径替换为您自己的 PDF 文件所在位置。将目录保存到变量中可以使代码更易复用和测试。

## 第 3 步：加载源 PDF 文档

```csharp
// Step 2: Load the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // All subsequent operations happen inside this using block
```

在 `using` 语句中打开文档可确保在保存更改后自动释放文件句柄。

## 第 4 步：访问第一页及其 Resources 字典

```csharp
    // Step 3: Get the first page and its Resources dictionary
    var firstPage = pdfDocument.Pages[1];
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
    var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

* `Pages[1]` 获取第一页（PDF 页码从 1 开始）。
* `DictionaryEditor` 提供了一种便捷方式来读取和修改 PDF 字典。
* `ExtGState` 条目保存了页面的所有图形状态对象。如果该键不存在，Aspose.Pdf 会自动创建一个空字典。

## 第 5 步：构建一个新的空图形状态字典

您添加的图形状态可以是空的，也可以预先填充诸如不透明度（`CA`、`ca`）或混合模式（`BM`）等参数。在本教程中，我们创建一个**空的图形状态**，随后设置几个典型值以演示字典的工作方式。

```csharp
    // Step 4: Create a new empty graphics‑state dictionary and set its parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // Stroke opacity
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };
    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

* `CosPdfDictionary.CreateEmptyDictionary` 创建一个干净的容器，您可以向其中填入任意图形状态键。
* 添加 `CA`、`ca` 和 `BM` 是可选的；如果您真的需要一个空状态，可以省略它们。代码展示了在以后需要控制渲染时如何添加条目。

## 第 6 步：将新图形状态插入 ExtGState 字典

```csharp
    // Step 5: Add the new graphics state to the page's ExtGState dictionary (e.g., name it "GS0")
    extGStateDict.Add("GS0", newGraphicsState);
```

将条目命名为 `"GS0"` 符合常见的以 “GS” 为前缀的图形状态命名约定。您可以选择任何不与现有键冲突的有效 PDF 名称。

## 第 7 步：保存修改后的 PDF 文档

```csharp
    // Step 6: Save the modified PDF document
    pdfDocument.Save(dataDir + "output.pdf");
}
```

`Save` 调用会将更新后的文件写入 `output.pdf`。在 PDF 查看器中打开此文件即可确认新图形状态已存在；随后您可以在内容流中使用 `gs` 操作符引用它。

### 完整源码列表

将所有内容组合在一起，完整程序如下：

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;

class Program
{
    static void Main()
    {
        // Define the folder that contains the PDF files
        string dataDir = @"C:\PdfSamples\";

        // Load the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Get the first page and its Resources dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create a new empty graphics‑state dictionary and set its parameters
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters)
                newGraphicsState.Add(p);

            // Add the new graphics state to the page's ExtGState dictionary (name it "GS0")
            extGStateDict.Add("GS0", newGraphicsState);

            // Save the modified PDF document
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("Empty graphics state created and saved to output.pdf");
    }
}
```

运行程序会打印确认信息，并生成包含新添加图形状态的 `output.pdf`。

## 为什么这种做法是最佳选择

* **直接字典编辑** – 使用 `DictionaryEditor` 可避免解析整个内容流，只修改您关心的资源。
* **强类型 PDF 原始对象** – `CosPdfNumber`、`CosPdfName` 和 `CosPdfDictionary` 确保生成的 PDF 符合 PDF 1.7 规范。
* **安全性** – `using` 块会释放 `Document` 对象，防止文件锁定导致后续构建损坏。
* **可扩展性** – 一旦空的图形状态存在，您可以在任何内容操作符（`gs`）中引用它，以改变选定绘图命令的透明度、混合模式或其他参数。

## 常见变体和边缘情况

| 情形 | 推荐的调整 |
|-----------|-------------------|
| **多页文档** | 遍历 `pdfDocument.Pages`，对每个需要修改的页面重复字典插入操作。 |
| **不存在 ExtGState 条目** | `resourcesEditor["ExtGState"]` 会在键不存在时自动创建空字典，无需额外代码。 |
| **不同的图形状态名称** | 将 `"GS0"` 替换为符合您命名约定的名称，例如 `"MyTransparentState"`。 |
| **仅添加空状态** | 省略 `parameters` 数组和 `foreach` 循环；字典将保持为空。 |
| **处理加密 PDF** | 在构造 `new Document(path, password)` 时提供密码，然后再编辑资源。 |

## 验证结果

您可以使用诸如 **PDF‑Tron** 或 **iText Sharp** 等低层查看器检查 PDF，以确认图形状态已被添加。查找类似以下的条目：

```
/ExtGState << /GS0 << /CA 1 /ca 0.5 /BM /Normal >> >>
```

如果出现该条目，**创建空的图形状态**操作即告成功。

## 结论

现在，您已经掌握了如何使用 C# 和 Aspose.Pdf 在 PDF 中**创建空的图形状态**。本教程涵盖了从加载文档、编辑 `ExtGState` 字典到保存结果的每一步，并解释了每个操作背后的原理。

接下来您可以：

* 在内容流中使用新图形状态（`gs /GS0`）。
* 试验其他键，例如 `/SM`（描边调整）或 `/OPM`（过印模式）。
* 将相同技术应用于其他资源类型，如 `/XObject` 或 `/ColorSpace`。

祝您 PDF 开发愉快，欢迎探索其他 **Aspose PDF 图形状态** 场景，如动态透明度变化或自定义混合模式！

## 接下来您应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助您在项目中进一步使用 API 功能并探索替代实现方式，每篇都提供完整可运行的代码示例和逐步说明。

- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [How to Remove Graphics from PDFs Using Aspose.PDF .NET&#58; A Complete Guide](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Create & Fill Rectangles in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}