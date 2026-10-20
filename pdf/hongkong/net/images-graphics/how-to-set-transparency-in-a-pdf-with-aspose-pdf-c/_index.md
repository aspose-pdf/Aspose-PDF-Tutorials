---
category: general
date: 2026-10-13
description: 了解如何使用 Aspose.Pdf for C# 在 PDF 中設定透明度。另請參閱如何儲存已修改的 PDF 以及變更填充透明度。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set transparency
- save modified pdf
- change fill alpha
- set fill opacity
- edit pdf resources
language: zh-hant
lastmod: 2026-10-13
og_description: 如何在使用 Aspose.Pdf for C# 的 PDF 中設定透明度。請參考本指南編輯 PDF 資源、變更填充 Alpha，並儲存已修改的
  PDF 檔案。
og_image_alt: Screenshot of a PDF page showing transparent graphics applied with Aspose.Pdf
  in C#
og_title: 如何使用 Aspose.Pdf C# 在 PDF 中設定透明度 – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  headline: How to set transparency in a PDF with Aspose.Pdf C#
  type: TechArticle
- description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  name: How to set transparency in a PDF with Aspose.Pdf C#
  steps:
  - name: Load the PDF document
    text: '```csharp using Aspose.Pdf; using System.Collections.Generic;'
  - name: Edit PDF resources to add a graphics state
    text: '```csharp // Get the first page (pages are 1‑based) Page firstPage = pdfDocument.Pages[1];'
  - name: Change fill alpha and set fill opacity
    text: '```csharp // Create an empty graphics state dictionary CosPdfDictionary
      newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);'
  - name: Add the new graphics state to the ExtGState dictionary
    text: '```csharp // Register the new state under the name "GS0" extGStateDict.Add("GS0",
      newGraphicsState); ```'
  - name: (Optional) Apply the graphics state in a content stream
    text: 'If you want to draw a rectangle using the new fill opacity, add the following
      after the previous steps:'
  - name: Save modified PDF
    text: '```csharp // Persist the changes to a new file pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
      ```'
  - name: Next steps
    text: '* Explore other blend modes (`Multiply`, `Screen`, etc.) by changing the
      `BM` entry. * Adjust stroke alpha (`CA`) to create semi‑transparent outlines.
      * Combine multiple graphics states to build a library of reusable visual effects.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- Transparency
title: 如何在 PDF 中使用 Aspose.Pdf C# 設定透明度
url: /zh-hant/net/images-graphics/how-to-set-transparency-in-a-pdf-with-aspose-pdf-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 PDF 中使用 Aspose.Pdf C# 設定透明度

如果您需要在使用 C# 的 PDF 中設定透明度，本教學將示範完整步驟。您還將學習如何在不離開 Aspose.Pdf 環境的情況下儲存已修改的 PDF 檔案以及變更填充透明度 (fill alpha)。

本指南將說明載入文件、編輯 PDF 資源、建立定義填充不透明度的圖形狀態 (graphics state) 以及持久化變更的過程。無需外部工具；所有操作皆在標準 .NET 專案內執行。

## 前置條件

* 已安裝 .NET 6.0 或更新版本  
* 有效的 Aspose.Pdf for .NET 授權（或免費評估金鑰）  
* 位於已知目錄的輸入 PDF 檔案  

您可以透過 NuGet 新增 Aspose.Pdf 套件：

```bash
dotnet add package Aspose.Pdf
```

## 如何在 PDF 中設定透明度

本節包含核心實作。每一步都說明 **為何** 需要此程式碼，而不僅是 **它做了什麼**。

### 步驟 1：載入 PDF 文件

```csharp
using Aspose.Pdf;
using System.Collections.Generic;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*為何需要此步驟？*  
`Document` 代表記憶體中的整個 PDF 檔案。開啟檔案後，您即可存取頁面、資源以及將要修改的低階物件。

### 步驟 2：編輯 PDF 資源以新增圖形狀態

```csharp
// Get the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];

// Create an editor for the page's resource dictionary
DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);

// Retrieve the ExtGState dictionary; it holds graphics state objects
CosPdfDictionary extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
```

*為何需要此步驟？*  
PDF 頁面在資源字典 (resource dictionary) 中儲存可重複使用的物件——字型、影像與圖形狀態。`ExtGState` 條目包含透明度設定。編輯此字典即可加入新狀態，讓頁面參照。

### 步驟 3：變更填充透明度 (fill alpha) 並設定填充不透明度

```csharp
// Create an empty graphics state dictionary
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the graphics state entries
var graphicsStateEntries = new[]
{
    // Stroke alpha (CA) – fully opaque
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    // Fill alpha (ca) – 50 % transparent
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // Blend mode (BM) – normal composition
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

// Populate the new graphics state
foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*為何需要此步驟？*  
`ca` 控制 **填充不透明度**，而 `CA` 控制 **描邊不透明度**。將 `ca` 設為 `0.5` 會使填充形狀呈現 50 % 透明。`BM` 條目用於選擇混合模式；`"Normal"` 為標準透明度最常使用的選項。

### 步驟 4：將新圖形狀態加入 ExtGState 字典

```csharp
// Register the new state under the name "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

*為何需要此步驟？*  
為圖形狀態命名（`"GS0"`）可讓頁面的內容串流使用 `gs` 運算子參照它。完成註冊後，頁面即可套用剛才定義的透明度。

### 步驟 5：（可選）在內容串流中套用圖形狀態

如果您想使用新設定的填充不透明度繪製矩形，請在前述步驟之後加入以下程式碼：

```csharp
// Create a content stream that uses the new graphics state
string cs = @"
q               % Save graphics state
/GS0 gs         % Apply the graphics state defined earlier
0 0 200 100 re  % Define a rectangle (x, y, width, height)
0.2 0.6 0.8 rg  % Set fill color (RGB)
f               % Fill the rectangle using the current graphics state
Q               % Restore graphics state
";

firstPage.Contents.Add(new Aspose.Pdf.Operator.GsContent(cs));
```

*為何需要此步驟？*  
`q`/`Q` 運算子用於保存與還原圖形狀態，確保透明度僅影響指定的繪圖指令。`gs` 運算子則切換至名為 `"GS0"` 的圖形狀態。

### 步驟 6：儲存已修改的 PDF

```csharp
// Persist the changes to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*為何需要此步驟？*  
儲存會將更新後的資源字典與任何新內容串流寫入磁碟。最終產生的檔案（`output.pdf`）即包含前一步所定義的透明矩形。

## 完整可執行範例

將上述各部份組合起來，以下是一個可編譯執行的完整程式範例：

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using System.Collections.Generic;

class SetTransparencyDemo
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Access the first page and its resources
        Page firstPage = pdfDocument.Pages[1];
        var resourceEditor = new DictionaryEditor(firstPage.Resources);
        var extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();

        // Create a new graphics state with 50 % fill opacity
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var graphicsStateEntries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke alpha
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill alpha
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var entry in graphicsStateEntries)
            newGraphicsState.Add(entry);

        // Register the graphics state as "GS0"
        extGStateDict.Add("GS0", newGraphicsState);

        // Optional: draw a rectangle using the new transparency
        string cs = @"
q
/GS0 gs
0 0 200 100 re
0.2 0.6 0.8 rg
f
Q
";
        firstPage.Contents.Add(new GsContent(cs));

        // Save the modified PDF
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

**預期結果** – `output.pdf` 會顯示一個填滿淡紫色且 50 % 透明的矩形，讓任何背景內容可部分可見。

## 常見問題與邊緣情況

* **我可以變更描邊不透明度而非填充不透明度嗎？**  
  將 `CA`（大寫）設定為介於 `0`（完全透明）與 `1`（完全不透明）之間的數值。範例已將 `CA` 設為 `1`，表示描邊保持不透明。

* **如果頁面尚未有 ExtGState 字典，該怎麼辦？**  
  `resourceEditor["ExtGState"]` 會自動建立一個空字典。加入 `"GS0"` 仍可正常運作。

* **圖形狀態可以在多個頁面間重複使用嗎？**  
  可以。只要將條目加入文件的資源字典，任何參照 `"GS0"` 的頁面都會繼承相同的透明度設定。

* **這種做法與使用高階 `Graphics` API 有何不同？**  
  編輯低階資源字典可讓您精確控制 PDF 內部結構，且因避免嵌入額外物件而產生較小的檔案。

## 結論

您現在已了解如何使用 Aspose.Pdf for C# **在 PDF 中設定透明度**。本教學涵蓋了編輯 PDF 資源、變更填充透明度、設定填充不透明度以及儲存已修改的 PDF。掌握此基礎後，您可以嘗試不同的混合模式、將透明度套用於文字，或為複雜文件建立可重複使用的圖形狀態。

### 往後步驟

* 透過變更 `BM` 條目來探索其他混合模式（`Multiply`、`Screen` 等）。  
* 調整描邊透明度 (`CA`) 以產生半透明輪廓。  
* 結合多個圖形狀態，建立可重複使用的視覺效果庫。

歡迎在留言區分享您的成果或提出問題。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索替代實作方式。

- [如何使用 Aspose.PDF for .NET 自訂 PDF：設定頁邊距與繪製線條](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [如何使用 Aspose-PDF for .NET 設定 PDF 中的影像大小](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [如何使用 Aspose.PDF for .NET 設定 PDF 權限：完整指南](/pdf/english/net/security-permissions/set-pdf-privileges-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}