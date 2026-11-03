---
category: general
date: 2026-10-26
description: 学习如何创建 OpenAI 客户端，使用 Aspose.Pdf.AI 将 PDF 转换为摘要并保存摘要 PDF，只需几个简单步骤。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create openai client
- convert pdf to summary
- generate pdf summary
- create summary copilot
- save summary pdf
language: zh
lastmod: 2026-10-26
og_description: 创建 OpenAI 客户端，将任意 PDF 转换为简洁摘要。本指南展示如何使用 Aspose.Pdf.AI 生成 PDF 摘要并保存摘要
  PDF。
og_image_alt: C# code displaying creation of OpenAI client and PDF summary generation
og_title: 使用 C# 创建 OpenAI 客户端并生成 PDF 摘要 – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to create OpenAI client, convert PDF to summary and save
    summary PDF using Aspose.Pdf.AI in a few easy steps.
  headline: How to create OpenAI client and generate a PDF summary in C#
  type: TechArticle
tags:
- openai
- pdf
- csharp
- summary
- ai
title: 如何在 C# 中创建 OpenAI 客户端并生成 PDF 摘要
url: /zh/net/programming-with-text/how-to-create-openai-client-and-generate-a-pdf-summary-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中创建 OpenAI 客户端并生成 PDF 摘要

如果您需要 **create OpenAI client**（创建 OpenAI 客户端）来读取 PDF 并返回简洁的摘要，本教程将准确演示如何操作。完成本指南后，您将能够 **convert PDF to summary**（将 PDF 转换为摘要），生成 **generate PDF summary**（生成 PDF 摘要）文档，并 **save summary PDF**（保存摘要 PDF）到磁盘——全部使用 Aspose.Pdf.AI。

您将看到完整的可运行示例、每行代码重要性的解释，以及处理常见陷阱（如大文件或自定义 temperature 参数）的技巧。无需外部文档；所有所需内容均已在此提供。

## 前提条件

* 已安装 .NET 6.0 或更高版本。  
* 包含 AI 模块的 Aspose.Pdf for .NET 许可证（或免费试用）。  
* 拥有足够额度用于摘要请求的 OpenAI API 密钥。  
* Visual Studio 2022（或任何支持 .NET 的 IDE）。

下面的代码针对 C# 10，但相同的概念同样适用于早期版本，只需进行少量语法更改。

## 步骤 1：创建 OpenAI 客户端

创建 OpenAI 客户端是所有 AI 驱动的 PDF 操作的基础。客户端封装了身份验证、HTTP 处理和请求限流，因此您只需提供一次 API 密钥。

```csharp
using System;
using System.Threading.Tasks;
using Aspose.Pdf;
using Aspose.Pdf.AI;

// Replace with your real key – never hard‑code it in production code.
const string ApiKey = "YOUR_OPENAI_API_KEY";

await using var openAiClient = OpenAIClient
    .CreateWithApiKey(ApiKey)   // supply your OpenAI key
    .Build();                    // builds a reusable HttpClient internally
```

**为什么这很重要：**  
* `CreateWithApiKey` 提前验证密钥格式，防止运行时出现 401 错误。  
* `Build()` 返回 `IAsyncDisposable`，因此在 `using` 块结束时会自动释放底层 HTTP 连接。  
* 使用 `await using` 可确保异步释放，这对高吞吐场景至关重要。

> **专业提示：** 将 API 密钥存储在环境变量 (`OPENAI_API_KEY`) 中，并使用 `Environment.GetEnvironmentVariable` 读取。这可防止密钥泄露到源码管理中。

## 步骤 2：配置 summary copilot 选项

summary copilot 决定 AI 处理 PDF 的方式。您可以通过 *temperature* 参数调整创造力，并指定源文档。

```csharp
var summaryOptions = OpenAISummaryCopilotOptions
    .Create()
    .WithTemperature(0.5)                     // 0 = deterministic, 1 = very creative
    .WithDocument("YOUR_DIRECTORY/input.pdf"); // path to the PDF you want to summarise
```

**为什么这很重要：**  
* `0.5` 的 temperature 提供平衡的输出——足够的多样性使语言自然，同时仍忠实于源文档。  
* `WithDocument` 将文件加载到 Aspose 的内部 PDF 解析器中，在发送给 OpenAI 之前提取文本、图像和布局信息。  
* 如果 PDF 大于 5 MB，建议将其拆分为多个章节，并分别进行摘要，以保持在 token 限制范围内。

## 步骤 3：创建 summary copilot

现在您已有客户端和选项，可以实例化 copilot。copilot 抽象了请求‑响应循环，并提供用于纯文本和 PDF 结果的辅助方法。

```csharp
ISummaryCopilot summaryCopilot = AICopilotFactory
    .CreateSummaryCopilot(openAiClient, summaryOptions);
```

**为什么这很重要：**  
* `AICopilotFactory` 确保 copilot 使用与客户端相同的 HTTP 管道，保持连接池。  
* 返回的 `ISummaryCopilot` 接口允许您以后替换实现（例如用于单元测试的 mock），而无需更改外围代码。

## 步骤 4：以纯文本获取摘要

如果您只需要文本摘要（用于日志、UI 显示或进一步处理），请调用 `GetSummaryAsync`。

```csharp
string summaryText = await summaryCopilot.GetSummaryAsync();
Console.WriteLine("=== Summary ===");
Console.WriteLine(summaryText);
```

**您将看到：**  
一段简明的文字（或几条要点），概括源 PDF 的主要思想。长度取决于原始文档和模型的 token 配额。

### 处理大输出

如果摘要比预期更长，您可以在构建 `summaryOptions` 时使用 `WithMaxTokens` 限制 token 数量。例如：

```csharp
summaryOptions = summaryOptions.WithMaxTokens(300);
```

## 步骤 5：生成 PDF 摘要（convert PDF to summary）

当您需要可视化的产物（例如与非技术利益相关者共享）时，请使用 PDF 生成方法。此步骤在一次调用中完成 **convert pdf to summary** 和 **generate pdf summary**。

```csharp
Document summaryDoc = await summaryCopilot.GetSummaryDocumentAsync();
```

返回的 `Document` 对象是完整的 Aspose.Pdf 文档，包含摘要文本、可选标题以及原始 PDF 的元数据（如果您保留了它）。

**为什么这很重要：**  
* PDF 保持矢量质量，适合打印或嵌入其他报告中。  
* Aspose 会自动添加包含源文件名和时间戳的标题页，有助于审计追踪。

## 步骤 6：保存摘要 PDF（save summary pdf）

最后，将生成的 PDF 写入磁盘。`SaveSummaryAsync` 辅助方法已将第 5 步和第 6 步合并，但我们将展示显式保存以说明文件系统的注意事项。

```csharp
string outputPath = "YOUR_DIRECTORY/Summary_out.pdf";
await summaryCopilot.SaveSummaryAsync(outputPath);
Console.WriteLine($"Summary PDF saved to {outputPath}");
```

**保存文件的最佳实践：**

| 情况                                    | 建议                                             |
|----------------------------------------|---------------------------------------------------|
| 在 Windows 和 Linux 上运行               | 使用 `Path.Combine` 构建跨 OS 的路径。           |
| 多个并发摘要                             | 在文件名后追加 GUID 或时间戳。                    |
| 长期运行的服务（例如 Web API）           | 将 PDF 存储在专用的 Blob 存储中，而不是本地文件系统。 |

## 完整、可运行的示例

下面是完整的程序，您可以复制粘贴到新的控制台项目（`dotnet new console`）中。它包含所有必需的 `using` 指令，并演示了从 **create openai client** 到 **save summary pdf** 的完整流程。

```csharp
// Program.cs
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.Pdf;
using Aspose.Pdf.AI;

class Program
{
    // Replace with your actual OpenAI key or read from env variables.
    private const string ApiKey = "YOUR_OPENAI_API_KEY";

    static async Task Main()
    {
        // 1️⃣ Create OpenAI client
        await using var openAiClient = OpenAIClient
            .CreateWithApiKey(ApiKey)
            .Build();

        // 2️⃣ Configure summary copilot options
        var summaryOptions = OpenAISummaryCopilotOptions
            .Create()
            .WithTemperature(0.5)
            .WithDocument("YOUR_DIRECTORY/input.pdf"); // path to source PDF

        // 3️⃣ Create the summary copilot
        ISummaryCopilot summaryCopilot = AICopilotFactory
            .CreateSummaryCopilot(openAiClient, summaryOptions);

        // 4️⃣ Get plain‑text summary (optional)
        string summaryText = await summaryCopilot.GetSummaryAsync();
        Console.WriteLine("=== Plain‑text summary ===");
        Console.WriteLine(summaryText);
        Console.WriteLine();

        // 5️⃣ Generate PDF summary (convert pdf to summary)
        Document summaryDoc = await summaryCopilot.GetSummaryDocumentAsync();

        // 6️⃣ Save the generated PDF (save summary pdf)
        string outputPath = Path.Combine("YOUR_DIRECTORY", "Summary_out.pdf");
        await summaryCopilot.SaveSummaryAsync(outputPath);
        Console.WriteLine($"✅ PDF summary saved at: {outputPath}");
    }
}
```

**预期输出**

```
=== Plain‑text summary ===
This document outlines the quarterly performance metrics, highlighting a 12% increase in revenue and a 5% reduction in operational costs...

✅ PDF summary saved at: YOUR_DIRECTORY\Summary_out.pdf
```

打开生成的 `Summary_out.pdf`，您会看到一个排版整齐的页面，包含相同的文本，以及带有原始文件名和时间戳的标题页。

## 常见问题与边缘情况

| 问题 | 回答 |
|----------|--------|
| *如果 PDF 包含扫描的图像怎么办？* | 当调用 `WithDocument` 时，Aspose.Pdf.AI 会自动运行 OCR，但您可以通过设置 `WithOcrLanguage("eng")` 提高准确性。 |
| *我能在一次调用中摘要多个 PDF 吗？* | 不能直接实现。为每个文件创建单独的 `summaryCopilot`，或在摘要前先将 PDF 合并。 |
| *如何更改输出语言？* | 使用 `summaryOptions.WithLanguage("fr")` 让模型返回法语文本。 |
| *如果请求超出 token 限制怎么办？* | 减少 `WithMaxTokens`，或将 PDF 拆分为多个章节并分别进行摘要。 |
| *生成的 PDF 可搜索吗？* | 可以。摘要文本以可选取的文字形式嵌入，而不是仅仅作为图像。 |

## 结论

现在您已经了解如何使用 Aspose.Pdf.AI 在 C# 中 **create OpenAI client**、配置 **create summary copilot**、**convert PDF to summary**、**generate PDF summary**，以及最终 **save summary pdf**。这一端到端的流程只需几行代码，即可为任何 .NET 应用程序添加 AI 驱动的摘要功能。

您可以进一步探索以下步骤：

* 使用 `WithPrompt("Summarise in three bullet points.")` **自定义提示工程**。  
* **与 ASP.NET Core 集成**，以提供按需返回摘要 PDF 的 REST 端点。  
* **结合其他 AI 服务**（例如翻译），生成多语言摘要。

欢迎尝试不同的 temperature、max‑token 设置和 OCR 选项，以满足项目的具体需求。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于所示技术进行扩展。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [使用 Aspose.Pdf.AI 和 OpenAI 生成 PDF 摘要](/pdf/english/net/programming-with-text/generate-pdf-summary-with-aspose-pdf-ai-and-openai/)
- [如何在 C# 中使用 Aspose.Pdf.AI 将 PDF 转换为摘要](/pdf/english/net/text-operations/how-to-convert-pdf-to-summary-with-aspose-pdf-ai-in-c/)
- [使用 Aspose.PDF .NET 创建 PDF 小册子：完整指南](/pdf/english/net/printing-rendering/create-pdf-booklet-using-asposepdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}