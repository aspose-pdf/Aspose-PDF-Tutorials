---
category: general
date: 2026-03-14
description: 使用 Aspose.Pdf 在 C# 中為 PDF 添加 Bates 編號。了解如何自動為法律或檔案文件加入 Bates 編號與順序頁碼。
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- Aspose PDF Bates artifact
- C# PDF automation
language: zh-hant
og_description: 一步一步為 PDF 添加 Bates 編號。本教程展示如何使用 Aspose.Pdf for .NET 添加 Bates 編號及順序頁碼。
og_title: 在 C# 中為 PDF 添加 Bates 編號 – 完整指南
tags:
- Aspose.Pdf
- C#
- PDF
- Bates numbering
title: 在 C# 中為 PDF 添加 Bates 編號 – 完整指南
url: /zh-hant/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 新增 Bates 編號 PDF – 完整教學

有沒有曾經需要 **在大量法律文件集中加入 Bates 編號 PDF**，卻不知從何著手？加入 Bates 編號是文件審閱工作流程中常見卻相當繁瑣的一環。好消息是？使用 Aspose.Pdf for .NET，你只要幾行程式碼就能自動完成整個流程。

在本指南中，我們將逐步說明 **如何在 PDF 的每一頁加入 Bates 編號**，討論 **加入連續頁碼** 的選項，並提供一段可直接執行的程式碼範例。完成後，你將擁有一個可直接嵌入任何 C# 專案的完整解決方案——不需額外腳本，也不需手動蓋章。

## 你需要的條件

- **Aspose.Pdf for .NET**（版本 23.10 或更新）。此函式庫為商業授權，但免費評估版已足以測試使用。
- .NET 開發環境（Visual Studio、Rider，或 `dotnet` CLI）。
- 一個欲標記的輸入 PDF（`input.pdf`）。
- 一點點耐心以因應偶發的邊緣案例（我們會一併說明）。

如果以上都已備妥，太好了——讓我們直接開始。

![新增 Bates 編號 PDF 範例](/images/bates-numbering-example.png "顯示已套用 Bates 編號 PDF 的畫面截圖")

## 步驟 1：建立專案並安裝 Aspose.Pdf

為了保持整潔，先建立一個全新的主控台應用程式：

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

`dotnet add package` 指令會從 NuGet 取得最新的 Aspose.Pdf 程式集，讓你立即可以開始編寫程式碼。

### 為什麼選擇主控台應用程式？

主控台應用程式輕量、可在任何環境執行，且讓你專注於 PDF 邏輯而不受 UI 干擾。當然，之後你也可以將程式碼移植到 Web API 或背景服務中——核心邏輯本身並不依賴主控台。

## 步驟 2：載入來源 PDF

開啟文件相當直接。我們會使用 `using` 區塊，讓檔案句柄自動釋放。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing;   // Required for Color

class Program
{
    static void Main()
    {
        // Adjust these paths to match your environment
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string outputPdfPath = @"C:\Docs\output.pdf";

        // Load the PDF – this is where the “add bates numbering pdf” process begins
        using (var pdfDocument = new Document(sourcePdfPath))
        {
            // Next steps go here...
        }
    }
}
```

**發生了什麼事？** `Document` 類別代表整個 PDF 檔案。透過 `using` 包裝，我們保證在結束時會呼叫 `Dispose`，將任何未寫入的變更刷新至磁碟。

## 步驟 3：定義 Bates 編號 Artifact（「如何加入 Bates」的核心）

Aspose.Pdf 將 Bates 編號視為 *artifact*——一種可在螢幕上或列印時呈現的中繼資料，除非你將 PDF 扁平化，否則不會成為永久的內容串流。以下是我們將附加到每一頁的物件：

```csharp
var batesArtifact = new BatesNumberArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    Increment = 1,
    X = 36,               // 0.5 inch from the left edge (points)
    Y = 36,               // 0.5 inch from the bottom edge (points)
    FontSize = 9,
    FontColor = Color.Black
};
```

### 為什麼使用 artifact？

- **效能**：編號即時渲染，讓你可以在不重新寫入整本 PDF 的情況下變更前綴或起始號碼。
- **彈性**：之後若需要「硬編碼」的印章以符合法院提交要求，只要執行扁平化即可。
- **精準**：位置使用點（1/72 吋）作單位，讓你能做到像素級的控制。

如果需要不同的前綴或較大的字型，只要調整屬性即可。`Increment` 欄位決定編號在每頁之間的遞增步幅——正好符合 **加入連續頁碼** 的需求。

## 步驟 4：將 Artifact 附加至每一頁

現在我們遍歷 `Pages` 集合，將 artifact 加入每頁。這就是實際的 **加入 Bates 編號 PDF** 動作。

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

### 邊緣案例說明

如果你的 PDF 已經包含 Bates artifact，可能會出現重複。可以加上一個簡易的防護機制：

```csharp
foreach (Page page in pdfDocument.Pages)
{
    bool alreadyHasBates = page.Artifacts.Any(a => a is BatesNumberArtifact);
    if (!alreadyHasBates)
        page.Artifacts.Add(batesArtifact);
}
```

這個小檢查能避免在處理已預先標記的文件批次時產生雜亂的雙重印章。

## 步驟 5：儲存更新後的 PDF

最後，將檔案寫回磁碟。你可以選擇覆寫原檔，或產生新檔——此處我們會產生一個全新的副本：

```csharp
pdfDocument.Save(outputPdfPath);
Console.WriteLine($"Bates numbers added successfully. Output saved to {outputPdfPath}");
```

當你在任何檢視器中開啟 `output.pdf`，會看到左下角出現「CASE‑1000」、「CASE‑1001」等字樣。

### 可選：扁平化 PDF

若收件方要求不可編輯的 PDF（法院提交常見需求），可將頁面扁平化：

```csharp
pdfDocument.FlattenAllPages();   // Turns artifacts into permanent content
pdfDocument.Save(outputPdfPath);
```

扁平化是一個一次性的操作；執行後，Bates 編號會成為頁面內容串流的一部份，除非重新處理，否則無法再變更。

## 完整範例程式

以下是可直接貼到 `Program.cs` 的完整程式碼，已將可選的扁平化步驟以註解方式保留，方便切換。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System;
using System.Drawing;
using System.Linq;

class Program
{
    static void Main()
    {
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string outputPdfPath = @"C:\Docs\output.pdf";

        using (var pdfDocument = new Document(sourcePdfPath))
        {
            var batesArtifact = new BatesNumberArtifact
            {
                Prefix = "CASE-",
                StartNumber = 1000,
                Increment = 1,
                X = 36,
                Y = 36,
                FontSize = 9,
                FontColor = Color.Black
            };

            foreach (Page page in pdfDocument.Pages)
            {
                // Prevent duplicate artifacts if the PDF was processed before
                bool alreadyHasBates = page.Artifacts.Any(a => a is BatesNumberArtifact);
                if (!alreadyHasBates)
                    page.Artifacts.Add(batesArtifact);
            }

            // Uncomment the next line if you need a flattened PDF for legal submission
            // pdfDocument.FlattenAllPages();

            pdfDocument.Save(outputPdfPath);
        }

        Console.WriteLine($"Bates numbers added successfully. Output saved to {outputPdfPath}");
    }
}
```

使用 `dotnet run` 執行，並在主控台看到操作成功的訊息。

## 常見問題與進階小技巧

| 問題 | 解答 |
|----------|--------|
| **可以在每頁自行調整位置嗎？** | 可以。不要使用單一的 `batesArtifact`，而是在迴圈內建立新實例，並根據頁面尺寸設定 `X`/`Y`。 |
| **如果 PDF 有密碼保護該怎麼辦？** | 使用 `new Document(sourcePdfPath, new LoadOptions { Password = "mySecret" })` 載入。其餘流程保持不變。 |
| **處理超大型檔案會不會效能太差？** | 加入 artifact 的時間複雜度為 O(N)（N 為頁數），且記憶體使用量保持低，因為 Aspose 會串流頁面。若 PDF 超過 10 000 頁，建議分批處理以避免長時間的 GC 暫停。 |
| **編號能否在每個章節重新開始？** | 完全可以。在進入下一章節的第一頁前，將 `StartNumber` 設為新值，或建立第二個 `BatesNumberArtifact` 並指定不同的 `Prefix`。 |
| **這能在 .NET Core 上執行嗎？** | 能。Aspose.Pdf 支援 .NET Framework、.NET Core 以及 .NET 5/6+，只要在 csproj 中設定正確的目標執行環境即可。 |

### 進階小技巧

當你需要為多卷文件 **加入連續頁碼** 時，可將最後使用的編號寫入一個小型 JSON 檔案。執行前先讀取、遞增，完成後再寫回。這層微小的持久化機制能防止跨次執行時意外重複編號。

## 驗證結果

在 Adobe Reader、Foxit，或甚至 Chrome 中開啟 `output.pdf`，應該會看到類似以下的畫面：

```
CASE-1000   (Page 1)
CASE-1001   (Page 2)
…
CASE-1015   (Page 16)
```

如果已執行扁平化，編號會成為頁面圖形的一部份——右鍵點擊 →「檢查」即可看到它們作為普通文字物件。

## 結論

我們剛剛示範了如何使用 Aspose.Pdf **加入 Bates 編號 PDF**，探討了 **如何加入 Bates** 的機制，並展示了在整份文件中 **加入連續頁碼** 的乾淨做法。這段程式碼已具備生產環境可用性，處理重複 artifact，並提供可選的扁平化步驟以符合法律合規需求。

接下來，你可能想要探索：

- 合併多個 PDF 同時保持 Bates 編號連續（使用 `Document.AppendDocument` 並即時調整 `StartNumber`）。
- 在 Bates 編號旁加入 QR Code，以實現自動追蹤。
- 將此邏輯整合至 ASP.NET Core API，讓你的 Web 服務能即時為 PDF 加標。

試著跑跑看，調整前綴、變換字型，讓自動化幫你減輕文件審閱的繁重工作。祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}