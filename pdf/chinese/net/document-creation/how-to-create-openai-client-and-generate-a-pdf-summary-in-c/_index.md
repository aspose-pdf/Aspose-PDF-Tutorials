---
category: general
date: 2026-10-10
description: 在 C# 中创建 OpenAI 客户端，学习如何对 PDF 进行摘要，将 PDF 转换为摘要，并使用 Aspose.Pdf.AI 保存生成的
  PDF 摘要。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create openai client
- convert pdf to summary
- how to summarize pdf
- how to save summary
- generate pdf summary
language: zh
lastmod: 2026-10-10
og_description: 在 C# 中创建 OpenAI 客户端，立即学习如何对 PDF 进行摘要、将 PDF 转换为摘要，并保存生成的 PDF 摘要。
og_image_alt: Screenshot of C# code that creates an OpenAI client and generates a
  PDF summary
og_title: 在 C# 中创建 OpenAI 客户端并生成 PDF 摘要 – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create OpenAI client in C# and learn how to summarize a PDF, convert
    PDF to summary, and save the generated PDF summary with Aspose.Pdf.AI.
  headline: How to create OpenAI client and generate a PDF summary in C#
  type: TechArticle
- description: Create OpenAI client in C# and learn how to summarize a PDF, convert
    PDF to summary, and save the generated PDF summary with Aspose.Pdf.AI.
  name: How to create OpenAI client and generate a PDF summary in C#
  steps:
  - name: '**Console output** – the plain‑text summary displayed on the screen.'
    text: '**Console output** – the plain‑text summary displayed on the screen.'
  - name: '**`Summary_out.pdf`** – a downloadable PDF containing the same summary,
      ready for distribution.'
    text: '**`Summary_out.pdf`** – a downloadable PDF containing the same summary,
      ready for distribution.'
  - name: Lower the `WithTemperature` to 0.2 for more deterministic output.
    text: Lower the `WithTemperature` to 0.2 for more deterministic output.
  - name: Increase the
    text: Increase the
  type: HowTo
tags:
- OpenAI
- C#
- PDF processing
- Aspose.Pdf.AI
title: 如何在 C# 中创建 OpenAI 客户端并生成 PDF 摘要
url: /zh/net/document-creation/how-to-create-openai-client-and-generate-a-pdf-summary-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中创建 OpenAI 客户端并生成 PDF 摘要

如果您需要在 .NET 应用程序中 **创建 OpenAI 客户端**，本教程将准确演示如何操作以及如何将任意 PDF 转换为简洁的 AI 生成摘要。您将看到如何 **将 PDF 转换为摘要**、检索文本，并 **将摘要保存** 为新的 PDF 文件——全部使用 Aspose.Pdf.AI。

对 PDF 进行摘要是文档密集型工作流（如法律审查、研究汇总或自动化报告生成）的常见需求。阅读完本指南后，您将能够以编程方式 **生成 PDF 摘要**，无需离开 C# 代码库。

## 您需要的环境

- .NET 6.0 或更高（示例针对 .NET 6，但任何近期的 .NET 版本均可使用）
- Aspose.Pdf.AI NuGet 包 (`Aspose.Pdf.AI`) —— 此包装器简化了对 PDF 内容的 OpenAI 调用
- 有效的 OpenAI API 密钥（可从 OpenAI 门户获取）
- 您想要摘要的示例 PDF 文件（例如 `SampleDocument.pdf`）
- Visual Studio 2022、VS Code 或任何支持 C# 开发的 IDE

> **专业提示：** 将您的 API 密钥保存在安全位置，例如 [user‑secrets](https://learn.microsoft.com/en-us/aspnet/core/security/app-secrets) 或 Azure Key Vault。切勿在源代码控制中硬编码。

## 第一步：安装 Aspose.Pdf.AI NuGet 包

在项目文件夹中打开终端并运行：

```bash
dotnet add package Aspose.Pdf.AI
```

该包会引入必要的 HTTP 客户端、PDF 操作工具以及围绕 OpenAI API 的轻量包装器。安装完成后，恢复项目以确保所有依赖可用：

```bash
dotnet restore
```

## 第二步：使用您的 API 密钥 **创建 OpenAI 客户端**

创建客户端是进行任何 AI 驱动的 PDF 操作的第一步。`OpenAIClient` 为您处理身份验证、请求限流和连接池。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.AI;
using System;
using System.Threading.Tasks;

class PdfSummarizer
{
    // Replace with your real key – never commit it to source control
    private const string ApiKey = "YOUR_OPENAI_API_KEY";

    public static async Task Main()
    {
        // ---- Step 2: create OpenAI client ----
        using var openAiClient = OpenAIClient
            .CreateWithApiKey(ApiKey)
            .Build();

        // The client is now ready for any Aspose.Pdf.AI operation.
        await SummarizePdfAsync(openAiClient);
    }
}
```

> **原因说明：** `using` 语句确保客户端得到正确释放，释放网络资源，避免在长时间运行的服务中出现套接字耗尽。

## 第三步：配置摘要选项 – **将 PDF 转换为摘要**

`OpenAISummaryCopilotOptions` 对象告诉 AI 要执行的操作。您可以调整 temperature、限制 token 使用量，最重要的是指定源 PDF。

```csharp
private static async Task SummarizePdfAsync(OpenAIClient client)
{
    // ---- Step 3: set up summary options (convert PDF to summary) ----
    var summaryOptions = OpenAISummaryCopilotOptions
        .Create()
        .WithTemperature(0.5)                     // Balanced creativity vs. factuality
        .WithDocument("YOUR_DIRECTORY/SampleDocument.pdf");

    // The options are immutable; each call returns a new instance.
```

### 为什么使用 temperature 0.5？

temperature 为 0.5 时，可生成简洁、准确的语言，同时仍允许模型改写句子。更高的值（例如 0.9）会使输出更具创意，但可能偏离原意——这在法律或技术摘要中是不理想的。

## 第四步：**如何摘要 PDF** – 实例化 copilot 并获取文本

现在客户端和选项已准备就绪，创建一个 summary copilot。该对象协调对 OpenAI 的请求，并以多种格式返回结果。

```csharp
    // ---- Step 4: instantiate the summary copilot (how to summarize PDF) ----
    var summaryCopilot = AICopilotFactory
        .CreateSummaryCopilot(client, summaryOptions);

    // Retrieve the generated summary as plain text
    string summaryText = await summaryCopilot.GetSummaryAsync();

    Console.WriteLine("=== Text Summary ===");
    Console.WriteLine(summaryText);
```

`GetSummaryAsync` 方法返回干净的纯文本版本，您可以将其嵌入 UI、通过电子邮件发送或存入数据库。

## 第五步：以 PDF 文档形式检索摘要

如果您需要可携带、可打印的版本，可让 copilot 生成 PDF 文档。本步骤演示如何直接从 AI 模型 **生成 PDF 摘要**。

```csharp
    // ---- Step 5: retrieve the summary as a PDF document (generate PDF summary) ----
    Document summaryDocument = await summaryCopilot.GetSummaryDocumentAsync();

    // Optionally, you can add a cover page or watermark here before saving.
```

返回的 `Aspose.Pdf.Document` 在 Aspose 生态系统中表现如同其他 PDF 对象，这意味着您可以进一步编辑页面、添加元数据或与其他 PDF 合并。

## 第六步：**如何保存摘要** – 将 PDF 持久化到磁盘

最后，将生成的摘要存储在文件系统中。`SaveSummaryAsync` 辅助方法在一次调用中完成检索和保存，但我们也会展示显式保存的完整示例。

```csharp
    // ---- Step 6: save the summary PDF (how to save summary) ----
    const string outputPath = "YOUR_DIRECTORY/Summary_out.pdf";

    // Direct helper method
    await summaryCopilot.SaveSummaryAsync(outputPath);

    // Or, save the Document object manually
    // summaryDocument.Save(outputPath);
    Console.WriteLine($"Summary PDF saved to: {outputPath}");
}
```

> **提示：** 如果需要强制使用命名约定（例如带时间戳的文件），可使用 `DateTime.UtcNow:yyyyMMdd_HHmmss` 编程构建路径。

### 完整可运行示例

将所有内容组合在一起，以下是一个可自行复制粘贴到 `Program.cs` 并运行的完整程序示例：

```csharp
using Aspose.Pdf;
using Aspose.Pdf.AI;
using System;
using System.Threading.Tasks;

class PdfSummarizer
{
    private const string ApiKey = "YOUR_OPENAI_API_KEY";

    public static async Task Main()
    {
        // Create OpenAI client
        using var openAiClient = OpenAIClient
            .CreateWithApiKey(ApiKey)
            .Build();

        // Configure summary options (convert PDF to summary)
        var summaryOptions = OpenAISummaryCopilotOptions
            .Create()
            .WithTemperature(0.5)
            .WithDocument("YOUR_DIRECTORY/SampleDocument.pdf");

        // Instantiate the copilot (how to summarize PDF)
        var summaryCopilot = AICopilotFactory
            .CreateSummaryCopilot(openAiClient, summaryOptions);

        // Get plain‑text summary
        string summaryText = await summaryCopilot.GetSummaryAsync();
        Console.WriteLine("=== Text Summary ===");
        Console.WriteLine(summaryText);

        // Get PDF version (generate PDF summary)
        Document summaryDoc = await summaryCopilot.GetSummaryDocumentAsync();

        // Save the PDF (how to save summary)
        const string outPath = "YOUR_DIRECTORY/Summary_out.pdf";
        await summaryCopilot.SaveSummaryAsync(outPath);
        Console.WriteLine($"Summary PDF saved to: {outPath}");
    }
}
```

运行程序会生成两个产物：

1. **控制台输出** – 屏幕上显示的纯文本摘要。
2. **`Summary_out.pdf`** – 包含相同摘要的可下载 PDF，已准备好分发。

## 常见变体和边缘情况

| Situation | Recommended tweak |
|-----------|-------------------|
| **大型 PDF（> 10 MB）** | 将文档拆分为更小的块（例如按章节），分别对每个块进行摘要。使用 `Document.AppendDocument` 合并结果。 |
| **需要自定义提示** | 在调用 `CreateSummaryCopilot` 之前使用 `WithPrompt("Summarize the following legal contract in bullet points:")`。 |
| **非英文源 PDF** | 设置 `WithLanguage("es")`（或相应的 ISO 代码）以引导模型的语言处理。 |
| **速率限制错误** | 增加 `WithRetryCount` 或在调用之间添加 `Task.Delay`。 |
| **保存到云存储** | 将文件系统路径替换为流 (`MemoryStream`)，并将该流上传至 Azure Blob Storage 或 AWS S3。 |

## 验证结果

程序完成后，在任意 PDF 查看器中打开 `Summary_out.pdf`。您应看到一份干净的单页（或多页，取决于长度）文档，捕捉了 `SampleDocument.pdf` 的主要思想。将控制台打印的文本摘要与 PDF 版本进行对比——两者应完全一致。

如果摘要不完整：

1. 将 `WithTemperature` 降至 0.2，以获得更确定的输出。
2. 增加 

## 接下来您应该学习什么？

以下教程涵盖与本指南技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能，并在自己的项目中探索替代实现方案。

- [如何在 C# 中创建 PDF – 添加页面、绘制矩形并保存](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [学习如何使用 Aspose.PDF for .NET 生成 PDF 文档](/pdf/english/net/document-creation/)
- [如何使用 Aspose.PDF for .NET 创建标签 PDF – 提升可访问性](/pdf/english/net/bookmarks-navigation/tagged-pdf-creation-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}