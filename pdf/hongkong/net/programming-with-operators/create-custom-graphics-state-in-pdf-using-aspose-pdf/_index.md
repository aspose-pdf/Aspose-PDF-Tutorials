---
category: general
date: 2026-08-20
description: 使用 Aspose.Pdf 在 PDF 中建立自訂圖形狀態。了解如何編輯 PDF 資源並在簡單的幾個步驟中加入透明度。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom graphics state
- edit pdf resources
- add transparency pdf
- Aspose.Pdf graphics state
- PDF resource dictionary
language: zh-hant
lastmod: 2026-08-20
og_description: 使用 Aspose.Pdf 在 PDF 中建立自訂圖形狀態。本教學示範如何快速編輯 PDF 資源並加入透明效果。
og_image_alt: Screenshot of C# code that creates a custom graphics state in a PDF
og_title: 在 PDF 中建立自訂圖形狀態 – Aspose.Pdf 指南
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create custom graphics state in PDF with Aspose.Pdf. Learn how to edit
    PDF resources and add transparency PDF in just a few steps.
  headline: Create custom graphics state in PDF using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- Aspose.Pdf
- C#
- Graphics state
title: 使用 Aspose.Pdf 在 PDF 中建立自訂圖形狀態
url: /zh-hant/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Pdf 在 PDF 中建立自訂圖形狀態

如果您需要在 PDF 中 **建立自訂圖形狀態**，本指南將向您展示如何使用 Aspose.Pdf for .NET 完成此操作。完成本教學後，您將能夠 **編輯 PDF 資源**、注入新的 graphics‑state 字典，並且 **在 PDF 中加入透明度** 內容，而無需離開您的 C# 專案。

您將看到完整且可執行的範例、每行程式碼重要性的說明，以及處理多頁文件或不同混合模式的技巧。無需任何外部工具——只需 Aspose.Pdf 函式庫和基本的 .NET 開發環境。

## 前置條件

* .NET 6.0 或更新版本（此程式碼亦可在 .NET Framework 4.7+ 上執行）
* 取得 **Aspose.Pdf for .NET** 的授權副本（免費試用版可用於測試）
* 一個名為 `input.pdf` 的輸入 PDF 檔案，放置於可於程式碼中參照的資料夾
* Visual Studio 2022 或任何支援 C# 開發的 IDE

本教學假設您已熟悉基本的 C# 語法以及 PDF 頁面的概念。

## 步驟 1：載入來源 PDF 並存取第一頁

第一步是開啟 PDF 檔案並取得您想要修改其資源的頁面。Aspose.Pdf 將每一頁表示為 `Page` 物件，且每頁都包含一個 **resource dictionary**，用於儲存圖形狀態、字型、XObject 等等。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

// Load the PDF you want to edit
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Get the first page (pages are 1‑based in Aspose.Pdf)
    Page firstPage = pdfDocument.Pages[1];
```

*此處重要原因：* `Document` 類別將檔案載入記憶體，而 `Pages[1]` 直接存取第一頁的 resource dictionary，也就是圖形狀態所在的地方。

## 步驟 2：開啟資源字典以進行編輯

Aspose.Pdf 提供了 `DictionaryEditor` 輔助類別，讓您可以將資源字典視為一般的 .NET `Dictionary`。這使得讀取、加入或取代如 `ExtGState` 等條目變得相當直接。

```csharp
    // Create an editor for the page’s resources
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*此處重要原因：* `DictionaryEditor` 抽象化了低階的 COS 物件，讓您能以熟悉的鍵/值配對操作，同時仍保持 PDF 的相容性。

## 步驟 3：取得（或建立）ExtGState 字典

**ExtGState** 條目保存了該頁面的所有外部 graphics‑state 物件。如果字典不存在，Aspose.Pdf 會為您建立一個空的字典。

```csharp
    // Ensure the ExtGState dictionary exists
    var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
        ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
        : new CosPdfDictionary(pdfDocument);
```

*此處重要原因：* 若缺少 `ExtGState` 條目，稍後會拋出 `KeyNotFoundException`。此保護機制讓程式碼能在從未定義過自訂圖形狀態的 PDF 上運作——是 **edit PDF resources** 穩健性的關鍵。

## 步驟 4：建立自訂圖形狀態字典

圖形狀態描述了繪圖操作的呈現方式。若要 **add transparency PDF**，您需要設定 `ca`（填充不透明度）和 `CA`（描邊不透明度）條目，並可選擇設定混合模式（`BM`）。以下程式碼會使用這些參數建立新的字典。

```csharp
    // Create an empty dictionary that will become the new graphics state
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Define the parameters you want for the custom state
    var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
    {
        // Stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        // Fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        // Blend mode – "Normal" is the default, but you can use "Multiply", "Screen", etc.
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };

    // Populate the dictionary with the parameters
    foreach (var param in graphicsStateParams)
        newGraphicsState.Add(param);
```

*此處重要原因：* `ca` 與 `CA` 條目分別控制填充與描邊的透明度。設定 `BM` 可讓您嘗試不同的合成效果，這在稍後 **add transparency PDF** 內容（如半透明形狀或影像）時相當有用。

## 步驟 5：以唯一名稱註冊新的圖形狀態

`ExtGState` 字典中的每個圖形狀態必須有唯一的名稱（例如 `GS0`、`GS1`）。您可以選擇任何不與現有條目衝突的名稱。

```csharp
    // Choose a name that is unlikely to collide with existing states
    const string graphicsStateName = "GS0";

    // Add the new graphics state to the ExtGState dictionary
    extGStateDict.Add(graphicsStateName, newGraphicsState);

    // If the ExtGState entry was missing, attach it back to the page resources
    if (!resourcesEditor.ContainsKey("ExtGState"))
        resourcesEditor["ExtGState"] = extGStateDict;
```

*此處重要原因：* 透過在 `GS0` 下插入新字典，您使該狀態可在頁面內容串流中被引用。條件區塊確保即使是未包含 `ExtGState` 的 PDF 也會先建立該條目——另一項 **edit PDF resources** 的防護措施。

## 步驟 6：在頁面內容中使用自訂圖形狀態（可選）

前面的步驟僅 *定義* 了圖形狀態。若要實際看到效果，必須在頁面的內容串流中引用它。以下是一個快速範例，使用剛剛建立的狀態繪製半透明矩形。

```csharp
    // Get the page’s content stream (or create a new one if empty)
    var content = firstPage.Contents[1];
    var graphics = new ContentWriter(content);

    // Save current graphics state
    graphics.WriteOperator(OperatorName.SaveState);
    // Set the custom graphics state we just defined
    graphics.WriteOperand($"/{graphicsStateName}");
    graphics.WriteOperator(OperatorName.SetExtGState);
    // Draw a rectangle (coordinates are in points)
    graphics.WriteOperand(100);   // lower‑left x
    graphics.WriteOperand(500);   // lower‑left y
    graphics.WriteOperand(200);   // width
    graphics.WriteOperand(100);   // height
    graphics.WriteOperator(OperatorName.Rectangle);
    // Fill the rectangle using the current fill opacity (ca = 0.5)
    graphics.WriteOperator(OperatorName.Fill);
    // Restore the previous graphics state
    graphics.WriteOperator(OperatorName.RestoreState);
```

*此處重要原因：* `SetExtGState` 運算子（`gs`）告訴 PDF 渲染器套用 `GS0` 中定義的參數。矩形將以 50 % 的填充不透明度顯示，而其描邊則保持完全不透明。

## 步驟 7：儲存已修改的 PDF

最後，將變更寫回磁碟。您可以覆寫原始檔案或建立新檔案。

```csharp
    // Save the updated PDF
    pdfDocument.Save("YOUR_DIRECTORY/output_with_custom_gs.pdf");
}
```

當您在 PDF 檢視器中開啟 `output_with_custom_gs.pdf` 時，應該會在第一頁看到半透明矩形。這證明您已成功 **create custom graphics state**、**edit PDF resources**，以及 **add transparency PDF** 內容。

## 常見變化與邊緣情況

| Situation | What to adjust |
|-----------|----------------|
| **多頁需要相同狀態** | 僅註冊一次圖形狀態（步驟 1‑5），然後在任何頁面的內容串流中引用 `GS0`。 |
| **每個元素的透明度不同** | 定義額外的狀態（`GS1`、`GS2`、…）並設定不同的 `ca`/`CA` 值，然後使用 `SetExtGState` 在它們之間切換。 |
| **非 Normal 的混合模式** | 在 `BM` 條目中將 `"Normal"` 替換為 `"Multiply"`、`"Screen"` 或任何 PDF 標準的混合模式。 |
| **名稱衝突** | 加入前，檢查 `extGStateDict.ContainsKey(yourName)`，如有需要則選擇唯一的後綴。 |
| **PDF 已包含 ExtGState 字典** | 步驟 3 的程式碼已重新使用現有的字典，無需額外處理。 |

**Pro tip:** 在處理大型 PDF 時，將 `Document` 的使用包在 `using` 區塊中（如範例所示），以即時釋放原生資源。另外，若需在編輯資源後保證 PDF/A 或 PDF/X 相容性，可考慮啟用 Aspose.Pdf 的 `PdfCompliance` 屬性。

## 完整範例程式碼

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Load the PDF you want to edit
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 1: Get the first page
            Page firstPage = pdfDocument.Pages[1];

            // Step 2: Open the page resources for editing
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 3: Retrieve or create the ExtGState dictionary
            var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
                ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
                : new CosPdfDictionary(pdfDocument);

            // Step 4: Build a custom graphics state (50 % fill opacity, 100 % stroke opacity)
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var param in graphicsStateParams)
                newGraphicsState.Add(param);

            // Step 5: Register the graphics state under the name GS0
            const string graphicsStateName = "GS0";
            extGStateDict.Add(graphicsStateName, newGraphics


## 接下來您應該學習什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上進一步說明。每個資源皆包含完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [如何使用 Aspose 建立 PDF – 新增表單欄位與頁面](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [如何在 PDF 中使用 Aspose.PDF .NET 建立自訂表格](/pdf/english/net/tables-lists/create-custom-tables-in-pdfs-aspose-pdf-dot-net/)
- [建立自訂 PDF 印章 Aspose Pdf Net](/pdf/hongkong/net/images-graphics/create-custom-pdf-stamps-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}