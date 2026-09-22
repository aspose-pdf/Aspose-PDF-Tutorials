---
category: general
date: 2026-02-14
description: 轻松为文档添加 Bates 编号 PDF。了解如何在几分钟内使用 Aspose.Pdf 为页脚添加页码并添加顺序编号 PDF。
draft: false
keywords:
- add bates numbering pdf
- add footer page numbers
- how to add bates numbers
- add sequential numbers pdf
language: zh
og_description: 快速为PDF添加Bates编号。本指南展示如何使用 Aspose.Pdf 为 PDF 添加页脚页码和顺序编号，并提供完整代码和技巧。
og_title: 为 PDF 添加贝茨编号 – 步骤详解 C# 教程
tags:
- Aspose.Pdf
- C#
- PDF automation
title: 在 PDF 中添加贝茨编号 – 完整 C# 指南
url: /zh/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 添加 Bates 编号 PDF – 完整 C# 指南

是否曾需要 **add Bates numbering PDF** 文件，却不知从何入手？你并不孤单。法律团队、审计员以及处理大量文档的人员经常会问：“如何在不破坏布局的情况下添加 Bates 编号？”好消息是，使用 Aspose.Pdf for .NET，你可以将这些编号作为简单的页脚注入——无需手动编辑。

在本教程中，我们将一步步演示一个实用的端到端解决方案，不仅 **adds footer page numbers**，还能 **add sequential numbers PDF** 文件，并支持自定义前缀、字体大小和对齐方式。完成后，你将拥有一个可直接运行的 C# 程序，清晰了解每个设置的意义，以及避免常见陷阱的专业技巧。

## 你将学习的内容

- 如何加载已有的 PDF 并为 Bates 编号做准备。  
- 哪些 **BatesNumberingOptions** 属性控制外观和位置。  
- 如何一次调用为每页应用编号。  
- 如何自定义前缀、起始编号以及不同法律格式的边距。  
- 边缘情况处理——加密 PDF 或已经包含页脚的文档该怎么办。

**先决条件**：.NET 6+（或 .NET Framework 4.7+），最近版本的 Aspose.Pdf（示例使用 23.10），以及你拥有修改权限的输入 PDF。无需其他第三方库。

---

## 第一步 – 加载需要编号的 PDF

首先我们创建一个指向源文件的 `Document` 实例。使用 `using var` 模式可确保文件句柄自动释放。

```csharp
using Aspose.Pdf;

// Replace with the path to your source PDF
using var doc = new Document("YOUR_DIRECTORY/input.pdf");
```

> **为何重要：** Aspose.Pdf 会将整个 PDF 结构读取到内存中，使我们能够在不触碰磁盘上原始文件的情况下操作页面、注释和元数据。如果 PDF 受密码保护，可在构造函数中传入密码——请参阅文末的 “Encrypted PDFs” 说明。

---

## 第二步 – 定义你的 Bates 编号选项

Bates 编号本质上是带有可配置前缀和顺序计数的页面页脚。`BatesNumberingOptions` 类让你可以微调每一个视觉细节。

```csharp
var batesOptions = new BatesNumberingOptions
{
    // The text that will appear before the numeric part
    Prefix = "ABC-",

    // Starting number; the library will increment this automatically
    StartNumber = 1000,

    // Font size of the footer text (points)
    FontSize = 12,

    // Align the number to the right side of the page
    HorizontalAlignment = HorizontalAlignment.Right,

    // Place the number at the bottom of the page
    VerticalAlignment = VerticalAlignment.Bottom,

    // Margins: left, top, right, bottom (in points)
    Margin = new MarginInfo(0, 20, 0, 0)
};
```

### 小技巧

- **Prefix**：使用简短且唯一的标识符（例如案号），以保持页脚可读。  
- **StartNumber**：法律事务所通常从 `1` 开始或使用自定义偏移；请选择符合你归档系统的数字。  
- **Margins**：`20` 点的底部边距可确保文字不与脚注或签名等已靠近页面边缘的内容冲突。

---

## 第三步 – 为所有页面应用编号

配置好选项后，实际注入只需一行代码。Aspose.Pdf 会处理分页、更新已有内容流，并自动遵循页面旋转。

```csharp
doc.Pages.AddBatesNumbering(batesOptions);
```

> **内部原理是什么？** 库会遍历每个 `Page` 对象，创建一个包含前缀和当前计数的 `TextFragment`，随后使用页面的坐标系绘制。由于我们设置了 `HorizontalAlignment.Right` 和 `VerticalAlignment.Bottom`，文本会自动贴靠右下角，无论页面尺寸如何。

---

## 第四步 – 保存修改后的 PDF

最后，将结果写入新文件。虽然可以覆盖原文件，但保留副本有助于版本控制。

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

如果需要保留原始元数据（作者、创建日期），Aspose.Pdf 默认会复制。你也可以指定 `SaveOptions` 对象以实现 PDF/A 合规或压缩。

---

## 完整工作示例

下面是完整的、可直接运行的程序。将其粘贴到控制台应用项目中，调整文件路径后按 **F5** 运行。

```csharp
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using var doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Configure Bates numbering options
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC-",
            StartNumber = 1000,
            FontSize = 12,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(0, 20, 0, 0)
        };

        // 3️⃣ Apply numbering to every page
        doc.Pages.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the output PDF
        doc.Save("YOUR_DIRECTORY/output.pdf");

        System.Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**预期结果：** `output.pdf` 的每一页现在都会在右下角显示类似 `ABC-1000`、`ABC-1001` … 的页脚。使用任意 PDF 阅读器打开即可验证。

---

## 常见变体处理

### 仅添加页脚页码

如果只需要简单的页码而不带前缀，设置 `Prefix = ""`，并根据需要调整边距以避免与已有页脚冲突。

```csharp
batesOptions.Prefix = "";
batesOptions.StartNumber = 1; // classic page numbering
```

### 使用不同的对齐方式

法律文档有时要求编号居中显示在底部。只需切换对齐方式：

```csharp
batesOptions.HorizontalAlignment = HorizontalAlignment.Center;
```

### 处理加密 PDF

当源 PDF 受密码保护时，按如下方式提供密码：

```csharp
using var doc = new Document("secure.pdf", new LoadOptions { Password = "mySecret" });
```

其余工作流程保持不变。

### 跳过已有页脚

如果文档已经包含不想覆盖的页脚，你可以在前面添加自定义字符串使新编号与旧编号区分，或手动遍历页面，仅在不存在页脚的地方添加 `TextFragment`。`Page` 类公开的 `Annotations` 和 `Contents` 集合可实现细粒度控制。

---

## 专业技巧与常见陷阱

- **避免裁剪**：过小的底部边距可能导致打印时文字被切掉。若要分发纸质版，请进行实际打印测试。  
- **性能**：在现代笔记本上为 500 页 PDF 添加 Bates 编号耗时不到一秒，但大批量处理时可考虑并行——只需记住 `Document` 不是线程安全的，每个线程需要各自的实例。  
- **版本兼容性**：代码适用于 Aspose.Pdf 23.10 及以上版本。若使用旧版，属性名称相同，但 `MarginInfo` 构造函数可能需要 `float` 参数。  
- **法律合规**：某些司法辖区要求 Bates 编号放置在特定位置（例如左下角），只需相应调整 `HorizontalAlignment` 即可。

---

## 结论

我们已经演示了如何使用 Aspose.Pdf for .NET **add Bates numbering PDF** 文件，涵盖了从加载文档到保存带有整洁页脚的最终版本的全部步骤。通过微调少数属性，你同样可以 **add footer page numbers**、**add sequential numbers PDF**，或自定义外观以满足任何法律标准。

准备好下一步了吗？尝试将此技术与 OCR 文本提取结合，在 Bates 编号旁嵌入可搜索关键字，或使用 `Directory.GetFiles` 自动处理整个文件夹。可能性无限，而你现在拥有的基础将使这些扩展轻而易举。

祝编码愉快，愿你的 PDF 永远编号准确！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}