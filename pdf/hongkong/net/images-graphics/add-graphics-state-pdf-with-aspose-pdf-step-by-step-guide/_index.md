---
category: general
date: 2026-08-04
description: 使用 Aspose.Pdf 新增圖形狀態 PDF，以控制不透明度和混合模式。請參考此完整教學，安全地修改 PDF 資源。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- Aspose.Pdf
- PDF opacity
- PDF blend mode
- ExtGState dictionary
language: zh-hant
lastmod: 2026-08-04
og_description: 使用 Aspose.Pdf 為 PDF 新增圖形狀態以設定不透明度和混合模式。本指南展示完整程式碼，說明每一步，並涵蓋常見陷阱。
og_image_alt: Screenshot of a PDF page showing modified graphics state after using
  add graphics state pdf
og_title: 使用 Aspose.Pdf 為 PDF 添加圖形狀態 – 完整程式設計指南
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Add graphics state pdf using Aspose.Pdf to control opacity and blend
    mode. Follow this complete tutorial for modifying PDF resources safely.
  headline: Add graphics state pdf with Aspose.Pdf – step‑by‑step guide
  type: TechArticle
- description: Add graphics state pdf using Aspose.Pdf to control opacity and blend
    mode. Follow this complete tutorial for modifying PDF resources safely.
  name: Add graphics state pdf with Aspose.Pdf – step‑by‑step guide
  steps:
  - name: Locate (or create) the `ExtGState` dictionary.
    text: Locate (or create) the `ExtGState` dictionary.
  - name: Build a new graphics‑state dictionary with the desired entries.
    text: Build a new graphics‑state dictionary with the desired entries.
  - name: Reference the new state from drawing commands (outside the scope of this
      tutorial).
    text: Reference the new state from drawing commands (outside the scope of this
      tutorial).
  type: HowTo
tags:
- PDF
- Aspose
- C#
- Graphics state
title: 使用 Aspose.Pdf 添加圖形狀態 PDF – 步驟指南
url: /zh-hant/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Pdf 新增圖形狀態 PDF – 步驟教學

如果您需要 **新增圖形狀態 PDF** 以控制不透明度或混合模式，本教學將提供完整、可直接投入生產環境的解決方案。您將學會如何使用 Aspose.Pdf 編輯 PDF 頁面的 ExtGState 字典，並看到可以直接複製到專案中的完整程式碼。

本指南涵蓋從專案設定到處理缺少 ExtGState 條目的邊緣情況。完成後，您的 PDF 首頁將以您定義的圖形狀態呈現。

## 前置條件

在開始之前，請確保您已具備：

* 已安裝 .NET 6.0 SDK 或更新版本。
* 最近版本的 **Aspose.Pdf** NuGet 套件（例如 23.12 或更新）。
* 位於可從程式碼參考的資料夾中的輸入 PDF 檔案。
* 如 Visual Studio 2022 或 VS Code 等開發環境。

## 圖形狀態工作流程概觀

PDF 圖形狀態決定繪圖操作的呈現方式。最常用於視覺效果的兩個屬性為：

* **Opacity** – `ca`（填充）與 `CA`（描邊）條目。
* **Blend mode** – `BM` 條目。

這些值存放於附加於頁面資源字典的 **ExtGState dictionary** 中。新增圖形狀態的步驟包括三個動作：

1. 找到（或建立）`ExtGState` 字典。
2. 建立包含所需條目的新圖形狀態字典。
3. 從繪圖指令（本教學不涵蓋）引用新狀態。

## 步驟 1：建立新的 .NET 主控台專案

```bash
dotnet new console -n PdfGraphicsStateDemo
cd PdfGraphicsStateDemo
dotnet add package Aspose.Pdf
```

`dotnet add package` 指令會下載 **Aspose.Pdf** 函式庫，提供本指南中使用的 API。

## 步驟 2：載入 PDF 並存取第一頁

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.IO;

// Load the source PDF
using var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");

// PDF pages are 1‑based; page 1 is the first page
Page firstPage = pdfDoc.Pages[1];
```

*為什麼這很重要*：PDF 物件模型使用 1 為基礎的索引，若使用 `Pages[0]` 會拋出例外。將文件放在 `using` 區塊中載入，可確保檔案句柄自動釋放。

## 步驟 3：確保 ExtGState 字典已存在

```csharp
// The page’s Resources dictionary holds many sub‑dictionaries (Font, XObject, etc.)
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);

// Try to get the existing ExtGState dictionary; create one if it is missing
CosCosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create an empty ExtGState dictionary and attach it to the page resources
    extGStateDict = CosCosPdfDictionary.CreateEmptyDictionary(pdfDoc);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

**小技巧**：務必先檢查 `ExtGState` 是否存在。有些 PDF 產生時未包含此字典，若直接編輯不存在的條目會引發 `KeyNotFoundException`。

## 步驟 4：建立新的圖形狀態

```csharp
// Create a fresh dictionary for the new graphics state
CosCosPdfDictionary newGraphicsState = CosCosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Stroke opacity (CA) – 1.0 means fully opaque
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes the fill 50 % transparent
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default compositing operation
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

*為什麼要這樣設定*：  
- `CA` 影響線條與邊框（描邊）。  
- `ca` 影響填充形狀與文字。  
- `BM` 決定來源顏色與目標顏色的混合方式；`"Normal"` 會保留原始外觀，同時遵守不透明度設定。

## 步驟 5：將圖形狀態插入 ExtGState 字典

```csharp
// Choose a unique name for the graphics state; "GS0" is common for the first entry
extGStateDict.Add("GS0", newGraphicsState);
```

若需要多個狀態，只需遞增後綴（`GS1`、`GS2`…），之後在內容串流中引用相應名稱即可。

## 步驟 6：儲存已修改的 PDF

```csharp
pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
Console.WriteLine("PDF saved with new graphics state.");
```

產生的檔案（`output.pdf`）在視覺內容上與原始檔相同，但任何之後引用 `/GS0` 的繪圖指令，將以 **PDF 不透明度** 0.5 以及 **PDF 混合模式** `Normal` 呈現。

## 完整可執行範例

將下列程式碼複製到步驟 1 建立的專案的 `Program.cs` 中。將 `YOUR_DIRECTORY` 佔位符替換為您實際的路徑。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.IO;

namespace PdfGraphicsStateDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the PDF document
            using var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");

            // 2️⃣ Access the first page's resources
            Page firstPage = pdfDoc.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // 3️⃣ Retrieve or create ExtGState dictionary
            CosCosPdfDictionary extGStateDict;
            if (resourcesEditor.ContainsKey("ExtGState"))
            {
                extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
            }
            else
            {
                extGStateDict = CosCosPdfDictionary.CreateEmptyDictionary(pdfDoc);
                resourcesEditor["ExtGState"] = extGStateDict;
            }

            // 4️⃣ Define a new graphics state (opacity & blend mode)
            var newGraphicsState = CosCosPdfDictionary.CreateEmptyDictionary(pdfDoc);
            newGraphicsState.Add("CA", new CosPdfNumber(1));           // stroke opacity
            newGraphicsState.Add("ca", new CosPdfNumber(0.5));         // fill opacity
            newGraphicsState.Add("BM", new CosPdfName("Normal"));     // blend mode

            // 5️⃣ Add the graphics state to the ExtGState dictionary
            extGStateDict.Add("GS0", newGraphicsState);

            // 6️⃣ Save the modified PDF
            pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
            Console.WriteLine("PDF saved with new graphics state.");
        }
    }
}
```

### 預期結果

在任意檢視器中開啟 `output.pdf`。若之後加入引用 `/GS0` 的繪圖指令（例如透過內容串流或其他 Aspose.Pdf API 呼叫），填充將以 50 % 不透明度顯示，描邊則保持完全不透明。混合模式保持為 `"Normal"`，適用於大多數合成情境。

## 常見變化處理

| 情境 | 需要變更的地方 | 原因 |
|-----------|----------------|--------|
| **多頁需要相同狀態** | 在 `pdfDoc.Pages` 上迴圈，對每頁重複步驟 3‑5，或在文件全域資源中建立單一 ExtGState 字典，然後讓每頁引用它。 | 避免重複字典，減少檔案大小。 |
| **每頁不同的不透明度** | 使用不同名稱（`GS0`、`GS1`…）並在加入每頁的 ExtGState 前調整 `ca`/`CA`。 | 提供細緻的渲染控制。 |
| **ExtGState 已包含名為 “GS0” 的鍵** | 改用其他鍵名（`GS1`、`MyState`…），並更新所有引用該鍵的內容串流。 | 防止意外覆寫既有圖形狀態。 |
| **PDF 未產生 ExtGState 字典** | 步驟 3 的程式碼已會自行建立字典，無需額外處理。 | 確保任何輸入 PDF 都能順利執行。 |

## 小技巧與最佳實踐

* **在修改後驗證 PDF** – 使用 `pdfDoc.Validate()`（在較新版本的 Aspose.Pdf 中提供）可提前捕捉結構問題。  
* **保持圖形狀態字典精簡** – 只保留必要條目，額外鍵會增加檔案大小卻無實質效益。  
* **在加入使用新狀態的內容串流時**，於繪圖運算子前加上 `/GS0 gs`。例如：`contentStream.Append("/GS0 gs 100 100 m 200 200 l S");`  
* **及時釋放大型 PDF** – 範例中的 `using` 陳述式可確保檔案句柄被釋放，這在 Web 服務情境下尤為重要。

## 結論

您現在已掌握如何使用 Aspose.Pdf **新增圖形狀態 PDF**、操作 **PDF 不透明度**、設定 **PDF 混合模式**，以及安全地處理 **ExtGState 字典**。完整程式碼範例可直接放入任何 .NET 專案，配合本文提供的技巧，可避免常見的陷阱。

接下來，您可以探索如何將新建立的圖形狀態套用於文字、影像或向量圖形。亦可研究其他 ExtGState 條目，如 `SM`（描邊調整）或大於 1 的 `CA` 值，以實現更特殊的效果。祝您 PDF 開發順利！

## 接下來該學什麼？

以下教學與本指南緊密相關，能在此基礎上延伸技術。每篇資源皆包含完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能並探索替代實作方式。

- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET: A Complete Guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Add Image Stamps to PDFs Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)
- [How to Remove Graphics from PDFs Using Aspose.PDF .NET: A Complete Guide](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}