---
category: general
date: 2026-02-25
description: Bates 编号教程 – 学习如何在 PDF 中添加页码并使用 Aspose.Pdf 在 C# 中应用自定义 Bates 编号。一步一步的指南，附完整代码。
draft: false
keywords:
- bates numbering tutorial
- add page numbers pdf
- how to add bates
- add bates numbering
language: zh
og_description: Bates 编号教程向您展示如何在 C# 中为 PDF 添加页码和自定义 Bates 编号。完整代码、解释和技巧。
og_title: Bates 编号教程 – 使用 C# 为 PDF 添加 Bates 编号
tags:
- PDF
- C#
- Aspose.Pdf
title: Bates 编号教程：使用 C# 为 PDF 添加 Bates 编号
url: /zh/net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-bates-numbers-to-pdfs-with-c/
---

Also bullet lists.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# bates numbering tutorial – 在 C# 中为 PDF 添加 Bates 编号

有没有想过在 PDF 中添加页码的同时嵌入法律风格的 Bates 编号？你并不孤单。在本 **bates numbering tutorial** 中，我们将逐步讲解如何使用 Aspose.Pdf for .NET 在 PDF 的每一页上盖上自定义前缀、前导零以及精确定位的标签。

好消息是？只要掌握核心概念，这个过程相当直接。阅读完本指南后，你将拥有一个可运行的程序，能够将 *input.pdf* 处理成 *bates_out.pdf*，并在每页上显示类似 “ABC‑01000” 的标签。让我们开始吧。

## 你需要准备的东西

- **Aspose.Pdf for .NET**（版本 23.10 或更高）。该库为商业产品，但免费试用版足以用于学习。
- .NET 6+ SDK（任意近期版本均可）。
- 基本的 C# 开发环境——Visual Studio、VS Code 或 Rider。
- 用于实验的输入 PDF（任意多页文档均可展示效果）。

除 Aspose.Pdf 外无需额外的 NuGet 包，代码可在 Windows、Linux 或 macOS 上直接运行，无需修改。

## 第一步：加载源 PDF 文档（bates numbering tutorial – initialization）

首先我们创建一个 `Document` 对象来表示要修改的 PDF。可以把它想象成加载了一块可以绘制的空白画布。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF – replace the path with your actual file location
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// Quick sanity check – make sure the document actually has pages
if (pdfDocument.Pages.Count == 0)
{
    throw new InvalidOperationException("The PDF you provided contains no pages.");
}
```

**为什么重要：** 如果不先加载文件，就没有可供标注的对象。此检查可以防止在后续尝试向不存在的页面集合添加工件时出现静默失败。

## 第二步：定义 Bates 编号工件（how to add bates）

`BatesNumberingArtifact` 告诉 Aspose 在何处以及如何绘制标识符。你可以控制前缀、起始编号、零填充、字体大小以及精确的 X/Y 坐标。

```csharp
// Configure the Bates numbering artifact
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
{
    Prefix = "ABC",          // Text that appears before the number
    Start = 1000,            // First number in the sequence
    LeadingZeros = 5,        // Pad the number with zeros (e.g., 01000)
    FontSize = 9,            // Small enough to sit in the margin
    Position = new Position   // Position measured from the lower‑left corner
    {
        X = 50,               // Horizontal offset (points)
        Y = 30                // Vertical offset (points)
    }
};
```

**为什么重要：** `LeadingZeros` 属性确保每个标签长度一致，这在对齐要求严格的法律文档中至关重要。通过调整 `X` 和 `Y` 可以将印章移动到右上角、左下角或工作流所需的任何位置。

## 第三步：将工件附加到每一页（add page numbers pdf）

接下来遍历每一页并附加相同的工件。这一步实现了 *add page numbers pdf* 的需求——每页都会自动获得一个顺序标签。

```csharp
// Iterate over each page and add the Bates artifact
foreach (Page page in pdfDocument.Pages)
{
    // The artifact is added to the page's Artifacts collection.
    // Aspose will handle the incrementing of the number for us.
    page.Artifacts.Add(batesArtifact);
}
```

**为什么重要：** 将工件添加到 `Artifacts` 集合而不是手动绘制文本，可让 Aspose 负责编号逻辑、前导零以及渲染，从而减少错误并保持代码简洁。

## 第四步：保存修改后的 PDF（add bates numbering）

最后，将更改保存为新文件。养成写入不同文件名的习惯可以避免覆盖原始文件。

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");

// Optional: let the user know we succeeded
Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
```

**为什么重要：** `Save` 方法会写入完整的 PDF，并将工件嵌入页面内容流。生成的文件可在任何 PDF 查看器中打开，并会按照指定方式显示 Bates 编号。

## 完整可运行示例（所有步骤合并）

下面是完整的、可直接运行的程序。复制粘贴到控制台应用项目中，替换占位路径，然后按 **F5** 运行。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
            if (pdfDocument.Pages.Count == 0)
                throw new InvalidOperationException("The PDF you provided contains no pages.");

            // 2️⃣ Configure the Bates numbering artifact
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                Start = 1000,
                LeadingZeros = 5,
                FontSize = 9,
                Position = new Position { X = 50, Y = 30 }
            };

            // 3️⃣ Attach the artifact to every page
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesArtifact);
            }

            // 4️⃣ Save the modified PDF
            pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");
            Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
        }
    }
}
```

### 预期结果

在 Adobe Reader、Foxit 或任意查看器中打开 *bates_out.pdf*。你应该会看到第一页显示 **ABC‑01000**，第二页显示 **ABC‑01001**，以此类推，标签位于左边距 50 pt、底部 30 pt 处。由于前导零的存在，数字右对齐，使文档看起来整洁专业。

## 常见变体与边缘情况

| 场景 | 调整方法 |
|----------|---------------|
| **不同的前缀** | 在工件定义中将 `Prefix = "XYZ"` 改为所需前缀。 |
| **从自定义数字开始** | 设置 `Start = 5000`（或任意整数）。 |
| **将编号放在右上角** | 使用 `Position = new Position { X = pdfDocument.PageInfo.Width - 50, Y = pdfDocument.PageInfo.Height - 30 }`。 |
| **为更大的文档更改字体大小** | 将 `FontSize = 12`（或任意大小）修改为所需值。 |
| **添加背景矩形** | 在 `BatesNumberingArtifact` 之前创建 `RectangleArtifact` 并加入。 |
| **跳过特定页面** | 在 `foreach` 循环内加入 `if (page.Number % 2 == 0) continue;` 以跳过偶数页。 |

**小技巧：** 先用短小的 PDF 进行测试。这样可以更快验证定位是否正确，再对 200 页的案件文件运行脚本。

## 常见问答

- **这能处理加密的 PDF 吗？**  
  Aspose.Pdf 可以通过 `Document(string, string)` 提供密码来打开受保护的文件。解密后仍会应用 Bates 工件。

- **我可以同时添加 Bates 编号和普通页码吗？**  
  可以。将 `PageNumberArtifact` 与 `BatesNumberingArtifact` 同时添加即可。每个工件都有各自的计数器。

- **如果我的 PDF 页面尺寸各不相同怎么办？**  
  `Position` 值是绝对点数。对于混合尺寸的文档，可在循环中使用 `page.PageInfo.Width` 和 `page.PageInfo.Height` 计算每页的定位。

## 后续步骤与相关主题

掌握了 **bates numbering tutorial** 后，你可能想进一步探索：

- **添加水印** – 使用 `TextArtifact` 的类似工件方法。
- **合并多个 PDF** – 使用 `Document.AppendDocument`。
- **提取文本用于搜索索引** – `TextAbsorber` 类。
- **批量自动化处理** – 循环遍历文件夹中的 PDF 并应用相同工件。

所有这些主题都基于你刚学到的概念，帮助你进一步扩展 PDF 自动化工具箱。

---

*祝编码愉快！如果遇到问题或有进一步自定义的想法，欢迎在下方留言。PDF 操作的世界很广阔，但有了扎实的 **bates numbering tutorial**，你已经走在前列。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}