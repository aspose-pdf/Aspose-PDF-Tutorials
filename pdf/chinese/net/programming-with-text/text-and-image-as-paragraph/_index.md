---
"description": "使用 Aspose.PDF for .NET 创建包含文本和图像的 PDF。学习如何逐步添加文本和内联图像。"
"linktitle": "PDF 文件中的文本和图像作为段落"
"second_title": "Aspose.PDF for .NET API参考"
"title": "PDF 文件中的文本和图像作为段落"
"url": "/zh/net/programming-with-text/text-and-image-as-paragraph/"
"weight": 530
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF 文件中的文本和图像作为段落

## 介绍

在当今的数字世界中，PDF 是我们大多数人每天都会遇到的通用文档格式。无论是报告、电子书还是商业发票，PDF 都可以轻松地跨平台共享信息。但是，如果您想以编程方式自定义 PDF 怎么办？Aspose.PDF for .NET 正是为此而生。在本教程中，我们将指导您使用 Aspose.PDF for .NET 将文本和图像作为内联段落插入 PDF 文件中。

## 先决条件

在深入研究代码之前，让我们确保您拥有顺利进行所需的一切：

- Aspose.PDF for .NET 库：您需要安装 Aspose.PDF for .NET。您可以下载 [这里](https://releases。aspose.com/pdf/net/).
- Visual Studio：任何支持 .NET 的版本都可以正常工作。
- 对 C# 的基本了解：熟悉一些 C# 将会有所帮助，但别担心 - 我会引导您完成每一步！
- PDF 文档就绪：如果您想添加自定义图像，请准备好。

您还可以免费试用该库 [这里](https://releases.aspose.com/)或者如果你正在从事大型项目，可以考虑购买 [这里](https://purchase.aspose.com/buy)需要更多详细信息？查看文档 [这里](https://reference。aspose.com/pdf/net/).

## 导入包

要开始使用 Aspose.PDF for .NET，您需要导入所需的命名空间。这些命名空间允许您的 C# 代码与 Aspose.PDF 功能进行交互。

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System;
```

很简单，对吧？现在让我们进入最有趣的部分——创建你自己的 PDF 文件。

## 分步指南：创建包含文本和内嵌图像的 PDF

让我们把它分解成易于理解、易于遵循的步骤。想象一下你在拼拼图；每个步骤都像是找到并拼好正确的一块。

## 步骤 1：初始化 PDF 文档

第一步是使用 Aspose.PDF 初始化一个新的 PDF 文档。该文档将作为添加文本和图像的基础。

```csharp
// 文档目录的路径。
string dataDir = "YOUR DOCUMENT DIRECTORY";
// 实例化 Document 实例
Document doc = new Document();
```

这里发生了什么？我们只是使用 `Document` 类并定义要保存 PDF 的目录。这就像为你的杰作开辟了一块新的画布！

## 第 2 步：向 PDF 添加页面

没有页面的文档没什么用，对吧？让我们在文档中添加一个空白页。

```csharp
// 将页面添加到 Document 实例的页面集合中
Page page = doc.Pages.Add();
```

这段代码会将新页面添加到文档的页面集合中。你可以将其想象成翻开笔记本中的一张空白页。

## 步骤 3：添加段落文本

接下来，我们将添加一个文本段落。您可以在这里插入消息或标题。

```csharp
// 创建 TextFragment
TextFragment text = new TextFragment("Hello World.. ");
// 将文本片段添加到 Page 对象的段落集合中
page.Paragraphs.Add(text);
```

在这里，我们创建一个 `TextFragment` 对象保存文本“Hello World...”，然后将其作为段落添加到页面中。这就像在 PDF 文档中写下第一句话一样。

## 步骤 4：添加图像作为内联段落

现在我们已经有了文本，接下来让我们来添加一张图片作为内联段落，让它更有趣一些。内联段落的意思是，图片会紧跟在文本之后显示，就像 Word 文档中图片的显示方式一样。

```csharp
// 创建图像实例
Aspose.Pdf.Image image = new Aspose.Pdf.Image();
// 将图像设置为内联段落，以便它出现在 
// 上一段对象（TextFragment）
image.IsInLineParagraph = true;
// 指定图像文件路径 
image.File = dataDir + "aspose-logo.jpg";
```

在此代码片段中，我们创建了一个 `Image` 对象，指定其与文本对齐，并指定图像文件的路径。这相当于在文档中将图像粘贴到句子后面。您可以将“aspose-logo.jpg”替换为您想要的图像。

## 步骤5：设置图像大小（可选）

想要调整图像大小吗？没问题。Aspose.PDF 允许您在将图像添加到文档之前调整其高度和宽度。

```csharp
// 设置图像高度（可选）
image.FixHeight = 30;
// 设置图像宽度（可选）
image.FixWidth = 100;
```

此部分是可选的，但它可以帮助您控制图像在 PDF 中的显示大小。这就像在打印照片之前调整其大小一样。

## 步骤 6：将图像添加到段落集合

我们已经准备好了图像。现在让我们将其作为内联段落插入到文档中。

```csharp
// 将图像添加到页面对象的段落集合中
page.Paragraphs.Add(image);
```

这行代码会在段落集合中的文本之后立即添加图片。这就像在文本编辑器中点击“插入图片”按钮一样。

## 步骤 7：添加另一个内联文本段落

如果您想在图片后立即添加更多文本怎么办？让我们通过插入另一个内联文本片段来实现。

```csharp
// 使用不同的内容重新初始化 TextFragment 对象
text = new TextFragment(" Hello Again..");
// 将 TextFragment 设置为内联段落
text.IsInLineParagraph = true;
// 将新创建的 TextFragment 添加到页面的段落集合中
page.Paragraphs.Add(text);
```

我们正在重复使用 `TextFragment` 在此处添加一个对象，并在图片后插入新文本（“Hello Again...”），使其内联。这样可以使您的 PDF 看起来更流畅、更协调。

## 步骤 8：保存 PDF 文档

快完成了！现在，让我们将文档保存到您指定的目录。

```csharp
dataDir = dataDir + "TextAndImageAsParagraph_out.pdf";
doc.Save(dataDir);
Console.WriteLine("\nText and image added successfully as inline paragraphs.\nFile saved at " + dataDir);
```

最后一步将文件保存到您的目录中，名称为“TextAndImageAsParagraph_out.pdf”。恭喜您——您已创建包含文本和内联图片的 PDF！

## 结论

就这样，使用 Aspose.PDF for .NET 创建包含文本和图像作为内联段落的 PDF 非常简单，只需按照以下步骤操作即可。只需几行代码，即可向 PDF 文件添加动态内容，使其更具视觉吸引力和专业性。无论是用于商业报告还是电子书，掌控 PDF 的布局都能带来显著的改变。

## 常见问题解答

### 我可以添加多个图像作为内联段落吗？  
是的，您可以通过创建单独的 `Image` 对象并将它们添加到段落集合中。

### 我可以控制 PDF 中文本和图像的位置吗？  
是的，使用边距等属性，您可以控制文本和图像的精确位置。

### Aspose.PDF for .NET 免费吗？  
不，这是授权产品，但你可以得到 [免费试用](https://releases.aspose.com/) 或购买许可证 [这里](https://purchase。aspose.com/buy).

### 我可以在文本中添加超链接吗？  
是的，Aspose.PDF 允许您在文本片段中添加超链接。请查看 [文档](https://reference.aspose.com/pdf/net/) 了解更多详情。

### 我可以自定义文本的字体和样式吗？  
当然！您可以轻松自定义文本片段的字体、颜色和其他样式属性。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}