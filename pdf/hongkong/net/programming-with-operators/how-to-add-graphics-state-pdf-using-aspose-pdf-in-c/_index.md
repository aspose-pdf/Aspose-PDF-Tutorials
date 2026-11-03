---
category: general
date: 2026-09-28
description: 了解如何在 C# 中使用 Aspose.PDF 新增圖形狀態 PDF。本分步指南將教您如何設定 PDF 頁面的不透明度與混合模式。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- Aspose PDF graphics state
- PDF opacity settings
- modify PDF resources
- Aspose.Pdf DictionaryEditor
language: zh-hant
lastmod: 2026-09-28
og_description: 使用 Aspose.PDF 在 C# 中新增圖形狀態 PDF。依照本指南，可在任何 PDF 頁面上變更描邊/填充的不透明度與混合模式。
og_image_alt: Screenshot of a PDF page after adding graphics state pdf with opacity
  settings
og_title: 使用 Aspose.PDF 為 PDF 添加圖形狀態 – 完整 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-09-28'
  description: Learn how to add graphics state pdf with Aspose.PDF in C#. This step‑by‑step
    guide shows you how to set opacity and blend mode for PDF pages.
  headline: How to add graphics state pdf using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: 如何在 C# 中使用 Aspose.PDF 添加圖形狀態 PDF
url: /zh-hant/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.PDF 新增圖形狀態 (Graphics State) PDF

如果您需要 **新增圖形狀態 PDF** 以控制不透明度或混合模式，本教學將一步步示範操作方式。透過 Aspose.PDF，您只需幾行程式碼即可編輯頁面的資源字典，注入自訂的圖形狀態。

您將學會如何載入 PDF、建立新的圖形狀態字典、設定描邊不透明度、填充不透明度與混合模式，最後儲存修改後的文件。此過程不需要任何外部工具——只需 Aspose.PDF for .NET 套件。

## 前置條件

在開始之前，請確保您已具備：

* .NET 6.0 或更新版本（程式碼同樣支援 .NET Core 3.1 與 .NET Framework 4.7+）
* 有效的 **Aspose.PDF for .NET** 授權（免費試用版可用於評估）
* 一個放在已知資料夾中的輸入 PDF 檔案（`input.pdf`）
* Visual Studio 2022 或您偏好的 C# 編輯器

> **專業提示：** 請將 PDF 檔案放在專案資料夾之外，以免不小心將大型二進位檔提交至版本控制系統。

## 步驟 1：安裝 Aspose.PDF NuGet 套件

在專案目錄的終端機執行：

```bash
dotnet add package Aspose.Pdf
```

此套件會提供 `Aspose.Pdf` 命名空間，其中包含稍後會使用的 `Document`、`DictionaryEditor` 與 `CosPdfDictionary` 類別。

## 步驟 2：載入 PDF 文件

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Path to the source PDF
string pdfPath = @"C:\MyPdfs\input.pdf";

// The `using` statement ensures the document is disposed automatically
using var pdfDocument = new Document(pdfPath);
```

*此步驟的重要性*：載入 PDF 後會在記憶體中產生可供操作的表示。`Document` 物件讓您可以存取頁面、資源與低階 COS 物件，這些都是 **新增圖形狀態 PDF** 所必需的。

## 步驟 3：存取第一頁的資源

```csharp
// Get the first page (pages are 1‑based in Aspose.PDF)
Page firstPage = pdfDocument.Pages[1];

// Create a DictionaryEditor to work with the page’s resource dictionary
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`Resources` 字典保存了字型、影像以及 **ExtGState** 條目等物件。編輯此字典是安全 **修改 PDF 資源** 的唯一途徑。

## 步驟 4：取得（或建立）ExtGState 字典

```csharp
// Try to get the existing ExtGState dictionary; if it does not exist, create one
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
```

*此步驟的重要性*：`ExtGState` 條目儲存圖形狀態物件。若 PDF 已有此條目，我們會重複使用；若沒有，則建立全新字典，確保 **新增圖形狀態 PDF** 的操作不會失敗。

## 步驟 5：建立新的圖形狀態字典

```csharp
// Create an empty dictionary that will hold our graphics state parameters
CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Stroke opacity (CA) – 1.0 means fully opaque strokes
graphicsStateDict.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes filled shapes 50 % transparent
graphicsStateDict.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default PDF blend mode
graphicsStateDict.Add("BM", new CosPdfName("Normal"));
```

`CA`、`ca` 與 `BM` 鍵是 PDF 規範所定義。設定這些鍵即可控制 **PDF 不透明度設定** 以及後續繪圖指令的混合行為。

## 步驟 6：在 ExtGState 中註冊新圖形狀態

```csharp
// Choose a unique name for the graphics state, e.g., GS0
extGStateDict.Add("GS0", graphicsStateDict);
```

現在頁面的資源字典已包含名為 `GS0` 的新條目。當您在內容串流中引用 `GS0` 時，PDF 瀏覽器會套用先前定義的不透明度與混合模式。

## 步驟 7：（可選）將圖形狀態套用至現有內容

若要修改已存在的繪圖指令，必須編輯頁面的內容串流。以下範例示範在任何繪圖發生前，先在內容串流最前端加入 `gs` 運算子以設定圖形狀態：

```csharp
// Retrieve the page’s content stream as a string
string originalContent = firstPage.Contents[1].ToString();

// Prepend the graphics state operator
string updatedContent = "GS0 gs\n" + originalContent;

// Replace the page content with the updated stream
firstPage.Contents[1].Replace(updatedContent);
```

> **注意：** 直接操作內容串流相當精細，請務必先在 PDF 副本上測試。

## 步驟 8：儲存修改後的 PDF

```csharp
string outputPath = @"C:\MyPdfs\output.pdf";
pdfDocument.Save(outputPath);
```

儲存完成後，使用 PDF 閱讀器開啟 `output.pdf`。任何在 `GS0 gs` 運算子之後繪製的填充形狀，都會以 50 % 的填充不透明度呈現，而描邊則保持完全不透明，證明您已成功 **新增圖形狀態 PDF**。

### 預期結果

| 之前 | 之後（使用 GS0） |
|--------|------------------|
| ![Original PDF page](placeholder-before.png){.img-fluid alt="原始 PDF 頁面"} | ![PDF page after adding graphics state pdf with opacity settings](placeholder-after.png){.img-fluid alt="加入圖形狀態（不透明度設定）後的 PDF 頁面"} |

“之後”欄位顯示填充半透明，而描邊仍保持實心，正如圖形狀態字典中所定義的效果。

## 常見問題與邊緣案例

| 問題 | 解答 |
|----------|--------|
| **我可以新增多個圖形狀態嗎？** | 可以。只要在 `extGStateDict` 中再加入其他條目（`GS1`、`GS2` …），並在內容串流中引用相應名稱即可。 |
| **如果 PDF 已經使用了 `GS0` 這個名稱怎麼辦？** | 請改用唯一的識別碼（例如 `GS_custom1`）。在加入前可先檢查 `extGStateDict.Keys`。 |
| **這個方法能處理加密的 PDF 嗎？** | 必須使用正確的密碼開啟 PDF。範例：`new Document(pdfPath, new LoadOptions { Password = "secret" })`。 |
| **混合模式只能是 “Normal” 嗎？** | 不限。PDF 規範支援多種混合模式（`Multiply`、`Screen`、`Overlay` 等），只要將 `"Normal"` 替換為支援的名稱即可。 |
| **會不會影響其他頁面？** | 只會影響您編輯資源的那一頁。若需在多頁使用相同狀態，請對每一頁重複步驟 3‑6，或編輯文件的全域資源。 |

## 結論

現在您已掌握如何使用 Aspose.PDF for .NET **新增圖形狀態 PDF**，設定描邊與填充不透明度、選擇混合模式，並可選擇性地將此狀態套用至既有內容。此技巧讓您在不將 PDF 轉為影像的前提下，對 PDF 渲染擁有精細的控制權。

接下來，您可以探索：

* **PDF 不透明度設定**，應用於影像與文字區塊
* 使用 **Aspose.Pdf DictionaryEditor** 取代字型或嵌入自訂 ICC 色彩描述檔
* 結合多個圖形狀態以產生複雜的視覺效果

歡迎嘗試不同的不透明度數值、混合模式與資源範圍。熟悉這些低階 PDF 操作後，您將能開發出更高階的文件產生與遮蔽方案。

---


## 接下來該學什麼？

以下教學與本篇內容緊密相關，能進一步深化您所學的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，助您掌握更多 API 功能，並在專案中探索其他實作方式。

- [How to Add Stamp to PDF with Aspose.Pdf – Step‑by‑Step Guide](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-stamp-to-pdf-with-aspose-pdf-step-by-step-guide/)
- [How to Add Images to PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/add-images-to-pdfs-aspose-pdf-net/)
- [How to Remove Graphics from PDFs Using Aspose.PDF .NET&#58; A Complete Guide](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}