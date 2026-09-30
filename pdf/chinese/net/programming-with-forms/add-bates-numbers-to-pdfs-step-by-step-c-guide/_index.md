---
category: general
date: 2026-02-12
description: 快速为 PDF 文件添加贝茨编号。了解如何使用 Aspose.PDF 添加文本字段 PDF、表单字段 PDF 和页码 PDF。
draft: false
keywords:
- add bates numbers
- add text field pdf
- add form field pdf
- add page numbers pdf
- how to add bates
language: zh
og_description: 在 C# 中为 PDF 文档添加 Bates 编号。本指南展示了如何使用 Aspose.PDF 添加文本字段 PDF、表单字段 PDF
  和页码 PDF。
og_title: 为 PDF 添加贝茨编号 – 完整 C# 教程
tags:
- PDF
- C#
- Aspose.PDF
title: 为PDF添加贝茨编号 – 步骤详解 C# 指南
url: /zh/net/programming-with-forms/add-bates-numbers-to-pdfs-step-by-step-c-guide/
---











{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 为 PDF 添加 Bates 编号 – 完整 C# 指南

是否曾需要 **为一堆法律 PDF 添加 Bates 编号**，却不知道从何入手？你并不孤单。在许多律所和电子取证项目中，为每页打上唯一标识是日常工作，而手动操作简直是噩梦。  

好消息是？只需几行 C# 代码和 Aspose.PDF，即可实现全自动化。在本教程中，我们将逐步演示 **如何添加 Bates** 编号、在每页上放置文本字段，并保存为干净、可搜索的 PDF——整个过程轻松无压力。

> **你将获得：** 完整可运行的代码示例、每行代码意义的解释、边缘情况的技巧，以及快速检查输出的清单。  

我们还会涉及相关任务，如 **add text field pdf**、**add form field pdf**、**add page numbers pdf**，让你拥有一整套文档自动化工具箱。

---

## 前置条件

- .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.6+）  
- Visual Studio 2022（或任意你喜欢的 IDE）  
- 有效的 Aspose.PDF for .NET 许可证（免费试用版可用于测试）  
- 一个名为 `source.pdf` 的源 PDF，放置在可引用的文件夹中  

如果上述任意项你不熟悉，请先暂停并安装缺失的部分再继续。下面的步骤假设你已经添加了 Aspose.PDF NuGet 包：

```bash
dotnet add package Aspose.Pdf
```

---

## 使用 Aspose.PDF 为 PDF 添加 Bates 编号的步骤

下面是完整的、可直接复制运行的程序。它加载 PDF，在每页创建一个 **文本框字段**，写入格式化的 Bates 编号，最后将修改后的文件保存。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 👉 Step 1: Load the source PDF document
        using (var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf"))
        {
            // 👉 Step 2: Add a Bates number text field to each page
            for (int pageNumber = 1; pageNumber <= pdfDocument.Pages.Count; pageNumber++)
            {
                // Define the rectangle where the field will appear (10,10) = lower‑left corner
                var fieldRect = new Rectangle(10, 10, 150, 30);

                // Create the TextBoxField – this is the “add text field pdf” part
                var batesField = new TextBoxField(pdfDocument.Pages[pageNumber], fieldRect)
                {
                    // Format the number: BATES-00001, BATES-00002, …
                    Value = $"BATES-{pageNumber:D5}"
                };

                // Register the field with the form collection – “add form field pdf”
                pdfDocument.Form.Add(batesField, $"Bates_{pageNumber}", pageNumber);
            }

            // 👉 Step 3: Save the modified PDF with Bates numbers
            pdfDocument.Save(@"YOUR_DIRECTORY\bates.pdf");
        }

        Console.WriteLine("✅ Bates numbers added successfully!");
    }
}
```

### 为什么这样可行

- **`Document`** 是入口点，代表整个 PDF 文件。  
- **`Rectangle`** 定义字段在页面上的位置。数字使用点（1 pt ≈ 1/72 in）。如果需要将编号放在其他角落，请调整坐标。  
- **`TextBoxField`** 是一种 *表单字段*，可以容纳任意字符串。通过赋值 `Value`，我们实际上 **add page numbers pdf** 并使用自定义前缀。  
- **`pdfDocument.Form.Add`** 将字段注册到 PDF 的 AcroForm 中，使其在 Adobe Acrobat 等阅读器中可见。  

如果你想更改外观（字体、颜色、大小），可以调整 `TextBoxField` 的属性——请参考 Aspose 文档中的 `DefaultAppearance` 与 `Border`。

---

## 为每页 PDF 添加文本字段（“add text field pdf” 步骤）

有时你只想要一个可见标签，而不是交互式表单字段。这种情况下可以用 `TextFragment` 替代 `TextBoxField`，直接添加到页面的 `Paragraphs` 集合中。下面是一个快速替代方案：

```csharp
var fragment = new TextFragment($"BATES-{pageNumber:D5}")
{
    // Position the text using a TextState (font, size, color)
    TextState = new TextState
    {
        Font = FontRepository.FindFont("Arial"),
        FontSize = 12,
        ForegroundColor = Color.Black
    }
};

// Set the fragment’s rectangle (same coordinates as before)
fragment.Position = new Position(10, 10);
pdfDocument.Pages[pageNumber].Paragraphs.Add(fragment);
```

**add text field pdf** 方法适用于最终文档只读的场景，而 **add form field pdf** 方法则在后期仍可编辑编号。

---

## 保存带有 Bates 编号的 PDF（“add page numbers pdf” 时刻）

循环结束后，调用 `pdfDocument.Save` 即可将所有内容写入磁盘。如果需要保留原始文件，只需更改输出路径，或使用 `pdfDocument.Save` 的重载将结果直接流式输出到 Web API 的响应中。

```csharp
// Example: stream to HTTP response (ASP.NET Core)
Response.ContentType = "application/pdf";
pdfDocument.Save(Response.Body);
```

这就是简洁之处——无需临时文件、无需额外库，全部交给 Aspose 处理。

---

## 预期结果与快速验证

在任意 PDF 阅读器中打开 `bates.pdf`。你应该能在每页左下角看到一个小框，内容类似：

```
BATES-00001
BATES-00002
…
```

如果检查文档属性，会发现 AcroForm 中包含名为 `Bates_1`、`Bates_2` 等字段。这表明 **add form field pdf** 步骤已成功。

---

## 常见陷阱与专业技巧

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| 编号位置偏离中心 | `Rectangle` 坐标相对于页面左下角。 | 将 Y 值取反（`pageHeight - marginTop`）或使用 `page.PageInfo.Height` 计算顶部边距。 |
| 在 Adobe Reader 中字段不可见 | 默认边框设置为 “无”。 | 设置 `batesField.Border = new Border { Width = 0.5f, Color = Color.Black };` |
| 大型 PDF 导致内存压力 | `using` 仅在循环结束后才释放文档。 | 将页面分块处理，或使用带有流式选项的 `pdfDocument.Save`。 |
| 许可证未生效 | Aspose 在首页打印水印。 | 早期注册许可证：`License lic = new License(); lic.SetLicense("Aspose.Pdf.lic");` |

---

## 扩展方案

- **自定义前缀：** 将 `"BATES-"` 替换为任意字符串（如 `"DOC-"`、`"CASE-"` …）。  
- **零填充长度：** 将 `{pageNumber:D5}` 改为 `{pageNumber:D3}` 以显示三位数。  
- **动态定位：** 使用 `pdfDocument.Pages[pageNumber].PageInfo.Width` 将字段放置在右侧。  
- **条件编号：** 通过检查 `pdfDocument.Pages[pageNumber].IsBlank` 跳过空白页。

所有这些变体都保持 **add bates numbers**、**add text field pdf**、**add form field pdf** 的核心模式不变。

---

## 完整可运行示例（All‑in‑One）

下面是最终的、可直接运行的程序，已整合上述技巧。复制到新的控制台应用并按 F5 运行。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;

class AddBatesNumbers
{
    static void Main()
    {
        // Register your license here (optional for trial)
        // var license = new License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        using (var pdfDocument = new Document(inputPath))
        {
            int totalPages = pdfDocument.Pages.Count;

            for (int i = 1; i <= totalPages; i++)
            {
                // Position the field 10 pts from left and 10 pts from bottom
                var rect = new Rectangle(10, 10, 150, 30);

                var batesField = new TextBoxField(pdfDocument.Pages[i], rect)
                {
                    Value = $"BATES-{i:D5}"
                };

                // Optional: make the field look nicer
                batesField.Border = new Border
                {
                    Width = 0.5f,
                    Color = Color.Gray
                };
                batesField.DefaultAppearance = new DefaultAppearance
                {
                    Font = FontRepository.FindFont("Arial"),
                    FontSize = 10,
                    ForegroundColor = Color.DarkBlue
                };

                pdfDocument.Form.Add(batesField, $"Bates_{i}", i);
            }

            pdfDocument.Save(outputPath);
        }

        Console.WriteLine($"✅ Finished! Bates numbers saved to: {outputPath}");
    }
}
```

运行后打开生成的文件，你会看到每页都有专业的标识——正是诉讼支持专员所期待的效果。

---

## 结论

我们已经演示了 **如何使用 C# 和 Aspose.PDF 为任意 PDF 添加 Bates 编号**。通过在每页创建 **文本框字段**，我们一次性实现了 **add text field pdf**、**add form field pdf** 与 **add page numbers pdf**。该方法快速、可扩展，且易于为自定义前缀、不同布局或条件逻辑进行调整。

准备好迎接下一个挑战了吗？尝试嵌入指向原始案件文件的二维码，或生成单独的索引页列出所有 Bates 编号及对应的页标题。同一套 API 还能合并 PDF、提取页面，甚至马赛克敏感信息——无限可能等你探索。

如果遇到问题，请在下方留言或查阅 Aspose 官方文档获取更深入的内容。祝编码愉快，愿你的 PDF 永远编号精准！

---  

![add bates numbers screenshot](https://example.com/images/add-bates-numbers.png "add bates numbers example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}