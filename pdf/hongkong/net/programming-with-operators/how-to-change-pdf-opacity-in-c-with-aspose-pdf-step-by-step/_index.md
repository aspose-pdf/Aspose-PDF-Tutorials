---
category: general
date: 2026-10-23
description: 如何在 C# 中使用 Aspose.Pdf 更改 PDF 透明度。學習編輯 ExtGState、設定描邊/填充透明度，並在僅幾行程式碼內套用混合模式。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to change PDF opacity
- Aspose.Pdf opacity
- PDF graphics state
- ExtGState dictionary
- C# PDF manipulation
- PDF blend mode
language: zh-hant
lastmod: 2026-10-23
og_description: 如何在 C# 中使用 Aspose.Pdf 更改 PDF 的不透明度。請參考本簡明指南，修改描邊與填充的不透明度、設定混合模式，並儲存更新後的文件。
og_image_alt: Screenshot of a PDF page with semi‑transparent graphics created by Aspose.Pdf
  in C#
og_title: 如何在 C# 中更改 PDF 透明度 – 完整的 Aspose.Pdf 教程
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: How to change PDF opacity using Aspose.Pdf in C#. Learn to edit ExtGState,
    set stroke/fill opacity, and apply blend modes in just a few lines of code.
  headline: How to change PDF opacity in C# with Aspose.Pdf – step‑by‑step guide
  type: TechArticle
- description: How to change PDF opacity using Aspose.Pdf in C#. Learn to edit ExtGState,
    set stroke/fill opacity, and apply blend modes in just a few lines of code.
  name: How to change PDF opacity in C# with Aspose.Pdf – step‑by‑step guide
  steps:
  - name: Load the PDF document
    text: '```csharp using Aspose.Pdf;'
  - name: Get the first page and its resource dictionary
    text: '```csharp // Step 2: Get the first page and its resource dictionary var
      firstPage = pdfDocument.Pages[1]; var resourcesEditor = new DictionaryEditor(firstPage.Resources);
      ```'
  - name: Retrieve (or create) the ExtGState dictionary
    text: '```csharp // Step 3: Retrieve the ExtGState dictionary from the page resources
      // If ExtGState does not exist, create an empty one. CosPdfDictionary extGStateDict;
      if (resourcesEditor.ContainsKey("ExtGState")) { extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
      } else { extGStateDic'
  - name: Create a new graphics state dictionary and define opacity entries
    text: '```csharp // Step 4: Create a new graphics state dictionary and define
      its entries var graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
      var graphicsStateEntries = new[] { new KeyValuePair<string, ICosPdfPrimitive>("CA",
      new CosPdfNumber(1.0)), // Stroke opacity (fully opaque)'
  - name: Add the new graphics state to the ExtGState dictionary
    text: '```csharp // Step 5: Add the new graphics state to the ExtGState dictionary
      (named "GS0") extGStateDict.Add("GS0", graphicsStateDict); ```'
  - name: Save the updated PDF document
    text: '```csharp // Step 6: Save the updated PDF document pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
      } ```'
  type: HowTo
tags:
- PDF
- C#
- Aspose.Pdf
- Opacity
- GraphicsState
title: 如何在 C# 中使用 Aspose.Pdf 更改 PDF 透明度 – 逐步指南
url: /zh-hant/net/programming-with-operators/how-to-change-pdf-opacity-in-c-with-aspose-pdf-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 使用 Aspose.Pdf 調整 PDF 不透明度 – 步驟說明指南

如果您需要 **how to change PDF opacity**（調整 PDF 不透明度）於特定元素，本教學提供完整、可執行的解決方案。您將看到如何編輯 ExtGState 字典、設定筆畫與填充的不透明度，並選擇混合模式——全部只需幾行清晰的 C# 程式碼。

調整 PDF 不透明度在製作浮水印、覆蓋圖形或細緻視覺效果時非常有用，且不必重新建立整份文件。本指南假設您已具備基本的 C# 開發環境，並已安裝 Aspose.Pdf for .NET 套件。

![how to change PDF opacity using Aspose.Pdf in C#](https://example.com/og-image.png)

## 前置條件

開始之前，請確保您已具備：

* .NET 6.0 或更新版本（此程式碼亦相容 .NET Framework 4.7+）
* 正式授權的 **Aspose.Pdf for .NET**（免費試用版可用於測試）
* 一個可在程式碼中引用的 PDF 輸入檔案所在資料夾
* Visual Studio 2022 或您偏好的 C# 編輯器

不需要額外的 NuGet 套件——Aspose.Pdf 已包含本教學所需的所有類型。

## 了解 PDF 圖形狀態

PDF 頁面會在 **graphics state**（圖形狀態）物件中儲存繪圖參數。**ExtGState** 字典包含以下條目：

* **CA** – 筆畫不透明度 (0 = 透明, 1 = 不透明)
* **ca** – 填充不透明度
* **BM** – 混合模式（例如 *Normal*、*Multiply*、*Screen*）

透過建立新的圖形狀態字典並將其加入頁面的 ExtGState 集合，您可以在內容串流中稍後引用該狀態。此方式避免重新寫入整個頁面內容，且適用於任何既有 PDF。

## 使用 Aspose.Pdf 調整 PDF 不透明度

以下六個步驟涵蓋完整流程——從載入文件到儲存修改後的檔案。每一步皆提供完整程式碼與說明，說明其重要性。

### 步驟 1：載入 PDF 文件

```csharp
using Aspose.Pdf;

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

**為什麼重要** – 使用 `Aspose.Pdf.Document` 開啟檔案，可完整存取 PDF 內部結構，包括 **ExtGState** 字典所在的頁面資源。

### 步驟 2：取得第一頁及其資源字典

```csharp
// Step 2: Get the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

**為什麼重要** – 每一頁都有一個 *Resources* 字典，負責彙總字型、影像與圖形狀態。`DictionaryEditor` 提供對該集合的便利讀寫存取。

### 步驟 3：取得（或建立）ExtGState 字典

```csharp
// Step 3: Retrieve the ExtGState dictionary from the page resources
// If ExtGState does not exist, create an empty one.
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

**為什麼重要** – 某些 PDF 已包含 **ExtGState** 條目，某些則沒有。此條件判斷確保教學能同時適用於兩種情況，提升實務檔案的韌性。

### 步驟 4：建立新圖形狀態字典並定義不透明度條目

```csharp
// Step 4: Create a new graphics state dictionary and define its entries
var graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // Fill opacity (50 % transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

**為什麼重要** – 以下三個關鍵條目決定繪圖指令的呈現方式：

* `CA = 1.0` 讓筆畫線條保持完全可見。
* `ca = 0.5` 使填充形狀呈半透明。
* `BM = Normal` 使用預設混合模式；您可將 `"Normal"` 改為 `"Multiply"` 或 `"Screen"` 以產生創意效果。

### 步驟 5：將新圖形狀態加入 ExtGState 字典

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary (named "GS0")
extGStateDict.Add("GS0", graphicsStateDict);
```

**為什麼重要** – 為條目命名為 `"GS0"` 後，可在內容串流中使用 `/GS0 gs` 進行引用。若需多種不透明度變化，可再新增 `"GS1"`、`"GS2"` … 等條目，並設定不同的 `CA`/`ca` 值。

### 步驟 6：儲存更新後的 PDF 文件

```csharp
// Step 6: Save the updated PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

**為什麼重要** – 將變更寫回檔案，會把修改過的 **ExtGState** 字典持久化。最終的 PDF 現在包含可重複使用的圖形狀態，任何繪圖指令皆可呼叫。

## 將新圖形狀態套用至頁面內容

上述步驟僅建立圖形狀態，仍需在頁面的內容串流中引用它。以下是一個快速範例，使用剛剛新增的狀態繪製半透明矩形：

```csharp
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    var page = pdfDocument.Pages[1];
    var content = new PageContentEditor(page);
    // Begin the graphics state GS0
    content.InsertContent(0, "q /GS0 gs\n"); // Save graphics state and apply GS0
    // Draw a rectangle (100,100) to (300,300)
    content.InsertContent(0, "0.2 0.6 0.8 rg\n"); // Set fill color (light blue)
    content.InsertContent(0, "100 100 200 200 re\n");
    content.InsertContent(0, "f\n"); // Fill rectangle with current fill opacity
    // Restore graphics state
    content.InsertContent(0, "Q\n");
    pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

**說明** – `q` 運算子保存當前圖形狀態，`/GS0 gs` 套用不透明度設定，接著繪製矩形，最後 `Q` 恢復原始狀態。您可將此程式碼片段插入頁面的任意位置（在既有內容之前或之後），視視覺層次需求而定。

## 常見問題與避免方式

| 症狀 | 原因 | 解決方式 |
|------|------|----------|
| 不透明度未變化 | 頁面沒有 ExtGState 條目，或內容未引用新狀態。 | 確認 `ExtGState` 已存在，且內容串流包含 `/GS0 gs`（或您自訂的名稱）。 |
| 混合模式無效 | 使用不相容的色彩空間或 PDF 版本。 | 確保 PDF 版本至少為 1.4（透明度需求），且未在混合模式下混用點色。 |
| 文件在舊版檢視器無法開啟 | PDF 1.3 或更早版本不支援透明度。 | 在儲存前設定 `pdfDocument.Version = 1.4;`，或明確升級 PDF 版本。 |

## 測試結果

在 Adobe Acrobat Reader、Foxit 或任何現代 PDF 閱讀器中開啟 `output.pdf`。您應該會看到矩形的填充不透明度為 50%，而邊框保持完全不透明。可於 *Edit → Preferences → Accessibility* 中切換「使用高對比色」以驗證半透明效果仍然存在。

若需程式化驗證，Aspose.Pdf 也允許您讀回圖形狀態：

```csharp
var gs = pdfDocument.Pages[1].Resources["ExtGState"]["GS0"].ToCosPdfDictionary();
var fillOpacity = ((CosPdfNumber)gs["ca"]).Value; // Should be 0.5
```

## 延伸應用

* **多層不透明度** – 新增更多條目（`"GS1"`、`"GS2"`）並設定不同的 `ca` 值，於需要處使用。
* **不同混合模式** – 將 `"Normal"` 改為 `"Multiply"` 或 `"Screen"`，打造藝術性疊加效果。
* **套用於影像** – 在繪製 XObject 影像的 `Do` 運算子之前，使用相同的圖形狀態。

透過這些變化，您可以建立浮水印、強調區塊，或在不進行點陣化的情況下製作複雜視覺設計。

## 結論

您現在已掌握 **how to change PDF opacity**（如何在 C# 使用 Aspose.Pdf 調整 PDF 不透明度）。透過建立自訂圖形狀態、將其加入頁面的 ExtGState 字典，並在內容串流中呼叫該狀態，您即可細緻控制筆畫與填充的透明度以及混合模式。完整範例已可直接複製、執行，並套用於任何 PDF 操作情境。

準備好迎接下一個挑戰了嗎？試著將此技巧與 **Aspose.Pdf opacity** 結合於影像，或探索 **PDF blend mode** 效果，打造專業級的疊加層。祝您編程愉快！

## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步深化您所學的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，或在自己的專案中探索替代實作方式。

- [Change PDF Opacity with Aspose.PDF – Complete C# Guide](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Change opacity PDF in C# with Aspose.Pdf – step‑by‑step guide](/pdf/english/net/programming-with-pdf-pages/change-opacity-pdf-in-c-with-aspose-pdf-step-by-step-guide/)
- [How to change PDF transparency in C# using Aspose.Pdf](/pdf/english/net/programming-with-operators/how-to-change-pdf-transparency-in-c-using-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}