---
category: general
date: 2026-07-20
description: 使用 Aspose.Pdf 在 C# 中创建 PDF 文档：在 PDF 中定位文本并添加结构树以实现可访问性。请遵循本分步指南。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document c#
- position text in pdf
- add structural tree
- Aspose.Pdf tagging
- PDF/A‑2b generation
language: zh
lastmod: 2026-07-20
og_description: 使用 C# 即时创建 PDF 文档。了解如何在 PDF 中定位文本并使用 Aspose.Pdf 添加结构树，以实现 PDF/A‑2b
  合规。
og_image_alt: Screenshot showing positioned text inside a PDF generated with Aspose.Pdf
  in C#
og_title: 使用 C# 创建 PDF 文档 – 文本定位与标签结构完整指南
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: 'Create PDF document C# with Aspose.Pdf: position text in PDF and add
    structural tree for accessibility. Follow this step‑by‑step guide.'
  headline: Create PDF Document C# – Position Text and Add Structural Tree
  type: TechArticle
- description: 'Create PDF document C# with Aspose.Pdf: position text in PDF and add
    structural tree for accessibility. Follow this step‑by‑step guide.'
  name: Create PDF Document C# – Position Text and Add Structural Tree
  steps:
  - name: Can I use other units (mm, cm) for positioning?
    text: Aspose.Pdf works natively with points. If you prefer millimeters, convert
      using `1 mm ≈ 2.83465 pt`. For example, `Position(25.4, 254)` places the paragraph
      1 cm from the left and 9 cm from the bottom.
  - name: What if I need to add multiple tags (headings, tables)?
    text: Simply create additional `StructureElement` objects with tags like `"H1"`
      for headings or `"Table"` for tables, and add the corresponding content as kids.
      Nesting works the same way—children inherit the parent’s logical order.
  - name: Does this approach work for PDF/A‑1b or PDF/A‑3b?
    text: Yes. Replace `SaveFormat.PdfA2b` with `SaveFormat.PdfA1b` or `SaveFormat.PdfA3b`.
      Keep in mind that each PDF/A version has its own set of required metadata; Aspose.Pdf
      will prompt you if something is missing.
  type: HowTo
tags:
- C#
- PDF
- Aspose.Pdf
title: 创建 PDF 文档 C# – 定位文本并添加结构树
url: /zh/net/programming-with-tagged-pdf/create-pdf-document-c-position-text-and-add-structural-tree/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建 PDF 文档 C# – 定位文本并添加结构树

是否曾需要 **create PDF document C#**，不仅能够将文本精确放置在指定位置，还能嵌入适当的结构树以实现可访问性？你并不是唯一有此需求的人——开发发票、报告或电子书的开发者经常会碰到这种情况。在本教程中，我们将通过一个完整、可直接运行的示例，使用强大的 Aspose.Pdf 库来实现上述功能。

我们将介绍如何 **position text in PDF**，通过 **add structural tree** 步骤附加语义标签，最后将文件保存为符合 PDF/A‑2b 标准的文档。完成后，你将拥有一个可在任何 .NET 项目中直接使用的可复用代码片段。

---

## 您需要的条件

- **.NET 6.0** 或更高（代码同样适用于 .NET Framework 4.6+）  
- **Aspose.Pdf for .NET** NuGet 包 (`Install-Package Aspose.Pdf`)  
- 基本的 C# 开发环境（Visual Studio、Rider 或 VS Code）  

无需额外的第三方工具；该库已涵盖从页面布局到 PDF/A 合规性的所有工作。

---

## 步骤 1：初始化 PDF 文档（Create PDF Document C#）

首先我们创建一个全新的 `Document` 对象。可以把它看作一块干净的画布——目前上面什么都没有，但已经准备好接受页面、文本以及结构化元数据。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Struct;

// Create a new PDF document – this is the core of our create pdf document c# workflow
Document pdfDoc = new Document();

// Add a blank page to the document; the page will host our positioned text
Page pdfPage = pdfDoc.Pages.Add();
```

> **为什么这很重要：** `Document` 类是所有 Aspose.Pdf 操作的入口。提前添加页面可以为后续附加可视内容和结构树提供载体。

---

## 步骤 2：定义段落并定位它（Position Text in PDF）

接下来创建一个 `Paragraph` 对象，并告诉 Aspose 它在页面上的具体位置。PDF 坐标使用点（1 英寸 = 72 pt）为单位，因此我们使用 `Position(72, 720)` 将段落放置在距左边缘 1 英寸、距底部 10 英寸的位置。

```csharp
// Define a paragraph positioned 1 inch from the left and 10 inches from the bottom
Paragraph positionedParagraph = new Paragraph
{
    // Position(x, y) – X is horizontal, Y is vertical from the bottom-left corner
    Position = new Position(72, 720) // 72 pt = 1 inch, 720 pt = 10 inch
};

// Add the actual text we want to display
positionedParagraph.Segments.Add(
    new TextFragment("Tagged paragraph at a specific location.")
);
```

> **小技巧：** 若需定位多行文本，可为后续段落调整 `Y` 坐标，或使用 `TextBuilder` 实现更精细的控制。

---

## 步骤 3：创建结构元素（Add Structural Tree）

面向可访问性的 PDF 依赖于描述内容逻辑顺序的 *结构树*。这里我们创建一个标签为 `"P"`（段落）的 `StructureElement`，并将已定位的段落作为其子节点。

```csharp
// Create a structural element (tag) for the paragraph – this is the add structural tree step
StructureElement structElement = new StructureElement("P");

// Attach the paragraph as a child of the structural element
structElement.AddKid(positionedParagraph);
```

> **为什么要添加结构树：** 屏幕阅读器和其他辅助技术会利用这些标签来导航文档。若缺少这些标签，PDF 虽然在视觉上完美，却无法被辅助技术读取。

---

## 步骤 4：将结构元素挂载到页面

每个页面都有自己的结构元素集合。将我们的 `structElement` 添加到 `pdfPage.StructElements`，即可将逻辑层级与可视布局关联起来。

```csharp
// Attach the structural element to the page's structure tree
pdfPage.StructElements.Add(structElement);
```

> **常见错误：** 忘记此步骤会导致标签仅存在于内存中，却未关联到任何页面，从而使可访问性信息对阅读器不可见。

---

## 步骤 5：保存为 PDF/A‑2b（确保长期保存）

PDF/A‑2b 是专为归档设计的 PDF 子集。Aspose.Pdf 只需一次调用即可生成该格式。将 `"YOUR_DIRECTORY"` 替换为你机器上的实际路径。

```csharp
// Save the document as a PDF/A‑2b file – ideal for long‑term storage and compliance
pdfDoc.Save("YOUR_DIRECTORY/TaggedWithPosition.pdf", SaveFormat.PdfA2b);
```

> **结果：** 现在你拥有一个文本精确定位、且包含完整结构树以供辅助工具使用的 PDF。

---

## 完整工作示例

下面是可以直接复制到控制台应用程序中的完整程序。添加 Aspose.Pdf NuGet 引用后即可编译运行。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Struct;

namespace PdfPositioningDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Initialize the document
            Document pdfDoc = new Document();
            Page pdfPage = pdfDoc.Pages.Add();

            // Step 2: Define and position the paragraph
            Paragraph positionedParagraph = new Paragraph
            {
                Position = new Position(72, 720) // 1 inch left, 10 inches up
            };
            positionedParagraph.Segments.Add(
                new TextFragment("Tagged paragraph at a specific location.")
            );

            // Step 3: Create the structural element (tag)
            StructureElement structElement = new StructureElement("P");
            structElement.AddKid(positionedParagraph);

            // Step 4: Attach the structural element to the page
            pdfPage.StructElements.Add(structElement);

            // Step 5: Save as PDF/A‑2b
            string outputPath = @"C:\Temp\TaggedWithPosition.pdf";
            pdfDoc.Save(outputPath, SaveFormat.PdfA2b);

            Console.WriteLine($"PDF created successfully at: {outputPath}");
        }
    }
}
```

**预期输出：** 运行后，打开 `TaggedWithPosition.pdf`。你会看到句子 “Tagged paragraph at a specific location.” 位于第一页的右下角附近。若检查 PDF 的标签（例如使用 Adobe Acrobat 的 “Tags” 面板），会发现一个 `<P>` 元素链接到该段落。

---

![使用 Aspose.Pdf 生成的 PDF 中定位文本的截图](/images/pdf-positioned.png){: .align-center }

*图片替代文字:* **create pdf document c#** – 展示在使用 Aspose.Pdf 生成的 PDF 中定位文本的截图。

---

## 常见问题与边缘情况

### 我可以使用其他单位（mm、cm）来定位吗？

Aspose.Pdf 原生使用点作为单位。如果你更喜欢使用毫米，可使用 `1 mm ≈ 2.83465 pt` 进行换算。例如，`Position(25.4, 254)` 将段落放置在距左边缘 1 cm、距底部 9 cm 的位置。

### 如果需要添加多个标签（标题、表格）怎么办？

只需创建额外的 `StructureElement`，使用 `"H1"` 表示标题、`"Table"` 表示表格等标签，并将相应内容作为子节点加入。嵌套方式相同——子元素会继承父元素的逻辑顺序。

### 这种方法适用于 PDF/A‑1b 或 PDF/A‑3b 吗？

可以。将 `SaveFormat.PdfA2b` 替换为 `SaveFormat.PdfA1b` 或 `SaveFormat.PdfA3b` 即可。请注意，每个 PDF/A 版本都有其必需的元数据，Aspose.Pdf 会在缺失时提示你补全。

---

## 小结

我们已经演示了一个 **create pdf document c#** 场景，包含以下步骤：

1. 使用 Aspose.Pdf 实例化新的 PDF。  
2. 通过设置精确坐标 **position text in PDF**。  
3. 为可访问性 **add structural tree** 元素。  
4. 将结果保存为符合标准的 PDF/A‑2b 文件。

所有步骤都是独立完整的，你可以根据需要将代码片段扩展到更复杂的布局、多页文档或不同的标签类型。

---

## 接下来可以做什么？

- **文本样式** – 探索 `TextState` 以更改字体、颜色和大小。  
- **嵌入图像** – 使用 `ImageFragment` 并将其与段落一起定位。  
- **生成表格** – 创建 `Table` 对象并使用 `"Table"` 标签进行语义化。  
- **自动化流水线** – 将此代码集成到后台服务，实现夜间批量生成发票。

欢迎随意实验，并告诉我们哪些变体最有价值。祝编码愉快！

## 您接下来应该学习什么？

以下教程与本指南所示技术密切相关，帮助你进一步掌握 API 功能并探索在项目中的其他实现方式。每篇资源均提供完整可运行的代码示例和逐步解释。

- [使用 Aspose.PDF for .NET 创建带标签的 PDF：提升可访问性和文档结构的完整指南](/pdf/english/net/advanced-features/create-tagged-pdfs-aspose-pdf-net/)
- [使用 Aspose.PDF 创建 PDF 文档 – 步骤指南](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [使用 Aspose.PDF .NET 创建和旋转 PDF 文本：开发者的综合指南](/pdf/english/net/text-operations/create-rotate-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}