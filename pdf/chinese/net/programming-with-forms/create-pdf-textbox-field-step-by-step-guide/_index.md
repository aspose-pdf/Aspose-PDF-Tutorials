---
category: general
date: 2026-06-21
description: 使用 C# 创建 PDF 文本框字段，并学习如何在几行代码内复制 PDF 表单字段或向 PDF 表单添加文本框。
draft: false
keywords:
- create pdf textbox field
- duplicate pdf form field
- add textbox to pdf form
- pdf form automation
- c# pdf library
language: zh
og_description: 快速创建 PDF 文本框字段。本指南展示如何复制 PDF 表单字段并使用现代 C# PDF 库向 PDF 表单添加文本框。
og_title: 创建 PDF 文本框字段 – 完整 C# 教程
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  headline: Create PDF Textbox Field – Step‑by‑Step Guide
  type: TechArticle
- description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  name: Create PDF Textbox Field – Step‑by‑Step Guide
  steps:
  - name: What if I need the field on *more* than two pages?
    text: Just repeat the clone‑and‑add steps for each additional page. The underlying
      data object stays the same, so all widgets stay in sync.
  - name: How do I change the appearance (font, border, background)?
    text: Each `Widget` has a `SetBorderColor`, `SetBorderWidth`, and `SetBackgroundColor`
      method. You can also assign a default appearance string (`DA`) to control the
      font and size.
  - name: Can I make the field read‑only after the user fills it?
    text: Yes. Set the `ReadOnly` flag on the field after you’ve collected the data,
      or toggle it based on your workflow.
  - name: What about PDFs that already contain a form?
    text: If the document already has an AcroForm, `doc.GetForm()` simply returns
      it. You can then add new fields without disturbing existing ones. Just be careful
      to use unique field names.
  type: HowTo
tags:
- PDF
- C#
- FormFields
title: 创建 PDF 文本框字段 – 步骤指南
url: /zh/net/programming-with-forms/create-pdf-textbox-field-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建 PDF 文本框字段 – 完整 C# 教程

是否曾需要**创建 PDF 文本框字段**却不确定该使用哪些 API 调用？你并不孤单。无论是构建合同签署门户还是一个简单的数据采集表单，在 PDF 中添加交互式文本框都是表单自动化开发者的核心技能。

在本指南中，我们将通过一个实用示例，演示如何**向 PDF 表单添加文本框**，以及如何**复制 PDF 表单字段**以便在多个页面上显示相同的输入。完成后，你将拥有一个可直接放入任何 .NET 项目的可运行程序。

## 你需要准备的环境

- .NET 6.0 或更高版本（代码同样适用于 .NET Core）  
- 一个现代的 C# PDF 库——下面的代码片段使用 **PDFTron SDK**，但概念同样适用于 iText 7、PdfSharp 或其他库。  
- Visual Studio 2022（或任意你喜欢的 IDE）  

就这些——无需额外服务，也没有晦涩的依赖。如果你已经有一个 PDF 需要增强，只需将代码指向该文件即可。

---

## 步骤 1：创建项目并导入 SDK

首先，创建一个控制台应用：

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
```

添加 PDFTron NuGet 包：

```bash
dotnet add package PDFTron.NET
```

现在打开 `Program.cs`，引入我们需要的命名空间：

```csharp
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;
```

> **专业提示:** 如果您使用的是其他库，请将 `using` 语句替换为等价的（例如 iText 7 的 `iText.Kernel.Pdf`）。

## 步骤 2：初始化 PDF 文档和表单

我们将从一个包含两页的全新 PDF 开始——第一页作为原始文本框的来源页，第二页作为复制目标页。

```csharp
PDFNet.Initialize();                     // Initialize the PDFTron runtime

// Create a new PDF document
using (PDFDoc doc = new PDFDoc())
{
    // Add two blank pages (letter size)
    Page sourcePage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(sourcePage);
    Page targetPage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(targetPage);

    // Get (or create) the AcroForm object
    Form form = doc.GetForm();
```

`Form` 对象是所有交互字段所在的地方。如果文档尚未包含表单，`GetForm()` 会为我们创建一个。

## 步骤 3：在第一页**创建 PDF 文本框字段**

现在进入本教程的核心——创建文本框字段。矩形坐标使用点（1 英寸 = 72 点）表示。示例将框放置在第一页的顶部中心附近。

```csharp
    // Step 1: Create a text box field on the first page and set its initial value
    TextBoxField textBoxField = new TextBoxField(sourcePage, new Rect(100, 500, 300, 520))
    {
        Value = "Sample"
    };
```

为什么要立即设置 `Value`？预填充字段可以给用户提供输入提示，同时也演示了字段已完全可用。

## 步骤 4：将字段添加到表单 – **向 PDF 表单添加文本框**

接下来，我们使用逻辑名称将字段注册到表单中。以后在代码中读取或修改字段数据时，需要使用这个名称。

```csharp
    // Step 2: Add the field to the form with a logical name
    form.Add(textBoxField, "multiBox");
```

选择一个清晰的名称（如 `"multiBox"`）可以让后续代码更易读，尤其是当你拥有数十个字段时。

## 步骤 5：在另一页**复制 PDF 表单字段**

常见需求是让同一字段出现在多页上——比如每页发票都需要一个“客户名称”框。PDFTron 允许我们克隆 widget 注释，即字段的可视化表示。

```csharp
    // Step 3: Clone the field's widget annotation so it can appear on another page
    Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

    // Step 4: Place the cloned widget on the second page
    targetPage.Annotations.Add(clonedWidget);
```

克隆后的 widget 与原始文本框共享同一底层数据。当用户在一个实例中输入时，另一个实例会自动更新——这就是**复制 PDF 表单字段**的魔力。

## 步骤 6：保存文档并清理

最后，将 PDF 写入磁盘并关闭 PDFNet 运行时。

```csharp
    // Save the resulting PDF
    doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
    Console.WriteLine("PDF created: output.pdf");
}

// Shut down PDFNet (optional but good practice)
PDFNet.Terminate();
```

运行程序后会生成一个两页的 PDF（`output.pdf`）。在 Adobe Acrobat Reader 中打开，点击第 1 页的文本框输入内容，然后切换到第 2 页——相同的文字会立即出现。这就是一个完整的**创建 PDF 文本框字段**示例，并实现了字段的复制。

---

## 完整可运行示例（复制粘贴即用）

```csharp
// Program.cs
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;

class Program
{
    static void Main()
    {
        PDFNet.Initialize();

        using (PDFDoc doc = new PDFDoc())
        {
            // Create two pages
            Page sourcePage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(sourcePage);
            Page targetPage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(targetPage);

            // Get the form (creates one if missing)
            Form form = doc.GetForm();

            // Step 1: Create a text box field on the first page
            TextBoxField textBoxField = new TextBoxField(sourcePage,
                new Rect(100, 500, 300, 520))
            {
                Value = "Sample"
            };

            // Step 2: Add the field to the form
            form.Add(textBoxField, "multiBox");

            // Step 3: Clone the widget so it appears on page 2
            Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

            // Step 4: Attach the cloned widget to the second page
            targetPage.Annotations.Add(clonedWidget);

            // Save the file
            doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
            Console.WriteLine("PDF created: output.pdf");
        }

        PDFNet.Terminate();
    }
}
```

**预期输出:** 一个名为 `output.pdf` 的文件，包含两页。两页都显示同一个标记为 “Sample” 的可编辑文本框。编辑任意一页，另一页会即时同步更新。

---

## 常见问题与边缘情况

### 如果需要在*超过两页*上放置该字段怎么办？

只需对每个额外页面重复克隆并添加的步骤。底层数据对象保持不变，所有 widget 将保持同步。

```csharp
Widget anotherClone = textBoxField.CreateWidgetAnnotation();
thirdPage.Annotations.Add(anotherClone);
```

### 如何更改外观（字体、边框、背景）？

每个 `Widget` 都有 `SetBorderColor`、`SetBorderWidth` 和 `SetBackgroundColor` 方法。你也可以为字段分配默认外观字符串（`DA`）来控制字体和大小。

```csharp
textBoxField.SetBorderColor(new ColorPt(0, 0, 1), 3); // blue border
textBoxField.SetBackgroundColor(new ColorPt(0.9, 0.9, 0.9), 3); // light gray fill
textBoxField.SetDefaultAppearance("Helvetica 12 Tf 0 g");
```

### 能否在用户填写后将字段设为只读？

可以。在收集完数据后为字段设置 `ReadOnly` 标志，或根据工作流动态切换。

```csharp
textBoxField.SetFlag(Field.Flag.e_readonly, true);
```

### 已经包含表单的 PDF 该怎么办？

如果文档已有 AcroForm，`doc.GetForm()` 只会返回已有的表单。随后你可以在不影响现有字段的情况下添加新字段，只需确保使用唯一的字段名称。

---

## 实际项目技巧

- **命名约定:** 为字段名前缀加上页面或章节标识（例如 `invoice_customer_name`），以避免冲突。  
- **验证:** 如需客户端验证，可使用 JavaScript 动作（`field.SetAction(Field.Action.e_keystroke, "event.rc = /^[A-Za-z]+$/.test(event.change);")`）。  
- **性能:** 处理大型 PDF 时，批量操作前调用 `doc.Lock()` 可降低 I/O 开销。  
- **可访问性:** 设置 `AlternateName` 属性，让屏幕阅读器能够描述该字段。

---

## 结论

我们已经**创建了 PDF 文本框字段**，展示了如何在多页之间**复制 PDF 表单字段**，并演示了使用 C# **向 PDF 表单添加文本框**的最简方法。完整、可运行的代码已在上方提供，你可以在此基础上添加样式、验证或更多页面。

准备好下一步了吗？尝试嵌入下拉框（`ChoiceField`）或签名部件，或探索在数据录入后将表单扁平化以便归档。PDFTron SDK（或任何类似库）为你提供了构建块——最终形态由你的想象决定。

如果遇到问题，欢迎在下方留言或查阅库的官方文档；其中包含大量与本教程互补的示例。祝编码愉快，愿你的表单始终保持同步！

## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并在项目中探索替代实现方式。每个资源都提供完整的可运行代码示例和逐步解释。

- [How to Create PDF with Aspose – Add Form Field and Pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Add Form Field in PDF Document using Java](/pdf/english/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)
- [Add Form Field In Pdf Document Using Java](/pdf/german/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}