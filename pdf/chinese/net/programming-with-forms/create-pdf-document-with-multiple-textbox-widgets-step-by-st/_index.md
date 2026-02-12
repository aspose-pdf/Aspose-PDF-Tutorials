---
category: general
date: 2026-02-12
description: 创建 PDF 文档并在构建表单字段时添加空白页——快速学习如何在 C# 中添加文本框 PDF 小部件。
draft: false
keywords:
- create pdf document
- add blank page pdf
- create pdf form field
- how to create pdf form
- how to add textbox pdf
language: zh
og_description: 创建包含空白页和多个文本框小部件的 PDF 文档。请按照本指南了解如何使用 Aspose.Pdf 添加文本框 PDF 字段。
og_title: 创建 PDF 文档 – 在 C# 中添加文本框小部件
tags:
- pdf
- csharp
- aspose
- form-fields
title: 创建包含多个文本框小部件的 PDF 文档 – 步骤指南
url: /zh/net/programming-with-forms/create-pdf-document-with-multiple-textbox-widgets-step-by-st/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建带多个文本框小部件的 PDF 文档 – 完整教程

是否曾需要 **create pdf document**（创建 PDF 文档），其中包含一个包含多个 textbox 小部件的表单？你并不孤单——开发者常常会问，*“如何添加出现在两个位置的 textbox pdf 字段？”* 好消息是 Aspose.Pdf 让这变得轻而易举。在本指南中，我们将逐步演示创建 PDF、添加空白页面 pdf、构建表单字段，最后展示 **how to add textbox pdf**（如何添加 textbox pdf）小部件的编程方式。

我们将覆盖您需要了解的所有内容：从初始化文档到保存最终文件。完成后，您将拥有一个可直接使用的 PDF，演示了 **how to create pdf form**（如何创建 pdf 表单）元素的多小部件用法，并且您会了解保持表单在各种 PDF 查看器中可靠运行的一些细微差别。

## 您需要的条件

- **Aspose.Pdf for .NET**（任何近期版本；此处使用的 API 适用于 23.x 及更高版本）。  
- .NET 开发环境（Visual Studio、Rider，或甚至带 C# 扩展的 VS Code）。  
- 对 C# 语法有基本了解——不需要深入的 PDF 知识。

如果您已满足上述条件，让我们开始吧。

## 步骤 1：创建 PDF 文档 – 初始化并添加空白页面

我们首先要做的是 **create pdf document** 对象并为其提供一个干净的画布。添加空白页面 pdf 只需调用 `Pages.Add()` 即可。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

public class MultiWidgetExample
{
    public static void Main()
    {
        // Step 1: Create a new PDF document (the canvas)
        using (var pdfDocument = new Document())
        {
            // Step 2: Add a blank page pdf to the document
            var pdfPage = pdfDocument.Pages.Add();

            // The rest of the steps follow...
```

*为什么这很重要：* `Document` 类代表整个文件。没有页面，就没有放置表单字段的地方，因此空白页面 pdf 是您将要构建的任何表单的基础。

## 步骤 2：创建 PDF 表单字段 – 定义可容纳多个小部件的 TextBox

现在我们创建实际的 **create pdf form field**。Aspose 将其称为 `TextBoxField`。将 `MultipleWidgets = true` 设置为 true，告诉引擎该字段可以出现多次。

```csharp
            // Step 3: Create a TextBox field that supports multiple widgets
            var multiWidgetTextBox = new TextBoxField(
                pdfPage,
                new Rectangle(50, 700, 250, 730)); // position on the first page
            multiWidgetTextBox.MultipleWidgets = true;   // enable multiple widgets
            multiWidgetTextBox.Value = "First widget";
```

*专业提示：* 矩形坐标以点为单位（1 pt = 1/72 in）。根据您的布局进行调整；示例将框放置在左上角附近。

## 步骤 3：向表单添加第一个小部件

在定义字段后，我们将其附加到文档的表单集合中。这就是针对主小部件的 **how to add textbox pdf** 步骤。

```csharp
            // Step 4: Add the TextBox field to the form (first widget)
            pdfDocument.Form.Add(multiWidgetTextBox, "MultiTB", 1);
```

第三个参数（`1`）是小部件索引——从 1 开始，因为我们已经在前一步创建的页面上有一个小部件。

## 步骤 4：以编程方式附加第二个小部件 – 多小部件的真正威力

如果您曾想了解 **how to create pdf form**（如何创建 pdf 表单）元素的重复方式，这里就是魔法发生的地方。我们实例化一个 `WidgetAnnotation` 并将其添加到字段的 `Widgets` 集合中。

```csharp
            // Step 5: Create and attach a second widget programmatically
            var secondWidget = new WidgetAnnotation(
                new Rectangle(300, 700, 500, 730)); // position on the same page
            multiWidgetTextBox.Widgets.Add(secondWidget);
```

*为什么要添加第二个小部件？* 用户可能需要在两个位置填写相同的值——比如在表单顶部和签名块中都出现的 “Customer Name” 字段。通过共享相同的字段名（`MultiTB`），在一个位置的更改会自动更新另一个位置。

## 步骤 5：保存 PDF – 验证两个小部件是否出现

最后，我们将文档写入磁盘。文件将包含两个同步的 textbox 小部件。

```csharp
            // Step 6: Save the PDF with both widgets
            pdfDocument.Save("multiWidget.pdf");
        }
    }
}
```

当您在 Adobe Acrobat、Foxit 或甚至浏览器的 PDF 查看器中打开 `multiWidget.pdf` 时，您会看到并排的两个文本框。在一个框中输入会立即更新另一个——这证明我们已经成功 **how to add textbox pdf**（如何添加 textbox pdf）并使用了多个小部件。

### 预期结果

- 一个名为 `multiWidget.pdf` 的单页 PDF。  
- 两个标记为 “First widget” 的 textbox 小部件。  
- 两个框共享相同的字段名，因此它们的内容会相互镜像。

![创建 PDF 文档，包含多个文本框小部件](https://example.com/images/multi-widget.png "创建 PDF 文档示例")

*图片替代文字:* 创建 PDF 文档显示两个文本框小部件

## 常见问题与边缘情况

### 我可以将小部件放在不同的页面上吗？

当然可以。只需为第二个小部件创建一个新的 `Page` 对象并使用其坐标。由于名称（`"MultiTB"`）保持不变，字段仍然会关联。

```csharp
var secondPage = pdfDocument.Pages.Add();
var thirdWidget = new WidgetAnnotation(new Rectangle(50, 700, 250, 730));
multiWidgetTextBox.Widgets.Add(thirdWidget);
```

### 如果我需要为每个小部件设置不同的默认值怎么办？

`Value` 属性适用于整个字段，而不是单个小部件。如果需要不同的默认值，您必须创建独立的字段，而不是使用 `MultipleWidgets`。

### 这是否适用于 PDF/A 或 PDF/UA 合规性？

是的，但在添加表单字段后，您可能需要设置额外的文档属性（例如 `pdfDocument.ConvertToPdfA()`）。小部件的关联保持不变。

## 完整工作示例（可复制粘贴）

下面是完整的、可直接运行的程序。只需将其放入控制台项目，引用 Aspose.Pdf NuGet 包，然后按 **F5**。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

namespace AsposePdfMultiWidget
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create a new PDF document
            using (var pdfDocument = new Document())
            {
                // Add a blank page pdf
                var pdfPage = pdfDocument.Pages.Add();

                // Create a TextBox field that can contain multiple widgets
                var multiWidgetTextBox = new TextBoxField(
                    pdfPage,
                    new Rectangle(50, 700, 250, 730));
                multiWidgetTextBox.MultipleWidgets = true;   // enable multiple widgets
                multiWidgetTextBox.Value = "First widget";

                // Add the TextBox field to the form (first widget)
                pdfDocument.Form.Add(multiWidgetTextBox, "MultiTB", 1);

                // Create and attach a second widget programmatically
                var secondWidget = new WidgetAnnotation(
                    new Rectangle(300, 700, 500, 730));
                multiWidgetTextBox.Widgets.Add(secondWidget);

                // Save the PDF with both widgets
                pdfDocument.Save("multiWidget.pdf");
            }
        }
    }
}
```

运行程序并打开 `multiWidget.pdf`。您会看到两个同步的文本框——正是您在询问 **how to create pdf form**（如何创建 pdf 表单）并希望拥有多个条目时想要的效果。

## 回顾与后续步骤

我们刚刚演示了如何 **create pdf document**、添加 **blank page pdf**、定义 **create pdf form field**，以及最终回答 **how to add textbox pdf** 小部件共享数据的方法。核心思想是单个字段名可以渲染多次，从而在无需额外编码的情况下提供灵活的表单布局。

想进一步探索？试试以下想法：

- **Style the textbox** – 使用 `TextBoxField` 属性更改边框颜色、背景或字体。  
- **Add validation** – 使用 JavaScript 动作（`TextBoxField.Actions.OnValidate`）来强制格式。  
- **Combine with other fields** – 添加复选框、单选按钮或数字签名，以构建完整功能的表单。  
- **Export form data** – 调用 `pdfDocument.Form.ExportFields()` 将用户输入导出为 JSON 或 XML。

上述每项都基于我们已覆盖的相同基础，因此您已具备创建用于发票、合同、调查或任何其他业务需求的高级 PDF 表单的能力。

---

*祝编码愉快！如果遇到任何问题，请在下方留言或查阅 Aspose.Pdf 文档以深入了解。记住，掌握 PDF 生成的最佳方式是多加实验——调整坐标、添加更多小部件，观看您的表单活起来。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}