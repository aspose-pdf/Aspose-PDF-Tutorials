---
category: general
date: 2026-04-10
description: 使用 C# 创建 PDF 文档并提供清晰示例。学习如何添加多页 PDF、添加文本框字段、如何添加小部件，以及保存带有表单的 PDF。
draft: false
keywords:
- create pdf document c#
- add multiple pages pdf
- save pdf with form
- how to add widget
- add text box field
language: zh
og_description: 快速使用 C# 创建 PDF 文档。本指南展示了如何添加多页 PDF、添加文本框字段、添加小部件，以及保存带表单的 PDF。
og_title: 使用 C# 创建 PDF 文档 – 完整的多页表单教程
tags:
- C#
- PDF
- Form handling
title: 使用 C# 创建 PDF 文档 – 多页表单的逐步指南
url: /zh/net/programming-with-forms/create-pdf-document-c-step-by-step-guide-to-multi-page-forms/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建 PDF 文档 C# – 多页表单分步指南

有没有想过如何 **create PDF document C#**，让它跨越多页并包含交互式字段？也许你正在构建发票生成器、注册表单，或是用户稍后可以填写的简单报告。在本教程中，我们将完整演示整个过程——从初始化 PDF、添加多页、插入文本框字段、附加 widget 注释，到最终 **save PDF with form** 数据。没有废话，只有可以直接复制粘贴并立即运行的实战示例。

我们还会穿插一些实用技巧，例如*如何正确添加 widget*以及为何可能需要在页面之间复用字段。完成后，你将拥有一个名为 `multibox.pdf` 的示例，展示在两页之间共享的文本框。

## 前置条件

- .NET 6+（或 .NET Framework 4.7 或更高）——任何近期的运行时均可。
- 提供 `Document`、`TextBoxField` 和 `WidgetAnnotation` 类的 PDF 操作库。下面的代码使用流行的 **Aspose.PDF for .NET**，但概念同样适用于 iTextSharp、PdfSharp 或其他库。
- Visual Studio 2022 或你喜欢的任意 IDE。
- 基础 C# 知识——不需要深入了解 PDF 内部，只需会调用 API。

> **Pro tip:** 如果尚未安装该库，请在终端运行 `dotnet add package Aspose.PDF`。

## 步骤 1：Create PDF Document C# – 初始化 Document

首先，需要一个空白画布。`Document` 对象代表整个 PDF 文件。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Create a new PDF document
using (var document = new Document())
{
    // The rest of the code lives inside this using block
}
```

为什么要在 `using` 语句中包装文档？它保证所有非托管资源得到释放，并在调用 `Save` 时将文件刷新到磁盘。这是 C# 中处理 PDF 的推荐模式。

## 步骤 2：Add Multiple Pages PDF

没有页面的 PDF，简直是“隐形”。我们来添加两页——一页放置字段本身，另一页放置指向同一字段的 widget。

```csharp
// Step 2: Add two pages – one for the field, one for the widget
var firstPage = document.Pages.Add();
var secondPage = document.Pages.Add();
```

> **为什么是两页？** 当你希望相同的输入出现在多页时，只需创建一次 *field*，然后在其他页面使用 *widget annotations* 引用它。这样数据会自动保持同步。

下面是一张简单的示意图，直观展示了两页之间的关系（alt 文本已包含主要关键词以提升可访问性）。

![Create PDF document C# diagram showing field on page 1 and widget on page 2](image.png)

*Alt text: 创建 PDF 文档 C# 示例图，说明在两页之间共享的文本框字段。*

## 步骤 3：Add Text Box Field to Your PDF

现在在第一页放置一个文本框。矩形定义了它的位置和大小（坐标单位为点，72 pts = 1 inch）。

```csharp
// Step 3: Create a text box field on the first page and give it a shared name and value
var sharedTextBox = new TextBoxField(firstPage, new Rectangle(100, 600, 300, 620));
sharedTextBox.PartialName = "MultiBox";
sharedTextBox.Value = "Shared value";
```

- **PartialName** 是字段和任何 widget 共享的标识符。
- 在这里设置 `Value` 会为字段提供默认外观，该外观同样会出现在 widget 页面上。

## 步骤 4：How to Add Widget – 在另一页引用同一字段

widget 本质上是指向原始字段的可视占位符。复用相同的矩形后，widget 看起来与字段完全相同，只是位于不同的页面。

```csharp
// Step 4: Create a widget annotation on the second page that references the same field rectangle
var sharedWidget = new WidgetAnnotation(secondPage, sharedTextBox.Rect);
sharedWidget.PartialName = sharedTextBox.PartialName;
secondPage.Annotations.Add(sharedWidget);
```

> **常见坑点:** 忘记将 widget 添加到 `secondPage.Annotations`。如果缺少这行代码，widget 虽然已创建但根本不会显示。

## 步骤 5：Register the Field and Save PDF with Form

现在我们把新字段注册到文档的表单集合中。`Add` 方法接受字段实例及其名称。最后，将文件写入磁盘。

```csharp
// Step 5: Register the field with the document form
document.Form.Add(sharedTextBox, "MultiBox");

// Step 6: Save the PDF containing the multi‑page field
document.Save("YOUR_DIRECTORY/multibox.pdf");
```

当你在 Adobe Acrobat 或任何支持表单的 PDF 查看器中打开 `multibox.pdf` 时，会看到两页上都有相同的文本框。在一页上编辑，它会立即同步到另一页，因为它们共享同一个底层字段。

## 完整可运行示例

将所有代码组合在一起，下面是完整的、可直接运行的程序：

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Step 1: Create a new PDF document
        using (var document = new Document())
        {
            // Step 2: Add two pages – one for the field, one for the widget
            var firstPage = document.Pages.Add();
            var secondPage = document.Pages.Add();

            // Step 3: Create a text box field on the first page and give it a shared name and value
            var sharedTextBox = new TextBoxField(firstPage, new Rectangle(100, 600, 300, 620));
            sharedTextBox.PartialName = "MultiBox";
            sharedTextBox.Value = "Shared value";

            // Step 4: Create a widget annotation on the second page that references the same field rectangle
            var sharedWidget = new WidgetAnnotation(secondPage, sharedTextBox.Rect);
            sharedWidget.PartialName = sharedTextBox.PartialName;
            secondPage.Annotations.Add(sharedWidget);

            // Step 5: Register the field with the document form
            document.Form.Add(sharedTextBox, "MultiBox");

            // Step 6: Save the PDF containing the multi‑page field
            document.Save("multibox.pdf");
        }

        Console.WriteLine("PDF created successfully! Check the file 'multibox.pdf'.");
    }
}
```

### 预期结果

- **两页**：第 1 页显示带有默认文本 “Shared value” 的文本框。  
- **第 2 页** 镜像相同的框。任意一页输入后，另一页会即时更新。  
- 文件体积很小（几千字节），因为我们仅添加了简单的表单对象。

## 常见问题与边缘情况

### 可以为同一字段添加多个 widget 吗？

当然可以。只需在每个额外页面重复 widget 创建步骤，复用相同的 `PartialName`。这在多页合同中非常实用，常常需要在每页底部放置相同的签名字段。

### 第二页需要不同的大小或位置怎么办？

可以为 widget 创建新的 `Rectangle`，但仍使用相同的 `PartialName`。字段的值仍会同步，只是视觉布局可以在每页各自不同。

### 这能用于受密码保护的 PDF 吗？

可以，但必须先使用正确的密码打开文档：

```csharp
var document = new Document("protected.pdf", "ownerPassword");
```

随后按相同步骤继续。调用 `Save` 时库会保留加密信息。

### 如何以编程方式获取用户填写的值？

用户填写表单后再次加载 PDF 时：

```csharp
var loaded = new Document("multibox.pdf");
var field = loaded.Form["MultiBox"] as TextBoxField;
Console.WriteLine("User entered: " + field.Value);
```

### 如果想将表单扁平化（使字段不可编辑）怎么办？

在保存之前调用 `document.Form.Flatten()`。这会把交互式字段转换为静态内容，适用于最终的发票等场景。

## 小结

我们已经 **create PDF document C#**，实现了跨多页的文档，添加了可复用的文本框字段，演示了 **how to add widget** 注释，并最终 **save PDF with form** 数据。关键要点是：通过 widget 可以在任意数量的页面上可视化同一个字段，保持用户输入在整份文档中的一致性。

准备好迎接下一个挑战了吗？可以尝试：

- 使用相同模式添加 **checkbox** 或 **dropdown**。  
- 将 PDF 内容从数据库动态填充，而不是硬编码值。  
- 在 ASP.NET Core API 中将填好的 PDF 导出为字节数组供 HTTP 下载。

尽情实验、敢于出错再修复——这才是真正掌握 C# PDF 生成的方式。如果遇到问题，欢迎在下方留言或查阅库的官方文档获取更深入的细节。

祝编码愉快，构建更智能的 PDF！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}