---
category: general
date: 2026-10-10
description: 了解如何使用 Aspose.PDF 将 PDF 保存为 HTML，跳过光栅图像。本指南涵盖将 PDF 转换为 HTML 并高效地将文档保存为
  HTML。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save pdf as html
- convert pdf to html
- aspose pdf to html
- save pdf without images
- save document as html
language: zh
lastmod: 2026-10-10
og_description: 使用 Aspose.PDF 将 PDF 保存为 HTML，同时跳过光栅图像。请按照本完整教程将 PDF 转换为 HTML 并将文档保存为
  HTML。
og_image_alt: Screenshot showing PDF saved as HTML without images using Aspose.PDF
og_title: 将 PDF 保存为无图像的 HTML – Aspose.PDF 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to save PDF as HTML with Aspose.PDF, skipping raster images.
    This guide covers convert PDF to HTML and save document as HTML efficiently.
  headline: How to save PDF as HTML without images using Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- HTML conversion
title: 如何使用 Aspose.PDF 将 PDF 保存为不含图像的 HTML
url: /zh/net/document-conversion/how-to-save-pdf-as-html-without-images-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.PDF 将 PDF 保存为不含图像的 HTML

如果您需要在省略所有光栅图形的情况下 **save PDF as HTML**，本教程将一步步演示。通过配置 `HtmlSaveOptions`，您可以高效地将 PDF 转换为 HTML，并保持输出轻量——非常适合面向网页的文档或 SEO 优化的页面。

除了去除图像外，指南还演示了更广泛的 **convert PDF to HTML** 工作流，使您最终得到一个干净的 HTML 文件，保留文本、矢量图形和布局。无需外部工具；所有操作都在标准 .NET 项目中完成。

## 前提条件

在开始之前，请确保您拥有：

* .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.6+）
* 有效的 Aspose.PDF for .NET 许可证（或免费评估密钥）
* 位于已知目录的输入 PDF 文件
* Visual Studio 2022（或任意 C# IDE）

这些项目足以编译并运行后面示例代码。

## 第一步：安装 Aspose.PDF NuGet 包

您首先需要将 Aspose.PDF 库添加到项目中：

```bash
dotnet add package Aspose.PDF
```

运行此命令会恢复最新的稳定版 Aspose.PDF，其中包含转换所需的 `HtmlSaveOptions` 类。

## 第二步：加载源 PDF 文档

使用 `Document` 类加载 PDF 非常简单。该类在内存中表示整个 PDF 文件。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Saving;

// Step 2: Load the source PDF document
Document doc = new Document(@"C:\MyFiles\input.pdf");
```

*此步骤的重要性：*  
`Document` 解析 PDF 结构，提供对页面、字体和资源的访问。若未先加载文件，则无法应用任何保存选项。

## 第三步：配置 HTML 保存选项以跳过光栅图像

`HtmlSaveOptions` 对象允许您细致调节 HTML 输出。将 `SkipRasterImages` 设置为 `true` 可指示 Aspose.PDF 在转换过程中忽略所有位图图像（JPEG、PNG、GIF）。

```csharp
// Step 3: Configure HTML save options to skip raster images
HtmlSaveOptions htmlOpts = new HtmlSaveOptions
{
    // Exclude all raster (bitmap) images from the output HTML
    SkipRasterImages = true,

    // Optional: embed fonts as Base64 to avoid external font files
    EmbedFonts = true,

    // Optional: preserve the original layout as closely as possible
    FixedLayout = true
};
```

*此步骤的重要性：*  
光栅图像通常占据文件大小的大部分。跳过它们可生成更轻量的 HTML 文件，加载更快，并且更易于搜索引擎索引。额外的选项（`EmbedFonts`、`FixedLayout`）仅作完整展示；它们并非图像移除所必需。

## 第四步：将文档保存为不含图像的 HTML

现在您可以将转换后的内容写入磁盘。`Save` 重载接受目标路径、所需的 `SaveFormat`，以及前面配置的选项。

```csharp
// Step 4: Save the document as HTML without raster images
doc.Save(@"C:\MyFiles\no_images.html", SaveFormat.Html, htmlOpts);
```

调用完成后，`no_images.html` 包含文本内容、矢量形状和 CSS，能够重建原始 PDF 布局——不包含任何位图图像。

### 预期输出

在浏览器中打开 `no_images.html`。您应看到：

* 原始 PDF 中的所有标题、段落和表格。
* 矢量图形（例如 SVG 形状）正确渲染。
* 没有引用光栅文件的 `<img>` 标签；这些标签已完全省略。

如果检查 HTML 源码，您会发现缺少 `<img src="...">` 元素，证明 `SkipRasterImages` 已按预期工作。

## 完整、可运行的示例

下面是一个独立的控制台应用程序，整合了所有步骤。将代码复制到新的 .NET 控制台项目中并运行。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Saving;

namespace PdfToHtmlNoImages
{
    class Program
    {
        static void Main(string[] args)
        {
            // Input and output paths – adjust to your environment
            string inputPath = @"C:\MyFiles\input.pdf";
            string outputPath = @"C:\MyFiles\no_images.html";

            // 1. Load the PDF document
            Document doc = new Document(inputPath);
            Console.WriteLine($"Loaded PDF: {inputPath}");

            // 2. Set up HTML save options to omit raster images
            HtmlSaveOptions htmlOpts = new HtmlSaveOptions
            {
                SkipRasterImages = true,
                EmbedFonts = true,
                FixedLayout = true
            };
            Console.WriteLine("Configured HtmlSaveOptions to skip raster images.");

            // 3. Save as HTML
            doc.Save(outputPath, SaveFormat.Html, htmlOpts);
            Console.WriteLine($"PDF saved as HTML without images at: {outputPath}");
        }
    }
}
```

**运行程序** 会在控制台打印进度信息并生成 `no_images.html`。通过在任意现代浏览器中打开该文件进行验证。

## 常见变体和边缘情况

| 情况 | 如何调整代码 |
|-----------|-----------------------|
| **保留光栅图像** | 将 `SkipRasterImages = false`（或省略该属性）。 |
| **仅转换页面范围** | 在保存前使用 `doc.Pages.Delete(pageNumber)` 删除不需要的页面，或设置 `htmlOpts.PageIndex` 和 `htmlOpts.PageCount`。 |
| **将每个 PDF 页面保存为单独的 HTML 文件** | 将 `htmlOpts.SplitIntoPages = true`；库将生成 `output_page1.html`、`output_page2.html` 等文件。 |
| **压缩生成的 HTML** | 保存后，对文件运行压缩工具，或将 `htmlOpts.Compress = true`（在新版 Aspose 中可用）。 |
| **处理受密码保护的 PDF** | 在 `Document` 构造函数中传入密码：`new Document(inputPath, new LoadOptions { Password = "secret" })`。 |

这些变体让您能够将 **aspose pdf to html** 转换定制到各种实际场景。

## 专业技巧

* **尽早授权** – 在加载文档前注册 Aspose.PDF 许可证，以避免评估水印。  
* **性能** – 对于大型 PDF，复用同一个 `HtmlSaveOptions` 实例，并考虑启用 `htmlOpts.UseZOrder = true`，以加速重叠元素的渲染。  
* **测试** – 对比有无图像的 HTML 文件大小，以量化 `SkipRasterImages` 的收益。

## 结论

现在您已经了解如何使用 Aspose.PDF for .NET **save PDF as HTML** 并去除光栅图形。完整流程——加载 PDF、使用 `SkipRasterImages` 配置 `HtmlSaveOptions`，然后保存结果——涵盖了基本的 **convert PDF to HTML** 用例，并可扩展至页面范围转换、逐页输出或其他优化。

接下来，您可以探索使用嵌入 CSS 的 **save document as HTML**，或尝试 `SvgSaveOptions` 类生成可缩放矢量图形（SVG）而非 HTML。这两种方法都能进一步减小文件体积并提升现代 Web 应用的响应性。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术密切相关的主题，帮助您进一步学习。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方式。

- [在 .NET 中使用 Aspose.PDF 将 PDF 转换为 HTML（不保存图像）](/pdf/english/net/conversion-export/convert-pdf-html-net-asposepdf-no-images/)
- [使用 Aspose.PDF .NET 将 PDF 转换为 HTML：将图像保存为外部 PNG](/pdf/english/net/conversion-export/pdf-to-html-conversion-external-png-aspose-pdf-net/)
- [使用 Aspose.PDF 将 PDF 保存为 HTML – 快速 C# 指南](/pdf/english/net/conversion-export/save-pdf-as-html-with-aspose-pdf-quick-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}