---
category: general
date: 2026-09-24
description: 學習如何在 C# 中使用 Aspose.Pdf 更改 PDF 透明度。本分步指南涵蓋 PDF 不透明度、混合模式與圖形狀態編輯。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.Pdf graphics state
- PDF opacity
- C# PDF manipulation
- blend mode PDF
- modify PDF resources
language: zh-hant
lastmod: 2026-09-24
og_description: 使用 Aspose.Pdf 在 C# 中更改 PDF 透明度。遵循本指南編輯 PDF 的不透明度、混合模式及圖形狀態，以獲得專業文件輸出。
og_image_alt: Screenshot showing C# code that changes PDF transparency
og_title: 在 C# 中更改 PDF 透明度 – 完整 Aspose.Pdf 指南
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Learn how to change PDF transparency in C# with Aspose.Pdf. This step‑by‑step
    guide covers PDF opacity, blend mode and graphics state editing.
  headline: How to change PDF transparency in C# using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- C#
- Aspose.Pdf
- Transparency
title: 如何在 C# 中使用 Aspose.Pdf 更改 PDF 透明度
url: /zh-hant/net/programming-with-operators/how-to-change-pdf-transparency-in-c-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.Pdf 更改 PDF 透明度

如果您需要在 .NET 專案中**更改 PDF 透明度**，本指南將向您展示如何使用 Aspose.Pdf 完成此操作。您將看到一個完整且可執行的範例，該範例會修改 PDF 不透明度、設定混合模式，並更新頁面的圖形狀態字典。

當您需要加入浮水印、覆蓋圖形或自訂視覺效果時，更改 PDF 透明度是一項常見需求。在本教學中，您將學會編輯 **Aspose.Pdf 圖形狀態**、調整 **PDF 不透明度**，以及使用 **PDF 混合模式** 設定——全部透過簡潔的 C# 程式碼完成。

## 前置條件

* .NET 6.0 或更新版本已安裝  
* Aspose.Pdf for .NET 授權（或臨時評估金鑰）  
* 一個名為 `input.pdf` 的 PDF 檔案，放在您可以以 `YOUR_DIRECTORY` 參照的資料夾中  
* 具備基本的 C# 與 Visual Studio（任何 IDE 均可）使用經驗  

除了 `Aspose.Pdf` 之外，無需額外的 NuGet 套件。由於 Aspose.Pdf 為跨平台套件，程式碼可在 Windows、Linux 或 macOS 上執行。

## 更改 PDF 透明度 – 步驟 1：開啟 PDF 文件

第一步是載入來源 PDF。使用 `using` 區塊可確保檔案句柄會自動釋放。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System.Collections.Generic;

string inputPath  = @"YOUR_DIRECTORY\input.pdf";
string outputPath = @"YOUR_DIRECTORY\output.pdf";

using (var document = new Document(inputPath))
{
    // The document is now ready for manipulation.
```

開啟文件是任何 **C# PDF 操作** 任務的基礎。如果找不到檔案，Aspose.Pdf 會拋出 `FileNotFoundException`，因此在執行程式前請再次確認路徑。

## 使用 Aspose.Pdf 圖形狀態存取頁面資源

接下來，取得第一頁及其資源字典。資源字典包含字型、影像以及控制圖形參數的 **ExtGState** 條目等物件。

```csharp
    // Step 2: Get the first page of the document
    var page = document.Pages[1];

    // Step 3: Access the page's resource dictionary for editing
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

`DictionaryEditor` 類別提供了讀寫 PDF 字典的便利封裝。我們此處聚焦於 **ExtGState** 字典，因為它儲存了透明度設定。

## 建立並設定新的圖形狀態以調整 PDF 不透明度

現在我們建立一個全新的圖形狀態字典。此字典將保存定義筆畫不透明度 (`CA`)、填充不透明度 (`ca`) 以及混合模式 (`BM`) 的參數。

```csharp
    // Step 4: Retrieve the existing ExtGState dictionary (graphics states)
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

    // Step 5: Create a new empty graphics state dictionary
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

    // Step 6: Define graphics state parameters (stroke opacity, fill opacity, blend mode)
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),            // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),          // Fill opacity (50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))       // Blend mode PDF (standard normal blending)
    };

    // Step 7: Add each parameter to the new graphics state dictionary
    foreach (var param in parameters)
        newGraphicsState.Add(param);
```

* **`CA`** 控制筆畫操作（線條、邊框）的不透明度。  
* **`ca`** 控制填充操作（填滿形狀、文字）的不透明度。  
* **`BM`** 用於選擇混合模式；預設為 `"Normal"`，但您也可以使用 `"Multiply"` 或 `"Screen"` 來產生藝術效果。  

這些設定是 **PDF 不透明度** 操作的核心。依照您的視覺設計調整數值——`0` 代表完全透明，`1` 代表完全不透明。

## 插入圖形狀態並儲存文件

在建立新狀態後，我們將其以唯一名稱（`GS0`）加入現有的 **ExtGState** 字典。最後，將修改過的 PDF 儲存下來。

```csharp
    // Step 8: Insert the new graphics state into the ExtGState dictionary with a name
    extGState.Add("GS0", newGraphicsState);

    // Step 9: Save the modified PDF document
    document.Save(outputPath);
}
```

當 PDF 在檢視器中開啟時，任何引用 `GS0` 的內容都會以設定的透明度呈現。您之後也可以透過繪圖指令的 `GraphicsState` 屬性（例如 `page.Contents.Add(new TextFragment(...){ GraphicsState = "GS0" })`）將此圖形狀態套用到特定物件上。

## 驗證結果

在支援透明度的檢視器（如 Adobe Acrobat Reader、Foxit 或其他 PDF 閱讀器）中開啟 `output.pdf`。您應該會看到第一頁的填充元素以 50 % 不透明度呈現，而筆畫則保持完全不透明。如果未看到變化，請確認該頁面確實使用了新的圖形狀態——否則，您可以明確將 `GS0` 指派給想要影響的物件。

![Change PDF transparency in C# code example](path/to/image.png){: .img-responsive alt="在 C# 程式碼中更改 PDF 透明度的範例"}

*上圖顯示了完整的 C# 程式碼範例，用於更改 PDF 透明度。*

## 常見變化與邊緣情況

| 情況 | 如何調整程式碼 |
|-----------|-----------------------|
| **多頁面** | 對 `document.Pages` 進行迴圈，對每一頁重複步驟 2‑8。 |
| **不同的混合模式** | 將 `"Normal"` 替換為 `"Multiply"`、`"Screen"` 或任何 PDF 標準的混合名稱。 |
| **較高的填充不透明度** | 將 `new CosPdfNumber(0.5)` 改為介於 `0` 與 `1` 之間的值。 |
| **不存在 ExtGState** | 如果 `resourcesEditor["ExtGState"]` 回傳 `null`，則建立新字典：`var extGState = CosPdfDictionary.CreateEmptyDictionary(document); resourcesEditor["ExtGState"] = extGState;` |

這些變化展示了使用 Aspose.Pdf **修改 PDF 資源** 的彈性。透過調整參數，您可以在 PDF 中產生浮水印、半透明覆蓋層或自訂 UI 元素。

## 完整、可執行的範例

以下是完整的程式碼，您可以直接複製貼上到新的 Console App 專案中。它包含所有必要的 `using` 指示、錯誤處理與註解。



## 接下來您應該學習什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上進一步說明。每個資源皆提供完整可運作的程式碼範例與逐步說明，協助您精通其他 API 功能，並在自己的專案中探索替代實作方式。

- [使用 Aspose.PDF 更改 PDF 不透明度 – 完整 C# 指南](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [在 C# 中更改 PDF 不透明度 – 完整 Aspose 指南](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-in-c-complete-aspose-guide/)
- [使用 Aspose 為 PDF 添加透明度 – 完整 C# 指南](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}