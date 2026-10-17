---
category: general
date: 2026-06-21
description: 在 Word 中快速添加 Bates 编号。学习如何添加 Bates 编号、在法律文档中应用 Bates 编号，并使用 C# 自动化编号。
draft: false
keywords:
- add bates numbering
- how to add bates
- bates numbering in word
- bates numbering for legal
- apply bates numbering
language: zh
og_description: 使用 C# 在 Word 中添加 Bates 编号。本指南展示了如何添加 Bates 编号、为法律文档应用 Bates 编号以及自动化此过程。
og_title: 在 Word 中添加贝茨编号 – 完整编程演练
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  headline: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  name: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: '| Page | Bates Number | |------|--------------| | 1 | ABC-1000 | | 2 |
      ABC-1001 | | … | … | | N | ABC‑(1000 + N‑1) |'
  - name: What if the document already contains page numbers?
    text: The `AddBatesNumbering` method will **not** overwrite existing page number
      fields; it simply adds a new field. If you want to replace the existing numbers,
      remove them first or set `batesOptions.Position` to the same location as the
      current page numbers.
  - name: Can I skip pages (e.g., exclude a cover page)?
    text: 'Yes. Use the overload that accepts a `PageRange`:'
  - name: How do I change the numbering format (Roman numerals, letters)?
    text: 'The `BatesNumberingOptions` class supports a `NumberFormat` property:'
  - name: What about performance on huge files?
    text: Loading a 2‑GB Word file can consume a lot of RAM. To mitigate, process
      the document in chunks using the `DocumentSplitter` utility, apply Bates numbering
      to each chunk, then merge the parts back together. This pattern keeps memory
      usage under control while still letting you **apply bates numbering*
  type: HowTo
tags:
- document‑automation
- csharp
- legal‑tech
title: 在 Word 中添加贝茨编号 – 完整的逐步指南
url: /zh/net/programming-with-document/add-bates-numbering-in-word-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Word 中添加 Bates 编号 – 完整分步指南

是否曾想过如何在 Word 文件中添加 Bates 编号而不必手动输入每个数字？你并不孤单。许多律师、律师助理和电子发现专家都需要一种可靠的方式来 **添加 Bates 编号** 到数百页文档，手工操作简直是噩梦。

在本教程中，我们将演示一个简洁的 C# 解决方案，**为 .docx 文件应用 Bates 编号**，解释每行代码的意义，并展示如何根据法律需求对代码进行微调。完成后，你将在几秒钟内生成编号完好的文档——无需额外插件。

## 你将学到的内容

- 添加 **Bates 编号** 到 Word 文档的完整代码。
- `BatesNumberingOptions` 类的工作原理以及何时调整前缀或起始值。
- 在大型案件文件上使用此方法的技巧，包括内存方面的考虑。
- 前置条件快速概览，帮助你复制粘贴代码并立即运行。

**前置条件**  
- .NET 6+（或如果你更喜欢旧版运行时，可使用 .NET Framework 4.7.2+）。  
- 引用 Aspose.Words for .NET 库（或任何提供 `AddBatesNumbering` 的类似 API）。  
- 对 C# 和 Visual Studio（或你喜欢的 IDE）有基本了解。

如果你已经满足上述条件，下面开始吧。

## 第一步：创建项目并导入库

首先，新建一个控制台应用（或集成到已有服务中），然后添加 Aspose.Words NuGet 包：

```bash
dotnet add package Aspose.Words
```

> **小技巧：** 使用免费评估许可证进行测试；它会添加一个小水印，但功能与正式版完全相同。

```csharp
using Aspose.Words;
using Aspose.Words.BatesNumbering;
```

这些 `using` 语句将 `Document` 和 `BatesNumberingOptions` 类引入作用域，是后续 **应用 Bates 编号** 步骤的关键。

## 第二步：加载源文档

你需要一个 Word 文件作为操作对象。下面的代码从指定文件夹加载 `input.docx`。将 `"YOUR_DIRECTORY"` 替换为你机器上的实际路径。

```csharp
// Step 1: Load the source document
var document = new Document("YOUR_DIRECTORY/input.docx");
```

为什么要先加载文件？`Document` 对象会将整个 Word 包解析到内存中，便于我们在保存前操作页眉、页脚和页面布局。如果文件非常庞大（比如 10,000 页），可以考虑使用 `LoadOptions` 并指定 `LoadFormat.Docx` 来分块读取，而不是一次性全部加载。

## 第三步：配置 Bates 编号选项

这一步是核心。你告诉库使用什么前缀（示例中为 `"ABC-"`）以及从哪个数字开始计数（`1000`）。这两个值均可自定义。

```csharp
// Step 2: Define Bates numbering options (prefix and starting number)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",
    Start = 1000,
    // Optional: set the position, alignment, and font if you need legal‑specific styling
    // Position = BatesNumberingPosition.Footer,
    // Alignment = BatesNumberingAlignment.Right,
    // Font = new Font("Times New Roman", 10, FontStyle.Bold)
};
```

**为什么需要前缀？** 在法律实践中，前缀常用于标识案件或出具方（例如 `"ABC-"` 可能代表 *Acme Bank Corp.*）。从 `1000` 开始很常见，因为许多事务所会把前 999 个号码保留给内部草稿。

如果你处理的是 **法律文档的 Bates 编号**，还可以将 `batesOptions.Position` 设置为 `Header` 或 `Footer`，并根据法院规则调整对齐方式。库本身已支持这些配置。

## 第四步：对整个文档应用 Bates 编号

现在真正注入编号。`AddBatesNumbering` 方法会遍历每一页，插入格式化后的字符串，并更新文档内部的页码计数。

```csharp
// Step 3: Apply Bates numbering to the entire document
document.AddBatesNumbering(batesOptions);
```

在内部，Aspose.Words 会在每页创建一个隐藏字段，渲染为 `ABC-1000`、`ABC-1001` 等。因为是字段，后续如果需要更改前缀或起始号码，无需重新生成整个文件——这对 **在发现请求变更后如何添加 Bates** 非常便利。

## 第五步：保存修改后的文档

最后，将结果写入新文件。保持原始文件不变是最佳实践，尤其在处理必须保持原样的证据时。

```csharp
// Step 4: Save the modified document
document.Save("YOUR_DIRECTORY/output.docx");
```

现在你拥有了 `output.docx`，其中每页都附加了顺序递增的 Bates 编号。用 Word 打开，你会看到编号正好出现在你指定的位置（默认是页脚）。文件体积可能会因额外字段略有增加，但相对于带来的好处可以忽略不计。

### 预期输出

| 页码 | Bates 编号 |
|------|------------|
| 1    | ABC-1000   |
| 2    | ABC-1001   |
| …    | …          |
| N    | ABC‑(1000 + N‑1) |

如果在 Word 中切换到“域代码”视图（`Alt+F9`），每页会显示类似 `{ BATES \* MERGEFORMAT ABC-1000 }` 的内容。

## 边缘情况与常见问题

### 文档已经包含页码怎么办？

`AddBatesNumbering` 方法 **不会** 覆盖已有的页码字段；它只会添加新的字段。如果想替换已有页码，需要先删除旧字段，或将 `batesOptions.Position` 设置为与当前页码相同的位置。

### 能否跳过某些页（例如封面页）？

可以。使用接受 `PageRange` 参数的重载：

```csharp
var range = new PageRange(2, document.PageCount); // start at page 2
document.AddBatesNumbering(batesOptions, range);
```

这在需要 **法律文稿的 Bates 编号** 从标题页之后才开始时非常有用。

### 如何更改编号格式（罗马数字、字母等）？

`BatesNumberingOptions` 类提供 `NumberFormat` 属性：

```csharp
batesOptions.NumberFormat = BatesNumberFormat.RomanUpper;
```

在调用 `AddBatesNumbering` 之前设置即可。此灵活性帮助满足法院对特定样式的要求。

### 大文件的性能如何？

加载一个 2 GB 的 Word 文件会占用大量内存。为降低内存占用，可使用 `DocumentSplitter` 工具将文档分块处理，对每块应用 Bates 编号后再合并。该模式在保持 **应用 Bates 编号** 高效的同时，能够控制内存使用。

## 完整工作示例

将上述所有步骤整合，下面是一个可直接运行的控制台程序：

```csharp
using System;
using Aspose.Words;
using Aspose.Words.BatesNumbering;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            var inputPath = @"C:\Docs\input.docx";
            var document = new Document(inputPath);

            // 2️⃣ Define Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                // Optional styling for legal compliance
                Position = BatesNumberingPosition.Footer,
                Alignment = BatesNumberingAlignment.Right,
                Font = new Font("Times New Roman", 9, FontStyle.Bold)
            };

            // 3️⃣ Apply Bates numbering across all pages
            document.AddBatesNumbering(batesOptions);

            // 4️⃣ Save the result
            var outputPath = @"C:\Docs\output.docx";
            document.Save(outputPath);

            Console.WriteLine($"✅ Bates numbering applied! Saved to {outputPath}");
        }
    }
}
```

运行程序，打开 `output.docx`，即可看到整齐的编号系列，适用于归档、发现或法院提交。

## 结论

现在你已经掌握了使用 C# **向 Word 文档添加 Bates 编号** 的完整方法。加载、配置、应用、保存四个步骤既简洁又足够灵活，能够满足 **法律领域的 Bates 编号** 工作流、定制前缀以及大规模批处理的需求。

如果想进一步扩展，可考虑：

- 将代码集成到 Web API，让同事上传文件并即时获取带编号的 PDF。  
- 为缺失文件或权限问题添加错误处理（在 `Document.Load` 周围加入 `try/catch`）。  
- 探索 Aspose.Words 的其他功能，如水印或编辑遮蔽，以构建完整的电子发现工具套件。

欢迎尝试不同的前缀、起始号码，甚至在同一文档中组合多种编号方案。掌握了核心逻辑后，**应用 Bates 编号** 的可能性出乎意料地广阔。

有问题或遇到棘手场景？在下方留言，我们一起排查。祝编码愉快！


## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在已有技巧的基础上进一步提升。每篇资源都提供完整可运行的代码示例，并配有逐步解释，助你掌握更多 API 功能并探索替代实现方式。

- [Apply Numbering Style in Heading of PDF using Java](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/french/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}