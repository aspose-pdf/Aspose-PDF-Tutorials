---
category: general
date: 2026-03-14
description: 使用 Aspose.Pdf 在 C# 中为 PDF 添加贝茨编号。了解如何为法律或归档文件自动添加贝茨编号和顺序页码。
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- Aspose PDF Bates artifact
- C# PDF automation
language: zh
og_description: 逐步为 PDF 添加 Bates 编号。本教程展示如何使用 Aspose.Pdf for .NET 添加 Bates 编号和顺序页码。
og_title: 在 C# 中为 PDF 添加贝茨编号 – 完整指南
tags:
- Aspose.Pdf
- C#
- PDF
- Bates numbering
title: 在 C# 中为 PDF 添加贝茨编号 – 完整指南
url: /zh/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

.

Also need to translate headings.

Also need to translate bullet points.

Make sure not to translate code block placeholders.

Also need to keep the shortcodes at top and bottom.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 添加 Bates 编号 PDF – 完整教程

是否曾经需要在庞大的法律文档包中 **添加 Bates 编号 PDF**，却不知从何入手？为文档审阅工作流添加 Bates 编号是常规操作，但实际上相当繁琐。好消息是？使用 Aspose.Pdf for .NET，你只需几行代码即可实现全自动化。

在本指南中，我们将逐步演示 **如何为 PDF 的每一页添加 Bates 编号**，讨论 **添加顺序页码** 的选项，并提供可直接运行的代码示例。完成后，你将拥有一个可直接嵌入任何 C# 项目的完整解决方案——无需额外脚本，也无需手动盖章。

## 所需条件

- **Aspose.Pdf for .NET**（版本 23.10 或更高）。该库为商业授权，但免费评估版足以用于测试。
- .NET 开发环境（Visual Studio、Rider 或 `dotnet` CLI）。
- 需要标记的输入 PDF（`input.pdf`）。
- 对偶发的边缘情况保持一点耐心（我们会一并覆盖）。

如果这些都已准备好，太好了——我们开始吧。

![添加 Bates 编号 PDF 示例](/images/bates-numbering-example.png "显示已应用添加 Bates 编号 PDF 的 PDF 截图")

## 第一步：创建项目并安装 Aspose.Pdf

为了保持整洁，先新建一个控制台应用：

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

`dotnet add package` 命令会从 NuGet 拉取最新的 Aspose.Pdf 程序集，随后即可开始编写代码。

### 为什么选择控制台应用？

控制台应用轻量、可随处运行，让你专注于 PDF 逻辑而不受 UI 干扰。当然，后续也可以将代码迁移到 Web API 或后台服务中——核心逻辑并不依赖于控制台。

## 第二步：加载源 PDF

打开文档非常直接。我们使用 `using` 块，以便文件句柄能够自动释放。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing;   // Required for Color

class Program
{
    static void Main()
    {
        // Adjust these paths to match your environment
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string outputPdfPath = @"C:\Docs\output.pdf";

        // Load the PDF – this is where the “add bates numbering pdf” process begins
        using (var pdfDocument = new Document(sourcePdfPath))
        {
            // Next steps go here...
        }
    }
}
```

**这段代码在做什么？** `Document` 类代表整个 PDF 文件。将其放在 `using` 中，可确保在代码块结束时调用 `Dispose`，将任何未写入的更改刷新到磁盘。

## 第三步：定义 Bates 编号 Artifact（“如何添加 Bates”核心）

Aspose.Pdf 将 Bates 编号视为 *artifact*——一种可以在屏幕上渲染或打印的元数据，除非你对 PDF 进行扁平化，否则它不会成为永久的内容流。下面是我们将附加到每页的对象：

```csharp
var batesArtifact = new BatesNumberArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    Increment = 1,
    X = 36,               // 0.5 inch from the left edge (points)
    Y = 36,               // 0.5 inch from the bottom edge (points)
    FontSize = 9,
    FontColor = Color.Black
};
```

### 为什么使用 artifact？

- **性能**：编号在渲染时实时生成，修改前缀或起始编号时无需重新写入整个 PDF。
- **灵活性**：如需在法律提交时使用“硬编码”印章，可随后对 PDF 进行扁平化。
- **精度**：定位使用点（1/72 英寸），可实现像素级控制。

如果需要不同的前缀或更大的字体，只需调整相应属性。`Increment` 字段决定了页码的递增步幅——正好满足 **添加顺序页码** 的需求。

## 第四步：将 Artifact 附加到每一页

现在遍历 `Pages` 集合并添加 artifact。这才是真正的 “添加 Bates 编号 PDF” 操作。

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

### 边缘情况说明

如果你的 PDF 已经包含 Bates artifact，可能会出现重复。可以加入以下简易检查来防止：

```csharp
foreach (Page page in pdfDocument.Pages)
{
    bool alreadyHasBates = page.Artifacts.Any(a => a is BatesNumberArtifact);
    if (!alreadyHasBates)
        page.Artifacts.Add(batesArtifact);
}
```

这段小检查可以避免在批量处理已预标记文档时出现混乱的双重盖章。

## 第五步：保存更新后的 PDF

最后，将文件写回磁盘。你可以覆盖原文件，也可以生成新文件——这里我们生成一个全新的副本：

```csharp
pdfDocument.Save(outputPdfPath);
Console.WriteLine($"Bates numbers added successfully. Output saved to {outputPdfPath}");
```

在任意阅读器中打开 `output.pdf`，你会看到每页左下角显示 “CASE‑1000”、 “CASE‑1001” 等编号。

### 可选：扁平化 PDF

如果收件方要求不可编辑的 PDF（法院提交中常见），可对页面进行扁平化：

```csharp
pdfDocument.FlattenAllPages();   // Turns artifacts into permanent content
pdfDocument.Save(outputPdfPath);
```

扁平化是一次性操作；完成后，Bates 编号会成为页面内容流的一部分，除非重新处理，否则无法再更改。

## 完整可运行示例

下面是完整的程序代码，可直接复制到 `Program.cs` 中。为方便切换，已将可选的扁平化步骤以注释形式保留。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System;
using System.Drawing;
using System.Linq;

class Program
{
    static void Main()
    {
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string outputPdfPath = @"C:\Docs\output.pdf";

        using (var pdfDocument = new Document(sourcePdfPath))
        {
            var batesArtifact = new BatesNumberArtifact
            {
                Prefix = "CASE-",
                StartNumber = 1000,
                Increment = 1,
                X = 36,
                Y = 36,
                FontSize = 9,
                FontColor = Color.Black
            };

            foreach (Page page in pdfDocument.Pages)
            {
                // Prevent duplicate artifacts if the PDF was processed before
                bool alreadyHasBates = page.Artifacts.Any(a => a is BatesNumberArtifact);
                if (!alreadyHasBates)
                    page.Artifacts.Add(batesArtifact);
            }

            // Uncomment the next line if you need a flattened PDF for legal submission
            // pdfDocument.FlattenAllPages();

            pdfDocument.Save(outputPdfPath);
        }

        Console.WriteLine($"Bates numbers added successfully. Output saved to {outputPdfPath}");
    }
}
```

使用 `dotnet run` 运行它，控制台会确认操作已完成。

## 常见问题与专业技巧

| 问题 | 答案 |
|----------|--------|
| **可以为每页单独设置位置吗？** | 可以。在循环内部创建新的 `batesArtifact`，并根据页面尺寸设置 `X`/`Y`。 |
| **如果 PDF 有密码保护怎么办？** | 使用 `new Document(sourcePdfPath, new LoadOptions { Password = "mySecret" })` 加载。其余流程保持不变。 |
| **处理超大文件会不会性能问题？** | 添加 artifact 的时间复杂度为 O(N)，其中 N 为页数，内存占用保持低，因为 Aspose 会流式处理页面。对于超过 10 000 页的 PDF，建议分批处理以避免长时间的 GC 暂停。 |
| **编号能否在每个章节重置？** | 完全可以。在进入新章节的第一页前设置新的 `StartNumber`，或创建第二个具有不同 `Prefix` 的 `BatesNumberArtifact`。 |
| **这在 .NET Core 上可用吗？** | 可以。Aspose.Pdf 支持 .NET Framework、.NET Core 以及 .NET 5/6+，只需在 csproj 中指定相应的目标运行时。 |

### 专业技巧

在为多卷套件 **添加顺序页码** 时，可将上一次使用的编号保存在一个小型 JSON 文件中。运行前读取，随后递增并写回。这样的小持久层可以防止跨次运行时意外重复编号。

## 验证结果

在 Adobe Reader、Foxit 或 Chrome 中打开 `output.pdf`，应看到类似如下的效果：

```
CASE-1000   (Page 1)
CASE-1001   (Page 2)
…
CASE-1015   (Page 16)
```

如果已经扁平化，编号会成为页面图形的一部分——右键 → “检查” 将显示为普通文本对象。

## 结论

我们已经演示了如何使用 Aspose.Pdf **添加 Bates 编号 PDF**，探讨了 **如何添加 Bates** 的机制，并展示了在整个文档中 **添加顺序页码** 的简洁实现。该代码片段已具备生产级准备度，处理了重复 artifact，并提供了可选的扁平化步骤以满足法律合规需求。

接下来，你可以进一步探索：

- 合并多个 PDF 并保持 Bates 编号连续（使用 `Document.AppendDocument` 并动态调整 `StartNumber`）。
- 在 Bates 编号旁添加二维码，实现自动追踪。
- 将此逻辑集成到 ASP.NET Core API 中，使你的 Web 服务能够按需为 PDF 打标签。

动手试一试，修改前缀、尝试不同字体，让自动化为你的文档审阅流水线减轻繁重工作。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}