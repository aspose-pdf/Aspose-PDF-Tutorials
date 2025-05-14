---
"description": "通过本完整的分步指南了解如何使用 Aspose.PDF for .NET 将图像存储在 XImage 集合中。"
"linktitle": "将图像存储在 XImage 集合中"
"second_title": "Aspose.PDF for .NET API参考"
"title": "将图像存储在 XImage 集合中"
"url": "/zh/net/programming-with-images/store-image-in-ximage-collection/"
"weight": 290
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 将图像存储在 XImage 集合中

## 介绍

在当今的数字时代，以编程方式处理和操作文档对于许多应用程序至关重要。Aspose.PDF for .NET 使开发人员能够轻松处理 PDF 文件，从而增强工作流程并创建动态内容。在本指南中，我们将深入探讨将图像存储在 XImage 集合中的过程，这是一项至关重要的功能，可让您将视觉效果直接嵌入到 PDF 中。准备好踏上创建精彩内容的旅程吧。

## 先决条件

在深入研究代码和流程之前，您需要确保已做好以下几件事：

- .NET 环境：您的计算机上应已安装 .NET Framework。请根据项目需求选择合适的版本。
- Aspose.PDF for .NET：请确保您已安装 Aspose.PDF 库。您可以从以下网址下载： [这里](https://releases.aspose.com/pdf/net/) 或开始免费试用 [这里](https://releases。aspose.com/).
- 图像文件：您还需要一个要存储在 PDF 中的图像文件（例如 JPG 或 PNG）。在本例中，我们将使用名为“aspose-logo.jpg”的文件。
- 对 C# 的基本了解：熟悉 C# 编程将帮助您顺利完成。

## 导入包

要开始使用 Aspose.PDF for .NET，您需要导入所需的命名空间。此步骤为使用该库提供的所有功能奠定了基础。

```csharp
using System;
using System.IO;
using Aspose.Pdf.Operators;
```

通过导入这些命名空间，您可以启用 Aspose.PDF 中的各种功能，包括文档创建、图像处理等。

让我们将其分解为易于管理的步骤，以便您更轻松地遵循。

## 步骤 1：设置文档目录

你需要做的第一件事是什么？定义文档的存放位置。你需要设置一个变量来保存文档目录的路径。你的 PDF 将被保存在这里。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // 替换为您的实际文档目录。
```

## 第 2 步：初始化文档

现在，是时候创建一个新的 PDF 文档了。这一步将让你的 PDF 焕然一新。 

```csharp
Aspose.Pdf.Document document = new Document();
```

在这里，我们实例化一个新的 Document 对象作为我们的画布。

## 步骤 3：添加新页面

每个杰作都需要一块画布，对吧？在我们的例子中，我们需要在文档中有一页来创作。

```csharp
document.Pages.Add();
Page page = document.Pages[1]; // 获取第一页。
```

我们正在向文档添加一个新页面。现在，我们将对此页面进行操作。

## 步骤4：加载图像文件

接下来，你需要将图像加载到程序中。这一步类似于打开一本书阅读；你需要先访问其中的内容，然后才能使用它。

```csharp
using (FileStream imageStream = new FileStream(dataDir + "aspose-logo.jpg", FileMode.Open))
{
```

此行将图像文件作为流打开，这使我们能够操作它并将其嵌入到 PDF 中。

## 步骤5：将图像添加到页面资源

现在您已经准备好图像，是时候将其添加到页面资源中了，本质上就是告诉 PDF，“嘿，我有一张很酷的图像希望你记住！”

```csharp
page.Resources.Images.Add(imageStream, ImageFilterType.Flate);
XImage ximage = page.Resources.Images[page.Resources.Images.Count];
```

此代码负责将图像添加到 PDF 并将其分配给 `XImage` 我们稍后可以引用的变量。

## 步骤6：准备绘制图像

接下来是有趣的部分——在页面上定位图片。你需要设置坐标，以便将图片精确地放置在你想要的位置。

```csharp
page.Contents.Add(new GSave());
```

这行代码保存了图形状态，以便稍后恢复。这就像在我们进行任何更改之前，对当前设置进行快照一样。

## 步骤 7：定义图像位置和大小

现在，定义您想要放置图像的大小和位置：

```csharp
int lowerLeftX = 0;
int lowerLeftY = 0;
int upperRightX = 600;
int upperRightY = 600;
Aspose.Pdf.Rectangle rectangle = new Aspose.Pdf.Rectangle(lowerLeftX, lowerLeftY, upperRightX, upperRightY);
```

此代码块设置了图像所适合的矩形的尺寸，本质上是为图像在页面上提供了一个位置。

## 步骤 8：创建变换矩阵 

为了控制图像的放置方式，我们将定义一个变换矩阵。它控制着图像在目标坐标上的显示方式。

```csharp
Matrix matrix = new Matrix(new double[] { rectangle.URX - rectangle.LLX, 0, 0, rectangle.URY - rectangle.LLY, rectangle.LLX, rectangle.LLY });
```

可以把这想象成在旅行前绘制一张地图。它有助于确定图像在页面上的显示方式。

## 步骤 9：将图像放置在页面上

现在，是时候真正告诉 PDF 将图像放在哪里了。

```csharp
page.Contents.Add(new ConcatenateMatrix(matrix));
page.Contents.Add(new Do(ximage.Name));
page.Contents.Add(new GRestore());
```

在这里，我们向 PDF 的内容流添加命令，这些命令将根据我们刚刚建立的矩阵实际绘制图像。

## 步骤10：保存文档

终于，我们可以保存我们的杰作了！这是你所有辛勤劳动汇聚成实质成果的时刻。

```csharp
document.Save(dataDir + "FlateDecodeCompression.pdf");
```

您已告知 Aspose.PDF 使用提供的文件名保存文档。运行此代码后，您将在指定的目录中找到新创建的 PDF 文件，其中包含嵌入的图像。

## 结论

就这样！您已经学会了如何使用 Aspose.PDF for .NET 将图像逐点存储在 XImage 集合中。看到代码逐渐成型并生成有用的结果，是不是感到欣慰？无论您是构建应用程序，还是只想自动化报表，本指南都是您不可或缺的基础。请记住，Aspose.PDF 的强大功能不仅仅限于此，还能帮助您完成许多其他任务，所以请继续探索！

## 常见问题解答

### Aspose.PDF 支持哪些图像文件格式？
Aspose.PDF 支持各种图像格式，包括 JPG、PNG、BMP 和 GIF。

### 将图像添加到 PDF 时我可以更改其大小吗？
是的，通过调整矩形中定义的坐标，您可以更改 PDF 中显示的图像的大小。

### 我需要许可证才能使用 Aspose.PDF 吗？
Aspose 提供免费试用和多种购买选项。您可以找到它们 [这里](https://purchase。aspose.com/buy).

### 如果我遇到问题，如何获得支持？
您可以向 Aspose 社区寻求帮助 [这里](https://forum。aspose.com/c/pdf/10).

### 有没有办法对添加到 PDF 的图像应用压缩？
是的，当向 PDF 添加图像时，您可以指定图像过滤器类型以使用 Flate 等压缩方法。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}