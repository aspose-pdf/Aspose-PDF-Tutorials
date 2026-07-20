---
category: general
date: 2026-07-20
description: 如何使用 Aspose.Pdf 为 PDF 添加贝茨编号。学习快速且可靠地为 PDF 添加贝茨编号并在每页添加印章。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to add bates numbering
- add bates numbers pdf
- add stamp to each page
language: zh
lastmod: 2026-07-20
og_description: 如何使用 Aspose.Pdf 为 PDF 添加贝茨编号。本指南展示了仅用几行 C# 代码即可为 PDF 添加贝茨编号并在每页加盖印章。
og_image_alt: Screenshot of a PDF page displaying Bates numbering added by Aspose.Pdf
og_title: 如何在 PDF 中添加贝茨编号 – 完整的 Aspose.Pdf 教程
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: How to add bates numbering to a PDF using Aspose.Pdf. Learn to add
    bates numbers pdf and add stamp to each page quickly and reliably.
  headline: How to Add Bates Numbering in PDF with Aspose – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: Yes. Load the document with a `PdfLoadOptions` object that supplies the
      password, then proceed exactly as shown.
    question: Does this work with password‑protected PDFs?
  - answer: Create multiple `BatesNumberingStamp` instances, configure each with its
      own `Prefix`, and apply them only to the appropriate page ranges.
    question: What if I need different prefixes per case?
  - answer: 'Aspose.Pdf offers a 30‑day trial. For production use you’ll need a license,
      but the API surface remains identical. --- ## Conclusion We’ve just covered
      **how to add bates numbering** to any PDF using Aspose.Pdf, demonstrated how
      to **add bates numbers pdf** in a clean, repeatable fashion, and showed'
    question: Is the library free?
  type: FAQPage
tags:
- Aspose.Pdf
- Bates numbering
- PDF automation
title: 如何使用 Aspose 在 PDF 中添加贝茨编号 – 步骤指南
url: /zh/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-aspose-step-by-step-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose 在 PDF 中添加 Bates 编号 – 步骤指南

是否曾想过 **如何在法律文档中添加 Bates 编号** 而无需在 GUI 中花费数小时？你并非唯一有此需求的人。在许多律所、政府机构乃至大型企业中，为每页加上唯一标识是一项日常工作——然而只需一行 C# 代码即可轻松实现。

在本教程中，我们将通过一个完整且可运行的示例，向你展示 **如何使用 Aspose.Pdf 添加 Bates 编号**。结束时，你还将了解如何 **add bates numbers pdf** 文件以及 **add stamp to each page**，只需几行代码。没有魔法，只有清晰的思路和实用技巧。

## 您将学习到

- 使用 Aspose.Pdf 加载已有的 PDF。
- 创建 `BatesNumberingStamp` 并自定义其外观。
- 循环遍历每一页并自动 **add stamp to each page**。
- 将结果保存为新 PDF，使每页都带有专业的 Bates 编号。

### 前置条件

- .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.7+）。
- 有效的 Aspose.Pdf for .NET 许可证（或临时评估密钥）。
- 需要编号的原始 PDF 文件（我们将其称为 `Original.pdf`）。

如果满足以上三点，你就可以开始操作了。

---

## Step 1: Set Up Your Project and Install Aspose.Pdf

首先，创建一个新的控制台项目（或在已有项目中添加代码）。然后通过 NuGet 安装包：

```bash
dotnet add package Aspose.Pdf
```

> **专业提示：** 如果你在企业网络环境中，请确保已将 NuGet 源配置为能够访问 `https://www.nuget.org`。

## Step 2: Load the Source PDF Document

加载 PDF 就像把文件路径交给 Aspose 那样简单。`Document` 类代表整个文件。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the source PDF (replace the path with your own)
var document = new Document(@"C:\Temp\Original.pdf");

// Quick sanity check – how many pages are we dealing with?
Console.WriteLine($"Document contains {document.Pages.Count} pages.");
```

为什么要记录页数？因为 Bates 编号必须在 *所有* 页面上顺序递增，查看页数可以帮助确认没有误加载其他文件。

## Step 3: Create a Bates Numbering Stamp

操作的核心是 `BatesNumberingStamp`。它允许你定义前缀、分隔符、数字填充位数，甚至可以将印章标记为 *artifact*（即对文本提取工具不可见）。

```csharp
var batesStamp = new BatesNumberingStamp
{
    // Starting number – change this to whatever your workflow requires
    StartingNumber = 1000,

    // A human‑readable prefix, often a case or project code
    Prefix = "ABC-",

    // Separator between the running number and the total page count
    Separator = "/",

    // Pad the number with leading zeros to a fixed width (5 digits here)
    NumberOfDigits = 5,

    // Mark the stamp as an artifact so it won’t be indexed by search
    Artifact = true
};
```

**为什么这样设置？**  
- `StartingNumber = 1000` 模拟了已经有大量积压的典型法律案卷。  
- `NumberOfDigits = 5` 确保 `01000`、`01001` 等编号对齐美观。  
- `Artifact = true` 在 PDF 将被送入 OCR 或电子发现流程时至关重要；编号对人类可见，但会被文本搜索引擎忽略。

## Step 4: Add the Stamp to Every Page

现在遍历 `document.Pages`，在每页上应用相同的印章。Aspose 会自动为你递增编号。

```csharp
foreach (Page page in document.Pages)
{
    // The AddStamp method clones the stamp for the current page,
    // updates the running number, and positions it at the default location.
    page.AddStamp(batesStamp);
}
```

> **常见问题：** *我可以控制印章出现的位置吗？*  
> 当然可以。`BatesNumberingStamp` 继承自 `Stamp`，因此可以在循环前设置 `HorizontalAlignment`、`VerticalAlignment`、`XIndent`、`YIndent` 等属性。为简洁起见，这里使用默认的右下角位置。

## Step 5: Save the Modified PDF

最后，持久化更改。你可以覆盖原文件，也可以写入新位置——这里我们保留两个副本。

```csharp
// Save the new PDF with Bates numbers
document.Save(@"C:\Temp\BatesNumbered.pdf");

// Inform the user
Console.WriteLine("Bates numbering added successfully!");
```

打开 `BatesNumbered.pdf` 时，每页都会显示类似以下的印章：

```
ABC-01000/00123
ABC-01001/00123
…
ABC-01122/00123
```

其中 `00123` 为总页数，前缀 `ABC-` 保持不变。

---

## 完整工作示例

将下面的完整代码块复制到全新的 `Program.cs` 文件中并运行。根据你的环境调整文件路径。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            var srcPath = @"C:\Temp\Original.pdf";
            var document = new Document(srcPath);
            Console.WriteLine($"Loaded '{srcPath}' with {document.Pages.Count} pages.");

            // 2️⃣ Configure the Bates numbering stamp
            var batesStamp = new BatesNumberingStamp
            {
                StartingNumber = 1000,
                Prefix = "ABC-",
                Separator = "/",
                NumberOfDigits = 5,
                Artifact = true,
                // Optional: change alignment if you need a different location
                // HorizontalAlignment = HorizontalAlignment.Left,
                // VerticalAlignment = VerticalAlignment.Top,
                // XIndent = 20,
                // YIndent = 20
            };

            // 3️⃣ Apply the stamp to every page
            foreach (Page page in document.Pages)
            {
                page.AddStamp(batesStamp);
            }

            // 4️⃣ Save the new PDF
            var outPath = @"C:\Temp\BatesNumbered.pdf";
            document.Save(outPath);
            Console.WriteLine($"Saved Bates‑numbered PDF to '{outPath}'.");
        }
    }
}
```

**控制台预期输出：**

```
Loaded 'C:\Temp\Original.pdf' with 12 pages.
Saved Bates-numbered PDF to 'C:\Temp\BatesNumbered.pdf'.
```

打开保存的文件，你会看到每页上按顺序递增的编号——这正是你在 **add bates numbers pdf** 时所期待的效果。

---

## Advanced Tweaks (Optional)

| 目标 | 实现方式 |
|------|----------|
| **更改印章颜色** | 在循环前设置 `batesStamp.Color = Color.FromRgb(255, 0, 0);` |
| **将印章放置在页眉** | 如注释代码所示，调整 `HorizontalAlignment` 和 `VerticalAlignment` 属性 |
| **跳过特定页面** | 在 `foreach` 中加入 `if (page.Number % 2 == 0) continue;` 条件 |
| **使用自定义字体** | 赋值 `batesStamp.Font = FontRepository.FindFont("Arial");` |
| **使印章对 OCR 可见** | 将 `Artifact = false` |

这些变体让你在保持核心逻辑简洁的同时，仍然可以 **add stamp to each page**。

---

## Frequently Asked Questions

**Q: 这能用于受密码保护的 PDF 吗？**  
A: 可以。使用 `PdfLoadOptions` 对象提供密码加载文档，然后按示例操作即可。

**Q: 如果不同案件需要不同前缀怎么办？**  
A: 创建多个 `BatesNumberingStamp` 实例，为每个实例配置各自的 `Prefix`，并仅在相应的页码范围内应用。

**Q: 这个库免费吗？**  
A: Aspose.Pdf 提供 30 天试用。生产环境需要购买许可证，但 API 使用方式保持完全一致。

---

## Conclusion

我们已经演示了 **how to add bates numbering** 到任意 PDF 的完整过程，展示了如何以简洁、可重复的方式 **add bates numbers pdf**，并说明了使用单个循环 **add stamp to each page** 的最简方法。代码完全自包含，几秒钟即可运行，可直接嵌入更大的文档处理流水线而无需修改。

准备好迎接下一个挑战了吗？尝试生成一页封面，列出 Bates 编号范围，或在每个印章旁嵌入二维码。可能性无限，而今天学到的模式将在你需要自动化 PDF 元数据的任何场景中发挥作用。

如果本指南对你有帮助，请分享、留言，或浏览我们关于 PDF 合并、加水印和数字签名的其他教程。祝编码愉快！

## What Should You Learn Next?

以下教程紧扣本指南中展示的技术，帮助你进一步掌握相关 API 功能，并提供可直接运行的代码示例和逐步说明，便于你在项目中探索替代实现方案。

- [如何使用 Aspose.PDF for .NET 在 PDF 中添加页面印章：完整指南](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [如何使用 Aspose.PDF for .NET 在 PDF 中添加页码印章 | 水印与背景](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [如何使用 Aspose.PDF for .NET 添加并自定义 PDF 页码 | 文档操作指南](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}