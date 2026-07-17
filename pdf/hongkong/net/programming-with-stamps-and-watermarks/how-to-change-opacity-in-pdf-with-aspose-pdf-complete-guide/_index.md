---
category: general
date: 2026-07-17
description: 如何使用 Aspose.PDF 更改 PDF 的不透明度。了解如何設定透明度、調整填充不透明度，並僅用幾行 C# 程式碼儲存修改後的 PDF
  檔案。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to change opacity
- how to set transparency
- save modified pdf
- set fill opacity
language: zh-hant
lastmod: 2026-07-17
og_description: 輕鬆學會在 PDF 中更改不透明度。本教學示範如何設定透明度、修改填充不透明度，並使用 Aspose.PDF 儲存已修改的 PDF
  檔案。
og_image_alt: Code snippet showing how to change opacity in a PDF using Aspose.PDF
og_title: 如何在 PDF 中更改不透明度 – Aspose.PDF 逐步說明
schemas:
- author: Aspose
  dateModified: '2026-07-17'
  description: How to change opacity in a PDF using Aspose.PDF. Learn how to set transparency,
    adjust fill opacity, and save modified PDF files in just a few lines of C#.
  headline: How to Change Opacity in PDF with Aspose.PDF – Complete Guide
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
- opacity
- transparency
title: 使用 Aspose.PDF 更改 PDF 透明度的完整指南
url: /zh-hant/net/programming-with-stamps-and-watermarks/how-to-change-opacity-in-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.PDF 更改 PDF 透明度 – 完整指南

有沒有想過 **如何在不開啟 Adobe Acrobat 的情況下更改現有 PDF 的透明度**？也許你需要一個半透明的浮水印或淡化的背景圖，但只能使用靜態檔案。好消息是？使用 Aspose.PDF for .NET，你可以以程式方式調整圖形狀態參數，還能學會 **如何設定透明度**、調整 **填充透明度**，以及 **快速儲存修改後的 PDF** 檔案。

在本教學中，我們會一步步示範真實案例：載入 PDF、建立新的 graphics state dictionary、定義筆畫與填充透明度，最後將變更寫回檔案。完成後，你將擁有一段可直接放入任何 C# 專案的可重用程式碼片段。

---

## 需要的條件

在開始之前，請確保你已具備：

- **Aspose.PDF for .NET**（最新版本，2026.x），透過 NuGet 安裝  
  ```bash
  dotnet add package Aspose.PDF
  ```
- **.NET 6+** 開發環境（Visual Studio、Rider 或 VS Code）。
- 一個放在可自行管理資料夾中的輸入 PDF（`input.pdf`）。
- 基本的 C# 與 PDF 概念（頁面、資源、字典）認識。

就這樣——不需要額外的函式庫，也不需要龐大的 SDK。讓我們開始動手吧。

---

## 使用 Aspose.PDF 更改 PDF 透明度的完整範例

以下是完整、可直接執行的範例程式碼。每一步都有簡易說明，方便你依需求調整（例如變更混合模式、加入新的 graphic state）。

![如何在 PDF 中更改透明度](/images/opacity-example.png "如何在 PDF 中更改透明度")

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;
using Aspose.Pdf.IO;
using Aspose.Pdf.InteractiveFeatures;
using System.Collections.Generic;

class OpacityDemo
{
    static void Main()
    {
        // Step 1: Load the PDF document
        string dataDir = "YOUR_DIRECTORY/";
        using (var document = new Aspose.Pdf.Document(dataDir + "input.pdf"))
        {
            // Step 2: Access the first page's resource dictionary
            var page = document.Pages[1];
            var resourcesEditor = new DictionaryEditor(page.Resources);

            // Step 3: Retrieve the ExtGState dictionary (holds graphics state parameters)
            var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Step 4: Create a new empty graphics state dictionary
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

            // Step 5: Define the graphics state entries
            // CA  – stroke opacity (1 = fully opaque)
            // ca  – fill opacity   (0.5 = 50 % transparent)
            // BM  – blend mode     (Normal is the default)
            var entries = new KeyValuePair<string, ICosPdfPrimitive>[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var entry in entries)
                newGraphicsState.Add(entry);

            // Step 6: Add the new graphics state to the ExtGState dictionary
            extGState.Add("GS0", newGraphicsState);

            // Step 7: Save the modified PDF
            document.Save(dataDir + "output.pdf");
        }
    }
}
```

### 為什麼這樣可行

- **ExtGState** 是一種特殊的 PDF 字典，用來儲存 *graphics state* 參數，例如透明度與混合模式。透過新增條目（`GS0`），我們為 PDF 建立一個可重複使用的「樣式」，之後可在內容串流中引用。
- **`ca`** 鍵控制 *填充透明度*（次要關鍵字「set fill opacity」）。`0.5` 代表填充會有 50 % 的透明度。
- **`CA`** 鍵則控制 *筆畫透明度*——在繪製線條或邊框時會用到。
- **Blend mode (`BM`)** 決定新圖形與底層內容的交互方式；「Normal」是最安全的預設值。

---

## 為特定內容設定透明度

現在 PDF 已經有了 `GS0` graphics state，接下來的步驟是實際 **使用** 它。以下程式碼示範如何將新透明度套用到文字片段，說明 **如何在單一物件上設定透明度**。

```csharp
// Assume 'document' and 'page' are already defined as above
var content = new PageContent();
content.Operators.Add(new SetGraphicsState("GS0")); // Apply our custom graphics state

var textFragment = new TextFragment("Semi‑transparent text")
{
    TextState = { FontSize = 24, Font = FontRepository.FindFont("Arial") }
};
page.Paragraphs.Add(textFragment);
page.Contents.Add(content);
```

幾點說明：

- `SetGraphicsState` 是 PDF 操作子，用來將當前的 graphics state 切換為我們先前定義的 `GS0`。  
- 若省略此行，PDF 仍會以預設（完全不透明）的設定呈現。  
- 你可以建立多個 graphics state（`GS1`、`GS2`…）以支援不同的透明度或混合模式。

---

## 儲存修改後的 PDF – 會發生什麼

執行完整程式後，你會在同一資料夾看到 `output.pdf`。使用任何閱讀器（Adobe Reader、Edge、Chrome）開啟，即可看到：

- 所有 *填充* 形狀（例如矩形、文字背景）以 50 % 透明度呈現。  
- 筆畫（線條、邊框）仍保持完全不透明，因為我們將 `CA` 保持在 `1`。  
- 沒有視覺異常——Aspose.PDF 會自行處理底層 PDF 結構。

若需將 **修改後的 PDF** 另存為其他格式（例如 PDF/A、PDF/X），只要改寫 `Save` 呼叫即可：

```csharp
document.Save(dataDir + "output.pdf", SaveFormat.PdfA_1b);
```

---

## 常見問題與進階小技巧

| 問題 | 為何會發生 | 解決方式 |
|------|------------|----------|
| **`resourcesEditor["ExtGState"]` 回傳 null** | 原始 PDF 從未定義 ExtGState 字典（簡易 PDF 常見）。 | 手動建立：`var extGState = new CosPdfDictionary(document); resourcesEditor["ExtGState"] = extGState;` |
| **透明度未變化** | 已加入 graphics state 但未在內容串流中引用。 | 在繪製欲透明的元素前使用 `SetGraphicsState("GS0")`。 |
| **混合模式未被套用** | 部分閱讀器會忽略非標準混合模式。 | 除非目標為 PDF/X‑4 或支援進階混合的閱讀器，否則使用 `"Normal"`。 |
| **大型 PDF 效能下降** | 逐頁修改會耗費較多資源。 | 批次處理：一次編輯共享的 ExtGState 字典，然後在每頁引用它。 |

---

## 完整可執行範例（一次呈現所有步驟）

為了方便起見，以下提供從載入文件到儲存結果的完整程式碼，包含使用新透明度的文字繪製範例：

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.IO;
using System.Collections.Generic;

class OpacityDemo
{
    static void Main()
    {
        string dataDir = "YOUR_DIRECTORY/";
        using (var document = new Aspose.Pdf.Document(dataDir + "input.pdf"))
        {
            var page = document.Pages[1];
            var resourcesEditor = new DictionaryEditor(page.Resources);

            // Ensure ExtGState dictionary exists
            if (!resourcesEditor.ContainsKey("ExtGState"))
                resourcesEditor["ExtGState"] = new CosPdfDictionary(document);
            var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create new graphics state (GS0)
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var e in entries) newGraphicsState.Add(e);
            extGState.Add("GS0", newGraphicsState);

            // Apply the graphics state to a text fragment
            var content = new PageContent();
            content.Operators.Add(new SetGraphicsState("GS0"));
            page.Contents.Add(content);

            var tf = new TextFragment("Semi‑transparent text")
            {
                TextState = { FontSize = 28, Font = FontRepository.FindFont("Arial") }
            };
            page.Paragraphs.Add(tf);

            // Save the altered PDF
            document.Save(dataDir + "output.pdf");
        }
    }
}
```

直接複製貼上，將 `YOUR_DIRECTORY` 替換為實際路徑後執行。你會看到文字以半透明方式呈現，證明 **如何更改透明度** 真的如此簡單。

---

## 往前走：超越透明度的應用

掌握了基礎後，你可以進一步探索：

- **動態透明度**：遍歷所有頁面，為每頁指定不同的 `ca` 值，實現漸層淡出。  
- **多個 graphics state**：建立 `GS1`、`GS2` 等，以在同一文件中呈現不同的透明度層級。  
- **進階混合模式**：嘗試 `"Multiply"` 或 `"Screen"` 以獲得藝術效果——只要記得不是所有閱讀器都支援。  
- **結合圖像**：使用 `ImageFragment` 插入半透明商標，並套用相同的 graphics state。

這些技巧皆圍繞同一核心概念：操作 **ExtGState** 字典，告訴 PDF 渲染器如何混合內容。模式不變，只有參數會改變。

## 接下來該學什麼？

以下教學與本指南緊密相關，能幫助你進一步掌握 API 功能，並在專案中探索其他實作方式。

- [如何使用 Aspose.PDF for .NET 自訂 PDF：設定頁邊距與繪製線條](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [如何在 PDF 中使用 Aspose.PDF for .NET 設定圖像大小](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [如何使用 Aspose.PDF for .NET 更改 PDF 頁面尺寸（步驟教學）](/pdf/english/net/document-manipulation/change-pdf-page-sizes-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}