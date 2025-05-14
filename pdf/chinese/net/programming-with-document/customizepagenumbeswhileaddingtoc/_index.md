---
"description": "在本综合教程中学习如何使用 Aspose.PDF for .NET 向 PDF 文档添加目录并自定义页码。"
"linktitle": "添加目录时自定义页码"
"second_title": "Aspose.PDF for .NET API参考"
"title": "添加目录时自定义页码"
"url": "/zh/net/programming-with-document/customizepagenumbeswhileaddingtoc/"
"weight": 100
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 添加目录时自定义页码

## 介绍

在文档管理领域，PDF 占据主导地位。它们是跨平台共享和保存文档的首选格式。但是，如果您想使用目录 (TOC) 等功能来增强 PDF 文档，该怎么办？Aspose.PDF for .NET 正是为此而生！这个强大的库使开发人员能够轻松操作 PDF 文件，轻松添加、修改和自定义内容。在本教程中，我们将深入探讨如何使用 Aspose.PDF for .NET 为 PDF 文档添加目录并自定义页码。那就拿起您的编程帽子，开始吧！

## 先决条件

在我们进入代码之前，您需要做好以下几件事：

1. Visual Studio：确保您的计算机上已安装 Visual Studio。这将是我们的开发环境。
2. Aspose.PDF for .NET：您需要下载并安装 Aspose.PDF 库。您可以找到它 [这里](https://releases。aspose.com/pdf/net/).
3. C# 基础知识：熟悉 C# 编程将帮助您更好地理解代码片段。
4. PDF 示例文件：请准备好一个 PDF 示例文件以供我们使用。您可以创建一个简单的 PDF 示例文件，也可以下载现有的 PDF 示例文件。

## 导入包

首先，我们需要导入必要的软件包。打开您的 Visual Studio 项目并添加对 Aspose.PDF 库的引用。您可以使用 NuGet 包管理器来执行此操作：

1. 在解决方案资源管理器中右键单击您的项目。
2. 选择“管理 NuGet 包”。
3. 搜索“Aspose.PDF”并安装。

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

一旦安装了库，您就可以开始编码！

## 步骤 1：设置文档目录

首先，我们需要设置文档目录。我们将在这里存储输入和输出的 PDF 文件。 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string inFile = dataDir + "42824.pdf";
string outFile = dataDir + "42824_out.pdf";
```

在此代码片段中，替换 `YOUR DOCUMENT DIRECTORY` 替换为您的 PDF 文件的实际路径。这将帮助我们加载现有 PDF 并保存修改后的版本。

## 步骤2：加载现有PDF文件

现在我们已经设置了文档目录，让我们加载现有的 PDF 文件。 

```csharp
Document doc = new Document(inFile);
```

在这里，我们创建一个新的 `Document` 通过传递输入文件路径来获取 PDF 对象。这使我们能够以编程方式操作 PDF 内容。

## 步骤 3：为目录插入新页面

接下来，我们需要在 PDF 中创建一个新页面，用于存放目录。

```csharp
Aspose.Pdf.Page tocPage = doc.Pages.Insert(1);
```

此行在文档开头插入一个新页面。目录将显示在此页面上。

## 步骤4：创建目录信息

现在，让我们创建一个对象来表示目录信息。

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocInfo.PageNumbersPrefix = "P";
tocPage.TocInfo = tocInfo;
```

在此步骤中，我们创建一个 `TocInfo` 对象并将其标题设置为“目录”。我们还自定义了字体大小和样式。 `PageNumbersPrefix` 设置为“P”，它将作为目录中页码的前缀。

## 步骤 5：将标题添加到目录

现在到了最有趣的部分！我们将循环遍历文档的各个页面，并将标题添加到目录中。

```csharp
for (int i = 1; i < doc.Pages.Count; i++)
{
    Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
    TextSegment segment2 = new TextSegment();
    heading2.TocPage = tocPage;
    heading2.Segments.Add(segment2);
    heading2.DestinationPage = doc.Pages[i + 1];
    heading2.Top = doc.Pages[i + 1].Rect.Height;
    segment2.Text = "Page " + i.ToString();
    tocPage.Paragraphs.Add(heading2);
}
```

在这个循环中，我们创建一个新的 `Heading` 为每个页面创建一个对象。我们为每个标题设置目标页面，并指定要显示的文本，例如“第 X 页”，其中 X 代表页码。最后，我们将标题添加到目录页。

## 步骤6：保存更新后的文档

添加所有必要的标题后，就可以保存更新后的文档了。

```csharp
doc.Save(outFile);
```

这行代码保存了修改后的 PDF，其中包含目录。现在您可以打开输出文件并查看自定义的目录！

## 结论

就这样！您已经成功使用 Aspose.PDF for .NET 为 PDF 文档添加目录，并自定义了页码。这个强大的库让您轻松操作 PDF 文件，只需几行代码，就能显著提升文档质量。无论您是创建报告、电子书还是其他类型的 PDF，拥有目录都能显著提升读者的浏览体验。还在等什么？立即深入了解 Aspose.PDF，开始创建精彩的 PDF 吧！

## 常见问题解答

### 什么是 Aspose.PDF for .NET？
Aspose.PDF for .NET 是一个库，允许开发人员以编程方式创建、操作和转换 PDF 文档。

### 我可以免费使用 Aspose.PDF 吗？
是的，Aspose 提供免费试用版，您可以用它来探索该库的功能。您可以下载 [这里](https://releases。aspose.com/).

### 如何获得 Aspose.PDF 的支持？
您可以通过访问 Aspose 论坛获得支持 [这里](https://forum。aspose.com/c/pdf/10).

### 有临时执照吗？
是的，您可以申请 Aspose.PDF 的临时许可证。 [这里](https://purchase。aspose.com/temporary-license/).

### 在哪里可以购买 Aspose.PDF for .NET？
您可以购买 Aspose.PDF for .NET [这里](https://purchase。aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}