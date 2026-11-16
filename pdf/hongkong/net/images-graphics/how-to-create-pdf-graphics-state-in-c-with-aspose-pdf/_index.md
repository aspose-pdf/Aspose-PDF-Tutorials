---
category: general
date: 2026-11-16
description: 學習如何在 C# 中使用 Aspose.Pdf 建立 PDF 圖形狀態。本指南涵蓋不透明度、混合模式以及完整程式碼範例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf graphics state
- Aspose.Pdf ExtGState
- PDF opacity
- C# PDF manipulation
- PDF blend mode
- Aspose.Pdf graphics state
language: zh-hant
lastmod: 2026-11-16
og_description: 使用 Aspose.Pdf 在 C# 中建立 PDF 圖形狀態。遵循本完整教學，以程式方式設定不透明度與混合模式。
og_image_alt: Illustration of how to create PDF graphics state with Aspose.Pdf in
  C#
og_title: 在 C# 中建立 PDF 圖形狀態 – Aspose.Pdf 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to create PDF graphics state in C# using Aspose.Pdf. This
    guide covers opacity, blend mode, and full code example.
  headline: How to create PDF graphics state in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF
title: 如何在 C# 中使用 Aspose.Pdf 建立 PDF 圖形狀態
url: /zh-hant/net/images-graphics/how-to-create-pdf-graphics-state-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 使用 Aspose.Pdf 建立 PDF 圖形狀態

如果您需要在 .NET 專案中 **建立 PDF 圖形狀態**，本教學會一步一步示範如何使用 Aspose.Pdf 完成。無論是想控制不透明度、變更混合模式，或是在多頁之間重複使用自訂圖形狀態，以下步驟都提供完整、可直接執行的解決方案。

在本指南中，您將學會如何存取頁面資源、加入 **ExtGState** 條目，並將變更寫入新檔案。範例適用於 Aspose.Pdf 23.12（或更新版本），目標為 .NET 6+，但概念同樣適用於較早的版本。

## 前置條件

開始之前，請確保您已具備：

* 已安裝 .NET 6 SDK 的 Visual Studio 2022（或任何 C# IDE）。  
* Aspose.Pdf for .NET 授權或臨時評估金鑰。  
* 名為 `input.pdf` 的 PDF 檔案，放置於程式碼可參照的資料夾中。  

除 `Aspose.Pdf` 之外，無需額外的 NuGet 套件。

## 本教學涵蓋內容

* 載入既有 PDF 文件。  
* 取得第一頁的資源字典。  
* 建立一個新圖形狀態字典，定義描邊不透明度 (`CA`)、填充不透明度 (`ca`) 與混合模式 (`BM`)。  
* 使用自訂名稱 (`GS0`) 將新圖形狀態加入 **ExtGState** 集合。  
* 儲存已更新的 PDF，使後續繪圖指令能參照此新狀態。

完成本教學後，您將能以程式方式 **建立 PDF 圖形狀態** 物件，並在任何繪圖操作中重複使用它們。

## 步驟 1：設定專案並匯入命名空間

建立一個新的主控台應用程式（或將程式碼整合至現有專案）。加入 Aspose.Pdf 參考，並引入所需的命名空間：

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Generator;
```

> **小技巧：** 若使用免費評估版，請在載入文件前加入 `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` 以避免出現浮水印訊息。

## 步驟 2：載入 PDF 文件

開啟檔案相當簡單。`Document` 類別代表整個 PDF，並提供存取頁面與資源的介面。

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";

using (var document = new Document(inputPath))
{
    // All subsequent steps run inside this using block
```

將程式碼放在 `using` 區塊內，可確保在操作結束後釋放檔案句柄，這對於 **C# PDF 操作** 的正式服務相當重要。

## 步驟 3：取得第一頁的資源字典

每一頁 PDF 都有一個 *Resources* 字典，用來儲存字型、影像與圖形狀態。我們需要 `DictionaryEditor` 來編輯此結構。

```csharp
    // Step 3: Get the first page and its resources dictionary
    var page = document.Pages[1];
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

如果 PDF 已經包含 `ExtGState` 條目，`resourcesEditor["ExtGState"]` 會回傳它；否則，當我們加入第一個條目時，Aspose.Pdf 會自動為我們建立一個空字典。

## 步驟 4：存取或建立 ExtGState 字典

**ExtGState** 字典保存具名的圖形狀態物件。我們要麼取得現有的字典，要麼建立一個新的容器。

```csharp
    // Step 4: Access (or create) the ExtGState dictionary within the resources
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

當 `ExtGState` 不存在時，`resourcesEditor["ExtGState"]` 會自動回傳一個全新的空字典，確保程式碼對任何 PDF 都能正常運作。

## 步驟 5：建構新的圖形狀態字典

圖形狀態是一個 `CosPdfDictionary`，內含特定鍵值：

* `CA` – 描邊不透明度 (0‑1)  
* `ca` – 填充不透明度 (0‑1)  
* `BM` – 混合模式 (`Normal`、`Multiply` 等)

我們先建立空字典，填入資料，然後加入 `ExtGState`。

```csharp
    // Step 5: Create a new graphics state dictionary with desired parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (50% transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };

    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

您可以將 `0.5` 改成 0 到 1 之間的任意值以調整填充不透明度，或將 `"Normal"` 換成 `"Multiply"` 以使用不同的 **PDF 混合模式**。正是因為這種彈性，建立自訂圖形狀態成為 **Aspose.Pdf 圖形狀態** 處理中的強大技巧。

## 步驟 6：以名稱註冊圖形狀態

PDF 內容串流會以名稱引用圖形狀態。此處使用 `GS0`，但任何唯一名稱皆可。

```csharp
    // Step 6: Add the new graphics state to the ExtGState dictionary with a name (e.g., GS0)
    extGState.Add("GS0", newGraphicsState);
```

若需要多個狀態，只要以不同參數重複建立步驟，並分別以 `GS1`、`GS2`…等名稱加入即可。此模式在需要於不同圖層套用多樣不透明度或混合設定的複雜文件中相當實用。

## 步驟 7：儲存已修改的 PDF

最後，將更新後的文件寫入新檔案。保留原始檔可讓除錯更為方便。

```csharp
    // Step 7: Save the updated PDF document
    string outputPath = @"YOUR_DIRECTORY\output.pdf";
    document.Save(outputPath);
}
```

執行完畢後，`output.pdf` 會包含名為 `GS0` 的 `ExtGState` 條目。之後的任何繪圖運算子都可以使用 `gs` 運算子引用它（例如內容串流中的 `GS0 gs`）。

> **為什麼重要：** 透過建立可重複使用的圖形狀態，您可以避免在每個繪圖指令中重複設定不透明度與混合模式，從而提升效能與可維護性。

## 在內容串流中使用新圖形狀態（可選）

若想立即看到效果，可加入一個簡單的矩形，使用剛剛建立的狀態：

```csharp
using (var document = new Document(outputPath))
{
    var page = document.Pages[1];
    var content = page.Contents[1]; // Get the first content stream

    // Insert graphics state selection and a semi‑transparent rectangle
    var operators = new List<Operator>
    {
        new Operator("GS0", "gs"),                     // Select our custom graphics state
        new Operator("0.5", "w"),                      // Set line width (optional)
        new Operator("100", "100", "200", "150", "re"), // Rectangle (x, y, width, height)
        new Operator("B")                              // Stroke the rectangle
    };

    foreach (var op in operators)
        content.Operators.Add(op);

    document.Save(@"YOUR_DIRECTORY\final_output.pdf");
}
```

此矩形會以 50 % 填充不透明度繪製，而描邊則保持全不透明，正如 **create PDF graphics state** 字典中所定義的那樣。

## 常見問題與避免方式

| 問題 | 為何會發生 | 解決方式 |
|------|------------|----------|
| 找不到 `ExtGState` 條目 | 某些 PDF 完全沒有此字典。 | `DictionaryEditor` 在加入第一個條目時會自動建立，無需額外檢查。 |
| 不透明度值大於 1 或小於 0 | PDF 規範限制不透明度在 `[0,1]` 範圍內。 | 在建立 `CosPdfNumber` 前先將值限制在合法範圍。 |
| 混合模式拼寫錯誤 | PDF 混合模式名稱區分大小寫。 | 使用正確的名稱，如 `"Normal"`、`"Multiply"`、`"Screen"`。 |
| 授權浮水印 | 評估版會在第一頁加入浮水印。 | 在開啟文件前套用有效的授權檔。 |

處理好這些邊緣情況，即可確保您的 **create PDF graphics state** 實作在各種 PDF 來源上都能穩定運作。

## 完整可執行範例

以下是一個完整的自包含程式，您可以直接複製、貼上並執行。請將 `YOUR_DIRECTORY` 替換為您機器上的實際資料夾路徑。

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;

class Program
{
    static void Main()
    {
        // Optional: apply license to remove evaluation watermark
        // var license = new Aspose.Pdf.License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        using (var document = new Document(inputPath))
        {
            // 1️⃣ Get first page and its resources
            var page = document.Pages[1];
            var resourcesEditor = new DictionaryEditor(page.Resources);

            // 2️⃣ Access (or create) ExtGState dictionary
            var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // 3️⃣ Build new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // 4️⃣ Register the state with a name (GS0)
            extGState.Add("


## 接下來您應該學什麼？

以下教學與本指南緊密相關，能進一步深化您對此技術的掌握。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您在專案中探索更多 API 功能與替代實作方式。

- [Create custom graphics state in PDF using Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Add graphics state to PDF using Aspose.PDF for .NET (C#)](/pdf/english/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/)
- [How to create empty graphics state in a PDF with C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}