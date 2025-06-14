---
"description": "了解如何使用 Aspose.PDF for .NET 从 PDF 文档的所有页面中搜索和获取文本。"
"linktitle": "搜索并获取全部文本"
"second_title": "Aspose.PDF for .NET API参考"
"title": "搜索并获取全部文本"
"url": "/zh/net/programming-with-text/search-and-get-text-all/"
"weight": 420
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 搜索并获取全部文本

## 介绍

您是否曾经需要从 PDF 中提取特定文本，但却发现很难？PDF 有时会像上锁的容器一样，难以获取所需的信息。但好消息是：使用 Aspose.PDF for .NET，您可以轻松地从任何 PDF 中搜索和检索文本。这个强大的库提供了您在 .NET 应用程序中处理 PDF 所需的一切，让文本提取变得轻而易举。在本教程中，我们将引导您完成使用 Aspose.PDF for .NET 从 PDF 文件中搜索和提取文本的过程。无论您是要构建文本分析工具，还是只需要自动从 PDF 报告中提取数据，您都来对地方了！

## 先决条件

在我们进入代码之前，让我们确保您已设置好一切：

1. Aspose.PDF for .NET：您需要下载并安装 Aspose.PDF for .NET。您可以从下载页面获取 [这里](https://releases。aspose.com/pdf/net/).
2. .NET 环境：确保您的开发机器上已安装 .NET Framework 或 .NET Core。
3. 基本 C## 知识：建议熟悉 C# 并使用 .NET 项目。
4. PDF 文档：我们将从中提取文本的示例 PDF 文件。在本例中，我们将使用 `SearchAndGetTextFromAll。pdf`.

## 导入包

在编写任何代码之前，您需要将必要的命名空间导入到项目中以便使用 Aspose.PDF。

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

这些命名空间提供对 PDF 文档对象模型的访问，并允许我们操作文件中的文本。

我们将这个过程分解成简单的步骤，以便您可以轻松地遵循。

## 步骤1：设置文档目录

首先，您需要指定 PDF 所在目录的路径。这有助于应用程序找到您要从中提取文本的文件。

```csharp
// 文档目录的路径。
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

- 这 `dataDir` 变量应该指向你的 `SearchAndGetTextFromAll.pdf` 文件已存储。
- 代替 `"YOUR DOCUMENT DIRECTORY"` 使用您机器上的实际路径。

## 第 2 步：打开 PDF 文档

接下来，我们将使用 Aspose.PDF 的 `Document` 目的。

```csharp
// 打开文档
Document pdfDocument = new Document(dataDir + "SearchAndGetTextFromAll.pdf");
```

- 我们创建一个新的实例 `Document` 通过传递 PDF 的完整文件路径来类。
- 这会将 PDF 加载到内存中，使其准备好进行处理。

## 步骤3：创建文本吸收器

这 `TextFragmentAbsorber` 对象用于在 PDF 中搜索特定文本。在本例中，我们将查找单词“text”。

```csharp
// 创建 TextAbsorber 对象来查找输入搜索短语的所有实例
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("text");
```

- 这 `TextFragmentAbsorber` 使用字符串初始化 `"text"`。这意味着它将在 PDF 文档中查找任何出现的单词“text”。

## 步骤 4：接受所有页面的吸收器

现在，我们将指示 PDF 文档接受吸收器并在其所有页面上搜索文本。

```csharp
// 接受所有页面的吸收器
pdfDocument.Pages.Accept(textFragmentAbsorber);
```

- 这 `Accept` 方法应用于文档的页面。这将在所有页面中搜索指定的文本。

## 步骤5：提取文本片段

一旦吸收器扫描了文档，我们就可以检索提取的文本片段。

```csharp
// 获取提取的文本片段
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- 这 `TextFragments` 的财产 `TextFragmentAbsorber` 返回与搜索词匹配的所有文本片段的集合。

## 步骤 6：循环遍历文本片段

现在我们已经收集了文本片段，我们将循环遍历它们并提取详细信息。

```csharp
// 循环遍历片段
foreach (TextFragment textFragment in textFragmentCollection)
{
    Console.WriteLine("Text : {0} ", textFragment.Text);
    Console.WriteLine("Position : {0} ", textFragment.Position);
    Console.WriteLine("XIndent : {0} ", textFragment.Position.XIndent);
    Console.WriteLine("YIndent : {0} ", textFragment.Position.YIndent);
    Console.WriteLine("Font - Name : {0}", textFragment.TextState.Font.FontName);
    Console.WriteLine("Font - IsAccessible : {0} ", textFragment.TextState.Font.IsAccessible);
    Console.WriteLine("Font - IsEmbedded : {0} ", textFragment.TextState.Font.IsEmbedded);
    Console.WriteLine("Font - IsSubset : {0} ", textFragment.TextState.Font.IsSubset);
    Console.WriteLine("Font Size : {0} ", textFragment.TextState.FontSize);
    Console.WriteLine("Foreground Color : {0} ", textFragment.TextState.ForegroundColor);
}
```

- 这 `foreach` 循环遍历每个 `TextFragment` 在收藏中。
- 我们打印每个片段的各种属性，例如实际文本、其在页面上的位置、字体详细信息和字体大小。
- 这 `XIndent` 和 `YIndent` 属性给出了 PDF 中文本片段的精确坐标。

## 结论

就这样！只需几行代码，我们就成功地使用 Aspose.PDF for .NET 从 PDF 文件中搜索并提取了文本。Aspose.PDF 的灵活性允许您以多种方式操作 PDF，对于需要在 .NET 环境中构建强大 PDF 解决方案的开发人员来说，它是绝佳的选择。您可以轻松扩展此示例，以搜索其他词语、提取更多详细信息，甚至根据需要操作 PDF 内容。希望本指南能为您提供清晰直观的 PDF 操作方法。赶快用您自己的 PDF 尝试一下吧！

## 常见问题解答

### 我可以一次搜索多个单词吗？  
是的，您可以修改 `TextFragmentAbsorber` 通过相应地调整搜索字符串来搜索多个短语。

### 如果文本跨越多行怎么办？  
即使文本跨越多行，Aspose.PDF 仍能识别并提取文本。您可以单独处理这些片段。

### 如何将提取的文本保存到文件？  
您可以使用标准 C# 文件 I/O 操作将提取的文本写入文件，例如 `StreamWriter`。

### Aspose.PDF 是否支持从扫描的 PDF 中提取文本？  
Aspose.PDF 不支持 OCR。对于扫描的 PDF，您需要 OCR 工具来识别文本。

### 如何处理加密的 PDF？  
如果您的 PDF 受密码保护，您可以在加载文档时提供密码，使用 Aspose.PDF 将其解锁。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}