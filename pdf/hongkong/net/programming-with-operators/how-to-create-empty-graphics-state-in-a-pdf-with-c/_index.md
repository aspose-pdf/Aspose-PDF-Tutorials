---
category: general
date: 2026-08-17
description: 使用 C# 與 Aspose.Pdf 在 PDF 中建立空的圖形狀態。請遵循此逐步指南安全地編輯 ExtGState 資源。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty graphics state
- Aspose PDF graphics state
- C# modify PDF resources
- add ExtGState dictionary
- PDF page resources editing
language: zh-hant
lastmod: 2026-08-17
og_description: 使用 C# 在 PDF 中建立空的圖形狀態。本教學示範如何使用 Aspose.Pdf 編輯 ExtGState 資源，以實現可靠的
  PDF 修改。
og_image_alt: Screenshot of C# code that adds an empty graphics state to a PDF document
og_title: 使用 C# 在 PDF 中建立空的圖形狀態 – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Create empty graphics state in a PDF using C# and Aspose.Pdf. Follow
    this step‑by‑step guide to edit ExtGState resources safely.
  headline: How to create empty graphics state in a PDF with C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: 如何使用 C# 在 PDF 中建立空的圖形狀態
url: /zh-hant/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 PDF 中使用 C# 建立空白圖形狀態

如果您需要在 PDF 中 **建立空的圖形狀態**，本指南會向您展示如何使用 C# 和 Aspose.Pdf 完成此操作。您將看到一個完整、可執行的範例，該範例會在頁面的 ExtGState 字典中新增一個條目，而不會影響現有內容。

在 PDF 中使用圖形狀態是常見需求，特別是當您想要在每個物件層面控制透明度、混合模式或其他渲染參數時。以下程式碼示範了建議的做法，說明每一步的重要性，並涵蓋您可能遇到的典型變化。

## 前置條件

* .NET 6.0 或更新版本（此範例亦可在 .NET Core 上編譯）。
* Aspose.Pdf for .NET 授權（或暫時的評估金鑰）。
* 包含您想要修改的 `input.pdf` 檔案的資料夾。
* 具備基本的 C# 語法與 PDF 概念（如資源字典）的熟悉度。

## 第一步：設定專案並匯入命名空間

建立一個新的主控台應用程式，或將程式碼整合至現有專案中。加入 Aspose.Pdf NuGet 套件：

```bash
dotnet add package Aspose.Pdf
```

接著匯入所需的命名空間：

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
```

這些匯入讓您可以存取 `Document`、`DictionaryEditor` 以及建立 **空的圖形狀態** 條目所需的 PDF 原始類別。

## 第二步：定義存放 PDF 檔案的資料夾

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfSamples\";
```

將路徑替換為您自己的 PDF 檔案所在位置。將目錄存於變數中可提升程式碼的可重用性與測試便利性。

## 第三步：載入來源 PDF 文件

```csharp
// Step 2: Load the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // All subsequent operations happen inside this using block
```

在 `using` 陳述式內開啟文件，可確保在儲存變更後自動釋放檔案句柄。

## 第四步：存取第一頁及其 Resources 字典

```csharp
    // Step 3: Get the first page and its Resources dictionary
    var firstPage = pdfDocument.Pages[1];
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
    var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

* `Pages[1]` 取得第一頁（PDF 頁碼從 1 開始）。
* `DictionaryEditor` 提供便利的方式來讀取與修改 PDF 字典。
* `ExtGState` 條目保存該頁面的所有圖形狀態物件。若鍵不存在，Aspose.Pdf 會自動建立空字典。

## 第五步：建立新的空白圖形狀態字典

您新增的圖形狀態可以是空的，或預先填入如不透明度 (`CA`, `ca`) 或混合模式 (`BM`) 等參數。在本教學中，我們建立一個 **空的圖形狀態**，然後設定少數典型值，以說明字典的運作方式。

```csharp
    // Step 4: Create a new empty graphics‑state dictionary and set its parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // Stroke opacity
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };
    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

* `CosPdfDictionary.CreateEmptyDictionary` 建立一個乾淨的容器，您可以在其中填入任何圖形狀態鍵。
* 加入 `CA`、`ca` 與 `BM` 為可選項目；若真的需要空狀態，可省略它們。程式碼示範了在之後決定控制渲染時如何加入條目。

## 第六步：將新圖形狀態插入 ExtGState 字典

```csharp
    // Step 5: Add the new graphics state to the page's ExtGState dictionary (e.g., name it "GS0")
    extGStateDict.Add("GS0", newGraphicsState);
```

將條目命名為 `"GS0"` 符合以 “GS” 為前綴的常見圖形狀態命名慣例。您可以選擇任何不與現有鍵衝突的有效 PDF 名稱。

## 第七步：儲存已修改的 PDF 文件

```csharp
    // Step 6: Save the modified PDF document
    pdfDocument.Save(dataDir + "output.pdf");
}
```

`Save` 呼叫會將更新後的檔案寫入 `output.pdf`。在 PDF 檢視器中開啟此檔案即可確認新圖形狀態已存在；之後您可以在內容串流中使用 `gs` 運算子來參考它。

### 完整程式碼清單

將所有步驟整合起來，完整程式如下：

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;

class Program
{
    static void Main()
    {
        // Define the folder that contains the PDF files
        string dataDir = @"C:\PdfSamples\";

        // Load the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Get the first page and its Resources dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create a new empty graphics‑state dictionary and set its parameters
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters)
                newGraphicsState.Add(p);

            // Add the new graphics state to the page's ExtGState dictionary (name it "GS0")
            extGStateDict.Add("GS0", newGraphicsState);

            // Save the modified PDF document
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("Empty graphics state created and saved to output.pdf");
    }
}
```

執行程式會印出確認訊息，並產生包含新加入圖形狀態的 `output.pdf`。

## 為何此方法最佳

* **直接編輯字典** – 使用 `DictionaryEditor` 可避免必須解析整個內容串流。您只會修改關心的資源。
* **具型別的 PDF 原始類別** – `CosPdfNumber`、`CosPdfName` 與 `CosPdfDictionary` 確保產生的 PDF 符合 PDF 1.7 規範。
* **安全性** – `using` 區塊會釋放 `Document` 物件，防止檔案鎖定導致後續建置受損。
* **可擴充性** – 一旦空的圖形狀態存在，您即可從任何內容運算子（`gs`）引用它，以變更選取繪圖指令的透明度、混合模式或其他參數。

## 常見變化與邊緣案例

| 情況 | 建議調整 |
|-----------|-------------------|
| **多頁面** | 對 `pdfDocument.Pages` 進行迴圈，並在每個需要修改的頁面重複插入字典的動作。 |
| **不存在 ExtGState 條目** | `resourcesEditor["ExtGState"]` 若不存在會自動建立空字典。無需額外程式碼。 |
| **不同的圖形狀態名稱** | 將 `"GS0"` 替換為符合您命名慣例的名稱，例如 `"MyTransparentState"`。 |
| **僅加入空狀態** | 省略 `parameters` 陣列與 `foreach` 迴圈；字典將保持空白。 |
| **處理加密 PDF** | 在建立 `new Document(path, password)` 時提供密碼，然後再編輯資源。 |

## 驗證結果

您可以使用低階檢視器（如 **PDF‑Tron** 或 **iText Sharp**）檢查 PDF，以驗證圖形狀態是否已加入。尋找類似以下的條目：

```
/ExtGState << /GS0 << /CA 1 /ca 0.5 /BM /Normal >> >>
```

若出現該條目，表示 **建立空的圖形狀態** 操作成功。

## 結論

現在您已了解如何使用 C# 與 Aspose.Pdf 在 PDF 中 **建立空的圖形狀態**。本教學涵蓋了每一步——從載入文件、編輯 `ExtGState` 字典到儲存結果——同時說明了每個動作背後的原理。

從此您可以：

* 在內容串流中使用新的圖形狀態（`gs /GS0`）。
* 嘗試額外的鍵值，如 `/SM`（筆畫調整）或 `/OPM`（覆蓋模式）。
* 將相同技巧套用於其他資源類型，如 `/XObject` 或 `/ColorSpace`。

祝您 PDF 開發順利，並隨時探索其他 **Aspose PDF 圖形狀態** 的情境，例如動態不透明度變化或自訂混合模式！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，建立在所示技巧之上。每個資源皆包含完整可執行的程式碼範例與逐步說明，協助您精通其他 API 功能，並在自己的專案中探索替代實作方式。

- [如何使用 Aspose.PDF for .NET 在 PDF 中建立虛線&#58; 步驟指南](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [如何使用 Aspose.PDF .NET 移除 PDF 中的圖形&#58; 完整指南](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [如何使用 Aspose.PDF for .NET 在 PDF 中建立與填充矩形&#58; 步驟指南](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}