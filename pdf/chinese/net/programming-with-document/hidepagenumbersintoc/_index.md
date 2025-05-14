---
"description": "了解如何使用 Aspose.Pdf for .NET 在目录中隐藏页码。遵循本指南和代码示例，创建专业的 PDF 文件。"
"linktitle": "隐藏目录中的页码"
"second_title": "Aspose.PDF for .NET API参考"
"title": "隐藏目录中的页码"
"url": "/zh/net/programming-with-document/hidepagenumbersintoc/"
"weight": 220
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 隐藏目录中的页码

## 介绍

处理 PDF 时，有时您可能希望生成目录 (TOC)，但为了保持文档的简洁，可以隐藏页码。或许是因为没有页码文档会更流畅，又或许是出于美观考虑。无论您出于何种原因，如果您使用 Aspose.PDF for .NET，本教程将向您展示如何在目录中隐藏页码。

## 先决条件

在我们开始之前，您需要准备一些东西。以下是一份快速清单：

- 已安装 Visual Studio：您需要一个可运行的 Visual Studio 版本来编写代码。
- Aspose.PDF for .NET 库：确保您已经安装了 Aspose.PDF for .NET 库。
  - 下载链接： [Aspose.PDF for .NET](https://releases.aspose.com/pdf/net/)
- 临时许可证：如果您正在测试这些功能，那么拥有临时许可证会很有帮助。
  - 临时执照： [在这里获取](https://purchase.aspose.com/temporary-license/)

## 导入包

在开始编写代码之前，请确保在 C# 项目中导入以下命名空间。这些命名空间将提供处理 PDF 文档和创建目录 (TOC) 所需的类和方法。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

现在您的环境已准备就绪，软件包也已导入，让我们来分解一下整个过程。我们将涵盖代码的每个部分，以确保清晰易懂，让您轻松跟进。

## 步骤 1：初始化您的 PDF 文档

我们需要做的第一件事是创建一个新的 PDF 文档并添加一个目录 (TOC) 页面。


```csharp
// 文档目录的路径。
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "HiddenPageNumbers_out.pdf";
Document doc = new Document();
Page tocPage = doc.Pages.Add();
```

- dataDir：这是保存输出文件的目录。
- Document()：初始化一个新的PDF文档。
- Pages.Add()：向文档添加一个新的空白页，该页面稍后将保存您的目录。

## 第 2 步：设置目录信息和标题

接下来，我们将定义目录信息，包括设置将显示在目录顶部的标题。

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocPage.TocInfo = tocInfo;
```

- TocInfo：此对象保存有关 TOC 的所有信息。
- TextFragment：代表TOC标题的文本，这里我们将其设置为“Table Of Contents”。
- FontStyle：我们将 TOC 标题的大小设置为 20 并将其设为粗体，以设置其样式。
- tocPage.TocInfo：我们将目录信息分配给将显示目录的页面。

## 步骤 3：隐藏目录中的页码

现在到了最有趣的部分！在这里，我们配置目录以隐藏页码。

```csharp
tocInfo.IsShowPageNumbers = false;
tocInfo.FormatArrayLength = 4;
```

- IsShowPageNumbers：这是隐藏页码的神奇开关。将其设置为 `false`，并且页码不会出现在目录中。
- FormatArrayLength：我们将其设置为 4，表示我们要为四个级别的 TOC 标题定义格式。

## 步骤 4：自定义目录格式

为了给您的目录添加更多样式，我们现在将为不同级别的标题定义格式。

```csharp
tocInfo.FormatArray[0].Margin.Right = 0;
tocInfo.FormatArray[0].TextState.FontStyle = FontStyles.Bold | FontStyles.Italic;
tocInfo.FormatArray[1].Margin.Left = 30;
tocInfo.FormatArray[1].TextState.Underline = true;
tocInfo.FormatArray[1].TextState.FontSize = 10;
tocInfo.FormatArray[2].TextState.FontStyle = FontStyles.Bold;
tocInfo.FormatArray[3].TextState.FontStyle = FontStyles.Bold;
```

- FormatArray：此数组控制目录条目的格式。每个索引代表不同的标题级别。
- 边距和文本样式：我们为每个标题级别设置边距并应用粗体、斜体和下划线等字体样式。

## 步骤 5：向文档添加标题

最后，让我们添加将成为目录一部分的实际标题。

```csharp
Page page = doc.Pages.Add();
for (int Level = 1; Level != 5; Level++)
{ 
    Heading heading2 = new Heading(Level); 
    TextSegment segment2 = new TextSegment(); 
    heading2.TocPage = tocPage; 
    heading2.Segments.Add(segment2); 
    heading2.IsAutoSequence = true; 
    segment2.Text = "this is heading of level " + Level; 
    heading2.IsInList = true; 
    page.Paragraphs.Add(heading2); 
}
```

- 标题和文本段：这些代表目录中将出现的标题。每个级别都有自己的标题。
- IsAutoSequence：自动对标题进行编号。
- IsInList：确保每个标题都出现在目录中。

## 步骤6：保存文档

一切设置完成后，将 PDF 文档保存到指定的输出文件。

```csharp
doc.Save(outFile);
```

就这样！您已成功创建带有目录的 PDF，并且页码已隐藏！

## 结论

在 PDF 中创建目录并隐藏页码看似棘手，但使用 Aspose.PDF for .NET，一切变得轻而易举。通过本分步指南，您将学习如何自定义目录格式、隐藏页码以及为标题应用不同的样式。现在，您可以根据自己的具体需求创建专业的 PDF 文件。

## 常见问题解答

### 我可以显示目录中特定标题的页码吗？
不可以，Aspose.PDF 会隐藏或显示整个目录的页码。您无法选择性地隐藏特定条目的页码。

### 是否可以向 TOC 添加更多级别？
是的，你可以增加 `FormatArrayLength` 定义更多级别的目录标题。

### 如何更改所有目录条目的字体？
您可以通过修改 `TextState.Font` 每个级别的属性 `FormatArray`。

### 我可以在目录中插入超链接吗？
是的，您可以使用 `Heading.TocPage` 财产。

### 我需要 Aspose.PDF 的许可证吗？
是的，生产使用需要有效的许可证。您可以申请临时许可证 [这里](https://purchase.aspose.com/temporary-license/) 测试功能。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}