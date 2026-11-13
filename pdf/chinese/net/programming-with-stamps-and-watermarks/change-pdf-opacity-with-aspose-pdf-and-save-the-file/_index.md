---
category: general
date: 2026-11-12
description: 学习如何使用 Aspose.Pdf 更改 PDF 不透明度、添加透明效果、设置混合模式，并在 C# 中保存修改后的 PDF。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF opacity
- how to add transparency
- save modified PDF
- how to set blend mode
- set fill opacity
language: zh
lastmod: 2026-11-12
og_description: 使用 Aspose.Pdf 更改 PDF 不透明度，学习如何添加透明度、设置混合模式，并在 C# 中保存修改后的 PDF 文件。
og_image_alt: Screenshot of a PDF page with altered opacity using Aspose.Pdf
og_title: 使用 Aspose.Pdf 更改 PDF 不透明度 – 添加透明效果并保存
schemas:
- author: Aspose
  dateModified: '2026-11-12'
  description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  headline: Change PDF opacity with Aspose.Pdf and save the file
  type: TechArticle
- description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  name: Change PDF opacity with Aspose.Pdf and save the file
  steps:
  - name: Load the PDF document
    text: Start by creating a `Document` instance that points to your source file.
      The constructor reads the entire PDF into memory, allowing you to manipulate
      its internal objects.
  - name: Access the first page’s resources
    text: Each PDF page stores a *resource dictionary* that holds objects such as
      fonts, images, and graphics states. You need to edit this dictionary to inject
      a new `ExtGState` entry.
  - name: Ensure an ExtGState dictionary exists
    text: The `ExtGState` dictionary holds custom graphics states. If it does not
      exist, the code creates one automatically.
  - name: Define a new graphics state (ExtGState)
    text: A graphics state defines how drawing operations behave. The following dictionary
      sets stroke opacity (`CA`), fill opacity (`ca`), and blend mode (`BM`).
  - name: Register the graphics state in the resource dictionary
    text: Give the new state a name (e.g., `GS0`) and add it to the `ExtGState` dictionary.
      This name will be referenced later in the page content stream.
  - name: Apply the graphics state to page content
    text: To actually see the opacity effect, insert the `/GS0 gs` operator before
      the drawing commands you want to affect. The example below draws a semi‑transparent
      rectangle.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The `Save` method overwrites
      the target file or creates a new one if it does not exist.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: 使用 Aspose.Pdf 更改 PDF 的不透明度并保存文件
url: /zh/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-and-save-the-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Pdf 更改 PDF 不透明度并保存文件

如果您需要在文档中 **更改 PDF 不透明度**，Aspose.Pdf 提供了直接的 API 来调整描边和填充的透明度。本教程将完整演示 **如何添加透明度**、**如何设置混合模式**，以及仅用几行 C# 代码 **保存修改后的 PDF** 文件。

您将逐步完成从加载已有 PDF、定义新的图形状态到持久化更改的全过程。阅读完本指南后，您可以：

* 降低矢量图形或图像的可见度。
* 应用自定义混合模式，如 *Normal* 或 *Multiply*。
* 导出更新后的文件且不丢失其他内容。

唯一的前置条件是拥有可用的 .NET 开发环境并引用 Aspose.Pdf 库（版本 23.9 或更高）。无需任何外部工具。

## 前置条件

| 需求 | 原因 |
|------|------|
| .NET 6.0 SDK 或更高版本 | 确保与最新的 Aspose.Pdf API 兼容。 |
| Aspose.Pdf for .NET NuGet 包 | 提供代码中使用的 `Document`、`CosPdfDictionary` 等类。 |
| 用于编辑的 PDF 文件（例如 `input.pdf`） | 作为不透明度更改的源文件。 |

使用以下命令安装 NuGet 包：

```bash
dotnet add package Aspose.Pdf
```

## 使用 Aspose.Pdf 更改 PDF 不透明度

### 步骤 1：加载 PDF 文档

首先创建指向源文件的 `Document` 实例。构造函数会将整个 PDF 读取到内存中，便于您操作其内部对象。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;

// Load the existing PDF
var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");
```

> **为什么要这样做？** 加载文件会生成可操作的对象模型。后续的所有更改都基于此内存表示，确保原始文件在您显式保存之前保持不变。

### 步骤 2：访问第一页的资源

每个 PDF 页面都有一个 *资源字典*，其中存放字体、图像和图形状态等对象。您需要编辑此字典以注入新的 `ExtGState` 条目。

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor simplifies access to the page's resource dictionary
var resourcesEditor = new DictionaryEditor(page.Resources);
```

> **提示：** 如果 PDF 包含多页且需要相同的不透明度，请为每页重复此步骤，或在页面之间共享同一个 `ExtGState`。

### 步骤 3：确保 ExtGState 字典存在

`ExtGState` 字典用于保存自定义图形状态。如果不存在，代码会自动创建一个。

```csharp
// Get or create the ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                     ?? new CosPdfDictionary(pdfDoc);
resourcesEditor["ExtGState"] = extGStateDict;
```

> **为什么要这样做？** 没有 `ExtGState` 容器，任何对新图形状态的引用都会失败，导致 PDF 忽略您的不透明度设置。

### 步骤 4：定义新的图形状态（ExtGState）

图形状态决定绘图操作的行为。下面的字典设置了描边不透明度 (`CA`)、填充不透明度 (`ca`) 和混合模式 (`BM`)。

```csharp
// Create an empty dictionary for the new graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Set desired parameters
var parameters = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (1 = opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (0.5 = 50% transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var param in parameters)
    newGraphicsState.Add(param);
```

> **如何设置填充不透明度：** `ca` 条目控制填充形状（文本、路径）的透明度。将数值设为 `0`（完全透明）到 `1`（完全不透明）之间，以满足设计需求。  
> **如何设置混合模式：** `BM` 条目选择合成算法。常用值包括 `Normal`、`Multiply`、`Screen` 和 `Overlay`。请选择最符合您视觉意图的模式。

### 步骤 5：在资源字典中注册图形状态

为新状态指定一个名称（例如 `GS0`），并将其添加到 `ExtGState` 字典中。此名称稍后将在页面内容流中引用。

```csharp
// Add the graphics state with a symbolic name
extGStateDict.Add("GS0", newGraphicsState);
```

> **专业技巧：** 当创建多个状态时，使用 `GS0`、`GS1` … 等命名约定，可避免名称冲突并简化调试。

### 步骤 6：将图形状态应用于页面内容

要实际看到不透明度效果，需要在想要影响的绘图指令前插入 `/GS0 gs` 操作符。下面的示例绘制了一个半透明矩形。

```csharp
// Build a content stream that uses the new graphics state
var content = new MemoryStream();
var writer = new StreamWriter(content);

// Activate the graphics state
writer.WriteLine("q");                 // Save graphics state
writer.WriteLine("/GS0 gs");           // Apply custom ExtGState
writer.WriteLine("0.2 0.5 0.8 rg");    // Set fill color (RGB)
writer.WriteLine("100 500 200 100 re"); // Rectangle (x y width height)
writer.WriteLine("f");                 // Fill rectangle
writer.WriteLine("Q");                 // Restore graphics state
writer.Flush();

content.Position = 0;
page.Contents.Add(new ContentStream(content));
```

> **为什么要使用 `q` 和 `Q` 操作符？** 它们会压入和弹出图形状态栈，确保不透明度的更改仅影响矩形本身，而不影响页面的其他部分。

### 步骤 7：保存修改后的 PDF

最后，将更新后的文档写入磁盘。`Save` 方法会覆盖目标文件，或在文件不存在时创建新文件。

```csharp
// Persist the changes
pdfDoc.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **如何保存修改后的 PDF：** `Save` 调用会将所有内存中的修改（包括新的 `ExtGState`）写入指定路径。您也可以将结果流式传输到 `MemoryStream`，用于 Web 响应。

## 完整可运行示例

下面是一段完整、独立的程序，囊括了上述所有步骤。将其复制到控制台应用程序中并运行，即可验证不透明度的更改。



## 接下来您应该学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助您在项目中进一步掌握 API 功能并探索替代实现方式。

- [How to save modified PDF with Aspose.Pdf and add transparency](/pdf/english/net/document-manipulation/how-to-save-modified-pdf-with-aspose-pdf-and-add-transparenc/)
- [How to add transparency to PDF using Aspose.PDF in C#](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [How to add graphics state pdf and control transparency with Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}