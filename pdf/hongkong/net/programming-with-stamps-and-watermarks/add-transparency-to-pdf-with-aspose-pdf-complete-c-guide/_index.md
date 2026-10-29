---
category: general
date: 2026-07-14
description: 使用 Aspose.PDF 在 C# 中為 PDF 添加透明度。本指南快速說明如何編輯 PDF 資源、設定透明度以及定義混合模式。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- edit pdf resources
- aspnet pdf opacity
- c# pdf manipulation
- aspose pdf graphics state
language: zh-hant
lastmod: 2026-07-14
og_description: 即時為 PDF 添加透明度。學習使用 Aspose.PDF 在 C# 中編輯 PDF 資源、控制不透明度與混合模式。
og_image_alt: Screenshot showing a PDF page with semi‑transparent shapes after applying
  Aspose.PDF code
og_title: 在 PDF 中加入透明度 – 完整 C# 教學與 Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Add transparency to PDF using Aspose.PDF in C#. This guide shows how
    to edit PDF resources, set opacity, and define blend modes quickly.
  headline: Add transparency to PDF with Aspose.PDF – Complete C# Guide
  type: TechArticle
- description: Add transparency to PDF using Aspose.PDF in C#. This guide shows how
    to edit PDF resources, set opacity, and define blend modes quickly.
  name: Add transparency to PDF with Aspose.PDF – Complete C# Guide
  steps:
  - name: – Load the source PDF
    text: '```csharp using Aspose.Pdf; using Aspose.Pdf.Collections; using Aspose.Pdf.Devices;'
  - name: – Grab the first page’s resource dictionary
    text: '```csharp var firstPage = pdfDocument.Pages[1]; // PDF pages are 1‑based
      var resourcesEditor = new DictionaryEditor(firstPage.Resources); var extGStateDict
      = resourcesEditor["ExtGState"] .ToCosPdfDictionary(); ```'
  - name: – Build a new graphics state dictionary
    text: '```csharp // Create an empty dictionary that will hold our transparency
      settings var graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);'
  - name: – Register the graphics state in the resource dictionary
    text: '```csharp // "GS0" is an arbitrary name; you can choose any identifier
      you like extGStateDict.Add("GS0", graphicsStateDict); ```'
  - name: – Apply the graphics state and save
    text: 'At this point the PDF knows about the new graphics state, but you still
      need to tell the page’s content stream to use it. The simplest way is to prepend
      a small snippet that sets the state before any drawing commands:'
  type: HowTo
- questions:
  - answer: Aspose.PDF automatically creates it when you access `resourcesEditor["ExtGState"]`.
      If you encounter a `null`, instantiate a new `CosPdfDictionary` and assign it
      back.
    question: What if the page has no `ExtGState` dictionary yet?
  - answer: Yes. Define `GS1`, `GS2`, … with distinct `ca`/`CA` values and switch
      between them in the content stream (`/GS1 gs`, `/GS2 gs`).
    question: Can I set different opacities for multiple objects?
  - answer: You must provide the password when constructing `new Document(inputPath,
      password)`. After decryption, the same resource‑editing steps apply.
    question: Will this work on encrypted PDFs?
  - answer: PDF names are case‑sensitive, so use the exact spelling (`Normal`, `Multiply`,
      `Screen`, etc.) as defined in the PDF spec.
    question: Is the blend mode case‑sensitive?
  type: FAQPage
tags:
- PDF
- C#
- Aspose.PDF
- Transparency
title: 使用 Aspose.PDF 為 PDF 添加透明度 – 完整 C# 指南
url: /zh-hant/net/programming-with-stamps-and-watermarks/add-transparency-to-pdf-with-aspose-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.PDF 為 PDF 加入透明度 – 完整 C# 教程

有沒有想過在不使用大型圖形編輯器的情況下，**為 PDF 加入透明度**？你並不孤單。許多開發者需要即時調整 PDF——例如浮水印、覆蓋圖形或細微陰影，而最簡單的方式就是直接編輯底層的 PDF 資源。

在本教學中，我們將示範一個實用的端對端解決方案，使用 Aspose.PDF for .NET **為 PDF 加入透明度**。完成後，你將清楚知道如何 **編輯 PDF 資源**、設定描邊與填充的不透明度，並挑選符合設計目標的混合模式。

## 您將學習到

- 如何使用 Aspose.PDF 載入既有 PDF。
- 了解頁面資源字典中 **ExtGState** 條目的運作原理。
- 如何建立定義不透明度 (`CA`/`ca`) 與混合模式 (`BM`) 的圖形狀態字典。
- 儲存修改後的文件，使透明度生效。
- 常見的 PDF 資源操作陷阱以及避免方法。

*先決條件:* .NET 6+ (或 .NET Framework 4.6+)，Aspose.PDF 的授權或評估版，以及基本的 C# 開發環境（Visual Studio、Rider 或 VS Code）。不需要事先了解 PDF 內部結構——只要跟著步驟做即可。

![Add transparency to PDF example](https://example.com/og-image.png){alt="套用 Aspose.PDF 程式碼後，PDF 頁面顯示半透明圖形的螢幕截圖"}

## 為 PDF 加入透明度 – 概述

在深入程式碼之前，我們先釐清「加入透明度」在 PDF 世界中的意義。PDF 以 *content streams* 儲存繪圖指令，這些串流會參照 **graphics state** 物件，控制形狀的呈現方式。以下兩個鍵值尤為重要：

| 鍵 | 說明 |
|-----|---------|
| `CA` | 描邊不透明度 (1 = 完全不透明，0 = 完全透明) |
| `ca` | 填充不透明度 (同上) |
| `BM` | 混合模式 (例如 `Normal`、`Multiply`) |

當你建立新的 **ExtGState** 條目，並讓繪圖指令指向它時，之後的所有形狀都會繼承此透明度設定。關鍵在於 **編輯 PDF 資源**——特別是 `ExtGState` 字典，讓 PDF 引擎認識你的自訂狀態。

## 使用 Aspose.PDF 編輯 PDF 資源

Aspose.PDF 以友善的 API 隱藏了低階 PDF 結構，但在需要精細控制時仍可直接操作資源字典。以下程式碼示範了完整流程：載入 PDF、建立新的圖形狀態字典，並將其注入第一頁的資源中。

### 步驟 1 – 載入來源 PDF

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Collections;
using Aspose.Pdf.Devices;

// Adjust these paths to point at your actual files
string inputPath  = "YOUR_DIRECTORY/input.pdf";
string outputPath = "YOUR_DIRECTORY/output.pdf";

using (var pdfDocument = new Document(inputPath))
{
    // The rest of the steps go here
}
```

*為什麼這很重要:* `Document` 類別是 **編輯 PDF 資源** 的入口。將它放在 `using` 區塊中，可確保檔案句柄及時釋放，這是一個小卻關鍵的效能技巧。

### 步驟 2 – 取得第一頁的資源字典

```csharp
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
var extGStateDict = resourcesEditor["ExtGState"]
                    .ToCosPdfDictionary();
```

*說明:* 每一頁都有一個 `/Resources` 字典，內含字型、影像與圖形狀態等資源。`DictionaryEditor` 讓我們把這個集合當作普通的 .NET 字典來操作，輕鬆取得 `ExtGState` 子字典。

### 步驟 3 – 建立新的圖形狀態字典

```csharp
// Create an empty dictionary that will hold our transparency settings
var graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the entries we care about
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),    // Stroke opacity (fully opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (50 % transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

*為什麼要加入這些鍵:*  
- `CA = 1` 讓形狀的輪廓保持實心，適合描邊。  
- `ca = 0.5` 使內部半透明，產生典型的「浮水印」效果。  
- `BM = Normal` 為預設混合模式；若需要藝術效果，可改為 `Multiply` 或 `Screen`。

### 步驟 4 – 在資源字典中註冊圖形狀態

```csharp
// "GS0" is an arbitrary name; you can choose any identifier you like
extGStateDict.Add("GS0", graphicsStateDict);
```

*提示:* 若要加入多個透明物件，請為每個物件使用唯一名稱（`GS1`、`GS2`…），並在內容串流中引用相對應的名稱。

### 步驟 5 – 套用圖形狀態並儲存

此時 PDF 已認識新的圖形狀態，但仍需在頁面的內容串流中指示使用它。最簡單的做法是於所有繪圖指令前加入一小段程式碼，設定該狀態：

```csharp
// Insert a small content stream that selects our graphics state
var content = "q\n/GS0 gs\n"; // 'q' saves graphics state, '/GS0 gs' sets it
firstPage.Contents.Insert(0, new MemoryStream(System.Text.Encoding.ASCII.GetBytes(content)));
```

現在可以安全地儲存修改後的檔案：

```csharp
pdfDocument.Save(outputPath);
```

**完整範例**

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Collections;
using Aspose.Pdf.Devices;
using System.Collections.Generic;
using System.IO;

string inputPath  = "YOUR_DIRECTORY/input.pdf";
string outputPath = "YOUR_DIRECTORY/output.pdf";

using (var pdfDocument = new Document(inputPath))
{
    // Access first page resources
    var firstPage = pdfDocument.Pages[1];
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
    var extGStateDict = resourcesEditor["ExtGState"]
                        .ToCosPdfDictionary();

    // Build new graphics state
    var graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    var graphicsStateEntries = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };
    foreach (var entry in graphicsStateEntries)
        graphicsStateDict.Add(entry);

    // Add to ExtGState dictionary
    extGStateDict.Add("GS0", graphicsStateDict);

    // Prepend content that selects the new graphics state
    var prepend = "q\n/GS0 gs\n";
    firstPage.Contents.Insert(0, new MemoryStream(System.Text.Encoding.ASCII.GetBytes(prepend)));

    // Save the result
    pdfDocument.Save(outputPath);
}
```

#### 預期結果

在任何檢視器（Adobe Reader、Foxit 等）開啟 `output.pdf`。在 `q /GS0 gs` 指令之後繪製的任何形狀（例如稍後加入的矩形），其 **填充不透明度為 50 %**，而描邊仍保持完全不透明。若在內容串流中之後再加入其他繪圖指令，它們會持續繼承相同的透明度，直到遇到 `Q`（還原圖形狀態）為止。

## 常見問題與邊緣案例

- **如果頁面尚未有 `ExtGState` 字典怎麼辦？**  
  當你存取 `resourcesEditor["ExtGState"]` 時，Aspose.PDF 會自動建立它。若回傳 `null`，請自行實例化 `CosPdfDictionary` 並指派回去。

- **能否為多個物件設定不同的不透明度？**  
  可以。定義 `GS1`、`GS2`…，分別給予不同的 `ca`/`CA` 值，然後在內容串流中使用 `/GS1 gs`、`/GS2 gs` 來切換。

- **這在加密的 PDF 上能運作嗎？**  
  必須在建立 `new Document(inputPath, password)` 時提供密碼。解密後，與未加密檔案相同的資源編輯步驟皆可使用。

- **混合模式是否區分大小寫？**  
  PDF 名稱是區分大小寫的，請使用規範中精確的拼寫（`Normal`、`Multiply`、`Screen` 等）。

- **效能提示:** 若要處理上百頁文件，建議在整份文件只編輯一次資源字典，並在各頁共用同一個圖形狀態，這樣可減少記憶體佔用並保持檔案大小較小。

## 接下來您可以學習什麼？

以下教學與本指南的技巧密切相關，提供完整的程式碼範例與逐步說明，協助你掌握更多 API 功能，或在專案中探索其他實作方式。

- [如何使用 Aspose.PDF .NET 為 PDF 添加文字印章：完整指南](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)
- [如何使用 Aspose.PDF for .NET 為 PDF 添加頁面印章：完整指南](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [如何使用 Aspose.PDF for .NET 為 PDF 添加線條物件：逐步指南](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}