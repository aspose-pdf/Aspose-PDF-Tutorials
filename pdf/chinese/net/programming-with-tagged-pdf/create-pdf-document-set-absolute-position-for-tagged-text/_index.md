---
category: general
date: 2026-03-24
description: 创建 PDF 文档并学习如何为标记文本设置绝对位置。本教程展示如何添加 span 元素、如何添加标记内容以及如何在页面上定位文本。
draft: false
keywords:
- create pdf document
- set absolute position
- add span element
- how to add tagged
- position text on page
language: zh
og_description: 创建 PDF 文档，立即了解如何设置绝对位置、添加 span 元素以及在页面上使用标记 PDF 内容定位文本。
og_title: 创建 PDF 文档 – 标记文本的绝对定位
tags:
- Aspose.Pdf
- C#
- PDF Tagging
title: 创建 PDF 文档 – 为标记文本设置绝对位置
url: /zh/net/programming-with-tagged-pdf/create-pdf-document-set-absolute-position-for-tagged-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建 PDF 文档 – 为标记文本设置绝对位置

是否曾需要**创建 pdf 文档**，其中包含可访问的、标记的文本，并且能够精确定位到您想要的位置？也许您正在构建类似表单的 PDF，需要标签位于精确坐标，或者您正在生成证书，需要姓名与背景图像完美对齐。  

在本指南中，我们将逐步演示一个完整且可运行的示例，展示**如何添加标记**内容、**设置绝对位置**以及**添加 span 元素**，从而让您**在页面上定位文本**而无需猜测。没有外部引用——只提供可复制粘贴的代码，并解释每行代码背后的“原因”。

## 前提条件

- .NET 6+（或 .NET Framework 4.6+）以及 C# 编译器  
- Aspose.Pdf for .NET（撰写时的最新版本 23.12），通过 NuGet 安装  
- 对 C# 语法有基本了解  

如果您已经具备上述条件，让我们开始吧。

---

## 创建 PDF 文档 – 设置绝对位置

我们首先实例化一个空的 `Document`。该对象代表整个 PDF 文件，并让我们能够访问标记内容树。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();
```

**Why this matters:**  
`Document` 是 PDF 结构的根节点。首先创建它可以确保有一个画布用于视觉元素（页面、图形）和逻辑结构（标签）。`using` 语句保证文件被正确释放，防止 Windows 上出现文件句柄泄漏。

## 启用标记内容（如何添加标记）

在插入任何标记元素之前，文档必须被标记为 *tagged*。Aspose.Pdf 会自动创建 `TaggedContent` 对象，但仍需将该标志打开。

```csharp
// Step 2: Mark the document as tagged (required for accessibility)
pdfDocument.TaggedContent = true;
```

**What happens under the hood?**  
将 `TaggedContent` 设置为 `true` 告诉 PDF 阅读器文件包含逻辑结构树。这对屏幕阅读器以及 `SetPosition` 方法在 span 元素上正常工作至关重要。

## 获取标记内容树的根元素

根元素是所有结构标签（如 `<Document>`、`<Section>`、`<Span>`）的入口点。可以把它看作 PDF 的不可见“body”。

```csharp
// Step 3: Retrieve the root element of the tag tree
var rootElement = pdfDocument.TaggedContent.RootElement;
```

**Why we need the root:**  
所有后续标签必须附加到树的某个位置；否则它们不会出现在可访问性层次结构中。

## 添加 Span 元素 – 行内文本的构建块

*span* 是 PDF 中相当于 HTML `<span>` 的元素——非常适合需要精确定位的短文本。

```csharp
// Step 4: Create a span element that will hold the text
var spanElement = rootElement.CreateSpanElement();
```

**Design note:**  
如果需要更丰富的格式（粗体、斜体、超链接），可以将 span 包裹在 `<Paragraph>` 中或随后使用 `TextFragment` 对象。对于绝对定位，普通 span 是最轻量的选择。

## 设置绝对位置 – X=100, Y=200

现在进入有趣的部分：将 span 放置在页面的精确位置。坐标系以左下角 (0,0) 为起点，使用点（1 pt ≈ 1/72 英寸）。

```csharp
// Step 5: Position the span at an absolute location (X=100, Y=200)
spanElement.SetPosition(100, 200);
```

**Why absolute positioning?**  
当您需要像素级精确布局——比如证书、发票或表单——相对流（如从左到右的文本）不足以满足需求。`SetPosition` 绕过普通文本流，将元素固定在您指定的位置。

## 向 Span 添加文本

在 span 定位后，我们现在注入实际的字符串。

```csharp
// Step 6: Add the desired text to the span
spanElement.AddText("Positioned tagged text");
```

**Tip:**  
如果需要 Unicode 字符或从右到左的脚本，只需传入字符串；Aspose.Pdf 会自动处理编码。

## 将 Span 附加到根元素

最后，我们将 span 附加到文档的逻辑树中，使其成为最终 PDF 的一部分。

```csharp
// Step 7: Append the span to the root so it becomes part of the PDF structure
rootElement.AppendChild(spanElement);
```

**What if you forget this step?**  
span 只会存在于内存中，却永远不会序列化到文件中，导致看不到文本且可访问性树不完整。

## 完整、可运行的示例

下面是完整的程序代码，可直接放入控制台应用。它创建一个单页 PDF，在 (100, 200) 处添加一个标记的 span，并将文件保存为 `TaggedPositioned.pdf`。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Enable tagging for accessibility
        pdfDocument.TaggedContent = true;

        // 3️⃣ Add a blank page (required for visual placement)
        var page = pdfDocument.Pages.Add();

        // 4️⃣ Get the root element of the tagged‑content tree
        var rootElement = pdfDocument.TaggedContent.RootElement;

        // 5️⃣ Create a span element that will hold the text
        var spanElement = rootElement.CreateSpanElement();

        // 6️⃣ Position the span at an absolute location on the page (X=100, Y=200)
        spanElement.SetPosition(100, 200);

        // 7️⃣ Add the desired text to the span
        spanElement.AddText("Positioned tagged text");

        // 8️⃣ Append the span to the root so it becomes part of the PDF structure
        rootElement.AppendChild(spanElement);

        // 9️⃣ Save the document
        pdfDocument.Save("TaggedPositioned.pdf");

        Console.WriteLine("PDF created successfully – check TaggedPositioned.pdf");
    }
}
```

**Expected output:**  
在任意查看器（Adobe Acrobat、Foxit 等）中打开 `TaggedPositioned.pdf`。您会看到短语 **“Positioned tagged text”** 正好位于距左边缘 100 pt、距底部 200 pt 的位置。如果检查 *Tags* 面板，会在文档根节点下列出一个 `<Span>` 元素，确认内容已正确标记。

## 常见问题与边缘情况

### 如果需要在除第一页之外的特定页面上定位文本怎么办？

在调用 `SetPosition` 之前，先获取所需的页面（`var page = pdfDocument.Pages[3];`）。span 将自动附加到活动页面的上下文中。

### 我可以使用英寸或厘米来设置位置吗？

`SetPosition` 接受点（points）作为单位。可使用以下公式进行转换：  
- **英寸 → 点：** `points = inches * 72`  
- **厘米 → 点：** `points = cm * 28.3465`

### 如何更改 span 的字体或颜色？

After creating the span, you can retrieve its `TextState` and modify it:

```csharp
var textState = spanElement.TextState;
textState.Font = FontRepository.FindFont("Arial");
textState.FontSize = 12;
textState.ForegroundColor = Color.GetBlack();
```

### 如果文档已经有现有标签怎么办？

仍然可以创建新的 span 并将其附加到任何现有元素（`rootElement`、特定的 `<Section>` 等）。只需确保保持逻辑层次结构——屏幕阅读器期望有结构良好的树。

### 这是否适用于 PDF/A 或 PDF/UA 合规性？

是的。标记的 PDF 是 PDF/UA 的核心要求。如果需要 PDF/A，可在构建内容后调用 `pdfDocument.Convert(new PdfAConversionOptions(PdfAStandard.PdfA_1b));`。

## 专业技巧与常见陷阱

- **专业提示：** 在定位内容之前务必先添加页面。没有页面时，`SetPosition` 会悄悄失败，因为没有可渲染的目标。  
- **注意单位：** 将 UI 设计中的像素与 PDF 点混用会导致文本位置错误。请仔细检查转换。  
- **性能提示：** 如果要生成成千上万的 PDF，建议复用同一个 `Document` 实例，并在每次运行后调用 `pdfDocument.Pages.Clear()`，以避免过度的内存分配。  
- **可访问性提醒：** 标记不仅是锦上添花；许多法规（Section 508、EN 301 549）都要求如此。使用 `CreateSpanElement` 可确保文本被辅助技术发现。

## 结论

我们已经从零**创建了 pdf 文档**，**设置了绝对位置**，**添加了 span 元素**，并演示了**如何添加标记**内容，使您能够以像素级精确度**在页面上定位文本**。完整示例已可直接运行，说明同时涵盖了*如何*以及*为什么*——正是开发者（以及 AI 助手）在寻找可靠解决方案时所需的。

接下来，您可以探索：

- 在定位文本后面添加图像，以实现带水印的证书。  
- 使用 `CreateParagraphElement` 创建仍需绝对定位的多行块。  
- 导出为 PDF/UA，以满足严格的可访问性审计。  

随意调整坐标、字体或颜色——实验是掌握标记 PDF 生成的最快方式。如果遇到问题，欢迎在下方留言；祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}