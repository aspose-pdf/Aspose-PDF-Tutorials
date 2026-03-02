---
category: general
date: 2026-01-02
description: 使用 Aspose.Pdf 在 C# 中快速为 PDF 添加页码。学习如何添加 Bates 编号、页脚文本、自定义水印，并在单个脚本中遍历
  PDF 页面。
draft: false
keywords:
- add page numbers pdf
- add bates numbering
- add footer text
- add custom watermark
- loop through pdf pages
language: zh
og_description: 使用 Aspose.Pdf 即时为 PDF 添加页码。本指南还涵盖了添加 Bates 编号、页脚文字、自定义水印以及遍历 PDF 页面。
og_title: 使用 C# 为 PDF 添加页码 – 完整编程教程
tags:
- C#
- Aspose.Pdf
- PDF manipulation
title: 使用 C# 为 PDF 添加页码 – 完整分步指南
url: /zh/net/programming-with-pdf-pages/add-page-numbers-pdf-with-c-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 为 PDF 添加页码 – 完整编程教程

是否曾经需要 **add page numbers pdf** 文件，却不知从何入手？你并不是唯一的——开发者们经常询问如何在 PDF 的每一页上添加页码、页脚，甚至是 Bates 风格的标识符。

在本教程中，你将看到一个可直接运行的 C# 示例，演示 **loops through pdf pages**，在页脚添加页码（如果需要），并可添加自定义水印。我们还会展示如何将印章切换为 Bates 编号，这其实就是为法律或取证文档“add bates numbering”。完成后，你将拥有一个单一、可复用的方法，轻松完成所有这些任务。

## Add page numbers pdf – 概述

在深入代码之前，让我们先弄清楚在 Aspose.Pdf 中 “add page numbers pdf” 实际指的是什么。该库将你在页面上放置的任何文本视为 **TextStamp**。只需创建一个带有页码占位符（`{page}`）的印章并将其应用到每一页，即可自动获得顺序编号。同一个印章还可以携带额外文本，从而 **add footer text** 如 “Confidential” 或特定案件标识。

> **为什么使用印章而不是编辑 PDF 内容流？**  
> 印章是高级对象，能够自动考虑页面边距、旋转以及已有的图形。它们也更易于维护——只需更改少量属性并重新运行脚本。

## Loop through PDF pages to apply stamps

第一步是打开源 PDF 并遍历其页面。这是大多数 Aspose 示例中常见的 **loop through pdf pages** 模式。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Paths – change these to match your environment
string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // The loop – every Page object lives in pdfDocument.Pages
    foreach (Page page in pdfDocument.Pages)
    {
        // We'll attach a stamp later (see next section)
    }

    // Save the modified document
    pdfDocument.Save(outputPdfPath);
}
```

> **专业提示：** 如果你的 PDF 很大（数百页），考虑分批处理以降低内存占用。Aspose.Pdf 会惰性加载页面，因此循环本身已经相当高效。

## Add bates numbering and footer text

现在我们可以逐页遍历了，接下来创建一个 **reusable TextStamp**，同时携带页码和可选的页脚文本。`{page}` 占位符会自动替换为当前页码。

```csharp
// Create a stamp that will be reused for every page
var batesStamp = new TextStamp("Bates-{page} – Confidential")
{
    // Position the stamp 20 points from the left and bottom edges
    XIndent = 20,
    YIndent = 20,
    // Align left‑bottom so it behaves like a traditional footer
    HorizontalAlignment = HorizontalAlignment.Left,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Font styling – Times New Roman, 10pt, bold, gray
    Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Gray }
};

// Attach the stamp to every page
foreach (Page page in pdfDocument.Pages)
    page.AddStamp(batesStamp);
```

### 为什么这样可行

* **`Bates-{page}`** – Aspose 会用实际页码替换 `{page}`，从而自动生成经典的 Bates 编号。  
* **`Confidential`** – 这就是 **add footer text** 部分。你可以替换为任意字符串，甚至从数据库中读取。  
* **样式** – 使用 `TextState` 可以在不触碰 PDF 内部内容流的情况下调整颜色、不透明度以及旋转角度。

如果只需要纯数字，去掉 “Bates‑” 前缀和额外文本即可：

```csharp
var simpleStamp = new TextStamp("{page}")
{
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    Font = new Font(FontFamily.Helvetica, 12, FontStyle.Regular),
    TextState = { ForegroundColor = Color.Black }
};
```

## Add a custom watermark (optional)

有时你需要的不止页脚——比如一个半透明的徽标或在整页上覆盖 “DRAFT”。这时 **add custom watermark** 就派上用场。只需重新设置 `TextStamp` 的对齐方式和不透明度即可。

```csharp
var watermark = new TextStamp("DRAFT")
{
    // Center it both horizontally and vertically
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Center,
    // Make it big and light
    Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Red, FontSize = 72, FontStyle = FontStyle.Bold, 
                  Transparency = 0.5f }   // 50% transparent
};

// Apply the watermark on top of the page‑number stamp
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(watermark);   // watermark on top
    page.AddStamp(batesStamp);  // then the footer
}
```

> **注意：** 顺序很重要。先添加水印可以确保页码在半透明文字之上保持可读。

## Save the PDF and verify results

完成印章后，最后一步是将更改写回磁盘。我们之前的 `Save` 调用已经完成了主要工作，这里再补充一个快速验证片段，打开新文件并打印处理的页数。

```csharp
pdfDocument.Save(outputPdfPath);

// Quick verification
using (var resultDoc = new Document(outputPdfPath))
{
    Console.WriteLine($"✅ Successfully added page numbers to {resultDoc.Pages.Count} pages.");
}
```

运行完整程序后，你应该会看到每页底部显示类似 **“Bates‑3 – Confidential”**（如果使用了简单印章，则只会显示 “3”），并且如果启用了水印，页面中间会出现淡淡的 “DRAFT”。

### 预期输出

| Page | Footer (example) |
|------|------------------|
| 1    | Bates‑1 – Confidential |
| 2    | Bates‑2 – Confidential |
| …    | … |
| N    | Bates‑N – Confidential |

如果在查看器中打开文件，页码会距左侧和底部边距 20 pts，符合常见的法律文档规范。

## Full working example (copy‑paste ready)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // ---------- Create the page‑number/footer stamp ----------
    var batesStamp = new TextStamp("Bates-{page} – Confidential")
    {
        XIndent = 20,
        YIndent = 20,
        HorizontalAlignment = HorizontalAlignment.Left,
        VerticalAlignment   = VerticalAlignment.Bottom,
        Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Gray }
    };

    // ---------- Optional watermark ----------
    var watermark = new TextStamp("DRAFT")
    {
        HorizontalAlignment = HorizontalAlignment.Center,
        VerticalAlignment   = VerticalAlignment.Center,
        Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Red, Transparency = 0.5f }
    };

    // ---------- Apply stamps to every page ----------
    foreach (Page page in pdfDocument.Pages)
    {
        page.AddStamp(watermark);   // comment out if you don't need a watermark
        page.AddStamp(batesStamp);
    }

    // ---------- Save and verify ----------
    pdfDocument.Save(outputPdfPath);
    Console.WriteLine($"✅ Added page numbers and watermark to {pdfDocument.Pages.Count} pages.");
}
```

将其保存为 `AddPageNumbers.cs`，恢复 Aspose.Pdf NuGet 包（`Install-Package Aspose.Pdf`），然后运行。你将得到一个 **add page numbers pdf** 文件，同时演示 **add bates numbering**、**add footer text**、**add custom watermark** 以及经典的 **loop through pdf pages** 模式——全部集中在一个整洁的脚本中。

![add page numbers pdf example](https://example.com/images/add-page-numbers-pdf.png "Screenshot showing numbered PDF pages with footer and watermark")

## Conclusion

我们已经完整展示了如何使用 Aspose.Pdf 在 C# 中 **add page numbers pdf**。从遍历每一页、印刷 Bates 编号、追加自定义页脚文本，到叠加半透明水印，代码足够简洁，可直接嵌入任何现有项目。

接下来，你可以探索更高级的场景——比如从数据库读取页脚文本、为不同章节使用不同字体，或生成一个单独的索引 PDF 列出所有 Bates 编号。所有这些扩展都基于我们这里展示的核心思路，让你能够随着需求的增长轻松扩展解决方案。

试一试，调整样式，并在评论中告诉我们你的使用体验。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}