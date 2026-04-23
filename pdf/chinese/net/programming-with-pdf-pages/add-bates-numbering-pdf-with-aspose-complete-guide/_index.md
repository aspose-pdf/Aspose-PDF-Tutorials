---
category: general
date: 2026-03-24
description: 使用 Aspose.Pdf 在 C# 中为 PDF 添加贝茨编号。了解如何添加新页面 PDF、应用贝茨编号以及高效更新贝茨编号。
draft: false
keywords:
- add bates numbering pdf
- add new page pdf
- apply bates number
- create pdf aspose
- update bates numbering
language: zh
og_description: 快速为 PDF 添加 Bates 编号。本指南展示如何添加新页面 PDF、应用 Bates 编号以及使用 Aspose.Pdf 更新
  Bates 编号。
og_title: 使用 Aspose 为 PDF 添加贝茨编号 – 完整指南
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: 使用 Aspose 为 PDF 添加 Bates 编号 – 完整指南
url: /zh/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose 添加 Bates 编号 PDF – 完整指南

是否曾经需要**添加 Bates 编号 PDF**文件，却不知从何入手？您并非唯一面临此难题的人——法律团队、审计员以及处理大量文档的任何人经常会碰到这个障碍。好消息是？使用 Aspose.Pdf for .NET，您只需几行代码即可实现，并且还能学习如何**添加新页面 PDF**对象、**应用 Bates 编号**以及随后**更新 Bates 编号**。

在本教程中，我们将演示一个真实场景：您拥有一个源 PDF，想在新页面上插入 Bates 印章，并且可能需要在以后重新编号整个文档。完成后，您将能够创建**Aspose PDF**解决方案，具备生产就绪的能力，并且了解每一步的意义。

## 您将实现的目标

- 使用 Aspose.Pdf 加载现有 PDF。
- **添加新页面 PDF**以容纳 Bates 印章。
- **使用 `TextStamp` 应用 Bates 编号**。
- (可选) **更新所有页面的 Bates 编号**。
- 一个完整、可运行的 C# 示例，您可以直接放入任何 .NET 项目中。

### 前置条件

- .NET 6.0 或更高（代码同样适用于 .NET Framework 4.7+）。
- Aspose.Pdf for .NET NuGet 包（`Install-Package Aspose.Pdf`）。
- 一个放置在已知文件夹中的源 PDF 文件（`source.pdf`）。

无需复杂配置——只需库和一个 PDF 即可使用。

![添加 Bates 编号 PDF 示例](https://example.com/placeholder.png "展示在 PDF 页面上添加 Bates 编号的示意图")

## 步骤 1 – 加载源 PDF（基础）

在您能够**添加 Bates 编号 PDF**之前，需要一个文档对象来操作。将 `Document` 视为画布；没有它，就没有可加盖印章的对象。

```csharp
using Aspose.Pdf;

// Load the existing PDF – replace the path with your actual file location
using var pdfDocument = new Document(@"C:\MyPdfs\source.pdf");

// Verify the document was loaded (optional but handy for debugging)
Console.WriteLine($"Document loaded: {pdfDocument.Pages.Count} pages found.");
```

*为什么重要：* 加载文件后，您即可访问其页面集合、元数据和安全设置。如果文件损坏，Aspose 会抛出详细异常，帮助您避免后续的静默失败。

## 步骤 2 – 为 Bates 印章**添加新页面 PDF**

为何将印章放在全新页面上？许多法律工作流要求 Bates 编号出现在单独的标题页上，以保持原始内容不受影响。使用 Aspose 添加页面只需一行代码。

```csharp
// Create a fresh page at the end of the document
var newPage = pdfDocument.Pages.Add();

// Quick sanity check – print the new total page count
Console.WriteLine($"New page added. Total pages: {pdfDocument.Pages.Count}");
```

*小技巧：* 如果需要在每页都加盖印章，可以跳过添加新页面，直接遍历 `pdfDocument.Pages`。这里我们特意**添加新页面 PDF**，以演示最常见的“封面页”模式。

## 步骤 3 – 使用 TextStamp **应用 Bates 编号**

操作的核心是 `TextStamp`。它允许您精确定位文本、设置边距并定义外观样式。

```csharp
// Create a TextStamp that holds the Bates number
var batesStamp = new TextStamp("Bates: 001")
{
    // Align the stamp to the bottom‑right corner
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Bottom,
    
    // Margin values are in points (1 point = 1/72 inch)
    Margin = new Margin(0, 0, 20, 20) // left, bottom, right, top
};

// Attach the stamp to the newly created page
newPage.AddStamp(batesStamp);
```

*为何选择这些设置：* 右下角放置符合大多数法院对 Bates 编号的要求。20 点的边距确保文本远离页面边缘，避免打印机裁切。若需顺序编号，可将 `"Bates: 001"` 替换为变量。

## 步骤 4 – 保存更新后的 PDF

保存操作很简单，但您可能希望保留原始文件。我们将保存到新位置。

```csharp
string outputPath = @"C:\MyPdfs\output_with_bates.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved with Bates stamp at: {outputPath}");
```

此时，您已经成功**添加 Bates 编号 PDF**到文档，并且**添加新页面 PDF**以容纳印章。使用任意查看器打开文件——您应能看到印章紧贴在最后一页的右下角。

## 步骤 5 – （可选）**更新所有页面的 Bates 编号**

如果您之后决定在其他页面插入更多印章怎么办？Aspose 提供了一个辅助方法，可自动在每页递增编号，免去手动字符串处理的麻烦。

```csharp
// This will renumber all pages using the same stamp format
pdfDocument.Pages.UpdateBatesNumbering();
pdfDocument.Save(@"C:\MyPdfs\output_renumbered.pdf");
Console.WriteLine("All pages have been renumbered.");
```

*何时使用：* 适用于每页都需要唯一标识的大批量文档。该方法遵循原始 `TextStamp` 的属性，确保对齐和边距保持一致。

## 完整工作示例 – 从头到尾

下面是完整的程序代码，您可以复制粘贴到控制台应用中。它包含所有步骤、错误处理和注释。

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // Path to the source PDF – adjust as needed
        const string sourcePath = @"C:\MyPdfs\source.pdf";
        const string resultPath = @"C:\MyPdfs\output_with_bates.pdf";

        try
        {
            // 1️⃣ Load the existing PDF
            using var pdfDocument = new Document(sourcePath);
            Console.WriteLine($"Loaded PDF with {pdfDocument.Pages.Count} pages.");

            // 2️⃣ Add a new blank page for the Bates stamp
            var newPage = pdfDocument.Pages.Add();
            Console.WriteLine($"Added new page. Total pages now: {pdfDocument.Pages.Count}");

            // 3️⃣ Create and configure the Bates TextStamp
            var batesStamp = new TextStamp("Bates: 001")
            {
                HorizontalAlignment = HorizontalAlignment.Right,
                VerticalAlignment   = VerticalAlignment.Bottom,
                Margin = new Margin(0, 0, 20, 20) // left, bottom, right, top
            };

            // 4️⃣ Place the stamp on the newly added page
            newPage.AddStamp(batesStamp);
            Console.WriteLine("Bates stamp applied to the new page.");

            // 5️⃣ Save the modified PDF
            pdfDocument.Save(resultPath);
            Console.WriteLine($"PDF saved successfully at {resultPath}");

            // Optional: Renumber all pages if you add more stamps later
            // pdfDocument.Pages.UpdateBatesNumbering();
            // pdfDocument.Save(@"C:\MyPdfs\output_renumbered.pdf");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

**预期结果：** 打开 `output_with_bates.pdf`，您会看到原始内容保持不变，新增的最后一页，以及右下角紧贴的文本 “Bates: 001”。如果取消注释 `UpdateBatesNumbering` 行，则每页都会得到递增的编号。

## 常见问题与边缘情况

- **我可以更改字体或颜色吗？**  当然可以。`TextStamp` 继承自 `Stamp`，因此您可以设置 `Font`、`FontSize`、`Color` 等。例如：`batesStamp.Font = FontRepository.FindFont("Arial"); batesStamp.FontSize = 12; batesStamp.TextColor = Color.Red;`。
- **如果我的 PDF 受密码保护怎么办？**  使用密码加载：`new Document(sourcePath, new LoadOptions { Password = "mySecret" })`。
- **是否需要释放 `Document`？**  如示例所示，使用 `using` 语句会自动释放，关闭文件句柄。
- **边距是以点还是像素为单位？**  点。1 点等于 1/72 英寸，这是 PDF 的标准单位。
- **我可以将印章放在第一页而不是新页面吗？**  可以——只需将 `newPage` 替换为 `pdfDocument.Pages[1]`（页面索引从 1 开始）。

## 结论

现在，您已经掌握了使用 Aspose.Pdf **添加 Bates 编号 PDF**的完整端到端方案，涵盖了如何**添加新页面 PDF**、**应用 Bates 编号**以及在文档扩展时**更新 Bates 编号**。代码已可直接嵌入任何 C# 项目，说明有助于您根据自定义布局、不同字体或批量处理进行调整。

### 接下来做什么？

- 深入了解 **Aspose PDF 创建**，通过添加图像、表格或数字签名。
- 自动化批处理：遍历文件夹中的 PDF 并为每个文件加盖印章。
- 如果需要归档文档，可探索 Aspose 的 PDF/A 合规功能。

动手试一试，微调对齐方式，尝试不同的印章文本，让库来完成繁重工作。如果遇到任何问题，Aspose 社区论坛是提问的好去处——祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}