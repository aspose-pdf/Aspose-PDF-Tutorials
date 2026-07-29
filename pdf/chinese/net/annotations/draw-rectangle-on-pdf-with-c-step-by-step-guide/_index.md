---
category: general
date: 2026-06-21
description: 使用 C# 在 PDF 上绘制矩形。学习如何加载 PDF 文档、创建黑色矩形批注，并高效保存修改后的 PDF。
draft: false
keywords:
- draw rectangle on pdf
- load pdf document
- add black rectangle
- create black rectangle
- save modified pdf
language: zh
og_description: 在 C# 中通过加载 PDF 文档、创建黑色矩形注释并保存修改后的 PDF 来在 PDF 上绘制矩形。完整代码已包含。
og_title: 使用 C# 在 PDF 上绘制矩形 – 完整编程教程
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
    black rectangle annotation, and save modified PDF efficiently.
  headline: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
  type: TechArticle
- description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
    black rectangle annotation, and save modified PDF efficiently.
  name: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
  steps:
  - name: .NET 6.0 SDK (or any recent .NET version) installed
    text: .NET 6.0 SDK (or any recent .NET version) installed
  - name: 'A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package
      Aspose.PDF`)'
    text: 'A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package
      Aspose.PDF`)'
  - name: An existing PDF file (`input.pdf`) placed in a folder you can read/write
    text: An existing PDF file (`input.pdf`) placed in a folder you can read/write
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
title: 使用 C# 在 PDF 上绘制矩形 – 步骤指南
url: /zh/net/annotations/draw-rectangle-on-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 上绘制矩形（C#） – 完整编程教程

是否曾经需要在 .NET 应用中 **draw rectangle on PDF** 文件，但不确定从何入手？你并非唯一。无论是高亮某个区域、涂抹敏感信息，还是仅仅添加一个视觉提示，学习如何以编程方式 *draw rectangle on PDF* 都能为你节省大量手动编辑的时间。

在本指南中，我们将通过一个实用示例，演示 **loads a PDF document**、**creates a black rectangle**，以及 **saves the modified PDF**。完成后，你将拥有一个可复用的代码片段，能够直接嵌入任何 C# 项目——没有神秘，只是清晰的代码和说明。

## 本教程涵盖内容

- 如何使用 Aspose.PDF for .NET 库 **load pdf document**  
- 定义矩形坐标并确保其位于页面边界内  
- 使用 **add black rectangle** 方法对页面进行注释  
- **Save modified pdf** 到新文件位置  
- 边缘情况处理（多页、超出页面边界的矩形、自定义颜色）  

无需外部工具，也没有模糊的引用——只有完整、可运行的示例，直接 copy‑paste 即可。

---

## 前置条件

在开始之前，请确保你已拥有：

1. .NET 6.0 SDK（或任何近期的 .NET 版本）已安装  
2. 对 **Aspose.PDF for .NET** 的引用（可通过 NuGet 获取：`Install-Package Aspose.PDF`）  
3. 已存在的 PDF 文件（`input.pdf`）放置在可读写的文件夹中  

就这些。如果你对基本的 C# 语法已经熟悉，就可以开始了。

---

## 步骤 1：加载 PDF 文档

我们首先需要进行一次 **load pdf document** 调用。Aspose.PDF 的 `Document` 类接受文件路径并将整个文件读取到内存中。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing;

// Load the source PDF
Document pdfDocument = new Document(@"C:\MyFiles\input.pdf");
```

*为什么这很重要*：加载 PDF 后，你才能访问其页面、元数据以及绘图表面。如果没有这一步，就无法放置任何形状。

---

## 步骤 2：选择目标页面

在 Aspose 中，PDF 页面采用从 1 开始的索引，因此首页的索引为 1。获取你想要注释的页面——通常为了快速演示会选择第一页。

```csharp
// Get the first page (pages are 1‑based)
Page targetPage = pdfDocument.Pages[1];
```

如果需要在其他页面上操作，只需更改索引。记得验证该索引是否存在，以避免 `ArgumentOutOfRangeException`。

---

## 步骤 3：定义矩形几何形状

矩形由左下角 (X,Y) 和右上角 (X,Y) 坐标定义。`Rectangle` 结构体将这些坐标存储为 `LLX`、`LLY`、`URX`、`URY`。

```csharp
// Define the rectangle (lower‑left X,Y and upper‑right X,Y)
Rectangle boundingRect = new Rectangle(100, 100, 300, 300);
```

可以随意调整这些数值——`100,100` 将左下角距离左边和底部各 100 点，而 `300,300` 将右上角距离边缘各 300 点。

---

## 步骤 4：验证矩形是否位于页面内部

尝试在页面边界之外绘制要么会被忽略，要么会抛出异常，这取决于库的版本。快速检查可以让你的代码更健壮。

```csharp
// Ensure the rectangle fits within the page dimensions
if (targetPage.PageInfo.Width >= boundingRect.URX &&
    targetPage.PageInfo.Height >= boundingRect.URY)
{
    // Rectangle is safe to add
}
else
{
    throw new InvalidOperationException("Rectangle exceeds page dimensions.");
}
```

*专业提示*：如果你计划支持不同尺寸的 PDF，建议根据页面宽高的百分比来计算矩形，而不是使用绝对点数。

---

## 步骤 5：添加黑色矩形注释

现在是有趣的部分——向页面 **add black rectangle**。Aspose 提供的 `AddRectangle` 接受几何信息和一个 `Color`。我们将使用 `Color.Black` 来 **create black rectangle**。

```csharp
// Add a black rectangle annotation to the page
targetPage.AddRectangle(boundingRect, Color.Black);
```

这行代码完成了主要工作：它创建一个注释对象，将其边框颜色设为黑色，并将其插入页面的注释集合中。

如果你需要不同的填充或边框样式，可以查看接受 `Annotation` 对象的重载，在其中可以调整线宽、虚线模式，甚至不透明度。

---

## 步骤 6：保存修改后的 PDF

最后，使用 **save modified pdf** 将更改持久化。你可以覆盖原文件或写入新文件——这里我们将创建一个输出文件。

```csharp
// Save the updated PDF to a new location
pdfDocument.Save(@"C:\MyFiles\output.pdf");
```

这就是完整的工作流程。运行程序并打开 `output.pdf`；你应该能看到在你定义的位置出现了一个实心黑色矩形。

---

## 完整可运行示例

下面是一个独立的控制台应用程序，整合了所有步骤。将其复制到新的 `.csproj` 中并点击 **Run**。

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load PDF document
            Document pdfDocument = new Document(@"C:\MyFiles\input.pdf");

            // 2️⃣ Get the first page (pages are 1‑based)
            Page firstPage = pdfDocument.Pages[1];

            // 3️⃣ Define the rectangle geometry
            Rectangle rect = new Rectangle(100, 100, 300, 300);

            // 4️⃣ Verify bounds
            if (firstPage.PageInfo.Width < rect.URX || firstPage.PageInfo.Height < rect.URY)
            {
                Console.WriteLine("Rectangle does not fit on the page.");
                return;
            }

            // 5️⃣ Add a black rectangle annotation
            firstPage.AddRectangle(rect, Color.Black);

            // 6️⃣ Save modified PDF
            pdfDocument.Save(@"C:\MyFiles\output.pdf");

            Console.WriteLine("Successfully drew rectangle on PDF and saved the file.");
        }
    }
}
```

**预期的控制台输出**：

```
Successfully drew rectangle on PDF and saved the file.
```

打开 `output.pdf`，你会看到一个位于指定坐标的黑色矩形。

---

## 处理常见变体

| 场景 | 需要更改的内容 | 原因 |
|-----------|----------------|-----|
| **Multiple pages** | 遍历 `pdfDocument.Pages`，对每个 `Page` 对象应用相同的逻辑。 | 允许对整个文档进行批量注释。 |
| **Different colors** | 将 `Color.Black` 替换为 `Color.Red` 或任意 `System.Drawing.Color`。 | 用于高亮而非涂抹时更有用。 |
| **Transparent fill** | 使用 `new Annotation(rect) { Color = Color.Black, Opacity = 0.5 }`。 | 提供半透明覆盖层，而非实心块。 |
| **Dynamic rectangle size** | 根据 `PageInfo.Width * 0.5` 等计算 `URX` 和 `URY`。 | 使矩形适应不同的页面尺寸。 |
| **Error handling** | 将整个代码块包裹在 `try…catch` 中并记录 `Aspose.Pdf.IOException`。 | 防止在源文件缺失或被锁定时导致崩溃。 |

这些微调展示了如何在多种场景下 **create black rectangle** 注释，而无需重写核心逻辑。

---

## 专业技巧与常见陷阱

- **Dispose the Document**：虽然 Aspose.PDF 实现了 `IDisposable`，但对于短生命周期的控制台应用并非必须使用 `using` 模式。在长期运行的服务中，建议将 `Document` 包裹在 `using` 块中，以及时释放本机资源。  
- **Coordinate System**：PDF 坐标系原点位于左下角。如果你习惯于左上角原点（如 WinForms），需要对 Y 轴进行反转：`pageHeight - y`。  
- **Performance**：向非常大的 PDF 添加注释可能会占用大量内存。考虑分块处理页面或使用 `PdfFileEditor` 进行更轻量的编辑。  
- **Legal**：确保你有权修改源 PDF——某些文档受编辑保护。

---

## 结论

我们刚刚演示了如何使用 C# **draw rectangle on PDF**——从 **load pdf document** 开始，定义几何形状，**add black rectangle**，最后 **save modified pdf**。该示例完整、可运行，并可适配批量处理或自定义样式等实际场景。

接下来，你可以尝试添加其他注释类型（文本、突出显示）或在注释后合并多个 PDF。**load pdf document** 与 **save modified pdf** 步骤保持不变，因而可以自信地扩展此模式。

有自己的实现方式吗？欢迎在评论中分享，祝编码愉快！

## 接下来你应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题。每个资源都提供完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能，并在项目中探索替代实现方案。

- [Create Filled Rectangle Object in PDF using Java](/pdf/english/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)
- [Create Filled Rectangle Object In Pdf Using Java](/pdf/german/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)
- [Create Filled Rectangle Object In Pdf Using Java](/pdf/french/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}