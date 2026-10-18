---
category: general
date: 2026-10-17
description: 使用 Aspose.PDF for .NET 為 PDF 添加透明度，編輯 PDF 資源，並在單一可執行範例中儲存修改後的 PDF 檔案。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- save modified pdf
- edit pdf resources
- Aspose.PDF transparency
- C# PDF manipulation
language: zh-hant
lastmod: 2026-10-17
og_description: 使用 Aspose.PDF for .NET 為 PDF 添加透明度、編輯 PDF 資源，並以完整的 C# 範例儲存已修改的 PDF
  檔案。
og_image_alt: Screenshot showing a PDF with added transparency using Aspose.PDF in
  C#
og_title: 使用 Aspose.PDF 為 PDF 添加透明度 – 指南
schemas:
- author: Aspose
  dateModified: '2026-10-17'
  description: Add transparency to PDF with Aspose.PDF for .NET, edit PDF resources,
    and save modified PDF files in a single, runnable example.
  headline: How to add transparency to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- pdf
- aspnet
- csharp
title: 如何在 C# 中使用 Aspose.PDF 為 PDF 添加透明度
url: /zh-hant/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.PDF 為 PDF 添加透明度

如果您需要以程式方式 **add transparency to PDF**（為 PDF 添加透明度），本指南將向您展示使用 Aspose.PDF for .NET 的完整端到端解決方案。您將學習如何 **edit PDF resources**（編輯 PDF 資源）、建立自訂圖形狀態，並 **save modified PDF**（儲存已修改的 PDF）輸出，而無需離開您的 C# 專案。

處理 PDF 透明度通常感覺被低階 PDF 操作符隱藏。完成本教學後，您將擁有一個可直接複製貼上、執行，並可套用至多頁或不同混合模式的完整範例。

## 前置條件

- .NET 6.0（或任何較新的 .NET 版本）  
- Aspose.PDF for .NET NuGet 套件（`Aspose.Pdf`）  
- 基本的 C# 知識  
- 放置於可參考資料夾中的輸入 PDF 檔案（`input.pdf`）

> **Pro tip:** 在開始之前，使用 `dotnet add package Aspose.Pdf` 安裝套件。

## 步驟 1：載入 PDF 文件

第一步是開啟來源 PDF。Aspose.PDF 以 `Document` 物件表示 PDF，讓您可以存取頁面、資源與低階字典。

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Collections;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;   // for graphics‑state objects

// Path to the original PDF
string pdfPath = @"YOUR_DIRECTORY\input.pdf";

// Open the document in a using block so it disposes automatically
using (var document = new Document(pdfPath))
{
    // The rest of the steps are inside this block
```

*為什麼這很重要：* 以此方式開啟文件可確保在完成編輯後釋放檔案句柄，避免在之後 **save modified PDF**（儲存已修改的 PDF）時發生檔案鎖定問題。

## 步驟 2：存取第一頁及其資源字典

PDF 頁面將圖形物件（字型、影像、ExtGState 條目）儲存在 *資源字典* 中。若要變更不透明度，我們需要操作 `ExtGState` 子字典。

```csharp
    // Get the first page (pages are 1‑based in Aspose.PDF)
    Page page = document.Pages[1];

    // Obtain a mutable editor for the page's resources
    var resourcesEditor = new DictionaryEditor(page.Resources);

    // Retrieve the ExtGState dictionary; create it if missing
    var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                         ?? new CosPdfDictionary(document);
```

*為什麼這很重要：* 若原始 PDF 已包含 `ExtGState` 字典，我們會擴充它；否則會建立新的字典，以便安全地 **edit PDF resources**（編輯 PDF 資源）。

## 步驟 3：建立具透明度的新圖形狀態

圖形狀態（`ExtGState`）包含諸如描邊不透明度（`CA`）、填充不透明度（`ca`）以及混合模式（`BM`）等參數。我們會建立一個空字典，並填入所需的值。

```csharp
    // Create an empty ExtGState dictionary for the new entry
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

    // Define the transparency entries
    var entries = new[]
    {
        // CA – stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA",
            new CosPdfNumber(1)),

        // ca – fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca",
            new CosPdfNumber(0.5)),

        // BM – blend mode (Normal is the default)
        new KeyValuePair<string, ICosPdfPrimitive>("BM",
            new CosPdfName("Normal"))
    };

    // Add each entry to the new ExtGState dictionary
    foreach (var entry in entries)
        newGraphicsState.Add(entry);
```

*為什麼這很重要：* `ca` 條目是 **add transparency to PDF**（為 PDF 添加透明度）內容的關鍵。您可以調整數值（0 – 1）以控制物件的透視程度。

## 步驟 4：將圖形狀態插入頁面資源

我們必須為新的圖形狀態命名（例如 `"GS0"`）。之後內容串流可透過此名稱引用，以套用透明度。

```csharp
    // Add the new ExtGState under the name "GS0"
    extGStateDict.Add("GS0", newGraphicsState);

    // Ensure the modified ExtGState dictionary is written back to the page
    resourcesEditor["ExtGState"] = extGStateDict;
```

*為什麼這很重要：* 將 `"GS0"` 加入 `ExtGState` 字典後，任何選取此狀態的繪圖操作都會以設定的不透明度呈現。這是 **edit PDF resources**（編輯 PDF 資源）以實現透明度的核心。

## 步驟 5：將圖形狀態套用至頁面內容（可選）

如果您希望現有頁面內容自動使用新透明度，必須在頁面的內容串流前置加入圖形狀態運算子。以下程式碼示範如何使用 `gs`（設定圖形狀態）與 `Q`（還原圖形狀態）將現有內容包裹起來。

```csharp
    // Get the current content stream
    var content = page.Contents[1]; // assume a single content stream

    // Build a new stream that sets the graphics state, draws the original content, then restores
    string gsOperator = "/GS0 gs\n"; // select the graphics state we created
    string restoreOperator = "Q\n";   // restore graphics state after drawing

    // Prepend the gs operator and append the restore operator
    string newStream = gsOperator + content.Stream.ToString() + restoreOperator;

    // Replace the original stream with the modified one
    content.Stream = new CosPdfStream(document);
    content.Stream.SetData(newStream);
```

*為什麼這很重要：* 若省略此步驟，圖形狀態雖已存在卻未被使用。加入 `gs` 運算子可告訴 PDF 渲染器將透明度套用於其後的所有內容。

## 步驟 6：**Save modified PDF**（儲存已修改的 PDF）至磁碟

最後，將變更後的文件寫入新檔案。`Save` 方法會自動處理所有低階更新。

```csharp
    // Path for the output PDF
    string outputPath = @"YOUR_DIRECTORY\output.pdf";

    // Persist the changes
    document.Save(outputPath);
}
```

*為什麼這很重要：* `document.Save` 呼叫確保更新後的 **save modified pdf**（儲存已修改的 PDF）包含新的 `ExtGState` 條目以及引用它的內容串流。產生的檔案將在第一頁顯示半透明填充。

## 預期結果

在任何 PDF 檢視器（Adobe Reader、Chrome 等）中開啟 `output.pdf`，您應該會看到第一頁的圖形以 50 % 填充不透明度呈現。若使用 **PDF‑Tron** 或 **iText** 等工具檢查 PDF，會發現名為 `GS0` 的 `ExtGState` 字典條目，其 `ca` 值為 `0.5`。

## 邊緣情況與變體

| 情況 | 需要變更的地方 |
|-----------|----------------|
| **多頁** | 遍歷 `document.Pages`，對每頁重複步驟 2‑5，使用如 `GS1`、`GS2`… 的唯一名稱。 |
| **已存在的 ExtGState 名稱衝突** | 在加入前檢查 `extGStateDict.ContainsKey("GS0")`；若已存在，產生新鍵（`"GS" + Guid.NewGuid().ToString("N")`）。 |
| **不同的混合模式** | 將 `BM` 條目改為 `"Multiply"`、`"Screen"` 等，以取代 `"Normal"`。 |
| **僅需描邊不透明度** | 省略 `ca` 條目或將其設為 `1`，改為調整 `CA`。 |

## 完整、可執行範例



## 接下來該學什麼？

以下教學涵蓋與本指南示範技術密切相關的主題。每個資源皆提供完整可運作的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [使用 Aspose.PDF 為 PDF 添加透明度 – 完整 C# 指南](/pdf/english/net/programming-with-stamps-and-watermarks/add-transparency-to-pdf-with-aspose-pdf-complete-c-guide/)
- [如何使用 Aspose.PDF for .NET 為 PDF 添加頁面印章：完整指南](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [如何使用 Aspose.PDF for .NET 為 PDF 添加影像：完整指南](/pdf/english/net/images-graphics/add-images-to-pdfs-using-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}