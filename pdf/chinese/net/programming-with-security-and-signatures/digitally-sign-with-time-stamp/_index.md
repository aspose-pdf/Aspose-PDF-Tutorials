---
"description": "了解如何使用 Aspose.PDF for .NET 对 PDF 进行数字签名并添加时间戳。本分步指南涵盖先决条件、证书设置、时间戳等内容。"
"linktitle": "在 PDF 文件中使用时间戳进行数字签名"
"second_title": "Aspose.PDF for .NET API参考"
"title": "在 PDF 文件中使用时间戳进行数字签名"
"url": "/zh/net/programming-with-security-and-signatures/digitally-sign-with-time-stamp/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 文件中使用时间戳进行数字签名

## 介绍

您是否曾经需要对 PDF 进行数字签名并添加时间戳以增强安全性？无论您处理的是法律文件、合同还是任何需要安全认证的文件，带有时间戳的数字签名都能提升您的可信度。在本教程中，我们将详细介绍如何使用 Aspose.PDF for .NET 为您的 PDF 文档添加数字签名和时间戳。别担心，我们会一步一步教您！

## 先决条件

在深入研究代码之前，您需要先进行一些设置。以下是入门必备条件的快速清单：

- Aspose.PDF for .NET 库：您需要在项目中安装 Aspose.PDF for .NET 库。您可以 [点击此处下载最新版本](https://releases.aspose.com/pdf/net/) 或者通过 NuGet 将其添加到您的项目中。
- PDF 文档：您需要一个示例 PDF 文件。请确保您的项目目录中包含要签名的文件。
- 数字证书（PFX 文件）：确保您拥有数字证书（ `.pfx` 文件）对文档进行数字签名。
- 时间戳 URL：这是一个在线时间戳服务，将用于将时间戳附加到数字签名。 
- 基本的 C# 知识：您不需要成为专家，但了解 C# 的基础知识将有助于您理解和自定义代码。

一旦勾选了所有这些框，您就可以开始编码了！

## 导入包

首先，您需要将以下命名空间导入到您的 C# 项目中。这确保您可以访问相关的 Aspose.PDF 类和函数。

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;
using System.Collections;
```

## 步骤 1：加载 PDF 文档

我们首先需要加载需要签名的 PDF 文档。操作方法如下：

```csharp
// 定义文档目录的路径
string dataDir = "YOUR DOCUMENTS DIRECTORY";

// 加载 PDF 文档
Document document = new Document(dataDir + @"DigitallySign.pdf");
```

这一步非常简单。我们只需定义要签名的文档的路径即可。 `Document` Aspose.PDF 中的类负责加载文件。

## 第 2 步：设置数字签名

接下来，我们将使用 PKCS7 类创建数字签名并加载 PFX 文件。此 PFX 文件包含您的证书和私钥，它们是签署文档所必需的。

```csharp
// .pfx 文件的路径
string pfxFile = "YOUR DOCUMENTS DIRECTORY\\certificate.pfx";

// 初始化签名对象
PdfFileSignature signature = new PdfFileSignature(document);

// 使用密码加载 PFX 文件
PKCS7 pkcs = new PKCS7(pfxFile, "pfx_password");
```

此时，您正在告诉 Aspose 使用您的数字证书来签署文档。 `PKCS7` 对象为您处理所有加密工作，因此您不必担心细节。

## 步骤3：添加时间戳设置

时间戳是可靠数字签名的关键组成部分之一。它确保即使证书过期，文档的签名也能被验证。让我们使用在线时间戳机构来设置时间戳。

```csharp
// 定义时间戳设置
TimestampSettings timestampSettings = new TimestampSettings("https://您的时间戳网址”，“用户名：密码”）；

// 向 PKCS7 对象添加时间戳设置
pkcs.TimestampSettings = timestampSettings;
```

这里，您需要指定时间戳服务的 URL，该服务将自动为您的签名提供时间和日期。此操作可以在有或无身份验证的情况下完成。

## 步骤 4：定义签名位置和外观

现在，我们将定义签名在 PDF 中的显示位置及其尺寸。您可以自定义签名框在页面上的位置和大小。

```csharp
// 定义签名的外观和位置（第 1 页，指定矩形）
System.Drawing.Rectangle rect = new System.Drawing.Rectangle(100, 100, 200, 100);
```

在这里，我们定义一个矩形，将签名定位在 PDF 第一页的坐标 (100, 100) 处，宽度为 200，高度为 100。您可以更改这些值以适合您的设计。

## 步骤5：签署PDF文档

一切设置完毕后，就该将数字签名实际应用于 PDF 了。此步骤将证书、时间戳和定位合并到一个简单的命令中。

```csharp
// 在文件第一页上签名
signature.Sign(1, "Signature Reason", "Contact", "Location", true, rect, pkcs);
```

以下是正在发生的事情：
- 1：这表示签名应应用于第一页。
- “签名原因”：您可以在此处指定签署文件的原因。
- “联系方式”：输入签名人的联系方式。
- “地点”：指定签名者的位置。
- true：此布尔值表示签名是否在文档中可见。
- rect：我们之前定义的矩形，指定了签名的大小和位置。
- pkcs：PKCS7 对象包含数字证书和时间戳设置。

## 步骤 6：保存签名的 PDF

文档签名完成后，只需保存即可。您可以选择新的文件名，以便同时保留原始版本和签名版本。

```csharp
// 保存签名的 PDF 文档
signature.Save(dataDir + "DigitallySignWithTimeStamp_out.pdf");
```

您新签名并带有时间戳的 PDF 现已保存到指定目录！

## 结论

就这样！您已成功使用 Aspose.PDF for .NET 对 PDF 进行数字签名，并添加了时间戳。此过程可确保文档的真实性和完整性，让您和收件人都安心无虞。在当今的数字世界中，数字签名变得越来越重要，因此掌握此过程绝对是一项值得掌握的技能。

## 常见问题解答

### 我可以使用不同的证书文件格式吗？  
是的，但本教程重点介绍如何使用 PFX 文件，这是最常见的数字证书格式。

### 我需要互联网连接来应用时间戳吗？  
是的，由于时间戳是从在线时间戳机构获取的，因此您需要互联网访问。

### 我可以在 PDF 中的多个页面进行签名吗？  
当然！您可以修改 `signature.Sign()` 方法定位多个页面或循环遍历所有页面。

### 如果 PFX 文件密码不正确会发生什么？  
如果密码错误，您将收到异常，因此请确保密码输入正确。

### 我可以让签名不可见吗？  
是的，您可以通过 `false` 到 `Sign` 方法的可见性参数使签名不可见。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}