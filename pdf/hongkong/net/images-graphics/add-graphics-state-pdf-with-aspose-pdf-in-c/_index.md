---
category: general
date: 2026-10-07
description: 使用 Aspose.Pdf 於 C# 新增圖形狀態 PDF，以修改 PDF 透明度。請按照本分步指南嵌入自訂圖形狀態並控制不透明度。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- modify pdf transparency
language: zh-hant
lastmod: 2026-10-07
og_description: 使用 Aspose.Pdf 在 C# 中新增圖形狀態 PDF。了解如何透過建立自訂圖形狀態字典來修改 PDF 的透明度。
og_image_alt: Screenshot showing the add graphics state pdf code editor in Visual
  Studio
og_title: 使用 Aspose.Pdf 為 PDF 添加圖形狀態 – 控制 PDF 透明度
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Add graphics state pdf using Aspose.Pdf in C# to modify PDF transparency.
    Follow this step‑by‑step guide to embed custom graphics states and control opacity.
  headline: Add graphics state pdf with Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: 在 C# 中使用 Aspose.Pdf 添加圖形狀態 PDF
url: /zh-hant/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Pdf 在 C# 中加入圖形狀態 (graphics state) PDF

如果您需要 **在 PDF 中加入圖形狀態**，本教學將會一步步示範如何使用 Aspose.Pdf for .NET 完成。完成本指南後，您也會了解如何 **修改 PDF 透明度**，讓您能在任何繪圖操作上設定自訂的不透明度值。

操作 PDF 圖形狀態可讓您控制線寬、混合模式，以及本文最關注的內容透明度。以下步驟針對熟悉 C# 的開發者編寫，提供即用即跑的解決方案，無需深入官方 SDK 文件。

## 您將學會

* 如何建立新的圖形狀態字典，並填入 `CA`、`ca` 與 `BM` 三個條目。  
* 如何將該字典插入頁面的 `ExtGState` 資源，使 PDF 能辨識它。  
* `ca`（描邊）與 `CA`（填充）值如何影響 **修改 PDF 透明度**，進而影響後續的繪圖指令。  
* 常見的陷阱，例如命名衝突與版本相容性，以及延伸圖形狀態的進階技巧。

**先備條件**

* .NET 6.0 或更新版本（此程式碼亦相容 .NET Framework 4.7+）。  
* 有效的 Aspose.Pdf for .NET 授權（免費評估版可用於測試）。  
* Visual Studio 2022 或您慣用的任何 C# IDE。  

---

## 步驟 1：安裝 Aspose.Pdf for .NET

將 NuGet 套件加入您的專案：

```bash
dotnet add package Aspose.Pdf
```

此套件會包含 `Aspose.Pdf` 命名空間，提供稍後會用到的 `Document`、`DictionaryEditor` 與 `CosPdfDictionary` 類別。

> **專業提示：** 若您打算批次處理大量 PDF，請在 `Program.cs` 內盡早啟用 **License**，以避免評估版浮水印。

```csharp
// Apply your license (optional for evaluation)
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Aspose.Pdf.lic");
```

## 步驟 2：定義輸入與輸出路徑

必須將 SDK 指向既有的 PDF（`input.pdf`），並指定修改後的檔案儲存位置（`output.pdf`）。

```csharp
// Define input and output PDF file paths
string inputPath = @"C:\MyPdfs\input.pdf";
string outputPath = @"C:\MyPdfs\output.pdf";
```

> **為何重要：** 使用絕對路徑可避免 SDK 在錯誤的工作目錄中尋找檔案，這是導致 `FileNotFoundException` 的常見原因。

## 步驟 3：開啟 PDF 並定位第一頁的資源

`ExtGState` 字典位於每一頁的資源字典內。為了簡化說明，我們以第一頁為例，其他頁面的操作方式相同。

```csharp
using (var pdfDocument = new Aspose.Pdf.Document(inputPath))
{
    // Get the first page (pages are 1‑based)
    var firstPage = pdfDocument.Pages[1];

    // Access the page’s resource dictionary via DictionaryEditor
    var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);

    // Retrieve (or create) the ExtGState entry
    var extGStateDict = resourcesEditor["ExtGState"]
        .ToCosPdfDictionary(); // Throws if ExtGState does not exist
```

**特殊情況：** 若頁面沒有 `ExtGState` 條目，必須自行建立：

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
{
    var emptyDict = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", emptyDict);
    extGStateDict = emptyDict;
}
```

## 步驟 4：建立新的圖形狀態字典

圖形狀態是一組描述繪圖行為的鍵/值對。針對透明度，我們需要三個鍵：

| 鍵   | 說明   | 常見值 |
|-----|--------|--------|
| `CA` | 填充不透明度（0 = 完全透明，1 = 完全不透明） | `1`（完全不透明） |
| `ca` | 描邊不透明度（同樣的比例） | `0.5`（50 % 透明） |
| `BM` | 混合模式（例如 `Normal`、`Multiply`） | `Normal` |

```csharp
    // Create an empty dictionary that will hold the graphics state
    var newGraphicsState = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Populate the dictionary with transparency and blend mode entries
    var graphicsStateEntries = new[]
    {
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "CA", new Aspose.Pdf.CosPdfNumber(1)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "ca", new Aspose.Pdf.CosPdfNumber(0.5)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "BM", new Aspose.Pdf.CosPdfName("Normal"))
    };

    foreach (var entry in graphicsStateEntries)
        newGraphicsState.Add(entry);
```

**為何使用這些值？**  
`ca = 0.5` 會讓任何描邊的路徑（線條、邊框）以 50 % 透明度呈現，而 `CA = 1` 則讓填充形狀保持完全不透明。您可自行調整這兩個數值，以達到所需的 **修改 PDF 透明度** 效果。

## 步驟 5：將圖形狀態插入 ExtGState 字典

必須為新狀態指定唯一名稱（例如 `GS0`）。若名稱已存在，Aspose.Pdf 會覆寫原有條目，可能會破壞依賴該狀態的其他內容。

```csharp
    // Add the new graphics state under a custom name
    const string stateName = "GS0";

    // Ensure we don’t clash with an existing entry
    if (extGStateDict.ContainsKey(stateName))
        extGStateDict.Remove(stateName);

    extGStateDict.Add(stateName, newGraphicsState);
```

現在頁面的資源已認識 `GS0`。若要實際使用它，您需要在內容串流中以 `gs` 運算子引用此圖形狀態（例如 `GS0 gs`）。Aspose.Pdf 允許您注入原始 PDF 運算子，以便自行繪製自訂圖形。

## 步驟 6：儲存修改後的 PDF

```csharp
    // Persist the changes to a new file
    pdfDocument.Save(outputPath);
}
```

產生的 `output.pdf` 仍保留原始的視覺內容，但任何後續使用 `GS0` 的繪圖指令，都會遵循您先前設定的透明度。

### 預期結果

在 Adobe Acrobat 或任何 PDF 閱讀器中開啟 `output.pdf`。若您使用 `GS0` 圖形狀態新增一條描邊線（例如透過 `pdfDocument.Pages[1].Contents.Add(...)`），該線條會呈現半透明，而填充仍保持不透明。這證明您已成功 **加入圖形狀態 PDF** 並 **修改 PDF 透明度**。

---

## 完整可執行範例

以下程式碼可直接貼到 Console 應用程式中執行，內含授權載入、錯誤處理與說明每一步的註解。



## 接下來您可以學習什麼？

以下教學與本指南的技巧密切相關，提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，並在專案中探索其他實作方式。

- [Add Transparency to PDF with Aspose PDF in C# – Step‑by‑Step Guide](/pdf/english/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Add Transparency to PDF using Aspose – Complete C# Guide](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [How to Add an Image Stamp to a PDF Using Aspose.PDF for .NET: A Comprehensive Guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}