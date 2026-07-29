---
category: general
date: 2026-06-21
description: 在 Word 中快速加入 Bates 編號。學習如何新增 Bates、為法律文件套用 Bates 編號，並使用 C# 自動化編號。
draft: false
keywords:
- add bates numbering
- how to add bates
- bates numbering in word
- bates numbering for legal
- apply bates numbering
language: zh-hant
og_description: 使用 C# 在 Word 中加入 Bates 編號。本指南說明如何加入 Bates、為法律文件套用 Bates 編號，以及自動化此流程。
og_title: 在 Word 中加入 Bates 編號 – 完整程式教學
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  headline: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  name: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: '| Page | Bates Number | |------|--------------| | 1 | ABC-1000 | | 2 |
      ABC-1001 | | … | … | | N | ABC‑(1000 + N‑1) |'
  - name: What if the document already contains page numbers?
    text: The `AddBatesNumbering` method will **not** overwrite existing page number
      fields; it simply adds a new field. If you want to replace the existing numbers,
      remove them first or set `batesOptions.Position` to the same location as the
      current page numbers.
  - name: Can I skip pages (e.g., exclude a cover page)?
    text: 'Yes. Use the overload that accepts a `PageRange`:'
  - name: How do I change the numbering format (Roman numerals, letters)?
    text: 'The `BatesNumberingOptions` class supports a `NumberFormat` property:'
  - name: What about performance on huge files?
    text: Loading a 2‑GB Word file can consume a lot of RAM. To mitigate, process
      the document in chunks using the `DocumentSplitter` utility, apply Bates numbering
      to each chunk, then merge the parts back together. This pattern keeps memory
      usage under control while still letting you **apply bates numbering*
  type: HowTo
tags:
- document‑automation
- csharp
- legal‑tech
title: 在 Word 中加入 Bates 編號 – 完整逐步指南
url: /zh-hant/net/programming-with-document/add-bates-numbering-in-word-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Word 中加入 Bates 編號 – 完整逐步指南

有沒有想過如何在 Word 檔案中加入 Bates 編號，而不必手動輸入每一個編號？你並不孤單。許多律師、律師助理與電子發現專家都需要一種可靠的方法，**為數百頁加入 Bates 編號**，手動操作簡直是噩夢。

在本教學中，我們將逐步說明一個乾淨的 C# 解決方案，**套用 Bates 編號**於 `.docx` 檔案，解釋每一行程式碼的意義，並示範如何依法律需求微調程式碼。完成後，你只需幾秒鐘就能產生編號完整的文件，無需額外外掛。

## 你將學會

- 完整的程式碼，能 **為 Word 文件加入 Bates 編號**。
- `BatesNumberingOptions` 類別的運作方式，以及何時調整前綴或起始值。
- 在大型案件檔案上使用此方法的技巧，包含記憶體使用的考量。
- 前置條件快速概覽，讓你可以直接複製貼上解決方案並立即執行。

**前置條件**  
- .NET 6+（或若偏好舊版執行環境，可使用 .NET Framework 4.7.2+）。  
- 參考 Aspose.Words for .NET 套件（或任何提供 `AddBatesNumbering` 的類似 API）。  
- 具備基本的 C# 與 Visual Studio（或你慣用的 IDE）知識。

如果你已符合上述條件，讓我們開始吧。

## 步驟 1：設定專案並匯入函式庫

首先，建立一個新的 Console 應用程式（或整合到既有服務中）。接著加入 Aspose.Words NuGet 套件：

```bash
dotnet add package Aspose.Words
```

> **專業小技巧：** 使用免費評估授權進行測試；會加上一個小水印，但功能與正式版完全相同。

```csharp
using Aspose.Words;
using Aspose.Words.BatesNumbering;
```

這些 `using` 陳述式會將 `Document` 與 `BatesNumberingOptions` 類別引入作用域，這對稍後的 **套用 Bates 編號** 步驟至關重要。

## 步驟 2：載入來源文件

你需要一個 Word 檔案作為操作對象。以下程式碼會從你指定的資料夾載入 `input.docx`。請將 `"YOUR_DIRECTORY"` 替換為實際的路徑。

```csharp
// Step 1: Load the source document
var document = new Document("YOUR_DIRECTORY/input.docx");
```

為什麼要先載入檔案？`Document` 物件會將整個 Word 套件解析至記憶體，讓我們在儲存前就能操作頁首、頁尾與版面配置。若檔案極大（例如 10,000 頁），建議使用 `LoadOptions` 搭配 `LoadFormat.Docx` 以串流方式載入區段，而非一次全部載入。

## 步驟 3：設定 Bates 編號選項

這裡就是魔法發生的地方。你告訴函式庫使用什麼前綴（範例中的 `"ABC-"`）以及從哪個數字開始計數（`1000`）。兩者皆可自由客製化。

```csharp
// Step 2: Define Bates numbering options (prefix and starting number)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",
    Start = 1000,
    // Optional: set the position, alignment, and font if you need legal‑specific styling
    // Position = BatesNumberingPosition.Footer,
    // Alignment = BatesNumberingAlignment.Right,
    // Font = new Font("Times New Roman", 10, FontStyle.Bold)
};
```

**為什麼需要前綴？** 在法律實務中，前綴常用來識別案件或製作單位（`"ABC-"` 可能代表 *Acme Bank Corp.*）。從 `1000` 開始是常見做法，因為許多律所會保留前 999 個編號作內部草稿使用。

如果你正在處理 **法律文件的 Bates 編號**，也可以將 `batesOptions.Position` 設為 `Header` 或 `Footer`，並調整對齊方式以符合法院規範。此函式庫已內建支援這些調整。

## 步驟 4：為整份文件套用 Bates 編號

現在正式注入編號。`AddBatesNumbering` 方法會逐頁走訪，插入格式化字串，並更新文件內部的頁數計算。

```csharp
// Step 3: Apply Bates numbering to the entire document
document.AddBatesNumbering(batesOptions);
```

在背後，Aspose.Words 會在每一頁建立一個隱藏欄位，呈現為 `ABC-1000`、`ABC-1001` 等等。因為是欄位，之後若要變更前綴或起始號碼，只需編輯欄位即可，無需重新產生整個檔案——對於 **如何在發現請求變更後加入 Bates** 十分便利。

## 步驟 5：儲存已修改的文件

最後，將結果寫入新檔案。保留原始檔不被改動是最佳實務，尤其在處理必須保持原始狀態的證據時。

```csharp
// Step 4: Save the modified document
document.Save("YOUR_DIRECTORY/output.docx");
```

現在你已擁有 `output.docx`，每頁都附加了連續的 Bates 編號。用 Word 開啟後，你會看到編號正好出現在你指定的位置（預設為頁腳）。檔案大小可能會因額外欄位稍微增加，但相較於帶來的好處可說是微不足道。

### 預期輸出

| 頁碼 | Bates 編號 |
|------|------------|
| 1    | ABC-1000   |
| 2    | ABC-1001   |
| …    | …          |
| N    | ABC‑(1000 + N‑1) |

如果你開啟文件的「欄位代碼」檢視（Word 中按 `Alt+F9`），會看到類似 `{ BATES \* MERGEFORMAT ABC-1000 }` 的內容出現在每一頁。

## 邊緣情況與常見問題

### 若文件已包含頁碼該怎麼辦？

`AddBatesNumbering` 方法 **不會** 覆寫既有的頁碼欄位；它只會新增一個欄位。若想取代現有頁碼，請先移除舊的欄位，或將 `batesOptions.Position` 設為與現有頁碼相同的位置。

### 可以跳過特定頁面嗎（例如排除封面）？

可以。使用接受 `PageRange` 參數的重載版本：

```csharp
var range = new PageRange(2, document.PageCount); // start at page 2
document.AddBatesNumbering(batesOptions, range);
```

這在需要 **法律簡報的 Bates 編號** 從標題頁之後才開始的情況下非常實用。

### 如何變更編號格式（羅馬數字、字母）？

`BatesNumberingOptions` 類別支援 `NumberFormat` 屬性：

```csharp
batesOptions.NumberFormat = BatesNumberFormat.RomanUpper;
```

在呼叫 `AddBatesNumbering` 前先設定即可。此彈性有助於符合法院規定的特定樣式。

### 大檔案的效能表現如何？

載入 2 GB 的 Word 檔案會佔用大量記憶體。為降低需求，可使用 `DocumentSplitter` 工具將文件分塊處理，對每個區段套用 Bates 編號後再合併。此方式能在保持效能的同時，仍能 **有效套用 Bates 編號**。

## 完整範例程式

以下是整合所有步驟的可直接執行的 Console 程式：

```csharp
using System;
using Aspose.Words;
using Aspose.Words.BatesNumbering;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            var inputPath = @"C:\Docs\input.docx";
            var document = new Document(inputPath);

            // 2️⃣ Define Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                // Optional styling for legal compliance
                Position = BatesNumberingPosition.Footer,
                Alignment = BatesNumberingAlignment.Right,
                Font = new Font("Times New Roman", 9, FontStyle.Bold)
            };

            // 3️⃣ Apply Bates numbering across all pages
            document.AddBatesNumbering(batesOptions);

            // 4️⃣ Save the result
            var outputPath = @"C:\Docs\output.docx";
            document.Save(outputPath);

            Console.WriteLine($"✅ Bates numbering applied! Saved to {outputPath}");
        }
    }
}
```

執行程式後，開啟 `output.docx`，即可看到一串整齊的編號，適合提交、發現或法院使用。

## 結論

現在你已完全掌握 **如何在 Word 文件中加入 Bates 編號** 的 C# 實作。從載入、設定、套用到儲存的流程簡單明瞭，同時具備足夠彈性，能滿足 **法律工作流程的 Bates 編號**、自訂前綴、甚至大規模批次處理的需求。

如果想更進一步，可考慮：

- 將程式碼整合到 Web API，讓同事上傳檔案後即時取得編號後的 PDF。  
- 為檔案遺失或權限問題加入錯誤處理（在 `Document.Load` 周圍加上 `try/catch`）。  
- 探索 Aspose.Words 其他功能，如浮水印或遮蔽，打造完整的電子發現工具組。

歡迎自行嘗試不同的前綴、起始號碼，甚至在同一文件中結合多種編號方案。只要掌握核心邏輯，**套用 Bates 編號** 的應用範圍相當廣泛。

有任何問題或特殊情境想討論？在下方留言，我們一起解決。祝開發順利！

## 接下來該學什麼？

以下教學與本指南的技術緊密相關，能進一步深化你的 API 應用與實作方式，每篇皆提供完整範例與逐步說明，協助你在專案中靈活運用。

- [在 PDF 標題中套用編號樣式（Java）](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [在 PDF 標題中套用編號樣式（Java）](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [在 PDF 標題中套用編號樣式（Java）](/pdf/french/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}