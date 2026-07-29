---
category: general
date: 2026-06-21
description: 使用 C# 在 PDF 上繪製矩形。了解如何載入 PDF 文件、建立黑色矩形註解，並有效地儲存已修改的 PDF。
draft: false
keywords:
- draw rectangle on pdf
- load pdf document
- add black rectangle
- create black rectangle
- save modified pdf
language: zh-hant
og_description: 在 C# 中於 PDF 上繪製矩形，方法是載入 PDF 文件、建立黑色矩形標註，並儲存已修改的 PDF。已包含完整程式碼。
og_title: 使用 C# 在 PDF 上繪製矩形 – 完整程式設計教學
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
    black rectangle annotation, and save modified PDF efficiently.
  headline: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
  type: TechArticle
- description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
    black rectangle annotation, and save modified PDF efficiently.
  name: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
  steps:
  - name: .NET 6.0 SDK (or any recent .NET version) installed
    text: .NET 6.0 SDK (or any recent .NET version) installed
  - name: 'A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package
      Aspose.PDF`)'
    text: 'A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package
      Aspose.PDF`)'
  - name: An existing PDF file (`input.pdf`) placed in a folder you can read/write
    text: An existing PDF file (`input.pdf`) placed in a folder you can read/write
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
title: 使用 C# 在 PDF 上繪製矩形 – 逐步指南
url: /zh-hant/net/annotations/draw-rectangle-on-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 在 PDF 上繪製矩形 – 完整程式教學

曾經需要在 .NET 應用程式中 **在 PDF 上繪製矩形**，卻不知從何下手嗎？你並不孤單。無論是想標示某個區段、遮蔽敏感資料，或只是加入視覺提示，學會以程式方式 *在 PDF 上繪製矩形* 都能為你節省大量手動編輯的時間。

在本指南中，我們將示範一個實用範例，**載入 PDF 文件**、**建立黑色矩形**，最後 **儲存已修改的 PDF**。完成後，你將擁有一段可直接放入任何 C# 專案的可重用程式碼——沒有神祕，只要清晰的程式與說明。

## 本教學涵蓋內容

- 如何使用 **Aspose.PDF for .NET** 套件 **載入 pdf 文件**  
- 定義矩形座標並確保其位於頁面範圍內  
- 使用 **add black rectangle** 方法為頁面加上註解  
- **Save modified pdf** 至新檔案位置  
- 邊緣情況處理（多頁、超出範圍的矩形、自訂顏色）  

不需要外部工具，也沒有模糊的參考——只要一個完整、可執行的範例，你可以直接 copy‑paste。

---

## 前置需求

在開始之前，請確保你已具備：

1. 已安裝 .NET 6.0 SDK（或任何較新的 .NET 版本）  
2. 參考 **Aspose.PDF for .NET**（可透過 NuGet 取得：`Install-Package Aspose.PDF`）  
3. 已有一個 PDF 檔案（`input.pdf`）放在可讀寫的資料夾中  

就這樣。如果你對基本的 C# 語法感到熟悉，就可以直接開始。

---

## 步驟 1：載入 PDF 文件

首先，我們需要呼叫 **load pdf document**。Aspose.PDF 的 `Document` 類別接受檔案路徑，並將整個檔案讀入記憶體。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing;

// Load the source PDF
Document pdfDocument = new Document(@"C:\MyFiles\input.pdf");
```

*為什麼這很重要*：載入 PDF 後，你才能取得其頁面、元資料以及繪圖表面。沒有這一步，就無法放置任何圖形。

---

## 步驟 2：選取目標頁面

Aspose 中的 PDF 頁面編號是從 1 開始的，所以第一頁的索引為 1。取得你想要註解的頁面——通常為示範的第一頁。

```csharp
// Get the first page (pages are 1‑based)
Page targetPage = pdfDocument.Pages[1];
```

如果需要在其他頁面上操作，只要更改索引即可。記得先驗證該索引是否存在，以避免拋出 `ArgumentOutOfRangeException`。

---

## 步驟 3：定義矩形幾何

矩形由左下 (X,Y) 與右上 (X,Y) 座標決定。`Rectangle` 結構以 `LLX`、`LLY`、`URX`、`URY` 儲存這些值。

```csharp
// Define the rectangle (lower‑left X,Y and upper‑right X,Y)
Rectangle boundingRect = new Rectangle(100, 100, 300, 300);
```

隨意調整這些數字——`100,100` 代表左下角距離左邊與底部各 100 點，而 `300,300` 則是右上角距離邊緣 300 點。

---

## 步驟 4：驗證矩形是否在頁面內

若嘗試在頁面範圍外繪製，可能會被忽略或拋出例外，視套件版本而定。快速檢查可讓程式更健全。

```csharp
// Ensure the rectangle fits within the page dimensions
if (targetPage.PageInfo.Width >= boundingRect.URX &&
    targetPage.PageInfo.Height >= boundingRect.URY)
{
    // Rectangle is safe to add
}
else
{
    throw new InvalidOperationException("Rectangle exceeds page dimensions.");
}
```

*小技巧*：若要支援尺寸不同的 PDF，建議以頁面寬高的百分比來計算矩形，而非絕對點數。

---

## 步驟 5：加入黑色矩形註解

現在來到有趣的部分——**add black rectangle** 到頁面。Aspose 提供 `AddRectangle`，接受幾何資訊與 `Color`。我們使用 `Color.Black` 來 **create black rectangle**。

```csharp
// Add a black rectangle annotation to the page
targetPage.AddRectangle(boundingRect, Color.Black);
```

這一行完成了主要工作：建立註解物件、將邊框顏色設為黑色，並將其插入頁面的註解集合。

若日後需要不同的填色或邊框樣式，可使用接受 `Annotation` 物件的重載，進一步調整線寬、虛線樣式，甚至透明度。

---

## 步驟 6：儲存已修改的 PDF

最後，使用 **save modified pdf** 將變更寫回磁碟。你可以覆寫原檔或寫入新檔——此處示範產生輸出檔。

```csharp
// Save the updated PDF to a new location
pdfDocument.Save(@"C:\MyFiles\output.pdf");
```

完整流程就這樣。執行程式後開啟 `output.pdf`，即可看到你所定義的實心黑色矩形。

---

## 完整範例程式

以下是一個獨立的 Console 應用程式，將所有步驟整合在一起。將它貼到新的 `.csproj` 中，然後 **Run**。

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load PDF document
            Document pdfDocument = new Document(@"C:\MyFiles\input.pdf");

            // 2️⃣ Get the first page (pages are 1‑based)
            Page firstPage = pdfDocument.Pages[1];

            // 3️⃣ Define the rectangle geometry
            Rectangle rect = new Rectangle(100, 100, 300, 300);

            // 4️⃣ Verify bounds
            if (firstPage.PageInfo.Width < rect.URX || firstPage.PageInfo.Height < rect.URY)
            {
                Console.WriteLine("Rectangle does not fit on the page.");
                return;
            }

            // 5️⃣ Add a black rectangle annotation
            firstPage.AddRectangle(rect, Color.Black);

            // 6️⃣ Save modified PDF
            pdfDocument.Save(@"C:\MyFiles\output.pdf");

            Console.WriteLine("Successfully drew rectangle on PDF and saved the file.");
        }
    }
}
```

**預期的主控台輸出**：

```
Successfully drew rectangle on PDF and saved the file.
```

開啟 `output.pdf`，即可看到位於指定座標的黑色矩形。

---

## 常見變化處理

| 情境 | 需要變更的地方 | 原因 |
|-----------|----------------|-----|
| **多頁文件** | 在 `pdfDocument.Pages` 上迴圈，對每個 `Page` 物件套用相同邏輯。 | 可一次為整份文件批次加註解。 |
| **不同顏色** | 將 `Color.Black` 改為 `Color.Red` 或任意 `System.Drawing.Color`。 | 用於標示而非遮蔽。 |
| **透明填色** | 使用 `new Annotation(rect) { Color = Color.Black, Opacity = 0.5 }`。 | 產生半透明覆蓋層，而非實心方塊。 |
| **動態矩形大小** | 依照 `PageInfo.Width * 0.5` 等比例計算 `URX`、`URY`。 | 讓矩形能自動適應不同頁面尺寸。 |
| **錯誤處理** | 將整段程式碼包在 `try…catch`，並記錄 `Aspose.Pdf.IOException`。 | 防止來源檔案遺失或被鎖定時程式當機。 |

這些調整說明了如何在各種情境下 **create black rectangle** 註解，而不必重寫核心邏輯。

---

## 專業提示與常見陷阱

- **釋放 Document**：雖然 Aspose.PDF 實作了 `IDisposable`，但在短暫的 Console 應用中不一定需要 `using`。在長時間執行的服務中，建議使用 `using` 包住 `Document`，以即時釋放原生資源。  
- **座標系統**：PDF 的座標原點在左下角。若你習慣 WinForms 的左上原點，需要將 Y 軸反轉：`pageHeight - y`。  
- **效能**：對非常大的 PDF 加註解可能會佔用大量記憶體。考慮分批處理頁面，或改用 `PdfFileEditor` 進行較輕量的編輯。  
- **法律層面**：確保你有權限修改來源 PDF——有些文件受到編輯保護。

---

## 結論

我們已示範如何使用 C# **draw rectangle on PDF**：從 **load pdf document**、定義幾何、**add black rectangle**，最後 **save modified pdf**。此範例完整、可執行，且可依實際需求調整，例如批次處理或自訂樣式。

接下來，你可以探索加入其他註解類型（文字、標記）或在註解後合併多個 PDF。**load pdf document** 與 **save modified pdf** 的步驟保持不變，讓你能自信地擴充此模式。

有任何實作上的變化想分享嗎？歡迎在評論區留下你的想法，祝開發順利！

## 接下來該學什麼？

以下教學與本篇內容緊密相關，能進一步擴充你對 API 的掌握，並提供不同實作方式的完整範例與步驟說明。

- [Create Filled Rectangle Object in PDF using Java](/pdf/english/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)
- [Create Filled Rectangle Object In Pdf Using Java](/pdf/german/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)
- [Create Filled Rectangle Object In Pdf Using Java](/pdf/french/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}