---
category: general
date: 2026-10-10
description: 在 C# 中建立 OpenAI 客戶端，學習如何對 PDF 進行摘要、將 PDF 轉換為摘要，並使用 Aspose.Pdf.AI 保存生成的
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
language: zh-hant
lastmod: 2026-10-10
og_description: 在 C# 中建立 OpenAI 客戶端，即時學習如何摘要 PDF、將 PDF 轉換為摘要，並儲存產生的 PDF 摘要。
og_image_alt: Screenshot of C# code that creates an OpenAI client and generates a
  PDF summary
og_title: 在 C# 中建立 OpenAI 客戶端並產生 PDF 摘要 – 逐步指南
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
title: 如何在 C# 中建立 OpenAI 客戶端並產生 PDF 摘要
url: /zh-hant/net/document-creation/how-to-create-openai-client-and-generate-a-pdf-summary-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中建立 OpenAI 客戶端並產生 PDF 摘要

如果您需要在 .NET 應用程式中 **create OpenAI client**，本教學將完整示範如何操作，以及如何將任何 PDF 轉換為簡潔的 AI 生成摘要。您將看到如何 **convert PDF to summary**、取得文字，並 **save the summary** 為新的 PDF 檔案——全部使用 Aspose.Pdf.AI。

對於文件密集的工作流程（如法律審查、研究彙整或自動化報告產生），PDF 摘要是一項常見需求。完成本指南後，您將能以程式方式 **generate PDF summary**，無需離開 C# 程式碼庫。

## 您需要的環境

- .NET 6.0 或更新版本（範例以 .NET 6 為目標，但任何較新的 .NET 版本皆可）
- Aspose.Pdf.AI NuGet 套件 (`Aspose.Pdf.AI`) – 此封裝簡化了對 PDF 內容的 OpenAI 呼叫
- 有效的 OpenAI API 金鑰（可從 OpenAI 入口網站取得）
- 您想要摘要的範例 PDF 檔案（例如 `SampleDocument.pdf`）
- Visual Studio 2022、VS Code，或任何支援 C# 開發的 IDE

> **專業提示：** 請將 API 金鑰存放於安全位置，例如 [user‑secrets](https://learn.microsoft.com/en-us/aspnet/core/security/app-secrets) 或 Azure Key Vault。切勿在原始碼控制中硬編碼。

## 步驟 1：安裝 Aspose.Pdf.AI NuGet 套件

在專案資料夾中開啟終端機並執行：

```bash
dotnet add package Aspose.Pdf.AI
```

此套件會引入必要的 HTTP 客戶端、PDF 操作工具，以及 OpenAI API 的輕量封裝。安裝完成後，還原專案以確保所有相依性皆已就緒：

```bash
dotnet restore
```

## 步驟 2：**Create OpenAI client** 並使用您的 API 金鑰

建立客戶端是任何 AI 驅動 PDF 操作的第一步。`OpenAIClient` 會為您處理驗證、請求速率限制與連線池管理。

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

**為什麼重要：** `using` 陳述式確保客戶端能正確釋放，釋放網路資源，避免長時間服務中出現 socket 耗盡的情況。

## 步驟 3：設定摘要選項 – **convert PDF to summary**

`OpenAISummaryCopilotOptions` 物件告訴 AI 要執行的操作。您可以調整 temperature、限制 token 使用量，且最重要的是指向來源 PDF。

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

### 為什麼使用 temperature 0.5？

temperature 為 0.5 時，可產生簡潔且精確的語句，同時仍允許模型重新表述句子。較高的值（例如 0.9）會使輸出更具創意，但可能偏離原意——這在法律或技術摘要中是不理想的。

## 步驟 4：**How to summarize PDF** – 建立 copilot 並取得文字

現在客戶端與選項已備妥，建立一個 summary copilot。此物件負責協調對 OpenAI 的請求，並以多種格式回傳結果。

```csharp
    // ---- Step 4: instantiate the summary copilot (how to summarize PDF) ----
    var summaryCopilot = AICopilotFactory
        .CreateSummaryCopilot(client, summaryOptions);

    // Retrieve the generated summary as plain text
    string summaryText = await summaryCopilot.GetSummaryAsync();

    Console.WriteLine("=== Text Summary ===");
    Console.WriteLine(summaryText);
```

`GetSummaryAsync` 方法會回傳乾淨的純文字版本，您可以將其嵌入 UI、透過電子郵件傳送，或儲存至資料庫。

## 步驟 5：以 PDF 文件取得摘要

若需要可攜帶、可列印的版本，可向 copilot 索取 PDF 文件。此步驟示範如何直接從 AI 模型 **generate PDF summary**。

```csharp
    // ---- Step 5: retrieve the summary as a PDF document (generate PDF summary) ----
    Document summaryDocument = await summaryCopilot.GetSummaryDocumentAsync();

    // Optionally, you can add a cover page or watermark here before saving.
```

回傳的 `Aspose.Pdf.Document` 行為與 Aspose 生態系統中的其他 PDF 物件相同，您可以進一步編輯頁面、加入中繼資料，或與其他 PDF 合併。

## 步驟 6：**How to save summary** – 將 PDF 持久化至磁碟

最後，將產生的摘要儲存於檔案系統。`SaveSummaryAsync` 輔助方法會在一次呼叫中完成取得與儲存，但我們也會示範明確的儲存方式以完整說明。

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

**提示：** 若需遵循命名規則（例如時間戳記檔案），可使用 `DateTime.UtcNow:yyyyMMdd_HHmmss` 程式化建立路徑。

### 完整可執行範例

將所有步驟整合起來，以下是一個可自行複製貼上至 `Program.cs` 並執行的完整程式：

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

執行程式會產生兩個產物：

1. **Console output** – 在螢幕上顯示的純文字摘要。
2. **`Summary_out.pdf`** – 可下載的 PDF，內含相同的摘要，隨時可供分發。

## 常見變化與邊緣情況

| 情境 | 建議調整 |
|-----------|-------------------|
| **大型 PDF（> 10 MB）** | 將文件拆分為較小的區塊（例如每章），分別摘要每個區塊。使用 `Document.AppendDocument` 合併結果。 |
| **需要自訂提示詞** | 在呼叫 `CreateSummaryCopilot` 前使用 `WithPrompt("Summarize the following legal contract in bullet points:")`。 |
| **非英文來源 PDF** | 設定 `WithLanguage("es")`（或相應的 ISO 代碼）以指導模型的語言處理。 |
| **速率限制錯誤** | 增加 `WithRetryCount` 或在呼叫之間加入 `Task.Delay`。 |
| **儲存至雲端儲存** | 將檔案系統路徑改為串流（`MemoryStream`），並上傳至 Azure Blob Storage 或 AWS S3。 |

## 驗證結果

程式執行完畢後，使用任何 PDF 檢視器開啟 `Summary_out.pdf`。您應該會看到一份乾淨的單頁（或多頁，視長度而定）文件，概括 `SampleDocument.pdf` 的主要概念。將在主控台列印的文字摘要與 PDF 版本比較——兩者應完全相同。

若摘要顯示不完整：

1. 將 `WithTemperature` 降至 0.2，以獲得更確定的輸出。
2. 增加

## 接下來您可以學習什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上延伸。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [如何在 C# 中建立 PDF – 新增頁面、繪製矩形與儲存](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [學習如何使用 Aspose.PDF for .NET 產生 PDF 文件](/pdf/english/net/document-creation/)
- [如何使用 Aspose.PDF for .NET 建立標記 PDF – 增強可及性](/pdf/english/net/bookmarks-navigation/tagged-pdf-creation-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}