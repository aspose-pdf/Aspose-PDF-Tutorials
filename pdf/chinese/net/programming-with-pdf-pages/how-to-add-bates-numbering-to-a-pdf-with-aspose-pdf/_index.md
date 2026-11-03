---
category: general
date: 2026-10-07
description: 学习如何使用 C# 为 PDF 添加贝茨编号。本分步指南还涵盖 PDF 页码编号及其他编号技巧。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- pdf page numbering
- number pdf pages
- how to add bates
- bates numbering pdf
language: zh
lastmod: 2026-10-07
og_description: 快速为 PDF 添加贝茨编号。按照本教程掌握 PDF 页码编号、为 PDF 页面编号，并实现文档追踪自动化。
og_image_alt: Screenshot of a PDF with Bates numbers added using Aspose.Pdf
og_title: 在 C# 中为 PDF 添加 Bates 编号 – 完整的 Aspose 指南
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  headline: How to add bates numbering to a PDF with Aspose.Pdf
  type: TechArticle
- description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  name: How to add bates numbering to a PDF with Aspose.Pdf
  steps:
  - name: 1. Can I change the location of the numbers?
    text: Yes. Set `batesOptions.Position = new Position(10, 10, 10, 10);` where the
      four values represent margins from the top, bottom, left, and right edges. Aspose
      also provides predefined enums such as `BatesNumberingPosition.BottomCenter`.
  - name: 2. What if my PDF already contains page numbers?
    text: Adding Bates numbers will **stack** on top of existing numbers. To avoid
      visual clutter, either hide the original numbers (if they are part of a text
      layer) or adjust the `batesOptions` font size and position.
  - name: 3. Does this work with encrypted PDFs?
    text: 'Aspose can open password‑protected PDFs if you supply the password:'
  - name: 4. How do I **number pdf pages** with a simple sequential counter (no prefix/suffix)?
    text: 'Just set `Prefix = string.Empty` and `Suffix = string.Empty`:'
  - name: 5. Can I use this approach in ASP.NET Core to serve PDFs on‑the‑fly?
    text: 'Absolutely. Load the document, apply the numbering, then write the stream
      to the HTTP response:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: 如何使用 Aspose.Pdf 为 PDF 添加 Bates 编号
url: /zh/net/programming-with-pdf-pages/how-to-add-bates-numbering-to-a-pdf-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.Pdf 为 PDF 添加 Bates 编号

如果您需要 **add bates numbering** 到 PDF，本指南将向您展示如何在 C# 中实现。无论您是准备法律文书、管理案件文件，还是仅仅想要可靠的 **pdf page numbering**，以下步骤都提供了完整、可运行的解决方案。

在本教程中，您将学习：

* 加载现有的 PDF 文件。
* 配置 Bates 编号选项，如前缀、起始号码、数字填充、分隔符和后缀。
* 将编号应用到每一页。
* 保存更新后的文档。

无需任何外部工具，只需使用 Aspose.Pdf for .NET 库，代码可在 .NET 6+ 以及 .NET Framework 4.7.2+ 上运行。  

---

## 前提条件

在开始之前，请确保您具备以下条件：

| 要求 | 为什么重要 |
|------|-----------|
| **Aspose.Pdf for .NET** (NuGet 包 `Aspose.Pdf`) | 提供代码中使用的 `Document` 和 `BatesNumberingOptions` 类。 |
| **.NET SDK** (推荐 6.0 或更高) | 使您能够编译并运行 C# 控制台应用程序。 |
| **A source PDF** 您想要编号的源 PDF | 本教程使用 `source.pdf` 作为示例；请将路径替换为您自己的文件。 |
| **Write permission** 对输出文件夹的写入权限 | `Save` 调用需要写入新文件。 |

您可以使用以下 CLI 命令安装库：

```bash
dotnet add package Aspose.Pdf
```

---

## 第 1 步：创建新的控制台项目

打开终端并运行：

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
```

这将创建一个最小的 C# 项目，我们将在其中填入实现 **add bates numbering** 所需的代码。

---

## 第 2 步：添加所需的 `using` 指令

打开 `Program.cs`，在文件顶部添加以下命名空间：

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

* `Aspose.Pdf` 为您提供加载和保存 PDF 所需的 `Document` 类。  
* `Aspose.Pdf.Text` 包含 `BatesNumberingOptions`，用于定义编号的显示方式。

---

## 第 3 步：加载源 PDF

第一行可执行代码加载您要编号的 PDF。将 `"YOUR_DIRECTORY/source.pdf"` 替换为实际文件路径。

```csharp
// Load the source PDF
Document pdf = new Document("YOUR_DIRECTORY/source.pdf");
```

如果找不到文件，Aspose 会抛出 `FileNotFoundException`。为避免此情况，您可以事先验证路径：

```csharp
if (!System.IO.File.Exists("YOUR_DIRECTORY/source.pdf"))
{
    Console.WriteLine("Source PDF not found.");
    return;
}
```

---

## 第 4 步：定义 Bates 编号选项

`BatesNumberingOptions` 让您可以控制编号的每个视觉元素。下面的示例展示了针对法律案件文件的典型配置：

```csharp
// Define Bates numbering options
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",          // Text before the numeric part
    StartNumber = 1000,       // First number to use
    Digits = 6,               // Pad with leading zeros (e.g., 001000)
    Separator = "-",          // Character between prefix, number, and suffix
    Suffix = "-2025"          // Text after the numeric part
};
```

**Why each property matters**

| Property | Purpose |
|----------|---------|
| `Prefix` | 帮助您按项目、客户或案件对文档进行分组。 |
| `StartNumber` | 设置初始计数器；在已有编号文件时非常有用。 |
| `Digits` | 保证统一宽度，便于排序。 |
| `Separator` | 提高可读性，尤其是在前缀和后缀组合时。 |
| `Suffix` | 允许您添加年份、版本或任何后缀标识。 |

您还可以通过访问 `batesOptions.Position` 和 `batesOptions.Font` 来控制位置（上、下、左、右）和字体样式。对大多数场景而言，默认设置（右下角，12 pt Times New Roman）已足够。

---

## 第 5 步：将编号应用到每一页

调用 `pdf.BatesNumbering.Add` 会按照页面顺序在每页插入编号。

```csharp
// Apply Bates numbering to every page
pdf.BatesNumbering.Add(batesOptions);
```

如果只想在部分页面（例如跳过封面页）**number pdf pages**，可以传入 `PageCollection`：

```csharp
// Example: skip the first page
pdf.BatesNumbering.Add(batesOptions, pdf.Pages.Skip(1));
```

---

## 第 6 步：保存更新后的 PDF

最后，将修改后的文档写入磁盘。文件名通常会反映 PDF 已包含 Bates 编号。

```csharp
// Save the PDF with Bates numbers applied
pdf.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering added successfully.");
```

如果输出文件夹不存在，Aspose 会自动创建。但请确保您拥有写入权限，以免出现 `UnauthorizedAccessException`。

---

## 完整、可运行的示例

将所有代码片段组合在一起，下面是一个完整的程序，您可以复制、粘贴并运行：

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source PDF
        // -------------------------------------------------
        const string inputPath = "YOUR_DIRECTORY/source.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        Document pdf = new Document(inputPath);

        // -------------------------------------------------
        // 2️⃣ Configure Bates numbering
        // -------------------------------------------------
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            Digits = 6,
            Separator = "-",
            Suffix = "-2025"
        };

        // -------------------------------------------------
        // 3️⃣ Apply the numbering to every page
        // -------------------------------------------------
        pdf.BatesNumbering.Add(batesOptions);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";
        pdf.Save(outputPath);
        Console.WriteLine($"Bates numbering added. Saved to {outputPath}");
    }
}
```

**Expected output** (console):

```
Bates numbering added. Saved to YOUR_DIRECTORY/bates_numbered.pdf
```

打开 `bates_numbered.pdf`，您会看到每页都标记了类似 `CASE-001000-2025`、`CASE-001001-2025` 等编号，默认位于右下角。

---

## 常见问题 (FAQ)

### 1. 我可以更改编号的位置吗？
可以。设置 `batesOptions.Position = new Position(10, 10, 10, 10);`，四个数值分别代表距顶部、底部、左侧和右侧的边距。Aspose 还提供预定义枚举，如 `BatesNumberingPosition.BottomCenter`。

### 2. 如果我的 PDF 已经包含页码怎么办？
添加 Bates 编号会 **stack** 在已有页码之上。为避免视觉混乱，您可以隐藏原始页码（如果它们位于文本层），或调整 `batesOptions` 的字体大小和位置。

### 3. 这在加密的 PDF 上有效吗？
如果提供密码，Aspose 能打开受密码保护的 PDF：

```csharp
Document pdf = new Document("source.pdf", new LoadOptions { Password = "mySecret" });
```

随后按相同方式应用 Bates 编号。

### 4. 如何使用 **number pdf pages** 的简单顺序计数器（无前缀/后缀）？
只需将 `Prefix = string.Empty` 和 `Suffix = string.Empty`：

```csharp
BatesNumberingOptions simple = new BatesNumberingOptions
{
    StartNumber = 1,
    Digits = 4   // 0001, 0002, …
};
pdf.BatesNumbering.Add(simple);
```

### 5. 我能在 ASP.NET Core 中实时提供带编号的 PDF 吗？
完全可以。加载文档、应用编号后，将流写入 HTTP 响应：

```csharp
using (var ms = new MemoryStream())
{
    pdf.Save(ms);
    ms.Position = 0;
    return File(ms, "application/pdf", "bates_numbered.pdf");
}
```

---

## 边缘情况与最佳实践提示

| 情况 | 推荐做法 |
|-----------|----------------------|
| **Large PDFs (hundreds of pages)** | 在完成任何页面级别的转换后再调用 `pdf.BatesNumbering.Add`，以避免多次处理同一页面。 |
| **Custom fonts** | 设置 `batesOptions.Font = FontRepository.FindFont("Arial")` 并调整 `batesOptions.FontSize`，以提升扫描文档的可读性。 |
| **Performance‑critical batch jobs** | 在循环处理中复用单个 `Document` 实例；每次迭代后释放以节省内存。 |
| **International characters** | 使用 Unicode 兼容字体（如 `Times New Roman Unicode`），确保前缀或后缀能够正确显示。 |
| **Version compatibility** | 代码适用于 Aspose.Pdf 23.10 及以上版本。若使用旧版，请检查 API 文档中是否有属性名称变更。 |

---

## 结论

您现在已经掌握了使用 Aspose.Pdf for .NET **add bates numbering** 到 PDF 的方法。教程涵盖了加载 PDF、配置 `BatesNumberingOptions`、对每页应用编号以及保存结果。借助这些构建块，您还可以实现通用的 **pdf page numbering**、**number pdf pages** 自定义格式，并将该过程集成到更大的自动化流水线中。

**后续步骤**

* 深入探索 **bates numbering pdf** API，以自定义字体、颜色和位置。  
* 将此技术与 **digital signatures** 结合，创建防篡改的法律文书。  
* 了解 Aspose 的 **PDF merging** 功能，以在编号前合并多个案件文件。

欢迎尝试不同的前缀、后缀和数字长度，以符合您组织的归档标准。祝编码愉快！

## 接下来该学习什么？

以下教程与本指南紧密相关，帮助您进一步掌握 API 功能并探索替代实现方式：

- [创建 PDF 文档 C# – 添加 Bates 编号指南](/pdf/english/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/)
- [如何在 PDF 中使用 C# 添加 Bates 编号 – 完整指南](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-c-complete-guide/)
- [Aspose PDF 教程 – 插入空白页并更新 Bates 编号](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}