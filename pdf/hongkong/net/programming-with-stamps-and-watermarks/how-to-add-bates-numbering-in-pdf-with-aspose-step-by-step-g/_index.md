---
category: general
date: 2026-07-20
description: 如何使用 Aspose.Pdf 為 PDF 添加 Bates 編號。學習快速且可靠地在 PDF 中加入 Bates 編號並在每頁加蓋印章。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to add bates numbering
- add bates numbers pdf
- add stamp to each page
language: zh-hant
lastmod: 2026-07-20
og_description: 如何使用 Aspose.Pdf 為 PDF 添加 Bates 編號。本指南示範如何在 PDF 中加入 Bates 編號，並僅用幾行
  C# 程式碼為每頁加蓋印章。
og_image_alt: Screenshot of a PDF page displaying Bates numbering added by Aspose.Pdf
og_title: 如何在 PDF 中加入 Bates 編號 – 完整 Aspose.Pdf 教學
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: How to add bates numbering to a PDF using Aspose.Pdf. Learn to add
    bates numbers pdf and add stamp to each page quickly and reliably.
  headline: How to Add Bates Numbering in PDF with Aspose – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: Yes. Load the document with a `PdfLoadOptions` object that supplies the
      password, then proceed exactly as shown.
    question: Does this work with password‑protected PDFs?
  - answer: Create multiple `BatesNumberingStamp` instances, configure each with its
      own `Prefix`, and apply them only to the appropriate page ranges.
    question: What if I need different prefixes per case?
  - answer: 'Aspose.Pdf offers a 30‑day trial. For production use you’ll need a license,
      but the API surface remains identical. --- ## Conclusion We’ve just covered
      **how to add bates numbering** to any PDF using Aspose.Pdf, demonstrated how
      to **add bates numbers pdf** in a clean, repeatable fashion, and showed'
    question: Is the library free?
  type: FAQPage
tags:
- Aspose.Pdf
- Bates numbering
- PDF automation
title: 使用 Aspose 為 PDF 添加 Bates 編號 – 步驟指南
url: /zh-hant/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-aspose-step-by-step-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose 在 PDF 中添加 Bates 編號 – Step‑by‑Step Guide

有沒有想過 **如何在法律文件中添加 bates numbering** 而不必在圖形介面上花上數小時？你並非唯一有此疑問的人。在許多律師事務所、政府機構，甚至大型企業中，為每頁加上唯一識別碼是日常工作——但只需一行 C# 程式碼，就能輕鬆搞定。

在本教學中，我們將逐步示範一個完整且可執行的範例，說明如何使用 Aspose.Pdf 函式庫 **添加 bates numbering**。完成後，你也會知道如何 **add bates numbers pdf** 檔案以及 **add stamp to each page**，僅需幾行程式碼。沒有魔法，只有清晰的推理與實用技巧。

## 你將學到

- 使用 Aspose.Pdf 載入現有的 PDF。
- 建立 `BatesNumberingStamp` 並自訂外觀。
- 逐頁迴圈，自動 **add stamp to each page**。
- 將結果儲存為新 PDF，使每頁都帶有專業的 Bates 編號。

### 前置條件

- .NET 6.0 或更新版本（此程式碼亦可在 .NET Framework 4.7+ 上執行）。
- 有效的 Aspose.Pdf for .NET 授權（或暫時的評估金鑰）。
- 需要編號的原始 PDF 檔案（以下稱為 `Original.pdf`）。

如果你符合以上三項條件，即可開始動手。

---

## 步驟 1：設定專案並安裝 Aspose.Pdf

首先，建立一個新的 Console 專案（或將程式碼加入現有專案）。接著取得 NuGet 套件：

```bash
dotnet add package Aspose.Pdf
```

> **小技巧：** 若你位於企業網路，請確保已將 NuGet 來源設定為能連線至 `https://www.nuget.org`。

## 步驟 2：載入來源 PDF 文件

載入 PDF 如同指向檔案路徑給 Aspose 那麼簡單。`Document` 類別代表整個檔案。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the source PDF (replace the path with your own)
var document = new Document(@"C:\Temp\Original.pdf");

// Quick sanity check – how many pages are we dealing with?
Console.WriteLine($"Document contains {document.Pages.Count} pages.");
```

為什麼要記錄頁數？因為 Bates 編號必須在 *所有* 頁面上保持連續，同時也能確認你沒有誤載入其他檔案。

## 步驟 3：建立 Bates 編號印章

此操作的核心是 `BatesNumberingStamp`。它允許你設定前綴、分隔符、位數填充，甚至決定印章是否視為 *artifact*（即對文字擷取工具隱形）。

```csharp
var batesStamp = new BatesNumberingStamp
{
    // Starting number – change this to whatever your workflow requires
    StartingNumber = 1000,

    // A human‑readable prefix, often a case or project code
    Prefix = "ABC-",

    // Separator between the running number and the total page count
    Separator = "/",

    // Pad the number with leading zeros to a fixed width (5 digits here)
    NumberOfDigits = 5,

    // Mark the stamp as an artifact so it won’t be indexed by search
    Artifact = true
};
```

**為什麼這樣設定？**  
- `StartingNumber = 1000` 模擬常見的法律案卷已具備的編號起點。  
- `NumberOfDigits = 5` 確保編號如 `01000`、`01001` 等能整齊對齊。  
- `Artifact = true` 在 PDF 需送入 OCR 或 e‑discovery 流程時相當重要；編號對人類可見，但會被文字搜尋引擎忽略。

## 步驟 4：為每頁加上印章

現在我們遍歷 `document.Pages`，將相同的印章套用至每一頁。Aspose 會自動為你遞增編號。

```csharp
foreach (Page page in document.Pages)
{
    // The AddStamp method clones the stamp for the current page,
    // updates the running number, and positions it at the default location.
    page.AddStamp(batesStamp);
}
```

> **常見問題：** *我可以控制印章出現的位置嗎？*  
> 當然可以。`BatesNumberingStamp` 繼承自 `Stamp`，因此你可以在迴圈前設定 `HorizontalAlignment`、`VerticalAlignment`、`XIndent`、`YIndent` 等屬性。為了簡潔，我們僅使用預設的右下角位置。

## 步驟 5：儲存已修改的 PDF

最後，將變更寫入檔案。你可以覆寫原始檔案或寫入新位置——此處我們保留兩個副本。

```csharp
// Save the new PDF with Bates numbers
document.Save(@"C:\Temp\BatesNumbered.pdf");

// Inform the user
Console.WriteLine("Bates numbering added successfully!");
```

當你開啟 `BatesNumbered.pdf` 時，每頁都會顯示類似以下的印章：

```
ABC-01000/00123
ABC-01001/00123
…
ABC-01122/00123
```

其中 `00123` 為總頁數，前綴 `ABC-` 為固定不變。

---

## 完整範例程式

將下方整段程式碼複製到全新的 `Program.cs` 檔案中並執行。依照你的環境調整檔案路徑。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            var srcPath = @"C:\Temp\Original.pdf";
            var document = new Document(srcPath);
            Console.WriteLine($"Loaded '{srcPath}' with {document.Pages.Count} pages.");

            // 2️⃣ Configure the Bates numbering stamp
            var batesStamp = new BatesNumberingStamp
            {
                StartingNumber = 1000,
                Prefix = "ABC-",
                Separator = "/",
                NumberOfDigits = 5,
                Artifact = true,
                // Optional: change alignment if you need a different location
                // HorizontalAlignment = HorizontalAlignment.Left,
                // VerticalAlignment = VerticalAlignment.Top,
                // XIndent = 20,
                // YIndent = 20
            };

            // 3️⃣ Apply the stamp to every page
            foreach (Page page in document.Pages)
            {
                page.AddStamp(batesStamp);
            }

            // 4️⃣ Save the new PDF
            var outPath = @"C:\Temp\BatesNumbered.pdf";
            document.Save(outPath);
            Console.WriteLine($"Saved Bates‑numbered PDF to '{outPath}'.");
        }
    }
}
```

**預期在主控台的輸出：**

```
Loaded 'C:\Temp\Original.pdf' with 12 pages.
Saved Bates-numbered PDF to 'C:\Temp\BatesNumbered.pdf'.
```

開啟已儲存的檔案，你會看到每頁都有連續的編號——正是你在 **add bates numbers pdf** 時所期待的結果。

## 進階調整（可選）

| 目標 | 如何實現 |
|------|-------------------|
| **Change stamp color** | Set `batesStamp.Color = Color.FromRgb(255, 0, 0);` before the loop. |
| **Place stamp in the header** | Adjust `HorizontalAlignment` and `VerticalAlignment` properties as shown in the commented code. |
| **Skip certain pages** | Add an `if (page.Number % 2 == 0) continue;` condition inside the `foreach`. |
| **Use a custom font** | Assign `batesStamp.Font = FontRepository.FindFont("Arial");`. |
| **Make the stamp visible to OCR** | Set `Artifact = false`. |

這些變化讓你在保持核心邏輯簡潔的同時，仍能 **add stamp to each page**。

## 常見問題

**Q: 這能用於受密碼保護的 PDF 嗎？**  
A: 可以。使用提供密碼的 `PdfLoadOptions` 物件載入文件，然後照示範步驟繼續執行。

**Q: 若每個案件需要不同的前綴怎麼辦？**  
A: 建立多個 `BatesNumberingStamp` 實例，為每個實例設定不同的 `Prefix`，並僅在相應的頁面範圍內套用。

**Q: 這個函式庫是免費的嗎？**  
A: Aspose.Pdf 提供 30 天試用。正式環境需購買授權，但 API 介面保持不變。

---

## 結論

我們剛剛說明了如何使用 Aspose.Pdf **添加 bates numbering** 到任何 PDF，示範了以乾淨且可重複的方式 **add bates numbers pdf**，以及如何透過單一迴圈以最簡單的方式 **add stamp to each page**。程式碼完整自足，執行僅需數秒，且可直接嵌入更大的文件處理流程中，無需修改。

準備好接受下一個挑戰了嗎？試著產生一頁列出 Bates 範圍的封面，或在每個印章旁嵌入 QR Code。可能性無窮無盡，今天學到的模式將在任何需要自動化 PDF 中繼資料的情境中派上用場。

如果你覺得本指南對你有幫助，請分享、留下評論，或探索我們其他關於 PDF 合併、浮水印與數位簽章的教學。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，建立在本篇示範的技巧之上。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET&#58; A Complete Guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [How to Add Page Number Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}