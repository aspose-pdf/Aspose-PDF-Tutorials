---
category: general
date: 2026-09-28
description: 在 C# 中初始化 OpenAI 客户端，并使用 AI 对 PDF 进行摘要，提取简洁的摘要并将其转换为 PDF 文件。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- initialize openai client
- summarize pdf with ai
- extract summary from pdf
- convert summary to pdf
- create summary copilot
language: zh
lastmod: 2026-09-28
og_description: 在 C# 中初始化 OpenAI 客户端，以使用 AI 对 PDF 进行摘要，提取摘要，并使用 Aspose.Pdf.AI 将其转换为
  PDF。
og_image_alt: Code editor view showing how to initialize OpenAI client in C#
og_title: 初始化 OpenAI 客户端并使用 AI 对 PDF 进行摘要 – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-09-28'
  description: Initialize OpenAI client in C# and summarize PDF with AI, extracting
    a concise summary and converting it to a PDF file.
  headline: How to initialize OpenAI client and summarize PDF with AI
  type: TechArticle
tags:
- OpenAI
- C#
- PDF processing
title: 如何初始化 OpenAI 客户端并使用 AI 对 PDF 进行摘要
url: /zh/net/document-creation/how-to-initialize-openai-client-and-summarize-pdf-with-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何初始化 OpenAI 客户端并使用 AI 摘要 PDF

如果您需要在 .NET 项目中 **初始化 OpenAI 客户端** 并 **使用 AI 摘要 PDF**，本指南提供了完整、可运行的解决方案。您将学习如何设置客户端、创建摘要 copilot、从 PDF 中提取简洁摘要，最后 **将摘要转换为 PDF**——全部配有清晰的代码示例和说明。

本教程涵盖了从必需的 NuGet 包到处理异步调用的所有内容，您可以直接复制粘贴最终程序到自己的解决方案中，立刻看到效果。

## 前置条件

在开始之前，请确保您具备：

* 已安装 .NET 6.0 或更高版本  
* 一个 OpenAI API 密钥（可在 OpenAI 门户获取）  
* **Aspose.Pdf.AI** NuGet 包 – 使用以下方式安装  

```bash
dotnet add package Aspose.Pdf.AI
```

无需额外的外部服务；提供 API 密钥后，代码将在本地完整运行。

## 步骤 1：初始化 OpenAI 客户端

第一步是 **初始化 OpenAI 客户端**。这会创建一个可复用的 HTTP 客户端，帮助您处理身份验证和请求限流。

```csharp
using var openAiClient = Aspose.Pdf.AI.OpenAIClient
    .CreateWithApiKey(Environment.GetEnvironmentVariable("OPENAI_API_KEY"))
    .Build();
```

*为什么重要*：只初始化一次并复用客户端可以避免重复握手、降低延迟，并确保您的 API 密钥永远不会硬编码在源码中。

> **专业提示**：将 API 密钥存放在环境变量或密钥管理器中。切勿将其提交到源码控制。

## 步骤 2：配置摘要 copilot 选项

接下来，需要告诉 AI 要摘要的内容以及方式。options 对象允许您设置 temperature（控制随机性）并指向源 PDF。

```csharp
var summaryOptions = Aspose.Pdf.AI.OpenAISummaryCopilotOptions.Create()
    .WithTemperature(0.5)                     // Balanced creativity vs. factuality
    .WithDocument("YOUR_DIRECTORY/SampleDocument.pdf"); // Path to the PDF you want to summarize
```

*为什么重要*：调整 temperature 能帮助您在 **从 PDF 中提取摘要** 时获得确定性的结果。0.5 是大多数业务文档的良好默认值。

## 步骤 3：创建摘要 copilot

现在，您通过将已初始化的客户端与刚才设置的 options 组合，**创建摘要 copilot**。copilot 抽象了底层的请求处理细节。

```csharp
var summaryCopilot = Aspose.Pdf.AI.AICopilotFactory
    .CreateSummaryCopilot(openAiClient, summaryOptions);
```

*为什么重要*：copilot 模式遵循单一职责原则——您的代码只需处理诸如 “GetSummaryAsync” 之类的高级操作，而无需手动构造原始 HTTP 负载。

## 步骤 4：异步生成摘要文本

调用 `GetSummaryAsync` 会将 PDF 发送至 OpenAI，运行摘要模型，并返回纯文本摘要。

```csharp
string summaryText = await summaryCopilot.GetSummaryAsync();
Console.WriteLine("=== Extracted Summary ===");
Console.WriteLine(summaryText);
```

此时，您已经在字符串变量中 **从 PDF 中提取了摘要**。典型输出如下：

```
=== Extracted Summary ===
This report outlines the quarterly revenue growth of 12% across all regions, highlights key product launches, and recommends strategic investments in cloud infrastructure.
```

## 步骤 5：将摘要转换为 PDF

最后一步是 **将摘要转换为 PDF**，以便像其他文档一样共享或归档。copilot 提供了便捷的 `SaveSummaryAsync` 方法。

```csharp
await summaryCopilot.SaveSummaryAsync("YOUR_DIRECTORY/Summary_out.pdf");
Console.WriteLine("Summary saved to Summary_out.pdf");
```

*为什么重要*：将摘要保存为 PDF 可保留格式，便于通过电子邮件附件发送，并且保持在您已经使用的文档生态系统中。

## 完整可运行示例

下面是一个完整的控制台应用程序示例，展示了所有步骤的组合。运行前请替换 `YOUR_DIRECTORY` 并设置 `OPENAI_API_KEY` 环境变量。

```csharp
// Program.cs
using System;
using System.Threading.Tasks;
using Aspose.Pdf.AI;

class Program
{
    static async Task Main()
    {
        // 1️⃣ Initialize the OpenAI client
        using var openAiClient = OpenAIClient
            .CreateWithApiKey(Environment.GetEnvironmentVariable("OPENAI_API_KEY"))
            .Build();

        // 2️⃣ Set up summary copilot options (temperature and source document)
        var summaryOptions = OpenAISummaryCopilotOptions.Create()
            .WithTemperature(0.5)
            .WithDocument("YOUR_DIRECTORY/SampleDocument.pdf");

        // 3️⃣ Create the summary copilot
        var summaryCopilot = AICopilotFactory
            .CreateSummaryCopilot(openAiClient, summaryOptions);

        // 4️⃣ Generate the summary text asynchronously
        string summaryText = await summaryCopilot.GetSummaryAsync();
        Console.WriteLine("=== Extracted Summary ===");
        Console.WriteLine(summaryText);

        // 5️⃣ Save the generated summary as a PDF file
        await summaryCopilot.SaveSummaryAsync("YOUR_DIRECTORY/Summary_out.pdf");
        Console.WriteLine("Summary saved to Summary_out.pdf");
    }
}
```

### 预期输出

```
=== Extracted Summary ===
[Your concise summary here]

Summary saved to Summary_out.pdf
```

在任意 PDF 查看器中打开 `Summary_out.pdf`——您将看到相同的文本，已被格式化为正式的 PDF 文档。

## 常见变体和边缘情况

| 场景 | 如何调整代码 |
|-----------|----------------------|
| **大文件 PDF（> 10 MB）** | 在 `summaryOptions` 中添加 `.WithTimeout(TimeSpan.FromMinutes(5))` 以延长超时时间。 |
| **自定义提示** | 使用 `.WithPrompt("Provide a bullet‑point summary focusing on financial metrics.")`。 |
| **多个 PDF** | 对文件路径列表进行循环，为每个文件创建新的 `summaryCopilot`，或在不同选项下复用同一客户端。 |
| **非英文文档** | 设置 `.WithLanguage("es")`，让模型以西班牙语生成摘要。 |
| **保存为其他格式** | 在 `GetSummaryAsync` 之后，您可以使用任意 PDF 库（如 iTextSharp）自行生成 PDF，但 `SaveSummaryAsync` 已覆盖最常见的场景。 |

## 生产环境使用技巧

* **速率限制** – OpenAI 对请求配额有限制。请在多次摘要时复用同一个 `openAiClient` 实例，以保持在配额范围内。  
* **错误处理** – 将异步调用包装在 `try/catch` 中，并检查 `OpenAIException` 以捕获限流或身份验证错误。  
* **安全性** – 切勿记录原始 API 密钥。使用安全的密钥存储（Azure Key Vault、AWS Secrets Manager 等）。  
* **测试** – 如需单元测试而不调用真实 API，可使用假实现来 Mock `OpenAIClient`。

## 结论

现在，您已经掌握了使用 Aspose.Pdf.AI 在 C# 中 **初始化 OpenAI 客户端**、**创建摘要 copilot**、**从 PDF 中提取摘要**以及**将摘要转换为 PDF**的完整流程。完整示例可端到端运行，为任何文档摘要工作流提供即插即用的解决方案。

接下来，您可以进一步探索：

* **使用 AI 摘要 PDF** 进行批量归档处理  
* 为生成的 PDF 添加 **元数据**（作者、日期）  
* 将摘要步骤集成到更大的 **文档管理流水线** 中  

欢迎尝试不同的 temperature 值、自定义提示或多语言摘要，以便将输出精准匹配到您的业务领域。祝编码愉快！

## 接下来该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式。每篇资源均提供完整可运行的代码示例和逐步说明。

- [Extract & Convert PDF Regions to Images with Aspose.PDF](/pdf/english/net/images-graphics/extract-convert-pdf-regions-aspose-net/)
- [Extract Convert Pdf Regions Aspose Net](/pdf/german/net/images-graphics/extract-convert-pdf-regions-aspose-net/)
- [Extract Convert Pdf Regions Aspose Net](/pdf/french/net/images-graphics/extract-convert-pdf-regions-aspose-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}