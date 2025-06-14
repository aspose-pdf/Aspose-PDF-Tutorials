---
"description": "通过我们的分步指南学习如何使用 Aspose.PDF for .NET 在 PDF 文件中添加文本标记并提升您的文档演示效果。"
"linktitle": "在 PDF 文件中添加文本印章"
"second_title": "Aspose.PDF for .NET API参考"
"title": "在 PDF 文件中添加文本印章"
"url": "/zh/net/programming-with-stamps-and-watermarks/add-text-stamp/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 文件中添加文本印章

## 介绍

在当今的数字时代，PDF 是共享和交付文档的常用格式。无论您是开发人员、内容创作者，还是仅仅想增强 PDF 文件质量的人，了解如何以编程方式操作 PDF 都可能带来巨大的改变。您可能想要利用的一个实用功能是在 PDF 文件中添加文本印章。添加文本印章可以为您的文档增添专业感，或传达重要信息，例如“示例”、“机密”，甚至是水印。

## 先决条件

在我们开始编写代码之前，需要满足一些先决条件，以确保所有设置都正确无误。以下是您需要准备的：

1. Aspose.PDF for .NET：请确保您的项目中已安装 Aspose.PDF 库。如果您尚未安装，可以从 [Aspose 网站](https://releases。aspose.com/pdf/net/).
2. Visual Studio 或兼容的 IDE：您需要一个开发环境来编写和运行 .NET 代码。Visual Studio 是开发人员最常见的选择。
3. C# 基础知识：熟悉 C# 和面向对象编程原理将帮助您更好地理解示例。
4. 示例 PDF 文件：您应该准备好一个可用的 PDF 文件。您可以创建一个基本 PDF 文件，也可以使用任何现有 PDF 文件来测试其功能。

一旦解决了这些先决条件，我们就可以继续编码了！

## 导入包

现在，让我们导入必要的包。此步骤至关重要，因为它使 Aspose 库中的类和方法在您的项目中可用。

### 导入 Aspose.PDF 程序集

首先，您需要导入 Aspose.PDF 命名空间。在 C# 文件的顶部，添加以下 using 指令：

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

这将使您能够访问创建和操作 PDF 文档所必需的类。

现在，让我们进入本教程的正题。我们将把整个过程分解成清晰简洁的步骤。每个步骤都会引导您完成向 PDF 文件添加文本标记的代码。

## 步骤 1：设置文档目录

首先，您需要建立存储 PDF 文档的目录。这意味着您的代码需要知道在哪里找到您想要编辑的 PDF 文件。

```csharp
// 文档目录的路径。
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

解释：替换 `"YOUR DOCUMENT DIRECTORY"` 与您的 PDF 文件的实际路径（`AddTextStamp.pdf`) 被存储。此路径稍后将用于打开和保存修改后的 PDF。

## 第 2 步：打开 PDF 文档

接下来，我们将使用 `Document` 来自 Aspose.PDF 命名空间的类。

```csharp
// 打开文档
Document pdfDocument = new Document(dataDir + "AddTextStamp.pdf");
```

解释：在这里，我们正在创建一个 `Document` 类并传递 PDF 文件的路径。这将加载 PDF，以便我们可以对其进行操作。

## 步骤 3：创建文本印章

现在，我们将创建一个文本印章，稍后将其应用到我们的 PDF 文档中。

```csharp
// 创建文本戳
TextStamp textStamp = new TextStamp("Sample Stamp");
```

解释： `TextStamp` 对象已创建，其中包含要显示的文本。在本例中，我们使用“示例印章”作为印章的文本。

## 步骤4：设置图章属性

要自定义图章，我们可以设置各种属性，例如背景颜色、位置和旋转。现在就开始吧：

```csharp
// 设置图章是否为背景
textStamp.Background = true;

// 设置原点
textStamp.XIndent = 100;
textStamp.YIndent = 100;

// 旋转印章
textStamp.Rotate = Rotation.on90;
```

解释：
- 背景：将其设置为 `true` 意味着印章将出现在 PDF 内容的后面。
- XIndent 和 YIndent：这两个属性决定了图章在页面上的位置。在本例中，图章将放置在距离页面左边缘和上边缘 100 个单位的位置。
- 旋转：将印章旋转 90 度。您可以根据设计需求选择不同的旋转选项。

## 步骤5：自定义文本属性

接下来，让我们发挥创意，自定义图章内文本的外观：

```csharp
// 设置文本属性
textStamp.TextState.Font = FontRepository.FindFont("Arial");
textStamp.TextState.FontSize = 14.0F;
textStamp.TextState.FontStyle = FontStyles.Bold | FontStyles.Italic;
textStamp.TextState.ForegroundColor = Aspose.Pdf.Color.FromRgb(Color.Aqua);
```

解释：
- 字体：我们使用 Arial 字体并将其设为粗体和斜体。
- FontSize：设置为14点。
- 前景颜色：使用 RGB 将文本颜色设置为浅绿色。您可以随意更改颜色以适合您的品牌或设计需求！

## 步骤 6：向 PDF 页面添加图章

现在是时候将印章添加到 PDF 文档的特定页面了。

```csharp
// 将图章添加到特定页面
pdfDocument.Pages[1].AddStamp(textStamp);
```

说明：在此示例中，图章被添加到 PDF 的第一页（页面索引为 1）。请根据文档的需要调整页码。

## 步骤 7：保存修改后的 PDF

最后，让我们保存带有新添加的文本戳的文档。

```csharp
dataDir = dataDir + "AddTextStamp_out.pdf";

// 保存输出文档
pdfDocument.Save(dataDir);
Console.WriteLine("\nText stamp added successfully.\nFile saved at " + dataDir);
```

解释：我们为输出文件定义一个新路径，然后保存修改后的文档。保存后，该路径将打印到控制台，确认操作成功。

## 结论

恭喜！您已成功使用 Aspose.PDF for .NET 为 PDF 文件添加文本图章。此方法可让您高效地注释文档，从而提升文档的专业性和易用性。无论您是添加水印、签名还是简单的注释，Aspose 库都能提供强大的工具，让您轻松操作 PDF。

## 常见问题解答

### PDF 中的文本标记是什么？
文本图章是一种包含文本的图形覆盖，可以放置在 PDF 文档上，通常用于注释或水印。

### 我可以用图像定制邮票吗？
是的，Aspose.PDF 也支持添加图像印章，提供更多的设计灵活性。

### 我可以与 Aspose.PDF 一起使用哪些编程语言？
Aspose.PDF 主要专注于 .NET，但也有适用于 Java 和 Python 等其他语言的版本。

### 如何获得 Aspose.PDF 的临时许可证？
您可以通过访问申请临时驾照 [购买链接](https://purchase.aspose.com/temporary-license/) 在他们的网站上。

### 在哪里可以找到对 Aspose.PDF 的支持？
Aspose.PDF 支持 [支持论坛](https://forum。aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}