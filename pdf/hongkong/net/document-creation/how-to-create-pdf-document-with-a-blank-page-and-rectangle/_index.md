---
category: general
date: 2026-09-05
description: 在 C# 中建立 PDF 文件，新增空白頁、繪製矩形，並儲存 PDF 檔案。請遵循 Aspose.PDF 的逐步範例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add blank page pdf
- draw rectangle pdf
- save pdf file
- how to add rectangle
language: zh-hant
lastmod: 2026-09-05
og_description: 在 C# 中建立 PDF 文件，新增空白頁、繪製矩形，並儲存 PDF 檔案。請參考使用 Aspose.PDF 的完整範例。
og_image_alt: Screenshot showing a PDF document with a drawn rectangle on a blank
  page
og_title: 使用 C# 建立包含空白頁與矩形的 PDF 文件 – 指南
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  headline: How to create PDF document with a blank page and rectangle
  type: TechArticle
- description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  name: How to create PDF document with a blank page and rectangle
  steps:
  - name: 'Edge case: custom page size'
    text: 'If your layout requires a 6 × 9 inch page, replace the default call with:'
  - name: 'Pro tip: styling the rectangle'
    text: 'You can change the stroke color and line width:'
  - name: 'Edge case: overwriting existing files'
    text: 'Aspose.PDF overwrites an existing file by default. To protect previous
      outputs, check for file existence first:'
  - name: Expected output
    text: Running the program creates a single‑page PDF. When you open `output.pdf`
      you will see a blank white page with a red rectangle positioned 100 points from
      the left and bottom edges, measuring 200 × 200 points.
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
- PDF generation
title: 如何建立包含空白頁與矩形的 PDF 文件
url: /zh-hant/net/document-creation/how-to-create-pdf-document-with-a-blank-page-and-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 PDF 文件中建立空白頁面與矩形

如果您需要以程式方式 **create PDF document**，本指南提供了完整的 C# 解決方案。您將學習如何新增空白頁面、在該頁面上繪製矩形，最後儲存 PDF 檔案。範例使用 Aspose.PDF 函式庫，支援 .NET 6+ 與 .NET Framework 4.5+。

在發票、證書或自訂報表中，新增空白頁面並繪製圖形是常見需求。完成本教學後，您將擁有一個可執行的專案，產生的 PDF 會包含一個位於 (100, 100) 且尺寸為 200 × 200 點的單一矩形。

## 前置條件

開始之前，請確保您已具備：

* Visual Studio 2022（或任何 C# IDE）
* .NET 6 SDK 或 .NET Framework 4.5+
* Aspose.PDF for .NET NuGet 套件  
  ```bash
  dotnet add package Aspose.PDF
  ```
* 對輸出目錄的寫入權限

不需要額外的設定；程式碼可直接執行。

## 建立 PDF 文件 – 概觀

整個流程分為四個邏輯步驟：

1. **Instantiate** `Document` 物件 – 代表 PDF 檔案本身。  
2. **Add a blank page** – 為繪圖提供畫布。  
3. **Draw a rectangle** – 使用 `Path` 物件定義形狀。  
4. **Save the PDF file** – 將文件寫入磁碟。

每個步驟皆獨立於各自的章節，方便您依需求重複使用或替換。

![Diagram of a PDF with a rectangle on a blank page](https://example.com/placeholder-image.png){.img-fluid alt="顯示在空白頁面上繪製矩形的 PDF 文件截圖"}

## 新增空白頁面 PDF

在放置任何圖形之前，PDF 必須至少包含一個頁面。`Pages.Add()` 方法會以預設尺寸（A4）建立空白頁面。若需其他尺寸，請傳入 `PageSize` 參數。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();

// Step 2: Add a blank page to the document
Page pdfPage = pdfDocument.Pages.Add();   // adds an A4 page by default
```

*Why this step matters* – 頁面物件保存了文字、影像與向量圖形的集合。若沒有頁面，任何嘗試加入矩形的操作都會拋出例外。

### 邊緣情況：自訂頁面大小

如果您的版面需要 6 × 9 英吋的頁面，請改用以下呼叫：

```csharp
var pageSize = new Size(432, 648); // 72 points per inch
Page pdfPage = pdfDocument.Pages.Add(pageSize);
```

## 繪製矩形 PDF

繪製矩形只需要建立 `Rectangle` 幾何形狀，並將其包裹在 `Path` 中。`ValidateBounds()` 呼叫可確保形狀位於頁面邊界內，避免被裁切。

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

// Step 4: Add the rectangle to the page contents
Path rectanglePath = new Path(shapeRect).ValidateBounds();
pdfPage.Contents.Add(rectanglePath);
```

*Why this step matters* – `Path` 物件是 Aspose.PDF 使用的低階向量基元。透過驗證邊界，可避免矩形超出頁面限制而產生執行時錯誤。

### 專業提示：樣式化矩形

您可以變更筆畫顏色與線寬：

```csharp
rectanglePath.GraphInfo = new GraphInfo
{
    StrokeColor = Color.Red,
    LineWidth = 2
};
```

這會產生一條紅色輪廓，線寬為 2 點。

## 儲存 PDF 檔案

將文件持久化即完成磁碟上的檔案寫入。`Save` 方法接受檔案路徑或串流。使用絕對路徑可明確指定位置，對自動化腳本特別有用。

```csharp
// Step 5: Save the PDF to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

*Why this step matters* – 儲存是唯一將記憶體中的表示轉換為實體檔案的時機。若需從 Web API 回傳 PDF，請將檔案路徑改為 `MemoryStream`。

### 邊緣情況：覆寫已存在的檔案

Aspose.PDF 會預設覆寫已存在的檔案。為保護先前的輸出，請先檢查檔案是否存在：

```csharp
if (File.Exists(outputPath))
{
    File.Delete(outputPath);
}
pdfDocument.Save(outputPath);
```

## 如何新增矩形 – 最佳實踐

* **Keep coordinates within the page margins** – 使用 `ValidateBounds()` 或自行計算邊距。  
* **Reuse `GraphInfo` objects** 於繪製多個圖形時，可減少記憶體分配。  
* **Dispose of the `Document` object**（如 `using var` 所示）以即時釋放原生資源。  
* **Test with different DPI settings** 若稍後嵌入點陣圖，向量圖形（如矩形）在任何解析度下皆保持清晰。

## 完整可執行範例

以下是完整程式碼，您可直接貼到 Console 應用程式中。編譯後即可在專案資料夾產生 `output.pdf`。

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using var pdfDocument = new Document();

        // Add a blank page to the document
        Page pdfPage = pdfDocument.Pages.Add();

        // Define a rectangle shape (x, y, width, height)
        Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

        // Create a path for the rectangle and validate its bounds
        Path rectanglePath = new Path(shapeRect).ValidateBounds();

        // Optional: style the rectangle (red outline, 2‑pt width)
        rectanglePath.GraphInfo = new GraphInfo
        {
            StrokeColor = Color.Red,
            LineWidth = 2
        };

        // Add the rectangle to the page contents
        pdfPage.Contents.Add(rectanglePath);

        // Determine output path
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");

        // Ensure no leftover file blocks the save operation
        if (File.Exists(outputPath))
        {
            File.Delete(outputPath);
        }

        // Save the PDF to a file
        pdfDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

### 預期輸出

執行程式會產生單頁 PDF。開啟 `output.pdf` 後，您會看到一張白色空白頁，左側與下側各距 100 點的位置有一個紅色矩形，尺寸為 200 × 200 點。

## 結論

您現在已掌握如何使用 Aspose.PDF 在 C# 中 **create PDF document**、**add blank page pdf**、**draw rectangle pdf**，以及 **save pdf file**。本範例說明了關鍵 API 呼叫、每一步的必要性，並提供自訂頁面大小或矩形樣式等常見變化的技巧。

接下來，您可以探索 **adding text**、**embedding images** 或 **creating multi‑page reports** 等相關主題。相同的模式——實例化 `Document`、操作頁面、加入向量或點陣內容，最後 `Save`——適用於所有情境。歡迎嘗試不同的形狀、顏色與版面配置，以符合您的專案需求。

## 接下來該學什麼？

以下教學與本指南所示技巧緊密相關，能進一步深化您的能力。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，並在專案中探索替代實作方式。

- [建立 PDF 文件 C# – 新增頁面、繪製矩形與儲存](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)
- [使用 Aspose.PDF 建立 PDF 文件 – 步驟說明指南](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [使用 Aspose 建立 PDF 文件 – 新增頁面、文字方塊與表單](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}