---
category: general
date: 2026-02-14
description: 快速使用 C# 建立 PDF 文件：在 PDF 中新增頁面、繪製矩形形狀，並使用 Aspose.Pdf 以幾行程式碼將 PDF 儲存至檔案。
draft: false
keywords:
- create pdf document c#
- add page to pdf
- how to draw rectangle
- add shape to pdf
- save pdf to file
language: zh-hant
og_description: 在幾分鐘內使用 C# 建立 PDF 文件。學習如何向 PDF 添加頁面、繪製矩形、加入圖形，並以清晰的程式碼範例將 PDF 儲存為檔案。
og_title: C# 建立 PDF 文件 – 步驟指南
tags:
- Aspose.Pdf
- C#
- PDF generation
title: 建立 PDF 文件 C# – 新增頁面、繪製矩形並儲存
url: /zh-hant/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/
---

.

I'll write final markdown.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 PDF 文件 C# – 新增頁面、繪製矩形與儲存

是否曾需要 **建立 PDF 文件 C#** 從頭開始，卻不知道從哪裡著手？你並不孤單——許多開發者在首次嘗試程式化產生 PDF 時，都會卡在同一個關卡。好消息是，只要幾行 Aspose.Pdf 程式碼，就能在 PDF 中新增頁面、繪製矩形，並 **將 PDF 儲存至檔案**，輕鬆完成。

在本教學中，我們會一步步說明：初始化 PDF、插入新頁面、繪製矩形形狀，最後將檔案寫入磁碟。完成後，你將得到一個可執行的 Console 應用程式，會在全新 PDF 頁面上產生一個藍色邊框的矩形。

## 需要的環境

- **.NET 6 或更新版本**（範例使用頂層語句，但任何近期的 .NET 版本皆可）
- **Aspose.Pdf for .NET** NuGet 套件  
  ```bash
  dotnet add package Aspose.Pdf
  ```
- 具有寫入權限的資料夾——教學會將檔案儲存至 `YOUR_DIRECTORY/shapes.pdf`。

不需要額外設定、XML，僅需純 C#。

## 建立 PDF 文件 C# – 概觀

第一步是建立一個 `Document` 物件。把它想成你的空白畫布，之後加入的所有頁面、文字、圖形，都會附著在這個實例上。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document (the canvas)
using var pdfDocument = new Document();
```

> **為什麼使用 `using var`？**  
> `Document` 類別實作了 `IDisposable`。將它包在 `using` 陳述式中，可確保所有非受控資源（檔案句柄、原生緩衝區）在使用完畢後立即釋放，這在長時間執行的服務中特別重要。

## 新增頁面至 PDF

沒有頁面的 PDF 就像一本沒有頁面的書——毫無用處。新增頁面只需要一次方法呼叫，同時會取得一個 `Page` 物件，之後可以進一步操作。

```csharp
// Step 2: Add a fresh page to the document
var pdfPage = pdfDocument.Pages.Add();
```

> **小技巧：** 新增的頁面會自動採用預設大小（A4）。如果需要自訂尺寸，可在加入任何內容前，設定 `pdfPage.PageInfo.Width` 與 `Height`。

## 如何繪製矩形

接下來是有趣的部分：繪製矩形。Aspose.Pdf 使用 `RectangleShape` 類別，需傳入一個 `Rectangle`（x、y、寬度、高度）來定義邊界。座標系統的原點位於頁面的左下角。

```csharp
// Step 3: Define the rectangle bounds (x, y, width, height)
// This will be validated – an exception is thrown if the rectangle is out of bounds
var rectangleBounds = new Rectangle(50, 50, 200, 150);
```

> **邊緣情況：** 若 `x + width` 超過頁面寬度，或 `y + height` 超過頁面高度，Aspose 會拋出 `ArgumentException`。請務必再次確認尺寸，特別是針對不同頁面大小產生 PDF 時。

## 將圖形加入 PDF

取得邊界後，我們建立圖形、設定藍色筆畫，然後將它加入頁面的段落集合中。

```csharp
// Step 4: Create a rectangle shape with a blue stroke and add it to the page
var rectangleShape = new RectangleShape(rectangleBounds)
{
    StrokeColor = Color.Blue,   // Outline color
    // FillColor = Color.LightGray, // Uncomment to add a fill
    // LineWidth = 2                // Adjust border thickness if needed
};
pdfPage.Paragraphs.Add(rectangleShape);
```

> **為什麼加入 `Paragraphs`？**  
> 在 Aspose.Pdf 中，視覺元素（如圖形）被視為「段落」，因為它們佔據頁面上的矩形區域。這樣的設計讓版面引擎在處理文字與圖形時保持一致。

## 儲存 PDF 至檔案

最後一步是將文件寫入磁碟。提供完整路徑後，Aspose 會自動處理壓縮、物件串流與交叉參照表等繁雜工作。

```csharp
// Step 5: Save the PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/shapes.pdf");
```

> **專業提示：** 若想將檔案放在執行檔旁邊，可使用 `Path.Combine(Environment.CurrentDirectory, "shapes.pdf")`；若需先建立資料夾，請先呼叫 `Directory.CreateDirectory`，以避免 `DirectoryNotFoundException`。

### 預期結果

使用任何 PDF 檢視器開啟 `shapes.pdf`。你應該會看到一張 A4 大小的單頁，頁面左側與下側各距 50 點的位置，有一個 **藍色邊框的矩形**，尺寸為 200 × 150 點。沒有文字，只有圖形——非常適合作為浮水印、表單欄位或視覺佔位符。

![PDF document with a blue rectangle created using create pdf document c#](https://example.com/images/pdf-rectangle.png "PDF document with a blue rectangle created using create pdf document c#")

*Alt text:* *PDF document with a blue rectangle created using create pdf document c#.*

## 完整範例程式

以下是可直接複製貼上的完整程式碼。它會編譯為 Console 應用程式（`dotnet new console`），除 NuGet 套件外不需其他設定。

```csharp
// Program.cs
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

using var pdfDocument = new Document();               // Create PDF document
var pdfPage = pdfDocument.Pages.Add();                // Add a page

// Define rectangle bounds (x, y, width, height)
// Aspose validates the rectangle – out‑of‑bounds throws an exception
var rectangleBounds = new Rectangle(50, 50, 200, 150);

// Create the rectangle shape (blue stroke) and add it to the page
var rectangleShape = new RectangleShape(rectangleBounds)
{
    StrokeColor = Color.Blue
};
pdfPage.Paragraphs.Add(rectangleShape);

// Save the document to disk
pdfDocument.Save("YOUR_DIRECTORY/shapes.pdf");

// Inform the user
Console.WriteLine("PDF created successfully at YOUR_DIRECTORY/shapes.pdf");
```

執行程式、開啟產生的檔案，即可看到圖形正好出現在我們定義的位置。

## 常見問題與注意事項

- **Q:** *如果需要填滿的矩形該怎麼做？*  
  **A:** 取消註解 `RectangleShape` 初始化子句中的 `FillColor` 行。Aspose 支援純色、漸層，甚至圖像填充。

- **Q:** *可以在同一頁面上繪製多個圖形嗎？*  
  **A:** 當然可以。只要再建立 `RectangleShape`、`Ellipse` 或 `Polygon` 物件，並分別加入 `pdfPage.Paragraphs` 即可。

- **Q:** *座標系統是否永遠是左下角為原點？*  
  **A:** 是的，Aspose 依照 PDF 規範，原點 (0,0) 位於左下角。若想使用左上角為原點，需要自行計算 `y = pageHeight - desiredY`。

- **Q:** *若目標資料夾不存在會發生什麼？*  
  **A:** `pdfDocument.Save` 會拋出 `DirectoryNotFoundException`。請先使用 `Directory.CreateDirectory` 建立資料夾。

## 往後的步驟

既然已掌握 **新增頁面至 PDF**、**繪製矩形**、**將圖形加入 PDF**，以及 **儲存 PDF 至檔案**，你可以在此基礎上擴展：

- 在圖形旁加入文字、圖片或表格。  
- 使用 `Graphics` 進行自由形狀繪製（線條、弧線、自訂路徑）。  
- 若有安全需求，可探索 PDF 加密或數位簽章。

上述主題皆直接建立在剛才的程式碼之上，盡情實驗吧。

---

**重點摘要：** 你剛剛學會了使用 Aspose.Pdf 完整的 **建立 PDF 文件 C#** 工作流程——初始化、加入頁面、繪製矩形形狀，最後將檔案寫入磁碟。這是製作發票、報表、證書或任何自動化文件的堅實基礎。祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}