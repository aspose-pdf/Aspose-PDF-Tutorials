---
category: general
date: 2026-10-01
description: 使用 Aspose.PDF 新增自訂 ExtGState PDF，以快速設定 PDF 透明度。請參考本指南，了解如何使用自訂圖形狀態設定
  PDF 透明度。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom extgstate pdf
- how to set transparency pdf
- Aspose.PDF graphics state
- PDF opacity settings
- PDF blend mode tutorial
language: zh-hant
lastmod: 2026-10-01
og_description: 新增自訂 ExtGState PDF，並學習如何只用幾行 C# 程式碼設定 PDF 透明度。本指南涵蓋從載入檔案到儲存結果的每一步。
og_image_alt: Screenshot of a PDF page showing transparent graphics after adding a
  custom ExtGState
og_title: 在 PDF 中新增自訂 ExtGState – 完整 Aspose.PDF 教程
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Add custom ExtGState PDF using Aspose.PDF to set transparency PDF quickly.
    Follow this guide to learn how to set transparency PDF with a custom graphics
    state.
  headline: Add custom ExtGState PDF with Aspose.PDF – step‑by‑step guide
  type: TechArticle
tags:
- PDF
- Aspose.PDF
- C#
- GraphicsState
title: 使用 Aspose.PDF 新增自訂 ExtGState PDF – 一步一步教學
url: /zh-hant/net/images-graphics/add-custom-extgstate-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.PDF 新增自訂 ExtGState PDF – 步驟說明

如果您需要 **add custom ExtGState PDF** 以控制不透明度和混合模式，本教學將逐步說明。您將看到一個完整、可執行的範例，示範如何使用 Aspose.PDF for .NET **how to set transparency PDF**。

在以下章節中，我們將說明所需的 NuGet 套件、逐行程式碼解析，以及處理多頁或自訂混合模式等邊緣情況的技巧。完成後，您將能在不離開 IDE 的情況下，修改任何既有 PDF 並套用透明圖形狀態。

## 前置條件

- .NET 6.0 或更新版本（此程式碼亦相容 .NET Framework 4.7+）
- Visual Studio 2022（或您偏好的任何 C# 編輯器）
- **Aspose.PDF for .NET** NuGet 套件（版本 23.12 或更新）
- 一個名為 `input.pdf` 的範例 PDF 檔，放置於可於專案中參考的資料夾

> **Pro tip:** 在解決方案中使用專屬的 “Resources” 資料夾，以將輸入與輸出 PDF 放在一起。這可避免程式執行時的路徑相關錯誤。

## 安裝 Aspose.PDF

在 NuGet 套件管理員主控台中執行以下指令：

```bash
dotnet add package Aspose.PDF
```

此套件提供程式範例中使用的 `Aspose.Pdf.Document`、`CosPdfDictionary` 以及相關類別。

## 步驟 1 – 載入 PDF 文件

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;

// Load the source PDF
using var pdfDocument = new Document("Resources/input.pdf");
```

**此步驟的重要性：**  
`Document` 代表整個 PDF 檔案於記憶體中。以 `using` 區塊開啟可確保在完成處理後釋放所有非受管理資源。

## 步驟 2 – 取得第一頁的資源字典

```csharp
// Get the first page (pages are 1‑based in Aspose.PDF)
Page firstPage = pdfDocument.Pages[1];

// The resource dictionary holds objects like fonts, XObjects, and ExtGState entries
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

**說明：**  
每個 PDF 頁面都有一個 *Resources* 字典，用於彙集可重複使用的物件。編輯此字典即可注入新的圖形狀態，供該頁稍後參考。

## 步驟 3 – 取得（或建立）ExtGState 字典

```csharp
// Try to get the existing ExtGState dictionary; create one if it does not exist
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    extGStateDict = new CosPdfDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", extGStateDict);
}
```

**為何先檢查：**  
某些 PDF 已經定義了 `ExtGState` 條目。若再新增相同項目會覆寫既有狀態，可能導致其他內容損壞。此防禦式程式碼可保持原始條目完整。

## 步驟 4 – 建立自訂圖形狀態

```csharp
// Create an empty dictionary that will become our custom graphics state
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the graphics state entries
var graphicsStateEntries = new[]
{
    // CA – stroke opacity (range 0‑1)
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),
    // ca – fill opacity (range 0‑1)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // BM – blend mode (Normal, Multiply, Screen, etc.)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

// Add each entry to the dictionary
foreach (var entry in graphicsStateEntries)
{
    newGraphicsState.Add(entry);
}
```

**每個鍵的功能：**

| Key | 含義 | 典型值 |
|-----|------|--------|
| `CA` | 描邊不透明度 | `0.0` (完全透明) → `1.0` (不透明) |
| `ca` | 填充不透明度 | 與 `CA` 相同範圍 |
| `BM` | 混合模式 | `Normal`, `Multiply`, `Screen`, `Overlay`, 等 |

將 `ca` 設為 `0.5` 可使填充形狀呈現 50 % 透明度，而 `CA` 仍保持描邊完全不透明。變更 `BM` 可讓您試驗類似 Photoshop 的混合效果。

## 步驟 5 – 以唯一名稱註冊自訂圖形狀態

```csharp
// Choose a unique name for the new state, e.g., "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

**命名慣例：**  
PDF 規範建議使用簡短的大寫識別字。使用 `GS0`（Graphics State 0）可讓名稱在內容串流中易於引用。

## 步驟 6 – 在內容串流中套用自訂圖形狀態（可選）

若要在第一頁繪製透明矩形，可在前面加入以下運算子：

```csharp
// Build the content stream that uses the new graphics state
var content = new Operator[]
{
    new Operator("q"),                 // Save graphics state
    new Operator("GS0", "gs"),         // Set our custom ExtGState
    new Operator("0.5 0.5 1 rg"),      // Set fill color (light blue)
    new Operator("100 500 200 100 re"),// Rectangle (x, y, width, height)
    new Operator("f"),                 // Fill the rectangle using the fill opacity
    new Operator("Q")                  // Restore graphics state
};

// Add the operators to the page's content
firstPage.Contents.Add(content);
```

**此步驟為何可選：**  
前面的步驟僅 *定義* 圖形狀態。若要看到效果，必須在頁面的內容串流中引用它。上述程式碼示範了一個實用案例，您亦可將此狀態套用於 PDF 中已存在的繪圖指令。

## 步驟 7 – 儲存已修改的 PDF

```csharp
// Persist the changes to a new file
pdfDocument.Save("Resources/output.pdf");
```

開啟 `output.pdf` 時，您會看到矩形以 50 % 填充不透明度呈現，而其邊框仍保持完全不透明——這正是使用自訂 ExtGState **how to set transparency PDF** 的結果。

## 處理多頁文件

若需在每一頁套用相同的透明效果，可遍歷 `pdfDocument.Pages`，對每頁的資源重複 **Step 2**‑**Step 5**。請注意每頁僅加入一次圖形狀態；在多頁間重複使用相同字典違反 PDF 規範。

```csharp
foreach (Page page in pdfDocument.Pages)
{
    var editor = new DictionaryEditor(page.Resources);
    // Ensure ExtGState exists, then add GS0 as shown earlier
    // (code omitted for brevity)
}
```

## 常見陷阱與避免方法

| 症狀 | 原因 | 解決方案 |
|------|------|----------|
| 不透明度未變化 | `ca` 或 `CA` 的值超出 0‑1 範圍 | 使用介於 `0.0` 與 `1.0` 之間的十進位值。 |
| 內容消失 | 未套用圖形狀態（缺少 `gs` 運算子） | 在繪圖指令前插入 `GS0 gs`。 |
| PDF 無法開啟 | `ExtGState` 字典中有重複鍵 | 在新增前檢查 `extGStateDict.ContainsKey("GS0")`。 |
| 混合模式被忽略 | 檢視器不支援指定的模式 | 使用標準模式如 `Normal`、`Multiply`。 |

## 完整可執行範例

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Load the PDF
        using var pdfDocument = new Document("Resources/input.pdf");

        // Work with the first page
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        CosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        else
        {
            extGStateDict = new CosPdfDictionary(pdfDocument);
            resourcesEditor.Add("ExtGState", extGStateDict);
        }

        // Create custom graphics state
        CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var entries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var e in entries) newGraphicsState.Add(e);

        // Register under a unique name
        extGStateDict.Add("GS0", newGraphicsState);

        // Optional: draw a transparent rectangle
        var ops = new Operator[]
        {
            new Operator("q"),
            new Operator("GS0", "gs"),
            new Operator("0.5 0.5 1 rg"),
            new Operator("100 500 200 100 re"),
            new Operator("f"),
            new Operator("Q")
        };
        firstPage.Contents.Add(ops);

        // Save result
        pdfDocument.Save("Resources/output.pdf");
    }
}
```

**預期輸出：**  
開啟 `output.pdf` 會看到座標 (100, 500) 處有一個淡藍色矩形，填充不透明度為 50 %。矩形邊框保持完全不透明，因為 `CA` 設為 `1.0`。

## 結論

現在您已了解如何使用 Aspose.PDF **add custom ExtGState PDF** 物件，並精確控制不透明度與混合模式——回應了常見問題 **how to set transparency PDF**。本教學涵蓋了載入文件、編輯資源字典、定義圖形狀態、套用以及儲存結果的步驟。

接下來，您可以探索：

- 使用不同的混合模式（`Multiply`、`Screen`）以創造效果。
- 將相同的 ExtGState 套用於影像 XObject，以製作半透明標誌。
- 在背景服務中自動化大量 PDF 修改流程。

歡迎隨意嘗試不同的數值、重新命名圖形狀態，或

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，建立在此處示範的技巧之上。每個資源皆提供完整可運作的程式碼範例與逐步說明，協助您精通其他 API 功能，並在專案中探索替代實作方式。

- [使用 Aspose 為 PDF 添加透明度 – 完整 C# 教學](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [如何使用 Aspose.PDF for Java 為 PDF 添加頁面印章（2023 教學）](/pdf/english/java/watermarks-backgrounds/add-page-stamp-aspose-pdf-java/)
- [如何使用 Aspose.PDF for Java 為 PDF 添加文字印章：完整指南](/pdf/english/java/document-manipulation/aspose-pdf-java-add-text-stamp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}