---
category: general
date: 2026-10-26
description: 學習使用 Aspose.PDF for C# 建立空的 PDF 字典並編輯 PDF 資源。一步一步的指南，附完整程式碼範例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- edit PDF resources
- Aspose.PDF C#
- PDF manipulation C#
- PDF graphics state
language: zh-hant
lastmod: 2026-10-26
og_description: 使用 Aspose.PDF for C# 建立空的 PDF 字典並編輯 PDF 資源。請參考此完整教學，了解如何在 PDF 中修改圖形狀態。
og_image_alt: Screenshot showing creation of empty PDF dictionary in Aspose.PDF
og_title: 在 C# 中建立空的 PDF 字典並編輯 PDF 資源 – Aspose.PDF 指南
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  headline: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  type: TechArticle
- description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  name: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  steps:
  - name: Populate the graphics state entries
    text: 'Add the standard keys:'
  - name: Register the new graphics state in the resource dictionary
    text: Give the state a name (`GS0`) and add it to the `ExtGState` dictionary that
      lives inside the page resources.
  - name: Expected output
    text: 'Running the program prints:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF
title: 如何在 C# 中使用 Aspose.PDF 建立空的 PDF 字典並編輯 PDF 資源
url: /zh-hant/net/programming-with-document/how-to-create-empty-pdf-dictionary-and-edit-pdf-resources-wi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.PDF 建立空的 PDF 字典並編輯 PDF 資源

如果您需要在 C# 應用程式中**建立空的 PDF 字典**，然後**編輯 PDF 資源**，本指南將向您展示完整步驟。您將看到一個完整、可執行的範例，將自訂圖形狀態新增至現有 PDF 的第一頁。

操作低階 PDF 物件可能會讓人感到困難，但 Aspose.PDF 提供了清晰的 API 來處理字典。完成本教學後，您將了解每個操作的意義，以及如何將程式碼套用到其他資源類型。

## 前置條件

* .NET 6.0（或更新版本）已安裝。
* 取得 **Aspose.PDF for .NET** 的授權版——免費試用版可用於測試。
* 使用如 Visual Studio 2022 的 IDE。
* 將名為 `input.pdf` 的 PDF 檔放在程式碼可參考的資料夾中。

無需其他 NuGet 套件，僅需 `Aspose.Pdf`。

## 步驟 1：設定專案並匯入命名空間

建立一個新的主控台專案，並加入 Aspose.PDF 套件：

```bash
dotnet new console -n PdfDictionaryDemo
cd PdfDictionaryDemo
dotnet add package Aspose.Pdf
```

在 `Program.cs` 中匯入您將使用的命名空間：

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
```

這些匯入會公開 `Document`、`DictionaryEditor` 與 COS（Canonical Object Structure）類別，讓您能**建立空的 PDF 字典**物件並修改現有的資源字典。

## 步驟 2：定義存放 PDF 檔案的資料夾

指定保存 `input.pdf` 的目錄。使用絕對路徑可避免程式在不同工作目錄執行時產生歧義。

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfDemo\";
```

將 `C:\PdfDemo\` 替換為您機器上的路徑。將路徑存於變數中，可方便於輸入與輸出檔案皆使用。

## 步驟 3：開啟來源 PDF 文件

在 `using` 區塊內載入您要修改的 PDF，讓檔案句柄自動釋放。

```csharp
// Step 2: Open the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // The rest of the workflow lives inside this block
}
```

開啟文件後，您即可存取其頁面集合、資源字典以及低階 COS 物件。

## 步驟 4：存取第一頁及其資源字典

第一頁的索引為 `1`（PDF 頁碼從 1 開始）。取得該頁的 `Resources` 字典，並以 `DictionaryEditor` 包裝，以便安全編輯。

```csharp
// Step 3: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` 抽象化底層 COS 結構，讓您能在不損壞 PDF 的情況下讀取或建立條目。

## 步驟 5：為新圖形狀態**建立空的 PDF 字典**

圖形狀態控制透明度、混合模式及其他繪圖參數。若要新增自訂狀態，首先需要一個空字典，然後填入必要的條目。

```csharp
// Step 4: Retrieve the ExtGState dictionary and add a new graphics state
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

// Create an empty dictionary that will hold the graphics state parameters
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
```

呼叫 `CreateEmptyDictionary` 是**建立空的 PDF 字典**物件的核心。它會回傳屬於同一文件的 COS 字典，確保交叉參照的完整性。

### 填入圖形狀態的條目

加入標準鍵值：

* `CA` – 描邊的 alpha 常數（範圍 0 – 1）。
* `ca` – 非描邊的 alpha 常數。
* `BM` – 混合模式名稱。

```csharp
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

每個條目皆加入您剛建立的空字典。將定義與插入迴圈分開，可提升程式碼可讀性，且日後若需加入其他鍵值也更容易擴充。

### 在資源字典中註冊新圖形狀態

給予此狀態一個名稱（`GS0`），並將它加入頁面資源內的 `ExtGState` 字典。

```csharp
// Name the new graphics state "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

現在頁面的資源字典已包含對自訂圖形狀態的參照，之後您即可將其套用至內容串流。

## 步驟 6：儲存更新後的 PDF

最後，將修改過的文件寫入新檔案。保留原始檔不變有助於驗證變更。

```csharp
// Step 5: Save the updated PDF
pdfDocument.Save(dataDir + "output.pdf");
```

當您在支援圖形狀態檢查的檢視器（例如 Adobe Acrobat Pro）中開啟 `output.pdf` 時，會看到 `ExtGState` 字典中有名為 `GS0` 的條目，且其值為您先前設定的內容。

## 完整原始碼

將所有片段組合起來即可得到一個自包含的程式：

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

class Program
{
    static void Main()
    {
        // Step 1: Define the folder that contains the PDF files
        string dataDir = @"C:\PdfDemo\"; // adjust to your environment

        // Step 2: Open the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Step 3: Access the first page and its resource dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 4: Retrieve the ExtGState dictionary and add a new graphics state
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // **Create empty PDF dictionary** for the new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateEntries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };

            foreach (var entry in graphicsStateEntries)
                newGraphicsState.Add(entry);

            // Register the new graphics state as "GS0"
            extGStateDict.Add("GS0", newGraphicsState);

            // Step 5: Save the updated PDF
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

### 預期輸出

執行程式會印出：

```
PDF updated successfully.
```

並在同一資料夾產生 `output.pdf`。開啟該檔案會在 **Resources → ExtGState → GS0** 下看到您設定的參數新條目。

## 常見變化與邊緣情況

| 情況 | 如何調整程式碼 |
|-----------|-----------------------|
| **多頁面** 需要相同的圖形狀態 | 先建立一次字典，然後將相同的 `GS0` 參照加入每一頁的 `ExtGState` 字典中。 |
| **不同的混合模式**（例如 `Multiply`） | 將 `CosPdfName("Normal")` 的值改為 `CosPdfName("Multiply")`。 |
| **不存在 ExtGState 字典** | 在存取 `resourcesEditor["ExtGState"]` 前，先檢查 `resourcesEditor.ContainsKey("ExtGState")`。若不存在，建立一個新的空字典並加入 `firstPage.Resources`。 |
| **大型 PDF** 造成記憶體壓力 | 使用支援分頁串流的 `PdfDocument.Load` 重載，或在 `using` 區塊內一次處理一頁。 |
| **需要編輯其他資源**（字型、XObject） | 在 `resourcesEditor` 查找時將 `"ExtGState"` 換成 `"Font"` 或 `"XObject"`，然後依照相同的建立空字典並填入內容的模式進行。 |

這些變化說明了相同的**建立空的 PDF 字典**模式如何套用於任何您想要**編輯 PDF 資源**的資源類型。

## 專業技巧

* **驗證結果** – 儲存後，使用能顯示原始資源字典的工具（例如 PDF‑Box 的 `PDFDebugger`）開啟 PDF，以確保條目存在。
* **重複使用字典** – 若將相同的圖形狀態加入多個頁面，請將字典存於變數中並引用，而非每次都重新建立。
* **版本相容性** – 此程式碼適用於 Aspose.PDF 23.12 及以上版本。較早版本可能需要使用 `CosDictionary` 取代 `CosPdfDictionary`。

## 結論

現在您已了解如何使用 Aspose.PDF for C# **建立空的 PDF 字典** 物件並 **編輯 PDF 資源**。本教學涵蓋了開啟文件、存取頁面資源字典、建立自訂圖形狀態、註冊以及儲存結果的步驟。接下來您可以嘗試其他資源類型、結合多個圖形狀態，或將此技術整合至更大的 PDF 處理流程中。

---

*想進一步探索嗎？試著將自訂 **ExtGState** 加入內容串流，或操作 **Font** 字典以嵌入新字型。兩者皆遵循相同的建立空字典並編輯 PDF 資源的模式。*

## 接下來該學什麼？

以下教學涵蓋與本指南技術緊密相關的主題。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，並在自己的專案中探索其他實作方式。

- [Edit PDF Resource Dictionary with Aspose.PDF – C# Guide](/pdf/english/net/programming-with-operators/edit-pdf-resource-dictionary-with-aspose-pdf-c-guide/)
- [Create custom graphics state in PDF using Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [How to create empty graphics state in a PDF with C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}