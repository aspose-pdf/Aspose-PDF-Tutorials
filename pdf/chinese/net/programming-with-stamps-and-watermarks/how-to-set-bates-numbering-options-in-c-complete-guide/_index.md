---
category: general
date: 2026-08-14
description: 如何在 C# 中使用 GroupDocs 设置 Bates 编号选项。请按照本分步教程，在将 Word 转换为 PDF 时添加自定义前缀和起始编号。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set bates numbering options
- Bates numbering C#
- GroupDocs API
- document conversion C#
- AddBatesNumbering method
- C# PDF generation
language: zh
lastmod: 2026-08-14
og_description: 如何快速在 C# 中设置 Bates 编号选项。本指南展示了在将 Word 转换为 PDF 时，如何添加自定义前缀和起始编号。
og_image_alt: Screenshot of C# code applying Bates numbering to a PDF
og_title: 如何在 C# 中设置 Bates 编号选项——一步一步教程
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  headline: How to set bates numbering options in C# – complete guide
  type: TechArticle
- description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  name: How to set bates numbering options in C# – complete guide
  steps:
  - name: '`Document` – loads the source file.'
    text: '`Document` – loads the source file.'
  - name: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
    text: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
  - name: '`AddBatesNumbering` – the method that injects the numbering into each page.'
    text: '`AddBatesNumbering` – the method that injects the numbering into each page.'
  type: HowTo
tags:
- Bates numbering
- C#
- .NET
- GroupDocs
- PDF conversion
title: 如何在 C# 中设置 Bates 编号选项——完整指南
url: /zh/net/programming-with-stamps-and-watermarks/how-to-set-bates-numbering-options-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中设置 Bates 编号选项 – 完整指南

如果你需要 **如何在 C# 中设置 Bates 编号选项**，本指南将一步步带你完成。你将学习如何配置起始编号、添加前缀，以及在使用 GroupDocs API 将 Word 文档转换为 PDF 时应用编号。

文档处理常常需要在每页上添加唯一标识，以满足法律或归档需求。完成本教程后，你将拥有一个可复用的代码片段，能够直接嵌入任何 .NET 项目，无论是构建诉讼支持工具还是自动化报告生成器。无需外部工具——只需 GroupDocs.Conversion 库和几行 C# 代码。

## 所需环境

在开始之前，请确保你具备以下条件：

* 已安装 .NET 6.0 SDK 或更高版本  
* Visual Studio 2022（或任何支持 .NET 的 IDE）  
* 有效的 GroupDocs.Conversion 许可证（免费试用可用于测试）  
* 一个需要编号的示例 Word 文档（`input.docx`）  

这些前置条件可确保代码在无需额外配置的情况下运行。

## 如何设置 Bates 编号选项 – 概览

**如何设置 Bates 编号选项** 的核心在于三个对象：

1. `Document` – 加载源文件。  
2. `BatesNumberingOptions` – 保存起始编号、前缀以及其他格式细节。  
3. `AddBatesNumbering` – 将编号注入每一页的方法。

了解每个组成部分的作用，有助于你在更复杂的场景中进行适配，例如自定义字体或多语言编号。

## 步骤 1：安装 GroupDocs.Conversion NuGet 包

在解决方案文件夹的终端中运行：

```bash
dotnet add package GroupDocs.Conversion
```

**GroupDocs API** 提供了后续教程中使用的 `Document` 类和 `AddBatesNumbering` 扩展方法。

## 步骤 2：加载源文档

```csharp
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;

// Step 2: Load the source Word document
Document document = new Document(@"C:\Docs\input.docx");
```

*为什么需要这一步？*  
加载文件会在内存中创建一个可供转换引擎操作的表示。没有 `Document` 实例，你无法应用 Bates 编号或进行其他转换。

## 步骤 3：创建 Bates 编号选项

```csharp
// Step 3: Configure Bates numbering
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // The first page will be numbered 1000
    StartNumber = 1000,
    // Each page will be prefixed with "CASE-"
    Prefix = "CASE-",
    // Optional: set the number format (e.g., 4 digits)
    NumberFormat = "#0000",
    // Optional: choose where the number appears (header/footer)
    Position = BatesNumberingPosition.FooterRight
};
```

*为什么需要这一步？*  
`BatesNumberingOptions` 封装了在 **设置 Bates 编号选项** 时可能需要的所有设置。调整 `StartNumber` 和 `Prefix` 可以让输出与案件管理系统保持一致。`Position` 属性控制视觉位置，通常是合规要求。

## 步骤 4：将 Bates 编号应用到文档

```csharp
// Step 4: Apply the numbering to every page
document.AddBatesNumbering(batesOptions);
```

`AddBatesNumbering` 方法会遍历已加载的 `Document` 的每一页，并插入配置好的字符串。由于该方法在内存表示上工作，你可以在保存之前链式调用其他处理步骤（例如添加水印）。

## 步骤 5：转换并保存为 PDF

```csharp
// Step 5: Define PDF conversion options (optional)
PdfConvertOptions pdfOptions = new PdfConvertOptions
{
    // Preserve original layout
    EmbedStandardFonts = true
};

// Save the numbered document as PDF
document.Save(@"C:\Docs\output.pdf", pdfOptions);
```

*为什么需要这一步？*  
PDF 是法律文档的常见最终格式。`PdfConvertOptions` 对象可用于微调输出，但对基本编号并非必需。`Save` 调用会将完整编号的 PDF 写入磁盘。

## 完整可运行示例

将所有代码整合在一起，下面是一个可自行编译运行的控制台应用程序：

```csharp
using System;
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;
using GroupDocs.Conversion.Options.Convert.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the source Word document
            Document document = new Document(@"C:\Docs\input.docx");

            // Configure Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1000,
                Prefix = "CASE-",
                NumberFormat = "#0000",
                Position = BatesNumberingPosition.FooterRight
            };

            // Apply numbering to each page
            document.AddBatesNumbering(batesOptions);

            // Optional: set PDF conversion preferences
            PdfConvertOptions pdfOptions = new PdfConvertOptions
            {
                EmbedStandardFonts = true
            };

            // Save the numbered PDF
            document.Save(@"C:\Docs\output.pdf", pdfOptions);

            Console.WriteLine("Bates numbering applied successfully. Output saved to output.pdf");
        }
    }
}
```

**预期输出**

运行程序后会生成 `output.pdf`，每页都会显示类似 `CASE-1000`、`CASE-1001` 等标签，位于右下角页脚。使用任意 PDF 阅读器打开即可验证编号是否如预期显示。

## 常见问题与最佳实践

| 问题 | 产生原因 | 规避方法 |
|-------|----------------|-----------------|
| **相对路径导致 `FileNotFoundException`** | 控制台应用的工作目录可能与 Visual Studio 不同。 | 使用绝对路径或 `Path.Combine(AppContext.BaseDirectory, "input.docx")`。 |
| **编号覆盖了已有页脚** | 如果源文档在选定的页脚区域已有内容，新编号可能被遮挡。 | 更换 `Position`（例如 `HeaderLeft`）或调整源模板。 |
| **大文档处理缓慢** | Bates 编号会遍历每一页，文件越大内存占用越高。 | 使用 `Document.Split` 将文档分块处理，尤其在超过 500 页时。 |
| **许可证过期** | 免费试用版 30 天后会在 `AddBatesNumbering` 时抛出异常。 | 在加载文档前设置有效许可证：`License license = new License(); license.SetLicense("license.lic");`。 |

**小技巧：** 如果需要为不同案件使用不同的编号格式（例如 `2023-CASE-001`），可以在创建 `BatesNumberingOptions` 前动态生成前缀。

## 扩展方案

相同的 **Bates 编号 C#** 方法同样适用于 `.txt`、`.html` 或图像等其他源格式。只需在构造 `Document` 对象时更改文件扩展名，转换引擎会自动处理其余工作。

你还可以将 **文档转换 C#** 与 OCR 结合，用于扫描的 PDF：

```csharp
// Example: add OCR before numbering (requires GroupDocs.Viewer)
using GroupDocs.Viewer;
using GroupDocs.Viewer.Options;

Document scannedPdf = new Document(@"C:\Docs\scanned.pdf");
var viewer = new Viewer(scannedPdf);
var viewOptions = new HtmlViewOptions();
viewer.View(viewOptions); // OCR step
// Then apply Bates numbering as shown earlier
```

## 结论

现在，你已经掌握了在 C# 中 **如何设置 Bates 编号选项** 的完整流程。通过创建 `BatesNumberingOptions` 对象、使用 `AddBatesNumbering` 应用它，并将结果保存为 PDF，你可以实现合法合规、唯一标识的文档自动化生成。

接下来，你可以进一步探索 **C# PDF 生成**、**文档转换 C#** 或高级 **GroupDocs API** 功能，如水印和数字签名。尝试不同的前缀、位置和编号格式，以匹配你的工作流。

祝编码愉快！


## 接下来该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你在项目中进一步运用这些技巧。每篇资源都提供完整的可运行代码示例和逐步说明，帮助你掌握更多 API 功能并探索替代实现方式。

- [在 C# 中为 PDF 添加 Bates 编号 – 完整指南](/pdf/english/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/)
- [使用 Aspose.PDF for .NET 为 PDF 添加并自定义页码 | 文档操作指南](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [使用 Aspose.PDF for .NET 在 PDF 中添加文本戳脚注 – 步骤详解](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}