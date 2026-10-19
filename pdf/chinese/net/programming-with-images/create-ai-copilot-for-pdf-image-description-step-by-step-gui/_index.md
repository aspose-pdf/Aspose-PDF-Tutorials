---
category: general
date: 2026-08-04
description: 创建 AI 副驾驶，为 PDF 文件生成图像描述。学习如何配置 OpenAI 图像选项并高效提取图像描述。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create AI copilot
- generate image description
- image description PDF
- OpenAI image options
- extract image description
language: zh
lastmod: 2026-08-04
og_description: 创建 AI 副驾驶，为 PDF 文件生成图像描述。本教程展示如何配置 OpenAI 图像选项、运行副驾驶并在 C# 中提取图像描述。
og_image_alt: Screenshot of C# code that creates an AI copilot for PDF image description
og_title: 为PDF图像描述创建AI副驾驶——完整指南
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create AI Copilot to generate image description for PDF files. Learn
    how to configure OpenAI image options and extract image description efficiently.
  headline: Create AI Copilot for PDF image description – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Pdf.AI
- C#
- PDF processing
title: 为 PDF 图像描述创建 AI 副驾驶——分步指南
url: /zh/net/programming-with-images/create-ai-copilot-for-pdf-image-description-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 为 PDF 图像描述创建 AI 副驾驶 – 完整指南

如果您需要 **创建 AI 副驾驶**，它能够自动为 PDF 中嵌入的图像编写描述，本指南将准确展示如何操作。您将学习配置 OpenAI 图像选项、运行副驾驶，并在不离开 C# 项目的情况下 **提取图像描述**。

为 PDF 图像生成文本内容是实现可访问性、内容索引和自动化报告的常见需求。完成本教程后，您将拥有一个可复用的组件，能够为任意指向的 PDF 文档 **生成图像描述**。

## 前提条件

* .NET 6.0 或更高版本已安装  
* Aspose.Pdf.AI 许可证（或免费试用）  
* Aspose 客户端可使用的 OpenAI API 密钥  
* Visual Studio 2022（或任何支持 C# 的 IDE）  

除了 `Aspose.Pdf.AI` 外，无需其他 NuGet 包。

## 步骤 1：设置 Aspose.Pdf.AI 客户端

第一步是使用您的身份验证信息实例化 AI 客户端。客户端在后台处理与 OpenAI 服务的通信。

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual credentials
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    // Optional: set a custom endpoint if you use Azure OpenAI
    // Endpoint = "https://my-openai-instance.openai.azure.com/"
});
```

**为什么这很重要：** `AiClient` 封装了所有请求级别的设置（API 密钥、超时、重试策略）。只创建一次并在多个副驾驶实例中复用，可降低开销并确保身份验证一致。

## 步骤 2：创建图像描述副驾驶

现在您将创建 **AI 副驾驶**，它会读取 PDF 并为每个图像生成描述。`CreateImageDescriptionCopilot` 工厂方法接受客户端以及一组定义描述生成方式的选项。

```csharp
// Configure OpenAI image options – this is where you control model, temperature, etc.
var imageOptions = OpenAIImageDescriptionOptions.Create()
    .WithModel("gpt-4o-mini")           // Choose a model that balances cost and quality
    .WithTemperature(0.7)               // Controls creativity; 0 = deterministic
    .WithMaxTokens(150);                // Maximum length of each description

// Point the copilot at the PDF you want to process
var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
    client,
    imageOptions.WithDocument(@"C:\Reports\AnnualReport.pdf"));
```

**为什么这很重要：**  
* `OpenAIImageDescriptionOptions`（即 **OpenAI 图像选项**）让您微调语言模型。调整 temperature 或模型可以提升对技术图表与自然照片的相关性。  
* 指定文档路径告诉副驾驶要扫描哪个 PDF。副驾驶会提取所有光栅图像，将其发送至模型，并返回可读的描述。

## 步骤 3：异步检索生成的描述

副驾驶以异步方式工作，因为它可能需要上传数兆字节的图像数据并等待模型响应。使用 `await` 可确保调用完成后再访问结果。

```csharp
try
{
    // Get a dictionary where the key is the page number and the value is the description
    var descriptionMap = await imgCopilot.GetDescriptionAsync();

    // Example: iterate over each image description
    foreach (var entry in descriptionMap)
    {
        Console.WriteLine($"Page {entry.Key}: {entry.Value}");
    }
}
catch (AiException ex)
{
    Console.Error.WriteLine($"AI service error: {ex.Message}");
}
```

**为什么这很重要：** 该方法返回一个 `Dictionary<int, string>`，将每页（或图像索引）映射到其描述。处理 `AiException` 可让您捕获网络或配额错误，而不是让应用崩溃。

## 步骤 4：显示或存储描述

您可以将描述写入控制台、日志文件，或嵌入回 PDF 作为可访问性的 alt‑text。下面是一个快速示例，将输出写入 JSON 文件以供后续使用。

```csharp
using System.Text.Json;

// Serialize the map to JSON
var json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
File.WriteAllText(@"C:\Reports\ImageDescriptions.json", json);

Console.WriteLine("Image descriptions saved to ImageDescriptions.json");
```

**为什么这很重要：** 将输出保存为 JSON 可保留每页与其描述的关联，便于下游流程（搜索索引、UI 渲染等）使用这些数据。

## 处理每页多个图像

如果一页包含多个图像，副驾驶会返回用换行分隔的连贯描述。要拆分它们，请检查原始结果并在 `\n\n`（双换行）处拆分。以下是一个帮助方法：

```csharp
static IEnumerable<string> SplitDescriptions(string combined)
{
    return combined.Split(new[] { "\n\n" }, StringSplitOptions.RemoveEmptyEntries);
}
```

然后您可以遍历每个单独的图像描述，并在需要时分别存储它们。

## 边缘情况：大型 PDF 与超时管理

处理大于 100 MB 的 PDF 可能会超出默认 HTTP 超时。在创建 `AiClient` 时调整客户端的超时设置：

```csharp
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    Timeout = TimeSpan.FromMinutes(5)   // Increase timeout for heavy workloads
});
```

增加超时可防止在服务处理大量高分辨率图像时提前终止。

## 专业提示：缓存结果以降低成本

OpenAI 按 token 收费，且相同报告的不同版本的图像描述可能重复。缓存 JSON 输出，并在 PDF 哈希与已处理文件匹配时复用。这种做法可省钱并加快后续运行。

```csharp
static string ComputeFileHash(string path)
{
    using var sha256 = System.Security.Cryptography.SHA256.Create();
    using var stream = File.OpenRead(path);
    var hash = sha256.ComputeHash(stream);
    return Convert.ToHexString(hash);
}
```

将哈希与 JSON 文件一起存储；如果后续运行时哈希匹配，则跳过 AI 调用。

## 完整可运行示例

将所有内容整合在一起，下面是一个可自行粘贴到新 .NET 项目中的独立控制台应用程序。

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Text.Json;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

class Program
{
    static async Task Main()
    {
        // 1️⃣ Initialize AI client
        var client = new AiClient(new AiClientOptions
        {
            ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
            Timeout = TimeSpan.FromMinutes(5)
        });

        // 2️⃣ Configure OpenAI image options and create copilot
        var imageOptions = OpenAIImageDescriptionOptions.Create()
            .WithModel("gpt-4o-mini")
            .WithTemperature(0.7)
            .WithMaxTokens(150);

        string pdfPath = @"C:\Reports\AnnualReport.pdf";

        var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
            client,
            imageOptions.WithDocument(pdfPath));

        // 3️⃣ Retrieve descriptions
        Dictionary<int, string> descriptionMap;
        try
        {
            descriptionMap = await imgCopilot.GetDescriptionAsync();
        }
        catch (AiException ex)
        {
            Console.Error.WriteLine($"Error from AI service: {ex.Message}");
            return;
        }

        // 4️⃣ Output results
        foreach (var entry in descriptionMap)
        {
            Console.WriteLine($"Page {entry.Key}:");
            Console.WriteLine(entry.Value);
            Console.WriteLine(new string('-', 40));
        }

        // 5️⃣ Save to JSON for later use
        string json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
        string jsonPath = Path.ChangeExtension(pdfPath, ".descriptions.json");
        await File.WriteAllTextAsync(jsonPath, json);
        Console.WriteLine($"Descriptions saved to {jsonPath}");
    }
}
```

**预期输出（截断）**

```
Page 2:
A bar chart showing quarterly revenue growth, with blue bars representing Q1–Q4.
----------------------------------------
Page 5:
A high‑resolution photograph of the new manufacturing facility, showing the assembly line in operation.
...
Descriptions saved to C:\Reports\AnnualReport.descriptions.json
```

程序读取 `AnnualReport.pdf`，创建一个 **AI 副驾驶**，并写入一个将每页映射到生成描述的 JSON 文件。

## 常见问题

* **这能用于加密的 PDF 吗？**  
  可以，但在创建副驾驶时必须提供密码：  
  `imageOptions.WithPassword("mySecret")`。

* **我可以限制处理特定页面吗？**  
  使用 `imageOptions.WithPageRange(1, 10)` 将副驾驶限制在第 1‑10 页。

* **如果图像中包含文字怎么办？**  
  模型会尝试描述视觉内容；若需 OCR 风格的文字提取，应改用 `CreateTextExtractionCopilot`。

## 结论

您现在已经了解如何 **创建 AI 副驾驶**，为 PDF 文件 **生成图像描述**，配置 **OpenAI 图像选项**，以及在 C# 中以编程方式 **提取图像描述**。完整示例展示了异步处理、错误管理和结果缓存等最佳实践。

接下来，您可以探索：  
* 将生成的描述重新嵌入 PDF 作为 alt‑text，以提升可访问性（`PdfDocument` → `PdfImage.AlternativeText`）。  
* 使用相同的副驾驶模式为批量处理 **生成图像描述 PDF** 报告。  
* 试验不同的 OpenAI 模型或 temperature 设置，以微调描述风格。

欢迎自由地改写代码，尝试更大的文档，并将输出集成到您的索引流水线中。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术密切相关的主题，构建在本指南演示的技巧之上。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [在 Java 中创建带标签的 PDF 图像](/pdf/hindi/java/pdf-structure-elements/create-pdf-with-tagged-image-in-java/)
- [创建带标签的 PDF 图像](/pdf/hindi/net/programming-with-tagged-pdf/create-pdf-with-tagged-image/)
- [在 .NET 中创建带标签的 PDF 图像](/pdf/hindi/net/images-graphics/create-tagged-pdf-image-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}