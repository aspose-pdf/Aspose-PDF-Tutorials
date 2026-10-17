---
category: general
date: 2026-03-06
description: 在 C# 中建立 PDF 文件，輕鬆加入 Bates 編號。學習如何在 PDF 中新增空白頁、在頁面上放置印章，並實作 Bates 編號。
draft: false
keywords:
- create pdf document
- add bates number
- add blank page pdf
- how to add bates numbering
- place stamp on page
language: zh-hant
og_description: 在 C# 中建立 PDF 文件並加入 Bates 編號。本指南說明如何新增空白頁 PDF、在頁面上放置印章，以及套用 Bates 編號。
og_title: 使用 Bates 編號建立 PDF 文件 – C# 教學
tags:
- Aspose.Pdf
- C#
- PDF automation
title: 使用 C# 建立帶有 Bates 編號的 PDF 文件 – 完整指南
url: /zh-hant/net/programming-with-stamps-and-watermarks/create-pdf-document-with-bates-numbering-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 建立帶 Bates 編號的 PDF 文件

有沒有過想 **在 C# 中建立 PDF 文件**，卻不知道如何加入 Bates 編號，結果抓狂的時候？你並不孤單——律師事務所、法院，甚至一些企業合規團隊每天都會碰到這個難題。好消息是，只要寫幾行 Aspose.Pdf 程式碼，就能快速產生全新 PDF、加上一頁空白頁，並在同一流程中蓋上正確的 Bates 編號。

在本教學中，我們會一步步說明整個過程：從專案設定、加入空白頁 PDF、了解 **如何加入 Bates 編號**，最後 **在頁面上放置印章** 並儲存結果。完成後，你會得到一段可直接放入任何 .NET 應用程式的完整範例程式碼。沒有模糊的參考，只有完整、可執行的範例。

## 你需要的環境

- **.NET 6+**（或 .NET Framework 4.6+ – Aspose.Pdf 兩者皆支援）
- **Aspose.Pdf for .NET** NuGet 套件（`Install-Package Aspose.Pdf`）
- 一個好用的 IDE（Visual Studio、Rider，或是安裝 C# 擴充功能的 VS Code）

就這樣。無需額外 DLL，亦不需要外部服務。現在就開始吧。

## 步驟 1：建立 PDF 文件 – 初始設定

首先，我們需要一個全新的 `Document` 物件。把它想像成所有內容將要寫入的空白畫布。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Initialize a new PDF document
Document pdfDocument = new Document();
```

> **為什麼這很重要：** `Document` 類別是每個 Aspose 操作的入口點。建立它後，你就能存取 `Pages` 集合、metadata 與安全設定——所有打造專業 PDF 的基礎元件。

## 步驟 2：加入空白頁 PDF

沒有頁面的 PDF 就像一本沒有頁面的書——毫無用處。加入空白頁相當簡單，且提供了可供蓋上 Bates 編號的表面。

```csharp
// Add a single blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **小技巧：** 若需要多頁，只要在迴圈中呼叫 `pdfDocument.Pages.Add()`。每次呼叫都會回傳一個全新的 `Page` 物件，讓你可以獨立客製化。

## 步驟 3：如何加入 Bates 編號 – 建立 TextStamp

接下來就是重點：**Bates 編號**。在 Aspose.Pdf 中，它只是一個帶有特殊 artifact 標記的 `TextStamp`。

```csharp
// Create a text stamp that will serve as a Bates number
TextStamp batesStamp = new TextStamp("Bates-001")
{
    // Mark the stamp as a Bates‑numbering artifact (helps PDF viewers treat it specially)
    Artifact = ArtifactType.BatesNumbering,
    // Align the stamp to the bottom‑right corner of the page
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Add a small margin so the number isn’t glued to the edge
    Margin = new Margin { Bottom = 10, Right = 10 }
};
```

> **為什麼要設定 `Artifact`：** 某些 PDF 閱讀器會把 Bates 編號當作可搜尋的 metadata。將印章標記為 `BatesNumbering` artifact，可確保下游工具自動辨識。

## 步驟 4：在頁面上放置印章

印章準備好後，我們現在 **在頁面上放置印章**。這一步會讓視覺上的編號真的出現在 PDF 中。

```csharp
// Add the Bates number stamp to the previously created page
page.AddStamp(batesStamp);
```

> **邊緣情況：** 若需要每頁的編號自動遞增，可在遍歷 `pdfDocument.Pages` 時，先更新 `batesStamp.Value`，再呼叫 `AddStamp`。此範例僅示範使用固定的 “Bates‑001”。

## 步驟 5：儲存並驗證結果

最後，我們把 PDF 寫入磁碟。請選擇一個你有寫入權限的資料夾，否則會拋出 `UnauthorizedAccessException`。

```csharp
// Save the stamped PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/BatesStamped.pdf");
```

當你在任何檢視器中開啟 `BatesStamped.pdf`，應該會看到左下角（右下角）有一個小小的 “Bates‑001”。

> **預期輸出：**  
> ![PDF with Bates number stamp](image-placeholder.png "PDF with Bates number stamp")  
> *Alt text: PDF with Bates number stamp on the bottom‑right corner.*

如果編號沒有顯示，請再次檢查 margin 設定，並確認頁面尺寸不是太小（預設 A4 正常）。同時也要確保 `Artifact` 標記沒有在後續處理工具中被剝除。

## 完整可執行範例

以下是完整、可直接複製貼上的程式碼。它包含所有 `using` 指示與說明註解，方便你快速上手。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize a new PDF document
        Document pdfDocument = new Document();

        // 2️⃣ Add a blank page – this is where we’ll put the Bates number
        Page page = pdfDocument.Pages.Add();

        // 3️⃣ Create a TextStamp for the Bates number
        TextStamp batesStamp = new TextStamp("Bates-001")
        {
            Artifact = ArtifactType.BatesNumbering,          // Marks it as a Bates‑numbering artifact
            HorizontalAlignment = HorizontalAlignment.Right, // Align right
            VerticalAlignment = VerticalAlignment.Bottom,    // Align bottom
            Margin = new Margin { Bottom = 10, Right = 10 }  // Small margin from edges
        };

        // 4️⃣ Place the stamp on the page
        page.AddStamp(batesStamp);

        // 5️⃣ Save the PDF to disk
        string outputPath = @"C:\Temp\BatesStamped.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"PDF created successfully: {outputPath}");
    }
}
```

執行程式、打開 PDF，你會看到 Bates 編號正好出現在我們指定的位置。 🎉

## 常見變化與注意事項

| 情境 | 需要變更的地方 | 原因 |
|----------|----------------|-----|
| **多頁且編號遞增** | 在 `pdfDocument.Pages` 迴圈中，於 `AddStamp` 前設定 `batesStamp.Value = $"Bates-{i:D3}"` | 為每頁提供唯一識別碼，符合法律文件的常見需求 |
| **不同位置（左上）** | 將 `HorizontalAlignment = HorizontalAlignment.Left` 與 `VerticalAlignment = VerticalAlignment.Top` | 某些組織偏好將編號放在頁首而非頁腳 |
| **自訂字型或顏色** | 設定 `batesStamp.TextState.Font = FontRepository.FindFont("Arial"); batesStamp.TextState.FontSize = 12; batesStamp.TextState.ForegroundColor = Color.Red;` | 提升可讀性或符合品牌指引 |
| **將既有 PDF 作為背景** | 使用 `Document src = new Document("source.pdf"); pdfDocument.Pages.Add(src.Pages[1]);` | 需要在預先產生的表單上蓋章時非常實用 |

## 小結

我們剛剛示範了如何 **建立 PDF 文件**、**加入空白頁 PDF**，以及 **加入 Bates 編號**，再 **在頁面上放置印章** 並儲存檔案。程式碼刻意寫得精簡，方便你在更大的工作流程中自行調整——無論是一次處理數十個檔案，或是整合到 Web 服務中。

如果想更進一步，可以考慮：

- 為大量案件檔案自動化遞增邏輯。
- 將 PDF 產生流程嵌入 ASP.NET Core API。
- 使用 `pdfDocument.Encrypt(...)` 加入密碼保護等安全機制。

盡情實驗、勇於嘗試，並在留言區提出問題。祝開發順利，願你的 PDF 永遠都能完美蓋章！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}