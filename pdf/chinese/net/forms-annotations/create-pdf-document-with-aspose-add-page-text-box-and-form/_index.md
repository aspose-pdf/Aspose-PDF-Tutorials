---
category: general
date: 2025-12-31
description: 使用 Aspose.PDF 在 C# 中创建 PDF 文档。学习如何向 PDF 添加页面、添加文本框，并在一个指南中保存带有表单的 PDF。
draft: false
keywords:
- create pdf document
- add page to pdf
- save pdf with form
- how to add text box
- how to create pdf form
language: zh
og_description: 使用 Aspose.PDF 创建 PDF 文档。本教程展示如何向 PDF 添加页面、插入文本框以及保存带有表单的 PDF。
og_title: 使用 Aspose 创建 PDF 文档 – 添加页面、文本框、表单
tags:
- Aspose.Pdf
- C#
- PDF Forms
title: 使用 Aspose 创建 PDF 文档 – 添加页面、文本框和表单
url: /zh/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose 创建 PDF 文档 – 添加页面、文本框和表单

是否曾经需要以编程方式 **create PDF document**，却不知从何入手？你并非唯一的困惑——开发者们经常问：“如何在 PDF 中添加页面并嵌入表单字段而不费力？”好消息是 Aspose.PDF 让这变得轻而易举。在本教程中，我们将完整演示整个过程：从初始化 PDF、**adding page to PDF**、插入 **text box**，到最终 **saving PDF with form**，使其可供最终用户使用。

我们将覆盖所有必需的知识，包括每一步为何重要、常见陷阱以及一些能为你节省时间的专业技巧。完成后，你将拥有一个功能完整的 PDF 文件，包含两个关联的文本框小部件——非常适合签名、评论或任何数据采集场景。

## 你将学到

- 如何使用 Aspose.PDF for .NET 从头 **create PDF document**。  
- 精确 **add page to PDF** 的代码以及元素定位方法。  
- 正确的 **how to add text box** 方式，将其作为表单字段，并将多个小部件附加到同一字段。  
- 如何 **save PDF with form**，使字段在 Adobe Reader 或任何 PDF 查看器中保持交互性。  
- 故障排除和扩展示例的技巧（例如，添加验证、设置字体或合并多页）。

### 前置条件

- .NET 6.0 或更高（代码同样适用于 .NET Framework 4.6+）。  
- Aspose.PDF for .NET NuGet 包（`Install-Package Aspose.Pdf`）。  
- 对 C# 语法的基本了解——不需要深入的 PDF 知识。

如果你具备以上条件，让我们开始吧。

## 创建 PDF 文档 – 初始化 Aspose PDF

我们首先需要实例化一个 **Document** 对象。可以把它看作是所有内容将要存在的空画布。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

// Step 1: Create a new PDF document (this is the core of create pdf document)
Document pdfDocument = new Document();
```

> **为什么重要：** `Document` 类封装了整个 PDF 文件——元数据、页面、注释和表单字段。没有它，后续就无法添加页面或小部件。

## 向 PDF 添加页面 – 设置画布

没有页面的 PDF 本质上是一个空文件。添加页面很简单，但你选择的坐标会影响表单字段的显示位置。

```csharp
// Step 2: Add a single page to the document
Page pdfPage = pdfDocument.Pages.Add();

// Optional: set page size if you need something other than A4
// pdfPage.SetPageSize(PageSize.A4.Width, PageSize.A4.Height);
```

> **专业提示：** Aspose 使用的坐标系以 (0,0) 为左下角。我们稍后使用的 `Rectangle` 需要以点为单位（1 point = 1/72 英寸）。定位小部件时请记住这一点。

## 如何添加文本框 – 定义表单字段

现在进入有趣的部分：创建一个用户可以填写的 **text box**。在 PDF 术语中，这称为 `TextBoxField`。我们将创建一个字段并配备两个可视小部件——这样同一个值会出现在页面的两个位置。

```csharp
// Step 3: Define the first text box widget (the actual field definition)
TextBoxField firstTextBox = new TextBoxField(pdfPage, new Rectangle(100, 600, 300, 650))
{
    PartialName = "tb1",          // field name – must be unique within the form
    Value = "Enter text here",    // default placeholder text
    // Optional visual tweaks:
    Border = new Border(BorderStyle.Solid, 1, Color.Black),
    BackgroundColor = Color.LightGray,
    TextAlignment = HorizontalAlignment.Center
};

// Step 4: Define a second widget for the same field (appears lower on the page)
TextBoxField secondTextBoxWidget = new TextBoxField(pdfPage, new Rectangle(100, 500, 300, 550))
{
    PartialName = "tb1"   // same name links it to the first widget
};
```

> **为什么需要两个小部件？** 将多个矩形链接到相同的 `PartialName` 会创建一个 *单一* 的逻辑字段，拥有多个可视表示。用户在一个框中输入的内容会立即出现在另一个框中——对于像 “Customer ID” 这样的重复数据非常方便。

### 将字段添加到表单

Aspose 要求先将字段注册到文档的表单集合中，然后手动附加任何额外的小部件。

```csharp
// Step 5: Register the field (the first widget is automatically added)
pdfDocument.Form.Add(firstTextBox, "tb1", 1);

// Attach the second widget to the same field
pdfPage.Annotations.Add(secondTextBoxWidget);
```

> **注意：** 如果忘记调用 `Form.Add`，打开 PDF 时字段将不具交互性。始终先添加主小部件，再添加其他小部件。

## 保存带表单的 PDF – 完成文档

我们已经构建好结构；现在将其保存到磁盘。`Save` 方法写入文件，保留所有交互元素。

```csharp
// Step 6: Save the PDF – the file will contain both text box widgets
string outputPath = @"C:\Temp\TextBoxWithTwoWidgets.pdf";
pdfDocument.Save(outputPath);
```

> **结果：** 在 Adobe Reader 中打开生成的 PDF。你会看到两个相同的文本框；在其中一个输入内容会立即更新另一个。该文件已完全 **save pdf with form**‑就绪，可分发给用户进行数据收集。

## 完整工作示例

下面是完整的、可直接复制粘贴的程序。它可以编译为控制台应用，但你也可以在任何 .NET 项目中嵌入相同的逻辑。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;   // for Color, Border, etc.

class Program
{
    static void Main()
    {
        // 1️⃣ Create PDF document
        Document pdfDocument = new Document();

        // 2️⃣ Add a page
        Page pdfPage = pdfDocument.Pages.Add();

        // 3️⃣ First text box (primary widget)
        TextBoxField firstTextBox = new TextBoxField(pdfPage,
            new Rectangle(100, 600, 300, 650))
        {
            PartialName = "tb1",
            Value = "Enter text here",
            Border = new Border(BorderStyle.Solid, 1, Color.Black),
            BackgroundColor = Color.LightGray,
            TextAlignment = HorizontalAlignment.Center
        };

        // 4️⃣ Second widget linked to the same field
        TextBoxField secondTextBoxWidget = new TextBoxField(pdfPage,
            new Rectangle(100, 500, 300, 550))
        {
            PartialName = "tb1"
        };

        // 5️⃣ Register field and attach extra widget
        pdfDocument.Form.Add(firstTextBox, "tb1", 1);
        pdfPage.Annotations.Add(secondTextBoxWidget);

        // 6️⃣ Save the document
        string outputPath = @"C:\Temp\TextBoxWithTwoWidgets.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"PDF created successfully at: {outputPath}");
    }
}
```

### 预期输出

- 在指定文件夹中生成名为 **TextBoxWithTwoWidgets.pdf** 的文件。  
- 两个标有 “Enter text here” 的相同文本框。  
- 编辑任意一个框会立即更新另一个——证明该字段真正共享。

使用任何支持 AcroForms 的查看器（Adobe Reader、Foxit、Chrome）打开 PDF 并测试交互性。

## 常见问题与边缘情况

**Q: 如果需要超过两个小部件怎么办？**  
A: 只需创建更多使用相同 `PartialName` 的 `TextBoxField` 实例，并将它们添加到 `pdfPage.Annotations`。没有硬性限制。

**Q: 能设置最大字符长度吗？**  
A: 可以。在添加字段之前设置 `firstTextBox.MaxLength = 50;`（或任意整数）。

**Q: 如何将字段设为必填？**  
A: 使用 `firstTextBox.Required = true;`。大多数查看器在表单为空提交时会高亮该字段。

**Q: 我针对 PDF/A 归档——这仍然有效吗？**  
A: 完全可以。只需在保存前调用 `pdfDocument.Convert(new PdfFormatConversionOptions(PdfFormat.PDFA_1_A));`。表单字段仍然可用。

## 专业技巧与最佳实践

- **明智地复用字段名称：** 如果需要不同的字段，请为每个字段提供唯一的 `PartialName`。复用相同名称会创建共享值，这既是强大功能，也可能在忘记时导致错误。  
- **坐标转换：** 在屏幕上设计时可能使用像素。转换为点 (`points = pixels * 72 / DPI`) 可避免位置错误。  
- **性能技巧：** 若生成大量页面，复用单个 `TextBoxField` 定义并使用 `firstTextBox.Clone()` 克隆——可降低内存消耗。  
- **样式：** Aspose 允许嵌入字体（`pdfDocument.Fonts.Add(FontRepository.FindFont("Arial"))`），确保跨平台外观一致。

## 下一步

现在你已经了解 **how to create pdf document**、**add page to pdf**、**how to add text box** 和 **save pdf with form**，可以进一步扩展此方案：

- 为调查添加 **checkboxes** 或 **radio buttons**。  
- 从数据库程序化填充表单（例如，填写发票）。  
- 合并多个 PDF 为单个文件，同时保留表单字段。

如果你对生成表格、图像或数字签名感兴趣，请查看我们关于 *Aspose.PDF for .NET* 的其他指南。

**祝编码愉快！** 如有不清楚之处，请留言，或分享你在项目中如何自定义表单。 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}