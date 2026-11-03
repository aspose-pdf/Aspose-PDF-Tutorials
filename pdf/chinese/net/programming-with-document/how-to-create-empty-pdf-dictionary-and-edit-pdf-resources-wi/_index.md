---
category: general
date: 2026-10-26
description: 学习使用 Aspose.PDF for C# 创建空的 PDF 字典并编辑 PDF 资源。一步一步的指南，附完整代码示例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- edit PDF resources
- Aspose.PDF C#
- PDF manipulation C#
- PDF graphics state
language: zh
lastmod: 2026-10-26
og_description: 使用 Aspose.PDF for C# 创建空的 PDF 字典并编辑 PDF 资源。请按照本完整教程修改 PDF 中的图形状态。
og_image_alt: Screenshot showing creation of empty PDF dictionary in Aspose.PDF
og_title: 在 C# 中创建空 PDF 字典并编辑 PDF 资源 – Aspose.PDF 指南
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  headline: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  type: TechArticle
- description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  name: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  steps:
  - name: Populate the graphics state entries
    text: 'Add the standard keys:'
  - name: Register the new graphics state in the resource dictionary
    text: Give the state a name (`GS0`) and add it to the `ExtGState` dictionary that
      lives inside the page resources.
  - name: Expected output
    text: 'Running the program prints:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF
title: 如何使用 Aspose.PDF 在 C# 中创建空 PDF 字典并编辑 PDF 资源
url: /zh/net/programming-with-document/how-to-create-empty-pdf-dictionary-and-edit-pdf-resources-wi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.PDF 创建空 PDF 字典并编辑 PDF 资源

如果您需要在 C# 应用程序中**创建空 PDF 字典**并随后**编辑 PDF 资源**，本指南将向您展示具体步骤。您将看到一个完整、可运行的示例，该示例向现有 PDF 的第一页添加自定义图形状态。

处理低层 PDF 对象可能令人望而生畏，但 Aspose.PDF 提供了清晰的字典操作 API。通过本教程，您将了解每个操作的意义以及如何将代码适配到其他资源类型。

## 前提条件

在开始之前，请确保您具备以下条件：

* 已安装 .NET 6.0（或更高版本）。
* 已获取 **Aspose.PDF for .NET** 的授权副本——免费试用版可用于测试。
* 如 Visual Studio 2022 等 IDE。
* 一个名为 `input.pdf` 的 PDF 文件，放置在代码可引用的文件夹中。

除 `Aspose.Pdf` 外，无需其他 NuGet 包。

## 第 1 步：设置项目并导入命名空间

创建一个新的控制台项目并添加 Aspose.PDF 包：

```bash
dotnet new console -n PdfDictionaryDemo
cd PdfDictionaryDemo
dotnet add package Aspose.Pdf
```

在 `Program.cs` 中导入您将使用的命名空间：

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
```

这些导入会暴露 `Document`、`DictionaryEditor` 和 COS（Canonical Object Structure）类，使您能够**创建空 PDF 字典**对象并修改现有资源字典。

## 第 2 步：定义包含 PDF 文件的文件夹

指定保存 `input.pdf` 的目录。使用绝对路径可避免程序在不同工作目录运行时产生歧义。

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfDemo\";
```

将 `C:\PdfDemo\` 替换为您机器上的路径。将路径保存在变量中，可方便在输入和输出文件之间复用。

## 第 3 步：打开源 PDF 文档

在 `using` 块中加载要修改的 PDF，以便文件句柄能够自动释放。

```csharp
// Step 2: Open the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // The rest of the workflow lives inside this block
}
```

打开文档后，您即可访问其页面集合、资源字典以及低层 COS 对象。

## 第 4 步：访问第一页及其资源字典

第一页的索引为 `1`（PDF 页面从 1 开始计数）。获取该页的 `Resources` 字典，并将其包装在 `DictionaryEditor` 中，以实现安全编辑。

```csharp
// Step 3: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` 抽象了底层 COS 结构，使您能够读取或创建条目而不会损坏 PDF。

## 第 5 步：为新图形状态**创建空 PDF 字典**

图形状态控制透明度、混合模式以及其他绘图参数。要添加自定义状态，首先需要一个空字典，然后填充所需的条目。

```csharp
// Step 4: Retrieve the ExtGState dictionary and add a new graphics state
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

// Create an empty dictionary that will hold the graphics state parameters
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
```

对 `CreateEmptyDictionary` 的调用是**创建空 PDF 字典**对象的核心。它返回一个属于同一文档的 COS 字典，确保交叉引用的完整性。

### 填充图形状态条目

添加标准键：

* `CA` – 描边 alpha 常数（范围 0 – 1）。
* `ca` – 非描边 alpha 常数。
* `BM` – 混合模式名称。

```csharp
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

每个条目都会添加到您刚创建的空字典中。通过将定义与插入循环分离，代码保持可读，并且以后可以轻松扩展更多键。

### 在资源字典中注册新图形状态

为该状态命名（`GS0`），并将其添加到页面资源内部的 `ExtGState` 字典中。

```csharp
// Name the new graphics state "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

现在页面的资源字典包含对自定义图形状态的引用，您可以随后将其应用于内容流。

## 第 6 步：保存更新后的 PDF

最后，将修改后的文档写入新文件。保留原始文件不变有助于您验证更改。

```csharp
// Step 5: Save the updated PDF
pdfDocument.Save(dataDir + "output.pdf");
```

当您在支持图形状态检查的查看器（例如 Adobe Acrobat Pro）中打开 `output.pdf` 时，您会看到 `ExtGState` 字典包含名为 `GS0` 的条目，其值为您定义的内容。

## 完整源代码

将所有代码片段组合在一起即可得到一个独立的程序：

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

class Program
{
    static void Main()
    {
        // Step 1: Define the folder that contains the PDF files
        string dataDir = @"C:\PdfDemo\"; // adjust to your environment

        // Step 2: Open the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Step 3: Access the first page and its resource dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 4: Retrieve the ExtGState dictionary and add a new graphics state
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // **Create empty PDF dictionary** for the new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateEntries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };

            foreach (var entry in graphicsStateEntries)
                newGraphicsState.Add(entry);

            // Register the new graphics state as "GS0"
            extGStateDict.Add("GS0", newGraphicsState);

            // Step 5: Save the updated PDF
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

### 预期输出

运行程序会输出：

```
PDF updated successfully.
```

并在同一文件夹中创建 `output.pdf`。打开文件后会在 **Resources → ExtGState → GS0** 下看到您设置的参数条目。

## 常见变体和边缘情况

| 情形 | 如何调整代码 |
|-----------|-----------------------|
| **多个页面**需要相同的图形状态 | 先创建一次字典，然后将相同的 `GS0` 引用添加到每个页面的 `ExtGState` 字典中。 |
| **不同的混合模式**（例如 `Multiply`） | 将 `CosPdfName("Normal")` 的值改为 `CosPdfName("Multiply")`。 |
| **不存在 ExtGState 字典** | 在访问 `resourcesEditor["ExtGState"]` 之前，检查 `resourcesEditor.ContainsKey("ExtGState")`。如果不存在，则创建一个新的空字典并将其添加到 `firstPage.Resources`。 |
| **大型 PDF**导致内存压力 | 使用支持分页流式读取的 `PdfDocument.Load` 重载，或在 `using` 块内一次处理一页。 |
| **需要编辑其他资源**（字体、XObject） | 在 `resourcesEditor` 查找中将 `"ExtGState"` 替换为 `"Font"` 或 `"XObject"`，然后遵循相同的创建空字典并填充的模式。 |

这些变体展示了相同的**创建空 PDF 字典**模式如何适用于您希望**编辑 PDF 资源**的任何资源类型。

## 专业技巧

* **验证结果** – 保存后，在能够显示原始资源字典的工具（例如 PDF‑Box 的 `PDFDebugger`）中打开 PDF，以确保条目存在。
* **复用字典** – 如果向多个页面添加相同的图形状态，请将字典存储在变量中并引用，而不是每次都重新创建。
* **版本兼容性** – 代码适用于 Aspose.PDF 23.12 及更高版本。早期版本可能需要使用 `CosDictionary` 而非 `CosPdfDictionary`。

## 结论

现在，您已经了解如何使用 Aspose.PDF for C# **创建空 PDF 字典**对象并**编辑 PDF 资源**。本教程涵盖了打开文档、访问页面资源字典、构建自定义图形状态、注册该状态以及保存结果的全过程。从此您可以尝试其他资源类型、组合多个图形状态，或将此技术集成到更大的 PDF 处理流水线中。

*准备好进一步探索了吗？尝试向内容流添加自定义 **ExtGState**，或操作 **Font** 字典以嵌入新字体。两者都遵循创建空字典并编辑 PDF 资源的相同模式。*

## 接下来应该学习什么？

以下教程涵盖与本指南技术密切相关的主题。每篇资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [Edit PDF Resource Dictionary with Aspose.PDF – C# Guide](/pdf/english/net/programming-with-operators/edit-pdf-resource-dictionary-with-aspose-pdf-c-guide/)
- [Create custom graphics state in PDF using Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [How to create empty graphics state in a PDF with C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}