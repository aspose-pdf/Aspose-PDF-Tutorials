---
category: general
date: 2026-09-18
description: 學習如何在 C# 中使用 Aspose.PDF 建立空的 PDF 字典。本分步指南涵蓋 ExtGState、圖形狀態以及 CosPdfDictionary
  的操作。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.PDF
- ExtGState dictionary
- graphics state
- CosPdfDictionary
- PDF manipulation C#
language: zh-hant
lastmod: 2026-09-18
og_description: 使用 Aspose.PDF 在 C# 中建立空的 PDF 字典。跟隨本完整教學，編輯 ExtGState 與圖形狀態字典。
og_image_alt: Screenshot showing creation of an empty PDF dictionary in C#
og_title: 在 C# 中建立空的 PDF 字典 – 完整的 Aspose.PDF 指南
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn to create empty PDF dictionary in C# using Aspose.PDF. This step‑by‑step
    guide covers ExtGState, graphics state, and CosPdfDictionary manipulation.
  headline: How to create empty PDF dictionary with Aspose.PDF in C#
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: 如何在 C# 中使用 Aspose.PDF 建立空的 PDF 字典
url: /zh-hant/net/programming-with-document/how-to-create-empty-pdf-dictionary-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.PDF 建立空的 PDF 字典

如果您需要在處理 PDF 檔案時 **create empty PDF dictionary**，本指南將精確說明如何使用 Aspose.PDF for .NET 來完成。無論您是調整透明度、混合模式，或任何自訂圖形狀態，以下步驟都能讓您安全且有效地編輯 `ExtGState` 字典。

在本教學中您將學會：

* 使用 Aspose.PDF 載入 PDF 文件。
* 取得第一頁的資源以及現有的 `ExtGState` 字典。
* 建立全新的空 `CosPdfDictionary` 並填入圖形狀態條目。
* 儲存已修改的 PDF，且不遺失任何原始內容。

此解決方案適用於任何至少包含一頁的 PDF，且僅需 Aspose.PDF 套件（版本 23.10 或更新）。

## 前置條件

* .NET 6.0 或更新版本（程式碼亦可在 .NET Framework 4.8 上執行）。
* 參考 **Aspose.PDF** NuGet 套件。
* 位於 `YOUR_DIRECTORY/input.pdf` 的輸入 PDF 檔案。
* 具備 C# 基礎以及 PDF 概念（如資源與圖形狀態）的熟悉度。

> **專業提示：** 處理大型 PDF 時，請將 `Document` 物件包在 `using` 區塊中，以確保檔案句柄能即時釋放。

## Step 1: 載入 PDF 文件

第一個動作是開啟來源檔案。Aspose.PDF 會將整個文件讀入記憶體，讓您得以編輯內部物件。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

*Why this matters*: 載入文件會建立可變更的物件模型。若未執行此步驟，您將無法取得進行字典操作所需的頁面資源。

## Step 2: 取得第一頁的資源

每一頁都會保存一個 `Resources` 字典，內含字型、影像與圖形狀態。存取它可取得 `DictionaryEditor`，簡化讀寫操作。

```csharp
// Step 2: Get the resources of the first page
Page firstPage = pdfDocument.Pages[1];
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Why this matters*: `ExtGState` 字典位於頁面資源內。編輯錯誤的字典不會對渲染產生任何影響。

## Step 3: 找到現有的 ExtGState 字典

`ExtGState` 條目可能已包含圖形狀態物件。我們將其以 `CosPdfDictionary` 形式取得，以便加入新條目。

```csharp
// Step 3: Access the existing ExtGState dictionary
CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

如果 `ExtGState` 條目不存在，稍後指派新字典時 Aspose.PDF 會自動建立一個空字典。

## Step 4: **Create empty PDF dictionary** 用於新的圖形狀態

此處我們建立全新的 `CosPdfDictionary`——即 **create empty PDF dictionary** 操作的核心，然後填入標準的圖形狀態鍵：

* `CA` – 描邊不透明度。
* `ca` – 填充不透明度。
* `BM` – 混合模式。

```csharp
// Step 4: Create a new graphics state dictionary and define its entries
CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

KeyValuePair<string, ICosPdfPrimitive>[] graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),          // Stroke opacity
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),       // Fill opacity
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))    // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

*Why this matters*: 透過明確定義每個條目，您即可控制頁面上物件的混合與渲染方式。此字典在加入鍵之前是 **empty**，符合在填入內容前 **create empty PDF dictionary** 的需求。

## Step 5: 將新圖形狀態加入 ExtGState 字典

每個圖形狀態必須擁有唯一名稱（例如 `GS0`）。我們將剛建立的字典插入該名稱下。

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary with a unique name
extGStateDict.Add("GS0", graphicsStateDict);
```

若需要多個狀態，請持續新增 `GS1`、`GS2` 等條目，並確保每個名稱在 `ExtGState` 字典中唯一。

## Step 6: 儲存更新後的 PDF 文件

最後，將變更寫回磁碟。原始檔案保持不變，因為我們儲存至新路徑。

```csharp
// Step 6: Save the updated PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

產生的 `output.pdf` 現在包含額外的圖形狀態 (`GS0`)，您可以在任何頁面的內容串流中使用 `/GS0` 運算子來參照它。

## 完整範例程式

將所有步驟結合，即可得到一個可立即執行的自包含程式。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources
            Page firstPage = pdfDocument.Pages[1];
            DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Get (or create) ExtGState dictionary
            CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Build a new empty PDF dictionary for graphics state
            CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var entry in entries)
                graphicsStateDict.Add(entry);

            // Insert the new graphics state with a unique name
            extGStateDict.Add("GS0", graphicsStateDict);

            // Save the modified document
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

**Expected output**: 執行程式後，`output.pdf` 會與 `input.pdf` 具有相同的視覺內容。使用 Adobe Acrobat 或 PDF‑Tron 等工具檢視時，您會在第一頁的 `ExtGState` 字典下看到新條目 `GS0`。

## 常見變化與例外情況

| 情況 | 需要調整的地方 |
|-----------|----------------|
| **No existing ExtGState entry** | 將 `resourcesEditor["ExtGState"]` 改為 `new CosPdfDictionary(pdfDocument)`，再指派回 `firstPage.Resources["ExtGState"]`。 |
| **Multiple pages need the same state** | 將相同的 `GS0` 條目加入每一頁的 `ExtGState` 字典，或從共享資源物件引用該字典。 |
| **Different blend mode** | 將 `CosPdfName` 的值從 `"Normal"` 改為 `"Multiply"`、`"Screen"` 等，依需求選擇混合模式。 |
| **Higher opacity values** | 使用 `new CosPdfNumber(0.8)` 取代 `ca` 或 `CA`，以提升填充或描邊的不透明度。 |
| **Using a stream operator** | 在內容串流中，於繪圖操作前寫入 `"/GS0 gs"`，以套用新的圖形狀態。 |

## 效能考量

* **記憶體使用量** – 載入極大 PDF 會消耗與頁數成比例的記憶體。若僅需編輯第一頁，處理完畢後可考慮使用 `pdfDocument.Pages.Delete(pageNumber)` 釋放資源。
* **執行緒安全性** – Aspose.PDF 物件非執行緒安全。請在單一執行緒上執行字典編輯，或為每個執行緒建立獨立的 `Document` 實例。

## 結論

您現在已掌握如何使用 Aspose.PDF **create empty PDF dictionary**，將其填入圖形狀態條目，並附加至頁面的 `ExtGState` 字典。此技巧讓您能以 C# 細緻控制不透明度、混合模式以及其他渲染參數。

接下來，可探索如 **PDF manipulation C#**、為進階透明效果加入自訂 **ExtGState dictionary** 條目，或使用 **CosPdfDictionary** 變更字型、XObject 等其他資源類型。嘗試多個圖形狀態，以在 PDF 中打造更複雜的視覺效果。

## 接下來該學什麼？

以下教學與本指南所示技術密切相關，能進一步深化您的實作能力。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，並在專案中探索替代實作方式。

- [Create & Fill Rectangles in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)
- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [How to Add an Empty Page at the End of a PDF Using Aspose.PDF for .NET | Step-by-Step Guide](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}