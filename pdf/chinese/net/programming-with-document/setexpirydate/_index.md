---
"description": "了解如何使用 Aspose.PDF for .NET 设置 PDF 文件的到期日期。本分步指南将帮助您增强文档安全性。"
"linktitle": "在 PDF 文件中设置到期日期"
"second_title": "Aspose.PDF for .NET API参考"
"title": "在 PDF 文件中设置到期日期"
"url": "/zh/net/programming-with-document/setexpirydate/"
"weight": 300
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 文件中设置到期日期

## 介绍

在当今的数字时代，文档的管理和保护比以往任何时候都更加重要。想象一下，发送一份 PDF 文件，它会在特定日期后自动变为不可访问状态。听起来很神奇，对吧？有了 Aspose.PDF for .NET，您可以轻松设置 PDF 文件的到期日期。此功能对于需要在特定期限后限制访问的敏感文档尤其有用。在本教程中，我们将逐步指导您如何在 PDF 文件中设置到期日期。所以，戴上您的编程帽，让我们开始吧！

## 先决条件

在我们开始之前，您需要做好以下几点：

1. 开发环境：确保您已设置好 .NET 开发环境。可以是 Visual Studio 或任何其他支持 .NET 的 IDE。
2. Aspose.PDF for .NET：您需要安装 Aspose.PDF 库。如果您还没有安装，可以从以下网址下载： [这里](https://releases。aspose.com/pdf/net/).
3. C# 基础知识：本教程假设您已具备 C# 编程基础知识。如果您是 C# 新手，不用担心！我们会尽量简化教程，使其直观易懂。

## 导入包

要开始使用 Aspose.PDF，您需要在 C# 项目中导入必要的命名空间。操作方法如下：

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
```

这些命名空间使您能够访问在 Aspose.PDF 中处理 PDF 文档所需的核心功能。

## 步骤 1：设置文档目录

首先，您需要指定文档目录的路径。输出的 PDF 将保存在这里。 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

代替 `"YOUR DOCUMENT DIRECTORY"` 替换为您想要保存 PDF 文件的实际路径。这就像告诉程序：“嘿，这就是我保存文件的地方！”

## 步骤2：实例化文档对象

接下来，您需要创建一个新的实例 `Document` 类。这是您将创建 PDF 的画布。

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

想想 `Document` 对象就像一张白纸。你可以随意添加内容！

## 步骤 3：向 PDF 添加页面

现在你已经设置好了文档，是时候添加页面了。你的内容将存放在这里。

```csharp
doc.Pages.Add();
```

您刚刚在 PDF 中创建了一个新页面。这就像在笔记本中添加了一个新页面，您可以在其中记录自己的想法。

## 步骤 4：向页面添加文本

让我们添加一些文字，让这个页面更有趣一些。我们将添加一条简单的“Hello World”消息。

```csharp
doc.Pages[1].Paragraphs.Add(new TextFragment("Hello World..."));
```

这行代码会在 PDF 的第一页添加一段文本。就像在页面顶部写个标题一样！

## 步骤 5：创建到期日期的 JavaScript

现在到了最有趣的部分！您将创建一个 JavaScript 操作来检查 PDF 的到期日期。如果当前日期超过了到期日期，则会向用户发出一条消息提醒。

```csharp
JavascriptAction javaScript = new JavascriptAction(
"var year=2017;"
+ "var month=5;"
+ "today = new Date(); today = new Date(today.getFullYear(), today.getMonth());"
+ "expiry = new Date(year, month);"
+ "if (today.getTime() > expiry.getTime())"
+ "app.alert('The file is expired. You need a new one.');");
```

以下是正在发生的事情：
- 您定义到期年份和月份。
- 您将获得今天的日期。
- 您将今天的日期与到期日进行比较。
- 如果今天的日期已过有效期，则会弹出一条消息！

## 步骤 6：将 JavaScript 设置为 PDF 打开操作

现在，您需要将 JavaScript 操作设置为 PDF 文档的打开操作。这意味着 JavaScript 将在 PDF 打开后立即运行。

```csharp
doc.OpenAction = javaScript;
```

这行代码告诉 PDF 在有人打开时执行 JavaScript。这就像设置一个提醒，只要你打开日历就会响起！

## 步骤 7：保存 PDF 文档

最后，是时候使用到期日期功能保存您的 PDF 文档了。 

```csharp
dataDir = dataDir + "SetExpiryDate_out.pdf";
doc.Save(dataDir);
```

这行代码会将您的 PDF 文件保存到指定目录，文件名为“SetExpiryDate_out.pdf”。就像把您完成的艺术品装裱起来一样！

## 结论

就这样！您已成功使用 Aspose.PDF for .NET 创建了一个带有到期日期的 PDF 文件。此功能不仅增强了安全性，还能确保敏感信息得到妥善管理。无论您发送的是合同、报告还是其他重要文件，设置到期日期都可能至关重要。

## 常见问题解答

### 什么是 Aspose.PDF for .NET？
Aspose.PDF for .NET 是一个强大的库，允许开发人员在 .NET 应用程序中创建、操作和转换 PDF 文档。

### 我可以免费使用 Aspose.PDF 吗？
是的，您可以使用 Aspose.PDF 的免费试用版。您可以下载它。 [这里](https://releases。aspose.com/).

### 如何购买 Aspose.PDF？
您可以通过访问购买 Aspose.PDF [购买页面](https://purchase。aspose.com/buy).

### 如果我需要支持怎么办？
如果您有任何疑问或需要帮助，您可以访问 [Aspose 支持论坛](https://forum。aspose.com/c/pdf/10).

### 我可以获得 Aspose.PDF 的临时许可证吗？
是的，您可以申请临时驾照 [这里](https://purchase。aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}