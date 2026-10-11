---
category: general
date: 2026-10-10
description: 學習如何使用 Aspose.PDF 在 PDF 中加入矩形、繪製圖形，並儲存已修改的 PDF。包括逐步說明，教您存取特定的 PDF 頁面。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to PDF
- draw shape on PDF
- save modified PDF
- add shape to PDF
- access specific PDF page
language: zh-hant
lastmod: 2026-10-10
og_description: 使用 Aspose.PDF 於 C# 為 PDF 加入矩形。本教學示範如何在 PDF 上繪製形狀、存取特定 PDF 頁面，並儲存已修改的
  PDF。
og_image_alt: Screenshot of a PDF page with a blue rectangle overlay created by Aspose.PDF
og_title: 使用 Aspose.PDF 在 PDF 中加入矩形 – 完整 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  headline: How to add rectangle to PDF with Aspose.PDF in C#
  type: TechArticle
- description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  name: How to add rectangle to PDF with Aspose.PDF in C#
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: What if the PDF has only one page?
    text: Attempting to access `pdfDocument.Pages[1]` throws an `ArgumentOutOfRangeException`.
      Guard against this by checking `pdfDocument.Pages.Count` before indexing.
  - name: How to add multiple rectangles on different pages?
    text: Repeat Steps 2‑4 for each target page, adjusting the rectangle’s coordinates
      as needed. You can place the logic inside a loop that iterates over `pdfDocument.Pages`.
  - name: Can I use other shapes such as circles or polygons?
    text: Yes. Aspose.PDF provides `Ellipse`, `Polygon`, and `Polyline` classes that
      follow the same pattern as `Rectangle`. Replace the `new Aspose.Pdf.Drawing.Rectangle`
      call with the desired shape class.
  - name: Does the library support PDFs with rotated pages?
    text: Aspose.PDF automatically respects page rotation when rendering shapes. The
      rectangle’s coordinates are interpreted in the page’s native coordinate system,
      so no extra transformation is required.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: 如何在 C# 中使用 Aspose.PDF 向 PDF 添加矩形
url: /zh-hant/net/images-graphics/how-to-add-rectangle-to-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.PDF 向 PDF 添加矩形

如果您需要以程式方式 **add rectangle to PDF**（向 PDF 添加矩形），本指南將逐步說明。您將學會 **draw shape on PDF**（在 PDF 上繪製形狀）、定位特定頁面，並 **save modified PDF**（儲存已修改的 PDF）而不會出錯。

處理 PDF 文件是報表、發票或文件註釋的常見需求。完成本教學後，您即可自信地 **add shape to PDF**（向 PDF 添加形狀）文件、處理超出範圍的錯誤，並將此解決方案整合至任何 .NET 專案中。

## 前置條件

* .NET 6.0 SDK 或更新版本已安裝  
* Visual Studio 2022（或任何 C# IDE）  
* Aspose.PDF for .NET 授權或免費評估金鑰 – 兩種模式下 API 的使用方式相同  
* 一個名為 `input.pdf` 的 PDF 檔案，放置於可在程式碼中引用的資料夾內  

上述項目即為此範例唯一的外部相依性。

## 步驟 1：安裝 Aspose.PDF NuGet 套件

Aspose.PDF 函式庫提供您所需的 `Document`、`Rectangle` 以及其他繪圖類別。

```bash
dotnet add package Aspose.PDF
```

執行此指令會將最新穩定版的 Aspose.PDF 加入您的專案，使 PDF 類別可供編譯使用。

## 步驟 2：載入 PDF 文件

第一步是載入來源檔案，這會在記憶體中建立可供修改的表示。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;

class PdfRectangleExample
{
    static void Main()
    {
        // Load the PDF document from disk
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

*為何重要*：載入文件後，您即可存取其頁面集合，稍後需要 **access specific PDF page**（存取特定 PDF 頁面）時必須使用它。

## 步驟 3：存取第二頁（零基索引）

PDF 的頁面索引從 `0` 開始。若要在第二頁放置矩形，請取得索引為 `1` 的頁面。

```csharp
        // Access the second page (pages are zero‑based)
        var page = pdfDocument.Pages[1];
```

若文件少於兩頁，將拋出 `ArgumentOutOfRangeException`，提醒您在正式程式碼中需要加入防護判斷。

## 步驟 4：建立矩形形狀

使用 `Rectangle` 結構定義矩形的位置與大小，然後將其包裝於 Aspose 繪圖物件中。

```csharp
        // Define rectangle bounds: (x, y, width, height)
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            // Optional visual styling
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };
```

*為何重要*：`BorderInfo` 與 `FillColor` 屬性讓您 **draw shape on PDF**（在 PDF 上繪製形狀）時具備可見的輪廓與可選的填色，使矩形在讀者眼中更為突出。

## 步驟 5：將矩形加入頁面的段落集合

Aspose.PDF 將繪圖物件視為段落元素。將矩形加入頁面的 `Paragraphs` 集合即可在頁面上呈現。

```csharp
        // Add the rectangle shape to the page
        page.Paragraphs.Add(rectangleShape);
```

此時記憶體中的 PDF 文件已包含新形狀，但磁碟上的檔案仍未變更，必須儲存才會寫入。

## 步驟 6：儲存已修改的 PDF 並處理超出範圍的錯誤

呼叫 `Save` 會將更新後的文件寫入新檔案。若矩形超出頁面尺寸，Aspose 會拋出 `PdfException`。捕捉此例外即可整潔地回報問題。

```csharp
        try
        {
            // Save the altered PDF to a new file
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            // Handle shape that does not fit on the page
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

*為何重要*：`try/catch` 區塊確保您的應用程式能安全 **save modified PDF**（儲存已修改的 PDF），且錯誤訊息可協助您在需要時調整矩形座標。

## 完整範例程式

將所有步驟整合，以下是完整、可直接執行的程式碼：

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;
using System.Drawing; // Required for Color

class PdfRectangleExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // Step 2: Access the second page (zero‑based)
        var page = pdfDocument.Pages[1];

        // Step 3: Create a rectangle shape positioned at (100,100) with width 300 and height 200
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };

        // Step 4: Add the rectangle shape to the page's paragraph collection
        page.Paragraphs.Add(rectangleShape);

        // Step 5: Save the modified PDF, handling out‑of‑bounds cases
        try
        {
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

### 預期輸出

執行程式會輸出：

```
PDF saved successfully with rectangle added.
```

並產生 `output.pdf`，其內容為原始檔案加上在第二頁指定座標處的藍色矩形。

若矩形大於頁面尺寸，則會看到：

```
Shape out of bounds: The shape exceeds page margins.
```

## 常見問題與邊緣情況

### 如果 PDF 只有一頁怎麼辦？

嘗試存取 `pdfDocument.Pages[1]` 會拋出 `ArgumentOutOfRangeException`。可在索引前先檢查 `pdfDocument.Pages.Count` 以避免此問題。

```csharp
if (pdfDocument.Pages.Count < 2)
{
    Console.WriteLine("Document does not contain a second page.");
    return;
}
```

### 如何在不同頁面上加入多個矩形？

對每個目標頁面重複步驟 2‑4，並依需求調整矩形座標。您可以將此邏輯放入遍歷 `pdfDocument.Pages` 的迴圈中。

### 我可以使用其他形狀，例如圓形或多邊形嗎？

可以。Aspose.PDF 提供 `Ellipse`、`Polygon` 與 `Polyline` 類別，其使用方式與 `Rectangle` 相同。只需將 `new Aspose.Pdf.Drawing.Rectangle` 呼叫替換為相應的形狀類別即可。

### 此函式庫支援含有旋轉頁面的 PDF 嗎？

Aspose.PDF 會自動遵循頁面旋轉來繪製形狀。矩形的座標會依頁面的原生座標系統解讀，無需額外的轉換。

## 效能考量

* **Memory usage** – 載入大型 PDF（數百 MB）會佔用相應的記憶體。若僅需修改單一頁面，可考慮使用 `PdfFileInfo` 取出該頁面、進行修改後再合併回去。  
* **Batch processing** – 在大量文件上加入形狀時，重複使用單一 `License` 實例，以避免重複的授權驗證開銷。

## 後續步驟

現在您已能 **add rectangle to PDF**，可進一步探索以下相關主題：

* **draw shape on PDF** – 學習在 PDF 上覆蓋文字、影像與浮水印  
* **add shape to PDF** – 將多個形狀合併為單一註解層  
* **save modified PDF** – 使用串流（`MemoryStream`）直接從 Web API 回傳 PDF  
* **access specific PDF page** – 實作頁面範圍抽取以供自訂報表使用  

可嘗試不同的顏色、線條樣式與透明度，以符合您的品牌指引。

---

*祝程式開發順利！若本教學協助您 **add rectangle to PDF**，歡迎與同事分享或回饋改進至社群。*

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以步驟說明與完整範例程式碼協助您精通其他 API 功能，或在專案中探索替代實作方式。

- [如何在 C# 中使用 Aspose.PDF 向 PDF 添加形狀 – 步驟指南](/pdf/english/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [如何使用 Aspose.PDF for .NET 在 PDF 中加入線條物件 – 步驟指南](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [如何在 C# 中建立 PDF – 新增頁面、繪製矩形與儲存](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}