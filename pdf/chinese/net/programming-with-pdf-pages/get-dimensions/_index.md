---
"description": "在本教程中，我们将讲解如何使用 Aspose.PDF for .NET 获取 PDF 页面尺寸并执行相关操作。我们将提供详细的步骤来指导您完成整个过程。"
"linktitle": "获取 PDF 页面尺寸"
"second_title": "Aspose.PDF for .NET API参考"
"title": "获取 PDF 页面尺寸"
"url": "/zh/net/programming-with-pdf-pages/get-dimensions/"
"weight": 60
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 获取 PDF 页面尺寸

## 介绍

您是否曾经需要调整 PDF 文档的页面尺寸？或者您想调整页面大小或旋转以满足您的需求？如果是这样，那么您来对地方了！在本教程中，我们将指导您使用 Aspose.PDF for .NET 获取和修改 PDF 页面尺寸。无论您是初学者还是经验丰富的开发人员，您都会发现本指南简单易懂。

Aspose.PDF for .NET 是一个功能强大的库，可让您轻松创建、操作和转换 PDF 文件。它就像一把 PDF 的瑞士军刀——您可以调整每个小细节以满足您的具体需求。那么，让我们深入学习一下如何使用这个强大的工具来获取和更新 PDF 页面尺寸！

## 先决条件

在开始之前，您需要做好一些准备才能顺利完成本教程：

1. Aspose.PDF for .NET：您可以 [点击此处下载最新版本](https://releases.aspose.com/pdf/net/)。如果您没有驾照，不用担心！您可以申请 [免费试用](https://releases.aspose.com/)或选择 [临时执照](https://purchase。aspose.com/temporary-license/).
2. Visual Studio：用于编写和执行代码的开发环境。
3. C# 的基础知识：虽然我们会让事情变得简单，但熟悉 C# 会使过程更加顺畅。
4. 要使用的 PDF 文件：获取任何示例 PDF 文件或创建一个新的 PDF 文件进行测试。

## 导入包

要使用 Aspose.PDF for .NET，您需要导入一些必要的命名空间。这将为与 PDF 文档的交互奠定基础。操作方法如下：

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

这些导入确保您可以访问操作 PDF 文件所需的核心类，特别是管理页面和检索其尺寸。

现在我们已经准备好一切，让我们将流程分解为易于遵循的步骤。

## 步骤 1：定义文件路径并加载文档

第一步是指定 PDF 文档的路径并使用 Aspose.PDF 加载它。这将允许您与 PDF 文件中的页面进行交互。

```csharp
// 文档目录的路径。
string dataDir = "YOUR DOCUMENT DIRECTORY";

// 打开文档
Document pdfDocument = new Document(dataDir + "UpdateDimensions.pdf");
```

在此步骤中，您实际上是打开要处理的 PDF 文件。如果您曾经打开过一本书并跳转到特定页面，那么这和打开 PDF 文件的操作非常相似——只不过，您打开的是 PDF 文档，以便访问其中的页面。

## 步骤 2：如果不存在页面，则添加空白页

如果您的文档没有页面怎么办？别担心！我们可以在文档中添加一个空白页并进行处理。以下是如何检查页面是否存在并在必要时添加新页面的方法：

```csharp
// 向 PDF 文档添加空白页
Page page = pdfDocument.Pages.Count > 0 ? pdfDocument.Pages[1] : pdfDocument.Pages.Add();
```

这行代码检查文档中是否已有页面。如果是，则选择第一页（`Pages[1]`）。否则，它会创建一个空白页并将其添加到 PDF 中。

想象一下打开一本空白笔记本，如果上面什么都没有就在第一页上写字——很简单，对吧？

## 步骤3：获取页面高度和宽度信息

现在我们有了一个可以使用的页面，让我们获取页面的尺寸。我们将使用 `GetPageRect()` 方法来获取高度和宽度。

```csharp
// 获取页面高度和宽度信息
Console.WriteLine(page.GetPageRect(true).Width.ToString() + ":" + page.GetPageRect(true).Height.ToString());
```

这里， `GetPageRect(true)` 返回一个包含页面高度和宽度的矩形。这就像用尺子测量一张纸一样。输出将显示在控制台中，显示当前页面的尺寸。

## 步骤 4：将页面旋转 90 度

你想旋转页面吗？没问题！只需一个简单的属性，你就可以把页面旋转 90 度。

```csharp
// 将页面旋转 90 度
page.Rotate = Rotation.on90;
```

这一步会将页面顺时针旋转 90 度。想象一下，你正在桌上旋转一张打印好的纸张——现在它就处于横向模式了！

## 步骤 5：旋转后重新检查页面尺寸

旋转页面后，最好再次检查尺寸。为什么？因为旋转会影响你对高度和宽度的理解。

```csharp
// 获取页面高度和宽度信息
Console.WriteLine(page.GetPageRect(true).Width.ToString() + ":" + page.GetPageRect(true).Height.ToString());
```

现在，页面尺寸将根据新的方向进行更新。这就像在手机上旋转照片一样——宽度突然变成了高度，反之亦然。


## 结论

恭喜！您已成功学习了如何使用 Aspose.PDF for .NET 获取和修改 PDF 页面尺寸。现在，您应该能够加载 PDF、检查其页面尺寸，甚至根据需要旋转页面。

处理 PDF 并不复杂。使用 Aspose.PDF，只需遵循几个步骤并使用直观的方法即可轻松完成。下次您需要处理 PDF 页面尺寸时，您就能轻松掌握！

## 常见问题解答

### 除了 90 度以外，我还可以按其他角度旋转页面吗？
是的，Aspose.PDF 允许您使用 `Rotation` 财产。

### 如果我的 PDF 没有页面会怎样？
如果您的 PDF 没有页面，您可以使用 `Pages.Add()` 方法，如本教程所示。

### 我可以同时操作多个页面吗？
是的，您可以循环遍历多个页面并对所有页面应用转换，例如调整大小或旋转。

### 页面尺寸会影响 PDF 中的内容吗？
页面尺寸只会改变画布的大小，而不会改变内容。但是，调整大小可能会改变内容在页面上的显示方式。

### 在哪里可以找到有关 Aspose.PDF for .NET 的更多信息？
您可以访问 [文档在这里](https://reference.aspose.com/pdf/net/) 了解更多详细信息和高级用例。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}