---
category: general
date: 2026-09-27
description: 创建 PDF 文档并在构建交互式 PDF 表单时向 PDF 添加页面。了解如何向 PDF 添加文本框以及使用 Aspose.Pdf 创建
  AcroForm PDF。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add pages to pdf
- create interactive pdf form
- how to add textbox to pdf
- how to create acroform pdf
language: zh
lastmod: 2026-09-27
og_description: 创建 PDF 文档并在构建交互式 PDF 表单时向 PDF 添加页面。请按照本指南了解如何向 PDF 添加文本框并使用 Aspose.Pdf
  创建 AcroForm PDF。
og_image_alt: Screenshot showing a PDF document with a textbox field on two pages
og_title: 使用交互式表单字段创建 PDF 文档 – 步骤详解 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: create PDF document and add pages to PDF while building an interactive
    PDF form. Learn how to add TextBox to PDF and create AcroForm PDF with Aspose.Pdf.
  headline: How to create PDF document with interactive form fields in C#
  type: TechArticle
- description: create PDF document and add pages to PDF while building an interactive
    PDF form. Learn how to add TextBox to PDF and create AcroForm PDF with Aspose.Pdf.
  name: How to create PDF document with interactive form fields in C#
  steps:
  - name: '**Create PDF document** and add the needed pages.'
    text: '**Create PDF document** and add the needed pages.'
  - name: '**Initialize AcroForm** and define a `TextBoxField`.'
    text: '**Initialize AcroForm** and define a `TextBoxField`.'
  - name: '**Add widget annotations** on each page to place the textbox.'
    text: '**Add widget annotations** on each page to place the textbox.'
  - name: '**Save** the document and test the interactive behavior.'
    text: '**Save** the document and test the interactive behavior.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF forms
title: 如何在 C# 中创建带交互式表单字段的 PDF 文档
url: /zh/net/programming-with-forms/how-to-create-pdf-document-with-interactive-form-fields-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中创建带交互式表单字段的 PDF 文档

如果您需要 **创建 PDF 文档**，其中包含多页和交互式表单，本指南将一步步演示如何实现。我们将讲解向 PDF 添加页面、构建 AcroForm，以及在每页上放置 TextBox 字段，使用 Aspose.Pdf for .NET。

完成后，您将得到一个单一的 PDF 文件，用户可以在两页上输入评论。无需外部工具，只需几行 C# 代码和强大的 Aspose.Pdf 库。

## 前置条件

在开始之前，请确保您拥有：

* .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.7+）
* 有效的 Aspose.Pdf for .NET 许可证或临时评估密钥
* Visual Studio 2022（或任何支持 C# 的 IDE）
* 对 C# 语法和面向对象概念的基本了解

> **专业提示：** 如果您使用免费试用版，请记得在程序早期设置 `License` 对象，以避免出现评估水印。

## 第 1 步：设置项目并导入命名空间

创建一个新的控制台应用程序并添加 Aspose.Pdf NuGet 包：

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
dotnet add package Aspose.Pdf
```

在 `Program.cs` 中导入所需的命名空间：

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Forms;
```

这些命名空间为您提供了核心 PDF 对象、注释类型以及本教程所需的表单字段类的访问权限。

## 第 2 步：创建 PDF 文档并向 PDF 添加页面

首个功能步骤是 **创建 PDF 文档**，随后 **向 PDF 添加页面**。每页都将承载相同的 TextBox 字段。

```csharp
// Initialize a new PDF document
var pdfDocument = new Document();

// Add two blank pages
var firstPage = pdfDocument.Pages.Add();
var secondPage = pdfDocument.Pages.Add();
```

*为什么这很重要：*  
`Document` 代表整个 PDF 文件。显式添加页面可确保您拥有放置表单部件的画布。您可以根据需要添加任意数量的页面，示例中使用两页以便说明。

## 第 3 步：创建交互式 PDF 表单（AcroForm）

**交互式 PDF 表单** 基于位于 `Document` 内的 AcroForm 对象构建。我们将创建一个 `TextBoxField`，该字段将在两页之间共享。

```csharp
// Initialize the AcroForm if it doesn't exist
if (!pdfDocument.AcroForm.IsPresent)
{
    pdfDocument.AcroForm = new AcroForm(pdfDocument);
}

// Create a TextBox field named "Comments"
var textBoxField = new TextBoxField(pdfDocument.AcroForm)
{
    Name = "Comments",
    // Optional: set default appearance (font size, color)
    DefaultAppearance = new DefaultAppearance("Helvetica", 12, Color.Black)
};
```

*为什么这很重要：*  
AcroForm 容器保存所有交互元素。通过创建单个 `TextBoxField`，我们可以在多页上复用同一逻辑字段，从而在用户填写时保持数据同步。

## 第 4 步：如何向 PDF 添加 TextBox —— 放置部件注释

**部件注释（widget annotation）** 将页面上的可视矩形与逻辑表单字段关联。我们将在每页添加一个部件。

```csharp
// Widget on the first page (coordinates: lower‑left X,Y – upper‑right X,Y)
var firstPageWidget = new WidgetAnnotation(
    firstPage,
    new Rectangle(50, 700, 200, 750))
{
    Parent = textBoxField,
    // Optional visual properties
    HighlightingMode = HighlightingMode.Invert,
    Border = new Border(BorderStyle.Solid, 1, Color.Black)
};

// Widget on the second page, positioned slightly lower
var secondPageWidget = new WidgetAnnotation(
    secondPage,
    new Rectangle(50, 600, 200, 650))
{
    Parent = textBoxField,
    HighlightingMode = HighlightingMode.Invert,
    Border = new Border(BorderStyle.Solid, 1, Color.Black)
};
```

*为什么这很重要：*  
`WidgetAnnotation` 定义了文本框出现的位置及其外观。通过将相同的 `Parent`（`textBoxField`）分配给两个部件，两个部件都引用同一个底层数据字段。用户在任一部件中输入的内容会即时在另一页显示。

## 第 5 步：保存 PDF 并验证结果

最后，将文档写入磁盘：

```csharp
// Save the PDF to the output folder
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);

Console.WriteLine($"PDF saved to {outputPath}");
```

打开 `output.pdf`（使用 Adobe Acrobat Reader）时：

* 文档显示两页。
* 每页包含一个标记为 “Comments” 的文本框。
* 在任一页的文本框中输入内容，另一页会立即同步显示（它们共享同一字段名）。

### 预期输出截图

![带有文本框的双页 PDF](https://example.com/pdf-form-screenshot.png "创建带交互式表单字段的 PDF 文档")

*(图片的 alt 文本包含主要关键词，以提升可访问性和 SEO。)*

## 常见变体和边缘情况

| 情况 | 处理方式 |
|-----------|------------------|
| **超过两页** | 为每个新页面创建额外的 `WidgetAnnotation` 对象，复用同一个 `textBoxField`。 |
| **每页不同字段名** | 创建独立的 `TextBoxField` 实例（例如 `CommentsPage1`、`CommentsPage2`），并为每个部件分配各自的父对象。 |
| **多行文本框** | 在添加部件之前设置 `textBoxField.Multiline = true;`。 |
| **只读字段** | 设置 `textBoxField.ReadOnly = true;` 以阻止用户编辑。 |
| **自定义字体** | 加载 `TrueTypeFont` 并通过 `textBoxField.DefaultAppearance = new DefaultAppearance(font, 12, Color.Black);` 进行分配。 |

这些变体展示了 AcroForm API 的灵活性，同时保持核心模式不变。

## 步骤回顾（快速参考）

1. **创建 PDF 文档** 并添加所需页面。  
2. **初始化 AcroForm** 并定义 `TextBoxField`。  
3. **在每页添加部件注释** 以放置文本框。  
4. **保存** 文档并测试交互行为。

## 后续步骤

现在您已经掌握了 **向 PDF 添加文本框** 和 **创建 AcroForm PDF** 的方法，可以进一步扩展表单：

* 使用 `CheckBoxField`、`RadioButtonField` 和 `ComboBoxField` 添加复选框、单选按钮或下拉列表。
* 将表单数据导出为 FDF 或 XFDF，以便服务器端处理。
* 为字段应用 JavaScript 动作，实现动态验证。

请查阅官方 Aspose.Pdf 文档，获取完整的表单字段类型列表及高级样式选项。

---

*您已经学习了如何 **创建 PDF 文档**、**向 PDF 添加页面**、**创建交互式 PDF 表单**、**向 PDF 添加文本框**，以及 **创建 AcroForm PDF**，并通过简洁可运行的示例实现。欢迎尝试其他字段类型和布局调整，以满足您的应用需求。*


## 接下来应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式。

- [How to Create PDF with Aspose – Add Form Field and Pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [How to Add Text Box PDF – Create PDF Form Field & Save Edited PDF Document](/pdf/english/net/programming-with-forms/how-to-add-text-box-pdf-create-pdf-form-field-save-edited-pd/)
- [Create PDF Document with Aspose – Add Page, Text Box, and Form](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}