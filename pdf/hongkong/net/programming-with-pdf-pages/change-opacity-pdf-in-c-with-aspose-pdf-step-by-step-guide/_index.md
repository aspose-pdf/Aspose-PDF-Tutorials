---
category: general
date: 2026-08-11
description: 使用 Aspose.Pdf 於 C# 更改 PDF 透明度。了解如何為 PDF 頁面加入透明效果、設定圖形狀態，並快速儲存結果。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change opacity PDF
- how to add transparency
- add pdf transparency
language: zh-hant
lastmod: 2026-08-11
og_description: 使用 Aspose.Pdf 在 C# 中更改 PDF 透明度。請參考本指南，了解如何為任何 PDF 文件加入透明效果、客製化圖形狀態，並匯出結果。
og_image_alt: Screenshot illustrating change opacity PDF example in C# code
og_title: 在 C# 中更改 PDF 透明度 – 完整 Aspose.Pdf 教程
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Change opacity PDF using Aspose.Pdf in C#. Learn how to add transparency
    to PDF pages, set graphic state, and save the result quickly.
  headline: Change opacity PDF in C# with Aspose.Pdf – step‑by‑step guide
  type: TechArticle
- description: Change opacity PDF using Aspose.Pdf in C#. Learn how to add transparency
    to PDF pages, set graphic state, and save the result quickly.
  name: Change opacity PDF in C# with Aspose.Pdf – step‑by‑step guide
  steps:
  - name: '**Missing ExtGState dictionary** – Some PDFs do not contain an `ExtGState`
      entry by default. In that case, create one:'
    text: '**Missing ExtGState dictionary** – Some PDFs do not contain an `ExtGState`
      entry by default. In that case, create one:'
  - name: '**Incorrect resource name** – The name you use in `SetGraphicsState` must
      match exactly the key you added (`GS0`). A typo results in the default, fully
      opaque rendering.'
    text: '**Incorrect resource name** – The name you use in `SetGraphicsState` must
      match exactly the key you added (`GS0`). A typo results in the default, fully
      opaque rendering.'
  - name: '**Overriding existing graphics states** – Adding a new entry does not replace
      existing ones. If you reuse a name that already exists, you may unintentionally
      alter other page elements that reference it.'
    text: '**Overriding existing graphics states** – Adding a new entry does not replace
      existing ones. If you reuse a name that already exists, you may unintentionally
      alter other page elements that reference it.'
  - name: '**Viewer compatibility** – Older PDF viewers (pre‑1.4) may ignore transparency.
      Ensure your target audience uses a modern viewer such as Adobe Reader DC or
      Chrome’s built‑in PDF viewer.'
    text: '**Viewer compatibility** – Older PDF viewers (pre‑1.4) may ignore transparency.
      Ensure your target audience uses a modern viewer such as Adobe Reader DC or
      Chrome’s built‑in PDF viewer.'
  type: HowTo
tags:
- PDF
- C#
- Aspose.Pdf
- Transparency
title: 使用 Aspose.Pdf 在 C# 中更改 PDF 透明度 – 步驟指南
url: /zh-hant/net/programming-with-pdf-pages/change-opacity-pdf-in-c-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中使用 Aspose.Pdf 更改 PDF 透明度 – 步驟指南

如果您需要以程式方式 **更改 PDF 透明度**，本教學將會完整示範。使用 Aspose.Pdf for .NET，您可以在 C# 程式碼中直接控制圖形物件、文字與影像的透明度。

在以下章節中，您將學習 **如何在 PDF 頁面加入透明度**、底層圖形狀態物件的意義，以及如何儲存已修改的文件。本指南亦會說明在 **新增 PDF 透明度** 時常見的陷阱，並提供實務情境的技巧。

## 您將完成的目標

* 載入現有的 PDF 文件。
* 建立一個定義透明度值的新 graphics state dictionary。
* 將 graphics state 插入頁面的 resource dictionary。
* 使用更新的 **change opacity PDF** 效果儲存文件。

不需要任何外部工具——只需 Aspose.Pdf for .NET 函式庫（版本 23.10 或更新）以及 .NET 開發環境。

## 前置條件

* 已安裝 .NET 6.0（或 .NET Framework 4.7.2+）。
* Visual Studio 2022 或任何相容 C# 的 IDE。
* 參考 `Aspose.Pdf` NuGet 套件。
* 位於可寫入目錄的輸入 PDF 檔案（`input.pdf`）。

> **專業提示：** 測試透明度變更時，請使用已包含向量圖形或文字的 PDF；光柵影像會忽略 `ca` 與 `CA` 參數，除非它們被放置在透明度群組中。

## 使用 Aspose.Pdf 更改 PDF 透明度

解決方案的核心是修改頁面的 **ExtGState**（外部圖形狀態）字典。此字典儲存諸如 **ca**（筆畫透明度）與 **CA**（填充透明度）等參數。透過新增條目，您可以在內容串流中稍後引用它。

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;

class ChangeOpacityPdfExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        using (var document = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 2: Access the first page and its resource dictionary
            var page = document.Pages[1];
            var dictEditor = new DictionaryEditor(page.Resources);
            var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();

            // Step 3: Create a new graphics state dictionary with desired opacity values
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                // Fill opacity (CA) – 1.0 means fully opaque
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                // Stroke opacity (ca) – 0.5 makes lines semi‑transparent
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                // Blend mode (BM) – Normal is the default blend mode
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // Step 4: Add the new graphics state to the ExtGState dictionary
            // “GS0” is the identifier you will reference later in the content stream
            extGState.Add("GS0", newGraphicsState);

            // Optional: Demonstrate usage by drawing a semi‑transparent rectangle
            // This part shows how the new graphics state affects drawing commands.
            var canvas = new Aspose.Pdf.Drawing.Graphic(page);
            canvas.SetGraphicsState("GS0"); // Apply the opacity settings
            canvas.Rectangle(100, 500, 200, 600);
            canvas.FillColor = Color.FromRgb(255, 0, 0); // Red fill
            canvas.StrokeColor = Color.FromRgb(0, 0, 255); // Blue border
            canvas.Draw();

            // Step 5: Save the modified PDF
            document.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF saved with changed opacity.");
    }
}
```

### 為何此方法可行

* **ExtGState** 是 PDF 的資源，用於儲存可重複使用的圖形參數。透過新增自訂條目 (`GS0`) 您即可建立可重複使用的透明度設定。
* **ca** 鍵控制筆畫操作（線條、邊框）的透明度。**CA** 鍵控制填充操作（彩色形狀、文字）的透明度。將 `ca = 0.5` 設為 50 % 透明，而 `CA = 1` 則保持填充完全不透明。
* `SetGraphicsState("GS0")` 呼叫告訴 Aspose.Pdf 在內容串流中產生 `/GS0 gs` 運算子，為後續的繪圖指令啟用新的透明度設定。

## 如何為現有內容加入透明度

如果頁面上已經有文字或影像，且您想在不重新繪製的情況下使其半透明，可在現有內容之前注入 **gs** 運算子。以下程式碼片段示範如何在頁面的 content stream 前置此運算子。

```csharp
// Retrieve the existing content stream
var content = page.Contents[1];
var originalBytes = content.ToByteArray();

// Build the new content with the graphics state applied
var gsOperator = System.Text.Encoding.ASCII.GetBytes("/GS0 gs\n");
var newBytes = new List<byte>(gsOperator);
newBytes.AddRange(originalBytes);

// Replace the page content
page.Contents[1].Replace(newBytes.ToArray());
```

### 邊緣情況與考量

| 情況 | 建議處理方式 |
|-----------|----------------------|
| **多頁面** | 迭代 `document.Pages`，對每個欲影響的頁面重複第 2‑4 步。 |
| **每個元素不同透明度** | 建立額外的 graphics states（`GS1`、`GS2` …），設定不同的 `ca`/`CA` 值，並選擇性套用。 |
| **含有既有 ExtGState 條目的 PDF** | 安全使用 `dictEditor["ExtGState"]`；若鍵不存在，建立新的 `CosPdfDictionary` 並指派給 `page.Resources`。 |
| **透明度群組** | 對於複雜的合成（例如重疊影像），設定 `/Group` 字典為 `S /Transparency` 且 `CS /DeviceRGB`。這超出基本 **change opacity PDF** 的範圍，但在進階版面配置可能需要。 |

## 為向量圖形加入 PDF 透明度

除了矩形之外，您也可以將相同的 graphics state 套用於任何向量繪圖——線條、曲線，甚至文字。以下是一個快速範例，寫入半透明文字：

```csharp
var textFragment = new TextFragment("Transparent text")
{
    Position = new Position(100, 400),
    TextState = { FontSize = 36, ForegroundColor = Color.Black }
};
page.Paragraphs.Add(textFragment);

// Apply the graphics state to the text fragment
textFragment.TextState.GraphicsState = "GS0";
```

`TextState` 的 `GraphicsState` 屬性告訴 PDF 引擎使用 `GS0` 中定義的透明度來渲染文字。這是將 **pdf 透明度** 加入文字內容最直接的方式。

## 更改 PDF 透明度時的常見陷阱

1. **缺少 ExtGState 字典** – 某些 PDF 預設不含 `ExtGState` 條目。此時需自行建立：
   ```csharp
   if (!dictEditor.ContainsKey("ExtGState"))
       dictEditor.Add("ExtGState", new CosPdfDictionary(document));
   ```
2. **資源名稱不正確** – 在 `SetGraphicsState` 中使用的名稱必須與您新增的鍵 (`GS0`) 完全相同。拼寫錯誤會導致使用預設的完全不透明渲染。
3. **覆寫既有圖形狀態** – 新增條目不會取代既有的。若重複使用已存在的名稱，可能會意外改變其他引用該名稱的頁面元素。
4. **檢視器相容性** – 舊版 PDF 檢視器（1.4 之前）可能會忽略透明度。請確保您的目標使用者使用如 Adobe Reader DC 或 Chrome 內建 PDF 檢視器等現代檢視器。

## 完整可執行範例

以下為完整、獨立的程式範例，您可以直接複製、貼上並執行。它包含所有必要的 `using` 指令、錯誤處理與註解。



## 接下來您應該學習什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上延伸技術。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [如何使用 Aspose.PDF .NET 為 PDF 添加文字浮水印：完整指南](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)
- [如何使用 Aspose.PDF for .NET 為 PDF 添加頁面浮水印：完整指南](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [如何使用 Aspose.PDF for .NET 為 PDF 添加頁面浮水印 | 浮水印與背景指南](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}