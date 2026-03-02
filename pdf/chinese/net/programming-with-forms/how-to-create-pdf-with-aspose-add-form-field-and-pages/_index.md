---
category: general
date: 2026-01-02
description: 如何使用 Aspose.Pdf 在 C# 中创建 PDF。学习添加表单字段、添加页面、嵌入文本框以及保存带表单的 PDF——一站式指南。
draft: false
keywords:
- how to create pdf
- add form field pdf
- add pages pdf
- pdf with text box
- save pdf with forms
language: zh
og_description: 如何使用 Aspose.Pdf 在 C# 中创建 PDF。逐步指南：添加表单字段、添加页面、插入文本框，并保存带表单的 PDF。
og_title: 如何使用 Aspose 创建 PDF – 添加表单字段和页面
tags:
- Aspose.Pdf
- C#
- PDF Forms
title: 如何使用 Aspose 创建 PDF – 添加表单字段和页面
url: /zh/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose 创建 PDF – 添加表单字段和页面

是否曾经想过 **如何创建 PDF** 文档并包含交互式字段，却感到束手无策？你并不孤单。许多开发者在需要多页文本框或想将同一个表单字段附加到多个页面时都会卡住。

在本教程中，我们将逐步演示一个完整、可直接运行的示例，展示如何 **add form field PDF**、**add pages PDF**、嵌入 **pdf with text box**，以及最终 **save PDF with forms**。完成后，你将得到一个文件，使用 Acrobat 打开时可以在三个不同页面看到相同的文本框。

> **Pro tip:** Aspose.Pdf 支持 .NET 6+、.NET Framework 4.6+，甚至 .NET Core。开始之前请确保已安装 NuGet 包 `Aspose.Pdf`。

## 前提条件

- Visual Studio 2022（或任意你喜欢的 C# IDE）
- 已安装 .NET 6 SDK
- NuGet 包 `Aspose.Pdf`（截至 2026 年的最新版本）
- 对 C# 语法有基本了解

如果以上任意一点不熟悉，只需安装 SDK 并添加该包——后续指南默认你已经能够打开一个控制台项目。

## 第一步：创建项目并导入命名空间

首先，创建一个新的控制台应用：

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
dotnet add package Aspose.Pdf
```

现在打开 `Program.cs`，在文件顶部添加所需的 `using` 语句：

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
```

这些命名空间让你能够使用 `Document`、`Page` 和 `TextBoxField` 类。

## 第二步：创建一个全新的 PDF 文档

在向文档中添加任何字段之前，需要先有一个空白画布。`Document` 类代表整个 PDF 文件。

```csharp
// Step 2: Initialize a new PDF document
using (var pdfDocument = new Document())
{
    // All further steps will live inside this block
}
```

将文档放在 `using` 块中，可确保在保存文件后自动释放资源。

## 第三步：添加初始页面

没有页面的 PDF 等于不存在。先添加第一页，文本框将在此页面首次出现。

```csharp
// Step 3: Add the first page (the field will be placed on this page initially)
Page firstPage = pdfDocument.Pages.Add();
```

`Pages.Add()` 方法返回一个 `Page` 对象，后续在定位小部件时可以引用它。

## 第四步：定义多页 TextBoxField

下面是核心代码：一个 `TextBoxField` 将被附加到多个页面。可以把字段视为数据容器，每个小部件则是特定页面上的可视化表现。

```csharp
// Step 4: Create a TextBox field that will span multiple pages
var multiPageTextBox = new TextBoxField(firstPage, new Rectangle(100, 600, 300, 650))
{
    PartialName = "MultiPageComment",
    Value = "Enter comment here..."
};
```

- **PartialName** 是内部标识符；在表单中必须唯一。
- **Value** 设置用户看到的默认文本。
- `Rectangle` 定义小部件的位置（左、下、右、上），单位为点。

## 第五步：添加额外页面并附加小部件

接下来确保文档至少有三页，然后使用 `AddWidgetAnnotation` 将同一个文本框附加到第 2 页和第 3 页。

```csharp
// Ensure the document has at least three pages
pdfDocument.Pages.Add(); // page 2
pdfDocument.Pages.Add(); // page 3

// Attach the same field to the new pages (widgets)
multiPageTextBox.AddWidgetAnnotation(pdfDocument.Pages[2], new Rectangle(100, 600, 300, 650));
multiPageTextBox.AddWidgetAnnotation(pdfDocument.Pages[3], new Rectangle(100, 600, 300, 650));
```

每次调用都会在目标页面上创建一个可视化小部件，但仍链接回原始的 `TextBoxField`。在任意页面编辑文本框时，所有实例的值会自动同步——这对于审阅表单或合同非常实用。

## 第六步：将字段注册到表单集合

如果省略此步骤，字段将不会出现在 PDF 的交互式表单层次结构中，Acrobat 也会忽略它。

```csharp
// Step 6: Add the field to the form collection
pdfDocument.Form.Add(multiPageTextBox, "MultiPageComment");
```

第二个参数是字段在 PDF 内部表单字典中的名称。保持名称一致有助于后续以编程方式提取数据。

## 第七步：将 PDF 保存到磁盘

最后，将文档写入文件。请选择一个有写入权限的文件夹；本例中使用名为 `output` 的子文件夹。

```csharp
// Step 7: Save the PDF with the multi‑page textbox
pdfDocument.Save("output/MultiWidgetTextBox.pdf");
```

当你在 Adobe Acrobat Reader 中打开 `output/MultiWidgetTextBox.pdf` 时，会看到第 1‑3 页都有相同的文本框。对任意实例进行输入，所有页面的文本框都会同步更新——正是我们想要的效果。

## 完整可运行示例

下面是可以直接复制粘贴到 `Program.cs` 的完整程序。它可以直接编译运行。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

namespace PdfFormDemo
{
    internal class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new PDF document
            using (var pdfDocument = new Document())
            {
                // Step 2: Add the first page (the field will be placed on this page initially)
                Page firstPage = pdfDocument.Pages.Add();

                // Step 3: Create a TextBox field that will span multiple pages
                var multiPageTextBox = new TextBoxField(firstPage, new Rectangle(100, 600, 300, 650))
                {
                    PartialName = "MultiPageComment",
                    Value = "Enter comment here..."
                };

                // Step 4: Ensure the document has at least three pages
                pdfDocument.Pages.Add(); // page 2
                pdfDocument.Pages.Add(); // page 3

                // Step 5: Attach the same field to additional pages (widgets)
                multiPageTextBox.AddWidgetAnnotation(pdfDocument.Pages[2], new Rectangle(100, 600, 300, 650));
                multiPageTextBox.AddWidgetAnnotation(pdfDocument.Pages[3], new Rectangle(100, 600, 300, 650));

                // Step 6: Add the field to the form collection
                pdfDocument.Form.Add(multiPageTextBox, "MultiPageComment");

                // Step 7: Save the PDF with the multi‑page textbox
                pdfDocument.Save("output/MultiWidgetTextBox.pdf");
            }
        }
    }
}
```

### 预期结果

- PDF 中 **三页**。
- 每页 **一个文本框**，坐标为 (100, 600)‑(300, 650)。
- **内容同步**：在任意页面编辑文本框，其他页面会同步更新。
- 文件保存为 `output/MultiWidgetTextBox.pdf`。

## 常见问题与边缘情况

### 如果需要在三页以上添加文本框怎么办？

只需使用 `pdfDocument.Pages.Add()` 再添加页面，并对每个新页面重复调用 `AddWidgetAnnotation`。字段对象保持不变，只是额外创建了小部件。

### 能否独立修改每个小部件的外观（字体、颜色）？

可以。创建小部件后，可通过 `multiPageTextBox.Widgets` 获取并修改其 `Appearance` 属性。不过，需要注意，修改一个小部件的外观不会自动影响其他小部件，除非分别进行设置。

```csharp
var widget = multiPageTextBox.Widgets[1]; // second widget (page 2)
widget.Appearance.NormalGraphicsState.Font = FontRepository.FindFont("Helvetica");
widget.Appearance.NormalGraphicsState.FontSize = 12;
widget.Appearance.NormalGraphicsState.TextColor = Color.GetBlue();
```

### 如何在后期提取用户填写的值？

当用户填写完 PDF 并将文件返回时，使用 Aspose.Pdf 读取表单字段：

```csharp
var filledDoc = new Document("filled.pdf");
var field = (TextBoxField)filledDoc.Form["MultiPageComment"];
Console.WriteLine($"User entered: {field.Value}");
```

### PDF/A 合规性怎么办？

如果需要 PDF/A‑1b 合规，在保存之前调用 `pdfDocument.ConvertToPdfA()`。表单字段仍然可用，但某些 PDF/A 查看器可能限制编辑。请针对目标受众进行测试。

## 提示与最佳实践

- **使用有意义的字段名称**——有助于轻松提取数据。
- **避免小部件重叠**——如果同一页面上两个小部件占据相同空间，Acrobat 可能会抛出 “field name already exists” 错误。
- 仅在需要用户编辑时才将 `ReadOnly = false` 设置为 `false`，否则请锁定字段以防意外更改。
- 在各页之间保持 **矩形坐标一致**，以获得统一外观；除非有意让尺寸不同。

## 结论

现在，你已经掌握了 **如何使用 Aspose.Pdf 创建包含可复用表单字段的多页 PDF**。通过七个步骤——初始化文档、添加页面、定义 `TextBoxField`、附加小部件、注册字段、保存文件——即可构建复杂的交互式 PDF，而无需第三方表单设计器。

接下来，尝试扩展此模式：添加复选框、下拉列表，甚至数字签名。所有这些都可以使用相同的“小部件‑附加”技术绑定到多个页面，从而实现 **add form field PDF**、**add pages PDF** 与 **save PDF with forms** 的完整工作流。

祝编码愉快，愿你的 PDF 如同想象般交互丰富！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}