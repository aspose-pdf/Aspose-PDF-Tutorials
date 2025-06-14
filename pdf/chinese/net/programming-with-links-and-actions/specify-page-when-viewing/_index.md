---
"description": "了解如何使用 Aspose.PDF for .NET 指定 PDF 中要查看的页面。本指南简单易懂，助您提升导航体验。"
"linktitle": "查看时指定页面"
"second_title": "Aspose.PDF for .NET API参考"
"title": "查看时指定页面"
"url": "/zh/net/programming-with-links-and-actions/specify-page-when-viewing/"
"weight": 110
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 查看时指定页面

## 介绍

您是否希望通过在用户打开文档时将用户引导至特定页面来增强您的 PDF 应用程序？您来对地方了！在本指南中，我们将深入探讨如何使用 Aspose.PDF for .NET 指定 PDF 打开时应显示的页面。此功能可以显著提升用户体验，尤其是在您需要吸引用户注意文档关键部分时。

## 先决条件

在开始编写代码之前，我们先确保你已经准备好一切准备就绪。以下是你需要准备的东西：

1. .NET 基础知识：熟悉 .NET 框架至关重要。如果您熟悉 C#，并且对面向对象编程有基本的了解，那就准备好了！

2. Aspose.PDF for .NET：您需要在项目中安装 Aspose.PDF 库。如果您尚未安装，可以下载 [这里](https://releases。aspose.com/pdf/net/).

3. Visual Studio：本教程假设您使用 Visual Studio 作为 IDE。请确保您的计算机上已安装 Visual Studio。

4. PDF 文件：您需要一个现有的 PDF 文件。如果没有，您可以创建一个示例文档，或使用您选择的任何 PDF 文件。

一旦满足了这些先决条件，我们就可以卷起袖子开始编码了！

## 导入包

现在我们已经完成了所有设置，接下来将必要的包导入到我们的项目中。请按照以下步骤操作：

### 启动 Visual Studio

打开 Visual Studio 并创建一个新项目或加载一个现有项目，在其中实现 PDF 页面查看功能。

### 参考Aspose.PDF

要使用 Aspose.PDF 库，您需要添加对它的引用：

1. 在解决方案资源管理器中右键单击您的项目。
2. 选择“管理 NuGet 包”。
3. 搜索 `Aspose.PDF` 并安装该软件包。

### 导入命名空间

在代码文件顶部添加以下使用指令：

```csharp
using System;
using System.IO;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
```

现在，您已准备好开始构建 PDF 页面导航逻辑！

让我们将任务分解成几个易于管理的步骤。我们将编写代码来打开 PDF 文档、指定查看时显示的特定页面，并保存更新后的文档。 

## 步骤1：设置文档目录

首先，您需要设置文档的路径：

```csharp
// 文档目录的路径。
string dataDir = "YOUR DOCUMENT DIRECTORY"; // 替换为您的目录
```

这行代码本质上是你的路线图。你正在告诉你的代码在哪里找到 PDF 文件。确保替换 `YOUR DOCUMENT DIRECTORY` 使用您机器上的实际路径。

## 步骤2：加载PDF文件

接下来，将 PDF 文件加载到应用程序中：

```csharp
// 加载 PDF 文件
Document doc = new Document(dataDir + "SpecifyPageWhenViewing.pdf");
```

这里发生的事情是，你正在创建一个新的 `Document` 对象，同时指定 PDF 文件的路径。您可以将其想象成打开刚刚放在桌子上的书。

## 步骤3：访问所需页面

现在，让我们访问文档打开时想要显示的页面：

```csharp
// 获取文档第二页的实例
Page page2 = doc.Pages[2]; // 请记住，索引从 1 开始
```

这里，我们正在访问文档的第二页。值得注意的是，页码从 1 开始，所以如果您要访问第 2 页，则需要使用索引 2。

## 步骤 4：设置缩放系数

您可以调整将显示的页面的缩放级别：

```csharp
// 创建变量来设置目标页面的缩放比例
double zoom = 1; // 表示 100% 缩放
```

设置缩放比例有助于确定用户打开页面后可立即看到的页面大小。值为 1 表示页面将以 100% 的缩放比例显示，这通常是一个不错的默认值。

## 步骤 5：创建 GoToAction 实例

让我们将导航功能付诸实践：

```csharp
// 创建 GoToAction 实例
GoToAction action = new GoToAction(doc.Pages[2]); 
```

在此步骤中，您将创建一个实例 `GoToAction` 这实质上代表了导航到 PDF 中特定点的操作——在本例中是第二页。

## 步骤 6：定义目标

现在，您需要定义操作应该导致什么结果：

```csharp
// 转至第 2 页
action.Destination = new XYZExplicitDestination(page2, 0, page2.Rect.Height, zoom);
```

这行代码相当于为 GoToAction 设置了一个 GPS 目的地。你告诉它以指定的缩放级别，从页面顶部（高度）跳转到第 2 页。

## 步骤 7：设置打开操作

让我们确保此操作在打开文档时发生：

```csharp
// 设置文档打开操作
doc.OpenAction = action;
```

这样，您就声明了当 PDF 打开时，我们刚刚定义的导航操作就会被激活。就好像您在文档的前门设置了迎宾垫一样。

## 步骤 8：保存更新后的文档

最后，让我们保存已做更改的文档：

```csharp
// 保存更新的文档
doc.Save(dataDir + "goto2page_out.pdf");
```

这一步完成了你的工作！你将获得一个名为 `goto2page_out.pdf` 直接打开您指定的页面。

这样，编码部分就完成了！您已成功编程 Aspose.PDF，使其在打开 PDF 时显示特定页面。 

## 结论

在本指南中，我们逐步讲解了如何使用 Aspose.PDF for .NET 在 PDF 文件中指定页面。此功能不仅可以提升用户导航体验，还能简化用户与文档中关键内容的交互。通过运用这些功能，您可以打造更加友好的用户体验，让您的 PDF 应用程序脱颖而出。

## 常见问题解答

### 什么是 Aspose.PDF for .NET？
Aspose.PDF for .NET 是一个库，使开发人员能够在 .NET 应用程序内创建、修改和管理 PDF 文档。

### 我可以指定查看多个页面吗？
不可以，您只能将文档设置为在指定的某个页面打开。但是，您可以为不同的初始页面创建不同的文档。

### 如果我想以不同的缩放级别查看页面怎么办？
您可以通过调整 `zoom` 保存文档之前变量。

### 在哪里可以找到更多使用 Aspose.PDF 的示例？
您可以检查 [文档](https://reference.aspose.com/pdf/net/) 了解更多示例和功能。

### Aspose.PDF for .NET 有免费试用版吗？
是的！您可以下载 Aspose.PDF 的免费试用版 [这里](https://releases。aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}