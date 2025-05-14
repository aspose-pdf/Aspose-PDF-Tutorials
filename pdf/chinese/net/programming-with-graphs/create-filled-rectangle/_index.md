---
"description": "通过本分步教程，学习如何使用 Aspose.PDF for .NET 在 PDF 中创建填充矩形。适合所有级别的开发人员。"
"linktitle": "创建填充矩形"
"second_title": "Aspose.PDF for .NET API参考"
"title": "创建填充矩形"
"url": "/zh/net/programming-with-graphs/create-filled-rectangle/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 创建填充矩形

## 介绍

您是否想过以编程方式创建美观的 PDF？如果您有，那么您来对地方了！在本教程中，我们将深入探讨 Aspose.PDF for .NET，这是一个功能强大的库，可让您轻松操作 PDF 文档。今天，我们将重点介绍如何在 PDF 文件中创建填充矩形。无论您是经验丰富的开发人员还是刚刚入门，本指南都将以友好且引人入胜的方式引导您完成每个步骤。所以，戴上您的编程帽，让我们开始吧！

## 先决条件

在我们进入代码之前，您需要做好以下几件事：

1. Visual Studio：确保您的计算机上已安装 Visual Studio。它是一款出色的 .NET 开发 IDE。
2. Aspose.PDF for .NET：您需要下载并安装 Aspose.PDF 库。您可以找到它 [这里](https://releases。aspose.com/pdf/net/).
3. C# 基础知识：稍微熟悉一下 C# 编程将有助于您更好地理解代码片段。

## 导入包

首先，你需要在 C# 项目中导入必要的包。具体操作如下：

### 创建新项目

打开 Visual Studio 并创建一个新的 C# 项目。为了简单起见，您可以选择“控制台应用程序”。

### 添加 Aspose.PDF 参考

1. 在解决方案资源管理器中右键单击您的项目。
2. 选择“管理 NuGet 包”。
3. 搜索“Aspose.PDF”并安装最新版本。

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

现在我们已经设置好了一切，让我们深入研究代码！

## 步骤 1：设置文档目录

首先，您需要指定 PDF 的保存路径。这很重要，因为它会告诉程序在哪里创建文件。

```csharp
// 文档目录的路径。
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

代替 `"YOUR DOCUMENT DIRECTORY"` 使用您想要保存 PDF 的机器上的实际路径。

## 步骤 2：创建文档实例

接下来，我们将创建一个 `Document` 类。此类代表您将要处理的 PDF 文档。

```csharp
// 创建 Document 实例
Document doc = new Document();
```

此行初始化一个我们可以操作的新 PDF 文档。

## 步骤 3：向文档添加页面

现在，让我们在文档中添加一页。每个 PDF 至少都需要一页，对吧？

```csharp
// 将页面添加到 PDF 文件的页面集合
Page page = doc.Pages.Add();
```

此代码向文档添加了一个新页面，允许我们在其上绘制形状。

## 步骤 4：创建图形实例

要绘制形状，我们需要创建一个 `Graph` 例如。将图表想象成一块画布，您可以在上面绘制各种形状。

```csharp
// 创建 Graph 实例
Aspose.Pdf.Drawing.Graph graph = new Aspose.Pdf.Drawing.Graph(100.0, 400.0);
```

这里，我们创建一个宽度为 100、高度为 400 的图表。

## 步骤 5：将图表添加到页面

现在我们有了图表，让我们将其添加到我们之前创建的页面中。

```csharp
// 将图形对象添加到页面实例的段落集合中
page.Paragraphs.Add(graph);
```

此行将图形附加到页面上，以便可以进行绘制。

## 步骤 6：创建矩形实例

接下来，我们将创建一个想要填充颜色的矩形。

```csharp
// 创建 Rectangle 实例
Aspose.Pdf.Drawing.Rectangle rect = new Aspose.Pdf.Drawing.Rectangle(100, 100, 200, 120);
```

在这段代码中，我们定义了矩形的位置和大小。参数分别代表 x 和 y 坐标、宽度和高度。

## 步骤 7：指定填充颜色

现在，让我们为矩形选择一种颜色。在本例中，我们将用红色填充。

```csharp
// 指定图形对象的填充颜色
rect.GraphInfo.FillColor = Aspose.Pdf.Color.Red;
```

这行代码将矩形的填充颜色设置为红色。你可以选择任何你喜欢的颜色！

## 步骤 8：将矩形添加到图形中

矩形准备好后，就可以将其添加到图表中了。

```csharp
// 将矩形对象添加到图形对象的形状集合中
graph.Shapes.Add(rect);
```

此代码将矩形添加到图形中，使其成为我们绘图的一部分。

## 步骤9：保存PDF文档

最后，我们需要将文档保存到指定的目录。

```csharp
dataDir = dataDir + "CreateFilledRectangle_out.pdf";
// 保存 PDF 文件
doc.Save(dataDir);
```

此代码将 PDF 文件保存为 `CreateFilledRectangle_out.pdf` 在您之前指定的目录中。

## 步骤10：确认消息

为了让我们知道一切进展顺利，我们可以打印一条确认信息。

```csharp
Console.WriteLine("\nFilled rectangle object created successfully.\nFile saved at " + dataDir);
```

此行将在控制台中输出一条消息，确认已成功创建填充矩形。

## 结论

就这样！您已经成功使用 Aspose.PDF for .NET 在 PDF 文档中创建了一个填充矩形。这个强大的库为 PDF 操作开辟了无限可能，让您能够以编程方式创建精美的文档。无论您是生成报告、发票还是任何其他类型的 PDF，Aspose.PDF 都能满足您的需求。

## 常见问题解答

### 什么是 Aspose.PDF for .NET？
Aspose.PDF for .NET 是一个库，允许开发人员以编程方式创建、操作和转换 PDF 文档。

### 我可以免费使用 Aspose.PDF 吗？
是的，Aspose 提供免费试用版，您可以用它来探索该库的功能。您可以下载 [这里](https://releases。aspose.com/).

### 有没有办法获得对 Aspose.PDF 的支持？
当然！您可以通过 Aspose 论坛获得支持 [这里](https://forum。aspose.com/c/pdf/10).

### 我如何购买 Aspose.PDF？
您可以通过访问购买页面购买 Aspose.PDF [这里](https://purchase。aspose.com/buy).

### 我可以使用 Aspose.PDF 创建哪些类型的形状？
您可以使用 Aspose.PDF 库创建各种形状，包括矩形、圆形、线条等。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}