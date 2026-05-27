---
category: general
date: 2026-05-27
description: 使用 Aspose.Pdf 在 C# 中為 PDF 添加 Bates 編號。了解如何快速添加 Bates 編號、客製化格式，並自動化法律文件標籤。
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbering
language: zh-hant
og_description: 使用 Aspose.Pdf 在 C# 中為 PDF 添加 Bates 編號。本指南說明如何添加 Bates 編號、設定前綴，並儲存結果。
og_title: 在 C# 中為 PDF 加入 Bates 編號 – 逐步教學
schemas:
- author: Aspose
  dateModified: '2026-05-27'
  description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  headline: Add Bates Numbering PDF in C# – Complete Guide
  type: TechArticle
- description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  name: Add Bates Numbering PDF in C# – Complete Guide
  steps:
  - name: Expected Output
    text: 'When you run the program, the console prints:'
  - name: Can I position the Bates number elsewhere?
    text: Yes. Use the `BatesNumberingArtifact`’s `Location` property (e.g., `Location
      = new Position(10, 10)`) to place the number at custom X/Y coordinates. You
      can also set `HorizontalAlignment` and `VerticalAlignment` for more control.
  - name: What if my PDF has thousands of pages?
    text: Aspose.Pdf streams pages efficiently, but it’s still a good idea to process
      in batches if you hit memory limits. The `Document` class also supports `PdfConverter`
      for incremental saving.
  - name: How do I change the font or color?
    text: 'Wrap the artifact in a `TextState` object:'
  - name: Do I need a license for production use?
    text: A licensed version removes evaluation watermarks and unlocks full performance.
      The free trial works fine for testing and proof‑of‑concepts.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- Bates numbering
- PDF automation
title: 在 C# 中為 PDF 添加 Bates 編號 – 完整指南
url: /zh-hant/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中為 PDF 加入 Bates 編號 – 完整指南

有沒有想過 **如何在 PDF 中加入 Bates 編號**，卻不必花上數小時手動操作？你並不孤單——法律團隊、稽核人員與 e‑discovery 專家都需要一種可靠的方式，能以程式方式 **為 PDF 檔案加入 Bates 編號**。  

在本教學中，我們將使用 Aspose.Pdf for .NET，示範一個簡潔、端到端的解決方案，讓你只需幾行 C# 程式碼，即可在任何文件上加上 Bates 編號。

## 你將學會

- 如何使用 Aspose.Pdf 開啟既有 PDF  
- 如何建立 Bates 編號的 Artifact 並微調其格式  
- 如何將 Artifact 附加至每一頁（或僅第一頁）  
- 如何儲存更新後的檔案並驗證結果  

不需要事先了解 Aspose——只要具備 C# 與 .NET 的基本概念即可。完成後，你將擁有一段可直接複製貼上的可重用程式碼。

## 前置條件

- .NET 6.0 或更新版本（此程式碼亦支援 .NET Framework 4.7+）  
- Aspose.Pdf for .NET NuGet 套件（`Install-Package Aspose.Pdf`）  
- 一個欲標記的來源 PDF 檔案（放在可參考的資料夾內）  

> **小技巧：** 若尚未取得授權，Aspose 提供免費的臨時金鑰，可移除評估水印。

## 步驟 1 – 開啟來源 PDF 文件  

首先，我們需要一個 `Document` 物件來代表磁碟上的檔案。把它想成載入一張空白畫布，之後再在上面繪製 Bates 編號。

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Adjust the path to point at your source PDF
        string sourcePath = @"C:\Docs\source.pdf";

        // Load the PDF – this is where we start to add Bates numbering
        using (var pdfDocument = new Document(sourcePath))
        {
            // The rest of the logic lives inside this using block
        }
    }
}
```

**為什麼這很重要：** 在 `using` 區塊內開啟文件，可確保所有非受控資源即時釋放，對大型 PDF 尤為關鍵。

## 步驟 2 – 建立 Bates 編號 Artifact  

`BatesNumberingArtifact` 是 Aspose 用來描述編號外觀的方式。你可以設定前綴、起始號碼、遞增值，甚至自訂格式字串。

```csharp
// Step 2: Define the Bates numbering artifact
var batesNumbering = new BatesNumberingArtifact
{
    Prefix = "ABC",            // Text that appears before each number
    StartNumber = 1000,        // First number in the sequence
    Increment = 1,             // Step between consecutive numbers
    Format = "{0:D5}"          // Zero‑padded 5‑digit number (e.g., 01000)
};
```

**可能需要調整的情境：**  
- **Prefix** 可用於案件編號（如 “CASE‑”、 “DOC‑”）。  
- **StartNumber** 讓你接續先前的編號系列。  
- **Increment** 若需要奇/偶編號，可設為 2。  
- **Format** 支援任何 .NET 複合格式；`{0:D5}` 會保證五位數且前面補零。

## 步驟 3 – 將 Artifact 附加至目標頁面  

你可以將 Artifact 加到單一頁面、頁面範圍，或整本文件。大多數法律工作流程會把它加到 *每一頁*，但以下範例示範最小情況——只在第一頁加入。

```csharp
// Step 3: Attach the artifact to the first page (index is 1‑based)
pdfDocument.Pages[1].Artifacts.Add(batesNumbering);
```

若需覆蓋全部頁面，可使用迴圈：

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesNumbering);
}
```

**此步驟關鍵所在：** Artifact 會在頁面內容之後渲染，因而讓編號顯示在原有文字之上，且不會改變原始版面配置。

## 步驟 4 – 儲存已修改的 PDF  

最後，將變更寫回磁碟。你可以覆寫原檔，或產生新檔——此處我們會產生名為 `bates.pdf` 的全新副本。

```csharp
// Step 4: Persist the changes
string outputPath = @"C:\Docs\bates.pdf";
pdfDocument.Save(outputPath);

Console.WriteLine($"Bates numbering added successfully. File saved to: {outputPath}");
```

開啟 `bates.pdf` 後，你會看到 “ABC01000”（或你設定的格式）以預設位置（通常是右下角）蓋章顯示。

## 完整範例程式  

以下為完整程式碼，直接編譯執行即可：

```csharp
using Aspose.Pdf;
using System;

class AddBatesNumbering
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Open the source PDF
        // -----------------------------------------------------------------
        string sourcePath = @"C:\Docs\source.pdf";
        using (var pdfDocument = new Document(sourcePath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Create and configure the Bates numbering artifact
            // -----------------------------------------------------------------
            var batesNumbering = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                StartNumber = 1000,
                Increment = 1,
                Format = "{0:D5}"
            };

            // -----------------------------------------------------------------
            // 3️⃣ Attach the artifact to each page (or a specific page)
            // -----------------------------------------------------------------
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesNumbering);
            }

            // -----------------------------------------------------------------
            // 4️⃣ Save the new PDF
            // -----------------------------------------------------------------
            string outputPath = @"C:\Docs\bates.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbers added. Output: {outputPath}");
        }
    }
}
```

### 預期輸出

執行程式後，主控台會印出：

```
Bates numbers added. Output: C:\Docs\bates.pdf
```

開啟 `bates.pdf` 後，可見前綴 “ABC” 加上零填充的五位數序列，出現在每一頁——正是程式碼所設定的結果。

## 常見問題與特殊情況

### 可以把 Bates 編號放在其他位置嗎？

可以。使用 `BatesNumberingArtifact` 的 `Location` 屬性（例如 `Location = new Position(10, 10)`）即可自訂 X/Y 座標。也可以設定 `HorizontalAlignment` 與 `VerticalAlignment` 取得更細緻的控制。

### 若我的 PDF 有上千頁怎麼辦？

Aspose.Pdf 會有效率地串流頁面，但若遇到記憶體限制，建議分批處理。`Document` 類別亦支援 `PdfConverter` 進行增量儲存。

### 如何變更字型或顏色？

將 Artifact 包裹在 `TextState` 物件中：

```csharp
batesNumbering.TextState = new TextState
{
    FontSize = 12,
    Font = FontRepository.FindFont("Arial"),
    ForegroundColor = Color.FromRgb(255, 0, 0) // red
};
```

### 生產環境需要授權嗎？

取得授權版可移除評估水印，並解鎖完整效能。免費試用版足以用於測試與概念驗證。

## 驗證 – 快速目視檢查  

若想自動化驗證，Aspose 能抽取頁面文字並確認前綴是否存在：

```csharp
string pageText = pdfDocument.Pages[1].ExtractText();
bool hasBates = pageText.Contains("ABC01000");
Console.WriteLine(hasBates ? "Bates number verified." : "Number missing!");
```

在儲存步驟之後執行此段程式，若一切順利，會印出 `Bates number verified.`。

## 結論  

現在你已掌握 **如何在 C# 中使用 Aspose.Pdf 為 PDF 加入 Bates 編號**。從開啟文件、設定 Artifact、附加至頁面，到最後儲存，整個流程簡單且可全程腳本化。  

接下來可以嘗試以下變化：

- 為不同案件批次設定不同的 `Prefix`  
- 使用自訂 `Location` 與 `TextState` 進行品牌化  
- 依迴圈調整 `StartNumber`，為每卷加入特定前綴（如 “VOL‑1‑”、 “VOL‑2‑”）  

這些調整能讓解決方案符合幾乎所有法律或檔案保存工作流程的需求。  

對 **如何為多語系 PDF 或加密檔案加入 Bates 編號** 有更多疑問嗎？歡迎在下方留言，祝開發順利！

## 相關教學

- [如何在 Aspose.PDF for .NET 中加入與自訂 PDF 頁碼 | 文件操作指南](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [如何在 Aspose.PDF for .NET 中加入不同的頁首 | 步驟說明](/pdf/english/net/document-manipulation/add-different-headers-aspose-pdf-net/)
- [如何在 Aspose.PDF for .NET 中加入文字印章頁腳 | 步驟說明](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}