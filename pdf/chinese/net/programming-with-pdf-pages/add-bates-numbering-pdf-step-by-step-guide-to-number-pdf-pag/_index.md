---
category: general
date: 2026-03-03
description: 快速为 PDF 添加 Bates 编号，并学习如何使用 Aspose.Pdf 在 C# 中对 PDF 页面进行编号或添加顺序编号。
draft: false
keywords:
- add bates numbering pdf
- number pdf pages
- add sequential pdf numbers
- pdf bates numbering tutorial
- aspnet pdf automation
language: zh
og_description: 在 C# 中为 PDF 添加 Bates 编号，以对 PDF 页面进行编号并添加顺序编号。完整代码、解释和最佳实践。
og_title: 为 PDF 添加 Bates 编号 – 完整 C# 教程
tags:
- PDF
- C#
- Aspose.Pdf
- Document Automation
title: 为 PDF 添加贝茨编号 – PDF 页面编号的逐步指南
url: /zh/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 添加 Bates 编号 PDF – 完整 C# 教程

是否曾需要 **add bates numbering pdf** 文件却不知从何入手？你并不孤单——法律团队、审计员和档案管理员都面临同样的问题。好消息是，只需几行 C# 代码和 Aspose.Pdf 库，你就可以 **number pdf pages** 自动编号，并且还能灵活地 **add sequential pdf numbers**，支持自定义前缀、后缀和位置。

在本指南中，我们将通过一个真实案例，解释每个设置为何重要，并展示如何针对不同页面尺寸或自定义位数等边缘情况进行微调。完成后，你将拥有一个可直接运行的代码片段，能够为任何 PDF 添加 Bates 编号，并且了解每个选项背后的“原因”。

## 前置条件

在开始之前，请确保你具备：

- .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.6+）
- 有效的 Aspose.Pdf for .NET 许可证（或免费评估密钥）
- Visual Studio 2022（或任意你喜欢的 C# 编辑器）
- 一个名为 `source.pdf` 的源 PDF，放在可引用的文件夹中

就这些——不需要除 Aspose.Pdf 之外的其他 NuGet 包。

## 第一步 – 打开源 PDF 文档

首先需要加载要加盖的 PDF。使用 `using` 块可以确保文件句柄被正确释放，避免后续的锁定问题。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the original PDF
using (var pdfDocument = new Document(@"C:\MyDocs\source.pdf"))
{
    // The rest of the steps will go inside this block.
}
```

> **为什么重要：** 在 `using` 语句中打开文档可确保确定性释放。如果省略，文件可能会保持锁定状态，后续保存或删除 PDF 时会失败——这在生产流水线中常常导致头疼。

## 第二步 – 配置 Bates 编号选项

现在告诉 Aspose 我们希望 Bates 编号的外观。每个属性直接映射到页面上的视觉元素。

```csharp
// Step 2: Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    Prefix = "2025-",               // Text before the number
    Suffix = "-A",                  // Text after the number
    Start = 5000,                   // First number in the sequence
    NumberOfDigits = 5,             // Pads with leading zeros (e.g., 05000)
    Placement = BatesNumberPlacement.BottomRight // Where the number appears
};
```

### 选项快速提示

| Property | 功能说明 | 何时修改 |
|----------|----------|----------|
| **Prefix / Suffix** | 在数字部分前后添加静态文本。 | 使用案件 ID、项目代码，或在机密文档前加 “CONF‑”。 |
| **Start** | 系列的起始数字。 | 若需延续上一批次的编号方案，请相应设置。 |
| **NumberOfDigits** | 控制前导零填充。 | 法律文件常需恰好 6 位数字；此时设为 `6`。 |
| **Placement** | BottomRight、BottomLeft、TopRight、TopLeft、Center。 | 根据文档布局选择；BottomRight 是最常用的 Bates 编号位置。 |

> **专业提示：** 若需在多列中 **number pdf pages**，可以使用不同的 `Placement` 值和不同的 `Prefix`，调用 `pdfDocument.AddBatesNumbering` 两次。

## 第三步 – 将 Bates 编号应用到文档

准备好选项后，实际的盖章只需一次方法调用。Aspose 在内部处理分页、旋转和边距计算。

```csharp
// Step 3: Apply the numbering to every page
pdfDocument.AddBatesNumbering(batesOptions);
```

> **为何一次调用即可：** 在内部，Aspose 会遍历 `pdfDocument.Pages`，为每页创建一个 `TextFragment`，并根据你选择的 `Placement` 进行定位。这一抽象省去了手写循环和坐标转换的麻烦。

## 第四步 – 保存更新后的 PDF

最后，将修改后的文件写入磁盘。你可以覆盖原文件，也可以生成新文件；下面的示例会创建一个全新的副本。

```csharp
// Step 4: Persist the changes
pdfDocument.Save(@"C:\MyDocs\bates_numbered.pdf");
```

如果需要 **add sequential pdf numbers** 到流中（例如通过 API 发送文件），请将文件路径替换为 `MemoryStream`：

```csharp
using var output = new MemoryStream();
pdfDocument.Save(output);
output.Position = 0; // Reset for downstream consumption
```

## 完整可运行示例

将上述所有步骤组合起来，下面是完整的、可直接运行的程序：

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Open the source PDF
        using (var pdfDocument = new Document(@"C:\MyDocs\source.pdf"))
        {
            // Configure Bates numbering
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "2025-",
                Suffix = "-A",
                Start = 5000,
                NumberOfDigits = 5,
                Placement = BatesNumberPlacement.BottomRight
            };

            // Apply the numbering
            pdfDocument.AddBatesNumbering(batesOptions);

            // Save the result
            pdfDocument.Save(@"C:\MyDocs\bates_numbered.pdf");
        }

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

### 预期输出

- 在 `C:\MyDocs` 中会生成一个新文件 `bates_numbered.pdf`。
- 每页右下角会显示类似 `2025-05000-A`、`2025-05001-A` … 的文字。
- 编号会零填充至五位数字，符合 `NumberOfDigits` 设置。

## 常见变体处理

### 1. 不同页面尺寸

如果 PDF 中混有纵向和横向页面，可能会出现编号在宽边被裁剪的情况。此时请启用 `AutoFit` 属性：

```csharp
batesOptions.AutoFit = true; // Adjusts font size to fit within page margins
```

### 2. 自定义字体或颜色

默认的 Bates 编号为黑色、12 pt Times New Roman。通过访问 `TextState` 可更改外观：

```csharp
batesOptions.TextState = new TextState
{
    FontSize = 10,
    Font = FontRepository.FindFont("Courier New"),
    ForegroundColor = Color.GetBlue()
};
```

### 3. 跳过特定页面

如果想 **number pdf pages** 时跳过封面页，可使用页面范围：

```csharp
pdfDocument.AddBatesNumbering(batesOptions, new PageNumbering { Start = 2 });
```

### 4. 添加多套编号方案

法律团队有时需要同时添加 Bates 编号和机密水印。只需对不同的 `Placement` 值调用两次 `AddBatesNumbering`：

```csharp
// First scheme – bottom right
pdfDocument.AddBatesNumbering(batesOptions);

// Second scheme – top left, different prefix
var confidentialOptions = new BatesNumberingOptions
{
    Prefix = "CONF-",
    Start = 1,
    NumberOfDigits = 4,
    Placement = BatesNumberPlacement.TopLeft,
    TextState = new TextState { FontSize = 8, ForegroundColor = Color.GetRed() }
};
pdfDocument.AddBatesNumbering(confidentialOptions);
```

## 常见问答

**问：这能否处理已经有文字的 PDF？**  
答：可以。Aspose 会将 Bates 编号作为独立图层添加，原有内容保持不变。如果需要让编号出现在已有文字的**后面**（极少见），则必须手动操作页面的内容流。

**问：如果 PDF 有密码保护怎么办？**  
答：先使用密码加载：`new Document(path, new LoadOptions { Password = "secret" })`。盖章后，可通过 `pdfDocument.Encrypt(...)` 重新加密。

**问：可以在 .NET Core 控制台应用中使用吗？**  
答：完全可以。相同代码在 .NET Core、.NET 5+ 以及 .NET Framework 中均可运行，只需引用相应的 Aspose.Pdf NuGet 包。

## 结论

我们已经介绍了如何 **add bates numbering pdf** 文件，如何 **number pdf pages**，以及如何 **add sequential pdf numbers**，并对格式、位置和边缘情况提供了完整控制。上面的简短代码片段完成了主要工作，而额外选项则让你能够将该方案适配到任何法律、档案或合规工作流中。

准备好进一步探索了吗？可以尝试以下方向：

- **批量处理** – 循环遍历文件夹中的 PDF，统一应用编号方案。
- **动态前缀** – 从数据库读取案件 ID，并在每个文档中注入。
- **PDF/A 合规** – 编号后调用 `pdfDocument.Convert(..., PdfFormat.PdfA2b)`，确保长期保存。

欢迎实验、分享你的发现，或在评论区提问。祝编码愉快，愿你的 PDF 永远井然有序！

![PDF 页面底部右侧带有 Bates 编号的截图](https://example.com/images/bates-numbered.png "add bates numbering pdf example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}