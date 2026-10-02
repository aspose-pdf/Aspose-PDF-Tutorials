---
category: general
date: 2026-02-28
description: 使用 C# 建立 PDF 文件並加入 Bates 編號。學習如何在 PDF 中添加 Bates 編號、設定前綴，並在一次教學中產生連續的
  PDF 編號。
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add document identification numbers
- add sequential pdf numbers
language: zh-hant
og_description: 使用 C# 建立帶有 Bates 編號的 PDF 文件。本教學示範如何在 PDF 中加入 Bates 編號、設定自訂前綴，並產生連續的
  PDF 編號。
og_title: 使用 C# 建立 PDF 文件 – 加入 Bates 編號
tags:
- Aspose.PDF
- C#
- PDF automation
title: 使用 C# 建立 PDF 文件 – 添加 Bates 編號指南
url: /zh-hant/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 PDF 文件 C# – 新增 Bates 編號指南

有沒有想過如何 **create PDF document C#** 在每一頁上已經帶有唯一識別碼？當你需要追蹤法律文件、法院提交的檔案，或任何必須以編號搜尋的 PDF 批次時，這是一個常見的痛點。好消息是？使用 Aspose.PDF 只需幾行程式碼即可加入 Bates 編號——不需要手動編輯。

在本指南中，我們將逐步說明整個流程：載入現有的 PDF、設定 **add bates numbering pdf**、套用編號，最後儲存結果。完成後，你將能夠自動 **add document identification numbers**，甚至 **add sequential PDF numbers**，全部使用 C#。

## 先決條件

- .NET 6.0 或更新版本（此 API 亦支援 .NET Framework 4.5 以上）
- 取得 **Aspose.PDF for .NET** 的授權版（免費試用版可用於測試）
- 想要編號的輸入 PDF 檔案（以下稱為 `input.pdf`）
- Visual Studio 2022（或任何你偏好的 IDE）

不需要除 Aspose.PDF 之外的其他 NuGet 套件。

![Create PDF Document C# with Bates numbering](https://example.com/image.png "Create PDF Document C# example")

## 第一步：載入來源 PDF 文件

在你能 **add bates numbering pdf** 之前，需要一個代表磁碟上檔案的 `Document` 物件。

```csharp
using Aspose.Pdf;

// Load the source PDF document
var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*為什麼這很重要*：`Document` 類別是 Aspose.PDF 所有操作的入口點。它抽象化檔案系統，讓你可以在不直接操作原始位元組的情況下，處理頁面、註解與中繼資料。

> **專業提示：** 如果你在迴圈中處理大量檔案，僅在來源相同的情況下重複使用同一個 `Document` 實例；否則，為每個檔案建立新的物件以避免記憶體洩漏。

## 第二步：定義 Bates 編號選項

這裡就是 **how to add bates** 變得具體的地方。你需要設定 `BatesNumberingOptions` 物件，告訴 Aspose 前綴應為何、起始位置以及字型大小。

```csharp
// Define Bates numbering options (prefix, start number, font size)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",   // You can change this to any string you need
    Start = 1000,      // Starting number – useful for continuous numbering across batches
    FontSize = 9       // Small enough to fit in the margin but still readable
};
```

*為什麼這很重要*：`Prefix` 讓你嵌入案件識別碼（例如 “ABC-”）。`Start` 屬性在你於多個文件之間 **adding sequential PDF numbers** 時至關重要——只要持續遞增即可。`FontSize` 確保編號不會遮蔽既有內容。

## 第三步：將 Bates 編號套用至整份文件

現在我們實際在每一頁上蓋上編號。`BatesNumbering` 類別負責所有繁重的工作。

```csharp
// Apply Bates numbering to the entire document
var bates = new BatesNumbering();
bates.AddBatesNumbering(pdfDocument, batesOptions);
```

*為什麼這很重要*：在底層，Aspose 會逐頁遍歷，計算適當的編號（Prefix + (Start + pageIndex)），預設將其繪製在右下角。你之後可以自訂位置，但預設對大多數法律樣式文件皆適用。

> **常見問題：** *如果我只需要編號部分頁面怎麼辦？*  
> 使用重載 `AddBatesNumbering(Document, BatesNumberingOptions, int startPage, int endPage)` 來限制範圍。

## 第四步：儲存已套用 Bates 編號的 PDF

最後一步是將修改過的文件寫回磁碟。

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*為什麼這很重要*：`Save` 方法會保留原始檔案格式，因此你會得到一個任何檢視器都能開啟的標準 PDF——每頁都已完整加入 **add document identification numbers**。

## 完整範例

把所有步驟結合起來，以下是一個可自行貼入新 Console 應用程式並立即執行的完整程式。

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF document
            var inputPath = @"YOUR_DIRECTORY/input.pdf";
            var pdfDocument = new Document(inputPath);

            // 2️⃣ Define Bates numbering options (prefix, start number, font size)
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                FontSize = 9
            };

            // 3️⃣ Apply Bates numbering to the entire document
            var bates = new BatesNumbering();
            bates.AddBatesNumbering(pdfDocument, batesOptions);

            // 4️⃣ Save the PDF with Bates numbers applied
            var outputPath = @"YOUR_DIRECTORY/output.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbering added successfully. Output saved to {outputPath}");
        }
    }
}
```

**預期結果**：在任何檢視器中開啟 `output.pdf`；你會看到每頁右下角分別印有 “ABC‑1000”、 “ABC‑1001”、 … 等字樣。這些編號是可選取的文字，因而可搜尋且可複製——正是正確 **add sequential PDF numbers** 實作所應有的行為。

## 邊緣情況與變化

### 自訂位置

如果預設的角落與現有頁腳衝突，你可以調整放置位置：

```csharp
batesOptions.Position = new Position(10, 10); // X, Y from the bottom‑left
```

### 不同的編號格式

想要零填充的編號（例如 001000）嗎？使用 `NumberFormat`：

```csharp
batesOptions.NumberFormat = "D6"; // Pads to 6 digits
```

### 批次處理多個檔案

在處理大量 PDF 時，維持一個遞增計數器：

```csharp
int globalStart = 5000;
foreach (var file in Directory.GetFiles(@"YOUR_DIRECTORY\Batch", "*.pdf"))
{
    var doc = new Document(file);
    var opts = new BatesNumberingOptions
    {
        Prefix = "BATCH-",
        Start = globalStart,
        FontSize = 9
    };
    new BatesNumbering().AddBatesNumbering(doc, opts);
    doc.Save(Path.ChangeExtension(file, ".bated.pdf"));
    globalStart += doc.Pages.Count; // Increment for the next file
}
```

### 處理受密碼保護的 PDF

如果來源 PDF 已加密，於建立 `Document` 時傳入密碼：

```csharp
var pdfDocument = new Document("protected.pdf", new LoadOptions { Password = "mySecret" });
```

## 常見問與答

| Question | Answer |
|----------|--------|
| **我可以使用其他函式庫嗎？** | 可以，像 iTextSharp 或 PdfSharp 等函式庫也支援頁面層級的文字插入，但 Aspose.PDF 提供最直接的 API 來進行 Bates 編號。 |
| **這會影響檔案大小嗎？** | 每頁僅加入少量文字位元組，影響可以忽略不計；輸出檔案大小通常每頁增加不到 1 KB。 |
| **編號可以被搜尋嗎？** | 絕對可以。Aspose 以文字物件寫入編號，而非影像，因而可被 PDF 閱讀器索引。 |
| **如果我需要不同的字型怎麼辦？** |將 `batesOptions.Font` 設為 `Font` 物件（例如 `FontRepository.FindFont("Arial")`）。 |

## 結論

我們剛剛示範了如何使用 Aspose.PDF **create PDF document C#** 並即時 **add bates numbering pdf**。此流程簡單、可靠且完全可程式化——非常適合法律事務所、政府機構或任何必須對大量檔案 **add document identification numbers** 與 **add sequential PDF numbers** 的組織。

以此為基礎進行實驗：為不同部門嘗試不同前綴、在多個檔案之間串接編號，或在 Bates 編號旁嵌入 QR Code 以提升可追溯性。一旦掌握核心工作流程，想像空間無限。

如果你覺得本教學有幫助，請分享、留下評論，或探索我們其他關於 C# PDF 操作的指南。祝程式開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}