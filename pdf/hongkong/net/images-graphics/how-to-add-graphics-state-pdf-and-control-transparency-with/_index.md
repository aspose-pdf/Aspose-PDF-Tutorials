---
category: general
date: 2026-09-05
description: 學習如何使用 Aspose.PDF 添加圖形狀態 PDF 以設定透明度。此一步一步指南亦示範如何加入透明 PDF 以及高效地修改 PDF
  透明度。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- how to add transparency pdf
- modify pdf transparency
language: zh-hant
lastmod: 2026-09-05
og_description: 使用 Aspose.PDF 為 PDF 添加圖形狀態。跟隨本指南，學習如何在 PDF 中加入透明度以及僅用幾行 C# 代碼修改 PDF
  透明度。
og_image_alt: Screenshot of C# code that adds graphics state pdf to a PDF document
og_title: 使用 Aspose.PDF 添加圖形狀態 PDF – 在 C# 中控制透明度
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Learn how to add graphics state pdf using Aspose.PDF to set transparency.
    This step‑by‑step guide also shows how to add transparency pdf and modify pdf
    transparency efficiently.
  headline: How to add graphics state pdf and control transparency with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- PDF graphics state
- PDF transparency
- C# PDF manipulation
title: 如何使用 Aspose.PDF 添加圖形狀態並控制透明度
url: /zh-hant/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何新增 graphics state pdf 並使用 Aspose.PDF 控制透明度

如果您需要 **add graphics state pdf** 到現有文件，本指南會示範完整步驟。您將看到如何使用 Aspose.PDF for .NET 新增 transparency pdf，以及如何在不破壞原始版面的前提下修改 pdf 透明度。

在以下章節中，我們會逐步走過一個完整、可執行的範例，說明每一行程式碼的意義，並討論常見的陷阱。完成後，您將能在任何 PDF 頁面中嵌入自訂的 graphics state（例如筆畫與填色的 alpha 值）。

## 前置條件

開始之前，請確保您已具備：

* .NET 6.0 或更新版本（程式碼亦適用於 .NET Framework 4.7+）
* 有效的 Aspose.PDF for .NET 授權或臨時評估金鑰
* Visual Studio 2022（或您偏好的任何 C# 編輯器）
* 一個您有權修改的輸入 PDF 檔案（`input.pdf`）

除 `Aspose.Pdf` 之外，無需其他 NuGet 套件。

## 步驟 1：載入 PDF 文件

第一步是開啟來源 PDF。Aspose.PDF 會將檔案包裝成 `Document` 物件，讓您可以存取頁面、資源與低階 PDF 結構。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Generator;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;
using Aspose.Pdf.Xmp;

string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Open the document inside a using block so resources are released automatically.
using (var doc = new Document(inputPath))
{
    // The rest of the code lives inside this block.
}
```

**Why this matters:** 使用 `using` 陳述式開啟檔案可確保即使發生例外，檔案句柄也會被關閉。`Document` 物件同時會載入交叉參照表，讓我們之後能編輯低階字典。

## 步驟 2：存取第一頁的資源字典

每個 PDF 頁面都有一個 *Resources* 字典，用來儲存字型、XObject 與 graphics state（`ExtGState`）。要注入新的 graphics state，首先必須取得此字典。

```csharp
// Inside the using block
Page page = doc.Pages[1];                     // Get the first page (pages are 1‑based)
var dictEditor = new DictionaryEditor(page.Resources);
var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();
```

**Why this matters:** `ExtGState` 是存放 graphics state 物件的鍵。如果頁面尚未包含 `ExtGState` 條目，Aspose.PDF 會自動建立空字典，讓程式碼在兩種情況下皆可運作。

## 步驟 3：建立新的 graphics state 字典

graphics state 字典定義繪圖操作的行為。對於透明度，我們需要 `CA`（筆畫 alpha）、`ca`（填色 alpha）以及可選的混合模式（`BM`）。以下程式碼會建立此字典。

```csharp
// Create an empty COS dictionary that will become our new graphics state.
CosPdfDictionary newGs = CosPdfDictionary.CreateEmptyDictionary(doc);

// Define the entries we want: 1.0 stroke opacity, 0.5 fill opacity, Normal blend mode.
var entries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // stroke alpha (fully opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // fill alpha (50 % transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // blend mode
};

foreach (var entry in entries)
{
    newGs.Add(entry);
}
```

**Why this matters:**  
* `CA` 控制描邊路徑（線條、邊框）的不透明度。  
* `ca` 控制填充物件（圖形、文字）的不透明度。  
* `BM` 選擇混合模式；「Normal」是最常見且適用於所有 PDF 閱讀器的模式。

### 邊緣情況：缺少 `ExtGState` 條目

如果 `page.Resources` 不包含 `ExtGState` 字典，`dictEditor["ExtGState"]` 會回傳 `null`。此時您可以手動建立它：

```csharp
if (extGState == null)
{
    extGState = CosPdfDictionary.CreateEmptyDictionary(doc);
    dictEditor["ExtGState"] = extGState;
}
```

加入此防護可讓教學在從未使用過自訂 graphics state 的 PDF 上也能穩定執行。

## 步驟 4：將新的 graphics state 加入資源字典

現在我們把剛建立的字典綁定到一個名稱（例如 `GS0`）。內容串流可以引用此名稱來套用定義好的透明度。

```csharp
// Register the new graphics state under the name "GS0"
extGState.Add("GS0", newGs);
```

**Why this matters:** PDF 內容運算子如 `gs` 會切換至具名的 graphics state。加入 `GS0` 後，後續的內容串流即可使用 ` /GS0 gs ` 來啟用透明度設定。

## 步驟 5：（可選）將 graphics state 套用至現有內容

如果您希望目前頁面的既有元素變為透明，可以在頁面的內容串流前面加入 `gs` 運算子。此步驟為可選，因為許多情境只需要在新加入的物件上使用 graphics state。

```csharp
// Prepend "GS0" graphics state to the page’s content
page.Contents.Insert(0, new OperatorGraphicsState("GS0"));
```

**Why this matters:** 若未加入此行，頁面會保留原始外觀。加入運算子可確保在此之後繪製的所有內容都繼承新的不透明度值。

## 步驟 6：儲存已修改的 PDF

最後，將更新後的文件寫入磁碟。您可以覆寫原始檔案，或寫入新位置。

```csharp
string outputPath = @"YOUR_DIRECTORY\output.pdf";
doc.Save(outputPath);
```

**Why this matters:** `doc.Save` 會序列化已修改的交叉參照表、資源字典與任何新內容串流，產生任何閱讀器皆能開啟的有效 PDF。

## 完整範例

將所有片段組合起來，以下是一個可直接複製、貼上並執行的自包含程式。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Xmp;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;
using Aspose.Pdf.Cos;

class AddGraphicsStateExample
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        using (var doc = new Document(inputPath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Access the first page's resource dictionary
            // -----------------------------------------------------------------
            Page page = doc.Pages[1];
            var dictEditor = new DictionaryEditor(page.Resources);
            var extGState = dictEditor["ExtGState"]?.ToCosPdfDictionary();

            // Ensure ExtGState exists
            if (extGState == null)
            {
                extGState = CosPdfDictionary.CreateEmptyDictionary(doc);
                dictEditor["ExtGState"] = extGState;
            }

            // -----------------------------------------------------------------
            // 3️⃣ Create a new graphics state (transparency settings)
            // -----------------------------------------------------------------
            CosPdfDictionary newGs = CosPdfDictionary.CreateEmptyDictionary(doc);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var entry in entries) newGs.Add(entry);

            // -----------------------------------------------------------------
            // 4️⃣ Register the graphics state as "GS0"
            // -----------------------------------------------------------------
            extGState.Add("GS0", newGs);

            // -----------------------------------------------------------------
            // 5️⃣ (Optional) Apply the graphics state to existing content
            // -----------------------------------------------------------------
            page.Contents.Insert(0, new OperatorGraphicsState("GS0"));

            // -----------------------------------------------------------------
            // 6️⃣ Save the modified PDF
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath);
            Console.WriteLine($"PDF saved with new graphics state at: {outputPath}");
        }
    }
}
```

### 預期輸出

執行程式後，於 Adobe Acrobat Reader 或任何 PDF 閱讀器開啟 `output.pdf`。第一頁的任何填充形狀（例如彩色矩形）應以 **50 % 不透明度** 顯示，而筆畫仍保持完全不透明。若您加入了可選的 `gs` 運算子，該頁面的 *所有* 既有內容皆會繼承相同的透明度。

## 常見問題與疑難排解

| 問題 | 解答 |
|----------|--------|
| **我可以新增多個 graphics state 嗎？** | 可以。建立額外的字典（例如 `GS1`、`GS2`），並以不同的 `gs` 運算子引用它們。 |
| **如果 PDF 已經使用了像 `GS0` 這樣的名稱怎麼辦？** | 選擇唯一的名稱（例如 `MyGS`），或使用 `extGState.Keys` 檢查現有鍵。 |
| **這能用於加密的 PDF 嗎？** | 必須使用正確的密碼開啟文件。使用 `new Document(inputPath, new LoadOptions { Password = "pwd" })`。 |
| **變更會影響其他頁面嗎？** | 不會。graphics state 只會加入您編輯的頁面的資源。若要影響所有頁面，請對每頁重複此程序，或將字典加入 *文件層級* 資源。 |
| **會有效能影響嗎？** | 加入單一 graphics state 的影響可以忽略不計。大量頁面的 PDF 可能需要迴圈處理，但此操作仍為 O(頁數) 的複雜度。 |

## 專業技巧

* **Reuse graphics states:** 若需要在多頁使用相同的透明度，將字典加入 *文件* 資源 (`doc.Resources`) 並在每頁引用，這樣可減少檔案大小。  
* **Blend modes:** 嘗試其他 `BM` 值，如 `Multiply`、`Screen` 或 `Overlay` 以獲得創意效果。並非所有閱讀器皆支援每種混合模式，請針對目標受眾進行測試。  
* **Testing:** 始終將原始與修改後的 PDF 並排比較。使用能渲染 PDF 的差異工具（例如 `DiffPDF`）驗證僅有預期的變更發生。

## 後續步驟

現在您已了解 **how to add transparency pdf** 與 **modify pdf transparency**，可以進一步探索以下相關主題：

* **Add graphics state pdf** 用於 overprint 與半色調效果  
* **Embedding images with custom opacity** 使用 `ImageFragment` 與 graphics state  
* **Batch processing** 在資料夾中批次處理多個 PDF，使用平行化提升效能  
* **Using Aspose.PDF’s high‑level API** (`PdfSaveOptions`, `PdfPageEditor`) 用於更複雜的工作流程  

隨意嘗試不同的 alpha 值，觀察效果變化。

## 接下來該學什麼？

以下教學與本指南所示技術緊密相關，能幫助您進一步掌握 API 功能並探索其他實作方式：

- [Add Transparency to PDF using Aspose – Complete C# Guide](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [How to Add a Text Stamp to PDF Using Aspose.PDF .NET&#58; Comprehensive Guide](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)
- [How to Add Images to PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/add-images-to-pdfs-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}