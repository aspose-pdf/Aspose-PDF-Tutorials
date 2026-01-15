---
category: general
date: 2026-01-15
description: 使用 Aspose.Pdf 快速為 PDF 添加 Bates 編號。了解如何在 PDF 添加頁腳、添加頁碼以及自訂頁碼。
draft: false
keywords:
- add bates numbers
- bates numbering pdf
- add footer to pdf
- add page numbers pdf
- add custom page numbering
language: zh-hant
og_description: 使用 Aspose.Pdf 快速為 PDF 添加 Bates 編號。了解如何在 PDF 中加入頁腳、添加頁碼以及自訂頁碼。
og_title: 在 PDF 中加入 Bates 編號 – Bates 編號 PDF
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: 在 PDF 中添加 Bates 編號 – Bates 編號 PDF
url: /zh-hant/net/programming-with-text/add-bates-numbers-to-pdf-bates-numbering-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 為 PDF 添加 Bates 編號 – 完整指南

是否曾需要**add bates numbers**到 PDF，但不知從何開始？你並不孤單——法律團隊、審計師以及所有處理大量文件集的人每天都會遇到這個問題。好消息是？使用 Aspose.Pdf for .NET，你只需幾行程式碼就能在每頁上添加這些編號。

在本教學中，我們將逐步說明整個流程：從引入 Aspose.Pdf 函式庫、載入來源檔案、設定 *BatesNumberingArtifact*、將其作為頁腳附加，最後儲存結果。完成後，你還會了解如何**add footer to pdf**、**add page numbers pdf**，甚至**add custom page numbering**以應對那些棘手的特殊情況。

## 需要的條件

- .NET 6+（或 .NET Framework 4.8，如果你仍在使用傳統平台）  
- 對 **Aspose.Pdf** NuGet 套件的參考 (`Install-Package Aspose.Pdf`)  
- 你想要加蓋的 PDF 檔案（我們稱之為 `source.pdf`）  

就這樣——不需要額外工具，也不需要大型 PDF 編輯器。讓我們開始吧。

![add bates numbers example](https://example.com/images/add-bates-numbers.png "add bates numbers example")

## 步驟 1：添加 Bates 編號 – 載入 PDF 文件

首先，我們需要一個代表即將修改的 PDF 的 `Document` 物件。可以把它想像成在開始打字前先開啟 Word 文件。

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the PDF you want to add bates numbers to
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // The rest of the steps go here...
    }
}
```

> **為什麼這很重要：** 載入檔案後，你就可以存取它的 `Pages` 集合，之後我們會在此附加 Bates 編號工件。如果找不到檔案，Aspose 會拋出明確的 `FileNotFoundException`，因此請再次確認路徑。

## 步驟 2：設定 bates numbering pdf 參數

現在我們定義*編號的外觀*。`BatesNumberingArtifact` 允許你設定前綴、起始編號、位數填充、後綴以及放置位置。這就是 **bates numbering pdf** 的核心。

```csharp
// Step 2: Create and configure the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    NumberDigits = 5,          // forces 5 digits, e.g., 01000
    Suffix = "-A",
    Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
};
```

> **專業提示：** 如果需要將編號顯示在頁首，請將 `BottomCenter` 換成 `TopCenter`。placement 列舉還支援 `BottomLeft`、`BottomRight` 等，讓你在不同的 **add footer to pdf** 風格間保持彈性。

## 步驟 3：Add page numbers pdf – 將工件附加到每頁

工件準備好後，我們會遍歷每一頁，將其加入 `Artifacts` 集合。這一步實際上就是 **adds page numbers pdf**。

```csharp
// Step 3: Attach the artifact to each page
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

> **底層發生了什麼？** `Artifacts` 集合會在頁面的主要內容之後渲染，確保 Bates 編號位於任何現有文字之上，但在註解之下。如果需要編號位於內容之後（較少見），可以使用 `page.Artifacts.Insert(0, batesArtifact)`。

## 步驟 4：Add custom page numbering – 儲存更新後的 PDF

最後，我們將修改後的文件寫入磁碟。輸出檔案將會把 Bates 編號作為每頁的永久部分。

```csharp
// Step 4: Save the PDF with the new numbering
pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
```

> **驗證提示：** 在任何檢視器中開啟 `bates_out.pdf`。你應該會看到類似 `CASE-01000-A` 的文字位於每頁底部中央。如果編號缺失，請再次確認 `Placement` 屬性是否與預期位置相符。

## 完整可執行範例

把所有步驟結合起來，以下是完整、可直接執行的程式碼：

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the source PDF
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // Configure Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            NumberDigits = 5,
            Suffix = "-A",
            Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
        };

        // Attach artifact to each page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.Artifacts.Add(batesArtifact);
        }

        // Save the new PDF (adds footer to pdf)
        pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

        Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
    }
}
```

### 預期結果

- **檔案：** 與 `source.pdf` 同一資料夾中的 `bates_out.pdf`  
- **視覺：** 底部中央文字 `CASE-01000-A`、`CASE-01001-A`…，每頁遞增  
- **行為：** 編號永久嵌入；即使列印、扁平化或進一步編輯仍會保留。

## 常見變化與邊緣案例

| 情況 | 調整方式 |
|-----------|---------------|
| **不同的起始編號** | 將 `StartNumber` 改為任意整數（例如 `StartNumber = 500`）。 |
| **每卷的字母後綴** | 使用迴圈在每頁修改 `Suffix`，或建立多個具有不同後綴的工件。 |
| **右對齊編號** | 設定 `Placement = BatesNumberingArtifact.PlacementLocation.BottomRight`。 |
| **大型文件（超過 10k 頁）** | 考慮分批處理頁面或增加 `NumberDigits` 以避免溢位。 |
| **需要在特定頁面隱藏編號** | 在 `foreach` 迴圈中跳過這些頁面（例如 `if (page.Number != 1) page.Artifacts.Add(batesArtifact);`）。 |

> **注意：** 使用包含非法檔名字元的 `Prefix` 或 `Suffix`（例如 `*` 或 `?`）。Aspose 仍會嵌入它們，但在之後提取文字時可能會產生問題。

## 生產環境使用的專業提示

- **快取工件**：如果連續處理多個 PDF，先建立一次工件可為每個檔案節省數毫秒的時間。  
- **執行緒安全性：** `BatesNumberingArtifact` 實例不是執行緒安全的，請為每個執行緒提供自己的副本。  
- **效能：** 對於大批量處理，可在儲存前停用 PDF 壓縮（`pdfDocument.Compress = false`），必要時再重新啟用。  
- **測試：** 總是先對第一個產生的 PDF 進行快速視覺檢查，以確保放置位置符合法律團隊的標準。

## 結論

現在你已掌握一套完整、端到端的做法，能使用 Aspose.Pdf **add bates numbers** 於任何 PDF，並提供 **add footer to pdf**、**add page numbers pdf** 與 **add custom page numbering** 的選項。此程式碼完全自包含，支援 .NET 6 及以上版本，且可直接嵌入任何現有的自動化流程中。

接下來可以做什麼？嘗試將 `BottomCenter` 放置方式改為頁首樣式，實驗動態前綴（例如從資料庫取得的案件 ID），或結合 Aspose 的文字擷取功能，為新編號的文件產生可搜尋的索引。沒有任何限制，而你已獲得一個強大的文件控制工具。

祝開發愉快，願你的 PDF 永遠保持正確的編號！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}