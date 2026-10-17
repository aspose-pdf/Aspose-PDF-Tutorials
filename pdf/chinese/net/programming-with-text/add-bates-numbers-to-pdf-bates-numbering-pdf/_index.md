---
category: general
date: 2026-01-15
description: 使用 Aspose.Pdf 快速为 PDF 添加贝茨编号。了解如何向 PDF 添加页脚、添加页码以及自定义页码。
draft: false
keywords:
- add bates numbers
- bates numbering pdf
- add footer to pdf
- add page numbers pdf
- add custom page numbering
language: zh
og_description: 使用 Aspose.Pdf 快速为 PDF 添加 Bates 编号。了解如何向 PDF 添加页脚、添加页码以及自定义页码。
og_title: 为 PDF 添加贝茨编号 – 贝茨编号 PDF
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: 为PDF添加贝茨编号 – 贝茨编号 PDF
url: /zh/net/programming-with-text/add-bates-numbers-to-pdf-bates-numbering-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 为 PDF 添加 Bates 编号 – 完整指南

是否曾经需要**向 PDF 添加 Bates 编号**但不知从何入手？您并不孤单——法律团队、审计员以及处理海量文档的任何人每天都会遇到这个难题。好消息是？使用 Aspose.Pdf for .NET，您只需几行代码即可在每页上添加这些编号。

在本教程中，我们将完整演示整个过程：从引入 Aspose.Pdf 库、加载源文件、配置 *BatesNumberingArtifact*、将其作为页脚附加，最后保存结果。结束时，您还将了解如何**add footer to pdf**、**add page numbers pdf**，甚至**add custom page numbering**，以应对各种棘手的边缘情况。

## 您需要准备的环境

- .NET 6+（如果仍在使用经典堆栈，则为 .NET Framework 4.8）  
- 对 **Aspose.Pdf** NuGet 包的引用（`Install-Package Aspose.Pdf`）  
- 您想要加盖编号的 PDF 文件（我们称之为 `source.pdf`）  

就这些——无需额外工具，也不需要重量级的 PDF 编辑器。让我们开始吧。

![add bates numbers example](https://example.com/images/add-bates-numbers.png "add bates numbers example")

## 第一步：Add Bates Numbers – 加载 PDF 文档

首先，我们需要一个 `Document` 对象来表示即将修改的 PDF。可以把它想象成在开始编辑之前打开的 Word 文档。

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the PDF you want to add bates numbers to
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // The rest of the steps go here...
    }
}
```

> **为什么这很重要：** 加载文件后，您即可访问其 `Pages` 集合，后续我们将在该集合中附加 Bates 编号 artifact。如果文件未找到，Aspose 会抛出明确的 `FileNotFoundException`，请务必检查路径是否正确。

## 第二步：Configure bates numbering pdf Settings

现在我们定义**数字的外观**。`BatesNumberingArtifact` 允许您设置前缀、起始编号、位数填充、后缀以及放置位置。这是 **bates numbering pdf** 的核心。

```csharp
// Step 2: Create and configure the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    NumberDigits = 5,          // forces 5 digits, e.g., 01000
    Suffix = "-A",
    Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
};
```

> **小技巧：** 如果希望编号出现在页眉而不是页脚，只需将 `BottomCenter` 替换为 `TopCenter`。放置枚举还支持 `BottomLeft`、`BottomRight` 等，可灵活满足不同 **add footer to pdf** 样式的需求。

## 第三步：Add page numbers pdf – 将 Artifact 附加到每页

Artifact 准备好后，我们遍历每一页并将其添加到 `Artifacts` 集合中。这一步实际完成了 **adds page numbers pdf** 的操作。

```csharp
// Step 3: Attach the artifact to each page
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

> **内部原理是什么？** `Artifacts` 集合会在页面主内容渲染之后绘制，确保 Bates 编号位于任何现有文本之上、注释之下。如果需要编号位于内容后面（极少情况），可以使用 `page.Artifacts.Insert(0, batesArtifact)`。

## 第四步：Add custom page numbering – 保存更新后的 PDF

最后，将修改后的文档写入磁盘。输出文件将把 Bates 编号永久嵌入每一页。

```csharp
// Step 4: Save the PDF with the new numbering
pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
```

> **验证技巧：** 用任意阅读器打开 `bates_out.pdf`，您应当看到类似 `CASE-01000-A` 的文本居中显示在每页底部。如果编号缺失，请再次确认 `Placement` 属性是否与预期位置匹配。

## 完整工作示例

将上述步骤整合在一起，下面是完整的、可直接运行的程序：

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the source PDF
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // Configure Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            NumberDigits = 5,
            Suffix = "-A",
            Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
        };

        // Attach artifact to each page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.Artifacts.Add(batesArtifact);
        }

        // Save the new PDF (adds footer to pdf)
        pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

        Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
    }
}
```

### 预期结果

- **文件：** `bates_out.pdf` 与 `source.pdf` 位于同一文件夹  
- **视觉效果：** 底部居中显示文本 `CASE-01000-A`、`CASE-01001-A` …… 依次递增  
- **行为：** 编号被永久嵌入；即使打印、扁平化或进一步编辑也会保留。

## 常见变体与边缘情况

| 情况 | 调整方法 |
|-----------|---------------|
| **不同的起始编号** | 将 `StartNumber` 更改为任意整数（例如 `StartNumber = 500`）。 |
| **每卷的字母后缀** | 使用循环为每页修改 `Suffix`，或创建具有不同后缀的多个 artifact。 |
| **右对齐编号** | 设置 `Placement = BatesNumberingArtifact.PlacementLocation.BottomRight`。 |
| **大型文档（10k+ 页）** | 考虑对页面进行批处理或增加 `NumberDigits` 以避免溢出。 |
| **需要在特定页面隐藏编号** | 在 `foreach` 循环中跳过这些页面（例如 `if (page.Number != 1) page.Artifacts.Add(batesArtifact);`）。 |

> **注意事项：** 使用包含非法文件名字符的 `Prefix` 或 `Suffix`（例如 `*` 或 `?`）。Aspose 仍会嵌入它们，但在后续提取文本时可能会导致问题。

## 生产环境实用技巧

- **缓存 artifact**：如果一次处理大量 PDF，只创建一次 artifact 可为每个文件节省几毫秒。  
- **线程安全**：`BatesNumberingArtifact` 实例并非线程安全，请为每个线程提供独立副本。  
- **性能**：对于大批量处理，保存前可先关闭 PDF 压缩（`pdfDocument.Compress = false`），完成后再根据需要重新启用。  
- **测试**：始终对生成的第一份 PDF 进行快速目视检查，确保放置位置符合您的法律团队标准。

## 结论

现在，您已经掌握了使用 Aspose.Pdf 为任意 PDF **add bates numbers** 的完整端到端方案，并了解了 **add footer to pdf**、**add page numbers pdf** 以及 **add custom page numbering** 的各种选项。代码完全自包含，兼容 .NET 6 及更高版本，可直接嵌入任何现有自动化流水线。

接下来可以尝试将 `BottomCenter` 替换为页眉样式，实验动态前缀（例如来自数据库的案件 ID），或结合 Aspose 的文本提取功能，为新编号的文档生成可搜索的索引。天地无限，而您已经拥有了强大的文档控制利器。

祝编码愉快，愿您的 PDF 永远保持完美编号！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}