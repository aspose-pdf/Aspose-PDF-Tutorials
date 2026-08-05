---
category: general
date: 2026-08-04
description: 建立 AI 副駕駛，為 PDF 檔案產生圖像說明。學習如何設定 OpenAI 圖像選項，並有效提取圖像說明。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create AI copilot
- generate image description
- image description PDF
- OpenAI image options
- extract image description
language: zh-hant
lastmod: 2026-08-04
og_description: 建立 AI 副駕駛以產生 PDF 檔案的圖像描述。本教學示範如何設定 OpenAI 圖像選項、執行副駕駛，以及在 C# 中擷取圖像描述。
og_image_alt: Screenshot of C# code that creates an AI copilot for PDF image description
og_title: 打造 AI 副駕駛，為 PDF 圖片說明 – 完整指南
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
title: 為 PDF 圖片說明打造 AI 副駕駛 – 步驟指南
url: /zh-hant/net/programming-with-images/create-ai-copilot-for-pdf-image-description-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 AI Copilot 以產生 PDF 圖片說明 – 完整指南

如果您需要 **create AI Copilot**（建立 AI Copilot）自動為 PDF 中嵌入的圖片撰寫說明，本指南將一步步示範如何操作。您將學會設定 OpenAI image options、執行 copilot，並在不離開 C# 專案的情況下 **extract image description**（擷取圖片說明）。

產生 PDF 圖片的文字內容是為了可及性、內容索引與自動化報告等常見需求。完成本教學後，您將擁有一個可重複使用的元件，能夠 **generates image description**（產生圖片說明）給任意指定的 PDF 文件。

## 前置條件

* .NET 6.0 或更新版本已安裝  
* Aspose.Pdf.AI 授權（或免費試用）  
* 可供 Aspose 用戶端使用的 OpenAI API 金鑰  
* Visual Studio 2022（或任何支援 C# 的 IDE）  

除了 `Aspose.Pdf.AI` 之外，無需其他 NuGet 套件。

## 步驟 1：設定 Aspose.Pdf.AI 用戶端

第一步是以您的驗證資訊建立 AI 用戶端實例。此用戶端會在背後處理與 OpenAI 服務的通訊。

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

**Why this matters:** `AiClient` 封裝了所有請求層級的設定（API key、逾時、重試策略）。只建立一次並在多個 copilot 實例間重複使用，可減少開銷並確保驗證一致性。

## 步驟 2：建立 Image Description Copilot

現在您要建立 **AI copilot**，它會讀取 PDF 並為每張圖片產生說明。`CreateImageDescriptionCopilot` 工廠方法接受用戶端以及一組定義說明產生方式的選項。

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

**Why this matters:**  
* `OpenAIImageDescriptionOptions`（即 **OpenAI image options**）讓您微調語言模型。調整 temperature 或模型可提升對技術圖表與自然照片的相關性。  
* 指定文件路徑讓 copilot 知道要掃描哪一份 PDF。copilot 會擷取所有點陣圖，送至模型，並回傳可供人閱讀的說明。

## 步驟 3：非同步取得產生的說明

copilot 以非同步方式運作，因為可能需要上傳數 MB 的圖片資料並等待模型回應。請使用 `await` 確保呼叫完成後再存取結果。

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

**Why this matters:** 此方法回傳 `Dictionary<int, string>`，將每頁（或圖片索引）對應到其說明。處理 `AiException` 可讓您捕捉網路或配額錯誤，避免程式崩潰。

## 步驟 4：顯示或儲存說明

您可以將說明寫入主控台、日誌檔，或重新嵌入 PDF 作為 alt‑text 以提升可及性。以下是一個快速範例，將輸出寫入 JSON 檔供之後使用。

```csharp
using System.Text.Json;

// Serialize the map to JSON
var json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
File.WriteAllText(@"C:\Reports\ImageDescriptions.json", json);

Console.WriteLine("Image descriptions saved to ImageDescriptions.json");
```

**Why this matters:** 以 JSON 儲存輸出可保留每頁與其說明的對應關係，讓後續流程（搜尋索引、UI 呈現等）輕鬆取用資料。

## 處理每頁多張圖片

若頁面包含多張圖片，copilot 會回傳以換行分隔的合併說明。要分割它們，可檢查原始結果並以 `\n\n`（雙換行）作為分割依據。以下是一個輔助方法：

```csharp
static IEnumerable<string> SplitDescriptions(string combined)
{
    return combined.Split(new[] { "\n\n" }, StringSplitOptions.RemoveEmptyEntries);
}
```

之後您即可遍歷每個單獨的圖片說明，並視需要分別儲存。

## 邊緣情況：大型 PDF 與逾時管理

處理大於 100 MB 的 PDF 可能會超過預設 HTTP 逾時。建立 `AiClient` 時請調整用戶端的逾時設定：

```csharp
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    Timeout = TimeSpan.FromMinutes(5)   // Increase timeout for heavy workloads
});
```

延長逾時時間可避免服務在處理大量高解析度圖片時過早終止。

## 專業提示：快取結果以降低成本

OpenAI 依 token 收費，且相同報告的不同版本可能產生重複的圖片說明。快取 JSON 輸出，當 PDF 的雜湊值與先前處理過的檔案相符時直接重用。此做法可節省成本並加快後續執行。

```csharp
static string ComputeFileHash(string path)
{
    using var sha256 = System.Security.Cryptography.SHA256.Create();
    using var stream = File.OpenRead(path);
    var hash = sha256.ComputeHash(stream);
    return Convert.ToHexString(hash);
}
```

將雜湊值與 JSON 檔一起儲存；若稍後執行時雜湊相符，即可跳過 AI 呼叫。

## 完整可執行範例

將上述所有步驟整合，以下是一個可直接貼入新 .NET 專案的完整主控台應用程式。

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

**預期輸出（截斷）**

```
Page 2:
A bar chart showing quarterly revenue growth, with blue bars representing Q1–Q4.
----------------------------------------
Page 5:
A high‑resolution photograph of the new manufacturing facility, showing the assembly line in operation.
...
Descriptions saved to C:\Reports\AnnualReport.descriptions.json
```

程式會讀取 `AnnualReport.pdf`，建立 **AI copilot**，並寫入一個 JSON 檔，將每頁對應到產生的說明。

## 常見問題

* **這能用於加密的 PDF 嗎？**  
  是的，但在建立 copilot 時必須提供密碼：  
  `imageOptions.WithPassword("mySecret")`。

* **我可以限制只處理特定頁面嗎？**  
  使用 `imageOptions.WithPageRange(1, 10)` 可將 copilot 限制在第 1‑10 頁。

* **如果圖片中包含文字該怎麼辦？**  
  模型會嘗試描述視覺內容；若需 OCR 文字擷取，請改用 `CreateTextExtractionCopilot`。

## 結論

現在您已了解如何 **create AI Copilot**，為 PDF 檔案 **generates image description**，設定 **OpenAI image options**，以及在 C# 中以程式方式 **extract image description**。完整範例展示了非同步處理、錯誤管理與結果快取等最佳實踐。

接下來您可以探索：

* 將產生的說明重新嵌入 PDF 作為 alt‑text，以提升可及性（`PdfDocument` → `PdfImage.AlternativeText`）。  
* 使用相同的 copilot 模式，為批次處理產生 **generate image description PDF** 報告。  
* 嘗試不同的 OpenAI 模型或 temperature 設定，以微調說明風格。

歡迎自行調整程式碼、測試更大的文件，並將輸出整合至您的索引流程。祝開發順利！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索其他實作方式。

- [在 Java 中建立帶標記圖片的 PDF](/pdf/hindi/java/pdf-structure-elements/create-pdf-with-tagged-image-in-java/)
- [建立帶標記圖片的 PDF](/pdf/hindi/net/programming-with-tagged-pdf/create-pdf-with-tagged-image/)
- [在 .NET 中建立帶標記的 PDF 圖片](/pdf/hindi/net/images-graphics/create-tagged-pdf-image-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}