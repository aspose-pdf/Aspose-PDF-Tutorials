---
category: general
date: 2026-11-12
description: 學習如何使用 Aspose.Pdf 更改 PDF 不透明度、加入透明效果、設定混合模式，並在 C# 中儲存已修改的 PDF。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF opacity
- how to add transparency
- save modified PDF
- how to set blend mode
- set fill opacity
language: zh-hant
lastmod: 2026-11-12
og_description: 使用 Aspose.Pdf 更改 PDF 透明度，了解如何加入透明效果、設定混合模式，並以 C# 儲存修改後的 PDF 檔案。
og_image_alt: Screenshot of a PDF page with altered opacity using Aspose.Pdf
og_title: 使用 Aspose.Pdf 調整 PDF 透明度 – 添加透明效果並儲存
schemas:
- author: Aspose
  dateModified: '2026-11-12'
  description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  headline: Change PDF opacity with Aspose.Pdf and save the file
  type: TechArticle
- description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  name: Change PDF opacity with Aspose.Pdf and save the file
  steps:
  - name: Load the PDF document
    text: Start by creating a `Document` instance that points to your source file.
      The constructor reads the entire PDF into memory, allowing you to manipulate
      its internal objects.
  - name: Access the first page’s resources
    text: Each PDF page stores a *resource dictionary* that holds objects such as
      fonts, images, and graphics states. You need to edit this dictionary to inject
      a new `ExtGState` entry.
  - name: Ensure an ExtGState dictionary exists
    text: The `ExtGState` dictionary holds custom graphics states. If it does not
      exist, the code creates one automatically.
  - name: Define a new graphics state (ExtGState)
    text: A graphics state defines how drawing operations behave. The following dictionary
      sets stroke opacity (`CA`), fill opacity (`ca`), and blend mode (`BM`).
  - name: Register the graphics state in the resource dictionary
    text: Give the new state a name (e.g., `GS0`) and add it to the `ExtGState` dictionary.
      This name will be referenced later in the page content stream.
  - name: Apply the graphics state to page content
    text: To actually see the opacity effect, insert the `/GS0 gs` operator before
      the drawing commands you want to affect. The example below draws a semi‑transparent
      rectangle.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The `Save` method overwrites
      the target file or creates a new one if it does not exist.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: 使用 Aspose.Pdf 更改 PDF 不透明度並儲存檔案
url: /zh-hant/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-and-save-the-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Pdf 更改 PDF 不透明度並儲存檔案

如果您需要在文件中**更改 PDF 不透明度**，Aspose.Pdf 提供簡單易用的 API 來調整描邊與填充的透明度。本教學將完整說明**如何加入透明度**、**如何設定混合模式**，以及**以少量 C# 程式碼儲存已修改的 PDF**檔案。

您將逐步完成每個步驟——從載入現有 PDF、定義新的圖形狀態，到持久化變更。完成本指南後，您可以：

* 減低向量圖形或影像的可見度。
* 套用自訂的混合模式，例如 *Normal* 或 *Multiply*。
* 匯出更新後的檔案，同時保留其他所有內容。

唯一的前置條件是具備可運作的 .NET 開發環境，並參考 Aspose.Pdf 函式庫（版本 23.9 或更新）。不需要任何外部工具。

## 前置條件

| 需求 | 為何重要 |
|-------------|----------------|
| .NET 6.0 SDK 或更新版本 | 確保與最新的 Aspose.Pdf API 相容。 |
| Aspose.Pdf for .NET NuGet 套件 | 提供程式碼中使用的 `Document`、`CosPdfDictionary` 以及相關類別。 |
| 用於編輯的 PDF 檔案（例如 `input.pdf`） | 作為不透明度變更的來源檔案。 |

使用以下指令安裝 NuGet 套件：

```bash
dotnet add package Aspose.Pdf
```

## 使用 Aspose.Pdf 更改 PDF 不透明度

### 步驟 1：載入 PDF 文件

首先建立指向來源檔案的 `Document` 實例。建構子會將整個 PDF 讀入記憶體，讓您可以操作其內部物件。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;

// Load the existing PDF
var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");
```

> **為何需要此步驟？** 載入檔案會建立可操作的物件模型。所有後續的變更皆作用於此記憶體中的表示，確保原始檔案在您明確儲存前保持不變。

### 步驟 2：存取第一頁的資源

每個 PDF 頁面都儲存一個*資源字典*，其中包含字型、影像與圖形狀態等物件。您需要編輯此字典以注入新的 `ExtGState` 條目。

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor simplifies access to the page's resource dictionary
var resourcesEditor = new DictionaryEditor(page.Resources);
```

> **提示：** 若您的 PDF 包含多頁需要相同的不透明度，請對每頁重複此步驟，或在多頁之間共用同一個 `ExtGState`。

### 步驟 3：確保存在 ExtGState 字典

`ExtGState` 字典保存自訂的圖形狀態。若不存在，程式碼會自動建立一個。

```csharp
// Get or create the ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                     ?? new CosPdfDictionary(pdfDoc);
resourcesEditor["ExtGState"] = extGStateDict;
```

> **為何需要此步驟？** 若沒有 `ExtGState` 容器，任何對新圖形狀態的引用都會失敗，導致 PDF 忽略您的不透明度設定。

### 步驟 4：定義新的圖形狀態 (ExtGState)

圖形狀態定義繪圖操作的行為。以下字典設定描邊不透明度 (`CA`)、填充不透明度 (`ca`) 與混合模式 (`BM`)。

```csharp
// Create an empty dictionary for the new graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Set desired parameters
var parameters = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (1 = opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (0.5 = 50% transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var param in parameters)
    newGraphicsState.Add(param);
```

> **如何設定填充不透明度：** `ca` 條目控制已填充形狀（文字、路徑）的不透明度。將數值調整於 `0`（完全透明）至 `1`（完全不透明）之間，以符合您的設計需求。

> **如何設定混合模式：** `BM` 條目選擇合成演算法。常見的值包括 `Normal`、`Multiply`、`Screen` 與 `Overlay`。選擇最符合您視覺意圖的模式。

### 步驟 5：在資源字典中註冊圖形狀態

為新狀態命名（例如 `GS0`），並將其加入 `ExtGState` 字典。此名稱稍後會在頁面內容串流中被引用。

```csharp
// Add the graphics state with a symbolic name
extGStateDict.Add("GS0", newGraphicsState);
```

> **專業提示：** 建立多個狀態時，使用 `GS0`、`GS1`… 等命名規則。可避免名稱衝突，且讓除錯更容易。

### 步驟 6：將圖形狀態套用至頁面內容

若要實際看到不透明度效果，請在欲影響的繪圖指令前插入 `/GS0 gs` 運算子。以下範例會繪製一個半透明矩形。

```csharp
// Build a content stream that uses the new graphics state
var content = new MemoryStream();
var writer = new StreamWriter(content);

// Activate the graphics state
writer.WriteLine("q");                 // Save graphics state
writer.WriteLine("/GS0 gs");           // Apply custom ExtGState
writer.WriteLine("0.2 0.5 0.8 rg");    // Set fill color (RGB)
writer.WriteLine("100 500 200 100 re"); // Rectangle (x y width height)
writer.WriteLine("f");                 // Fill rectangle
writer.WriteLine("Q");                 // Restore graphics state
writer.Flush();

content.Position = 0;
page.Contents.Add(new ContentStream(content));
```

> **為何使用 `q` 與 `Q` 運算子？** 它們會推入與彈出圖形狀態堆疊，確保不透明度變更僅影響矩形，而不會影響頁面的其他部分。

### 步驟 7：儲存已修改的 PDF

最後，將更新後的文件寫入磁碟。`Save` 方法會覆寫目標檔案，若檔案不存在則會建立新檔案。

```csharp
// Persist the changes
pdfDoc.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **如何儲存已修改的 PDF：** `Save` 呼叫會將所有記憶體中的修改（包括新的 `ExtGState`）寫入指定路徑。您亦可將結果串流至 `MemoryStream` 以供網頁回應使用。

## 完整可執行範例

以下是一個完整、獨立的程式，整合了上述所有步驟。將其複製到主控台應用程式中執行，即可驗證不透明度變更。



## 接下來您可以學習什麼？

以下教學涵蓋與本指南密切相關的主題，並在此基礎上延伸技術。每個資源都提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [如何使用 Aspose.Pdf 儲存已修改的 PDF 並加入透明度](/pdf/english/net/document-manipulation/how-to-save-modified-pdf-with-aspose-pdf-and-add-transparenc/)
- [如何在 C# 中使用 Aspose.PDF 為 PDF 加入透明度](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [如何使用 Aspose.PDF 新增圖形狀態並控制透明度](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}