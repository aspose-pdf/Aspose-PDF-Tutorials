---
category: general
date: 2026-09-12
description: 學習如何在 PDF 中加入透明度、在 PDF 上繪製矩形，並使用 Aspose.PDF 於 C# 保存具透明效果的 PDF – 步驟教學
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- draw rectangle on pdf
- save pdf with transparency
language: zh-hant
lastmod: 2026-09-12
og_description: 在 PDF 中加入透明度、於 PDF 上繪製矩形，並使用 Aspose.PDF 於 C# 中儲存具透明度的 PDF。請參考完整教學。
og_image_alt: Screenshot of a PDF page showing a semi‑transparent rectangle drawn
  with Aspose.PDF
og_title: 在 PDF 中加入透明度並繪製矩形 – 完整 C# 教學
schemas:
- author: Aspose
  dateModified: '2026-09-12'
  description: Learn how to add transparency to PDF, draw a rectangle on PDF, and
    save PDF with transparency using Aspose.PDF in C# – step‑by‑step guide.
  headline: How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: 如何在 PDF 中加入透明度並使用 Aspose.PDF 繪製矩形
url: /zh-hant/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 PDF 中加入透明度並繪製矩形（使用 Aspose.PDF）

如果您需要 **在 PDF 中加入透明度**，本指南將一步步示範如何在 C# 中完成此操作。您還會學會 **在 PDF 上繪製矩形**，以及最終 **儲存帶有透明度的 PDF**，讓結果可在報表、發票或任何文件自動化工作流程中重複使用。

在本教學中，您將會：

* 載入既有的 PDF 文件。
* 建立自訂的圖形狀態，定義筆畫與填充的不透明度。
* 將該圖形狀態套用到畫布並繪製矩形。
* 儲存已修改的檔案，同時保留透明度設定。

不需要額外工具，只要使用 Aspose.PDF for .NET 套件，且每一行程式碼都會說明其目的，讓您了解 *為何* 每個步驟很重要。

## 前置條件

* .NET 6.0 或更新版本（此程式碼亦相容 .NET Framework 4.7+）。
* 已授權或評估版的 **Aspose.PDF for .NET**。可透過 NuGet 安裝：

```bash
dotnet add package Aspose.Pdf
```

* 一個放置於專案可參考路徑的輸入 PDF（`input.pdf`）。

## 步驟 1：載入 PDF 文件

第一步是開啟來源檔案。使用 `using` 陳述式可確保文件正確釋放，避免之後儲存時產生檔案鎖定問題。

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";
using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

*為何重要*：載入文件後即可取得頁面集合、資源字典與畫布物件，這些都是繪圖所必需的。

## 步驟 2：存取第一頁的資源字典

每一頁 PDF 都有一個 **資源字典**，儲存字型、影像與圖形狀態等物件。要加入新的透明度設定，我們需要編輯 `ExtGState` 條目。

```csharp
// Step 2: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

*為何重要*：`DictionaryEditor` 讓我們在不破壞文件結構的前提下，讀取與修改低階 PDF 物件。

## 步驟 3：建立自訂圖形狀態並設定透明度

圖形狀態（`ExtGState`）控制繪圖操作的呈現方式。我們會定義兩個不透明度參數：

* **CA** – 筆畫不透明度（形狀的輪廓）。
* **ca** – 填充不透明度（形狀的內部）。

同時將混合模式（`BM`）設定為 “Normal”，這是最常見的合成方式。

```csharp
// Step 3: Create a custom graphics state (ExtGState) with transparency settings
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
var customGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "CA", new Aspose.Pdf.Cos.CosPdfNumber(1)),          // stroke opacity = 100 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),        // fill opacity = 50 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))      // normal blend mode
};

foreach (var p in parameters)
    customGs.Add(p);

// Register the new graphics state under the name "GS0"
extGStateDict.Add("GS0", customGs);
```

*為何重要*：將 `GS0` 加入 `ExtGState` 字典後，我們即可在畫布繪圖前啟用此可重複使用的參考。`0.5` 的填充不透明度讓矩形呈現半透明，達成 **在 PDF 中加入透明度** 的目標。

## 步驟 4：套用圖形狀態並繪製矩形

現在告訴頁面的畫布使用剛才建立的圖形狀態，接著繪製矩形。座標遵循 PDF 座標系統（原點位於左下角）。

```csharp
// Step 4: Apply the custom graphics state and draw a rectangle
var canvas = firstPage.Canvas;

// Activate the transparency graphics state
canvas.SetGraphicsState("GS0");

// Draw a rectangle from (100, 500) to (200, 600)
canvas.Rectangle(100, 500, 200, 600);

// Render the rectangle outline using the current graphics state
canvas.Stroke();
```

*為何重要*：`SetGraphicsState("GS0")` 會將繪圖上下文切換至先前定義的透明度設定。`Rectangle` 方法定義形狀，`Stroke` 以指定的不透明度繪製輪廓。若想同時填滿矩形，請將 `Stroke()` 改為 `FillAndStroke()`。

## 步驟 5：儲存已修改的 PDF 並保留透明度

最後，將文件寫回磁碟。輸出檔案會包含新的圖形狀態、繪製的矩形以及透明度資訊。

```csharp
// Step 5: Save the modified PDF
string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
pdfDocument.Save(outputPath);
```

*為何重要*：儲存文件即完成所有變更。產生的檔案可在任何 PDF 閱讀器開啟，矩形將以 50 % 填充不透明度顯示。

### 預期結果

開啟 `output_with_extgstate.pdf` 後，您應該會看到一個邊框完全不透明、內部半透明的矩形，底下的頁面內容得以透過顯示。

## 邊緣情況與實務技巧

| 情境 | 建議調整 |
|-----------|------------------------|
| **多頁文件** | 迴圈 `pdfDocument.Pages`，對每個目標頁面重複步驟 2‑4。 |
| **不同的不透明度數值** | 將 `CosPdfNumber` 的 `CA`（筆畫）與 `ca`（填充）改為 0（完全透明）至 1（完全不透明）之間的任意數值。 |
| **自訂混合模式** | 將 `"Normal"` 替換為 `"Multiply"`、`"Screen"` 或任何 PDF 標準支援的混合模式。 |
| **填滿矩形** | 呼叫 `canvas.FillAndStroke()` 取代 `canvas.Stroke()`，同時套用填充與輪廓。 |
| **重複使用同一圖形狀態** | 在同一頁面上繪製任意數量的圖形前，都可先呼叫 `canvas.SetGraphicsState("GS0")`。 |

**小技巧**：在加入新 `ExtGState` 後，務必檢查資源字典是否已存在；若不存在，請先建立：

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
    resourcesEditor.Add("ExtGState", new Aspose.Pdf.Cos.CosPdfDictionary(pdfDocument));
```

## 完整可執行範例

以下是一個獨立的程式範例，您可以直接貼到 Console 應用程式中執行（將 `YOUR_DIRECTORY` 替換為實際路徑）。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF document
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Access the first page’s resources
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        if (!resourcesEditor.ContainsKey("ExtGState"))
            resourcesEditor.Add("ExtGState", new CosPdfDictionary(pdfDocument));

        // 3️⃣ Create a custom graphics state with transparency
        var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        var customGs = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };

        foreach (var p in parameters)
            customGs.Add(p);

        extGStateDict.Add("GS0", customGs);

        // 4️⃣ Apply the graphics state and draw a rectangle
        var canvas = firstPage.Canvas;
        canvas.SetGraphicsState("GS0");
        canvas.Rectangle(100, 500, 200, 600);
        canvas.Stroke(); // use FillAndStroke() for a filled shape

        // 5️⃣ Save the PDF with transparency
        string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine("PDF saved with a transparent rectangle at: " + outputPath);
    }
}
```

執行程式後會產生 `output_with_extgstate.pdf`，示範 **在 PDF 中加入透明度**、**繪製矩形** 以及 **儲存帶透明度的 PDF** 的完整流程。

## 結論

現在您已掌握如何使用 Aspose.PDF for .NET **在 PDF 中加入透明度**、**繪製矩形**，以及 **儲存帶透明度的 PDF**。此流程核心在於建立自訂 `ExtGState`、將其套用至畫布，最後寫入檔案。憑藉這些基礎，您可以將技巧擴展至其他圖形、多頁文件，或動態調整不透明度。

**後續建議**

* 探索其他繪圖基元，如 `canvas.Ellipse`、`canvas.Path` 或 `canvas.TextFragment`，同時重複使用相同的圖形狀態。
* 結合透明度與影像覆蓋，製作浮水印（`canvas.Image` + 自訂 `ExtGState`）。
* 參考 Aspose.PDF 文件中關於 **graphics state parameters** 的說明，深入了解進階合成效果。

祝開發順利，盡情享受透明度為 PDF 工作流程帶來的視覺彈性！

## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步擴展您所學的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，並在專案中探索其他實作方式。

- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [How to Add a Line Object in PDF Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Add Image Stamps to PDFs Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}