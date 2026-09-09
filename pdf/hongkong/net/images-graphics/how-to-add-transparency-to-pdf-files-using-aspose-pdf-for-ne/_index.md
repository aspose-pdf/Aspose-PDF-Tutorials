---
category: general
date: 2026-09-08
description: 使用 Aspose.PDF for .NET 為 PDF 添加透明度 – 學習設定筆畫與填充的不透明度、混合模式，並在幾分鐘內儲存結果。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- aspose.pdf transparency
- pdf graphics state
- extgstate dictionary
- pdf opacity settings
language: zh-hant
lastmod: 2026-09-08
og_description: 使用 Aspose.PDF for .NET 為 PDF 添加透明度。本教學示範如何修改 ExtGState 字典、設定透明度與混合模式，並儲存更新後的檔案。
og_image_alt: Screenshot of a PDF page showing semi‑transparent shapes created with
  Aspose.PDF
og_title: 使用 Aspose.PDF 為 PDF 添加透明度 – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Add transparency to PDF with Aspose.PDF for .NET – learn to set stroke
    and fill opacity, blend mode, and save the result in minutes.
  headline: How to add transparency to PDF files using Aspose.PDF for .NET
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: 如何使用 Aspose.PDF for .NET 為 PDF 檔案添加透明度
url: /zh-hant/net/images-graphics/how-to-add-transparency-to-pdf-files-using-aspose-pdf-for-ne/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.PDF for .NET 為 PDF 檔案加入透明度

如果您需要 **為 PDF** 文件 **加入透明度**，本指南將示範如何使用 Aspose.PDF for .NET 修改圖形狀態。您將學會在單一頁面上設定描邊不透明度、填充不透明度以及混合模式，然後將結果儲存為新檔案。

透明度常用於浮水印、覆蓋圖形或報表中的視覺效果。在本教學中，您會看到完整可執行的程式碼，了解每個 API 呼叫的意義，並取得處理缺少資源條目等邊緣情況的技巧。

## 您需要的環境

在開始之前，請確保您具備：

* .NET 6.0 或更新版本（此程式碼亦相容 .NET Framework 4.6+）
* 有效的 Aspose.PDF for .NET 授權（免費試用版可用於測試）
* 名為 `input.pdf` 的輸入 PDF，放置於程式碼可參考的資料夾中
* C# 開發環境（Visual Studio、Rider 或 VS Code）

除 `Aspose.Pdf` 之外，無需額外的 NuGet 套件。

## PDF 圖形狀態概述

PDF 圖形狀態儲存在頁面資源字典內的 **ExtGState 字典** 中。每個條目定義了渲染參數，例如線寬、不透明度與混合模式。透過建立新的圖形狀態物件並將其加入 `ExtGState` 字典，即可在多個繪圖指令間重複使用相同的透明度設定。

了解此結構可避免常見的陷阱，例如嘗試直接在 `Page` 物件上設定不透明度（API 不支援）。相反地，您需要操作對應 PDF 規範的低階 COS 物件。

## 步驟 1：載入 PDF 文件

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Cos;

// Load the source PDF
var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");
```

*為什麼要這樣做？*  
`Document` 是任何 PDF 操作的入口點。載入檔案會在記憶體中建立可編輯的表示，而不會直接修改磁碟上的原始檔案。

## 步驟 2：取得第一頁與其資源字典編輯器

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor provides convenient access to the page’s resources
var resourceEditor = new DictionaryEditor(page.Resources);
```

*為什麼要這樣做？*  
所有圖形狀態條目都位於頁面的資源內。`DictionaryEditor` 抽象化了低階 COS 字典的處理，讓您能讀取或建立像 `ExtGState` 這樣的條目。

## 步驟 3：從頁面資源中取得 ExtGState 字典

```csharp
// The ExtGState entry may already exist; if not, create it
CosPdfDictionary extGStateDict;
if (resourceEditor.ContainsKey("ExtGState"))
{
    extGStateDict = (CosPdfDictionary)resourceEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a new ExtGState dictionary and attach it to the page resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);
    resourceEditor.Add("ExtGState", extGStateDict);
}
```

*為什麼要這樣做？*  
PDF 可能根本沒有 `ExtGState` 字典。上述程式碼會安全處理已有或缺少的情況，確保本教學能在任何輸入 PDF 上執行。

## 步驟 4：建立新的圖形狀態字典並定義其條目

```csharp
// Create an empty dictionary that will hold our transparency settings
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Define the entries:
//   CA – stroke opacity (0 = fully transparent, 1 = opaque)
//   ca – fill opacity
//   BM – blend mode (Normal, Multiply, etc.)
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity = 100%
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // Fill opacity = 50%
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Standard blend mode
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*為什麼要這樣做？*  
`CA` 與 `ca` 是控制描邊與非描邊（填充）操作不透明度的 PDF 運算子。將 `BM` 設為 `Normal` 可保留預設的合成行為，您亦可嘗試 `Multiply` 或 `Screen` 以獲得藝術效果。

## 步驟 5：將新圖形狀態加入 ExtGState 字典

```csharp
// Choose a unique name for the graphics state (e.g., GS0)
extGStateDict.Add("GS0", newGraphicsState);
```

*為什麼要這樣做？*  
名稱 `GS0` 成為之後在內容串流中使用的參考（`/GS0 gs`）。將它加入 `ExtGState` 後，PDF 便會認識這個新的透明度參數。

## 步驟 6：在內容串流中套用圖形狀態（可選）

如果您想立即看到效果，可以在內容串流前置一段簡單的繪圖指令，使用新建立的狀態：

```csharp
// Build a content stream that draws a semi‑transparent rectangle
var content = new PageContent();
content.Operators.Add(new Operator("q"));                     // Save graphics state
content.Operators.Add(new Operator("GS0", "gs"));            // Set our custom graphics state
content.Operators.Add(new Operator("0.2", "0.2", "0.8", "rg")); // Set fill color (light blue)
content.Operators.Add(new Operator("100", "500", "200", "100", "re")); // Rectangle
content.Operators.Add(new Operator("f"));                    // Fill
content.Operators.Add(new Operator("Q"));                     // Restore graphics state

// Insert the new content at the beginning of the page
page.Contents.Insert(0, content);
```

*為什麼要這樣做？*  
這段可選程式碼示範了您加入的圖形狀態（`GS0`）實際被使用的方式。矩形的填充會以 50 % 透明度呈現，而描邊則保持完全不透明。

## 步驟 7：儲存已修改的 PDF 文件

```csharp
pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
```

產生的檔案 `output.pdf` 包含新的 `ExtGState` 條目，若您加入了可選內容，還會有半透明的矩形覆蓋層。

### 預期輸出

當您在 Adobe Acrobat Reader 或任何 PDF 檢視器中開啟 `output.pdf` 時，應看到：

* 原始頁面內容保持不變。
* 若執行了可選的繪圖程式碼，會出現一個淡藍色矩形，其填充透明度為 50 %，底下的頁面內容得以透視。

## 完整原始碼清單

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Operators;
using System.Collections.Generic;

class AddTransparencyExample
{
    static void Main()
    {
        // 1. Load the PDF
        var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2. Get the first page and its resources
        var page = pdfDoc.Pages[1];
        var resourceEditor = new DictionaryEditor(page.Resources);

        // 3. Retrieve or create ExtGState dictionary
        CosPdfDictionary extGStateDict;
        if (resourceEditor.ContainsKey("ExtGState"))
            extGStateDict = (CosPdfDictionary)resourceEditor["ExtGState"].ToCosPdfDictionary();
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);
            resourceEditor.Add("ExtGState", extGStateDict);
        }

        // 4. Create new graphics state with transparency settings
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);
        var graphicsStateEntries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // Fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
        };
        foreach (var entry in graphicsStateEntries)
            newGraphicsState.Add(entry);

        // 5. Add the graphics state to ExtGState with a unique name
        extGStateDict.Add("GS0", newGraphicsState);

        // 6. (Optional) Draw a rectangle using the new state
        var content = new PageContent();
        content.Operators.Add(new Operator("q"));
        content.Operators.Add(new Operator("GS0", "gs"));
        content.Operators.Add(new Operator("0.2", "0.2", "0.8", "rg"));
        content.Operators.Add(new Operator("100", "500", "200", "100", "re"));
        content.Operators.Add(new Operator("f"));
        content.Operators.Add(new Operator("Q"));
        page.Contents.Insert(0, content);

        // 7. Save the updated PDF
        pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

將程式碼複製到主控台應用程式中，將 `YOUR_DIRECTORY` 替換為實際的資料夾路徑，然後執行。程式會產生帶有新增透明度設定的 `output.pdf`。

## 常見問題與避免方式

| 症狀 | 原因 | 解決方案 |
|------|------|----------|
| `KeyNotFoundException` 發生在 `"ExtGState"` | 該頁面沒有 `ExtGState` 條目。 | 本教學已在缺少時建立字典；請確保使用提供的條件判斷區塊。 |
| 透明度在檢視器中看不到 | 繪圖指令未引用 `GS0`。 | 如可選程式碼所示，在任何描邊/填充操作前加入 `gs` 運算子（`"GS0 gs"`）。 |
| 儲存後 PDF 損毀 | 高階 `Page` API 與低階 COS 物件混用不當。 | 僅使用 `DictionaryEditor` 取得 `CosPdfDictionary`，避免對同一字典進行重複修改。 |
| 混合模式無效 | 檢視器不支援所選的混合模式。 | 為了相容性請使用 `Normal`；若要嘗試 `Multiply`，請在支援的檢視器中測試。 |

## 後續步驟

既然您已掌握 **為 PDF 檔案加入透明度** 的方法，接下來可以：

* 透過遍歷 `pdfDoc.Pages`，將相同的圖形狀態套用至多個頁面。
* 結合裁剪路徑與透明度，實作更複雜的浮水印效果。
* 探索其他 ExtGState 條目，例如 `SM`（描邊調整）或 `CA`（描邊不透明度）。

## 接下來該學什麼？

以下教學與本指南緊密相關，提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能並在專案中探索替代實作方式。

- [How to Add and Align Text Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-text-stamp-aspose-pdf-dotnet/)
- [How to Add a Rotating Image Watermark to PDFs Using Aspose.PDF for .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)
- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET: A Complete Guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}