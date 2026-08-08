---
category: general
date: 2026-03-27
description: 快速在 C# 中添加 Bates 编号。了解如何添加自定义页码、顺序页码以及向 Word 文档添加自定义编号。
draft: false
keywords:
- add bates numbering
- how to add bates
- add custom page numbers
- add sequential page numbers
- add custom numbers
language: zh
og_description: 在 C# 中添加 Bates 编号并提供清晰示例。本指南展示如何添加自定义页码、顺序页码等。
og_title: 在 C# 中添加贝茨编号 – 完整教程
tags:
- C#
- Document Processing
- Bates Numbering
title: 在 C# 中添加贝茨编号 – 步骤指南
url: /zh/net/programming-with-pdf-pages/add-bates-numbering-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中添加 Bates 编号 – 步骤指南

有没有想过如何 **添加 Bates 编号** 到 Word 文档而不抓狂？你并不是唯一的困惑者。在许多法律或合规项目中，每页都需要一个唯一标识，手工操作简直是噩梦。

在本教程中，我们将演示一个完整、可运行的示例，**添加 Bates 编号**，展示 **几行代码如何添加 Bates**，并且还涵盖 **添加自定义页码** 与 **添加顺序页码** 的方法。完成后，你将得到一个带有指定编号的 .docx 文件——无需第三方工具。

## 你将学到

- 使用 Aspose.Words for .NET API（或任何兼容库）加载 DOCX 文件。  
- 配置 **添加自定义数字**，如前缀、起始值和字体大小。  
- 一次调用即可将编号应用到每一页。  
- 保存结果并验证编号是否如预期显示。  

不需要任何 Bates 编号的先前经验；只要有基本的 C# 环境和一份源文档即可。让我们开始吧。

## 前置条件

- .NET 6+（代码在 .NET Core 和 .NET Framework 上均可运行）。  
- 通过 NuGet 安装 Aspose.Words for .NET (`Install-Package Aspose.Words`)。  
- 将名为 `input.docx` 的 Word 文档放在可引用的文件夹中（`YOUR_DIRECTORY`）。  
- Visual Studio、VS Code 或任意你喜欢的 C# IDE。

> **专业提示：** 如果使用其他库（例如 Open XML SDK），概念保持不变——只需替换 API 调用即可。

## 第一步：加载源文档

首先需要将 Word 文件加载到内存中。

```csharp
using Aspose.Words;

// Step 1: Load the source document
Document document = new Document("YOUR_DIRECTORY/input.docx");
```

*为什么重要：* 加载文件会创建一个 `Document` 对象，借此可以访问页面、章节以及底层节点树。没有它，就无法附加任何编号。

## 第二步：配置 Bates 编号选项

接下来定义编号的具体显示方式。这一步就是 **添加自定义页码** 或 **添加顺序页码** 的地方。

```csharp
// Step 2: Define Bates numbering options (prefix, start number, font size)
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Prefix that appears before every number, e.g., "ABC"
    Prefix = "ABC",
    // The first number in the sequence; change to 1 if you prefer
    Start = 1000,
    // Font size in points; 9 works well for most legal docs
    FontSize = 9
};
```

*为什么重要：* `Prefix` 让你 **添加自定义数字**（如案件编号），`Start` 决定初始计数。修改 `FontSize` 可防止数字侵占页面边距。

## 第三步：将 Bates 编号应用到每一页

选项准备好后，告诉库为每页加上编号。

```csharp
// Step 3: Apply Bates numbering to all pages of the document
document.Pages.AddBatesNumbering(batesOptions);
```

*为什么重要：* `AddBatesNumbering` 方法会遍历内部页面集合，在右下角（默认位置）插入文本框。这正是 **如何添加 Bates** 而无需自行编写循环的核心。

## 第四步：保存更新后的文档

最后，将修改后的文件写回磁盘。

```csharp
// Step 4: Save the updated document
document.Save("YOUR_DIRECTORY/output.docx");
```

*为什么重要：* 保存会生成一个新的 `output.docx`，你可以在 Word、LibreOffice 或任意查看器中打开，确认编号是否出现。

## 预期结果

打开 `output.docx`。每页应显示类似以下内容：

```
ABC‑1000   (on page 1)
ABC‑1001   (on page 2)
ABC‑1002   (on page 3)
...
```

如果打开文档的打印预览，你会看到右下角的编号，字体大小与设置相符。

## 边缘情况与变体

| 情况 | 需要更改的内容 | 原因 |
|-----------|----------------|-----|
| **不需要前缀** | `Prefix = string.Empty` | 移除 “ABC‑” 部分，仅保留数字序列。 |
| **从 1 开始** | `Start = 1` | 适用于简单的 **添加顺序页码**，无需自定义前缀。 |
| **大文档（>10,000 页）** | 增大 `FontSize` 或调整 `Location`（使用 `AddBatesNumbering` 的重载） | 防止与页脚或页眉重叠。 |
| **只读源文件** | 使用允许写入的 `LoadOptions` 打开，或先复制文件 | 否则 `document.Save` 会抛出异常。 |
| **不同的放置位置** | `batesOptions.Position = BatesNumberingPosition.TopLeft`（或其他枚举） | 有些公司要求编号位于页面顶部。 |

> **注意：** 并非所有库都提供 `BatesNumberingOptions` 类。使用 Open XML SDK 时，需要手动插入 `TextBox`——原理相同，只是代码更多。

## 完整工作示例

下面是一段完整的程序代码。复制粘贴到控制台应用并运行即可。

```csharp
using System;
using Aspose.Words;

class Program
{
    static void Main()
    {
        // Load the source document
        Document document = new Document("YOUR_DIRECTORY/input.docx");

        // Define Bates numbering options
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC",      // custom prefix
            Start = 1000,        // starting number
            FontSize = 9         // font size in points
        };

        // Apply numbering to every page
        document.Pages.AddBatesNumbering(batesOptions);

        // Save the result
        document.Save("YOUR_DIRECTORY/output.docx");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

运行程序，打开 `output.docx`，你会看到编号正好出现在预期位置。 🎉

## 常见问答

**问：可以更改数字的颜色吗？**  
答：可以。在调用 `AddBatesNumbering` 后，获取生成的 `Shape` 对象并设置其 `FillColor` 属性。

**问：如果想把编号放在左侧而不是右侧怎么办？**  
答：使用 `batesOptions.Position = BatesNumberingPosition.BottomLeft`（或 `TopLeft`, `TopRight`）。API 支持四个角落的所有位置。

**问：这能输出为 PDF 吗？**  
答：完全可以。添加编号后，调用 `document.Save("output.pdf")`。数字会像在 Word 中一样渲染到 PDF 中。

## 结论

现在你已经掌握了 **如何在 C# 中为 Word 文件添加 Bates 编号**。本教程涵盖了加载文档、配置 **添加自定义数字**、应用 **添加顺序页码**，以及保存最终结果。借助完整代码示例，你可以将其直接嵌入任何项目，立即开始给文档加盖编号。

准备好迎接下一个挑战了吗？尝试将其与批处理器结合，对文件夹中的多个文件循环处理，或在页眉/页脚中 **添加自定义页码** 以获得更精致的效果。无论哪种方式，你都已经为任何法律科技或合规自动化任务奠定了坚实基础。

有问题或酷炫的使用案例？在下方留言吧，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}