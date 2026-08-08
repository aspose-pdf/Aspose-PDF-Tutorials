---
category: general
date: 2026-05-27
description: 使用 Aspose.Pdf 在 C# 中为 PDF 添加 Bates 编号。了解如何快速添加 Bates 编号、自定义格式以及自动化法律文档标记。
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbering
language: zh
og_description: 使用 Aspose.Pdf 在 C# 中为 PDF 添加 Bates 编号。本指南展示了如何添加 Bates 编号、配置前缀并保存结果。
og_title: 在 C# 中为 PDF 添加 Bates 编号 – 步骤教程
schemas:
- author: Aspose
  dateModified: '2026-05-27'
  description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  headline: Add Bates Numbering PDF in C# – Complete Guide
  type: TechArticle
- description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  name: Add Bates Numbering PDF in C# – Complete Guide
  steps:
  - name: Expected Output
    text: 'When you run the program, the console prints:'
  - name: Can I position the Bates number elsewhere?
    text: Yes. Use the `BatesNumberingArtifact`’s `Location` property (e.g., `Location
      = new Position(10, 10)`) to place the number at custom X/Y coordinates. You
      can also set `HorizontalAlignment` and `VerticalAlignment` for more control.
  - name: What if my PDF has thousands of pages?
    text: Aspose.Pdf streams pages efficiently, but it’s still a good idea to process
      in batches if you hit memory limits. The `Document` class also supports `PdfConverter`
      for incremental saving.
  - name: How do I change the font or color?
    text: 'Wrap the artifact in a `TextState` object:'
  - name: Do I need a license for production use?
    text: A licensed version removes evaluation watermarks and unlocks full performance.
      The free trial works fine for testing and proof‑of‑concepts.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- Bates numbering
- PDF automation
title: 在 C# 中为 PDF 添加 Bates 编号 – 完整指南
url: /zh/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中为 PDF 添加 Bates 编号 – 完整指南

是否曾经想过 **如何为 PDF 添加 Bates 编号**，而不必花费数小时手动操作？你并不孤单——法律团队、审计员和电子取证专家都需要一种可靠的方式，以编程方式 **为 PDF 文件添加 Bates 编号**。  

在本教程中，我们将使用 Aspose.Pdf for .NET 逐步演示一个简洁的端到端解决方案，这样你只需几行 C# 代码即可在任何文档上添加 Bates 编号。

## 你将学到的内容

- 如何使用 Aspose.Pdf 打开现有 PDF  
- 如何创建 Bates 编号工件并微调其格式  
- 如何将工件附加到每一页（或仅第一页）  
- 如何保存更新后的文件并验证结果  

无需任何 Aspose 经验——只需对 C# 和 .NET 有基本了解。完成后，你将拥有一个可复用的代码片段，能够复制粘贴到任何项目中。

## 前提条件

- .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.7+）  
- Aspose.Pdf for .NET NuGet 包（`Install-Package Aspose.Pdf`）  
- 需要标记的源 PDF 文件（放在可引用的文件夹中）

> **专业提示：** 如果你还没有许可证，Aspose 提供免费临时密钥，可去除评估水印。

## 第一步 – 打开源 PDF 文档  

首先，我们需要一个表示磁盘上文件的 `Document` 对象。可以把它看作加载了一块空白画布，随后我们将在其上绘制 Bates 编号。

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Adjust the path to point at your source PDF
        string sourcePath = @"C:\Docs\source.pdf";

        // Load the PDF – this is where we start to add Bates numbering
        using (var pdfDocument = new Document(sourcePath))
        {
            // The rest of the logic lives inside this using block
        }
    }
}
```

**为什么这很重要：** 在 `using` 块中打开文档可确保及时释放所有非托管资源，这对大型 PDF 尤为重要。

## 第二步 – 创建 Bates 编号工件  

*BatesNumberingArtifact* 是 Aspose 用来描述编号外观的方式。你可以设置前缀、起始号码、增量，甚至自定义格式字符串。

```csharp
// Step 2: Define the Bates numbering artifact
var batesNumbering = new BatesNumberingArtifact
{
    Prefix = "ABC",            // Text that appears before each number
    StartNumber = 1000,        // First number in the sequence
    Increment = 1,             // Step between consecutive numbers
    Format = "{0:D5}"          // Zero‑padded 5‑digit number (e.g., 01000)
};
```

**为什么可能需要更改这些值：**  
- **Prefix** 对于案件 ID（如 “CASE‑”、 “DOC‑”）很有用。  
- **StartNumber** 允许你继续之前的序列。  
- **Increment** 若需要奇偶编号，可设置为 2。  
- **Format** 支持任何 .NET 复合格式；`{0:D5}` 可确保使用前导零的五位数字。

## 第三步 – 将工件附加到所需页面  

你可以将工件添加到单页、页范围或整个文档。对于大多数法律工作流，我们会将其附加到 *每* 页，但下面的示例展示了最小情况——仅在第一页添加。

```csharp
// Step 3: Attach the artifact to the first page (index is 1‑based)
pdfDocument.Pages[1].Artifacts.Add(batesNumbering);
```

如果需要覆盖所有页面，可循环遍历：

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesNumbering);
}
```

**为什么此步骤至关重要：** 工件在页面内容 *之后* 渲染，因此编号会显示在现有文本之上，而不改变原始布局。

## 第四步 – 保存修改后的 PDF  

最后，将更改写回磁盘。你可以覆盖原文件或创建新文件——这里我们将生成一个名为 `bates.pdf` 的新副本。

```csharp
// Step 4: Persist the changes
string outputPath = @"C:\Docs\bates.pdf";
pdfDocument.Save(outputPath);

Console.WriteLine($"Bates numbering added successfully. File saved to: {outputPath}");
```

打开 `bates.pdf` 时，你会看到默认位置（通常是右下角）印有 “ABC01000”（或你选择的任何格式）的编号。

## 完整工作示例  

将所有步骤整合在一起，下面是可以编译运行的完整程序：

```csharp
using Aspose.Pdf;
using System;

class AddBatesNumbering
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Open the source PDF
        // -----------------------------------------------------------------
        string sourcePath = @"C:\Docs\source.pdf";
        using (var pdfDocument = new Document(sourcePath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Create and configure the Bates numbering artifact
            // -----------------------------------------------------------------
            var batesNumbering = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                StartNumber = 1000,
                Increment = 1,
                Format = "{0:D5}"
            };

            // -----------------------------------------------------------------
            // 3️⃣ Attach the artifact to each page (or a specific page)
            // -----------------------------------------------------------------
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesNumbering);
            }

            // -----------------------------------------------------------------
            // 4️⃣ Save the new PDF
            // -----------------------------------------------------------------
            string outputPath = @"C:\Docs\bates.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbers added. Output: {outputPath}");
        }
    }
}
```

### 预期输出

运行程序后，控制台会输出：

```
Bates numbers added. Output: C:\Docs\bates.pdf
```

打开 `bates.pdf` 可看到每页都有前缀 “ABC” 加上零填充的五位序列——正是代码所实现的效果。

## 常见问题与边缘情况

### 我可以将 Bates 编号放在其他位置吗？

可以。使用 `BatesNumberingArtifact` 的 `Location` 属性（例如 `Location = new Position(10, 10)`）将编号放置在自定义的 X/Y 坐标上。你还可以设置 `HorizontalAlignment` 和 `VerticalAlignment` 以获得更精细的控制。

### 如果我的 PDF 有成千上万页怎么办？

Aspose.Pdf 能高效地流式处理页面，但如果遇到内存限制，仍建议分批处理。`Document` 类还支持 `PdfConverter` 用于增量保存。

### 如何更改字体或颜色？

将工件包装在 `TextState` 对象中：

```csharp
batesNumbering.TextState = new TextState
{
    FontSize = 12,
    Font = FontRepository.FindFont("Arial"),
    ForegroundColor = Color.FromRgb(255, 0, 0) // red
};
```

### 生产环境是否需要许可证？

授权版本会去除评估水印并解锁全部性能。免费试用版足以用于测试和概念验证。

## 验证 – 快速视觉检查  

如果你更喜欢自动化验证，Aspose 可以提取页面文本并确认前缀是否存在：

```csharp
string pageText = pdfDocument.Pages[1].ExtractText();
bool hasBates = pageText.Contains("ABC01000");
Console.WriteLine(hasBates ? "Bates number verified." : "Number missing!");
```

在保存步骤后运行此代码，如果一切顺利，将打印 `Bates number verified.`。

## 结论  

现在你已经了解了如何使用 Aspose.Pdf 在 C# 中 **为 PDF 添加 Bates 编号**。从打开文档、配置工件、将其附加到页面再到保存结果，整个过程简洁明了且可完全脚本化。  

下一步？尝试以下实验：  
- 为多个案件批次使用不同的 `Prefix` 值  
- 使用自定义 `Location` 和 `TextState` 进行品牌化  
- 通过在循环中调整 `StartNumber`，为每页添加特定前缀（例如 “VOL‑1‑”、 “VOL‑2‑”）  

这些微调使你能够将解决方案定制到几乎所有法律或档案工作流。  

对多语言 PDF 或加密文件的 **如何添加 Bates 编号** 还有其他疑问吗？在下方留言吧，祝编码愉快！

## 相关教程

- [如何使用 Aspose.PDF for .NET 为 PDF 添加和自定义页码 | 文档操作指南](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [如何使用 Aspose.PDF for .NET 在 PDF 中添加不同的页眉&#58; 步骤指南](/pdf/english/net/document-manipulation/add-different-headers-aspose-pdf-net/)
- [如何使用 Aspose.PDF for .NET 为 PDF 添加文本水印页脚&#58; 步骤指南](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}