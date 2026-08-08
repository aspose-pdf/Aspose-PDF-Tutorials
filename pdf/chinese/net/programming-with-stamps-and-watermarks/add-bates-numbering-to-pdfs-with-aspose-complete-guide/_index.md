---
category: general
date: 2026-04-25
description: 使用 Aspose.Pdf 快速为 PDF 添加 Bates 编号。了解如何在 C# 中添加 PDF 页码、自动调整字体大小以及添加文字水印。
draft: false
keywords:
- add bates numbering
- add page numbers pdf
- auto adjust font size
- how to add bates
- add text watermark
language: zh
og_description: 使用 Aspose.Pdf 为 PDF 添加 Bates 编号。本指南展示了如何在单个可运行示例中添加页码、自动调整字体大小以及添加文字水印。
og_title: 为 PDF 添加贝茨编号 – 完整 Aspose.C# 教程
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: 使用 Aspose 为 PDF 添加贝茨编号 – 完整指南
url: /zh/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 为 PDF 添加 Bates 编号 – 完整指南

是否曾需要 **add bates numbering** 到 PDF，却不知从何入手？你并不孤单——法律团队、审计员和开发者每天都碰到这个难题。好消息是，使用 Aspose.Pdf for .NET，你可以在几行 C# 代码中给文档盖上 Bates 编号、自动调整字体大小，甚至将其作为细微的文字水印。

在本教程中，我们将逐步演示如何 **add page numbers pdf**，调整字体防止溢出，并彻底解答 “how to add bates” 的疑问。完成后，你将拥有一个可直接运行的控制台应用，生成专业编号的 PDF，并了解如何将其扩展为完整的水印解决方案。

## 前置条件

在开始之前，请确保你具备：

* **Aspose.Pdf for .NET**（截至 2026 年 4 月的最新 NuGet 包）。  
* .NET 6.0 SDK 或更高版本——API 在 .NET Framework 上同样可用，但 .NET 6 提供最佳性能。  
* 一个名为 `input.pdf` 的示例 PDF，放置在可引用的文件夹中（例如 `C:\Docs\`）。  

无需额外配置，库是自包含的。

---

## 步骤 1 – 加载源 PDF 文档

首先打开需要编号的文件。Aspose 的 `Document` 类代表整个 PDF，加载方式只需将路径传入构造函数。

```csharp
using Aspose.Pdf;

string inputPath = @"C:\Docs\input.pdf";
Document pdfDocument = new Document(inputPath);
```

*为什么重要*：加载文档后即可访问 `Pages` 集合，后续我们将在其中添加 Bates 印章。如果文件未找到，Aspose 会抛出明确的 `FileNotFoundException`，让你快速定位问题。

---

## 步骤 2 – 为 Bates 编号创建 TextStamp

接下来构造将在每页显示的视觉元素。`TextStamp` 类允许嵌入任意字符串，我们使用占位符 `{page}-{total}` 让 Aspose 自动替换。

```csharp
// Create a stamp that will display "Bates: 1-10", "Bates: 2-10", etc.
TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
{
    // Let the stamp automatically adjust its font size to fit the stamp rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Optional: make the stamp look like a subtle watermark
    Opacity = 0.4,
    // Position the stamp at the bottom‑right corner
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Choose a readable font
    Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
};
```

*关键点*：

* **auto adjust font size** – 将 `AutoAdjustFontSizeToFitStampRectangle` 设置为 `true`，可确保文字永不超出矩形，非常适合长度可变的页码。  
* **add text watermark** – 降低 `Opacity` 后，Bates 编号会呈现为淡淡的水印，满足 “add text watermark” 的需求，无需额外步骤。  
* **how to add bates** – `{page}` 与 `{total}` 这两个 token 是关键，Aspose 在运行时自动替换，你无需自行计算。

---

## 步骤 3 – 将印章应用到每一页

常见的陷阱是只在首页盖章。要真正 **add page numbers pdf**，必须遍历整个 `Pages` 集合。

```csharp
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp for each page to avoid shared state issues
    page.AddStamp(batesStamp);
}
```

为什么要 clone？`AddStamp` 方法内部会创建副本，但在循环中显式使用新实例可以避免后续修改印章属性（例如为特定页面更改颜色）时产生意外副作用。

---

## 步骤 4 – 保存更新后的 PDF

印章就位后，持久化非常简单。你可以覆盖原文件，也可以写入新位置——这里我们将生成名为 `output.pdf` 的新文件。

```csharp
string outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

打开 `output.pdf` 时，你会看到每页底部右侧显示 “Bates: 1‑10”、 “Bates: 2‑10” …，且透明度较低，兼具 **add text watermark** 效果。

---

## 完整工作示例

将上述代码整合后，得到一个可直接复制粘贴到 Visual Studio 的完整控制台程序。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        string inputPath = @"C:\Docs\input.pdf";
        Document pdfDocument = new Document(inputPath);

        // 2️⃣ Create a Bates number stamp with auto‑adjusted font size
        TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Opacity = 0.4, // acts as a subtle watermark
            XIndent = 20,
            YIndent = 20,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
        };

        // 3️⃣ Add the stamp to every page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.AddStamp(batesStamp);
        }

        // 4️⃣ Save the result
        string outputPath = @"C:\Docs\output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**预期结果**：在任意阅读器中打开 `output.pdf`，每页右下角都会出现类似 “Bates: 3‑12” 的文字，大小恰好适配矩形，透明度为 40%。这样既满足法律追踪需求，又实现了视觉水印。

---

## 常见变体与边缘情况

| Situation | What to change | Why |
|-----------|----------------|-----|
| **Different placement** | 调整 `HorizontalAlignment` / `VerticalAlignment` 或设置 `XIndent`/`YIndent` | 有些机构更喜欢左上角或居中放置。 |
| **Custom prefix** | 将 `"Bates: "` 替换为 `"Doc‑ID: "` 或任意字符串 | 可能使用不同的命名约定。 |
| **Multiple stamps** | 创建第二个 `TextStamp`（例如机密声明），并在第一个之后添加 | 将 **add bates numbering** 与其他 **add text watermark** 需求轻松组合。 |
| **Large page counts** | 增大初始字体大小（如 `14`）——自动调整会在需要时缩小 | 当页数 > 999 时字符串更长，自动调整可防止裁剪。 |
| **Encrypted PDFs** | 在盖章前调用 `pdfDocument.Decrypt("password")` | 未提供密码无法修改受保护的文件。 |

---

## 专业技巧与常见坑点

* **Pro tip:** 若文字紧贴页面边缘，可设置 `batesStamp.Margin = new MarginInfo(5, 5, 5, 5)`。  
* **注意:** 默认矩形尺寸为 100 × 30 pt，若需要更大区域，请手动设置 `batesStamp.Width` 与 `batesStamp.Height`。  
* **性能提示:** 为数千页盖章可能需要几秒钟，但 Aspose 会高效流式处理页面，无需一次性将整个文档加载到内存。

---

## 结论

我们已经演示了如何使用 Aspose.Pdf 为 PDF **add bates numbering**，同时实现 **add page numbers pdf**、**auto adjust font size** 与 **add text watermark** 的完整流程。上面的可运行示例为任何法律文档工作流或内部报告系统提供了坚实的基础。

准备好下一步了吗？可以尝试将此方法与 Aspose 的 PDF 合并 API 结合，批量处理多个文件，或探索 `TextFragment` 类实现更丰富的水印（彩色、旋转或多行）。可能性无限，而你现在拥有的代码是可靠的起点。

如果本指南对你有帮助，欢迎留言、给仓库加星或分享你的实现方式。祝编码愉快，愿你的 PDF 永远编号精准！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}