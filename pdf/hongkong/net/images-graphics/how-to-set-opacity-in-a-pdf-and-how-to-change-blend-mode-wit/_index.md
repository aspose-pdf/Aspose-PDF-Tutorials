---
category: general
date: 2026-11-19
description: 學習如何使用 Aspose.Pdf 在 PDF 中設定不透明度與變更混合模式。逐步 C# 教學，打造透明圖形。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set opacity
- how to change blend
- Aspose.Pdf graphics state
- PDF transparency C#
- modify PDF resources
language: zh-hant
lastmod: 2026-11-19
og_description: 使用 Aspose.Pdf 在 PDF 中設定不透明度與變更混合模式。跟隨這個完整的 C# 教程，使圖形透明。
og_image_alt: Code editor showing C# example that sets PDF opacity and blend mode
og_title: 如何在 PDF 中使用 Aspose.Pdf 設定不透明度並更改混合模式
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to set opacity and how to change blend mode in a PDF using
    Aspose.Pdf. Step‑by‑step C# guide for transparent graphics.
  headline: How to set opacity in a PDF and how to change blend mode with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- Transparency
title: How to set opacity in a PDF and how to change blend mode with Aspose.Pdf
url: /zh-hant/net/images-graphics/how-to-set-opacity-in-a-pdf-and-how-to-change-blend-mode-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 PDF 中使用 Aspose.Pdf 設定不透明度與變更混合模式

如果您需要為 PDF 內的物件 **設定不透明度**，本指南將示範完整步驟。它同時說明 **如何變更混合模式**，讓新的圖形狀態能正確與頁面內容混合。

在本教學中，您將會：

* 使用 Aspose.Pdf 載入既有 PDF。
* 取得頁面的資源字典。
* 建立一個定義筆畫不透明度、填充不透明度與混合模式的新圖形狀態字典。
* 將圖形狀態加入 `ExtGState` 集合。
* 儲存更新後的 PDF。

不需要任何外部工具——只要 Aspose.Pdf for .NET 套件與 .NET 開發環境即可。

## 前置條件

* .NET 6.0 或更新版本（此程式碼亦相容 .NET Framework 4.6+）。
* Aspose.Pdf for .NET NuGet 套件（`Install-Package Aspose.Pdf`）。
* 位於可寫入資料夾中的 PDF 檔案 `input.pdf`（將 `YOUR_DIRECTORY` 替換為實際路徑）。

## 步驟 1：安裝 Aspose.Pdf 並建立專案

建立一個新的 Console 專案，並加入 Aspose.Pdf 參考：

```bash
dotnet new console -n PdfOpacityDemo
cd PdfOpacityDemo
dotnet add package Aspose.Pdf
```

專案檔現在已包含 Aspose.Pdf 程式集，提供稍後會使用的 `Document`、`DictionaryEditor` 與 `CosPdfDictionary` 類別。

## 步驟 2：載入 PDF 文件

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Engine;
using Aspose.Pdf.Engine.Data;

// Load the existing PDF
Document pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

**為什麼這很重要：** 載入文件會在記憶體中建立可供修改的表示。若未執行此步驟，資源字典將無法存取。

## 步驟 3：取得第一頁及其資源字典

```csharp
// Retrieve the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];

// Open the page’s resource dictionary for editing
DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);
```

**說明：** `Resources` 字典包含字型、影像以及 `ExtGState` 集合等物件。編輯它即可注入控制不透明度與混合的全新圖形狀態。

## 步驟 4：存取（或建立）ExtGState 字典

```csharp
// Try to get the existing ExtGState dictionary; create it if missing
CosPdfDictionary extGStateDict = null;
if (resourceEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create an empty ExtGState dictionary and add it to resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourceEditor["ExtGState"] = extGStateDict;
}
```

**為什麼需要此步驟：** `ExtGState` 條目保存圖形狀態物件。若該條目不存在，必須先建立才能加入新條目。

## 步驟 5：建立具備不透明度與混合模式的圖形狀態

```csharp
// Create a new empty graphics state dictionary
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Set stroke opacity (CA) – 1 = fully opaque, 0 = fully transparent
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Set fill opacity (ca) – 0.5 = 50 % transparent fill
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Set blend mode (BM) – "Normal" is the default; other options: Multiply, Screen, Overlay, etc.
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

**此作法解決問題的方式：**  
* `CA` 控制筆畫路徑的不透明度（例如線條）。  
* `ca` 控制填充圖形的不透明度（例如矩形）。  
* `BM` 定義新圖形如何與現有頁面內容合成。變更混合模式即是 **如何變更混合** 的實作方式。

## 步驟 6：將圖形狀態註冊至 ExtGState 集合

```csharp
// Use a unique key for the new graphics state (e.g., GS0)
extGStateDict.Add("GS0", newGraphicsState);
```

現在頁面可以透過名稱 `/GS0` 參考此圖形狀態。任何在內容串流中設定 `/GS0 gs` 的指令，都會使用此不透明度與混合模式。

## 步驟 7：將圖形狀態套用至既有內容（可選）

若要修改既有的繪圖指令，可將圖形狀態運算子前置於頁面的內容串流：

```csharp
// Retrieve the content stream as a string
string pageContent = firstPage.Contents[1].ToString();

// Prepend the graphics state operator
string modifiedContent = "GS0 gs\n" + pageContent;

// Replace the original content
firstPage.Contents[1].Replace(modifiedContent);
```

**注意：** 此步驟為可選。若之後再加入新繪圖指令，只需在串流開頭使用 `GS0 gs` 即可。

## 步驟 8：儲存已修改的 PDF

```csharp
pdfDocument.Save(@"YOUR_DIRECTORY\out.pdf");
```

產生的 `out.pdf` 內含一個填充不透明度為 50 % 且混合模式為 `Normal` 的圖形狀態。任何使用 `/GS0 gs` 的內容都會以指定的透明度呈現。

## 完整範例程式

以下是可直接貼到 `Program.cs` 並執行的完整程式碼：

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Engine;
using Aspose.Pdf.Engine.Data;

class Program
{
    static void Main()
    {
        // 1. Load the PDF document
        Document pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // 2. Get the first page and its resource dictionary
        Page firstPage = pdfDocument.Pages[1];
        DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);

        // 3. Access or create the ExtGState dictionary
        CosPdfDictionary extGStateDict;
        if (resourceEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourceEditor["ExtGState"] = extGStateDict;
        }

        // 4. Define a new graphics state with opacity and blend mode
        CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity (fully opaque)
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity (50 % transparent)
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode (Normal)

        // 5. Add the graphics state to ExtGState collection
        extGStateDict.Add("GS0", newGraphicsState);

        // 6. (Optional) Apply the graphics state to existing page content
        if (firstPage.Contents.Count > 0)
        {
            string original = firstPage.Contents[1].ToString();
            string withGs = "GS0 gs\n" + original;
            firstPage.Contents[1].Replace(withGs);
        }

        // 7. Save the updated PDF
        pdfDocument.Save(@"YOUR_DIRECTORY\out.pdf");

        Console.WriteLine("PDF updated successfully – opacity set and blend mode changed.");
    }
}
```

### 預期輸出

執行程式會印出：

```
PDF updated successfully – opacity set and blend mode changed.
```

當您在 PDF 檢視器中開啟 `out.pdf` 時，使用新定義圖形狀態的圖形會以 50 % 填充透明度顯示，而筆畫仍保持完全不透明。混合模式 `Normal` 確保圖形在合成時不產生特殊效果。您也可以將 `"Normal"` 改為 `"Multiply"` 或 `"Screen"`，以觀察 **如何變更混合** 產生的不同視覺結果。

## 常見問題與邊緣情況

| 問題 | 解答 |
|----------|--------|
| **我可以為多個物件設定不同的不透明度值嗎？** | 可以。建立額外的圖形狀態（例如 `GS1`、`GS2`），設定不同的 `ca`/`CA` 值，並在繪製每個物件前引用相應的名稱。 |
| **如果 PDF 已經有名為 `GS0` 的 ExtGState 條目該怎麼辦？** | 使用唯一的鍵名（如 `GS1`、`MyOpacityState` 等），或在不再需要舊定義時直接覆寫。 |
| **混合模式只能是 `Normal` 嗎？** | 不是。有效的名稱包括 `Multiply`、`Screen`、`Overlay`、`Darken`、`Lighten`、`ColorDodge`、`ColorBurn`、`HardLight`、`SoftLight`、`Difference`、`Exclusion`，以及 `Hue`、`Saturation`、`Color`、`Luminosity`。 |
| **這能套用在加密的 PDF 上嗎？** | Aspose.Pdf 可在提供密碼的情況下開啟加密 PDF（使用 `Document(string, LoadOptions)`）。解密後的圖形狀態操作方式相同。 |
| **變更會影響所有頁面嗎？** | 範例僅修改第一頁。若要影響每一頁，請遍歷 `pdfDocument.Pages`，對每頁重複步驟 2‑6。 |

## 專業小技巧

* **重複使用圖形狀態：** 只需新增一次圖形狀態，於多個頁面引用，可減少檔案大小。  
* **效能考量：** 在記憶體中修改大型 PDF 可能佔用大量記憶體。若僅需小幅變更，可使用 `pdfDocument.Save(..., SaveOptions)` 搭配增量更新。  
* **測試混合模式：** 並非所有 PDF 檢視器都能一致呈現每種混合模式。建議在 Adobe Acrobat Reader 以及其他檢視器（如 Foxit）中測試，以確保視覺一致性。

## 結論

您現在已掌握 **如何設定不透明度** 與 **如何變更混合模式**，並能使用 Aspose.Pdf for .NET 在 PDF 中進行精細的透明度與合成控制，無需外部工具即可製作專業級的 PDF 圖形。

接下來，您可以進一步探索：

* 為具有透明背景的影像設定不透明度（`how to set opacity` on images）。  
* 建立可重複使用的內容串流，引用新建的圖形狀態。  
* 使用其他混合模式（`how to change blend` 為 `Multiply` 或 `Screen`）以創造更多視覺效果。

祝開發順利，讓您的 PDF 更具視覺動感！

## 接下來該學什麼？

以下教學與本指南所示技術密切相關，能幫助您進一步掌握 API 功能並探索其他實作方式：

- [How to Change Opacity in PDF with Aspose.PDF – Complete Guide](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-change-opacity-in-pdf-with-aspose-pdf-complete-guide/)
- [How to change opacity in a PDF with Aspose.Pdf for .NET](/pdf/english/net/images-graphics/how-to-change-opacity-in-a-pdf-with-aspose-pdf-for-net/)
- [How to change PDF transparency using Aspose.Pdf in C#](/pdf/english/net/programming-with-operators/how-to-change-pdf-transparency-using-aspose-pdf-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}