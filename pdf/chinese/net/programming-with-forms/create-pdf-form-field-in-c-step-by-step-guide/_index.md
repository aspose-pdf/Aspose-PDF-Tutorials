---
category: general
date: 2026-08-14
description: 使用 C# 快速创建 PDF 表单字段。学习如何向 PDF 添加文本框以及使用 Aspose.PDF 修改 PDF 以包含文本框。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf form field
- add text box to pdf
- modify pdf to include text box
- Aspose.PDF form field
- C# PDF manipulation
language: zh
lastmod: 2026-08-14
og_description: 使用 C# 创建 PDF 表单字段。本教程展示了如何向 PDF 添加文本框，以及如何使用 Aspose.PDF 修改 PDF 以包含文本框。
og_image_alt: Screenshot of a PDF page showing a newly added text box form field
og_title: 在 C# 中创建 PDF 表单字段 – 完整编程指南
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create pdf form field quickly with C#. Learn how to add text box to
    pdf and modify pdf to include text box using Aspose.PDF.
  headline: Create pdf form field in C# – step‑by‑step guide
  type: TechArticle
- description: Create pdf form field quickly with C#. Learn how to add text box to
    pdf and modify pdf to include text box using Aspose.PDF.
  name: Create pdf form field in C# – step‑by‑step guide
  steps:
  - name: Load the existing PDF document.
    text: Load the existing PDF document.
  - name: Instantiate a `TextBoxField` and configure its name and appearance.
    text: Instantiate a `TextBoxField` and configure its name and appearance.
  - name: Add a widget annotation that defines the visual rectangle on the target
      page.
    text: Add a widget annotation that defines the visual rectangle on the target
      page.
  - name: Insert the field into the document’s form collection.
    text: Insert the field into the document’s form collection.
  - name: Save the modified PDF.
    text: Save the modified PDF.
  - name: Open `output.pdf` in Adobe Acrobat Reader.
    text: Open `output.pdf` in Adobe Acrobat Reader.
  - name: Click inside the “Comments” box; the cursor should appear.
    text: Click inside the “Comments” box; the cursor should appear.
  - name: Type any text and press **Tab** or click elsewhere.
    text: Type any text and press **Tab** or click elsewhere.
  - name: Choose **File → Save As** to persist the entered value.
    text: Choose **File → Save As** to persist the entered value.
  - name: '(Optional) Use Aspose.PDF’s `Form` API to extract the value programmatically:'
    text: '(Optional) Use Aspose.PDF’s `Form` API to extract the value programmatically:'
  type: HowTo
tags:
- pdf
- csharp
- form-fields
title: 在 C# 中创建 PDF 表单字段 – 步骤指南
url: /zh/net/programming-with-forms/create-pdf-form-field-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中创建 PDF 表单字段 – 步骤指南

如果您需要 **在文档中创建 pdf 表单字段**，本指南将带您完整完成整个过程。您将看到如何 **向 pdf 添加文本框** 页面，以及如何使用 Aspose.PDF for .NET **修改 pdf 以包含文本框**。

处理 PDF 表单是发票系统、调查或任何收集用户输入的工作流中的常见需求。完成本教程后，您将拥有一段可复用的代码片段，能够创建功能完整的文本框字段，将其放置在指定位置，并保存更新后的 PDF——全部在您的 C# 项目中完成。

## 前置条件

开始之前，请确保您具备：

* .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.7+）
* Visual Studio 2022 或任何支持 C# 的 IDE
* 有效的 Aspose.PDF for .NET 授权（免费试用可用于开发）
* 一个名为 `input.pdf` 的 PDF 文件，放置在已知目录下（教程中使用 `YOUR_DIRECTORY` 作为占位符）

> **专业提示：** 如果您还没有授权，可以从 Aspose 官网申请临时密钥；库在评估模式下无需代码修改即可使用。

## 在 C# 中创建 pdf 表单字段的概览

1. 加载已有的 PDF 文档。  
2. 实例化 `TextBoxField` 并配置其名称和外观。  
3. 添加一个小部件注释，定义目标页面上的可视矩形。  
4. 将字段插入文档的表单集合。  
5. 保存修改后的 PDF。

下面将对每一步进行详细说明，并提供完整代码示例以及 API 调用背后的原理。

## 步骤 1：加载 PDF 文档

首要操作是读取源 PDF。Aspose.PDF 使用 `Document` 类来表示 PDF 文件。加载文档后，您即可访问其页面、表单集合以及其他结构。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

// Adjust the path to match your environment
string inputPath = Path.Combine("YOUR_DIRECTORY", "input.pdf");

// Load the PDF you want to modify
Document pdfDocument = new Document(inputPath);
```

**为什么重要：**  
加载文件会在内存中创建 PDF 的模型，允许您在不损坏原始文件的前提下添加、删除或编辑对象。`Document` 对象还公开了 `Form` 属性，稍后您将在这里 **向 pdf 添加文本框**。

## 步骤 2：创建文本框字段

文本框字段是一种表单字段，允许用户输入自由文本。在 Aspose.PDF 中，您通过实例化 `TextBoxField`，并传入目标页面和定义小部件初始大小的矩形来创建它。

```csharp
// Choose the page index (0‑based). Here we use page 2 (index 1).
Page targetPage = pdfDocument.Pages[1];

// Define the rectangle for the field’s *initial* size.
// Rectangle(left, bottom, right, top) – values are in points (1/72 inch).
Rectangle fieldRect = new Rectangle(100, 500, 200, 530);

// Create the TextBoxField with a partial name that will be used in form data.
TextBoxField textBox = new TextBoxField(targetPage, fieldRect)
{
    PartialName = "Comments", // This identifier appears in the PDF form data.
    // Optional: set default appearance (font, size, color)
    DefaultAppearance = new DefaultAppearance(FontRepository.FindFont("Helvetica"), 12, Color.Black)
};
```

**为什么重要：**  
* `PartialName` 是表单处理工具（如 Adobe Acrobat、服务器端解析器）用来检索输入值的键。  
* 此处传入的矩形仅定义 *初始* 小部件大小；您可以在后续步骤中通过小部件注释调整其可视位置。  
* 设置 `DefaultAppearance` 可确保文本在各查看器中保持一致的渲染效果。

## 步骤 3：定义可视小部件注释

表单字段可以拥有一个或多个 **小部件注释**，用于控制字段在每页上的显示位置。通过添加小部件，您可以将同一逻辑字段放置在不同位置，甚至跨多个页面。

```csharp
// Define where the field will actually be displayed on the page.
// This rectangle can differ from the one used in the constructor.
Rectangle widgetRect = new Rectangle(100, 300, 200, 330);
textBox.AddWidgetAnnotation(widgetRect);
```

**为什么重要：**  
小部件矩形决定了用户在屏幕上看到的坐标。如果跳过此步骤，字段虽然存在于 PDF 的数据结构中，却不会对终端用户可见。添加小部件正是 **向 pdf 添加文本框** 的关键步骤。

## 步骤 4：将配置好的字段添加到文档的表单中

当 `TextBoxField` 完全配置好后，需要将其注册到 PDF 的表单集合中。这会使字段成为交互式表单的一部分，并确保其被保存。

```csharp
pdfDocument.Form.Add(textBox);
```

**为什么重要：**  
如果不将字段添加到 `pdfDocument.Form`，PDF 查看器会忽略小部件注释，字段数据也永远不会被提交。这行代码完成了 **修改 pdf 以包含文本框** 的操作。

## 步骤 5：保存更新后的 PDF

最后，将更改写回磁盘。您可以覆盖原文件，也可以生成新文件；示例中保存为 `output.pdf`。

```csharp
string outputPath = Path.Combine("YOUR_DIRECTORY", "output.pdf");

// Save the document with the new form field
pdfDocument.Save(outputPath);
```

当您在 Adobe Acrobat Reader 中打开 `output.pdf` 时，会在第 2 页看到一个标注为 “Comments” 的矩形文本框。用户可以点击内部输入，输入的文本将成为 PDF 表单数据的一部分。

## 完整可运行示例

将所有代码片段组合起来，即得到一个完整、可直接运行的程序。将其复制到新的控制台项目中，替换 `YOUR_DIRECTORY` 为实际文件夹路径，然后运行。

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
using System.Drawing; // For Color

namespace PdfFormFieldDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the existing PDF
            string inputPath = Path.Combine("YOUR_DIRECTORY", "input.pdf");
            Document pdfDocument = new Document(inputPath);

            // 2️⃣ Create a TextBoxField on page 2 (index 1)
            Page targetPage = pdfDocument.Pages[1];
            Rectangle fieldRect = new Rectangle(100, 500, 200, 530);
            TextBoxField textBox = new TextBoxField(targetPage, fieldRect)
            {
                PartialName = "Comments",
                DefaultAppearance = new DefaultAppearance(
                    FontRepository.FindFont("Helvetica"), 12, Color.Black)
            };

            // 3️⃣ Add a widget annotation to control visual placement
            Rectangle widgetRect = new Rectangle(100, 300, 200, 330);
            textBox.AddWidgetAnnotation(widgetRect);

            // 4️⃣ Register the field with the document's form collection
            pdfDocument.Form.Add(textBox);

            // 5️⃣ Save the modified PDF
            string outputPath = Path.Combine("YOUR_DIRECTORY", "output.pdf");
            pdfDocument.Save(outputPath);

            Console.WriteLine("PDF form field created successfully.");
            Console.WriteLine($"Output saved to: {outputPath}");
        }
    }
}
```

**预期输出：**  
运行程序后，控制台会打印两行确认信息。打开 `output.pdf` 可看到第 2 页的文本框，用户可以在其中输入评论。当表单通过 Adobe Acrobat 的 “Submit” 按钮提交时，字段名 `Comments` 将出现在导出的 FDF 或 XFDF 数据中。

## 常见变体与边缘情况

| 情形 | 代码适配方式 |
|-----------|-----------------------|
| **将字段添加到其他页面** | 将 `pdfDocument.Pages[1]` 改为目标页面索引（基于 `0` 的索引）。 |
| **创建多行文本框** | 在添加小部件前设置 `textBox.Multiline = true;`。 |
| **设置默认值** | 赋值 `textBox.Value = "Enter your comments here";`。 |
| **将字段设为必填** | 设置 `textBox.Required = true;`。 |
| **在多个页面放置字段** | 对每个目标页面的矩形调用 `textBox.AddWidgetAnnotation`。 |
| **使用自定义字体** | 使用 `FontRepository.AddFont("path/to/font.ttf")` 加载字体，并在 `DefaultAppearance` 中引用。 |

**专业提示：** 始终将矩形坐标与页面尺寸（`pdfDocument.Pages[1].Rect`）进行校验。如果小部件位于页面边界之外，查看器可能会裁剪或隐藏该字段。

## 测试表单字段

1. 在 Adobe Acrobat Reader 中打开 `output.pdf`。  
2. 点击 “Comments” 框内部，光标应出现。  
3. 输入任意文字后按 **Tab** 或点击其他位置。  
4. 通过 **文件 → 另存为** 保存已输入的值。  
5. （可选）使用 Aspose.PDF 的 `Form` API 以代码方式提取该值：

```csharp
string commentValue = pdfDocument.Form["Comments"].Value;
Console.WriteLine($"Submitted comment: {commentValue}");
```

此代码片段演示了字段不仅可见，还可以通过代码检索——这对服务器端处理至关重要。

## 结论

现在，您已经掌握了在 C# 中 **创建 pdf 表单字段** 的完整流程。教程涵盖了加载 PDF、配置 `TextBoxField`、添加小部件注释、注册字段以及保存结果。凭借这些构建块，您可以 **向 pdf 添加文本框**、**修改 pdf 以包含文本框**，并将方法扩展到复选框、单选按钮或下拉列表等其他字段类型。

接下来，您可以进一步探索 **提取表单数据**、**扁平化 PDF 表单** 或 **使用边框和颜色样式化字段** 等相关主题。这些概念都基于您刚刚掌握的核心 API，帮助您在 C# 中创建功能强大的交互式 PDF。

祝编码愉快，欢迎尝试不同的矩形、字体和验证规则，以满足您应用的需求！

## 接下来您应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助您在已有技巧的基础上进一步深入。每篇资源都提供完整可运行的代码示例和逐步解释，助您掌握更多 API 功能并探索在项目中的替代实现方式。

- [Create PDF Document with Aspose – Add Page, Text Box, and Form](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)
- [How to Create PDF with Aspose – Add Form Field and Pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [How to Add a Text Stamp to PDF Using Aspose.PDF .NET: Comprehensive Guide](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}