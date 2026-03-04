---
category: general
date: 2026-03-03
description: 使用 Aspose.PDF 在 C# 中创建带页面的 PDF 并添加文本框表单字段。了解如何添加文本框、创建 PDF 表单字段以及快速添加多页
  PDF。
draft: false
keywords:
- create pdf with pages
- add text box pdf
- how to add textbox
- create pdf form field
- add multiple pages pdf
language: zh
og_description: 使用 Aspose.PDF 创建带页面的 PDF。本指南展示了如何添加文本框 PDF 字段、创建 PDF 表单字段以及在 C# 中添加多页
  PDF。
og_title: 使用 Pages 创建 PDF – 完整 C# 教程
tags:
- pdf
- csharp
- aspose
title: 使用页面和文本框字段创建 PDF – 完整 C# 指南
url: /zh/net/programming-with-forms/create-pdf-with-pages-and-text-box-fields-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用页面和文本框字段创建 PDF – 完整 C# 指南

是否曾需要 **创建带页面的 pdf**，并让用户能够输入备注？也许你在构建合同门户、反馈表单或简单问卷。在这种情况下，你会希望 PDF 不仅拥有多页，还包含可复用的文本框。好消息：使用 Aspose.PDF for .NET，你可以在几行代码内完成所有操作。

在本教程中，我们将逐步演示 **如何添加 textbox** 控件、注册一个 **create pdf form field**，以及最终 **add multiple pages pdf**，生成一个精致的交互式文档。没有废话——只提供可直接复制粘贴的代码，并解释每一步背后的原因。完成后，你将得到一个名为 `TextBoxTwoWidgets.pdf` 的 PDF，其中同一个文本框出现在两个不同页面上。

## 前置条件

- .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.6+）  
- Aspose.PDF for .NET NuGet 包（`Install-Package Aspose.PDF`）  
- 对 C# 类和对象释放有基本了解（我们将使用 `using` 块）  

> **专业提示：** 如果使用 Visual Studio，建议启用 *nullable reference types* 以获得更清晰的体验，但此示例并不强制要求。

## 步骤 1：创建带页面的 PDF – 初始化文档

首先需要创建一个空的 PDF 文档。把 `Document` 类想象成一本全新的笔记本，稍后会向其中添加页面。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

using (var pdfDocument = new Document())
{
    // The document is now ready for pages and form fields.
```

*为什么使用 `using` 块？* 它确保所有非托管资源（文件句柄、内存缓冲区）在使用完毕后立即释放，防止泄漏——在 Web 服务中生成大量 PDF 时尤为重要。

## 步骤 2：向第一页添加文本框 PDF 字段

文档已经创建好后，需要至少一个页面来放置表单字段。我们将添加 **两页**，因为希望同一个文本框出现在两页上。

```csharp
    // Add the first page
    var firstPage = pdfDocument.Pages.Add();

    // Add the second page (will host the widget copy)
    var secondPage = pdfDocument.Pages.Add();

    // Create a TextBoxField on the first page
    var notesField = new TextBoxField(
        firstPage,
        new Rectangle(50, 700, 300, 750))   // left, bottom, right, top
    {
        Name = "Notes",
        Value = "Type here..."
    };
```

矩形坐标遵循 PDF 坐标系（原点位于左下角）。`Name` 属性是内部标识符；稍后在用户填写表单后检索值时会用到它。

## 步骤 3：在第二页添加 Textbox Widget

*Widget* 是表单字段的可视化表现。默认情况下，一个字段在创建所在的页面上只有一个 widget。如果需要在另一页也显示同一个文本框，需要再添加一个 widget 注释。

```csharp
    // Place a second widget of the same field on the second page
    notesField.AddWidgetAnnotation(
        secondPage,
        new Rectangle(50, 500, 300, 550));
```

注意不同的 Y 坐标——这会把第二个文本框放在页面更低的位置。当然，你也可以使用相同的矩形，实现完全相同的布局。

## 步骤 4：创建 PDF 表单字段并注册

虽然已经实例化了 `notesField`，仍需将其注册到文档的 `Form` 集合中。此步骤使字段成为交互式表单结构的一部分。

```csharp
    // Register the field with the PDF form
    pdfDocument.Form.Add(notesField, notesField.Name);
```

如果省略此行，文本框虽然会在页面上显示，但不会被保存为表单字段，导致在处理 PDF 时其内容不会被提交。

## 步骤 5：保存 PDF 并验证多页面 PDF

最后，将文档写入磁盘。文件名随意，只要确保文件夹已存在且应用拥有写入权限即可。

```csharp
    // Save the resulting PDF
    pdfDocument.Save(@"C:\Temp\TextBoxTwoWidgets.pdf");
}
```

打开 `TextBoxTwoWidgets.pdf`（使用 Adobe Acrobat Reader），你会看到两页，每页都包含相同的 “Notes” 文本框。在第一页输入内容后切换到第二页——两个字段保持独立，因为它们共享同一个底层数据对象。

### 预期输出

- **第 1 页：** 文本框坐标为 (50, 700)，占位符为 “Type here…”。  
- **第 2 页：** 相同文本框位于更低位置 (50, 500)。  
- 两页属于同一个名为 “Notes” 的 **单一 PDF 表单**。  

你可以通过导出数据（Acrobat → Tools → Prepare Form → Export Data）进行测试，看到只有一条 `Notes` 条目。

## 常见变体和边缘情况

| 场景 | 需要更改的内容 | 原因 |
|----------|----------------|-----|
| **每页不同的默认文本** | 创建两个独立的 `TextBoxField` 对象并使用不同的 `Name` 值。 | 每个 widget 必须属于各自的字段，以保存独立的值。 |
| **只读文本框** | 在添加 widget 前设置 `notesField.ReadOnly = true;`。 | 防止用户编辑字段，同时仍可显示信息。 |
| **多行文本框** | 设置 `notesField.Multiline = true;` 并增大矩形高度。 | 允许输入更长的备注而无需滚动。 |
| **受密码保护的 PDF** | 保存后调用 `pdfDocument.Encrypt("ownerPwd", "userPwd", EncryptionAlgorithms.AESx128);`。 | 在保持表单字段的同时对文档进行加密。 |

## 使用 Aspose.PDF 表单的专业技巧

- **批量创建：** 若需要大量相同的 widget，可遍历 `pdfDocument.Pages`，在循环中调用 `AddWidgetAnnotation`。  
- **字段命名约定：** 使用前缀如 `txt_` 或 `fld_`，避免在后期合并 PDF 时出现冲突。  
- **性能优化：** 尽可能复用同一个 `Rectangle` 实例；库内部会复制其值，避免内存瓶颈。  

## 完整可运行示例（复制‑粘贴即可）

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using (var pdfDocument = new Document())
        {
            // 2️⃣ Add two pages – we’ll place a widget on each
            var firstPage = pdfDocument.Pages.Add();
            var secondPage = pdfDocument.Pages.Add();

            // 3️⃣ Define the textbox field (add text box pdf)
            var notesField = new TextBoxField(
                firstPage,
                new Rectangle(50, 700, 300, 750))
            {
                Name = "Notes",
                Value = "Type here..."
            };

            // 4️⃣ Add a second widget on the second page (how to add textbox)
            notesField.AddWidgetAnnotation(
                secondPage,
                new Rectangle(50, 500, 300, 550));

            // 5️⃣ Register the field (create pdf form field)
            pdfDocument.Form.Add(notesField, notesField.Name);

            // 6️⃣ Save the file (add multiple pages pdf)
            pdfDocument.Save(@"C:\Temp\TextBoxTwoWidgets.pdf");
        }

        System.Console.WriteLine("PDF created successfully!");
    }
}
```

运行程序，打开生成的文件，你将看到与教程描述完全一致的效果。

## 结论

我们已经 **创建了带页面的 pdf**，其中包含可复用的 **add text box pdf** 表单元素，演示了在多页上 **how to add textbox** widget 的方法，并正确 **create pdf form field**。最终文档证明，你可以在 **add multiple pages pdf** 的同时保持表单的交互性和轻量化。

接下来可以尝试添加复选框、单选按钮，甚至 JavaScript 动作，让 PDF 真正动态化。你也可以探索将多个此类 PDF 合并为单一报告——Aspose.PDF 能轻松搞定。

有问题或想分享酷炫的使用场景吗？在下方留言吧，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}