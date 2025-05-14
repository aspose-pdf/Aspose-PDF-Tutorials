---
"description": "通过本分步指南，学习如何使用 Aspose.PDF for .NET 在 PDF 文档中设置文件信息。轻松使用元数据增强您的 PDF 文档。"
"linktitle": "在 PDF 文件中设置文件信息"
"second_title": "Aspose.PDF for .NET API参考"
"title": "在 PDF 文件中设置文件信息"
"url": "/zh/net/programming-with-document/setfileinfo/"
"weight": 310
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 文件中设置文件信息

## 介绍

在管理 PDF 文件时，掌控文档元数据至关重要。无论您是想添加作者信息、关键字，还是主题行，Aspose.Pdf for .NET 都能为您提供无缝设置 PDF 文档文件信息的方法。本教程将逐步指导您完成整个过程，确保您理解代码的每个部分。所以，戴上您的编程帽，让我们一起探索 PDF 操作的世界吧！

## 先决条件

在我们开始之前，您需要做好以下几点：

1. Visual Studio：确保您的计算机上已安装 Visual Studio。您将在这里编写和执行 .NET 代码。
   
2. Aspose.PDF for .NET：您需要下载并安装 Aspose.PDF 库。您可以从 [Aspose 下载页面](https://releases。aspose.com/pdf/net/).

3. C# 基础知识：熟悉 C# 编程将帮助您理解我们将使用的代码片段。

4. PDF 文件：准备好要修改的示例 PDF 文件。在本教程中，我们将其称为 `SetFileInfo。pdf`.

一旦完成所有设置，我们就可以开始编写代码了！

## 导入包

首先，您需要导入处理 PDF 文件所需的软件包。在您的 C# 项目中，在代码文件的顶部添加以下 using 指令：

```csharp
using System;
using System.IO;
using Aspose.Pdf;
```

这些命名空间提供对有效操作 PDF 文档所需的类和方法的访问。

## 步骤1：定义文档目录

首先，您需要指定 PDF 文件所在的目录。这很重要，因为您将从此路径打开文件。

```csharp
// 文档目录的路径。
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

解释：替换 `"YOUR DOCUMENT DIRECTORY"` 包含您的文件夹的实际路径 `SetFileInfo.pdf`。这会告诉您的程序在哪里寻找 PDF 文件。

## 第 2 步：打开 PDF 文档

接下来，打开要修改的 PDF 文档。使用 `Document` Aspose.PDF 库中的类。

```csharp
// 打开文档
Document pdfDocument = new Document(dataDir + "SetFileInfo.pdf");
```

解释：在这里，我们创建了 `Document` 类并传递 PDF 文件的路径。这会将文档加载到内存中，以供编辑。

## 步骤3：创建文档信息对象

现在我们已经打开了文档，我们需要创建一个保存文档信息的对象。

```csharp
// 指定文档信息
DocumentInfo docInfo = new DocumentInfo(pdfDocument);
```

解释： `DocumentInfo` 该类允许我们设置 PDF 的各种元数据属性。此对象将用于存储作者、创建日期等信息。

## 步骤4：设置文档元数据

随着 `DocumentInfo` 对象准备就绪后，就可以用相关的元数据填充它了。在这里，您可以指定文档的作者、创建日期、关键字、修改日期、主题和标题。

```csharp
docInfo.Author = "Aspose";
docInfo.CreationDate = DateTime.Now;
docInfo.Keywords = "Aspose.Pdf, DOM, API";
docInfo.ModDate = DateTime.Now;
docInfo.Subject = "PDF Information";
docInfo.Title = "Setting PDF Document Information";
```

说明：每行设置文档的一个特定属性。例如， `docInfo.Author` 设置作者姓名，同时 `docInfo.CreationDate` 设置文档的创建日期。您可以根据需要自定义这些值。

## 步骤5：保存文档

设置所需的元数据后，下一步是保存修改后的 PDF。您需要为输出文件指定一个新路径。

```csharp
dataDir = dataDir + "SetFileInfo_out.pdf";
// 保存输出文档
pdfDocument.Save(dataDir);
```

解释：在这里，我们附加 `_out.pdf` 以原始文件名为修改后的文档创建一个新文件。 `Save` 方法然后将更改写入这个新文件。

## 步骤6：确认更改

最后，最好确认信息设置正确。您可以通过在控制台上打印一条成功消息来确认。

```csharp
Console.WriteLine("\nFile informations setup successfully.\nFile saved at " + dataDir);
```

说明：此行输出一条消息，指示文件已成功保存，以及新文件的路径。这是一种确保一切按计划进行的简单方法。

## 结论

使用 Aspose.PDF for .NET 在 PDF 文档中设置文件信息非常简单，可以显著提升 PDF 的可用性。按照以下步骤，您可以轻松添加元数据，例如作者、创建日期等，从而使您的文档更具信息量和专业性。无论您是开发生成 PDF 的应用程序，还是仅仅需要更好地管理文档，Aspose.PDF 都能为您提供高效完成工作所需的工具。

## 常见问题解答

### 什么是 Aspose.PDF for .NET？
Aspose.PDF for .NET 是一个强大的库，允许开发人员以编程方式创建、操作和转换 PDF 文档。

### 我可以免费使用 Aspose.PDF 吗？
是的，Aspose 提供免费试用版，您可以用它来评估该库。访问 [免费试用页面](https://releases.aspose.com/) 了解更多信息。

### 在哪里可以找到该文档？
Aspose.PDF 的完整文档可以在这里找到 [这里](https://reference。aspose.com/pdf/net/).

### 如何购买 Aspose.PDF？
您可以通过以下方式购买 Aspose.PDF 许可证 [购买页面](https://purchase。aspose.com/buy).

### 如果我需要支持怎么办？
如果您有任何疑问或需要帮助，您可以访问 [Aspose 支持论坛](https://forum。aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}