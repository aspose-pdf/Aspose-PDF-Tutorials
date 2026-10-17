---
category: general
date: 2026-04-12
description: 使用 C# 快速向 Word 添加图形。学习如何在 Word 中定位图形、将图形插入 docx，以及添加自定义 XML 以实现高级布局。
draft: false
keywords:
- add figure to word
- position figure in word
- insert figure into docx
- how to add custom xml
- how to position shape word
language: zh
og_description: 使用 C# 快速向 Word 添加图形。学习如何在 Word 中定位图形、将图形插入 docx，以及添加自定义 XML 以实现高级布局。
og_title: 向 Word 添加图形 – 完整的 C# 编程指南
tags:
- C#
- Word Automation
- Document Generation
title: 向 Word 添加图形 – 完整的 C# 编程指南
url: /zh/net/programming-with-images/add-figure-to-word-complete-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将图形添加到 Word – 完整的 C# 编程指南

是否曾经想要 **add figure to Word**，却不知从何入手？你并不孤单。在许多办公自动化项目中，缺失的往往是一张放置得当的图片或图表，它位于自定义 XML 部分内部。本文将手把手教你如何 **position figure in Word**，将图形插入 *.docx* 文件，并且微调底层的自定义 XML，使该形状的行为与原生 Word 对象无异。

我们将使用 GemBox.Document 库（小文件免费，大文件需商业授权）演示一个真实案例。完成后，你将拥有一个自包含、可直接运行的程序，它会在标记内容容器内部的坐标 X = 50、Y = 200 处放置图形。没有模糊的 “见文档” 说明——只有清晰的代码、工作原理以及可直接复制到自己项目中的技巧。

## 前置条件

- .NET 6.0 或更高（代码同样可以在 .NET Core 3.1 上编译）
- **GemBox.Document** NuGet 包（`Install-Package GemBox.Document`）
- 一个起始的 Word 文件（`input.docx`），其中已经包含了你希望放置图形的自定义 XML 标记
- 基础的 C# 知识（你将看到每行代码的意义）

> **Pro tip:** 如果没有预先标记的文档，可以在 Word 中插入 *Content Control* → *XML Mapping Pane* → 映射自定义 XML 部分。库会将该控件视为 `TaggedContent`。

## 第一步 – 加载源文档

首先打开已有的 *.docx* 文件。`Document` 是所有 GemBox 操作的入口。

```csharp
using GemBox.Document;
using System.Drawing;

// Set the license key (free version uses a limited license key)
ComponentInfo.SetLicense("FREE-LIMITED-KEY");

// Step 1: Load the source document
Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
```

*为什么要这样做？* 加载文件后我们才能访问其内部部件，包括任何自定义 XML 容器。若不加载，就无法定位将承载图形的 `TaggedContent` 节点。

## 第二步 – 访问标记内容（自定义 XML 容器）

自定义 XML 存放在 Word 的 *content control* 中。GemBox 将其暴露为 `TaggedContent`。

```csharp
// Step 2: Access the document's tagged content (the container for custom XML)
TaggedContent taggedContent = doc.TaggedContent;
```

如果文档中有多个标记段落，`TaggedContent` 会返回 **第一个**。你也可以遍历 `doc.TaggedContents`，按名称选择特定的标记。

## 第三步 – 创建图形元素

`FigureElement` 代表图片、图表或任何 Word 视作 *shape* 的可视对象。我们将在标记容器内部创建它。

```csharp
// Step 3: Create a new figure element that will be placed inside the tagged content
FigureElement figure = taggedContent.CreateFigureElement();
```

*为什么在这里创建图形？* 将其附加到自定义 XML 节点后，Word 会把该图形视为该逻辑段落的一部分，这对后续编辑或基于内容控件的工作流至关重要。

## 第四步 – 精确定位图形

Word 使用点（1 pt ≈ 1/72 in）进行定位。`PointF` 结构让我们可以轻松设置 X/Y 坐标。

```csharp
// Step 4: Position the figure at the desired coordinates (X = 50, Y = 200)
figure.Position = new PointF(50, 200);
```

> **How to position shape word:** `Position` 属性接受一个 `PointF`，第一个值为水平偏移（左），第二个值为垂直偏移（上），相对于页面边距。根据需要调整这些数值以微调位置。

## 第五步 – 将图形插入标记内容树

现在把图形附加到自定义 XML 树的根元素上。这会将形状实际加入 Word 文档。

```csharp
// Step 5: Insert the figure into the root element of the tagged content tree
taggedContent.RootElement.AppendChild(figure);
```

此时图形已经位于文档内部，但尚未设置图像来源。下面我们从磁盘添加一张简单的 PNG。

```csharp
// Optional: Load an image and assign it to the figure
using (var imageStream = System.IO.File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
{
    figure.Image = new Image(imageStream);
}
```

## 第六步 – 保存修改后的文档

最后，将更改写入一个新的 *.docx* 文件。

```csharp
// Step 6: Save the updated document
doc.Save(@"YOUR_DIRECTORY\output.docx");
```

打开 `output.docx` 时，你会看到图片正好位于自定义 XML 块内部的 (50, 200) 坐标处。

### 完整可运行示例

```csharp
using GemBox.Document;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // License (free version)
        ComponentInfo.SetLicense("FREE-LIMITED-KEY");

        // Load the source DOCX
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // Access the first tagged content container
        TaggedContent taggedContent = doc.TaggedContent;

        // Create a new figure element
        FigureElement figure = taggedContent.CreateFigureElement();

        // Position the figure (X = 50 pt, Y = 200 pt)
        figure.Position = new PointF(50, 200);

        // Load an image file and assign it
        using (FileStream fs = File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
        {
            figure.Image = new Image(fs);
        }

        // Append the figure to the custom XML root
        taggedContent.RootElement.AppendChild(figure);

        // Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

**预期结果：** 打开 `output.docx`，PNG 将出现在你指定的位置，且嵌套在自定义 XML 部分中。若检查文档的 XML（`.docx` → 解压 → `word/document.xml`），会看到带有正确 `<v:shape>` 坐标的 `<w:pict>` 元素。

## 常见问题与边缘情况

### 文档中有多个标记段落怎么办？

使用 `doc.TaggedContents` 进行枚举，并按标记名称选择：

```csharp
TaggedContent myTag = doc.TaggedContents.First(tc => tc.TagName == "MyCustomTag");
```

### 如何为图形添加标题？

```csharp
figure.Caption = new CaptionElement("Figure 1 – Sample Diagram");
```

### 这在 Word 2010 及以后版本都可用吗？

可以。GemBox.Document 基于 Open XML 标准，兼容 Word 2007 +（包括 2010、2013、2016、2019 以及 Microsoft 365）。

### 如果需要旋转形状怎么办？

```csharp
figure.Rotation = 45; // degrees
```

### 如何添加矢量图而非光栅图像？

```csharp
figure.Image = new Image(@"YOUR_DIRECTORY\vector.svg");
```

## 专业技巧与常见坑点

- **文件路径：** 使用 `Path.Combine` 避免硬编码分隔符，特别是在非 Windows 平台上。
- **授权限制：** 免费版 GemBox 限制文档大小为 20 KB。若处理更大文件，请购买商业密钥。
- **性能：** 对批量处理复用同一个 `Document` 实例，可显著降低内存开销。
- **形状溢出：** 若图形尺寸超出页面边距，Word 会裁剪它。请相应调整 `figure.Width` 与 `figure.Height`。

## 结论

现在你已经掌握了 **how to add figure to Word**、精准 **position figure in Word**，以及如何操作底层自定义 XML 使形状行为如同原生元素。完整的可运行示例展示了从加载文档、创建 `FigureElement`、设置坐标、附加图像到最终保存 *.docx* 的每一步。

接下来，尝试通过循环添加多个图形、动态生成图表，或使用 **insert figure into docx** 的方式进一步实验。你也可以探索 **how to add custom xml** 以实现更丰富的内容控件，或学习 **how to position shape word** 在表格和页眉中的技巧。可能性无限，有了本指南的基础，你已经可以像专业人士一样自动化 Word 文档。

祝编码愉快，若遇到任何问题，欢迎留言交流！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}