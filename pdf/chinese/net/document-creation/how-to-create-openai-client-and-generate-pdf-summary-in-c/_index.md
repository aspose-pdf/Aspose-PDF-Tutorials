---
category: general
date: 2026-11-25
description: 在 C# 中创建 OpenAI 客户端，并从源文档生成 PDF 摘要。学习如何将 PDF 转换为摘要，创建摘要副驾驶，并保存 PDF 摘要。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create openai client
- generate pdf summary
- convert pdf to summary
- create summary copilot
- save pdf summary
language: zh
lastmod: 2026-11-25
og_description: 在 C# 中创建 OpenAI 客户端并从源文档生成 PDF 摘要。按照本分步指南将 PDF 转换为摘要，创建摘要助手，并保存 PDF
  摘要。
og_image_alt: Screenshot showing C# code that creates an OpenAI client and saves a
  PDF summary
og_title: 在 C# 中创建 OpenAI 客户端并生成 PDF 摘要
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Create OpenAI client in C# and generate a PDF summary from a source
    document. Learn how to convert PDF to summary, create summary copilot, and save
    PDF summary.
  headline: How to create OpenAI client and generate PDF summary in C#
  type: TechArticle
tags:
- OpenAI
- C#
- PDF summary
- Aspose.Pdf.AI
title: 如何在 C# 中创建 OpenAI 客户端并生成 PDF 摘要
url: /zh/net/document-creation/how-to-create-openai-client-and-generate-pdf-summary-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中创建 OpenAI 客户端并生成 PDF 摘要

如果您需要 **创建 OpenAI 客户端** 来进行文档处理任务，本指南将为您展示一个完整的端到端解决方案。您将看到如何将 PDF 文件转换为简明摘要，如何以纯文本和新 PDF 两种形式获取摘要，最后将该 PDF 摘要保存到磁盘。

在需要自动化报告提取、创建执行摘要，或仅仅将大型文档浓缩为关键要点时，生成 PDF 摘要是一项常见需求。下面的代码示例使用 Aspose.Pdf.AI，它封装了 OpenAI API 并为 PDF 文件提供了便捷的 *summary copilot*。

## 前置条件

- 已安装 .NET 6.0 或更高版本  
- 已在项目中添加 Aspose.Pdf.AI NuGet 包 (`Aspose.Pdf.AI`)  
- 拥有有效的 OpenAI API 密钥（可从 OpenAI 门户获取）  
- 需要摘要的 PDF 文件（例如放在已知文件夹中的 `input.pdf`）

本教程假设您使用 Visual Studio，但任何 C# IDE 都可工作。

## 在 C# 中创建 OpenAI 客户端

第一步是使用您的 API 密钥 **创建 OpenAI 客户端**。客户端对象负责所有后续 AI 操作的身份验证和请求路由。

```csharp
// Step 1: Initialize the OpenAI client with your API key
using var openAiClient = Aspose.Pdf.AI.OpenAIClient
    .CreateWithApiKey("YOUR_API_KEY")
    .Build();
```

*为什么重要*：`OpenAIClient` 封装了 HTTP 层，处理令牌续订，并确保对摘要服务的所有调用都得到正确授权。通过使用 `using var`，客户端在方法退出时会自动释放，及时释放资源。

## 配置摘要选项（将 PDF 转换为摘要）

接下来您需要配置 AI 对源文档的处理方式。选项允许您设置 *temperature*（控制随机性）并指定要摘要的 PDF。

```csharp
// Step 2: Configure summary options (temperature and source document)
var summaryOptions = Aspose.Pdf.AI.OpenAISummaryCopilotOptions.Create()
    .WithTemperature(0.5)                     // Balanced creativity vs. factuality
    .WithDocument("YOUR_DIRECTORY/input.pdf"); // Path to the PDF you want to summarise
```

*为什么重要*：将 temperature 设置为适中的 0.5 可以获得可靠、简洁的摘要，避免更高值可能产生的幻觉。`WithDocument` 调用告诉 copilot 读取哪个文件，从而实现 **将 PDF 转换为摘要**。

## 构建摘要 copilot（创建摘要 copilot）

在客户端和选项准备就绪后，您现在可以 **创建摘要 copilot**。该 copilot 对象提供异步方法，以不同格式获取摘要。

```csharp
// Step 3: Create the summary copilot using the client and options
var summaryCopilot = Aspose.Pdf.AI.AICopilotFactory
    .CreateSummaryCopilot(openAiClient, summaryOptions);
```

*为什么重要*：工厂模式将创建逻辑隔离，便于以后替换实现（例如用于单元测试的 mock copilot）。生成的 `summaryCopilot` 是所有摘要操作的主要入口。

## 获取纯文本摘要

如果您只需要文本内容，调用 `GetSummaryAsync`。该方法返回一个字符串，您可以显示、记录或进一步处理。

```csharp
// Step 4: Retrieve the plain‑text summary
string plainTextSummary = await summaryCopilot.GetSummaryAsync();
Console.WriteLine("=== Plain‑text summary ===");
Console.WriteLine(plainTextSummary);
```

*预期输出*：一段简洁的文字（或几条要点），概括 `input.pdf` 的核心内容。具体措辞取决于源文档，但对于一般的 10 页报告，长度通常在 200 字以内。

## 获取 PDF 文档形式的摘要（生成 PDF 摘要）

当您需要可共享的成果时，可向 copilot 请求摘要的 PDF 版本。此步骤 **生成 PDF 摘要** 直接来自 AI 服务。

```csharp
// Step 5: Retrieve the summary as a PDF document
var pdfSummary = await summaryCopilot.GetSummaryDocumentAsync();
```

`pdfSummary` 是一个 `Aspose.Pdf.Document` 对象，可进一步操作（例如添加封面页）或直接保存。

## 将 PDF 摘要保存到文件（保存 PDF 摘要）

最后，使用 copilot 的辅助方法持久化生成的 PDF。这演示了单行代码完成 **保存 PDF 摘要** 的操作。

```csharp
// Step 6: Save the PDF summary to a file
await summaryCopilot.SaveSummaryAsync("YOUR_DIRECTORY/Summary_out.pdf");
Console.WriteLine("PDF summary saved to YOUR_DIRECTORY/Summary_out.pdf");
```

*为什么重要*：`SaveSummaryAsync` 方法使用 Aspose 高性能 PDF 引擎写入文档，保留字体、布局和元数据。保存的文件可在任何 PDF 查看器中打开。

## 完整示例

下面是将所有部分组合在一起的完整程序。将代码复制到新的控制台项目中，并将占位符值（`YOUR_API_KEY`、`YOUR_DIRECTORY`）替换为真实数据。

```csharp
using System;
using System.Threading.Tasks;
using Aspose.Pdf.AI;

class Program
{
    static async Task Main()
    {
        // Initialize the OpenAI client
        using var openAiClient = OpenAIClient
            .CreateWithApiKey("YOUR_API_KEY")
            .Build();

        // Configure options for summarizing a PDF
        var summaryOptions = OpenAISummaryCopilotOptions.Create()
            .WithTemperature(0.5)
            .WithDocument("YOUR_DIRECTORY/input.pdf");

        // Create the summary copilot
        var summaryCopilot = AICopilotFactory
            .CreateSummaryCopilot(openAiClient, summaryOptions);

        // Get plain‑text summary
        string plainText = await summaryCopilot.GetSummaryAsync();
        Console.WriteLine("=== Plain‑text summary ===");
        Console.WriteLine(plainText);

        // Get PDF version of the summary
        var pdfDoc = await summaryCopilot.GetSummaryDocumentAsync();

        // Save the PDF summary
        await summaryCopilot.SaveSummaryAsync("YOUR_DIRECTORY/Summary_out.pdf");
        Console.WriteLine("PDF summary saved to YOUR_DIRECTORY/Summary_out.pdf");
    }
}
```

### 预期结果

运行程序后，控制台会打印出纯文本摘要，并在目标文件夹中生成 `Summary_out.pdf`。打开该 PDF 可看到一个整洁、格式化的文档，包含相同的摘要文本，已准备好分发。

![创建 OpenAI 客户端并保存 PDF 摘要的 C# 代码截图](openai-pdf-summary.png){.center width="600" alt="创建 OpenAI 客户端并保存 PDF 摘要的 C# 代码截图"}

## 常见问题与边缘情况

| 问题 | 回答 |
|------|------|
| **如果源 PDF 受密码保护怎么办？** | 使用接受流的 `WithDocument` 重载，并通过 `PdfLoadOptions` 提供密码。copilot 在摘要之前会解密文件。 |
| **我可以更改摘要长度吗？** | 调整 temperature 或在 `summaryOptions` 中添加 `WithMaxTokens`。较低的 token 限制会产生更短的输出。 |
| **我需要互联网连接吗？** | 需要。copilot 通过 HTTPS 调用 OpenAI 服务，因此需要稳定的网络连接。 |
| **如何处理大 PDF（> 100 页）？** | 将文档拆分为更小的块，分别对每个块进行摘要，然后合并结果。这可以避免触及 token 限制。 |
| **生成的 PDF 可搜索吗？** | PDF 包含可选择的文本，因为摘要是以文本形式渲染的，而不是图像。 |

## 实战技巧

- **专业提示**：如果要摘要大量文档，请在应用程序生命周期内缓存 `OpenAIClient` 实例。这可以减少连接开销。  
- **注意**：使用高于 0.7 的 temperature 可能会产生幻觉式细节，  

## 接下来应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于所示技术进行扩展。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能，并在自己的项目中探索替代实现方案。

- [如何在 C# 中使用 Aspose.Pdf.AI 初始化 OpenAI API 客户端并使用 AI 摘要 PDF](/pdf/english/net/document-creation/how-to-initialize-openai-client-and-summarize-pdf-with-ai/)
- [如何在 C# 中使用 Aspose.Pdf.AI 将 PDF 转换为摘要](/pdf/english/net/text-operations/how-to-convert-pdf-to-summary-with-aspose-pdf-ai-in-c/)
- [使用 Aspose.Pdf.AI 和 OpenAI 生成 PDF 摘要](/pdf/english/net/programming-with-text/generate-pdf-summary-with-aspose-pdf-ai-and-openai/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}