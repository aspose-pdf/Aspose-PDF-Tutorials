---
category: general
date: 2026-03-06
description: 在 C# 中创建 PDF 文档并轻松添加 Bates 编号。学习如何添加空白页 PDF、在页面上放置印章以及实现 Bates 编号。
draft: false
keywords:
- create pdf document
- add bates number
- add blank page pdf
- how to add bates numbering
- place stamp on page
language: zh
og_description: 在 C# 中创建 PDF 文档并添加贝茨编号。本指南展示如何添加空白页 PDF、在页面上放置印章以及应用贝茨编号。
og_title: 使用Bates编号创建PDF文档 – C#教程
tags:
- Aspose.Pdf
- C#
- PDF automation
title: 使用 C# 创建带 Bates 编号的 PDF 文档 – 完整指南
url: /zh/net/programming-with-stamps-and-watermarks/create-pdf-document-with-bates-numbering-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 创建带 Bates 编号的 PDF 文档

是否曾经需要在 C# 中 **创建 PDF 文档**，并且想知道如何在不抓狂的情况下添加 Bates 编号？你并非唯一遇到此问题的人——律所、法院，甚至一些企业合规团队每天都面临同样的难题。好消息是？只需几行 Aspose.Pdf 代码，你就可以快速生成一个全新的 PDF，添加空白页，并在一次流畅的操作中盖上正确的 Bates 编号。

在本教程中，我们将完整演示整个过程：从项目设置、添加空白页 PDF、弄清 **how to add bates numbering**，到最终 **place stamp on page** 并保存结果。结束时，你将拥有一个可直接放入任何 .NET 应用的即用代码片段。没有模糊的引用，只有完整可运行的示例。

## 需要的条件

- **.NET 6+**（或 .NET Framework 4.6+ —— Aspose.Pdf 两者均支持）
- **Aspose.Pdf for .NET** NuGet 包 (`Install-Package Aspose.Pdf`)
- 一个合适的 IDE（Visual Studio、Rider 或带 C# 扩展的 VS Code）

就这么简单。无需额外的 DLL，也不需要外部服务。让我们开始吧。

## 步骤 1：创建 PDF 文档 – 初始设置

首先，我们需要一个全新的 `Document` 对象。可以把它看作是所有内容将要存在的空白画布。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Initialize a new PDF document
Document pdfDocument = new Document();
```

> **为什么这很重要：** `Document` 类是每个 Aspose 操作的入口。实例化它后，你可以访问 `Pages` 集合、元数据和安全设置——这些都是构建专业 PDF 的基石。

## 步骤 2：添加空白页 PDF

没有页面的 PDF 就像一本没有页码的书——毫无用处。添加空白页非常简单，并且为我们提供了一个可以盖上 Bates 编号的页面。

```csharp
// Add a single blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **小贴士：** 如果需要多页，只需在循环中调用 `pdfDocument.Pages.Add()`。每次调用都会返回一个全新的 `Page` 对象，你可以独立地进行自定义。

## 步骤 3：如何添加 Bates 编号 – 创建 TextStamp

现在进入关键部分：**Bates number**。在 Aspose.Pdf 中，它只是带有特殊 artifact 标记的 `TextStamp`。

```csharp
// Create a text stamp that will serve as a Bates number
TextStamp batesStamp = new TextStamp("Bates-001")
{
    // Mark the stamp as a Bates‑numbering artifact (helps PDF viewers treat it specially)
    Artifact = ArtifactType.BatesNumbering,
    // Align the stamp to the bottom‑right corner of the page
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Add a small margin so the number isn’t glued to the edge
    Margin = new Margin { Bottom = 10, Right = 10 }
};
```

> **为什么要设置 `Artifact`：** 某些 PDF 阅读器会将 Bates 编号作为可搜索的元数据暴露。将印章标记为 `BatesNumbering` artifact 可确保下游工具自动识别它。

## 步骤 4：在页面上放置印章

印章准备好后，我们现在 **place stamp on page**。这一步骤是将可视化编号实际显示在 PDF 中的过程。

```csharp
// Add the Bates number stamp to the previously created page
page.AddStamp(batesStamp);
```

> **边缘情况：** 如果需要每页的编号递增，你可以遍历 `pdfDocument.Pages` 并在调用 `AddStamp` 前更新 `batesStamp.Value`。此示例保持简单，使用静态的 “Bates‑001”。 

## 步骤 5：保存并验证结果

最后，我们将 PDF 持久化到磁盘。请选择一个你有写入权限的文件夹；否则会抛出 `UnauthorizedAccessException`。

```csharp
// Save the stamped PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/BatesStamped.pdf");
```

当你在任意查看器中打开 `BatesStamped.pdf` 时，应该能看到一个小小的 “Bates‑001” 整齐地位于空白页的右下角。

> **预期输出：**  
> ![PDF with Bates number stamp](image-placeholder.png "PDF with Bates number stamp")  
> *替代文字：PDF 在右下角的 Bates 编号印章.*

如果编号未显示，请仔细检查边距值，并确保页面尺寸不太小（默认 A4 正常）。还要确认 `Artifact` 标记没有被任何后处理工具剥离。

## 完整工作示例

下面是完整的、可直接复制粘贴的程序。它包含所有 `using` 指令和注释，帮助你快速上手。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize a new PDF document
        Document pdfDocument = new Document();

        // 2️⃣ Add a blank page – this is where we’ll put the Bates number
        Page page = pdfDocument.Pages.Add();

        // 3️⃣ Create a TextStamp for the Bates number
        TextStamp batesStamp = new TextStamp("Bates-001")
        {
            Artifact = ArtifactType.BatesNumbering,          // Marks it as a Bates‑numbering artifact
            HorizontalAlignment = HorizontalAlignment.Right, // Align right
            VerticalAlignment = VerticalAlignment.Bottom,    // Align bottom
            Margin = new Margin { Bottom = 10, Right = 10 }  // Small margin from edges
        };

        // 4️⃣ Place the stamp on the page
        page.AddStamp(batesStamp);

        // 5️⃣ Save the PDF to disk
        string outputPath = @"C:\Temp\BatesStamped.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"PDF created successfully: {outputPath}");
    }
}
```

运行程序，打开 PDF，你会看到 Bates 编号正好出现在我们指定的位置。 🎉

## 常见变体与注意事项

| 场景 | 需要更改的内容 | 原因 |
|----------|----------------|-----|
| **多页，递增编号** | 遍历 `pdfDocument.Pages`，在 `AddStamp` 之前设置 `batesStamp.Value = $"Bates-{i:D3}"` | 为每页提供唯一标识符，通常用于法律文档捆绑 |
| **不同位置（左上）** | 将 `HorizontalAlignment = HorizontalAlignment.Left` 和 `VerticalAlignment = VerticalAlignment.Top` 改为相应值 | 有些组织更喜欢将编号放在页眉而非页脚 |
| **自定义字体或颜色** | 设置 `batesStamp.TextState.Font = FontRepository.FindFont("Arial"); batesStamp.TextState.FontSize = 12; batesStamp.TextState.ForegroundColor = Color.Red;` | 提升可读性或符合品牌指南 |
| **将已有 PDF 作为背景添加** | 使用 `Document src = new Document("source.pdf"); pdfDocument.Pages.Add(src.Pages[1]);` 加载源 PDF | 当需要在预生成的表单上盖章时非常有用 |

## 总结

我们刚刚演示了如何使用 Aspose.Pdf for .NET **create PDF document**、**add blank page pdf** 和 **add bates number**，随后 **place stamp on page** 并保存文件。代码特意简洁，便于你在更大的工作流中进行适配——无论是批量处理数十个文件，还是集成到 Web 服务中。

如果你准备进一步深入，可以考虑：

- 为大型案件文件自动化递增逻辑。
- 将 PDF 生成嵌入到 ASP.NET Core API 中。
- 使用 `pdfDocument.Encrypt(...)` 添加安全性（密码保护）。

欢迎随意实验、尝试不同方案，并在评论中提问。祝编码愉快，愿你的 PDF 始终完美盖章！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}