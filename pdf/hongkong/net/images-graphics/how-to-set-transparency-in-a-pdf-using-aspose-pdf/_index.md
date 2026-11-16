---
category: general
date: 2026-11-16
description: 如何透過編輯 PDF 資源及有效載入 PDF，使用 Aspose.Pdf 設定 PDF 的透明度。請參考此完整的 C# 教學指南。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set transparency
- edit pdf resources
- load pdf aspose
language: zh-hant
lastmod: 2026-11-16
og_description: 如何使用 Aspose.Pdf 在 PDF 中設定透明度，直接從 C# 精確控制圖形的透明度。
og_image_alt: C# code snippet that sets PDF transparency via Aspose.Pdf
og_title: 使用 Aspose.Pdf 設定 PDF 透明度 – 步驟式 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to set transparency in a PDF with Aspose.Pdf by editing PDF resources
    and loading the PDF efficiently. Follow this complete C# guide.
  headline: How to set transparency in a PDF using Aspose.Pdf
  type: TechArticle
- description: How to set transparency in a PDF with Aspose.Pdf by editing PDF resources
    and loading the PDF efficiently. Follow this complete C# guide.
  name: How to set transparency in a PDF using Aspose.Pdf
  steps:
  - name: '**Load the PDF** with Aspose.Pdf (`load pdf aspose`).'
    text: '**Load the PDF** with Aspose.Pdf (`load pdf aspose`).'
  - name: '**Access the first page’s resources** dictionary (`edit pdf resources`).'
    text: '**Access the first page’s resources** dictionary (`edit pdf resources`).'
  - name: '**Create a custom ExtGState** that contains the desired transparency values.'
    text: '**Create a custom ExtGState** that contains the desired transparency values.'
  - name: '**Insert the ExtGState** back into the page resources.'
    text: '**Insert the ExtGState** back into the page resources.'
  - name: '**Save the modified PDF**.'
    text: '**Save the modified PDF**.'
  type: HowTo
tags:
- PDF
- Aspose.Pdf
- C#
title: 如何使用 Aspose.Pdf 在 PDF 中設定透明度
url: /zh-hant/net/images-graphics/how-to-set-transparency-in-a-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 PDF 中使用 Aspose.Pdf 設定透明度

如果您需要 **設定 PDF 文件的透明度**，本教學將示範使用 Aspose.Pdf for .NET 的完整步驟。無論是建立報表引擎或是加入浮水印，控制不透明度都是常見需求。閱讀完本指南後，您將擁有一個可執行的 C# 程式，能載入 PDF、編輯其資源，並將結果寫回磁碟。

處理 PDF 時常需要 **編輯 PDF 資源**（例如 ExtGState 字典），同時也必須 **正確載入 PDF Aspose** 以避免產生損毀的輸出。本指南同時說明這兩個重點，並解釋每個操作的意義，讓您能將此模式套用到多頁文件或自訂圖形狀態。

## 如何在 PDF 中設定透明度 – 概觀

PDF 中的透明度是由 *ExtGState*（外部圖形狀態）物件定義。此物件儲存筆畫不透明度 (`CA`)、填充不透明度 (`ca`) 與混合模式 (`BM`) 等參數。Aspose.Pdf 允許您直接操作這些字典，提供細緻的控制，而不必依賴較高階的 API。

整體流程如下：

1. **使用 Aspose.Pdf 載入 PDF**（`load pdf aspose`）。
2. **取得第一頁的資源字典**（`edit pdf resources`）。
3. **建立自訂 ExtGState**，內含所需的透明度數值。
4. **將 ExtGState 插回頁面資源**。
5. **儲存已修改的 PDF**。

每個步驟皆以簡潔的 C# 方法實作，完整原始碼則放在文章最後。

## 步驟 1：使用 Aspose.Pdf 載入 PDF（`load pdf aspose`）

在編輯任何內容之前，必須使用 Aspose 的 `Document` 類別開啟檔案。`using` 陳述式可確保即使發生例外，檔案句柄也會被釋放。

```csharp
// Step 1: Load the PDF document
using (var pdfDocument = new Aspose.Pdf.Document("YOUR_DIRECTORY/input.pdf"))
{
    // All subsequent operations happen inside this block.
}
```

**為什麼這很重要：**  
Aspose.Pdf 會將 PDF 結構解析成物件模型。一次載入文件並保留於記憶體，可避免重複 I/O，且確保您所做的變更套用於同一個實例。

**小技巧：** 若來源 PDF 受密碼保護，請將密碼傳入 `Document` 建構函式：

```csharp
var pdfDocument = new Aspose.Pdf.Document("input.pdf", new LoadOptions { Password = "mySecret" });
```

## 步驟 2：取得頁面資源字典（`edit pdf resources`）

每一頁 PDF 都有一個 *Resources* 字典，內含字型、影像與圖形狀態。要新增 ExtGState，先取得此字典，然後取得現有的 `ExtGState` 子字典（若不存在則建立）。

```csharp
// Step 2: Access the first page's resources dictionary
var firstPage = pdfDocument.Pages[1];                     // Aspose uses 1‑based indexing
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);

// Ensure the ExtGState entry exists; if not, create an empty dictionary.
if (!resourcesEditor.ContainsKey("ExtGState"))
{
    resourcesEditor["ExtGState"] = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
}
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

**為什麼這很重要：**  
`Resources` 字典是 PDF 渲染器唯一會搜尋圖形狀態定義的地方。如果缺少 `ExtGState` 條目，頁面將忽略您之後參考的任何不透明度設定。

**邊緣情況：** 有些 PDF 已經包含多筆 `ExtGState` 條目。此時如上所示直接重複使用現有字典，可避免覆寫與透明度無關的狀態。

## 步驟 3：定義透明度參數

透明度由三個鍵控制：

| 鍵 | 說明 | 常見範圍 |
|-----|---------|---------------|
| `CA` | 筆畫不透明度 | 0（完全透明） … 1（完全不透明） |
| `ca` | 填充不透明度 | 0 … 1 |
| `BM` | 混合模式 | `"Normal"`、`"Multiply"` 等 |

建立新的 `CosPdfDictionary`，並填入所需的值。

```csharp
// Step 3: Create a new ExtGState dictionary with desired entries
var customExtGState = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var graphicsStateParameters = new[]
{
    // Stroke opacity = 1 (fully opaque)
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("CA",
        new Aspose.Pdf.CosPdfNumber(1)),
    // Fill opacity = 0.5 (50% transparent)
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("ca",
        new Aspose.Pdf.CosPdfNumber(0.5)),
    // Blend mode = Normal (standard source‑over composition)
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("BM",
        new Aspose.Pdf.CosPdfName("Normal"))
};

foreach (var param in graphicsStateParameters)
    customExtGState.Add(param);
```

**為什麼這很重要：**  
將 `ca` 設為 `0.5` 會使任何填充形狀（例如矩形或文字）呈現半透明。您可以調整這些數值以取得精確的視覺效果。混合模式決定透明內容如何與底層圖形合成；`"Normal"` 是最常用的選擇。

**專業提示：** 若需要其他混合模式，只要把 `"Normal"` 換成 `"Multiply"`、`"Screen"` 等，即可產生暗化或亮化底層內容的藝術效果。

## 步驟 4：將自訂 ExtGState 插入頁面資源

接著為字典指定名稱（例如 `GS0`），並加入頁面的 `ExtGState` 集合。

```csharp
// Step 4: Add the custom ExtGState entry to the page resources
extGStateDict.Add("GS0", customExtGState);
```

**為什麼這很重要：**  
名稱 (`GS0`) 之後會在內容串流的圖形運算子中被引用。若要在多頁使用相同狀態，可重複使用同一名稱，或為每頁建立專屬名稱（`GS1`、`GS2`…）。

**進階變形：** 若要將此狀態套用於既有內容串流，可在繪圖指令前加入 PDF 運算子 `q /GS0 gs`。Aspose.Pdf 提供 `PdfContentEditor` 以完成此操作，但超出本基礎教學範圍。

## 步驟 5：儲存已修改的 PDF

最後，將變更寫入新檔案。保留原始檔不變，可方便比較前後差異。

```csharp
// Step 5: Save the modified PDF
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

**驗證方式：** 用任意 PDF 檢視器開啟 `output.pdf`。任何使用自訂圖形狀態（例如以 `GS0` 繪製的矩形）的填充形狀，都會以 50 % 不透明度呈現。若未看到變化，請再次確認內容串流確實引用了 `GS0`。您也可以使用 `PdfContentEditor` 插入測試矩形，以作為額外的驗證步驟。

## 完整可執行範例

將上述所有步驟整合，即可得到一個可直接貼到 Console 應用程式的自包含程式。

```csharp
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Operators;

class Program
{
    static void Main()
    {
        // Load the PDF (load pdf aspose)
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources (edit pdf resources)
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);
            if (!resourcesEditor.ContainsKey("ExtGState"))
                resourcesEditor["ExtGState"] = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create custom ExtGState with transparency
            var customExtGState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters) customExtGState.Add(p);
            extGStateDict.Add("GS0", customExtGState);

            // OPTIONAL: Apply the graphics state to a sample rectangle
            // This demonstrates that the transparency works.
            var canvas = new Aspose.Pdf.PageEditor(firstPage);
            canvas.AddRectangle(100, 500, 200, 600); // left, bottom, right, top
            // Set the graphics state before drawing
            canvas.ContentStream.Operators.Insert(0, new SetGraphicsState("GS0"));
            canvas.Save();

            // Save the modified PDF
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        System.Console.WriteLine("Transparency applied successfully.");
    }
}
```

**可選區塊說明：**  
`PageEditor` 會在頁面上加入一個簡單矩形，並明確設定圖形狀態為 `GS0`。此步驟適合測試；在實際情境中，您通常已經有內容會引用此狀態。

## 常見

## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步深化您對 API 的運用，並提供其他實作方式供您在專案中探索。

- [How to add graphics state pdf and control transparency with Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)
- [How to add transparency to PDF using Aspose.PDF in C#](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [How to change PDF transparency using Aspose.Pdf in C#](/pdf/english/net/programming-with-operators/how-to-change-pdf-transparency-using-aspose-pdf-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}