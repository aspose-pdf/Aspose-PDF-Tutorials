---
category: general
date: 2026-08-08
description: 使用 Aspose.PDF 在 C# 中設定 PDF 透明度 – 只需幾行程式碼，即可學習如何調整描邊與填充的透明度。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set pdf opacity
- Aspose.PDF for .NET
- C# graphics state
- PDF resource dictionary
- blend mode
- PDF transparency
language: zh-hant
lastmod: 2026-08-08
og_description: 快速在 C# 中設定 PDF 不透明度。本指南示範如何使用 Aspose.PDF 的圖形狀態 API 變更描邊與填充的透明度。
og_image_alt: Screenshot of C# code that sets PDF opacity with Aspose.PDF
og_title: 在 C# 中使用 Aspose.PDF 設定 PDF 透明度 – 步驟教學
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Set PDF opacity in C# using Aspose.PDF – learn how to adjust stroke
    and fill transparency with a few lines of code.
  headline: Set PDF opacity in C# with Aspose.PDF – complete guide
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: 使用 Aspose.PDF 在 C# 中設定 PDF 透明度 – 完整指南
url: /zh-hant/net/images-graphics/set-pdf-opacity-in-c-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中使用 Aspose.PDF 設定 PDF 不透明度 – 完整指南

如果您需要 **設定 PDF 不透明度** 於特定繪圖操作，本教學將示範如何使用 Aspose.PDF for .NET 完成。無論是製作浮水印、半透明覆蓋層，或是自訂圖形，您都能學到簡潔、可直接投入生產環境的做法。

在以下章節中，我們將從載入 PDF、編輯其圖形狀態、加入新的不透明度定義，到儲存結果，一步步說明。只需以下程式碼與簡短說明，即可完成，無需額外文件。

## 前置條件

開始之前，請確保您已具備：

* .NET 6.0 或更新版本（此程式碼亦相容 .NET Framework 4.7 以上）
* 有效的 Aspose.PDF for .NET 授權（免費試用版可用於評估）
* 位於可讀寫資料夾中的輸入 PDF 檔案（`input.pdf`）
* Visual Studio 2022 或您慣用的 C# IDE

## 第一步 – 載入 PDF 文件（Aspose.PDF for .NET）

首要任務是開啟既有的 PDF。Aspose.PDF 以 `Document` 類別代表 PDF 檔案，讓您完整存取頁面、資源與低階物件。

```csharp
// Load the PDF document from disk
string inputPath = @"C:\MyFolder\input.pdf";
using var doc = new Aspose.Pdf.Document(inputPath);
```

*為什麼這很重要*：載入文件會建立一個記憶體模型，您可以安全地進行修改。`using` 陳述式會在完成後自動釋放檔案句柄。

## 第二步 – 取得要編輯的第一頁

不透明度是依頁面於資源字典中定義的。此處以第一頁為目標，若需批次處理，可遍歷 `doc.Pages`。

```csharp
// Access the first page (pages are 1‑based in Aspose.PDF)
var page = doc.Pages[1];
```

*為什麼這很重要*：每一頁都有自己的 `Resources` 集合，儲存圖形狀態、字型、影像等。編輯正確的頁面才能讓不透明度效果出現在預期位置。

## 第三步 – 開啟頁面資源字典以供編輯

Aspose.PDF 提供 `DictionaryEditor` 輔助工具，讓您在不破壞檔案結構的前提下操作低階 PDF 字典。

```csharp
// Prepare a dictionary editor for the page's resources
var dictEditor = new Aspose.Pdf.DictionaryEditor(page.Resources);
```

*為什麼這很重要*：直接編輯 PDF 的 COS（Content Object System）字典是注入自訂圖形狀態的唯一途徑。編輯器抽象化低階語法，同時保持 PDF 的有效性。

## 第四步 – 取得現有的 ExtGState 字典

**ExtGState**（外部圖形狀態）字典保存不透明度、混合模式、線寬等資訊。若不存在，當您新增條目時，Aspose.PDF 會自動建立。

```csharp
// Get the ExtGState dictionary; create it if missing
var extGState = dictEditor["ExtGState"]?.ToCosPdfDictionary()
                ?? new Aspose.Pdf.Cos.CosPdfDictionary(doc);
```

*為什麼這很重要*：若沒有 `ExtGState` 條目，稍後在頁面內容串流中無法引用自訂不透明度。此步驟確保容器已存在。

## 第五步 – 建立具有目標不透明度的圖形狀態

圖形狀態是一組參數。對於不透明度，我們設定 `CA`（描邊不透明度）與 `ca`（填充不透明度）。同時設定 `BM`（混合模式）以控制透明像素與底層內容的互動方式。

```csharp
// Build a new graphics state dictionary
var newGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(doc);
newGs.Add("CA", new Aspose.Pdf.Cos.CosPdfNumber(0.8)); // 80 % stroke opacity
newGs.Add("ca", new Aspose.Pdf.Cos.CosPdfNumber(0.4)); // 40 % fill opacity
newGs.Add("BM", new Aspose.Pdf.Cos.CosPdfName("Normal")); // standard blend mode
```

*為什麼這很重要*：`CA` 與 `ca` 的取值範圍為 0（完全透明）至 1（完全不透明）。依需求調整這些數值即可得到所需的視覺效果。混合模式 `"Normal"` 為最常用，亦可嘗試 `"Multiply"` 或 `"Screen"` 以獲得藝術效果。

## 第六步 – 在 ExtGState 集合中註冊新的圖形狀態

每個圖形狀態必須有唯一名稱（例如 `GS0`）。我們將字典加入 `ExtGState` 集合，然後更新頁面的資源。

```csharp
// Add the new graphics state under the name "GS0"
extGState.Add("GS0", newGs);

// Ensure the ExtGState entry is stored back in the page resources
dictEditor["ExtGState"] = extGState;
```

*為什麼這很重要*：透過命名（`GS0`），您可以在頁面內容串流中使用 `gs` 運算子引用它。若需多種不透明度層級，只要再建立額外條目（`GS1`、`GS2` …）即可。

## 第七步 – 將圖形狀態套用至繪圖指令（可選）

若想立即對現有內容套用不透明度，必須編輯頁面的內容串流。以下示範使用新建的狀態繪製半透明矩形。

```csharp
// Build a content stream that uses the graphics state GS0
var content = new Aspose.Pdf.Operator.GSave();
content.Operators.Add(new Aspose.Pdf.Operator.SetGraphicsState("GS0"));
content.Operators.Add(new Aspose.Pdf.Operator.SetFillColorRgb(1, 0, 0)); // red fill
content.Operators.Add(new Aspose.Pdf.Operator.Rectangle(100, 500, 200, 100));
content.Operators.Add(new Aspose.Pdf.Operator.FillPath());
content.Operators.Add(new Aspose.Pdf.Operator.GRestore());

page.Contents.Add(content);
```

*為什麼這很重要*：`gs` 運算子（`SetGraphicsState`）告訴 PDF 渲染器在後續的繪圖指令中使用 `GS0` 定義的透明度值。`grestore`/`gsave` 配對確保其他頁面元素不受影響。

## 第八步 – 儲存已修改的 PDF

最後，將更新後的文件寫回磁碟。

```csharp
// Save the PDF with the new opacity settings
string outputPath = @"C:\MyFolder\output.pdf";
doc.Save(outputPath);
```

*為什麼這很重要*：儲存會完成所有變更、嵌入新的圖形狀態，產生任何檢視器（Adobe Acrobat、Chrome 等）皆能正確顯示設定透明度的 PDF。

### 預期結果

在 PDF 檢視器中開啟 `output.pdf`。您應該會看到一個紅色矩形，其邊框不透明度為 80%，填充不透明度為 40%，與背景內容平滑混合。其餘頁面保持不變。

## 常見變化與邊緣情況

| 情況 | 需要變更的地方 | 原因 |
|-----------|----------------|--------|
| **多層不透明度** | 建立額外的圖形狀態（`GS1`、`GS2` …）並設定不同的 `CA`/`ca` 值，於需要處使用 | 允許對不同元素進行細緻的控制 |
| **不同混合模式** | 在 `BM` 條目中使用 `"Multiply"`、`"Screen"`、`"Overlay"` 等取代 `"Normal"` | 產生藝術性的混合效果 |
| **套用於既有內容串流** | 在欲影響的繪圖運算子前插入 `SetGraphicsState` | 防止不相關物件被意外套用透明度 |
| **大型 PDF** | 使用 `foreach (Page p in doc.Pages)` 迴圈逐頁處理，避免一次載入整個檔案 | 提升效能並降低記憶體壓力 |
| **不存在 ExtGState** | 第 4 步的程式碼已會在缺少時自動建立，無需額外處理 | 確保字典已存在 |

### 專業小技巧

當您加入大量自訂圖形狀態時，請保持命名一致（`GS0`、`GS1` …），並在註解區塊說明每個狀態的用途。這樣在協作專案中維護會更容易。

## 完整可執行範例

以下提供完整程式，您可以直接複製、貼上並執行。內容包含所有步驟、必要的 `using` 指示詞與說明註解。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

namespace PdfOpacityDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the PDF
            string inputPath = @"C:\MyFolder\input.pdf";
            using var doc = new Document(inputPath);

            // 2. Get the first page (adjust index for other pages)
            var page = doc.Pages[1];

            // 3. Open the page's resource dictionary
            var dictEditor = new DictionaryEditor(page.Resources);

            // 4. Retrieve or create the ExtGState dictionary
            var extGState = dictEditor["ExtGState"]?.ToCosPdfDictionary()
                            ?? new CosPdfDictionary(doc);

            // 5. Create a new graphics state with desired opacity
            var newGs = CosPdfDictionary.CreateEmptyDictionary(doc);
            newGs.Add("CA", new CosPdfNumber(0.8));          // stroke opacity (80%)
            newGs.Add("ca", new CosPdfNumber(0.4));          // fill opacity (40%)
            newGs.Add("BM", new CosPdfName("Normal"));      // blend mode

            // 6. Register the graphics state as "GS0"
            extGState.Add("GS0", newGs);
            dictEditor["ExtGState"] = extGState; // write back to resources

            // 7. (Optional) Draw a rectangle using the new opacity
            var content = new Operator.GSave();
            content.Operators.Add(new Operator.SetGraphicsState("GS0"));
            content.Operators.Add(new Operator.SetFillColorRgb(1, 0, 0)); // red
            content.Operators.Add(new Operator.Rectangle(100, 500, 200, 100));
            content.Operators.Add(new Operator.FillPath());
            content.Operators.Add(new Operator.GRestore());

            page.Contents.Add(content);

            // 8. Save the modified PDF
            string outputPath = @"C:\MyFolder\output.pdf";
            doc.Save(outputPath);

            Console.WriteLine("PDF saved with new opacity settings at: " + outputPath);
        }
    }
}
```

執行程式後，

## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步擴展您對 API 的運用，並提供其他實作方式的範例。

- [Set Image Backgrounds in PDFs Using Aspose.PDF for .NET: A Comprehensive Guide](/pdf/english/net/images-graphics/aspose-pdf-net-set-image-backgrounds/)
- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [How to Customize PDFs with Aspose.PDF for .NET: Set Page Margins and Draw Lines](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}