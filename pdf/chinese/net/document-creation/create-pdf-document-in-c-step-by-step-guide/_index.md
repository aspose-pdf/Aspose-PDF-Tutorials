---
category: general
date: 2026-02-23
description: 快速在 C# 中创建 PDF 文档。学习如何向 PDF 添加页面、创建 PDF 表单字段、如何创建表单以及如何添加字段，并提供清晰的代码示例。
draft: false
keywords:
- create pdf document
- add pages to pdf
- create pdf form fields
- how to create form
- how to add field
language: zh
og_description: 使用实用教程在 C# 中创建 PDF 文档。了解如何向 PDF 添加页面、创建 PDF 表单字段、如何创建表单以及如何在几分钟内添加字段。
og_title: 在 C# 中创建 PDF 文档 – 完整编程演练
tags:
- C#
- PDF
- Form Generation
title: 在 C# 中创建 PDF 文档 – 步骤指南
url: /zh/net/document-creation/create-pdf-document-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中创建 PDF 文档 – 完整编程演练

是否曾经需要在 C# 中 **create PDF document**，但不确定从何入手？你并不孤单——大多数开发者在首次尝试自动化报告、发票或合同时都会遇到这个难题。好消息是？只需几分钟，你就能拥有一个具备多页和同步表单字段的完整功能 PDF，并且你将了解 **how to add field** 在跨页工作的方法。

在本教程中，我们将完整演示整个过程：从初始化 PDF，到 **add pages to PDF**，再到 **create PDF form fields**，最后解答 **how to create form** 如何共享单一值。无需外部参考，只需一个可以直接复制粘贴到项目中的完整代码示例。完成后，你将能够生成外观专业、行为如同真实表单的 PDF。

## Prerequisites

- .NET 6.0 或更高（代码同样适用于 .NET Framework 4.6 及以上）
- 一个提供 `Document`、`PdfForm`、`TextBoxField` 和 `Rectangle` 的 PDF 库（例如 Spire.PDF、Aspose.PDF，或任何兼容的商业/开源库）
- Visual Studio 2022 或你喜欢的 IDE
- 基础的 C# 知识（你会了解 API 调用为何重要）

> **Pro tip:** 如果你使用 NuGet，请使用 `Install-Package Spire.PDF`（或对应库的等价命令）安装包。  

现在，让我们开始吧。

---

## 第一步 – 创建 PDF 文档并添加页面

首先你需要一个空白画布。在 PDF 术语中，画布就是一个 `Document` 对象。拥有它后，你可以像向笔记本添加纸张一样 **add pages to PDF**。

```csharp
using Spire.Pdf;                 // Adjust the namespace to match your library
using Spire.Pdf.Graphics;        // For Rectangle definition

// Step 1: Initialize a new PDF document
Document pdfDocument = new Document();

// Add two pages – page indices start at 0 internally, but the library uses 1‑based indexing for convenience
pdfDocument.Pages.Add(); // Page 1
pdfDocument.Pages.Add(); // Page 2
```

*Why this matters:* `Document` 对象保存文件级元数据，而每个 `Page` 对象存储各自的内容流。提前添加页面为后续放置表单字段提供位置，并且使布局逻辑保持简洁。

---

## 第二步 – 设置 PDF 表单容器

PDF 表单本质上是交互式字段的集合。大多数库都会公开一个 `PdfForm` 类，你需要将其附加到文档上。可以把它看作一个了解哪些字段属于同一表单的“表单管理器”。

```csharp
// Step 2: Create a form container linked to the document
PdfForm pdfForm = new PdfForm(pdfDocument);
```

*Why this matters:* 如果没有 `PdfForm` 对象，你添加的字段将只是静态文本——用户无法输入。容器还允许你将相同的字段名称分配给多个小部件，这正是实现跨页 **how to add field** 的关键。

---

## 第三步 – 在第一页创建文本框

现在我们将在第 1 页创建一个文本框。`Rectangle` 定义了它在点（pt）单位下的位置 (x, y) 和尺寸 (宽度, 高度)，其中 1 pt ≈ 1/72 英寸。

```csharp
// Step 3: Define a TextBoxField on page 1
TextBoxField firstPageField = new TextBoxField(
    pdfDocument.Pages[0],                     // Zero‑based index for the first page
    new Rectangle(100, 100, 200, 20)          // Left, Bottom, Width, Height
);
```

*Why this matters:* 矩形坐标让你能够将字段与其他内容（如标签）对齐。`TextBoxField` 类型会自动处理用户输入、光标以及基本的验证。

---

## 第四步 – 在第二页复制字段

如果希望相同的值出现在多页上，你需要 **create PDF form fields** 并使用相同的名称。这里我们在第 2 页使用相同的尺寸放置第二个文本框。

```csharp
// Step 4: Define a matching TextBoxField on page 2
TextBoxField secondPageField = new TextBoxField(
    pdfDocument.Pages[1],                     // Second page (zero‑based index)
    new Rectangle(100, 100, 200, 20)
);
```

*Why this matters:* 通过镜像矩形，字段在各页之间保持一致——这是一点小小的用户体验提升。底层的字段名称会将这两个可视小部件关联在一起。

---

## 第五步 – 使用相同名称将两个小部件添加到表单

这正是实现 **how to create form** 共享单一值的核心。`Add` 方法接受字段对象、字符串标识符以及可选的页码。使用相同的标识符（`"myField"`）告诉 PDF 引擎这两个小部件代表同一个逻辑字段。

```csharp
// Step 5: Register both fields under the same name
pdfForm.Add(firstPageField, "myField", 1);   // Page number is 1‑based for the API
pdfForm.Add(secondPageField, "myField", 2);
```

*Why this matters:* 当用户在第一个文本框中输入时，第二个文本框会自动更新（反之亦然）。这对于多页合同非常适用，你可以在每页顶部放置同一个“Customer Name”字段。

---

## 第六步 – 将 PDF 保存到磁盘

最后，将文档写出。`Save` 方法接受完整路径；请确保文件夹已存在且你的应用拥有写入权限。

```csharp
// Step 6: Persist the PDF file
pdfDocument.Save(@"C:\Temp\output.pdf");

// Optionally open the file automatically (Windows only)
System.Diagnostics.Process.Start(@"C:\Temp\output.pdf");
```

*Why this matters:* 保存会完成内部流的最终化，扁平化表单结构，并使文件准备好分发。打开后即可立即验证结果。

---

## 完整可运行示例

下面是完整的可直接运行的程序。将其复制到控制台应用程序中，调整 `using` 语句以匹配你的库，然后按 **F5**。

```csharp
using System;
using Spire.Pdf;                 // Replace with your PDF library namespace
using Spire.Pdf.Graphics;        // For Rectangle

namespace PdfFormDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a new PDF document and add two pages
            Document pdfDocument = new Document();
            pdfDocument.Pages.Add(); // First page
            pdfDocument.Pages.Add(); // Second page

            // 2️⃣ Initialize a PdfForm container
            PdfForm pdfForm = new PdfForm(pdfDocument);

            // 3️⃣ Create a textbox on the first page
            TextBoxField firstPageField = new TextBoxField(
                pdfDocument.Pages[0],
                new Rectangle(100, 100, 200, 20));

            // 4️⃣ Create a matching textbox on the second page
            TextBoxField secondPageField = new TextBoxField(
                pdfDocument.Pages[1],
                new Rectangle(100, 100, 200, 20));

            // 5️⃣ Add both fields to the form using the same name
            pdfForm.Add(firstPageField, "myField", 1);
            pdfForm.Add(secondPageField, "myField", 2);

            // 6️⃣ Save the resulting PDF
            string outputPath = @"C:\Temp\output.pdf";
            pdfDocument.Save(outputPath);
            Console.WriteLine($"PDF saved to {outputPath}");

            // Open the PDF for quick verification (optional)
            System.Diagnostics.Process.Start(outputPath);
        }
    }
}
```

**Expected outcome:** 打开 `output.pdf`，你会看到两个相同的文本框——各在一页。向顶部文本框输入姓名，底部文本框会即时更新。这演示了 **how to add field** 正确工作，并确认表单按预期运行。

---

## 常见问题与边缘情况

### 如果需要超过两页怎么办？

只需根据需要多次调用 `pdfDocument.Pages.Add()`，然后为每个新页面创建 `TextBoxField` 并使用相同的字段名称注册。库会保持它们同步。

### 我可以设置默认值吗？

可以。创建字段后，赋值 `firstPageField.Text = "John Doe";`。相同的默认值会出现在所有关联的小部件上。

### 如何将字段设为必填？

大多数库都会公开一个 `Required` 属性：

```csharp
firstPageField.Required = true;
secondPageField.Required = true;
```

当 PDF 在 Adobe Acrobat 中打开时，如果用户尝试在未填写该字段的情况下提交，系统会提示。

### 样式（字体、颜色、边框）怎么办？

你可以访问字段的外观对象：

```csharp
firstPageField.Font = new PdfFont(PdfFontFamily.Helvetica, 12f);
firstPageField.BorderWidth = 1;
firstPageField.BorderColor = Color.Black;
```

对第二个字段使用相同的样式，以保持视觉一致性。

### 表单可以打印吗？

当然可以。由于字段是 *interactive* 的，打印时仍保留其外观。如果需要平面版，保存前调用 `pdfDocument.Flatten()`。

---

## 专业提示与常见坑

- **避免矩形重叠。** 重叠可能导致某些阅读器出现渲染错误。
- **记住 `Pages` 集合使用零基索引**；混用 0 基和 1 基索引是导致 “field not found” 错误的常见原因。
- **释放对象**，如果你的库实现了 `IDisposable`。将文档放在 `using` 块中以释放本机资源。
- **在多个阅读器中测试**（Adobe Reader、Foxit、Chrome）。某些阅读器对字段标志的解释略有差异。
- **版本兼容性：** 示例代码适用于 Spire.PDF 7.x 及以上版本。如果使用旧版本，`PdfForm.Add` 的重载可能需要不同的签名。

## 结论

现在，你已经掌握了在 C# 中从头 **how to create PDF document**、如何 **add pages to PDF**，以及最重要的，如何 **create PDF form fields** 以共享单一值，回答了 **how to create form** 与 **how to add field**。完整示例可直接运行，解释则提供了每行代码背后的 *why*。

准备好迎接下一个挑战了吗？尝试添加下拉列表、单选按钮组，甚至用于计算总额的 JavaScript 动作。这些概念都基于我们在此覆盖的相同基础。

如果你觉得本教程有帮助，请考虑与团队成员分享或为你保存 PDF 工具的仓库加星。祝编码愉快，愿你的 PDF 始终既美观又实用！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}