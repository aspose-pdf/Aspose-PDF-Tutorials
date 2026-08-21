---
category: general
date: 2026-02-10
description: 學習如何使用 Aspose.Pdf 在 C# 中編輯 PDF 透明度並儲存已修改的 PDF 檔案。附上完整程式碼範例。
draft: false
keywords:
- edit pdf transparency
- save modified pdf
language: zh-hant
og_description: 使用 Aspose.Pdf 編輯 PDF 透明度並儲存已修改的 PDF。完整、可執行的 C# 程式碼以及實用的開發者技巧。
og_title: 在 C# 中編輯 PDF 透明度 – 完整指南
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: 在 C# 中編輯 PDF 透明度 – 步驟指南
url: /zh-hant/net/advanced-features/edit-pdf-transparency-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 編輯 PDF 透明度 – 完整 C# 教程

是否曾需要 **編輯 PDF 透明度**，卻不知從何開始？你並非唯一面臨此問題的開發者——許多開發者在嘗試讓 PDF 的部分內容半透明而不重新寫整個檔案時卡住了。好消息是？使用 Aspose.Pdf，你可以直接在資源字典中調整不透明度和混合模式，然後只需幾行程式碼即可 **儲存已修改的 PDF** 檔案。

在本教學中，我們將逐步說明如何在頁面上變更描邊與填充的不透明度，解釋每個操作的意義，並示範如何將變更永久保存。完成後，你將擁有一段可直接放入任何 .NET 專案的即用程式碼片段。沒有模糊的說明，只有具體、可直接複製貼上的程式碼。

## 前置條件

在深入之前，請確保你已具備：

- .NET 6（或任何較新的 .NET 執行環境）已安裝。
- 已在專案中加入 Aspose.Pdf for .NET NuGet 套件（`Aspose.Pdf`）。
- 將 PDF 檔案（`input.pdf`）放置於可參考的資料夾中（將 `YOUR_DIRECTORY` 替換為實際路徑）。

就這樣——不需要額外的函式庫，也不需要奇怪的設定。

## 步驟 1 – 載入 PDF 文件

首先，我們打開現有的 PDF。Aspose.Pdf 的 `Document` 類別代表整個檔案，使用 `using` 陳述式可確保檔案句柄即時釋放。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.DataEditor;

// Load the PDF you want to edit
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*為什麼這很重要*：載入文件讓我們能存取其內部結構，包括存放透明度設定的頁面資源。使用 `using var` 是現代 C# 的寫法，可自動釋放物件，讓應用程式保持整潔。

## 步驟 2 – 取得第一頁及其資源

PDF 的頁碼是從 1 開始計算，因此 `Pages[1]` 會回傳第一頁。接著，我們使用 `DictionaryEditor` 包裝其 `Resources` 字典，以便更容易編輯。

```csharp
// Get a reference to the first page (pages are 1‑based)
var firstPage = pdfDocument.Pages[1];

// Access the page's resource dictionary
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*小技巧*：如果需要編輯其他頁面，只要更改索引 (`Pages[2]`, `Pages[3]`, …)。其餘邏輯保持不變。

## 步驟 3 – 定位（或建立）ExtGState 子字典

`ExtGState` 條目保存圖形狀態物件，其中包括不透明度 (`CA` / `ca`) 和混合模式 (`BM`)。如果字典不存在，當我們新增條目時，Aspose 會為我們自動建立它。

```csharp
// Retrieve the ExtGState dictionary; create if missing
var extGStateDict = resourcesEditor["ExtGState"]
    .ToCosPdfDictionary(); // throws if missing, so ensure it exists
```

*發生了什麼*：`ExtGState` 是 PDF 用來儲存可重複使用圖形狀態的地方。透過新增條目 (`GS0`)，之後即可在任何內容串流中引用它。

## 步驟 4 – 建立具有所需透明度的新圖形狀態

現在我們定義實際的透明度數值：

- **CA** – 描邊不透明度 (1 = 完全不透明)。
- **ca** – 填充不透明度 (0.5 = 50 % 透明)。
- **BM** – 混合模式 (通常為 `"Normal"`)。

```csharp
// Create a fresh graphics state dictionary
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define stroke opacity (CA), fill opacity (ca), and blend mode (BM)
newGraphicsState.Add("CA", new CosPdfNumber(1));          // stroke opacity
newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // fill opacity (50% transparent)
newGraphicsState.Add("BM", new CosPdfName("Normal"));    // blend mode
```

*為什麼使用這些鍵*：PDF 區分描邊 (`CA`) 與填充 (`ca`)，因為你可能想要實線輪廓搭配半透明的內部。混合模式決定物件與底層內容的混合方式；`"Normal"` 是最安全的預設值。

## 步驟 5 – 註冊圖形狀態並引用它

我們將新狀態以唯一名稱 (`GS0`) 加入 `ExtGState` 字典。之後你可以將它套用到特定的繪圖指令，但僅僅加入它對於許多 PDF 已經引用該狀態的使用情境已足夠。

```csharp
// Register the new graphics state in the ExtGState dictionary
extGStateDict.Add("GS0", newGraphicsState);
```

*特殊情況*：如果 `GS0` 已存在，建議產生唯一的鍵名（`GS1`、`GS2`、…）以避免覆寫既有設定。

## 步驟 6 – 儲存已修改的 PDF

最後，將變更後的文件寫入新檔案。此步驟 **儲存已修改的 PDF**，同時保留原始檔不受影響。

```csharp
// Persist the changes to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*結果*：`output.pdf` 現在包含一個圖形狀態，使任何填充物件的透明度為 50 %（描邊仍保持完全不透明）。使用 Adobe Acrobat 或任何檢視器開啟以驗證效果。

## 完整範例程式

將所有步驟整合起來，以下是完整、可直接執行的程式：

```csharp
using Aspose.Pdf;
using Aspose.Pdf.DataEditor;

using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// 1️⃣ Get first page and its resources
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);

// 2️⃣ Access (or create) ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"]
    .ToCosPdfDictionary();

// 3️⃣ Define a new graphics state with transparency
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
newGraphicsState.Add("CA", new CosPdfNumber(1));          // stroke opacity
newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // fill opacity (50% transparent)
newGraphicsState.Add("BM", new CosPdfName("Normal"));    // blend mode

// 4️⃣ Register it as GS0
extGStateDict.Add("GS0", newGraphicsState);

// 5️⃣ Save the result
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

> **預期結果** – 當你開啟 `output.pdf` 時，任何使用新加入圖形狀態的圖形都會呈現半透明的填充，而輪廓保持完整可見。如果沒有看到變化，請再次確認該頁面的內容確實引用了 `GS0`；否則你可以手動在內容串流中插入 `/GS0 gs` 運算子。

## 常見問題 (FAQs)

| Question | Answer |
|----------|--------|
| **我可以只對特定物件變更不透明度嗎？** | 可以。建立 `GS0` 後，編輯該頁面的內容串流（例如 `firstPage.Contents[1]`），並在想要影響的繪圖運算子前加上 `/GS0 gs` 前置。 |
| **如果 PDF 已經有 ExtGState 條目怎麼辦？** | 加入新的鍵名（`GS1`、`GS2`、…）以避免衝突。上面的程式碼為簡化起見使用 `GS0`。 |
| **這在加密的 PDF 上也能使用嗎？** | 載入時必須提供密碼，例如 `new Document("file.pdf", new LoadOptions { Password = "secret" })`。其餘步驟保持不變。 |
| **只有 “Normal” 這種混合模式嗎？** | 不是。PDF 支援 `"Multiply"`、`"Screen"`、`"Overlay"` 等等。只要在 `BM` 條目中替換字串即可。 |
| **如何以程式方式驗證變更？** | 儲存後，你可以重新讀取 `ExtGState` 字典，並斷言 `ca` 等於 `0.5`。 |

## 後續步驟與相關主題

既然你已了解如何 **編輯 PDF 透明度** 以及 **儲存已修改的 PDF** 檔案，接下來可以探索以下主題：

- **將圖形狀態套用於文字** – 在 `Tf` 運算子前使用相同的 `GS0`，即可取得半透明字體。
- **批次處理多頁** – 迴圈 `pdfDocument.Pages`，重複上述步驟。
- **結合影像覆蓋** – 在現有內容上疊加 PNG，並透過相同的圖形狀態控制其不透明度。
- **壓縮最終 PDF** – 在儲存前呼叫 `pdfDocument.Optimize()` 以減少檔案大小。

這些主題自然延伸核心技巧，讓你的 PDF 工作流程更有效率。

---

*祝程式開發愉快！如果遇到任何問題，歡迎在下方留言，或查閱 Aspose.Pdf API 參考文件以深入了解。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}