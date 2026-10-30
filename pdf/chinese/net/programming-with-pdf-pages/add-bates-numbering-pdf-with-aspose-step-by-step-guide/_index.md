---
category: general
date: 2026-08-08
description: 使用 Aspose.Pdf 在 C# 中为 PDF 添加 Bates 编号。本教程还展示了如何添加空白页 PDF 并以编程方式生成 PDF。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering pdf
- add blank page pdf
- generate pdf programmatically
- create pdf aspose
language: zh
lastmod: 2026-08-08
og_description: 使用 Aspose.Pdf 在 C# 中为 PDF 添加 Bates 编号。学习如何添加空白页 PDF、以编程方式生成 PDF，并在几分钟内保存最终文档。
og_image_alt: Screenshot of C# code adding Bates numbering and a blank page to a PDF
  using Aspose.Pdf
og_title: 使用 Aspose 为 PDF 添加贝茨编号 – 完整 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  headline: Add bates numbering pdf with Aspose – step‑by‑step guide
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  name: Add bates numbering pdf with Aspose – step‑by‑step guide
  steps:
  - name: What if I need a different font or position?
    text: 'The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`,
      `HorizontalAlignment`, and `VerticalAlignment`. For example:'
  - name: How do I exclude a specific page from numbering?
    text: Create a separate `BatesNumberingArtifact` for the pages you want to number
      and add it only to those pages. Pages without an attached artifact will remain
      unnumbered.
  - name: Does this work with existing PDFs?
    text: 'Yes. Instead of `new Document()`, load an existing file:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF generation
- Bates numbering
title: 使用 Aspose 为 PDF 添加贝茨编号 – 步骤指南
url: /zh/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose 为 PDF 添加 Bates 编号 – 步骤指南

一旦了解核心步骤，使用 Aspose.Pdf 为 PDF 添加 Bates 编号就非常简单。如果你还需要添加空白页 PDF 或以编程方式生成 PDF，本指南将涵盖所有必要内容。

在本教程中，你将：

* 从头创建一个新的 PDF 文档。  
* 添加一个将承载 Bates 编号的空白页 PDF。  
* 使用自定义前缀配置 Bates 编号工件。  
* 保存 PDF，使编号显示在生成的文件中。  

完成后，你将拥有一个完整的 C# 控制台应用程序，生成的 PDF 将包含类似 **CASE‑1000**、**CASE‑1001**、… 的 Bates 编号——这是法律和电子发现工作流中的常见需求。

## 前置条件

* .NET 6.0 SDK 或更高版本（代码同样适用于 .NET Framework 4.8）。  
* Visual Studio 2022 或任意支持 C# 的 IDE。  
* 有效的 Aspose.Pdf for .NET 许可证（或免费评估密钥）。  
* 对 C# 语法有基本了解。

> **专业提示：** 如果在没有许可证的情况下运行代码，Aspose 会在输出的 PDF 上添加一个小水印。

## 步骤 1：设置项目并导入 Aspose.Pdf

创建一个新的控制台项目并添加 Aspose.Pdf NuGet 包：

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

示例所需的 `using` 指令如下：

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
```

这些命名空间为你提供对后续使用的 `Document`、`Page` 和 `BatesNumberingArtifact` 类的访问权限。

## 步骤 2：添加空白页 PDF

Bates 编号必须附加到页面上，因此我们首先创建一个将接收编号工件的空白页。

```csharp
// Step 2: Add a blank page pdf
Document pdfDocument = new Document();          // creates an empty PDF
Page pdfPage = pdfDocument.Pages.Add();         // adds the first (blank) page
```

`Document` 类代表整个 PDF 文件，而 `Pages.Add()` 会在文档的页面集合末尾插入一个新的空白页。由于文档最初为空，此调用也会创建第一页面。

## 步骤 3：配置 Bates 编号工件

现在我们定义 Bates 编号的显示方式。`BatesNumberingArtifact` 允许你设置起始编号、前缀、后缀以及格式选项。

```csharp
// Step 3: Define Bates numbering settings
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
{
    StartNumber = 1000,          // first number in the sequence
    Prefix = "CASE-",            // custom prefix before each number
    // Optional: you can also set Suffix, FontSize, FontColor, etc.
};
```

**为什么重要：**  
将 `StartNumber` 设置为 **1000** 符合典型的法律案件文件惯例。`Prefix` 确保每个编号显示为 **CASE‑1000**、**CASE‑1001**、…，便于搜索和排序。

## 步骤 4：将工件附加到页面

必须将工件添加到页面的 `Artifacts` 集合中，这样 Aspose 在保存时会在每页上渲染它。

```csharp
// Step 4: Attach the Bates numbering artifact to the PDF page
pdfPage.Artifacts.Add(batesArtifact);
```

当文档保存时，Aspose 会自动在所有页面上重复该工件，并为每个后续页面递增编号。

## 步骤 5：（可选）添加更多页面

如果需要更多页面，只需重复 `pdfDocument.Pages.Add()`。在上一步中附加的 Bates 编号工件会自动出现在每个新页面上。

```csharp
// Example: add two more pages
pdfDocument.Pages.Add();
pdfDocument.Pages.Add();
```

## 步骤 6：保存 PDF – 以编程方式生成 PDF

最后，将文档持久化到磁盘。此时 Bates 编号会被渲染到页面上。

```csharp
// Step 6: Save the PDF – generate pdf programmatically
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumberedDocument.pdf");

// Ensure the directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);

pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to: {outputPath}");
```

**预期结果：**  
打开 *BatesNumberedDocument.pdf*，你会看到一个三页的 PDF。每页右下角显示 Bates 编号：

* 第 1 页 → **CASE‑1000**  
* 第 2 页 → **CASE‑1001**  
* 第 3 页 → **CASE‑1002**

由于工件已附加到页面集合，编号会自动递增。

## 完整、可运行的示例

将所有内容整合在一起，下面是一个完整的控制台程序，你可以复制、粘贴并运行：

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new PDF document
            Document pdfDocument = new Document();

            // Add a blank page pdf
            Page pdfPage = pdfDocument.Pages.Add();

            // Define Bates numbering settings (add bates numbering pdf)
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
            {
                StartNumber = 1000,
                Prefix = "CASE-"
            };

            // Attach the artifact to the page
            pdfPage.Artifacts.Add(batesArtifact);

            // (Optional) add more pages to see incremented numbers
            pdfDocument.Pages.Add(); // page 2
            pdfDocument.Pages.Add(); // page 3

            // Save the PDF – generate pdf programmatically
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "BatesNumberedDocument.pdf");

            Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);
            pdfDocument.Save(outputPath);

            Console.WriteLine($"PDF saved to: {outputPath}");
        }
    }
}
```

使用 `dotnet run` 运行程序。执行完毕后，在桌面上找到生成的文件并验证 Bates 编号。

![添加 Bates 编号 PDF 示例](/images/bates-numbering.png "添加 Bates 编号 PDF 示例")

## 常见问题与边缘情况

### 如果需要不同的字体或位置怎么办？

`BatesNumberingArtifact` 提供了 `FontSize`、`FontColor`、`HorizontalAlignment` 和 `VerticalAlignment` 等属性。例如：

```csharp
batesArtifact.FontSize = 12;
batesArtifact.FontColor = Color.Blue;
batesArtifact.HorizontalAlignment = HorizontalAlignment.Left;
batesArtifact.VerticalAlignment = VerticalAlignment.Top;
```

### 如何排除特定页面的编号？

为需要编号的页面创建单独的 `BatesNumberingArtifact`，仅将其添加到这些页面。未附加工件的页面将保持不编号。

### 这能用于已有的 PDF 吗？

可以。将 `new Document()` 替换为加载已有文件的方式：

```csharp
Document pdfDocument = new Document("input.pdf");
```

然后将工件附加到目标页面并保存。

## 结论

现在你已经掌握了如何使用 Aspose.Pdf **为 PDF 添加 Bates 编号**、**添加空白页 PDF**，以及 **以编程方式生成 PDF** 的完整、可复用的 C# 解决方案。该方法适用于任意页数、自定义前缀和样式选项，让你对最终文档拥有完整控制权。

接下来你可以探索：

* 使用 **create pdf as


## 接下来该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并在项目中探索替代实现方式，每篇资源均提供完整的可运行代码示例和逐步解释。

- [如何使用 Aspose.PDF for .NET 为 PDF 添加和自定义页码 | 文档操作指南](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [如何使用 Aspose.PDF for .NET 在 PDF 末尾添加空白页 | 步骤指南](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)
- [使用 Aspose.PDF 创建 PDF 文档 – 添加页面、形状并保存](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}