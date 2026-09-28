---
category: general
date: 2026-09-28
description: 在 C# 中初始化 OpenAI 客戶端，使用 AI 摘要 PDF，提取簡潔摘要並將其轉換為 PDF 檔案。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- initialize openai client
- summarize pdf with ai
- extract summary from pdf
- convert summary to pdf
- create summary copilot
language: zh-hant
lastmod: 2026-09-28
og_description: 初始化 OpenAI 客戶端於 C#，以 AI 為 PDF 產生摘要，提取摘要後，使用 Aspose.Pdf.AI 轉換成 PDF。
og_image_alt: Code editor view showing how to initialize OpenAI client in C#
og_title: 初始化 OpenAI 客戶端 & 使用 AI 摘要 PDF – 逐步指南
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
title: 如何初始化 OpenAI 客戶端並以 AI 摘要 PDF
url: /zh-hant/net/document-creation/how-to-initialize-openai-client-and-summarize-pdf-with-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何初始化 OpenAI 客戶端並使用 AI 摘要 PDF

如果您需要在 .NET 專案中 **initialize OpenAI client** 並 **summarize PDF with AI**，本指南將提供完整、可執行的解決方案。您將學習如何設定客戶端、建立 summary copilot、從 PDF 中提取簡潔摘要，最後 **convert summary to PDF**——全部附有清晰的程式碼與說明。

本教學涵蓋從必要的 NuGet 套件到處理非同步呼叫的所有內容，讓您可以直接將最終程式碼複製貼上到自己的解決方案中，即時看到結果。

## 前置條件

* .NET 6.0 或更新版本已安裝  
* OpenAI API 金鑰（可從 OpenAI 入口網站取得）  
* **Aspose.Pdf.AI** NuGet 套件 – 使用以下指令安裝  

```bash
dotnet add package Aspose.Pdf.AI
```

不需要額外的外部服務；只要提供 API 金鑰，程式碼即可完全在本機執行。

## 步驟 1：Initialize OpenAI client

第一步是 **initialize OpenAI client**。此操作會建立可重複使用的 HTTP 客戶端，為您處理驗證與請求速率限制。

```csharp
using var openAiClient = Aspose.Pdf.AI.OpenAIClient
    .CreateWithApiKey(Environment.GetEnvironmentVariable("OPENAI_API_KEY"))
    .Build();
```

*Why this matters*：只初始化一次並重複使用客戶端可避免重複握手、降低延遲，且確保您的 API 金鑰永不硬編碼於原始碼控制中。

> **Pro tip**：將 API 金鑰儲存在環境變數或祕密管理器中。切勿將其提交至原始碼控制。

## 步驟 2：Configure summary copilot options

接下來，您需要告訴 AI 要摘要什麼以及如何摘要。options 物件允許您設定 temperature（控制隨機性）並指向來源 PDF。

```csharp
var summaryOptions = Aspose.Pdf.AI.OpenAISummaryCopilotOptions.Create()
    .WithTemperature(0.5)                     // Balanced creativity vs. factuality
    .WithDocument("YOUR_DIRECTORY/SampleDocument.pdf"); // Path to the PDF you want to summarize
```

*Why this matters*：調整 temperature 有助於在 **extract summary from PDF** 時取得確定性的摘要。0.5 的數值對大多數商業文件而言是良好的預設值。

## 步驟 3：Create summary copilot

現在，您透過將已初始化的客戶端與剛設定的 options 結合，**create summary copilot**。copilot 抽象化了低階的請求處理。

```csharp
var summaryCopilot = Aspose.Pdf.AI.AICopilotFactory
    .CreateSummaryCopilot(openAiClient, summaryOptions);
```

*Why this matters*：copilot 模式遵循單一職責原則——您的程式碼只處理高階操作，如 “GetSummaryAsync”，而不必自行組裝原始 HTTP 負載。

## 步驟 4：Generate the summary text asynchronously

呼叫 `GetSummaryAsync` 會將 PDF 傳送至 OpenAI，執行摘要模型，並回傳純文字摘要。

```csharp
string summaryText = await summaryCopilot.GetSummaryAsync();
Console.WriteLine("=== Extracted Summary ===");
Console.WriteLine(summaryText);
```

此時您已在字串變數中 **extracted summary from PDF**。典型的輸出如下：

```
=== Extracted Summary ===
This report outlines the quarterly revenue growth of 12% across all regions, highlights key product launches, and recommends strategic investments in cloud infrastructure.
```

## 步驟 5：Convert summary to PDF

最後一步是 **convert summary to PDF**，讓您能像其他文件一樣分享或保存。copilot 提供便利的 `SaveSummaryAsync` 方法。

```csharp
await summaryCopilot.SaveSummaryAsync("YOUR_DIRECTORY/Summary_out.pdf");
Console.WriteLine("Summary saved to Summary_out.pdf");
```

*Why this matters*：將摘要保存為 PDF 可保留格式，方便附加於電子郵件，且保持在您已使用的文件生態系統中。

## 完整範例程式

以下是一個完整的主控台應用程式，將所有步驟整合。執行前請將 `YOUR_DIRECTORY` 替換為實際路徑，並設定 `OPENAI_API_KEY` 環境變數。

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

### 預期輸出

```
=== Extracted Summary ===
[Your concise summary here]

Summary saved to Summary_out.pdf
```

在任何 PDF 檢視器中開啟 `Summary_out.pdf`——您會看到相同的文字，已被格式化為正式的 PDF 文件。

## 常見變化與邊緣情況

| 情境 | 如何調整程式碼 |
|-----------|----------------------|
| **Large PDFs (> 10 MB)** | 在 `summaryOptions` 加入 `.WithTimeout(TimeSpan.FromMinutes(5))` 以延長逾時時間。 |
| **Custom prompt** | 使用 `.WithPrompt("Provide a bullet‑point summary focusing on financial metrics.")`。 |
| **Multiple PDFs** | 迭代檔案路徑清單，為每個檔案建立新的 `summaryCopilot`，或以不同的 options 重複使用相同的客戶端。 |
| **Non‑English documents** | 設定 `.WithLanguage("es")` 以請求模型以西班牙語進行摘要。 |
| **Saving as other formats** | 在 `GetSummaryAsync` 之後，您可以使用任何 PDF 函式庫（例如 iTextSharp）來建立 PDF，但 `SaveSummaryAsync` 已處理最常見的情況。 |

## 生產環境使用技巧

* **Rate limiting** – OpenAI 會強制請求配額。於多次摘要時重複使用相同的 `openAiClient` 實例以維持在限制內。  
* **Error handling** – 將非同步呼叫包在 `try/catch` 區塊中，並檢查 `OpenAIException` 以辨識速率限制或驗證錯誤。  
* **Security** – 絕不要記錄原始 API 金鑰。使用安全的祕密儲存（如 Azure Key Vault、AWS Secrets Manager 等）。  
* **Testing** – 若需要不連線至實際 API 的單元測試，可使用假實作來 Mock `OpenAIClient`。  

## 結論

您現在已了解如何使用 Aspose.Pdf.AI 在 C# 中 **initialize OpenAI client**、**create summary copilot**、**extract summary from PDF**，以及 **convert summary to PDF**。完整範例可端對端執行，為任何文件摘要工作流程提供即用的解決方案。

接下來，您可以探索：

* **Summarize PDF with AI** 用於批次處理檔案庫  
* 為產生的 PDF 加入 **metadata**（作者、日期）  
* 將摘要步驟整合至更大的 **document‑management pipeline** 中  

歡迎嘗試不同的 temperature 值、自訂提示或多語言摘要，以符合您的特定領域需求。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上延伸。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索替代實作方式。

- [Extract & Convert PDF Regions to Images with Aspose.PDF](/pdf/english/net/images-graphics/extract-convert-pdf-regions-aspose-net/)
- [Extract Convert Pdf Regions Aspose Net](/pdf/german/net/images-graphics/extract-convert-pdf-regions-aspose-net/)
- [Extract Convert Pdf Regions Aspose Net](/pdf/french/net/images-graphics/extract-convert-pdf-regions-aspose-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}