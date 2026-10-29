---
category: general
date: 2026-07-14
description: 使用 Aspose.Pdf 将 PDF 保存为 HTML —— 学习如何创建 PDF 文档、添加矩形形状到 PDF，并导出为不含图片的干净
  HTML。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save pdf as html
- how to create pdf document
- add rectangle shape pdf
language: zh
lastmod: 2026-07-14
og_description: 使用 Aspose.Pdf 将 PDF 保存为 HTML。了解如何创建 PDF 文档、绘制矩形形状 PDF，并在几分钟内生成不含图像的
  HTML。
og_image_alt: Screenshot of a PDF saved as HTML showing a rectangle shape
og_title: 将 PDF 保存为 HTML – 快速指南：创建 PDF 并添加矩形形状
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Save PDF as HTML using Aspose.Pdf – learn how to create PDF document,
    add rectangle shape PDF, and export to clean HTML without images.
  headline: Save PDF as HTML – Create PDF, add rectangle shape
  type: TechArticle
tags:
- pdf
- aspnet
- csharp
- html-export
title: 将 PDF 保存为 HTML – 创建 PDF，添加矩形形状
url: /zh/net/conversion-export/save-pdf-as-html-create-pdf-add-rectangle-shape/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将 PDF 保存为 HTML – 创建 PDF，添加矩形形状

是否曾想过在 **将 PDF 保存为 HTML** 的同时还能在源 PDF 上绘制图形？你并不是唯一有此需求的人。在许多内部工具中，我们需要一个干净的 PDF HTML 预览，其中包含自定义形状，而常规转换器要么嵌入庞大的光栅图像，要么完全去除矢量数据。

在本教程中，我们将演示 **如何使用 Aspose.Pdf 编程创建 PDF 文档**，绘制 **矩形形状 PDF**，配置 Bates 编号，最后 **将 PDF 保存为 HTML** 并省略光栅图像。完成后，你将拥有一个可直接运行的 C# 控制台应用程序，生成的 HTML 文件可在任意浏览器打开——无需额外的图像文件。

> **专业提示：** Aspose.Pdf 支持 .NET 6+、.NET Framework 4.6+ 以及 .NET Core，因而可以轻松嵌入到传统的 Windows 服务或全新的微服务中。

---

## 前置条件

- **Visual Studio 2022**（Community 或更高版本）或任何支持 C# 的 IDE。  
- **Aspose.Pdf for .NET** NuGet 包（版本 23.11 或更高）。通过包管理器控制台安装：

```powershell
Install-Package Aspose.Pdf
```

- 对 C# 语法有基本了解；无需 PDF 相关经验。

---

## 使用 Aspose.Pdf 将 PDF 保存为 HTML

下面是完整的、可直接复制粘贴的代码。它遵循原始片段的所有步骤，并添加了注释、错误处理以及一个小型辅助方法，以保持主流程的可读性。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

namespace PdfToHtmlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a fresh PDF document.
            Document pdfDoc = new Document();
            Page pdfPage = pdfDoc.Pages.Add();

            // 2️⃣ Draw a rectangle shape on the page.
            //    This demonstrates the "add rectangle shape pdf" requirement.
            var rectangle = new Rectangle(100, 500, 300, 700)
            {
                // Optional visual tweaks
                FillColor = Color.GetYellow(),
                Border = new Border
                {
                    Width = 2,
                    Color = Color.GetRed()
                }
            };
            pdfPage.Paragraphs.Add(rectangle);
            pdfPage.ValidateGraphicsState(); // Ensures the shape fits within page bounds

            // 3️⃣ Configure Bates numbering – useful for legal documents.
            var bates = new BatesNumbering { StartNumber = 1, Prefix = "DOC-" };
            pdfDoc.BatesNumbering = bates;

            // 4️⃣ Add a tagged element with an explicit position.
            //    Tagging is important for accessibility (PDF/UA).
            var taggedElement = new TagStructure();
            taggedElement.PositionSettings = new TagPositionSettings { X = 150, Y = 600 };
            pdfPage.TagStructure.Add(taggedElement);

            // 5️⃣ Enable detection of compromised signatures.
            pdfDoc.SecurityOptions.DetectCompromisedSignatures = true;
            bool hasCompromisedSignature = pdfDoc.SecurityOptions.HasCompromisedSignature;
            Console.WriteLine($"Compromised signature? {hasCompromisedSignature}");

            // 6️⃣ Finally, save the PDF as HTML *without* embedding raster images.
            var htmlOptions = new HtmlSaveOptions
            {
                SkipImages = true,               // Removes <img> tags for raster data
                FixedLayout = true,              // Preserves the original page layout
                ExportEmbeddedFonts = false      // Keeps the HTML lightweight
            };

            string outputPath = @"output.html";
            pdfDoc.Save(outputPath, htmlOptions);
            Console.WriteLine($"✅ PDF successfully saved as HTML at: {outputPath}");
        }
    }
}
```

### 代码逐步说明

| 步骤 | 为什么重要 |
|------|------------|
| **创建 PDF 文档** | 这是基础——没有 `Document` 对象就无法添加任何内容。 |
| **添加矩形形状 PDF** | 演示矢量绘图；矩形是最简单的形状，同一 API 还能绘制圆形、多边形等。 |
| **配置 Bates 编号** | 在诉讼或批处理场景中常需为每页分配唯一标识。 |
| **标签结构** | 提升可访问性；屏幕阅读器依赖标签来传达阅读顺序。 |
| **检测受损签名** | 安全敏感的应用需要知道数字签名是否被篡改。 |
| **将 PDF 保存为 HTML** | 最终目标——生成与 PDF 布局相匹配且不包含庞大图像文件的干净 HTML。 |

> **为什么要 `SkipImages = true`？**  
> 当转换包含矢量图形（如我们的矩形）的 PDF 时，通常不需要光栅回退。将 `SkipImages` 设置为 true 会去除 `<img>` 元素及其对应的 base‑64 数据，使 HTML 文件保持在几千字节以内。

---

## 如何使用 Aspose.Pdf 创建 PDF 文档

如果你是 Aspose 新手，该库对待 PDF 的方式类似于 Word 文档：先 **添加页面**，再向页面中加入 **段落**、**形状** 或 **批注**。`Document` 类是入口点，每个 `Page` 都拥有一个名为 `Paragraphs` 的集合。任何继承自 `TextFragmentAbsorber`、`Image`、`Rectangle` 等的对象都可以插入该集合。

下面是仅创建空白 PDF 的最小代码片段——在需要从零开始时非常有用：

```csharp
Document emptyPdf = new Document();
Page firstPage = emptyPdf.Pages.Add();   // Adds a default‑size A4 page
emptyPdf.Save("empty.pdf");
```

你可以使用简单的 `for` 循环链式添加更多页面，或通过 `PageInfo` 设置页面级属性（如边距、尺寸）。正是这种灵活性使得 Aspose.Pdf 成为服务器端 PDF 生成的首选。

---

## 添加矩形形状 PDF – 绘制图形

`Rectangle` 类位于 `Aspose.Pdf.Annotations` 命名空间。它接受四个坐标：**左下 X**、**左下 Y**、**右上 X**、**右上 Y**。可以把 PDF 坐标系想象成

## 接下来你应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并在项目中探索替代实现方式。每篇资源均提供完整可运行的代码示例和逐步解释。

- [使用 Aspose.PDF 创建 PDF 文档 – 添加页面、形状并保存](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [使用 Aspose.PDF 在 .NET 中将 PDF 转换为 HTML（不保存图像）](/pdf/english/net/conversion-export/convert-pdf-html-net-asposepdf-no-images/)
- [使用 Aspose.PDF .NET 将 PDF 转换为 HTML：将图像保存为外部 PNG](/pdf/english/net/conversion-export/pdf-to-html-conversion-external-png-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}