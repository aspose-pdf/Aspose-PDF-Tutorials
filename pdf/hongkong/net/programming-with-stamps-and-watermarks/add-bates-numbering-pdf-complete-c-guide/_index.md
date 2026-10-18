---
category: general
date: 2026-03-22
description: 使用 Aspose.Pdf 快速為 PDF 添加 Bates 編號。了解如何添加 Bates、添加連續頁碼、添加自訂頁腳 PDF，以及在數分鐘內向
  PDF 添加工件。
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- add custom footer pdf
- add artifact to pdf
language: zh-hant
og_description: 使用 Aspose.Pdf 為 PDF 添加 Bates 編號。本指南說明如何添加 Bates 編號、添加連續頁碼、添加自訂頁腳 PDF，以及向
  PDF 添加工件。
og_title: 在 PDF 中加入 Bates 編號 – 一步一步 C# 教學
tags:
- Aspose.Pdf
- C#
- PDF automation
title: 為 PDF 添加 Bates 編號 – 完整 C# 指南
url: /zh-hant/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 中加入 Bates 編號 – 完整 C# 教學

是否曾需要將 **add bates numbering pdf** 加入一批法律文件，但不確定從何開始？你不是第一個——許多開發者在構建案件管理工具時都碰到這個障礙。好消息是？使用 Aspose.Pdf，你可以 **add bates**、**add sequential page numbers**，甚至 **add custom footer pdf** 元素，只需幾行程式碼。

在本教學中，我們將逐步說明整個流程，從安裝函式庫到儲存最終檔案，並提供如何在不破壞現有內容的情況下 **add artifact to pdf** 檔案的技巧。完成後，你將擁有一段可直接放入任何 .NET 專案的即用程式碼片段。

## 需要的條件

- .NET 6+（此程式碼同時適用於 .NET Core 與 .NET Framework）  
- 有效的 Aspose.Pdf for .NET 授權（可先使用免費評估版）  
- 放置於可參考資料夾中的輸入 PDF（`input.pdf`）  
- Visual Studio、Rider，或任何你偏好的 C# 編輯器  

就這樣——除了 Aspose.Pdf，無需其他 NuGet 套件。

## 步驟 1：透過 NuGet 安裝 Aspose.Pdf

首先，先把函式庫安裝到你的機器上。於專案資料夾開啟終端機並執行：

```bash
dotnet add package Aspose.Pdf
```

或者，若你使用 Visual Studio 的套件管理員主控台：

```powershell
Install-Package Aspose.Pdf
```

*小技巧：* 安裝完成後，請再次確認 `Aspose.Pdf` 資料夾已出現在解決方案總管的 `Dependencies → Packages` 中。

## 步驟 2：載入來源 PDF 文件

現在我們建立一個代表欲加蓋的 PDF 的 `Document` 物件。使用 `using` 陳述式可確保檔案句柄自動釋放。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing; // For Color

// Step 2: Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

為什麼使用 `using var`？即使發生例外，它也能保證釋放資源，避免稍後嘗試覆寫同一檔案時出現檔案鎖定問題。

## 步驟 3：建立與設定 Bates 編號 Artifact

Bates 編號本質上是一個存在於 PDF 邏輯結構中的文字 artifact。你可以將它視為 **custom footer pdf**，因為它會出現在每一頁上，卻不屬於頁面的內容串流。

```csharp
// Step 3: Define the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "INV-",          // Optional prefix – change as needed
    Start = 1000,             // Starting number
    Format = "0000",          // Zero‑padded format (e.g., 1000 → 1000)
    X = 500,                  // Horizontal position (points from left)
    Y = 20,                   // Vertical position (points from bottom)
    FontSize = 10,
    FontColor = Color.Black
};
```

### 為何這些設定很重要

- **Prefix**：用於區分文件類型（例如發票的 “INV‑”）。  
- **Start**：設定起始編號；若需跨檔案保持連續，可從資料庫取得此值。  
- **Format**：`"0000"` 會強制以四位數顯示，確保編號增長時仍保持對齊。  
- **X/Y**：座標以左下角為原點，`Y = 20` 會將文字放在頁面邊距上方。若想讓編號左對齊或置中，可調整 `X`。

如果你需要 **add sequential page numbers** 而非 Bates 編號，只需省略 `Prefix`，並將 `Format` 調整為 `"###"` 或其他你喜好的模式。

## 步驟 4：將 Artifact 套用至所有頁面

Aspose.Pdf 允許你一次呼叫即將 artifact 附加至整個文件。這是 **add artifact to pdf** 的最高效方式，無需手動遍歷每一頁。

```csharp
// Step 4: Apply the artifact to the whole document
pdfDocument.Pages.AddArtifact(batesArtifact);
```

在背後，Aspose 會將 artifact 加入每頁的 page dictionary，這表示編號成為 PDF 邏輯結構的一部份——非常適合之後的抽取或搜尋。

## 步驟 5：儲存更新後的 PDF

最後，將變更寫回磁碟。你可以覆寫原始檔案，或另存為新檔；開發階段建議使用後者較安全。

```csharp
// Step 5: Save the PDF with Bates numbers
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

當你在檢視器中開啟 `output.pdf` 時，會在每頁的右下角看到 “INV‑1000”、 “INV‑1001”、 … 等字樣。

### 驗證結果

在 Adobe Acrobat 或任何檢視器中開啟 PDF，尋找這些編號。若需以程式方式驗證，可讀回 artifact：

```csharp
foreach (var page in pdfDocument.Pages)
{
    foreach (var artifact in page.Artifacts)
    {
        Console.WriteLine($"Page {page.Number}: {artifact.Text}");
    }
}
```

此程式碼會印出每頁的 Bates 標籤——對自動化測試相當方便。

## 邊緣情況與常見問題

### 如果我的 PDF 已經有頁腳怎麼辦？

加入 artifact 不會覆寫既有頁腳，因為 artifact 位於獨立層。若視覺上有重疊問題，可調整 `Y` 座標或增加 `X` 偏移量，將 Bates 編號移開。

### 我可以使用不同的字型或顏色嗎？

當然可以。`BatesNumberingArtifact` 繼承自 `Artifact`，因此你可以設定 `Font`、`FontColor`，甚至 `Opacity`。範例：

```csharp
batesArtifact.Font = FontRepository.FindFont("Arial");
batesArtifact.FontColor = Color.FromArgb(255, 0, 0); // Red
```

### 如何為新文件重設計數器？

只要在呼叫 `AddArtifact` 前修改 `Start` 即可。若在迴圈中產生大量 PDF，請在應用程式邏輯中保留一個遞增計數器。

### 此方法能相容於加密的 PDF 嗎？

若提供密碼，Aspose.Pdf 能開啟加密的 PDF：

```csharp
var loadOptions = new LoadOptions { Password = "mySecret" };
using var pdfDocument = new Document("encrypted.pdf", loadOptions);
```

解密後，相同的 artifact 加入步驟即可順利執行。

## 完整可執行範例

以下為完整、可直接執行的程式。將其貼到 Console 應用程式中，調整路徑後按 **F5**。

```csharp
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Create the Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "INV-",
            Start = 1000,
            Format = "0000",
            X = 500,
            Y = 20,
            FontSize = 10,
            FontColor = Color.Black
        };

        // Apply the artifact to every page
        pdfDocument.Pages.AddArtifact(batesArtifact);

        // Save the result
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**預期輸出：** 主控台會印出 “Bates numbering added successfully!”，且 `output.pdf` 會包含如 `INV‑1000`、`INV‑1001` 等依序編號，位於每頁的右下角。

## 重點回顧

- **Primary goal:** 使用 Aspose.Pdf **add bates numbering pdf**。  
- 我們說明了 **how to add bates**、**add sequential page numbers**，以及透過單一 artifact **add custom footer pdf** 元素的方式。  
- 本教學展示了如何 **add artifact to pdf**、處理邊緣情況並驗證結果。  

## 下一步？

- **Dynamic prefixes**：從資料庫取得值，產生 “CASE‑2023‑001”、 “CASE‑2023‑002”、 …  
- **Conditional placement**：利用頁面尺寸偵測（`page.MediaBox`）在橫向頁面上置中編號。  
- **Combine with watermarks**：在 Bates 編號旁加入半透明標誌，以作品牌標示。  

盡情嘗試吧——或許你會發現更聰明的方式來批次處理數千個檔案。若遇到問題，歡迎留言或查閱 Aspose 官方文件（相當清晰）。祝開發愉快！  

![add bates numbering pdf example](https://example.com/bates-numbering-screenshot.png "Screenshot showing add bates numbering pdf in a PDF viewer")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}