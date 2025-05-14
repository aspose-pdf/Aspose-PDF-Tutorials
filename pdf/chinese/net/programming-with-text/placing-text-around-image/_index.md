---
"description": "了解如何使用 Aspose.PDF for .NET 在 PDF 中的图像周围放置文本。按照我们的分步指南，创建图像和文本并排的专业 PDF。"
"linktitle": "在 PDF 文件中的图像周围放置文本"
"second_title": "Aspose.PDF for .NET API参考"
"title": "在 PDF 文件中的图像周围放置文本"
"url": "/zh/net/programming-with-text/placing-text-around-image/"
"weight": 260
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 文件中的图像周围放置文本

## 介绍

您是否曾尝试在 PDF 文件中的图像周围放置文本，但却发现这很棘手？如果是这样，那么您来对地方了！Aspose.PDF for .NET 简化了这一过程，只需几行代码即可将文本放置在图像旁边。无论您是创建报告、文档还是演示文稿，此功能都是增强内容布局并使其更具视觉吸引力的绝佳方法。今天，我们将介绍如何使用 Aspose.PDF for .NET 在 PDF 文档的图像周围放置文本。

## 先决条件

在开始编写代码之前，我们先确保所有设置都已完成。以下是您需要准备的材料：

- Aspose.PDF for .NET：您可以从 [这里](https://releases。aspose.com/pdf/net/).
- Visual Studio：确保您已安装最新版本，以便顺利进行。
- .NET Framework：此示例使用 .NET，因此请确保您的环境已设置为适合 .NET 开发。
- 临时驾照：您可以申请临时驾照 [这里](https://purchase.aspose.com/temporary-license/) 如果您正在评估该产品。

如果您尚未设置 Aspose.PDF for .NET，请按照 [文档](https://reference。aspose.com/pdf/net/).

## 导入命名空间

在开始编码之前，我们需要导入必要的命名空间。以下是执行此操作的代码片段：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

这些命名空间至关重要，因为它们提供了对以下类的访问： `Document`， `Page`， `Image`， 和 `HtmlFragment`，我们将使用它来创建和操作 PDF。

现在我们已经做好了准备，让我们来详细了解一下如何使用 Aspose.PDF for .NET 在 PDF 文件中的图像周围放置文本。我们将逐步指导您完成整个过程。

## 步骤 1：实例化文档对象

首先，您需要创建一个 PDF 文档。在 Aspose.PDF 中，这可以通过实例化一个 `Document` 对象。此对象将作为我们添加的所有内容的基础。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

到这里，我们创建了一个空的 PDF 文档。它目前还没有任何页面，不过不用担心，我们会在下一步中添加页面。

## 步骤 2：向文档添加页面

现在我们已经有了文档，是时候添加页面了。你可以把这想象成创建一张白纸，然后在上面添加内容。

```csharp
Aspose.Pdf.Page page = doc.Pages.Add();
```

这段代码向文档添加了一个新页面。默认情况下，该页面是空白的，但我们即将更改这种情况。

## 步骤 3：创建表格来组织内容

为了使图片和文字保持对齐，我们将使用表格。PDF 中的表格可以帮助您构建布局，就像在 Word 文档或 HTML 中一样。

```csharp
Aspose.Pdf.Table table1 = new Aspose.Pdf.Table();
page.Paragraphs.Add(table1);
```

此代码片段会创建一个表格并将其添加到页面。您可以将表格视为对齐图片和文本的框架。

## 步骤 4：设置表格的列宽

现在我们已经添加了一个表格，我们需要定义列的宽度。这可以确保图片和文本在页面上的大小合适。

```csharp
table1.ColumnWidths = "120 270";
```

此行设置两列的宽度——一列用于图片，一列用于文本。如果您的图片或文本需要更多或更少的空间，请调整这些值。

## 步骤 5：定义边距和填充

为了确保一切看起来整洁，让我们给表格添加一些边距和填充。

```csharp
Aspose.Pdf.MarginInfo margin = new Aspose.Pdf.MarginInfo();
margin.Top = 5f;
margin.Left = 5f;
margin.Right = 5f;
margin.Bottom = 5f;
table1.DefaultCellPadding = margin;
```

这些设置可确保您的表格具有一致的间距，使内容具有视觉吸引力。

## 步骤 6：将图像插入表格

现在，让我们进入最有趣的部分——添加图片。在本例中，我们将添加 Aspose 的 logo，但您也可以使用任何您喜欢的图片。

```csharp
Aspose.Pdf.Row row1 = table1.Rows.Add();
Aspose.Pdf.Image logo = new Aspose.Pdf.Image();
logo.File = dataDir + "aspose-logo.jpg";
logo.FixHeight = 120;
logo.FixWidth = 110;
row1.Cells.Add();
row1.Cells[0].Paragraphs.Add(logo);
```

以下是正在发生的事情：
- 我们从您指定的目录加载图像。
- 我们设置图像的高度和宽度。
- 最后，我们将图像添加到表格中的第一个单元格。

## 步骤 7：在图像旁边添加文本

现在图片已经就位，让我们在旁边添加一些文字。在本例中，我们将使用 HTML 格式的文本来设置内容的样式。

```csharp
string TitleString = "<font face=\"Arial\" size=6 color=\"#101090\"><b> Aspose.Pdf for .NET</b></font>";
string BodyString1 = "<font face=\"Arial\" size=2><br/>Aspose.Pdf for .NET is a non-graphical PDF document reporting component that enables .NET applications to <b>create PDF documents from scratch</b> without utilizing Adobe Acrobat.</font>";

Aspose.Pdf.HtmlFragment TitleText = new Aspose.Pdf.HtmlFragment(TitleString + BodyString1);
row1.Cells.Add();
row1.Cells[1].Paragraphs.Add(TitleText);
```

此区块在图片旁边的单元格中添加了样式化的标题和描述。您可以使用 HTML 标签设置文本格式，以实现更多自定义。

## 步骤 8：调整垂直对齐

默认情况下，表格单元格中的内容可能无法按您想要的方式对齐。在这种情况下，我们需要确保文本与单元格顶部对齐。

```csharp
row1.Cells[1].VerticalAlignment = Aspose.Pdf.VerticalAlignment.Top;
```

这确保文本位于单元格的顶部，保持布局整洁和专业。

## 步骤9：在图片和描述下方添加更多文本

您可能希望在图片和文本下方添加更多内容。为此，我们在表格中添加另一行。

```csharp
Aspose.Pdf.Row SecondRow = table1.Rows.Add();
SecondRow.Cells.Add();
SecondRow.Cells[0].ColSpan = 2;
SecondRow.Cells[0].VerticalAlignment = Aspose.Pdf.VerticalAlignment.Top;

string SecondRowString = "<font face=\"Arial\" size=2>Aspose.Pdf for .NET supports the creation of PDF files through API and XML or XSL-FO templates.</font>";
Aspose.Pdf.HtmlFragment SecondRowText = new Aspose.Pdf.HtmlFragment(SecondRowString);
SecondRow.Cells[0].Paragraphs.Add(SecondRowText);
```

在这里，我们添加了另一行附加文本，跨越两列以保持布局平衡。

## 步骤 10：保存 PDF 文档

最后，我们需要保存文档，以便您可以查看更改。

```csharp
doc.Save(dataDir + "PlacingTextAroundImage_out.pdf");
```

这将保存 PDF，其中图像和文本的格式正如我们想要的那样。

## 结论

在 PDF 中将文本放置在图像周围似乎是一项艰巨的任务，但 Aspose.PDF for .NET 简化了这一过程。通过利用表格、图像和样式文本，您可以轻松创建具有专业外观的 PDF。只需几行代码，您就可以将内容精确地放置在所需的位置，使您的文档看起来更加美观且井井有条。

## 常见问题解答

### 我可以使用此方法放置多张带有文字的图像吗？
是的，只需在表中添加更多行和单元格即可包含更多图像和文本。

### 我可以改变图像的对齐方式吗？
当然！您可以通过调整单元格的对齐属性来修改图像对齐方式。

### 我如何进一步设计文本样式？
您可以在 `HtmlFragment` 对象应用各种样式，如粗体、斜体或不同的字体。

### 我可以控制文本和图像之间的间距吗？
是的，使用 `MarginInfo` 对象允许您控制元素之间的填充和边距。

### 可以添加文本链接吗？
当然！您可以使用 `<a>` 标签。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}