---
category: general
date: 2026-03-22
description: 如何在 C# 中使用 Aspose.Pdf 對 PDF 檔案執行 OCR。學習將掃描的 PDF 轉換、使 PDF 可搜尋，並輕鬆載入 PDF
  文件。
draft: false
keywords:
- how to run OCR
- run OCR on pdf
- convert scanned pdf
- make pdf searchable
- load pdf document
language: zh-hant
og_description: 如何使用 Aspose.Pdf 在 PDF 檔案上執行 OCR。本教學示範如何將掃描的 PDF 轉換、使 PDF 可搜尋，並在 C#
  中載入 PDF 文件。
og_title: 如何在 PDF 上執行 OCR – 完整 C# 指南
tags:
- OCR
- Aspose.Pdf
- C#
- PDF processing
title: 使用 Aspose.Pdf 在 PDF 上執行 OCR – 完整 C# 指南
url: /zh-hant/net/advanced-features/how-to-run-ocr-on-pdf-with-aspose-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 PDF 上執行 OCR – 完整 C# 指南

在處理掃描文件時，如何在 PDF 檔案上執行 OCR 是常見的障礙。曾經嘗試在掃描的發票上搜尋卻找不到結果嗎？你並不孤單。在本教學中，我們將逐步說明如何使用 **Aspose.Pdf** **在 PDF 上執行 OCR**，把模糊的掃描檔轉換成完整可搜尋的文件。完成後，你也會知道如何 **轉換掃描 PDF**、**讓 PDF 可搜尋**，以及當然 **載入 PDF 文件** 物件而不會卡住。

我們會從專案設定講到驗證輸出，沒有手勢示意、沒有「請參考文件」的捷徑——只是一個完整、可直接貼到 Visual Studio 執行的範例。如果你在想這是否支援 .NET 6 或 .NET Framework 4.8，答案是肯定的；Aspose.Pdf 兩者皆支援，以下程式碼會自動適應。

## 前置條件

在開始之前，請確保你已具備：

- **Aspose.Pdf for .NET**（截至 2026 年 3 月的最新版本）。可從 NuGet 取得：`Install-Package Aspose.Pdf`。
- 一個 **要處理的掃描 PDF**（放在可參照的資料夾，例如 `YOUR_DIRECTORY/input.pdf`）。
- .NET 6 SDK 或更新版本（語法使用 `using var`，自 C# 8 起支援）。
- 任一你慣用的 IDE——Visual Studio、Rider 或 VS Code 都可。

就這樣。無需額外的 OCR 引擎或外部服務。Aspose 內建的 `OcrPlugin` 會負責所有繁重工作。

## 如何執行 OCR – 核心步驟

以下是完整、獨立的程式。存成 `Program.cs` 後執行；執行完畢後，主控台不會顯示任何訊息，且在輸入檔旁會產生一個可搜尋的 PDF。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Plugins;

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document you want to OCR
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Step 2: Create a PluginManager – this is the hub for all PDF plugins
        var pluginManager = new PluginManager();

        // Step 3: Register the built‑in OCR plugin (the one that actually reads the image)
        pluginManager.RegisterPlugin(new OcrPlugin());

        // Step 4: Prepare execution options – here we set English as the language.
        // You can add more languages by comma‑separating them, e.g., "eng,spa".
        var ocrOptions = new PluginExecutionOptions
        {
            Parameters = { ["Language"] = "eng" }
        };

        // Step 5: Execute the OCR plugin on the loaded document.
        // This mutates pdfDocument in‑place, turning each scanned page into searchable text.
        pluginManager.Execute(pdfDocument, ocrOptions);

        // Step 6: Save the OCR‑processed PDF to a new file.
        pdfDocument.Save("YOUR_DIRECTORY/ocr-output.pdf");

        Console.WriteLine("OCR complete! Output saved to ocr-output.pdf");
    }
}
```

### 程式碼逐步說明

1. **載入 PDF 文件** – `Document` 建構子會將檔案讀入記憶體。這滿足「載入 PDF 文件」的需求，並提供可變更的物件供後續操作。
2. **外掛管理員** – Aspose 透過管理員將可選功能（如 OCR）隔離。把它想成一個工具箱，讓你挑選合適的錘子。
3. **註冊 OCR 外掛** – 呼叫 `RegisterPlugin(new OcrPlugin())` 即告訴 Aspose 我們要執行光學字元辨識。
4. **執行選項** – `PluginExecutionOptions` 讓你微調處理流程。將 `Language` 設為 `"eng"` 代表引擎會尋找英文字符。你也可以加入 `"spa"`（西班牙文）或 `"deu"`（德文）。
5. **執行 OCR** – `pluginManager.Execute` 會逐頁擷取點陣圖、執行 OCR 引擎，並覆蓋一層隱形文字。這就是 **在 PDF 上執行 OCR** 的核心。
6. **儲存結果** – 最終的 PDF 內含隱藏文字層，使其 **讓 PDF 可搜尋**。在 Adobe Reader 中使用「搜尋」功能即可找到任何原本只是一張圖的文字。

## 步驟 1：載入 PDF 文件

你可能會好奇為什麼使用 `using var` 而不是直接 `new Document()`。`using` 陳述式可確保檔案句柄在使用完畢後立即釋放，這在之後想要在 Windows 上覆寫同一檔案時尤為重要。

```csharp
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

如果路徑錯誤，Aspose 會拋出 `FileNotFoundException`。請再次確認資料夾權限——特別是在 Linux 上，大小寫敏感可能會導致問題。

## 步驟 2：註冊與設定 OCR 外掛

OCR 外掛預設不會載入，以保持核心函式庫的輕量。註冊只需要一行程式碼，但若工作流程需要，你也可以串接多個外掛（例如去除浮水印的外掛）。

```csharp
var pluginManager = new PluginManager();
pluginManager.RegisterPlugin(new OcrPlugin());
```

> **專業提示：** 若你打算一次批次處理數百份 PDF，建議只建立一次 `PluginManager` 並重複使用。每個檔案都重新建立會產生不必要的開銷。

## 步驟 3：執行 OCR 流程（轉換掃描 PDF）

接下來就是重點。`Execute` 方法會掃描每一頁、執行 OCR，並把文字寫回 PDF。它相當高效——Aspose 會串流圖像資料，即使是 200 頁的掃描檔也不會耗盡記憶體。

```csharp
var ocrOptions = new PluginExecutionOptions
{
    Parameters = { ["Language"] = "eng" }
};

pluginManager.Execute(pdfDocument, ocrOptions);
```

**為什麼要設定語言？** OCR 的準確度高度依賴語言模型。提供 `"eng"` 讓引擎優先辨識英文字符，降低誤判的機率。

## 步驟 4：儲存並驗證可搜尋的 PDF

儲存相當直接，但驗證卻是許多開發者卡關的地方。執行完畢後，用任意 PDF 閱讀器開啟輸出檔，使用 **Ctrl + F** 快捷鍵搜尋。若能找到原本只是一張圖的文字，即代表已成功 **讓 PDF 可搜尋**。

```csharp
pdfDocument.Save("YOUR_DIRECTORY/ocr-output.pdf");
```

![執行 OCR 後的可搜尋 PDF](/images/ocr-searchable.png "執行 OCR 後產生的可搜尋 PDF")

*上圖顯示在搜尋關鍵字時，隱藏的文字層被高亮顯示。*

## 常見問題與專業技巧

| 問題 | 為何會發生 | 解決方式 |
|------|------------|----------|
| **輸出空白** | 未設定語言參數或使用了不支援的代碼。 | 確認 `["Language"] = "eng"`（或其他 ISO‑639‑2 代碼）。 |
| **處理緩慢** | 大圖未降解析度。 | 在 `Parameters` 中加入 `["Resolution"] = "300"`，讓 OCR 以較低 DPI 處理。 |
| **缺少字型** | OCR 產生文字但檢視器無法渲染字型。 | 設定 `pdfDocument.FontEmbeddingMode = FontEmbeddingMode.Always` 以嵌入字型。 |
| **記憶體洩漏** | 未釋放 `Document` 物件。 | 如範例使用 `using var`，或手動呼叫 `pdfDocument.Dispose()`。 |

### 邊緣案例

- **多語言 PDF**：傳入逗號分隔的清單，例如 `"eng,spa,fra"`，即可同時辨識多種語言。
- **受密碼保護的檔案**：使用 `new Document("file.pdf", new LoadOptions { Password = "secret" })` 載入。
- **選擇性 OCR**：若只需 OCR 特定頁面，可建立 `PageRange` 物件，並以 `Parameters["Pages"] = "1-3,5"` 傳入。

## 重點回顧

- 使用 Aspose.Pdf 內建外掛 **在 PDF 上執行 OCR**。
- **轉換掃描 PDF** 為可搜尋版本，無需外部服務。
- **讓 PDF 可搜尋**，讓最終使用者即時找到文字。
- **安全載入 PDF 文件**，並即時釋放資源。

全部只需不到 30 行乾淨的 C# 程式碼。

## 接下來可以嘗試的方向

- 嘗試不同語言，對多語言合約進行 OCR。
- 結合 OCR 與 **文字抽取**（`pdfDocument.Pages[i].ExtractText()`）以自動化資料輸入。
- 在 OCR 前使用 **Redaction 外掛** 清除敏感資訊，確保合規。
- 將程式碼部署為微服務，提供 API 端點，讓非開發者上傳掃描檔並即時取得可搜尋的 PDF。

對於在雲端擴展或與 Azure Functions 整合有任何疑問嗎？歡迎留言，我們一起探討。祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}