---
category: general
date: 2026-06-08
description: 使用 Aspose.Pdf 在 C# 中创建多页表单。学习如何向 PDF 添加文本框、创建 PDF 表单字段，并使用清晰的代码示例保存更新后的
  PDF。
draft: false
keywords:
- create multi page form
- add textbox to pdf
- create pdf form field
- how to save pdf
- save updated pdf
language: zh
og_description: 使用 Aspose.Pdf 在 C# 中创建多页表单。本指南展示如何向 PDF 添加文本框、创建 PDF 表单字段，并在几分钟内保存更新后的
  PDF。
og_title: 在 C# 中创建多页表单 – 完整的 Aspose.Pdf 教程
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create multi page form in C# using Aspose.Pdf. Learn how to add textbox
    to pdf, create pdf form field, and save updated pdf with clear code examples.
  headline: Create Multi Page Form in C# with Aspose.Pdf – Step‑by‑Step Guide
  type: TechArticle
- description: Create multi page form in C# using Aspose.Pdf. Learn how to add textbox
    to pdf, create pdf form field, and save updated pdf with clear code examples.
  name: Create Multi Page Form in C# with Aspose.Pdf – Step‑by‑Step Guide
  steps:
  - name: '**Load** the existing PDF.'
    text: '**Load** the existing PDF.'
  - name: '**Create** a `TextBoxField` on the first page – this is our form field.'
    text: '**Create** a `TextBoxField` on the first page – this is our form field.'
  - name: '**Add** a widget annotation on the second page so the same field appears
      there too.'
    text: '**Add** a widget annotation on the second page so the same field appears
      there too.'
  - name: '**Save** the modified document as a new file.'
    text: '**Save** the modified document as a new file.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF Forms
title: 使用 Aspose.Pdf 在 C# 中创建多页表单 – 步骤指南
url: /zh/net/programming-with-forms/create-multi-page-form-in-c-with-aspose-pdf-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Pdf 在 C# 中创建多页表单 – 完整指南

是否曾想过在 C# 中**创建多页表单**而不必与底层 PDF 规范搏斗？你并不是唯一的。无论是构建求职申请门户还是报税向导，多页 PDF 表单都能让数据收集显得流畅且专业。

在本教程中，我们将通过一个真实案例演示**向 pdf 添加文本框**、**创建 pdf 表单字段**，并最终**保存更新后的 pdf**。完成后，你将拥有一个可直接嵌入任何 .NET 项目的两页表单。

> **专业提示：** Aspose.Pdf 支持 .NET 6+、.NET Framework 4.6+ 以及 .NET Core，无论你在 Windows 还是 Linux 上，都能使用。

## 所需环境

- **Aspose.Pdf for .NET**（NuGet 包 `Aspose.Pdf`）。  
- 一个已有至少两页的简单 PDF 文件（`input.pdf`）。  
- Visual Studio 2022 或任何支持 C# 的编辑器。  
- 一个可读写的文件夹——我们将在示例中称其为 `YOUR_DIRECTORY`。

除此之外无需其他依赖。准备好了吗？让我们开始吧。

![使用 Aspose.Pdf 在 C# 中创建多页表单示例](image.png "使用 Aspose.Pdf 在 C# 中创建多页表单示例")

## 创建多页表单 – 概览

在编写代码之前，先梳理一下高层流程：

1. **加载**已有的 PDF。  
2. **创建**第一页上的 `TextBoxField`——这就是我们的表单字段。  
3. **在第二页添加**一个 widget 注释，使同一字段也出现在该页。  
4. **保存**修改后的文档为新文件。

每一步都被刻意隔离，方便你在不破坏整体的前提下替换某些部件（例如更改矩形大小或添加更多页面）。

## 步骤 1 – 加载 PDF 文档

使用任何 PDF 库时的第一件事就是打开源文件。Aspose.Pdf 只需一行代码即可完成。

```csharp
// Step 1: Load the PDF document from disk
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document(@"YOUR_DIRECTORY\input.pdf");
```

*为什么这很重要：* 加载文档后，你即可访问 `Pages` 集合，后续将在其中附加表单字段和 widget。如果文件未找到会抛出异常，请确保路径正确。

## 步骤 2 – 创建文本框表单字段（add textbox to pdf）

现在我们真正**创建 pdf 表单字段**——一个 `TextBoxField`。它相当于一个数据容器，用来保存用户输入的内容。

```csharp
// Step 2: Instantiate a TextBoxField on page 1
Aspose.Pdf.Forms.TextBoxField commentsField = new Aspose.Pdf.Forms.TextBoxField(
    pdfDocument.Pages[1],                                   // target page (1‑based index)
    new Aspose.Pdf.Rectangle(100, 100, 300, 120));         // position & size (LLX, LLY, URX, URY)
```

几点说明：

- 矩形坐标使用点（1 pt = 1/72 in）表示。根据你的布局自行调整。  
- `pdfDocument.Pages[1]` 指的是**第一页**，因为 Aspose 使用 1 基索引集合。  
- 在第 1 页创建字段时会同时生成默认外观，后面在第 2 页添加 widget 时会复用该外观。

## 步骤 3 – 设置字段名称和初始值

每个表单字段都需要一个标识符。后续提取用户输入时会通过该字符串引用。

```csharp
// Step 3: Assign a name and an empty default value
commentsField.Name = "Comments";   // unique field name
commentsField.Value = "";          // start with a blank textbox
```

*为什么叫 “Comments”？* 这个名字直观易懂，你也可以随意命名（如 `"Address"`、`"PhoneNumber"`），只要在整个 PDF 中保持唯一即可；重复名称会导致提交时数据冲突。

## 步骤 4 – 在第二页添加 Widget 注释

*widget* 是表单字段在特定页面上的可视化表现。默认情况下，我们创建的字段只存在于第 1 页。若要让同一文本框出现在第 2 页，需要添加一个 widget 注释。

```csharp
// Step 4: Place the same TextBoxField on page 2 via a widget
commentsField.Widgets.Add(
    new Aspose.Pdf.Forms.WidgetAnnotation(
        pdfDocument.Pages[2],                               // second page
        new Aspose.Pdf.Rectangle(50, 50, 250, 70)));       // widget rectangle
```

为什么需要 widget？因为 PDF 表单将**字段定义**（数据）与**widget 外观**（用户看到的内容）分离。添加 widget 可以让用户在多页上填写同一个字段，这是多页表单的经典需求。

### 边缘案例提示

如果源 PDF 超过两页且希望在每页都出现文本框，只需遍历 `pdfDocument.Pages` 并为每页添加一个 widget。记得根据每页的布局调整矩形大小。

## 步骤 5 – 保存更新后的 PDF（how to save pdf）

最后将修改写入磁盘。Aspose.Pdf 提供直观的 `Save` 方法，可覆盖或创建新文件。

```csharp
// Step 5: Save the updated PDF to a new file
pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
```

*为什么不直接覆盖 `input.pdf`？* 保留原始文件有助于调试，并且可以对比前后效果。如果确实需要替换源文件，只需使用相同路径调用 `Save` 即可。

## 完整可运行示例

将上述代码整合后，即得到下面的完整示例程序。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // Load the existing PDF (make sure the file exists)
        Document pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // Create a TextBoxField on the first page
        TextBoxField commentsField = new TextBoxField(
            pdfDocument.Pages[1],
            new Rectangle(100, 100, 300, 120));

        // Configure the field
        commentsField.Name = "Comments";
        commentsField.Value = ""; // blank by default

        // Add a widget on the second page so the same field appears there
        commentsField.Widgets.Add(
            new WidgetAnnotation(
                pdfDocument.Pages[2],
                new Rectangle(50, 50, 250, 70)));

        // Save the modified PDF
        pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");

        // Optional: inform the user
        System.Console.WriteLine("Multi‑page form created successfully!");
    }
}
```

### 预期输出

在 Adobe Acrobat Reader 中打开 `output.pdf` 时：

- 第 1 页会在坐标 (100, 100)‑(300, 120) 处显示一个空文本框。  
- 第 2 页会在坐标 (50, 50)‑(250, 70) 处显示相同的文本框。  
- 两个框共享 **字段名称** `Comments`，因此在任意一页输入的数据会自动同步。

## 常见问题与注意事项

| 问题 | 解答 |
|----------|--------|
| *可以添加多个文本框吗？* | 当然可以。只需使用新的 `TextBoxField` 实例并为其指定唯一 `Name`，重复步骤 2‑4 即可。 |
| *如果 PDF 没有第二页会怎样？* | 代码会抛出 `ArgumentOutOfRangeException`。可使用 `if (pdfDocument.Pages.Count >= 2) { … }` 进行判断。 |
| *需要设置字体吗？* | Aspose 默认使用 Helvetica。若需自定义字体，可在保存前设置 `commentsField.DefaultAppearance.Font`。 |
| *字段可打印吗？* | 是的——Aspose 默认将 widget 标记为可打印。如有需要，可通过 `WidgetAnnotation.Flags` 调整。 |
| *以后如何提取填写的值？* | 用户填写并返回 PDF 后，调用 `pdfDocument.Form["Comments"].Value` 即可读取数据。 |

## 后续步骤

了解了**如何在添加文本框后保存 pdf**后，你可以进一步探索：

- 添加**复选框**或**单选按钮**（`CheckBoxField`、`RadioButtonField`）。  
- 使用**JavaScript**动作进行客户端校验（`commentsField.Actions.OnMouseUp = "…"`）。  
- **扁平化**表单以防止后续编辑（`pdfDocument.Form.Flatten()`）。  

所有这些都基于我们在**创建多页表单**时掌握的概念。

---

**结论：** 你已经学会了如何在 C# 中使用 Aspose.Pdf **创建多页表单**、**向 pdf 添加文本框**、**创建 pdf 表单字段**，以及**保存更新后的 pdf**的完整步骤。随意调整矩形、添加更多字段，或遍历所有页面，实现真正动态的解决方案。

有想法或技巧想分享？在下方留言吧，祝编码愉快！

## 接下来该学习什么？

以下教程与本指南紧密相关，基于相同技术实现，提供完整代码示例和逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方式。

- [How to Create PDF with Aspose – Add Form Field and Pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Create PDF Document with Aspose – Add Page, Text Box, and Form](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)
- [How to Add and Extract PDF Form Fields Using Aspose.PDF for .NET: A Comprehensive Guide](/pdf/english/net/forms-annotations/manage-pdf-form-fields-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}