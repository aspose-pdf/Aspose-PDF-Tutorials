---
category: general
date: 2026-08-04
description: 使用 Aspose.Pdf 在 C# 中快速创建新 PDF 文档并添加 Bates 编号——学习添加空白页 PDF 和自定义页码。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new pdf document
- add bates numbering pdf
- how to add bates
- add blank page pdf
- add custom page numbers
language: zh
lastmod: 2026-08-04
og_description: 在 C# 中创建新的 PDF 文档，并自动为法律案件管理添加 Bates 编号 PDF——包含完整代码示例。
og_image_alt: Screenshot of a C# program creating a PDF document with Bates numbers
  applied
og_title: 在 C# 中创建带 Bates 编号的 PDF 文档
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create new PDF document in C# and add Bates numbering pdf quickly using
    Aspose.Pdf – learn to add blank page pdf and custom page numbers.
  headline: Create new PDF document with Bates numbering in C#
  type: TechArticle
tags:
- C#
- PDF
- Aspose.Pdf
- Bates numbering
title: 使用 C# 创建带 Bates 编号的新 PDF 文档
url: /zh/net/document-creation/create-new-pdf-document-with-bates-numbering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 创建带 Bates 编号的 PDF 文档

如果您需要在 C# 中 **创建新 PDF 文档**，本指南将向您展示如何使用 Aspose.Pdf **添加 Bates 编号 PDF**。您将学习 **添加空白页 PDF**、配置 **自定义页码**，并保存最终文件。

本教程涵盖了从安装库到生成符合法律案件文件标准的 PDF 的每一步。完成后，您可以生成 PDF、插入空白页、应用 Bates 编号，并自定义编号格式——全部通过一个可运行的程序实现。

## 前置条件

在开始之前，请确保您拥有：

* .NET 6.0 SDK 或更高版本已安装  
* Visual Studio 2022（或任何 C# IDE）  
* 有效的 Aspose.Pdf for .NET 许可证或免费评估密钥  

您无需额外的 NuGet 包；教程会自动安装所有必需的依赖。

## 步骤 1：通过 NuGet 安装 Aspose.Pdf

在项目文件夹的终端中运行：

```bash
dotnet add package Aspose.Pdf
```

该命令会将最新的稳定版 Aspose.Pdf 添加到您的项目中，提供您将使用的 `Document`、`BatesNumbering` 等 PDF 操作类。

## 步骤 2：创建新 PDF 文档 – 初始设置

创建 PDF 文件是后续所有操作的基础。`Document` 类代表整个 PDF 容器。

```csharp
using Aspose.Pdf;

// Step 2: Create a new PDF document
using var doc = new Document();
```

*重要性说明*：实例化 `Document` 会分配页面、字体和图形所需的内部结构。使用 `using var` 可确保在保存后正确释放文件。

## 步骤 3：添加空白页 PDF

在向 PDF 中放置内容之前，必须至少包含一页。添加空白页可为 Bates 编号提供干净的画布。

```csharp
// Step 3: Add a blank page to the document
Page page = doc.Pages.Add();
```

`Pages.Add()` 方法会在文档的页面集合末尾追加一个新的空白页。如果以后需要在多页上 **添加自定义页码**，可以重复调用此方法以添加更多页面。

## 步骤 4：配置 Bates 编号 – 如何添加 Bates

Bates 编号是一种在法律文件中常用的顺序标识符。您可以通过 `BatesNumbering` 类进行配置。

```csharp
// Step 4: Set up Bates numbering options
var bates = new BatesNumbering
{
    StartNumber = 1000,      // Starting number for the sequence
    Prefix = "CaseA-",       // Text to prepend to each number
    Increment = 1,           // Increment between consecutive numbers
    // Optional: Set the location, font size, etc.
};
```

*重要性说明*：`StartNumber` 定义起始编号，`Prefix` 添加可读标签，`Increment` 控制递增步长。您还可以调整 `HorizontalAlignment`、`VerticalAlignment`、`FontSize` 和 `Margins`，以控制编号在每页上的显示效果。

## 步骤 5：将 Bates 编号 PDF 应用于页面

编号选项准备就绪后，将其应用到页面（或整个文档）。

```csharp
// Step 5: Apply the Bates numbering to the page
bates.Apply(page);
```

调用 `Apply` 默认会将格式化后的编号插入页面底部的页脚。如果需要将编号放在其他位置，请在调用 `Apply` 前设置 `bates.Position`。

## 步骤 6：保存已应用 Bates 编号的 PDF

最后，将内存中的文档写入磁盘。

```csharp
// Step 6: Save the PDF with Bates numbers applied
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumbered.pdf");

doc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

保存后的文件现在包含一页，底部显示 **CaseA-1000** 的 Bates 编号。使用任意 PDF 查看器打开即可验证编号是否正确。

## 预期输出

打开 `BatesNumbered.pdf` 时，您应看到：

* 一个空白页（如果您添加了更多页面，则会有更多）  
* 页面底部显示 **CaseA-1000** 文本（默认位置）  

如果您添加了更多页面并复用同一个 `BatesNumbering` 实例，编号会自动递增（CaseA-1001、CaseA-1002，……）。

## 专业提示：在 Bates 编号之外添加自定义页码

有时您需要同时拥有 Bates 编号和传统页码。可以在应用 Bates 编号后添加 `TextFragment` 来实现两者共存：

```csharp
// Add a traditional page number in the header
var pageNumber = new TextFragment($"Page {page.Number}")
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Top,
    FontSize = 12,
    Font = FontRepository.FindFont("Arial")
};
page.Paragraphs.Add(pageNumber);
```

此代码片段演示了在保留 Bates 标签的同时 **添加自定义页码**。

## 边缘情况：将 Bates 编号应用于多个页面

如果文档包含多页，您可以在循环中将同一个 `BatesNumbering` 实例应用到每一页：

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    bates.Apply(doc.Pages[i]);
}
```

循环确保每页根据您定义的 `StartNumber` 和 `Increment` 获得顺序编号。

## 常见陷阱及避免方法

| 问题 | 原因 | 解决方案 |
|-------|----------------|-----|
| 数字居中偏移 | 默认对齐可能与布局不匹配 | 显式设置 `bates.HorizontalAlignment` 和 `bates.VerticalAlignment` |
| 数字覆盖现有内容 | 未定义边距 | 调整 `bates.Margin` 或使用 `bates.Position` 移动数字 |
| 运行时许可证异常 | 评估版限制输出 | 在创建文档前应用有效的 Aspose.Pdf 许可证 (`License license = new License(); license.SetLicense("Aspose.Pdf.lic");`) |

## 完整工作示例

下面是一个可直接复制、粘贴并运行的完整程序示例。

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1. Create a new PDF document
        using var doc = new Document();

        // 2. Add a blank page pdf
        Page page = doc.Pages.Add();

        // 3. Configure Bates numbering – how to add bates
        var bates = new BatesNumbering
        {
            StartNumber = 1000,
            Prefix = "CaseA-",
            Increment = 1,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(20, 20, 20, 20),
            FontSize =


## 接下来您应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助您进一步掌握 API 的其他功能，并在自己的项目中探索替代实现方案。每个资源都提供完整的可运行代码示例和逐步说明。

- [如何在 Aspose.PDF for .NET 中添加和自定义 PDF 页码 | 文档操作指南](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF .NET：使用 FloatingBox 为 PDF 添加页码](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [使用 Aspose.PDF 创建 PDF 文档 – 添加页面、形状并保存](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}