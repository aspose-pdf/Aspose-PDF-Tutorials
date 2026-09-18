---
category: general
date: 2026-02-12
description: 快速使用 C# 建立 PDF 文件：新增空白頁面、檢查頁面尺寸、繪製矩形，並儲存檔案。Aspose.Pdf 步驟說明指南。
draft: false
keywords:
- create pdf document c#
- add blank page pdf
- draw rectangle pdf
- save pdf file c#
- check pdf page size
language: zh-hant
og_description: 快速使用 C# 建立 PDF 文件：新增空白頁、檢查頁面尺寸、繪製矩形並儲存檔案。完整教學與程式碼。
og_title: 使用 C# 建立 PDF 文件 – 新增空白頁面並繪製矩形
tags:
- PDF
- C#
- Aspose.Pdf
- Document Generation
title: 建立 PDF 文件 C# – 新增空白頁面與繪製矩形
url: /zh-hant/net/document-creation/create-pdf-document-c-add-blank-page-draw-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 PDF 文件 C# – 新增空白頁面與繪製矩形

是否曾經需要從頭 **create PDF document C#** 並想知道如何新增空白頁面、驗證頁面尺寸、繪製圖形，最後儲存？你並不孤單。許多開發者在自動化報告、發票或任何可列印輸出時，都會碰到這個問題。

在本教學中，我們將逐步示範一個完整且可執行的範例，說明如何使用 Aspose.Pdf 函式庫 **add blank page PDF**、**check PDF page size**、**draw rectangle PDF**，以及 **save PDF file C#**。完成後，你將得到一個可直接使用的 PDF 檔案，內含一個藍色邊框的矩形，恰好位於 A4 大小的頁面上。

## 前置條件

- **.NET 6.0** 或更新版本（程式碼亦可在 .NET Framework 4.6+ 上執行）。
- **Aspose.Pdf for .NET** 已透過 NuGet 安裝（`Install-Package Aspose.Pdf`）。
- 具備基本的 C# 語法概念——不需要進階知識。
- 自行選擇的開發環境（Visual Studio、Rider、VS Code 等）。

> **專業提示：** 若你使用 Visual Studio，NuGet 套件管理員 UI 可讓加入 Aspose.Pdf 變得輕鬆——只要搜尋「Aspose.Pdf」並點擊 Install 即可。

## 步驟 1：建立 PDF 文件 C# – 初始化 Document

首先，你需要一個全新的 `Document` 物件。可將其視為空白畫布，之後的所有操作都會在其上繪製內容。

```csharp
using Aspose.Pdf;
using System;

// Step 1: Create a new PDF document
var pdfDocument = new Document();
```

> **為何重要：** `Document` 類別是所有 PDF 操作的入口。建立它會配置管理頁面、資源與中繼資料所需的內部結構。

## 步驟 2：新增空白頁面 PDF – 附加新頁面

沒有頁面的 PDF 就像一本沒有頁面的書——毫無意義。新增空白頁面即可提供可供繪製的畫布。

```csharp
// Step 2: Add a blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **背後發生了什麼？** `Pages.Add()` 會建立一個繼承預設尺寸（大多數設定為 A4）的頁面。若需要自訂尺寸，之後可再調整其尺寸。

## 步驟 3：定義矩形並檢查 PDF 頁面尺寸

在繪製之前，我們必須先定義矩形的放置位置，並確保它能容納於頁面內。這就是 **check PDF page size** 關鍵字發揮作用的地方。

```csharp
// Step 3: Define rectangle position and size (fits within a standard A4 page)
var rectangle = new Rectangle(50, 50, 550, 750);

// Step 3b: Verify that the rectangle fits inside the page boundaries
bool fitsWidth = page.PageInfo.Width >= rectangle.Width;
bool fitsHeight = page.PageInfo.Height >= rectangle.Height;

if (!fitsWidth || !fitsHeight)
{
    throw new InvalidOperationException(
        $"Rectangle (W:{rectangle.Width}, H:{rectangle.Height}) exceeds page size (W:{page.PageInfo.Width}, H:{page.PageInfo.Height}).");
}
```

> **為何要檢查：** 有些 PDF 可能使用自訂頁面尺寸（Letter、Legal 等）。若矩形大於頁面，繪製操作會被裁切或拋出錯誤。此檢查可讓程式在未來頁面尺寸變更時仍保持穩定。

## 步驟 4：繪製矩形 PDF – 呈現形狀

現在是有趣的部分：實際繪製一個藍色邊框、透明填充的矩形。這展示了 **draw rectangle PDF** 的功能。

```csharp
// Step 4: Draw the rectangle with a blue border and a transparent fill
page.AddRectangle(
    rectangle,
    Color.Blue,          // Border color
    Color.Transparent    // Fill color (transparent)
);
```

> **運作方式：** `AddRectangle` 接受三個參數——矩形幾何形狀、筆劃（邊框）顏色以及填充顏色。使用 `Color.Transparent` 可確保內部保持透明，讓底層內容得以顯示。

## 步驟 5：儲存 PDF 檔案 C# – 將文件寫入磁碟

最後，我們將文件寫入檔案。這就是 **save pdf file c#** 的步驟，完成整個流程。

```csharp
// Step 5: Save the PDF to a file
string outputPath = @"C:\Temp\shape.pdf"; // Adjust the path as needed
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved successfully to {outputPath}");
```

> **提示：** 將整個流程包在 `using` 區塊中（或呼叫 `pdfDocument.Dispose()`）以即時釋放原生資源，特別是在迴圈中大量產生 PDF 時。

## 完整、可執行範例

將所有部件組合起來，以下是完整程式碼，你可以直接複製貼上到 console 應用程式中：

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using (var pdfDocument = new Document())
        {
            // Add a blank page
            Page page = pdfDocument.Pages.Add();

            // Define rectangle (fits within a standard A4 page)
            var rectangle = new Rectangle(50, 50, 550, 750);

            // Ensure the rectangle fits inside the page boundaries
            if (page.PageInfo.Width >= rectangle.Width && page.PageInfo.Height >= rectangle.Height)
            {
                // Draw the rectangle with a blue border and a transparent fill
                page.AddRectangle(rectangle, Color.Blue, Color.Transparent);
            }
            else
            {
                Console.WriteLine("Rectangle does not fit on the page. Adjust dimensions.");
                return;
            }

            // Save the PDF to a file
            string outputPath = @"C:\Temp\shape.pdf"; // Change to your desired folder
            pdfDocument.Save(outputPath);
            Console.WriteLine($"PDF created at: {outputPath}");
        }
    }
}
```

### 預期結果

開啟 `shape.pdf` 後，你會看到一個單一的 A4 大小頁面，左側與底部各距 50 pts，呈現藍色邊框的矩形。矩形內部為透明，頁面背景仍可見。

![create pdf document c# 範例顯示矩形](https://example.com/placeholder.png "create pdf document c# 範例")

*(圖片替代文字：**create pdf document c# 範例顯示矩形**)  

如果將 `Color.Blue` 改為 `Color.Red` 或調整座標，矩形會相應變化——歡迎自行試驗。

## 常見問題與邊緣情況

### 如果需要不同的頁面尺寸？

你可以在加入內容之前設定頁面尺寸：

```csharp
Page customPage = pdfDocument.Pages.Add();
customPage.SetPageSize(PageSize.Letter.Width, PageSize.Letter.Height);
```

變更尺寸後，請記得重新執行 **check PDF page size** 的檢查邏輯。

### 我可以繪製其他形狀嗎？

當然可以。Aspose.Pdf 提供 `AddCircle`、`AddEllipse`、`AddLine`，甚至自由形狀的 `Path` 物件。使用相同的模式——先定義幾何形狀、驗證邊界，然後呼叫相對應的 `Add*` 方法。

### 如何為矩形填色？

將 `Color.Transparent` 替換為任意實色即可：

```csharp
page.AddRectangle(rectangle, Color.Blue, Color.LightGray);
```

### 有辦法在矩形內加入文字嗎？

當然可以。繪製矩形後，加入一個定位於矩形座標內的 `TextFragment`：

```csharp
var tf = new TextFragment("Hello, world!");
tf.Rect = new Rectangle(60, 60, 540, 730); // Slightly inset
page.Paragraphs.Add(tf);
```

## 結論

我們剛剛示範了如何 **create PDF document C#**、**add blank page PDF**、**check PDF page size**、**draw rectangle PDF**，以及最終的 **save PDF file C#**——全部以簡潔、端到端的範例呈現。程式碼已可直接執行，說明亦涵蓋每一步的 *原因*，讓你具備了進一步進行更複雜 PDF 產生工作的堅實基礎。

準備好接受下一個挑戰了嗎？試著疊加多個形狀、插入圖片，或產生表格——這些都遵循我們在此使用的相同模式。若日後需要調整頁面尺寸或改用其他 PDF 函式庫，概念仍然相同。

祝程式開發順利，願你的 PDF 總是如你所願正確呈現！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}