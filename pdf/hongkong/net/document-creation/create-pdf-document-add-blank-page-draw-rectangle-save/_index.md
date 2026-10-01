---
category: general
date: 2026-03-01
description: 使用 C# 的 Aspose.PDF 建立 PDF 文件。了解如何新增空白頁、繪製矩形 PDF 形狀，並快速儲存 PDF 檔案。
draft: false
keywords:
- create pdf document
- add blank page
- draw rectangle pdf
- add rectangle pdf
- save pdf file
language: zh-hant
og_description: 使用 Aspose.PDF 建立 PDF 文件。逐步指南教您新增空白頁、繪製矩形 PDF，並有效率地儲存 PDF 檔案。
og_title: 建立 PDF 文件 – 新增空白頁、繪製矩形並儲存
tags:
- pdf
- csharp
- aspose
- document-generation
title: 建立 PDF 文件 – 新增空白頁、繪製矩形並儲存
url: /zh-hant/net/document-creation/create-pdf-document-add-blank-page-draw-rectangle-save/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 PDF 文件 – 新增空白頁面、繪製矩形並儲存

有沒有曾經需要在 C# 中 **建立 PDF 文件**，卻不知從何入手？你並非唯一遇到這種情況的開發者——許多程式設計師在首次自動化報表產生時都會卡關。好消息是，使用 Aspose.PDF 只需幾行程式碼，就能產生 PDF、加入空白頁面、繪製矩形形狀，最後儲存 PDF 檔案。

在本教學中，我們會一步步說明每個呼叫的 **原因**，並提供可直接執行的程式碼範例。完成後，你將會知道如何 **add blank page**、**draw rectangle PDF**，以及 **save PDF file**，不必再翻閱大量文件。

## 前置條件

- .NET 6.0 或更新版本（任何近期的執行環境皆可）
- Aspose.PDF for .NET NuGet 套件（`Install-Package Aspose.PDF`）
- 基本的 C# 語法概念（不需要進階技巧）

如果你已經具備上述條件，太好了——讓我們馬上開始。

## 步驟 1 – 建立 PDF 文件

第一件事就是實例化 `Document` 類別。可以把它想像成打開一本全新的筆記本，之後加入的每一頁都會寫在裡面。

```csharp
using Aspose.Pdf;

// Step 1: Create a new PDF document
var pdfDocument = new Document();
```

> **Why this matters:** `Document` 是根物件；沒有它就無法新增頁面或圖形。建立文件同時會配置 Aspose 內部所需的結構，以有效管理資源。

## 步驟 2 – 新增空白頁面

沒有頁面的 PDF 就像一本沒有頁面的書——毫無用處。加入 **blank page** 後，你就有了可以繪圖的畫布。

```csharp
// Step 2: Add a blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **Pro tip:** `Add()` 方法會回傳新建立的 `Page` 物件，這樣就可以直接串接後續操作，而不必再額外查找。

## 步驟 3 – 定義矩形形狀

現在我們指定矩形的座標。Aspose 使用的座標系統是以頁面左下角 (0,0) 為原點。

```csharp
// Step 3: Define a rectangle shape (left, bottom, right, top)
Rectangle rectangle = new Rectangle(50, 50, 550, 800);
```

> **What the numbers mean:**  
> - **左側** = 從左邊緣起算 50 點  
> - **底部** = 從底部邊緣起算 50 點  
> - **右側** = 從左邊緣起算 550 點（寬度約 500）  
> - **上側** = 從底部邊緣起算 800 點（高度約 750）

如果把它想像成標準 A4 大小的頁面，矩形會舒適地置於中間，四周都有適當的邊距。

![顯示 PDF 頁面內矩形的示意圖](image-placeholder.png){: .align-center alt="建立 PDF 文件矩形範例"}

## 步驟 4 – 驗證矩形是否適合頁面

在繪製之前，先確認形狀是否仍在頁面範圍內。這可以避免執行時例外，並保持版面整齊。

```csharp
// Step 4: Verify the rectangle fits inside the page boundaries
if (page.IsInside(rectangle))
{
    // Continue only if the rectangle is fully inside the page
}
else
{
    throw new InvalidOperationException("Rectangle exceeds page bounds.");
}
```

> **Edge case:** 若之後改用自訂頁面尺寸，此檢查會自動適應，避免出現莫名其妙的裁切錯誤。

## 步驟 5 – 在 PDF 中繪製矩形

完成驗證後，我們即可使用藍色輪廓 **draw rectangle PDF**。Aspose 允許直接傳入 `Color`，呼叫相當簡潔。

```csharp
// Step 5: Draw the rectangle on the page using a blue outline
page.AddRectangle(rectangle, Color.Blue);
```

> **Why a blue outline?** 這只是一個清晰的示範用顏色。你可以將 `Color.Blue` 換成任何想要的 `Color`，甚至使用 `page.AddRectangle(rectangle, Color.Blue, Color.LightGray)` 來填充形狀。

## 步驟 6 – 儲存 PDF 檔案

最後一步是將文件寫入磁碟。這裡就是 **save PDF file** 的動作發生的地方。

```csharp
// Step 6: Save the PDF to a file
pdfDocument.Save(@"C:\Temp\shape.pdf");
```

> **Tip:** 測試時使用絕對路徑較為安全，部署到 Web 或雲端環境時再改為相對路徑或串流。

### 完整範例程式

以下是完整、可直接執行的程式碼：

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Graphics; // Needed for Color

class Program
{
    static void Main()
    {
        // 1️⃣ Create PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Add a blank page
        Page page = pdfDocument.Pages.Add();

        // 3️⃣ Define rectangle (left, bottom, right, top)
        Rectangle rectangle = new Rectangle(50, 50, 550, 800);

        // 4️⃣ Verify it fits inside the page
        if (!page.IsInside(rectangle))
        {
            Console.WriteLine("Rectangle does not fit the page.");
            return;
        }

        // 5️⃣ Draw rectangle with a blue outline
        page.AddRectangle(rectangle, Color.Blue);

        // 6️⃣ Save PDF file
        pdfDocument.Save(@"C:\Temp\shape.pdf");

        Console.WriteLine("PDF created successfully at C:\\Temp\\shape.pdf");
    }
}
```

**Expected result:** 開啟 `shape.pdf` 後，你會看到單一頁面，中央有一個藍色邊框的矩形，左側與底部各保留 50 點的邊距，右側與上側亦同。

## 常見問題與變化

### 如果我需要 **add rectangle PDF** 並填充顏色該怎麼辦？

將 `AddRectangle` 呼叫換成接受填充顏色的重載：

```csharp
page.AddRectangle(rectangle, Color.Blue, Color.LightYellow);
```

### 我可以多次 **add blank page** 嗎？

當然可以。只要多次呼叫 `pdfDocument.Pages.Add()`，每次都會回傳一個新的 `Page` 物件，讓你分別操作。

### 在繪製之前，我要如何變更頁面尺寸？

建立頁面時設定 `PageSize` 屬性：

```csharp
Page page = pdfDocument.Pages.Add();
page.PageInfo.Width = 595;   // A4 width in points
page.PageInfo.Height = 842;  // A4 height in points
```

變更尺寸後，請記得再次執行邊界檢查 (`IsInside`)。

### 有沒有辦法將 **save PDF file** 儲存至記憶體串流以供網頁回應使用？

可以——將檔案路徑改為 `MemoryStream`：

```csharp
using var ms = new MemoryStream();
pdfDocument.Save(ms);
byte[] pdfBytes = ms.ToArray(); // send this over HTTP
```

## 結論

我們剛剛示範了如何使用 Aspose.PDF for .NET **create PDF document**、**add blank page**、**draw rectangle PDF**、**add rectangle PDF**，最後 **save PDF file**。步驟刻意保持簡潔，讓你可以直接 copy‑paste、執行並立即看到結果。

接下來，你可以嘗試在同一頁加入文字、圖片，甚至表格——每個動作都遵循「建立 → 新增 → 驗證 → 繪製 → 儲存」的模式。盡情玩弄不同的顏色、線寬或頁面方向，讓 PDF 完全符合你的需求。

如果遇到任何問題，請再次確認 Aspose.PDF NuGet 套件與目標框架相符，並確保輸出資料夾在呼叫 `Save` 前已存在。祝你 PDF 開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}