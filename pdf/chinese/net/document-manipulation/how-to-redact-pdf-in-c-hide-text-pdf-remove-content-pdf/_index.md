---
category: general
date: 2026-03-01
description: 如何使用 Aspose.Pdf 在 C# 中快速编辑 PDF。学习隐藏 PDF 文本、删除 PDF 内容以及在 PDF 中进行区域编辑，提供完整可运行的示例。
draft: false
keywords:
- how to redact pdf
- hide text pdf
- remove content pdf
- create pdf document c#
- redact area in pdf
language: zh
og_description: 如何使用 Aspose.Pdf 在 C# 中对 PDF 进行编辑。 本指南向您展示如何隐藏 PDF 文本、删除 PDF 内容以及在
  PDF 中编辑区域，并提供完整的源代码。
og_title: 如何在 C# 中编辑 PDF – 隐藏文本 PDF 与 删除内容 PDF
tags:
- Aspose.Pdf
- C#
- PDF Redaction
title: 如何在 C# 中对 PDF 进行编辑 – 隐藏文本并删除内容
url: /zh/net/document-manipulation/how-to-redact-pdf-in-c-hide-text-pdf-remove-content-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中编辑 PDF – 隐藏文本 PDF 与 删除内容 PDF

是否曾经想过 **how to redact pdf** 而不需要花费数小时去摆弄第三方工具？你并不孤单。在许多合规性要求严格的项目中，你需要 hide text pdf，剥离机密数据，同时保持文档其余部分完整。  

好消息是？使用 Aspose.Pdf for .NET，你可以用几行代码完成所有操作。在本教程中，我们将演示如何在 C# 中创建 PDF 文档、定义编辑区域，最后保存干净的副本。完成后，你将准确了解如何 remove content pdf、hide text pdf，以及 redact area in pdf——全部通过可以直接放入任何 .NET 项目的代码实现。

## 前置条件与你将构建的内容

- **.NET 6+**（或 .NET Framework 4.6+ —— API 相同）
- **Aspose.Pdf for .NET** NuGet 包（`Aspose.Pdf`）
- 对 C# 语法的基本了解（不需要高级技巧）

我们将生成一个名为 `redacted.pdf` 的文件，其中包含一个覆盖坐标 (100, 100)‑(300, 200) 的红色矩形。矩形下方的所有内容将被永久删除，这正是当你被要求为 GDPR 或法律原因 **hide text pdf** 时所需要的。

> **专业提示：** 如果需要编辑多个不相连的区域，只需向同一页添加更多 `RedactionAnnotation` 对象——库会一次性处理所有区域。

---

## 如何编辑 PDF – 步骤详解

在每个步骤下，你会看到简洁的代码片段、该行代码重要性的说明 *why*，以及避免常见陷阱的快速提示。

### 1. 设置项目并添加 Aspose.Pdf

首先，创建一个新的控制台应用程序（或集成到现有服务中），并安装 NuGet 包：

```bash
dotnet new console -n PdfRedactionDemo
cd PdfRedactionDemo
dotnet add package Aspose.Pdf
```

> **为什么？** 安装该包会引入 `Aspose.Pdf` 程序集，其中包含 `Document`、`RedactionAnnotation` 以及所有你需要的低层 PDF 对象。没有它，你就无法以编程方式 **remove content pdf**。

### 2. 在内存中创建 PDF 文档

我们从一个空白 PDF 开始——把它想象成一张可以书写的全新纸张。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Redactions;

class Program
{
    static void Main()
    {
        // Step 2: Create a new PDF document in memory
        using var pdfDocument = new Document();

        // (Optional) Add a page with some sample text so you can see the redaction effect
        var page = pdfDocument.Pages.Add();
        page.Paragraphs.Add(new TextFragment("Sensitive data: 123‑45‑6789"));
```

**为什么这很重要：**  
- `using var` 确保文档正确释放，释放本机资源。  
- 添加带有可见文本的页面可以让你验证编辑确实 *删除* 内容，而不是仅仅覆盖它。

### 3. 定义 Redaction Annotation（即 “hide text pdf” 区域）

在这里我们指定将从页面中剔除的矩形区域。

```csharp
        // Step 3: Define a redaction annotation covering the desired area
        var redactionRect = new Rectangle(100, 100, 300, 200);
        var redactionAnnotation = new RedactionAnnotation(redactionRect)
        {
            // Optional: set the fill color to a solid black for visual feedback
            FillColor = Color.Black,
            // Optional: set overlay text that will appear after redaction
            OverlayText = "REDACTED"
        };

        // Attach the annotation to the first page (index 1)
        pdfDocument.Pages[1].Annotations.Add(redactionAnnotation);
```

**为什么？** `RedactionAnnotation` 告诉 Aspose *在何处* 擦除数据。矩形使用 PDF 坐标系（原点在左下角）。如果你习惯于 Windows GDI 坐标系，请记住 Y 轴是翻转的。

> **常见错误：** 忘记将注释添加到 `Pages[1].Annotations`。注释虽然存在，但不会进行任何编辑。

### 4. 准备资源（例如 XObjects） – 高级用法

如果你计划在编辑区域嵌入图像或自定义图形，可以预先将它们加载到注释的 resources 字典中。

```csharp
        // Step 4: Access the annotation's resources dictionary (optional)
        var resources = redactionAnnotation.Resources;
        // Example: add an XObject later – omitted here for brevity
```

**为什么要包含此步骤？** 即使你只需要一个简单的黑框，公开 resources 字典也向引擎表明你 *可能* 在以后添加额外内容。这是一个无害的调用，使代码在未来的扩展中保持灵活。

### 5. 应用编辑并保存 PDF

调用 `Redact()` 实际上会擦除内容。随后我们持久化文件。

```csharp
        // Step 5: Apply the redaction and save the PDF
        pdfDocument.Redact();   // This processes all redaction annotations
        pdfDocument.Save("redacted.pdf");

        Console.WriteLine("Redacted PDF saved as redacted.pdf");
    }
}
```

**为什么要调用 `Redact()`？** 仅仅添加注释并不会修改底层流。`Redact()` 会遍历每个注释，删除被覆盖的对象，并可选地添加覆盖文本。跳过此步骤会使原始数据保持不变——这违背了 **how to redact pdf** 的目的。

---

## 完整工作示例

将整个代码粘贴到 `Program.cs` 并运行 `dotnet run`。你会看到项目文件夹中出现 `redacted.pdf`，其中敏感字符串被标记为 “REDACTED” 的黑框取代。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Redactions;
using Aspose.Pdf.Text;   // For TextFragment
using Aspose.Pdf.Drawing; // For Color

class Program
{
    static void Main()
    {
        // Create a new PDF document in memory
        using var pdfDocument = new Document();

        // Add a page with sample text (so we can see the effect)
        var page = pdfDocument.Pages.Add();
        page.Paragraphs.Add(new TextFragment("Sensitive data: 123‑45‑6789"));

        // Define a redaction annotation covering the desired area
        var redactionRect = new Rectangle(100, 100, 300, 200);
        var redactionAnnotation = new RedactionAnnotation(redactionRect)
        {
            FillColor = Color.Black,
            OverlayText = "REDACTED"
        };
        pdfDocument.Pages[1].Annotations.Add(redactionAnnotation);

        // (Optional) Access resources dictionary – useful for XObjects
        var resources = redactionAnnotation.Resources;

        // Apply redaction and save the PDF
        pdfDocument.Redact();
        pdfDocument.Save("redacted.pdf");

        Console.WriteLine("Redacted PDF saved as redacted.pdf");
    }
}
```

**预期结果：** 打开 `redacted.pdf`，会看到单页上文本 “Sensitive data: 123‑45‑6789” 完全消失，取而代之的是一个实心黑色矩形，内部居中显示 “REDACTED”。没有隐藏的流，满足合规审计要求。

---

## 常见问题与边缘情况

| Question | Answer |
|----------|--------|
| **我可以一次编辑多个页面吗？** | 可以——只需遍历 `pdfDocument.Pages`，并向每页的 `Annotations` 集合添加 `RedactionAnnotation`。 |
| **如果编辑区域与已有图像重叠怎么办？** | 编辑引擎会删除与矩形相交的 *所有* 对象，包括图像、矢量和文本。 |
| **我需要在每个新注释后都调用 `Redact()` 吗？** | 不需要。在添加完所有想要应用的 *注释* 后一次性调用即可。 |
| **如何保持原始 PDF 不变？** | 将源文件加载到 `Document`，克隆它 (`var clone = (Document)source.Clone();`)，在克隆上应用编辑，然后保存克隆。 |
| **编辑是可逆的吗？** | 不可以。`Redact()` 执行后，原始内容会从 PDF 流中被剥除。如果以后可能需要未编辑的版本，请保留备份。 |

---

## 相关主题，你可能想进一步探索

- **Hide text pdf** 使用 PDF 图层（`OptionalContentGroup`）实现可逆的遮罩。  
- **Remove content pdf** 通过低层 PDF 对象模型删除页面或特定对象。  
- **Create PDF document C#** 使用表格、图像和数字签名。  
- **Redact area in PDF** 使用自定义覆盖图形（例如公司徽标）。  

---

## 结论

现在，你已经拥有一个稳健、可用于生产环境的 **how to redact pdf** 在 C# 中的解决方案。通过创建 `Document`、添加 `RedactionAnnotation`、调用 `Redact()` 并保存文件，你可以可靠地 **hide text pdf**、**remove content pdf** 和 **redact area in pdf**，无需第三方编辑器。

在自己的文件上试一试，尝试多个矩形，甚至可以将此过程自动化用于批量编辑流水线。如果遇到任何问题，欢迎在下方留言——祝编码愉快！

![如何编辑 PDF 示例](redaction-example.png){: .align-center alt="如何编辑 PDF 示例"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}