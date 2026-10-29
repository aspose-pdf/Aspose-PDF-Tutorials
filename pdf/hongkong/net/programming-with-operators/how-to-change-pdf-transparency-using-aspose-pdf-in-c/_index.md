---
category: general
date: 2026-10-04
description: 學習如何在 C# 中使用 Aspose.Pdf 更改 PDF 透明度。此逐步指南會新增自訂圖形狀態，以調整不透明度和混合模式。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.Pdf graphics state
- PDF opacity C#
- ExtGState dictionary
- blend mode PDF
language: zh-hant
lastmod: 2026-10-04
og_description: 使用 Aspose.Pdf 在 C# 中更改 PDF 透明度。請參考此簡潔教學，修改 PDF 的不透明度、混合模式及圖形狀態。
og_image_alt: Screenshot of a PDF page before and after changing transparency with
  Aspose.Pdf
og_title: 使用 Aspose.Pdf 變更 PDF 透明度 – 完整 C# 教學
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to change PDF transparency with Aspose.Pdf in C#. This step‑by‑step
    guide adds a custom graphics state to adjust opacity and blend mode.
  headline: How to change PDF transparency using Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- graphics state
title: 如何在 C# 中使用 Aspose.Pdf 更改 PDF 透明度
url: /zh-hant/net/programming-with-operators/how-to-change-pdf-transparency-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.Pdf 更改 PDF 透明度

如果您需要在 .NET 專案中 **更改 PDF 透明度**，本教學將一步步示範如何使用 Aspose.Pdf 完成。完成教學後，您將得到一個 PDF，選定的物件會使用自訂的不透明度與混合模式，且不需任何外部工具。

處理 PDF 不透明度是製作浮水印、覆蓋圖形或細膩視覺效果的常見需求。以下步驟涵蓋從載入文件、編輯 **ExtGState 字典**、建立新圖形狀態，到儲存結果的全部流程。

## 前置條件

開始之前，請確保您已具備：

* **Aspose.Pdf for .NET**（版本 23.12 或更新）。可透過 NuGet 安裝：

```bash
dotnet add package Aspose.Pdf
```

* .NET 開發環境（Visual Studio、VS Code，或 `dotnet` CLI）。
* 位於已知目錄的輸入 PDF 檔（範例使用 `input.pdf`）。

不需要其他額外函式庫。

## 步驟 1：載入 PDF 文件

首先打開既有的 PDF。使用 `using` 區塊可確保檔案句柄自動釋放。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Tools;

// ...

using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

*為什麼這很重要*：載入文件會在記憶體中建立可供修改的表示。`Document` 類別同時提供對低階 COS 物件的存取，這對變更 PDF 透明度至關重要。

## 步驟 2：取得第一頁的資源

圖形狀態儲存在頁面的資源字典中。我們取得第一頁，並以 `DictionaryEditor` 包裝其資源，以便於編輯。

```csharp
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*說明*：`DictionaryEditor` 抽象了 COS 字典的操作，讓您能像讀寫 `ExtGState` 這類條目，而不必直接處理原始 PDF 語法。

## 步驟 3：取得（或建立）ExtGState 字典

**ExtGState 字典**保存具名的圖形狀態物件。若已存在則直接使用；若不存在則建立新字典。

```csharp
CosPdfDictionary extGStateDict;

// Try to fetch an existing ExtGState entry
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a fresh ExtGState dictionary and add it to the resources
    extGStateDict = new CosPdfDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*為什麼要這麼做*：若沒有 `ExtGState` 條目，PDF 引擎就找不到自訂的不透明度設定。加入字典後，頁面即可識別您定義的任何新圖形狀態。

## 步驟 4：定義具有不透明度與混合模式的新圖形狀態

圖形狀態是一組 PDF 繪製參數。我們在此設定：

* **CA** – 線條不透明度（1 = 完全不透明）
* **ca** – 填充不透明度（0.5 = 50 % 透明）
* **BM** – 混合模式（預設為 `Normal`，您也可以嘗試 `Multiply`、`Screen` 等）

```csharp
// Create an empty dictionary that will become the new graphics state
var graphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Prepare the entries
var graphicsStateEntries = new KeyValuePair<string, ICosPdfPrimitive>[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // blend mode
};

// Populate the dictionary
foreach (var entry in graphicsStateEntries)
{
    graphicsState.Add(entry);
}
```

*洞見*：`CosPdfNumber` 的值是 0 到 1 之間的浮點數。調整它們即可微調線條與填充的透明程度。混合模式決定透明內容如何與底層圖形交互。

## 步驟 5：在 ExtGState 中註冊圖形狀態

我們為新狀態命名（`GS0`）。之後在內容串流中繪製物件時，只要引用此名稱即可。

```csharp
extGStateDict.Add("GS0", graphicsState); // "GS0" becomes the identifier you’ll use later
```

*最佳實踐*：使用清晰的命名規則（如 `GS0`、`GS_Watermark` 等），以免在管理多個狀態時產生混淆。

## 步驟 6：將圖形狀態套用至頁面內容（可選）

若要將新不透明度套用到既有頁面元素，需要修改頁面的內容串流。以下範例在頁面上方加入一個半透明矩形。

```csharp
// Build a content stream that sets the graphics state and draws a rectangle
var contentBuilder = new Aspose.Pdf.Operators.ContentBuilder(pdfDocument);
contentBuilder.SetGraphicsState("GS0");
contentBuilder.SetFillColor(Color.FromRgb(255, 0, 0)); // red fill
contentBuilder.Rectangle(100, 500, 200, 100); // x, y, width, height
contentBuilder.FillPath();

firstPage.Contents.Add(contentBuilder);
```

*為什麼會有效*：`SetGraphicsState` 運算子告訴 PDF 直譯器，之後的所有繪製指令都使用 `GS0` 中定義的參數。因此矩形的填充呈現 50 % 透明，而邊框則保持完全不透明。

## 步驟 7：儲存已修改的 PDF

最後，將變更寫回磁碟。

```csharp
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

產生的 `output.pdf` 包含新的圖形狀態，任何引用 `GS0` 的內容都會以設定的透明度呈現。

---

![顯示 PDF 透明度變更的示意圖](/images/pdf-transparency-before-after.png "套用自訂圖形狀態前後的 PDF 頁面")
*圖片替代文字（供 SEO 與無障礙使用）：* **變更 PDF 透明度範例 – 原始與修改後的頁面**

## 完整範例程式

將上述所有步驟整合，以下是一個可直接執行的程式，會變更 PDF 透明度並加入半透明矩形。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Tools;
using System.Collections.Generic;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Drawing;

class ChangePdfTransparency
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            CosPdfDictionary extGStateDict;
            if (resourcesEditor.ContainsKey("ExtGState"))
                extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
            else
            {
                extGStateDict = new CosPdfDictionary(pdfDocument);
                resourcesEditor["ExtGState"] = extGStateDict;
            }

            // Create a new graphics state (opacity + blend mode)
            var graphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var e in entries) graphicsState.Add(e);

            // Register the graphics state as GS0
            extGStateDict.Add("GS0", graphicsState);

            // OPTIONAL: draw a semi‑transparent rectangle using GS0
            var builder = new ContentBuilder(pdfDocument);
            builder.SetGraphicsState("GS0");
            builder.SetFillColor(Color.FromRgb(255, 0, 0)); // red
            builder.Rectangle(100, 500, 200, 100);
            builder.FillPath();
            firstPage.Contents.Add(builder);

            // Save the result
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF transparency changed and saved to output.pdf");
    }
}
```

### 預期輸出

* 會在指定資料夾產生 `output.pdf`。
* 開啟 PDF 後，您會看到一個紅色矩形，其填充為 50 % 透明，邊框則保持完全不透明。
* 任何其他引用 `GS0` 的物件（例如浮水印）也會繼承相同的不透明度與混合模式。

## 常見問題與邊緣案例處理

| 問題 | 解答 |
|----------|--------|
| **我只能更改線條不透明度嗎？** | 將 `CA` 設為所需值，並將 `ca` 保持為 `1`。 |
| **支援哪些混合模式？** | 所有標準 PDF 混合模式（`Normal`、`Multiply`、`Screen`、`Overlay` 等）皆可透過 `BM` 條目設定。 |
| **需要在使用後清理字典嗎？** | 不需要。`CosPdfDictionary` 物件由 Aspose.Pdf 管理，呼叫 `Save` 時會自動寫入檔案。 |
| **加密的 PDF 能這樣操作嗎？** | 使用正確的密碼載入文件（`new Document(path, password)`）。文件在記憶體中解密後，圖形狀態的操作方式相同。 |
| **可以將相同的圖形狀態套用到多個頁面嗎？** | 可以。將 `GS0` 條目加入每一頁的 `ExtGState` 字典，或在文件的全域資源中建立單一共享字典，然後在各頁引用。 |

## 小技巧與最佳實踐

* **專業提示**：圖形狀態名稱保持簡短且具描述性（如 `GS_Watermark`、`GS_Overlay`），可避免名稱衝突並提升除錯效率。
* **注意**：避免不小心覆寫已存在的 `ExtGState` 條目。建立新字典前，務必先檢查 `resourcesEditor.ContainsKey("ExtGState")`。
* **效能說明**：修改低階 COS 物件速度很快，但若需處理上千頁，建議批次執行變更以降低記憶體壓力。

## 往後的步驟

既然您已掌握 **變更 PDF 透明度** 的方法，接下來可以探索以下相關主題：

* 使用自訂不透明度加入 **浮水印**（`PDF opacity C#`）。
* 使用 **不同混合模式** 產生藝術效果（`blend mode PDF`）。
* 建立可重複使用的 **圖形狀態庫**，用於大規模文件產生（`Aspose.Pdf graphics state`）。

嘗試調整 `ca` 與 `CA` 的數值，或將紅色矩形換成圖片或文字覆蓋。原理相同——只要在繪製新內容前引用 `GS0` 圖形狀態即可。

---

*您已學會如何在 C# 中使用 Aspose.Pdf 變更 PDF 透明度。將此技巧應用於報表、發票或任何需要細緻視覺呈現的 PDF 輸出，提升專業度。*

## 接下來該學什麼？

以下教學與本篇內容緊密相關，能進一步深化您對 API 的運用與其他實作方式：

- [Change PDF Opacity with Aspose.PDF – Complete C# Guide](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Change PDF Opacity in C# – Complete Aspose Guide](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-in-c-complete-aspose-guide/)
- [Add Transparency to PDF using Aspose – Complete C# Guide](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}