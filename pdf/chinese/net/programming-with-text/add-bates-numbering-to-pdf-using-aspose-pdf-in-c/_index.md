---
category: general
date: 2026-09-27
description: 使用 Aspose.PDF 在 C# 中为 PDF 添加 Bates 编号。了解如何加载 PDF 文档、设置 Bates 编号选项并保存更新后的文件。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- load pdf document
- how to add bates numbering
- Aspose.PDF C#
- PDF Bates numbering example
language: zh
lastmod: 2026-09-27
og_description: 使用 Aspose.PDF 在 C# 中为 PDF 添加 Bates 编号。本教程展示了如何加载 PDF 文档、配置 Bates 编号并保存结果。
og_image_alt: Screenshot of a PDF page displaying Bates numbers in the footer
og_title: 使用 Aspose.PDF 为 PDF 添加贝茨编号 – C# 指南
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Add bates numbering to PDF using Aspose.PDF in C#. Learn how to load
    a PDF document, set Bates numbering options, and save the updated file.
  headline: Add bates numbering to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF processing
title: 使用 Aspose.PDF 在 C# 中为 PDF 添加 Bates 编号
url: /zh/net/programming-with-text/add-bates-numbering-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中使用 Aspose.PDF 为 PDF 添加 Bates 编号

如果您需要**为 PDF 文件添加 Bates 编号**，本指南将向您展示一个完整、可直接运行的解决方案。您将看到如何**加载 PDF 文档**、配置 Bates 编号选项，并将带编号的文件写回磁盘——全部使用 Aspose.PDF for .NET。

在法律、执法和档案工作流中，应用 Bates 编号是常见需求。完成本教程后，您可以在每页嵌入顺序标识符，定制前缀，并从任意数字开始计数。

## 您将学习的内容

* 如何将 **PDF 文档** 内容加载到 `Aspose.Pdf.Document` 对象中。  
* 使用 `BatesNumberingOptions` **添加 Bates 编号** 的完整步骤。  
* 如何在保持原始布局和质量的前提下保存修改后的文件。  

无需任何外部工具——只需 Aspose.PDF NuGet 包和 .NET 开发环境（Visual Studio、VS Code 或 Rider）。

---

## Step 1: Install Aspose.PDF for .NET

在终端中打开项目文件夹并运行：

```bash
dotnet add package Aspose.PDF
```

该包包含 `Aspose.Pdf` 命名空间，提供本教程中使用的所有类。安装完成后，重新加载项目，使 IDE 能识别新的引用。

## Step 2: Load PDF document

加载源文件是第一步，因为 Bates 编号引擎需要在已有的 `Document` 实例上工作。

```csharp
using Aspose.Pdf;

// ...

// Replace with the path to your input PDF
string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Load the PDF document into memory
Document doc = new Document(inputPath);
```

**为什么重要：** `Document` 类会解析 PDF 结构，让您可以访问页面、注释和元数据。若未先加载文件，就无法应用任何编号。

## Step 3: Configure Bates numbering options

创建 `BatesNumberingOptions` 对象并设置所需的前缀、起始编号以及可选的格式参数。

```csharp
using Aspose.Pdf;

// ...

BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Text that appears before the numeric part
    Prefix = "CASE01",

    // First number to use (1 means the first page gets CASE01-1)
    StartNumber = 1,

    // Optional: customize the appearance
    // The default places the number in the footer, centered.
    // You can change Font, FontSize, Color, and Position if needed.
    // Example:
    // Font = FontRepository.FindFont("Arial"),
    // FontSize = 10,
    // Color = Color.Black,
    // Margin = new Margin(0, 0, 0, 20)
};
```

**为什么重要：** `BatesNumberingOptions` 告诉 Aspose.PDF 如何为每页生成标签。`Prefix` 用于对相关案件进行分组，`StartNumber` 则可让您从前一次批次的序号继续。

## Step 4: Save the PDF with Bates numbers applied

将选项对象传递给 `Save` 方法。Aspose.PDF 会直接在每页上写入编号。

```csharp
// Replace with the desired output path
string outputPath = @"YOUR_DIRECTORY\output.pdf";

// Save the document, applying the Bates numbering
doc.Save(outputPath, batesOptions);
```

**为什么重要：** `Save(string, BatesNumberingOptions)` 重载将渲染步骤与编号过程合并，确保输出文件中包含可见的标识符。

## Full example – everything together

下面是一个完整的、可自行复制、粘贴并运行的程序示例，演示了**从头到尾添加 Bates 编号**的全过程。

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the PDF document
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Set up Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                Prefix = "CASE01",
                StartNumber = 1,
                // Optional appearance tweaks:
                // Font = FontRepository.FindFont("Times New Roman"),
                // FontSize = 9,
                // Color = Color.DarkBlue,
                // Margin = new Margin(0, 0, 0, 15)
            };

            // 3️⃣ Save the document with Bates numbers
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath, batesOptions);

            Console.WriteLine($"Bates numbering added. Output saved to: {outputPath}");
        }
    }
}
```

### Expected output

运行程序后会生成 `output.pdf`，每页显示类似以下的标签：

```
CASE01-1
CASE01-2
CASE01-3
...
```

默认情况下，编号出现在页脚；您可以通过调整 `BatesNumberingOptions` 中的 `Margin` 属性来移动它们的位置。

## Edge cases and common variations

| 情况 | 需要调整的内容 |
|-----------|----------------|
| **每批次不同前缀** | 在调用 `Save` 前更改 `Prefix`。可以对多个文档循环使用不同的前缀。 |
| **从上一个文件继续编号** | 将 `StartNumber` 设置为上次使用的数字 + 1。 |
| **将编号放在页眉** | 使用 `batesOptions.Margin = new Margin(20, 0, 0, 0);`（上边距）或自定义 `batesOptions.Position`。 |
| **自定义字体或颜色** | 如注释部分所示，分配 `Font`、`FontSize` 和 `Color` 属性。 |
| **大型 PDF（1000+ 页）** | 操作内存效率高；但可在保存前调用 `doc.OptimizeResources()` 以减小文件体积。 |

**技巧提示：** 如果您的工作流需要对每个文档使用不同的编号方案，可将逻辑封装到辅助方法中：

```csharp
static void ApplyBatesNumbering(string src, string dst, string prefix, int start)
{
    var doc = new Document(src);
    var opts = new BatesNumberingOptions { Prefix = prefix, StartNumber = start };
    doc.Save(dst, opts);
}
```

## Conclusion

您现在已经掌握了**使用 Aspose.PDF 在 C# 中为任意 PDF 添加 Bates 编号**的方法。教程涵盖了加载 PDF 文档、配置编号选项以及保存最终文件——全部在一个可执行程序中完成。

接下来，您可以进一步探索 **添加水印**、**合并多个 PDF** 或 **提取文本** 等相关主题。尝试不同的字体、颜色和位置，以符合贵组织的格式标准。

准备好自动化您的法律文档工作流了吗？将代码加入构建流水线，对批量文件运行，让 Aspose.PDF 处理繁重任务。祝编码愉快！

## 接下来您可以学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您在项目中进一步运用 API 功能并探索替代实现方式，每篇资源均提供完整可运行的代码示例和逐步解释。

- [Create PDF Document C# – Add Bates Numbering](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/)
- [Add Bates Numbering PDF – Step‑by‑Step Guide to Number PDF Pages](/pdf/english/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/)
- [Aspose PDF Tutorial – Insert a Blank Page and Update Bates Numbering](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}