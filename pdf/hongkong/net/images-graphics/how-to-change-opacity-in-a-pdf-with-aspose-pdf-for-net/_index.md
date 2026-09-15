---
category: general
date: 2026-09-15
description: 如何使用 Aspose.Pdf for .NET 更改 PDF 的不透明度，並學習在儲存已修改的 PDF 檔案時加入透明度。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to change opacity
- how to add transparency
- save modified pdf
language: zh-hant
lastmod: 2026-09-15
og_description: 如何使用 Aspose.Pdf for .NET 更改 PDF 的不透明度，包括如何加入透明效果以及在數分鐘內儲存修改後的 PDF
  檔案。
og_image_alt: Screenshot showing a PDF page before and after opacity changes
og_title: 如何使用 Aspose.Pdf 更改 PDF 透明度 – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: How to change opacity in a PDF using Aspose.Pdf for .NET and learn
    how to add transparency while you save modified PDF files.
  headline: How to change opacity in a PDF with Aspose.Pdf for .NET
  type: TechArticle
tags:
- Aspose.Pdf
- .NET
- PDF manipulation
title: 如何使用 Aspose.Pdf for .NET 在 PDF 中更改透明度
url: /zh-hant/net/images-graphics/how-to-change-opacity-in-a-pdf-with-aspose-pdf-for-net/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 PDF 中使用 Aspose.Pdf for .NET 更改不透明度

如果您需要**更改 PDF 內物件的不透明度**，本指南將示範使用 Aspose.Pdf for .NET 的具體步驟。您還會看到**如何為圖形狀態加入透明度**，以及學習正確的**儲存已修改 PDF**檔案而不失去品質的方法。

更改不透明度是常見需求，例如想要覆蓋浮水印、建立淡化背景，或在文件內製作類 UI 效果。以下程式碼範例可適用於任何 Aspose.Pdf 能開啟的 PDF，且本教學會逐行說明，讓您了解*為什麼*這麼做很重要。

## 您將學會

- 使用 Aspose.Pdf 載入 PDF 文件。
- 編輯頁面的資源字典以建立新的圖形狀態。
- 定義描邊不透明度 (`CA`)、填充不透明度 (`ca`) 與混合模式 (`BM`)。
- 將圖形狀態插入 `ExtGState` 字典。
- **儲存已修改 PDF** 檔案，保留新的透明度設定。
- 處理如缺少 `ExtGState` 條目或多頁文件等邊緣情況。

### 前置條件

| Requirement | Reason |
|-------------|--------|
| .NET 6.0 or later | 提供 C# 程式碼的執行環境。 |
| Aspose.Pdf for .NET (NuGet package `Aspose.Pdf`) | 提供範例中使用的 PDF 操作 API。 |
| Basic C# knowledge | 需要了解語法與專案結構。 |
| An input PDF (`input.pdf`) | 您將要修改的檔案。 |

> **專業提示：** 在開始之前，使用 `dotnet add package Aspose.Pdf` 安裝套件。

## 步驟 1：載入 PDF 文件

第一個操作是開啟來源檔案。使用 `using` 區塊可確保文件正確釋放，避免在 Windows 上產生檔案鎖定。

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";

using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

> **Why this matters:** 開啟文件會建立可編輯的記憶體表示。`using` 陳述式確保資源釋放，這在之後**儲存已修改 PDF**到同一資料夾時尤為重要。

## 步驟 2：取得第一頁及其資源字典

透明度設定位於頁面的資源字典中。此處以第一頁為例，其他頁面同理。

```csharp
// Step 2: Retrieve the first page and its resources
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

> **Why this matters:** `Resources` 包含字型、影像以及存放圖形狀態的 `ExtGState` 字典。編輯此字典是影響繪圖指令不透明度的唯一方式。

## 步驟 3：確保 ExtGState 字典存在

如果 PDF 已有 `ExtGState` 條目，我們可以直接使用；否則必須建立新字典，以避免拋出 `KeyNotFoundException`。

```csharp
// Step 3: Get or create the ExtGState dictionary
Aspose.Pdf.CosCosPdfDictionary extGStateDict;

if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a fresh ExtGState dictionary and attach it
    extGStateDict = Aspose.Pdf.CosCosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", extGStateDict);
}
```

> **Why this matters:** PDF 結構彈性，有些檔案根本不會定義 `ExtGState`。建立它可讓後續的不透明度參數有放置位置。

## 步驟 4：建立含不透明度值的新圖形狀態

圖形狀態 (`GS`) 保存渲染參數。`CA`（描邊不透明度）與 `ca`（填充不透明度）接受 0（完全透明）到 1（完全不透明）的值。`BM` 鍵則選擇混合模式，`"Normal"` 為最常見選項。

```csharp
// Step 4: Create a graphics state dictionary and set opacity parameters
var graphicsState = Aspose.Pdf.CosCosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("CA", new Aspose.Pdf.CosPdfNumber(1.0)),   // stroke opacity (fully opaque)
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("ca", new Aspose.Pdf.CosPdfNumber(0.5)), // fill opacity (50% transparent)
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("BM", new Aspose.Pdf.CosPdfName("Normal")) // blend mode
};

foreach (var p in parameters)
{
    graphicsState.Add(p);
}
```

> **Why this matters:** 將 `ca` 設為 `0.5` 代表 PDF 渲染器會以 50% 不透明度繪製填充形狀。依需求調整數值即可。`BM` 為可選項，但能說明透明內容如何與底層物件混合。

## 步驟 5：將新圖形狀態註冊到 ExtGState 字典

每個圖形狀態必須有唯一名稱（例如 `"GS0"`）。若要覆寫既有狀態可重複使用名稱，但使用全新識別碼可避免意外副作用。

```csharp
// Step 5: Add the graphics state to ExtGState with a unique name
extGStateDict.Add("GS0", graphicsState);
```

> **Why this matters:** 狀態儲存後，即可在頁面內容串流中使用 `/GS0` 操作符引用。這正是實際**如何為繪圖指令加入透明度**的機制。

## 步驟 6：儲存已修改的 PDF

更新資源字典後，將變更寫回磁碟。您可以覆寫原檔或另存新檔；範例會產生 `output.pdf` 以保留來源檔。

```csharp
// Step 6: Save the modified PDF
pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **Why this matters:** `Save` 方法會將記憶體中的物件（包括新圖形狀態）序列化成有效的 PDF 檔案。這就是**如何更改不透明度**以及**儲存已修改 PDF**文件的最後一步。

## 完整、可執行的範例

將所有片段組合起來，即可得到一個可直接貼入主控台應用程式的自包含程式。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Collections;

class Program
{
    static void Main()
    {
        // Path to the source PDF
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";

        // Load the document
        using var pdfDocument = new Document(pdfPath);

        // Work with the first page
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState exists
        CosCosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosCosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourcesEditor.Add("ExtGState", extGStateDict);
        }

        // Create a new graphics state with opacity settings
        var graphicsState = CosCosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // blend mode
        };
        foreach (var p in parameters)
            graphicsState.Add(p);

        // Add the state to ExtGState under the name "GS0"
        extGStateDict.Add("GS0", graphicsState);

        // Save the result
        pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");

        Console.WriteLine("Opacity changed and PDF saved successfully.");
    }
}
```

### 預期結果

在任何 PDF 檢視器中開啟 `output.pdf`。任何之後引用圖形狀態 `GS0`（例如使用 `/GS0 gs` 繪製的矩形）都會以**50 % 填充不透明度**顯示，而描邊仍保持完全不透明。若透過 Aspose.Pdf 的 `Page.Contents.Add` API 加入此類繪圖指令，您將立即看到透明效果。

## 處理多頁與多個圖形狀態

- **Multiple pages:** 迭代 `pdfDocument.Pages`，對每個需要影響的頁面重複步驟 2‑5。若不同頁面需要不同不透明度，請使用不同的狀態名稱（`GS1`、`GS2`…）。
- **Re‑using an existing state:** 若 PDF 已含名為 `"GS0"` 的狀態且只想修改其不透明度，可直接使用 `extGStateDict["GS0"]` 取得，而非建立新條目。
- **Performance tip:** 大量圖形狀態會增加檔案大小。將相同的不透明度設定合併為單一狀態，並在多頁中共用。

## 常見陷阱與避免方式

| Issue | Cause | Fix |
|-------|-------|-----|
| `KeyNotFoundException` on `"ExtGState"` | PDF 缺少該字典。 | 如步驟 3 所示建立字典。 |
| Transparency not visible | 內容串流未引用新狀態。 | 在繪圖指令前插入 `/GS0 gs`，或使用 Aspose.Pdf 的 `Graphics` API 並傳入 `GraphicsState` 參數。 |
| Output PDF is corrupted | 嘗試儲存至唯讀資料夾。 | 確認目標路徑可寫入，且不是仍在開啟的同一檔案。 |
| Opacity values > 1 or < 0 | 錯把百分比當成小數傳入。 | 使用介於 `0.0` 與 `1.0` 之間的數值。 |

## 下一步

現在您已掌握**如何更改不透明度**與**如何為圖形加入透明度**，可以進一步探索以下相關主題：

- **如何為影像加入透明度**，使用 `Image` 物件與 `Transparency` 屬性。
- 合併多個 PDF 同時保留圖形狀態。
- 使用 **儲存已修改 PDF** 的選項，如 `PdfSaveOptions`，以壓縮或加密結果。

嘗試不同的 `ca` 與 `CA` 數值、以及 `"Multiply"`、`"Screen"` 等混合模式，觀察它們對視覺輸出的影響。本文所涵蓋的技巧為進階 PDF 樣式設計奠定了堅實基礎。


## 您接下來應該學什麼？

以下教學與本指南的技術緊密相關，能幫助您在專案中進一步運用 API 功能與替代實作方式。

- [如何使用 Aspose.PDF for .NET 為 PDF 添加旋轉影像浮水印](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)
- [如何使用 Aspose.PDF for .NET 為 PDF 添加頁面印章：完整指南](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [如何使用 Aspose.PDF for .NET 為 PDF 添加頁碼印章 | 浮水印與背景](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}