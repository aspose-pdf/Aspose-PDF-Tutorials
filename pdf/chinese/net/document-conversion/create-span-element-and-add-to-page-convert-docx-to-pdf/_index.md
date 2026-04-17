---
category: general
date: 2026-03-27
description: 在 C# 中创建 span 元素，并学习在将 DOCX 转换为 PDF 并保存为 PDF 时如何将 span 添加到页面。面向开发者的分步指南。
draft: false
keywords:
- create span element
- how to add span
- convert docx to pdf
- add element to page
- save as pdf
language: zh
og_description: 在 C# 中创建 span 元素，并学习在将 DOCX 转换为 PDF 时如何将 span 添加到页面，然后保存为 PDF。附带完整代码示例。
og_title: 创建 span 元素并添加到页面 – 将 DOCX 转换为 PDF
tags:
- C#
- DocumentProcessing
- PDFConversion
title: 创建 span 元素并添加到页面 – 将 DOCX 转换为 PDF
url: /zh/net/document-conversion/create-span-element-and-add-to-page-convert-docx-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建 span 元素并添加到页面 – 将 DOCX 转换为 PDF

在 DOCX 文件中创建 **span 元素** 是在需要精确布局控制时的常见任务。在本教程中，我们将展示 **如何向页面添加 span**、**将 DOCX 转换为 PDF**，以及 **保存为 PDF**——全部只需几个简洁的步骤。  

如果你曾经盯着 Word 文档想说：“我真希望能在精确坐标处放一个小文本框”，那么这里正是你想要的。我们将从加载源文件一直走到生成精美的 PDF 输出的完整工作流。

## 你将完成的内容

完成本指南后，你将能够：

* 使用文档库的 `Document` 类加载 `.docx` 文件。  
* 使用 `TaggedContent` API **创建 span 元素**。  
* 将该 span 精确定位在选定页面的 X/Y 坐标上。  
* **可靠地将元素添加到页面**，即使该页面不是第一页。  
* 通过一次 `Save` 调用 **将 DOCX 转换为 PDF** 并 **保存为 PDF**。

无需外部工具，无需神秘设置——只需复制粘贴到项目中的普通 C# 代码。

## 前置条件

* .NET 6+（或任何你的库支持的近期 .NET 运行时）。  
* 提供 `Document`、`TaggedContent`、`Position` 等类的文档处理 SDK。  
* 基本的 C# 语法了解——只要会写 `Console.WriteLine`，就足够了。

> **专业提示：** 保持 SDK 版本为最新；截至 2026 年 3 月的最新发布（v3.2）已包含针对页面级操作的性能优化。

---

![Diagram illustrating how to create span element and place it on a PDF page](https://example.com/images/create-span-element.png "Create span element placement diagram")

## 创建 span 元素 – 定位并添加到页面

下面是完整的可运行代码，涵盖了从加载源 DOCX 到写入最终 PDF 的所有步骤。随意将其放入控制台应用，调整路径后运行即可。

```csharp
using DocumentProcessing;   // Replace with the actual namespace of your SDK
using DocumentProcessing.Models;

class Program
{
    static void Main()
    {
        // Step 1: Load the DOCX you want to modify
        // -------------------------------------------------
        // The constructor takes a file path; make sure the file exists.
        Document doc = new Document(@"C:\Docs\input.docx");

        // Step 2: Create a new span element using the TaggedContent API
        // -------------------------------------------------
        // A span is a lightweight container for inline content.
        var span = doc.TaggedContent.CreateSpanElement();
        // Optional: add some text inside the span
        span.Text = "Hello, world!";

        // Step 3: Position the span at the desired coordinates (X = 50, Y = 750)
        // -------------------------------------------------
        // Position uses points (1/72 inch). Adjust as needed.
        span.Position = new Position(50, 750);

        // Step 4: Add the span to the target page (page index 1 = second page)
        // -------------------------------------------------
        // Pages are zero‑based; index 1 means the second page in the document.
        doc.Pages[1].Add(span);

        // Step 5: Convert the modified DOCX to PDF and save the result
        // -------------------------------------------------
        // The Save method automatically detects the output format from the extension.
        doc.Save(@"C:\Docs\output.pdf");

        // Confirmation output
        Console.WriteLine("Span added, document converted, and PDF saved successfully.");
    }
}
```

### 步骤说明

#### 步骤 1 – 加载 DOCX 文档  
我们实例化一个指向 `input.docx` 的 `Document` 对象。该对象在内存中表示整个 Word 文件，提供对页面、内容和元数据的访问。

#### 步骤 2 – 创建 span 元素  
`TaggedContent.CreateSpanElement()` 调用返回一个轻量级的内联容器。可以把它想象成一个微小的、不可见的盒子，能够容纳文本、图像或其他内联元素。为 `span.Text` 赋值是可选的，但对调试很有帮助。

#### 步骤 3 – 定位 span  
`new Position(50, 750)` 将 span 的左上角设置在距左边距 50 pts、距页面顶部 750 pts 的位置。这些值是绝对坐标，因而可以将 span 放置在任意位置——非常适合精确布局。

#### 步骤 4 – 将 span 添加到目标页面  
`doc.Pages[1].Add(span)` 将 span 注入第二页。API 使用零基索引，因此第 0 页是第一页。如果需要添加到第一页，只需使用 `doc.Pages[0]`。

#### 步骤 5 – 将 DOCX 转换为 PDF 并保存为 PDF  
调用 `doc.Save("output.pdf")` 会执行两件事：将修改后的文档写入磁盘 **并** 因为扩展名为 `.pdf` 而自动转换为 PDF。无需额外的转换步骤——这是 **保存为 PDF** 的最简方式。

---

## 如何在不同页面添加 span（高级）

有时你事先并不知道页面索引。可以通过页面编号（对人友好）或搜索特定关键字来定位页面。

```csharp
// Find the page that contains the word "Summary"
int targetIndex = doc.Pages
    .Select((p, i) => new { Page = p, Index = i })
    .FirstOrDefault(x => x.Page.Text.Contains("Summary"))?.Index ?? 0;

// Fallback to first page if not found
targetIndex = Math.Max(targetIndex, 0);

// Add the span to the discovered page
doc.Pages[targetIndex].Add(span);
```

**为何重要：** 在页数会变化的报告中，硬编码 `Pages[1]` 可能导致布局失效。此代码片段展示了一个用于 **动态添加 span** 的稳健模式。

---

## 常见陷阱及规避方法

| 问题 | 会发生什么 | 解决方案 |
|------|------------|----------|
| **Span 不可见** | 坐标超出页面或 span 的宽高为零。 | 仔细检查 `Position` 值；在 PDF 查看器中使用标尺。 |
| **页面索引错误** | 你在第 0 页添加，却期望它出现在第 2 页。 | 记住 API 使用零基索引；将人类页面号减 1。 |
| **保存时覆盖源文件** | `doc.Save("input.docx")` 会替换原始文件。 | 转换时始终保存到新路径（如 `output.pdf`）。 |
| **缺少 SDK 引用** | 编译时找不到 `Document` 类。 | 安装 NuGet 包：`dotnet add package DocumentProcessing.SDK`。 |

---

## 验证结果

运行程序后，用任意 PDF 查看器打开 `output.pdf`。你应该在第二页的坐标 (50, 750) 处看到文本 “Hello, world!”。如果文本出现在其他位置，请调整 `Position` 值并重新运行。  

对于自动化测试，你可以使用 PDF 解析器（例如 iTextSharp）来以编程方式断言文本坐标。

```csharp
// Example using iTextSharp to verify position (pseudo‑code)
var pdfReader = new PdfReader(@"C:\Docs\output.pdf");
var page = pdfReader.GetPageContent(2);
Debug.Assert(page.Contains("Hello, world!"));
```

---

## 后续步骤

* **为 span 设置样式** – 探索 `span.Font`、`span.Color` 等样式属性。  
* **添加图像** – 使用 `CreateImageElement()` 替代 span 来插入图形。  
* **批量处理** – 对文件夹中的多个 DOCX 文件进行循环处理

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}