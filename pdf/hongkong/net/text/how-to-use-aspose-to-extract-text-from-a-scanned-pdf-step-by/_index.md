---
category: general
date: 2026-08-04
description: 如何使用 Aspose 以 C# 提取掃描 PDF 文字並將 PDF 轉換為文字。學習讀取掃描 PDF 檔案，獲得可靠的 OCR 結果。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use aspose
- extract scanned pdf text
- convert pdf to text
- read scanned pdf
- how to extract text
language: zh-hant
lastmod: 2026-08-04
og_description: 如何使用 Aspose 讀取掃描的 PDF 檔案、提取掃描 PDF 文字，並以完整可執行的範例將 PDF 轉換為文字。
og_image_alt: Screenshot showing how to use Aspose OCR copilot to extract text from
  a scanned PDF
og_title: 如何使用 Aspose – 在 C# 中從掃描的 PDF 提取文字
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
title: 如何使用 Aspose 從掃描的 PDF 中提取文字 – 逐步指南
url: /zh-hant/net/text/how-to-use-aspose-to-extract-text-from-a-scanned-pdf-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose 從掃描的 PDF 中提取文字 – 步驟指南

如果你需要 **how to use Aspose** 進行 OCR，本指南會示範如何僅用幾行 C# 程式碼提取掃描 PDF 的文字。無論你是構建文件歸檔服務，或是為舊有文件建立搜尋索引，這個解決方案都能處理你送至 Aspose.Pdf.AI 服務的任何掃描 PDF。

在本教學中，你將會：

* 建立一個能讀取掃描 PDF 的 OCR copilot。
* 非同步提取辨識出的文字。
* 顯示或進一步處理提取的字串。

唯一的前置條件是擁有有效的 Aspose.Pdf.AI 訂閱，以及 .NET 6（或更新）開發環境。

## 先決條件

| 需求 | 重要原因 |
|-------------|----------------|
| .NET 6 SDK or newer | 提供 `async Main` 以及現代語言功能。 |
| Aspose.Pdf.AI NuGet package (`Aspose.Pdf.AI`) | 包含 `AICopilotFactory` 與 OCR 選項。 |
| A valid Aspose.Pdf.AI `client` instance (API key) | 驗證你對雲端服務的請求。 |
| A scanned PDF file (e.g., `Scanned.pdf`) | 將從中提取文字的來源文件。 |

使用 .NET CLI 安裝套件：

```bash
dotnet add package Aspose.Pdf.AI
```

## 步驟 1：設定 Aspose.Pdf.AI 用戶端

在呼叫任何 OCR 端點之前，你必須建立一個保存 API 憑證的用戶端。此用戶端是執行緒安全的，且可在多個文件間重複使用。

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

**Why this step is required** – Aspose 服務會根據你的訂閱驗證每個請求。只建立一次用戶端即可避免重複的網路握手，並保持程式碼整潔。

## 步驟 2：為掃描的 PDF 文件建立 OCR copilot

`AICopilotFactory` 會建構一個專門的 OCR copilot，能處理你指定的檔案。你需要傳入 `client` 與指向 PDF 路徑的 `OpenAIOcrOptions` 物件。

```csharp
using Aspose.Pdf.AI;

// Step 2: Build the OCR copilot
var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
    client,                                   // Your Aspose.Pdf.AI client instance
    OpenAIOcrOptions.Create()
        .WithDocument("YOUR_DIRECTORY/Scanned.pdf") // Path to the scanned PDF
);
```

**Explanation** – `CreateOcrCopilot` 封裝所有低階 HTTP 呼叫。`WithDocument` 方法告訴服務要分析哪個檔案；如果 PDF 位於記憶體中，也可以提供 `Stream`。

## 步驟 3：非同步提取辨識文字

呼叫 `GetTextAsync` 會在雲端執行 OCR 作業，並回傳純文字結果。因為作業可能需要數秒，故此方法為非同步。

```csharp
// Step 3: Perform OCR and get the text
string ocrText = await ocrCopilot.GetTextAsync();
```

**Why asynchronous?** – 網路延遲與 OCR 處理時間皆難以預測。使用 `await` 可防止應用程式阻塞主執行緒，這在 UI 或 Web 服務情境中特別重要。

## 步驟 4：使用提取的文字

此時你已取得一個普通的 .NET `string`，內含掃描 PDF 的完整文字稿。你可以將它寫入主控台、存入資料庫，或送入搜尋引擎。

```csharp
// Step 4: Display the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrText);
```

### 預期輸出

如果 `Scanned.pdf` 只包含一頁，內容為「Hello, world!」，主控台會顯示：

```
=== OCR Result ===
Hello, world!
```

對於多頁文件，輸出會將每頁文字串接起來，並保留換行。

## 完整、可執行範例

以下是一個完整程式，你可以貼到新建的主控台專案（`dotnet new console`）中。它示範了 **how to use Aspose** 從頭到尾的流程，並包含常見問題的錯誤處理。

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

**Key points in the example**

* `await` 確保非阻塞執行。
* `try/catch` 區塊會顯示網路或服務錯誤，這在大規模 **reading scanned PDF** 檔案時至關重要。
* 在執行前，請將 `YOUR_API_KEY` 與 `YOUR_DIRECTORY/Scanned.pdf` 替換為真實的值。

## 處理邊緣情況與最佳實踐提示

| 情況 | 建議做法 |
|-----------|----------------------|
| **Large PDFs ( > 50 MB )** | 在客戶端將文件切割成較小的區塊，並使用獨立的 copilot 處理每個區塊。可減少記憶體壓力並提升可靠性。 |
| **Low‑quality scans** | 於 `OpenAIOcrOptions` 加入 `.WithLanguage("eng")` 或 `.WithEnhanceImage(true)` 以調整 OCR 品質。服務支援語言提示，可提升準確度。 |
| **Multiple languages** | 提供逗號分隔的語言清單，例如 `.WithLanguage("eng,spa")`。OCR 引擎會偵測並轉錄多種語言。 |
| **Non‑PDF image files** | 先將影像轉為 PDF（使用 `Aspose.Pdf` 函式庫），或直接使用 `OpenAIOcrOptions.WithImage` 送出影像。 |
| **Rate‑limit exceeded** | 實作指數退避與重試機制；當超過配額時，Aspose API 會回傳 HTTP 429。 |

### 專業提示

若計畫之後再次使用，可將 `ocrText` 結果快取。OCR 作業是工作流程中最耗費資源的步驟，重複使用字串可避免重複呼叫 API，節省點數。

## 常見問題

**Q: 這能處理受密碼保護的 PDF 嗎？**  
A: 可以。於建立 copilot 前，於選項建構器加入 `.WithPassword("yourPassword")`。

**Q: 我能以結構化格式（例如含頁碼的 JSON）提取文字嗎？**  
A: 使用 `GetTextStructureAsync()` 取代 `GetTextAsync()`。此方法會回傳包含頁索引、邊界框與信心分數的 JSON 資料。

**Q: 若 PDF 含有表格該怎麼辦？**  
A: 純文字提取會將表格展平成以換行分隔的列。若需更豐富的資料，可呼叫 PDF 轉 HTML 轉換（`GetHtmlAsync`），再解析 HTML 表格元素。

## 結論

你現在已瞭解 **how to use Aspose** 讀取掃描 PDF、提取掃描 PDF 文字，並以最小的 C# 程式 **convert PDF to text**。整個流程包括建立 OCR copilot、呼叫 `GetTextAsync`，以及處理回傳的字串。遵循上述邊緣情況的建議，即可將解決方案擴展至大量文件、多語言內容與受保護的 PDF。

接下來，你可以探索：

* **How to extract text** with layout preservation (`GetHtmlAsync`)。
* 使用 Aspose.Pdf.AI **extract tables** 並匯出為 CSV。
* 將 OCR 輸出與 Azure Cognitive Search 整合，打造可搜尋的文件檔案庫。

祝編程愉快，盡情體驗 Aspose AI 驅動 OCR 為你的掃描 PDF 工作流程帶來的高精準度！

## 接下來該學什麼？

以下教學與本指南的技巧密切相關，並提供完整可執行的程式碼範例與步驟說明，協助你掌握更多 API 功能，或在自己的專案中探索其他實作方式。

- [使用 Aspose.PDF for .NET 從 PDF 檔案提取文字](/pdf/english/net/text-operations/extract-text-pdf-aspose-dotnet/)
- [如何使用 Aspose.PDF for .NET 從 PDF 的特定區域提取文字](/pdf/english/net/text-operations/extract-text-specific-region-aspose-pdf-net/)
- [如何使用 Aspose.PDF for .NET 從 PDF 中提取已標註的文字](/pdf/english/net/text-operations/extract-highlighted-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}