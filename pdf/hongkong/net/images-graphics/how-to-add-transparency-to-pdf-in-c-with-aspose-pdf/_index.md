---
category: general
date: 2026-11-22
description: 使用 Aspose.PDF for C# 為 PDF 添加透明度。學習如何透過清晰的逐步範例更改 PDF 的透明度。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- how to change pdf opacity
- Aspose.PDF opacity
- PDF graphics state C#
- PDF blend mode example
language: zh-hant
lastmod: 2026-11-22
og_description: 使用 Aspose.PDF for C# 為 PDF 添加透明度。本教學示範如何快速且可靠地更改 PDF 的不透明度。
og_image_alt: Screenshot of a PDF page showing translucent graphics after adding transparency
og_title: 在 C# 中為 PDF 添加透明度 – 完整的 Aspose.PDF 指南
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Add transparency to PDF using Aspose.PDF for C#. Learn how to change
    PDF opacity with a clear, step‑by‑step example.
  headline: How to add transparency to PDF in C# with Aspose.PDF
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: 如何在 C# 使用 Aspose.PDF 為 PDF 添加透明度
url: /zh-hant/net/images-graphics/how-to-add-transparency-to-pdf-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.PDF 為 PDF 添加透明度

如果您需要**為 PDF 添加透明度**，本指南將展示使用 Aspose.PDF for .NET 的完整解決方案。您將看到如何在不離開 C# 環境的情況下**更改 PDF 不透明度**，適用於向量圖形、文字或圖像。

本教學涵蓋每一步——從載入文件、編輯頁面的圖形狀態，到儲存結果。完成後，您可以產生選定元素呈半透明的 PDF，這對於浮水印、覆蓋效果或設計樣稿都非常有用。

## 前置條件

開始之前，請確保您已具備：

* .NET 6.0 或更新版本（程式碼同樣適用於 .NET Framework 4.8）
* 有效的 Aspose.PDF for .NET 授權或臨時評估金鑰
* Visual Studio 2022（或任何支援 C# 的 IDE）
* 一個名為 `input.pdf` 的輸入 PDF，放置於已知資料夾

上述項目可確保程式碼在無需額外設定的情況下執行。

## 第一步：載入 PDF 文件

第一個操作是開啟既有的 PDF 檔案。Aspose.PDF 以 `Document` 類別代表整個檔案。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;

// Load the source PDF
var inputPath = @"C:\MyFiles\input.pdf";
var doc = new Document(inputPath);
```

*為什麼這一步很重要*：載入文件會建立一個記憶體模型，讓您檢查頁面、資源與內容串流。沒有此物件就無法修改圖形狀態。

## 第二步：存取第一頁的資源字典

透明度是透過儲存在頁面資源字典中的**圖形狀態**套用的。您需要 `DictionaryEditor` 來編輯該字典。

```csharp
// Get the first page (pages are 1‑based)
var page = doc.Pages[1];

// Open the resource dictionary for editing
var dictEditor = new DictionaryEditor(page.Resources);
var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();
```

如果頁面尚未包含 `ExtGState` 條目，Aspose.PDF 會在您請求時自動建立一個空的字典。此彈性意味著相同程式碼同時適用於已使用透明度的 PDF 與從未使用過的 PDF。

## 第三步：建立帶有不透明度值的新圖形狀態

圖形狀態保存了填充不透明度 (`ca`)、描邊不透明度 (`CA`) 與混合模式 (`BM`) 等參數。以下程式碼建立一個字典，將填充不透明度設定為 50%，同時保持描邊完全不透明。

```csharp
// Build a new graphics state dictionary
var graphicsState = CosPdfDictionary.CreateEmptyDictionary(doc);

// Stroke opacity – fully opaque (value between 0 and 1)
graphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity – 50 % transparent
graphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode – Normal (other modes: Multiply, Screen, etc.)
graphicsState.Add("BM", new CosPdfName("Normal"));
```

*為什麼使用這些鍵*：  
* `CA` 控制描邊路徑（線條、邊框）的不透明度。  
* `ca` 控制填充物件（文字填充、圖像填充）的不透明度。  
* `BM` 決定透明物件與底層內容的混合方式；`Normal` 是最常見的選擇。

## 第四步：將圖形狀態註冊到頁面資源中

建立圖形狀態後，必須將它以唯一名稱（例如 `GS0`）加入頁面的 `ExtGState` 字典。之後的內容串流即可引用此名稱以套用不透明度設定。

```csharp
// Add the new graphics state to the resource dictionary
extGState.Add("GS0", graphicsState);
```

此時 PDF 檔案已包含一個可重複使用的圖形狀態 `GS0`。任何使用 `/GS0 gs` 的繪圖指令都會以指定的不透明度呈現。

## 第五步：將圖形狀態套用到頁面內容（可選）

如果您想影響既有內容，需要在頁面的內容串流開頭插入指令。以下程式碼示範如何在內容前置加入圖形狀態運算子。

```csharp
// Retrieve the original content stream
var content = page.Contents[1];

// Insert the graphics state operator at the start of the stream
content.Contents.Insert(0, new CosPdfLiteral("GS0 gs"));
```

*何時使用此步驟*：若 PDF 已包含繪圖指令且您希望它們變為半透明，請在開頭前置運算子。若您之後會新增物件，則可在建立物件時直接引用 `GS0`。

## 第六步：儲存已修改的 PDF

最後，將更新後的文件寫入磁碟。

```csharp
var outputPath = @"C:\MyFiles\output.pdf";
doc.Save(outputPath);
```

產生的 `output.pdf` 會在第一頁的填充元素呈現 50% 不透明度，而描邊則保持完整可見。使用任何 PDF 檢視器開啟檔案即可驗證效果。

## 如何為多頁 PDF 更改不透明度

相同的做法適用於任意頁碼。只要遍歷 `doc.Pages` 並重複步驟 2‑5，為每頁指派不同的圖形狀態名稱（例如 `GS1`、`GS2`）。以下為精簡版範例：

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    var pg = doc.Pages[i];
    var editor = new DictionaryEditor(pg.Resources);
    var ext = editor["ExtGState"].ToCosPdfDictionary();

    var gs = CosPdfDictionary.CreateEmptyDictionary(doc);
    gs.Add("CA", new CosPdfNumber(1));
    gs.Add("ca", new CosPdfNumber(0.75)); // 75% fill opacity
    gs.Add("BM", new CosPdfName("Normal"));

    var gsName = $"GS{i - 1}";
    ext.Add(gsName, gs);

    var cnt = pg.Contents[1];
    cnt.Contents.Insert(0, new CosPdfLiteral($"{gsName} gs"));
}
```

此迴圈減少重複程式碼，示範了**如何在整份文件中更改 PDF 不透明度**。

## 常見陷阱與最佳實踐建議

| 問題 | 為什麼會發生 | 推薦的解決方式 |
|------|--------------|----------------|
| 缺少 `ExtGState` 條目 | 某些 PDF 從未建立圖形狀態字典 | `DictionaryEditor` 會自動建立；不需要額外程式碼 |
| 透明度未顯示 | 檢視器快取了原始頁面 | 清除檢視器快取或重新開啟檔案 |
| 混合模式不匹配 | 在深色背景使用 `Multiply` 可能導致物件消失 | 測試不同的 `BM` 值（`Normal`、`Screen`、`Overlay`）以達到所需的視覺效果 |
| 多個圖形狀態衝突 | 在不同頁面重複使用相同名稱（`GS0`）會覆寫先前的定義 | 為每個頁面使用唯一名稱（`GS0`、`GS1`、…） |

## 完整可執行範例

以下是一個可直接複製、貼上並執行的完整程式。它包含所有 `using` 陳述式、錯誤處理與註解。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

class AddTransparencyDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        const string inputPath = @"C:\MyFiles\input.pdf";
        const string outputPath = @"C:\MyFiles\output.pdf";

        // Load the PDF
        var doc = new Document(inputPath);

        // Process each page
        for (int pageIndex = 1; pageIndex <= doc.Pages.Count; pageIndex++)
        {
            var page = doc.Pages[pageIndex];
            var dictEditor = new DictionaryEditor(page.Resources);
            var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();

            // Create a graphics state with 60% fill opacity
            var graphicsState = CosPdfDictionary.CreateEmptyDictionary(doc);
            graphicsState.Add("CA", new CosPdfNumber(1));               // stroke opacity
            graphicsState.Add("ca", new CosPdfNumber(0.6));             // fill opacity
            graphicsState.Add("BM", new CosPdfName("Normal"));         // blend mode

            // Unique name for this page
            string gsName = $"GS{pageIndex - 1}";
            extGState.Add(gsName, graphicsState);

            // Prepend the graphics state operator to the page content
            var content = page.Contents[1];
            content.Contents.Insert(0, new CosPdfLiteral($"{gsName} gs"));
        }

        // Save the result
        doc.Save(outputPath);
        Console.WriteLine($"PDF saved with transparency at: {outputPath}");
    }
}
```

**預期輸出**：開啟 `output.pdf` 後，每頁的填充形狀、文字或圖像皆以 60% 不透明度呈現，而邊框則保持完全不透明。此視覺變化立即生效，且在 Adobe Acrobat、Edge、Chrome 或任何支援 PDF 圖形狀態的檢視器中皆可正常顯示。

## 結論

您現在已掌握如何使用 Aspose.PDF for C# **為 PDF 添加透明度**。本教學說明了載入文件、編輯頁面資源字典、建立自訂圖形狀態以及儲存修改後的檔案。您也學會了**如何為單頁或多頁 PDF 更改不透明度**，並獲得避免常見錯誤的實用技巧。

接下來，您可以探索以下相關主題：

* 使用可變不透明度的圖像浮水印
* 使用不同混合模式（`Multiply`、`Screen`）創造創意效果
* 結合透明度與 PDF 註解

嘗試這些變化，讓 PDF 輸出更貼合您專案的視覺需求。祝開發順利！

## 您接下來應該學習什麼？

以下教學與本指南所示技術密切相關，提供完整的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索其他實作方式。

- [如何使用 Aspose.PDF 添加圖形狀態並控制透明度](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)
- [如何在 PDF 中設定不透明度以及如何使用 Aspose.Pdf 更改混合模式](/pdf/hongkong/net/images-graphics/how-to-set-opacity-in-a-pdf-and-how-to-change-blend-mode-wit/)
- [如何使用 Aspose.PDF 為 PDF 添加透明度並在 PDF 上繪製矩形](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}