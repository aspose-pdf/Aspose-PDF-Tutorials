---
category: general
date: 2026-08-14
description: 使用 Aspose.Pdf 在 C# 中建立空的 PDF 字典 – 了解如何將圖形狀態加入 ExtGState 集合，並以程式方式修改 PDF。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.Pdf Document
- PDF graphics state
- ExtGState dictionary
- CosPdfDictionary usage
language: zh-hant
lastmod: 2026-08-14
og_description: 在 C# 中使用 Aspose.Pdf 建立空的 PDF 字典。請參考本完整指南，將自訂圖形狀態加入 PDF 的 ExtGState
  集合。
og_image_alt: Screenshot showing C# code that creates an empty PDF dictionary with
  Aspose.Pdf
og_title: 在 C# 中建立空的 PDF 字典 – Aspose.Pdf 步驟指南
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  headline: Create empty PDF dictionary in C# with Aspose.Pdf
  type: TechArticle
- description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  name: Create empty PDF dictionary in C# with Aspose.Pdf
  steps:
  - name: Create a new **Console App** project in Visual Studio.
    text: Create a new **Console App** project in Visual Studio.
  - name: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
    text: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
  - name: 'Add the following `using` directives at the top of `Program.cs`:'
    text: 'Add the following `using` directives at the top of `Program.cs`:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: 在 C# 中使用 Aspose.Pdf 建立空的 PDF 字典
url: /zh-hant/net/programming-with-operators/create-empty-pdf-dictionary-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 使用 Aspose.Pdf 建立空的 PDF 字典

如果您需要 **建立空的 PDF 字典** 物件來處理 PDF 檔案，本指南將示範如何在 C# 中使用 Aspose.Pdf 套件完成。無論是建立自訂圖形狀態、加入新資源，或是為日後使用準備範本，以下步驟提供完整、可執行的解決方案。

您將學會如何載入 PDF、存取第一頁的資源字典、建立全新的 `CosPdfDictionary`，並將其插入 `ExtGState` 集合。完成教學後，您將得到一個包含新建立字典的 `output.pdf`。

## 前置條件

在開始之前，請確保您已具備：

- .NET 6.0 或更新版本（此程式碼亦相容 .NET Framework 4.6+）
- Visual Studio 2022 或您慣用的 C# IDE
- Aspose.Pdf for .NET 授權（或暫時的評估金鑰）
- 一個名為 **input.pdf** 的範例 PDF，放置於您可控制的資料夾中（資料夾路徑將作為 `dataDir` 使用）

除 `Aspose.Pdf` 之外，無需其他 NuGet 套件。

## 步驟 1：建立專案並參考 Aspose.Pdf

1. 在 Visual Studio 中建立一個 **Console App** 專案。  
2. 開啟 **NuGet Package Manager**，安裝 `Aspose.Pdf`：

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. 在 `Program.cs` 檔案頂部加入以下 `using` 指令：

   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Text;
   using Aspose.Pdf.Operators;
   using Aspose.Pdf.Facades;
   using Aspose.Pdf.InteractiveFeatures;
   using Aspose.Pdf.Xmp;
   using Aspose.Pdf.Operators.Filters;
   using Aspose.Pdf.Operators.Gfx;
   ```

   *為什麼需要這些命名空間？* `Aspose.Pdf` 包含核心的 `Document` 類別，而 `Aspose.Pdf.Operators.Gfx` 提供 `CosPdfDictionary`、`CosPdfNumber` 以及其他建立 **空的 PDF 字典** 結構所需的低階 PDF 物件。

## 步驟 2：載入來源 PDF

第一步是將現有的 PDF 檔案載入至 `Document` 實例，這樣您就能存取所有頁面、資源與低階字典。

```csharp
// Step 2: Load the PDF document
string dataDir = @"C:\MyPdfFolder\";               // Change to your folder
using var pdfDocument = new Document(dataDir + "input.pdf");
```

*說明*：`Document` 會將檔案讀入記憶體並建立內部結構。`using` 陳述式確保在處理完畢後釋放檔案句柄。

## 步驟 3：存取第一頁的資源字典

每個 PDF 頁面都有一個 **Resources** 字典，用來彙總字型、影像、ExtGState 物件以及其他共享資源。要插入新的圖形狀態，我們需要編輯此字典。

```csharp
// Step 3: Get the first page and its Resources dictionary
Page firstPage = pdfDocument.Pages[1];                     // PDF pages are 1‑based
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` 是一個輔助類別，讓您可以將 PDF 字典當作 C# 的 `Dictionary<string, object>` 來操作。

## 步驟 4：取得（或建立）ExtGState 集合

`ExtGState` 保存圖形狀態物件，例如不透明度、混合模式與線寬。如果來源 PDF 已經包含 `ExtGState` 條目，我們會直接使用；否則就建立一個全新的空字典。

```csharp
// Step 4: Ensure an ExtGState dictionary exists
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a brand‑new ExtGState dictionary and add it to Resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*為什麼要這樣檢查？* 有些 PDF 完全沒有 `ExtGState` 條目。處理兩種情況可讓本教學對任何輸入檔案都具備韌性。

## 步驟 5：為新圖形狀態 **建立空的 PDF 字典**

現在我們真的要 **建立空的 PDF 字典** 物件，定義圖形狀態參數。字典起始為空，我們再加入必要的鍵值：

```csharp
// Step 5: Build a new graphics state dictionary (empty PDF dictionary + entries)
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Stroke opacity (CA) – 1 means fully opaque strokes
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes semi‑transparent fills
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default compositing mode
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

### 各條目說明

| 鍵 | 類型 | 說明 |
|-----|------|---------|
| **CA** | `CosPdfNumber` | 描邊不透明度（範圍 0‑1）。 |
| **ca** | `CosPdfNumber` | 填充不透明度（範圍 0‑1）。 |
| **BM** | `CosPdfName`   | 混合模式；最常用的是 `"Normal"`。 |

因為我們是從 **空的 PDF 字典** 開始，所以可以完全掌控加入哪些條目。日後若需要，可再加入其他圖形狀態參數，例如 `LW`（線寬）或 `LC`（線端點）等。

## 步驟 6：將新圖形狀態插入 ExtGState

`ExtGState` 字典的運作方式類似映射，每個條目以名稱（例如 `GS0`、`GS1`）作為鍵。我們將剛建立的字典放在一個唯一的鍵下。

```csharp
// Step 6: Add the graphics state to the ExtGState collection
extGStateDict.Add("GS0", newGraphicsState);
```

如果要加入多個狀態，請遞增後綴（`GS1`、`GS2`…）以避免名稱衝突。

## 步驟 7：儲存修改後的 PDF

最後，將變更寫回磁碟。`Save` 方法會自動序列化更新過的字典。

```csharp
// Step 7: Persist the changes
pdfDocument.Save(dataDir + "output.pdf");
```

在任意 PDF 檢視器中開啟 `output.pdf`，檢查 **Resources → ExtGState** 條目（大多檢視器會隱藏此資訊，但 Adobe Acrobat Preflight 或 PDF‑Tron 等工具可以顯示）。您應該會看到一個 `GS0` 條目，內含先前定義的不透明度與混合模式值。

## 完整可執行範例

將所有片段組合起來，以下程式碼可直接貼到 `Program.cs` 並執行：

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators.Gfx;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string dataDir = @"C:\MyPdfFolder\"; // <-- change to your folder
        using var pdfDocument = new Document(dataDir + "input.pdf");

        // -----------------------------------------------------------------
        // 2️⃣ Access the first page’s Resources dictionary
        // -----------------------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // -----------------------------------------------------------------
        // 3️⃣ Retrieve or create the ExtGState dictionary
        // -----------------------------------------------------------------
        CosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourcesEditor["ExtGState"] = extGStateDict;
        }

        // -----------------------------------------------------------------
        // 4️⃣ **Create empty PDF dictionary** for a new graphics state
        // -----------------------------------------------------------------
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode

        // -----------------------------------------------------------------
        // 5️⃣ Add the graphics state to ExtGState
        // -----------------------------------------------------------------
        extGStateDict.Add("GS0", newGraphicsState);

        // -----------------------------------------------------------------
        // 6️⃣ Save the modified PDF
        // -----------------------------------------------------------------
        pdfDocument.Save(dataDir + "output.pdf");

        Console.WriteLine("PDF saved with new empty dictionary at: " + dataDir + "output.pdf");
    }
}
```

**預期輸出** – 主控台會印出確認訊息，`output.pdf` 內會在 `ExtGState` 下出現新的 `GS0` 條目。當您在內容串流中使用 `gs` 操作符引用 `GS0` 時，描邊將完全不透明，而填充則為 50 % 透明。

## 常見問題與邊緣情況處理

| 問題 | 解答 |
|----------|--------|
| *如果 PDF 有多頁怎麼辦？* | 範例針對第一頁（`Pages[1]`）操作。若要影響所有頁面，可遍歷 `pdfDocument.Pages`，對每頁的資源重複步驟 3‑5。 |
| *我可以把字典加入已存在名稱為 “GS0” 的 ExtGState 條目嗎？* | 可以，但必須使用不同的鍵（`GS1`、`GS2`…）以免覆寫既有條目。 |
| *儲存後再修改字典安全嗎？* | 呼叫 `Save` 後，記憶體中的表示已與檔案分離。您仍可繼續編輯 `Document` 物件，必要時再次呼叫 `Save`。 |
| *使用 `Aspose.Pdf` 是否需要授權？* |  |

## 接下來您可以學習什麼？

以下教學與本指南緊密相關，能進一步深化您對 API 的運用，並提供其他實作方式的完整範例與步驟說明。

- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [How to Remove Graphics from PDFs Using Aspose.PDF .NET&#58; A Complete Guide](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [How to Create Multi-Layer PDFs Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/advanced-features/create-multi-layer-pdfs-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}