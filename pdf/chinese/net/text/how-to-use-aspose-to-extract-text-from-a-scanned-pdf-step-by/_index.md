---
category: general
date: 2026-08-04
description: 如何使用 Aspose 提取扫描的 PDF 文本并使用 C# 将 PDF 转换为文本。学习读取扫描的 PDF 文件并获得可靠的 OCR 结果。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use aspose
- extract scanned pdf text
- convert pdf to text
- read scanned pdf
- how to extract text
language: zh
lastmod: 2026-08-04
og_description: 如何使用 Aspose 读取扫描的 PDF 文件，提取扫描 PDF 文本，并通过完整可运行的示例将 PDF 转换为文本。
og_image_alt: Screenshot showing how to use Aspose OCR copilot to extract text from
  a scanned PDF
og_title: 如何使用 Aspose – 在 C# 中从扫描的 PDF 中提取文本
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: How to use Aspose to extract scanned PDF text and convert PDF to text
    with C#. Learn to read scanned PDF files and get reliable OCR results.
  headline: How to use Aspose to extract text from a scanned PDF – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: Yes. Add `.WithPassword("yourPassword")` to the options builder before
      creating the copilot.
    question: Does this work with password‑protected PDFs?
  - answer: Use `GetTextStructureAsync()` instead of `GetTextAsync()`. The method
      returns a JSON payload that includes page indices, bounding boxes, and confidence
      scores.
    question: Can I extract text in a structured format (e.g., JSON with page numbers)?
  - answer: 'The plain‑text extraction flattens tables into line‑break‑separated rows.
      For richer data, request the PDF‑to‑HTML conversion (`GetHtmlAsync`) and parse
      the HTML table elements. ## Conclusion You now know **how to use Aspose** to
      read a scanned PDF, extract scanned PDF text, and **convert PDF to tex'
    question: What if the PDF contains tables?
  type: FAQPage
tags:
- Aspose.PDF.AI
- OCR
- C#
- PDF processing
title: 如何使用 Aspose 从扫描的 PDF 中提取文本——一步步指南
url: /zh/net/text/how-to-use-aspose-to-extract-text-from-a-scanned-pdf-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose 从扫描的 PDF 中提取文本 – 步骤指南

如果您需要 **how to use Aspose** 进行 OCR，本指南将展示如何使用几行 C# 代码提取扫描 PDF 的文本。无论您是构建文档归档服务还是为旧文件构建搜索索引，该解决方案都适用于您提供给 Aspose.Pdf.AI 服务的任何扫描 PDF。

在本教程中，您将：

* 创建一个读取扫描 PDF 的 OCR 副驾驶（copilot）。
* 异步提取识别后的文本。
* 显示或进一步处理提取的字符串。

唯一的前提条件是拥有有效的 Aspose.Pdf.AI 订阅以及 .NET 6（或更高）开发环境。

## 前提条件

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6 SDK 或更高版本 | 提供 `async Main` 和现代语言特性。 |
| Aspose.Pdf.AI NuGet 包（`Aspose.Pdf.AI`） | 包含 `AICopilotFactory` 和 OCR 选项。 |
| 有效的 Aspose.Pdf.AI `client` 实例（API 密钥） | 对云服务的请求进行身份验证。 |
| 扫描的 PDF 文件（例如 `Scanned.pdf`） | 将从中提取文本的源文档。 |

使用 .NET CLI 安装包：

```bash
dotnet add package Aspose.Pdf.AI
```

## 第一步：设置 Aspose.Pdf.AI 客户端

在调用任何 OCR 接口之前，必须创建一个保存您 API 凭证的客户端。该客户端是线程安全的，可在多个文档之间复用。

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual API key and base URL if you use a private cloud.
var client = new PdfAiClient(new PdfAiConfiguration
{
    ApiKey = "YOUR_API_KEY",
    // BaseUrl = "https://api.aspose.cloud" // default, change only if needed
});
```

**为什么需要此步骤** – Aspose 服务会根据您的订阅验证每个请求。一次性创建客户端可避免重复的网络握手，并保持代码简洁。

## 第二步：为扫描的 PDF 文档创建 OCR 副驾驶

`AICopilotFactory` 会构建一个专门的 OCR 副驾驶，能够处理您指定的文件。您需要传入 `client` 和指向 PDF 路径的 `OpenAIOcrOptions` 对象。

```csharp
using Aspose.Pdf.AI;

// Step 2: Build the OCR copilot
var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
    client,                                   // Your Aspose.Pdf.AI client instance
    OpenAIOcrOptions.Create()
        .WithDocument("YOUR_DIRECTORY/Scanned.pdf") // Path to the scanned PDF
);
```

**说明** – `CreateOcrCopilot` 封装了所有底层 HTTP 调用。`WithDocument` 方法告诉服务要分析哪个文件；如果 PDF 位于内存中，也可以提供 `Stream`。

## 第三步：异步提取识别文本

调用 `GetTextAsync` 会在云端运行 OCR 操作并返回纯文本结果。由于该操作可能需要几秒钟时间，方法采用异步方式。

```csharp
// Step 3: Perform OCR and get the text
string ocrText = await ocrCopilot.GetTextAsync();
```

**为什么使用异步** – 网络延迟和 OCR 处理时间不可预测。使用 `await` 可防止应用阻塞主线程，这在 UI 或 Web 服务场景中尤为重要。

## 第四步：使用提取的文本

此时您已经拥有一个普通的 .NET `string`，其中包含扫描 PDF 的完整转录。您可以将其写入控制台、存入数据库，或送入搜索引擎。

```csharp
// Step 4: Display the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrText);
```

### 预期输出

如果 `Scanned.pdf` 包含一页，内容为 “Hello, world!”，控制台将显示：

```
=== OCR Result ===
Hello, world!
```

对于多页文档，输出会将每页的文本连接在一起，保留换行符。

## 完整、可运行的示例

下面是一个完整的程序示例，您可以将其粘贴到新建的控制台项目（`dotnet new console`）中。它演示了 **how to use Aspose** 的完整流程，并包含常见错误的处理方式。

```csharp
using System;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

namespace AsposeOcrDemo
{
    class Program
    {
        static async Task Main(string[] args)
        {
            // 1️⃣ Initialize the Aspose.Pdf.AI client
            var client = new PdfAiClient(new PdfAiConfiguration
            {
                ApiKey = "YOUR_API_KEY"
                // BaseUrl = "https://api.aspose.cloud" // optional
            });

            // 2️⃣ Build the OCR copilot for the target PDF
            var pdfPath = "YOUR_DIRECTORY/Scanned.pdf";
            var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
                client,
                OpenAIOcrOptions.Create().WithDocument(pdfPath)
            );

            try
            {
                // 3️⃣ Extract text asynchronously
                string ocrText = await ocrCopilot.GetTextAsync();

                // 4️⃣ Use the extracted text (display in console)
                Console.WriteLine("=== OCR Result ===");
                Console.WriteLine(ocrText);
            }
            catch (Exception ex)
            {
                // Common errors: invalid API key, missing file, unsupported PDF version
                Console.Error.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

**示例中的关键点**

* `await` 确保非阻塞执行。
* `try/catch` 块捕获网络或服务错误，这在大规模 **reading scanned PDF** 时尤为关键。
* 在运行前将 `YOUR_API_KEY` 和 `YOUR_DIRECTORY/Scanned.pdf` 替换为真实值。

## 处理边缘情况和最佳实践提示

| Situation | Recommended approach |
|-----------|----------------------|
| **Large PDFs ( > 50 MB )** | 在客户端将文档拆分为更小的块，并使用独立的副驾驶处理每个块。这样可降低内存压力并提升可靠性。 |
| **Low‑quality scans** | 通过在 `OpenAIOcrOptions` 中添加 `.WithLanguage("eng")` 或 `.WithEnhanceImage(true)` 来调整 OCR 质量。服务支持语言提示，可提升准确率。 |
| **Multiple languages** | 提供逗号分隔的列表，例如 `.WithLanguage("eng,spa")`。OCR 引擎会检测并转录这两种语言。 |
| **Non‑PDF image files** | 首先将图像转换为 PDF（使用 `Aspose.Pdf` 库），或使用 `OpenAIOcrOptions.WithImage` 直接发送图像。 |
| **Rate‑limit exceeded** | 实现指数退避和重试逻辑；当超出配额时，Aspose API 会返回 HTTP 429。 |

### 专业提示

如果计划后续复用提取结果，请缓存 `ocrText`。OCR 操作是工作流中最耗时的环节，复用字符串可避免重复调用 API，节省配额。

## 常见问题

**Q: 这能处理受密码保护的 PDF 吗？**  
A: 可以。在创建副驾驶之前，在选项构建器中添加 `.WithPassword("yourPassword")`。

**Q: 能否以结构化格式（例如带页码的 JSON）提取文本？**  
A: 使用 `GetTextStructureAsync()` 替代 `GetTextAsync()`。该方法返回包含页索引、边界框和置信度分数的 JSON 负载。

**Q: 如果 PDF 包含表格怎么办？**  
A: 纯文本提取会将表格展平成以换行分隔的行。若需更丰富的数据，可请求 PDF 转 HTML（`GetHtmlAsync`），然后解析 HTML 表格元素。

## 结论

您现在已经掌握 **how to use Aspose** 读取扫描 PDF、提取扫描 PDF 文本，并使用最小的 C# 程序 **convert PDF to text**。整个流程包括创建 OCR 副驾驶、调用 `GetTextAsync`，以及处理返回的字符串。遵循边缘情况的建议后，您即可将该方案扩展到大批量文档、多语言内容以及受保护的 PDF。

接下来，您可以进一步探索：

* 使用布局保留的方式提取文本（`GetHtmlAsync`）。
* 使用 Aspose.Pdf.AI **extract tables** 并导出为 CSV。
* 将 OCR 输出集成到 Azure Cognitive Search，实现可搜索的文档归档。

祝编码愉快，尽情体验 Aspose AI 驱动 OCR 为您的扫描 PDF 工作流带来的高精度吧！

## 接下来您应该学习什么？

以下教程涵盖与本指南密切相关的主题，帮助您在自己的项目中进一步掌握 API 功能并探索替代实现方式。每个资源都提供完整的可运行代码示例和逐步解释。

- [使用 Aspose.PDF for .NET 提取 PDF 文件文本](/pdf/english/net/text-operations/extract-text-pdf-aspose-dotnet/)
- [使用 Aspose.PDF for .NET 从 PDF 中提取特定区域的文本](/pdf/english/net/text-operations/extract-text-specific-region-aspose-pdf-net/)
- [使用 Aspose.PDF for .NET 提取 PDF 中的高亮文本](/pdf/english/net/text-operations/extract-highlighted-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}