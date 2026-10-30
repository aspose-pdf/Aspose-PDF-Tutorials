---
category: general
date: 2026-10-10
description: 學習如何使用 Aspose.PDF 將 PDF 儲存為 HTML，並跳過點陣圖像。本指南涵蓋將 PDF 轉換為 HTML 以及高效地將文件儲存為
  HTML。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save pdf as html
- convert pdf to html
- aspose pdf to html
- save pdf without images
- save document as html
language: zh-hant
lastmod: 2026-10-10
og_description: 使用 Aspose.PDF 將 PDF 另存為 HTML，並跳過點陣圖。請參考此完整教學，將 PDF 轉換為 HTML 並將文件儲存為
  HTML。
og_image_alt: Screenshot showing PDF saved as HTML without images using Aspose.PDF
og_title: 將 PDF 儲存為不含圖片的 HTML – Aspose.PDF 步驟指南
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to save PDF as HTML with Aspose.PDF, skipping raster images.
    This guide covers convert PDF to HTML and save document as HTML efficiently.
  headline: How to save PDF as HTML without images using Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- HTML conversion
title: 如何使用 Aspose.PDF 將 PDF 儲存為不含圖片的 HTML
url: /zh-hant/net/document-conversion/how-to-save-pdf-as-html-without-images-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在不含圖像的情況下使用 Aspose.PDF 將 PDF 儲存為 HTML

如果您需要在省略所有點陣圖的情況下 **將 PDF 儲存為 HTML**，本教學將完整說明操作方式。透過設定 `HtmlSaveOptions`，您可以有效地將 PDF 轉換為 HTML，並保持輸出檔案輕量化——非常適合網頁友善的文件或 SEO 優化的頁面。

除了移除圖像外，本指南亦示範更廣泛的 **convert PDF to HTML** 工作流程，讓您最終得到一個保留文字、向量圖形與版面配置的乾淨 HTML 檔案。無需任何外部工具；所有操作皆在標準 .NET 專案中執行。

## 前置條件

* .NET 6.0 或更新版本（程式碼亦可於 .NET Framework 4.6+ 執行）
* 有效的 Aspose.PDF for .NET 授權（或免費評估金鑰）
* 位於已知目錄的輸入 PDF 檔案
* Visual Studio 2022（或任何 C# IDE）

以上項目足以編譯並執行稍後示範的範例程式碼。

## 步驟 1：安裝 Aspose.PDF NuGet 套件

首先，您必須將 Aspose.PDF 函式庫加入專案中：

```bash
dotnet add package Aspose.PDF
```

執行此指令會還原最新的穩定版 Aspose.PDF，其中包含轉換所需的 `HtmlSaveOptions` 類別。

## 步驟 2：載入來源 PDF 文件

使用 `Document` 類別載入 PDF 非常簡單。此類別在記憶體中表示整個 PDF 檔案。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Saving;

// Step 2: Load the source PDF document
Document doc = new Document(@"C:\MyFiles\input.pdf");
```

*此步驟的重要性：*  
`Document` 會解析 PDF 結構，讓您取得頁面、字型與資源。若未先載入檔案，則無法套用任何儲存選項。

## 步驟 3：設定 HTML 儲存選項以跳過點陣圖

`HtmlSaveOptions` 物件讓您微調 HTML 輸出。將 `SkipRasterImages` 設為 `true`，即可指示 Aspose.PDF 在轉換過程中忽略所有點陣圖（JPEG、PNG、GIF）。

```csharp
// Step 3: Configure HTML save options to skip raster images
HtmlSaveOptions htmlOpts = new HtmlSaveOptions
{
    // Exclude all raster (bitmap) images from the output HTML
    SkipRasterImages = true,

    // Optional: embed fonts as Base64 to avoid external font files
    EmbedFonts = true,

    // Optional: preserve the original layout as closely as possible
    FixedLayout = true
};
```

*此步驟的重要性：*  
點陣圖通常佔據檔案大小的主要部分。跳過它們即可產生更輕量的 HTML 檔案，載入更快且更易被搜尋引擎索引。額外的選項（`EmbedFonts`、`FixedLayout`）僅為完整性示範，並非移除圖像所必需。

## 步驟 4：將文件儲存為不含圖像的 HTML

現在您可以將轉換後的內容寫入磁碟。`Save` 的多載接受目標路徑、欲使用的 `SaveFormat`，以及先前設定的選項。

```csharp
// Step 4: Save the document as HTML without raster images
doc.Save(@"C:\MyFiles\no_images.html", SaveFormat.Html, htmlOpts);
```

呼叫完成後，`no_images.html` 會包含文字內容、向量圖形與 CSS，重建原始 PDF 版面——但不含任何點陣圖。

### 預期輸出

在瀏覽器中開啟 `no_images.html`。您應該會看到：

* 原始 PDF 中的所有標題、段落與表格。
* 向量圖形（例如 SVG 形狀）正確呈現。
* 沒有引用點陣檔案的 `<img>` 標籤；此類標籤會完整省略。

若檢視 HTML 原始碼，您會發現缺少 `<img src="...">` 元素，證實 `SkipRasterImages` 已如預期運作。

## 完整、可執行的範例

以下是一個獨立的主控台應用程式，將所有步驟整合在一起。將程式碼複製到新的 .NET 主控台專案中並執行。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Saving;

namespace PdfToHtmlNoImages
{
    class Program
    {
        static void Main(string[] args)
        {
            // Input and output paths – adjust to your environment
            string inputPath = @"C:\MyFiles\input.pdf";
            string outputPath = @"C:\MyFiles\no_images.html";

            // 1. Load the PDF document
            Document doc = new Document(inputPath);
            Console.WriteLine($"Loaded PDF: {inputPath}");

            // 2. Set up HTML save options to omit raster images
            HtmlSaveOptions htmlOpts = new HtmlSaveOptions
            {
                SkipRasterImages = true,
                EmbedFonts = true,
                FixedLayout = true
            };
            Console.WriteLine("Configured HtmlSaveOptions to skip raster images.");

            // 3. Save as HTML
            doc.Save(outputPath, SaveFormat.Html, htmlOpts);
            Console.WriteLine($"PDF saved as HTML without images at: {outputPath}");
        }
    }
}
```

**執行程式** 會在主控台印出進度訊息，並產生 `no_images.html`。可透過任何現代瀏覽器開啟以驗證檔案。

## 常見變形與邊緣情況

| Situation | How to adapt the code |
|-----------|-----------------------|
| **保留點陣圖** | 將 `SkipRasterImages = false`（或省略此屬性）。 |
| **僅轉換特定頁範圍** | 使用 `doc.Pages.Delete(pageNumber)` 於儲存前移除不需要的頁面，或設定 `htmlOpts.PageIndex` 與 `htmlOpts.PageCount`。 |
| **將每個 PDF 頁面儲存為單獨的 HTML 檔案** | 將 `htmlOpts.SplitIntoPages = true`；函式庫會產生 `output_page1.html`、`output_page2.html` 等檔案。 |
| **壓縮產生的 HTML** | 儲存後，對檔案執行壓縮工具，或設定 `htmlOpts.Compress = true`（在較新版本的 Aspose 中可用）。 |
| **處理受密碼保護的 PDF** | 將密碼傳遞給 `Document` 建構子：`new Document(inputPath, new LoadOptions { Password = "secret" })`。 |

## 專業提示

* **盡早授權** – 在載入文件前註冊 Aspose.PDF 授權，以避免評估水印。
* **效能** – 對於大型 PDF，重複使用同一個 `HtmlSaveOptions` 實例，並考慮啟用 `htmlOpts.UseZOrder = true` 以加速重疊元素的渲染。
* **測試** – 比較有無圖像的 HTML 檔案大小，以量化 `SkipRasterImages` 的效益。

## 結論

您現在已了解如何使用 Aspose.PDF for .NET **將 PDF 儲存為 HTML**，同時移除點陣圖形。完整流程——載入 PDF、以 `SkipRasterImages` 設定 `HtmlSaveOptions`，再儲存結果——涵蓋了基本的 **convert PDF to HTML** 使用情境，且可延伸至頁面範圍轉換、逐頁輸出或其他最佳化。

接下來，您可以探索使用嵌入式 CSS 的 **save document as HTML**，或嘗試 `SvgSaveOptions` 類別以產生可縮放向量圖形取代 HTML。這兩種方法皆可進一步減少檔案大小，提升現代 Web 應用程式的回應速度。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在此處示範的技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [在 .NET 中使用 Aspose.PDF 轉換 PDF 為 HTML（不儲存圖像）](/pdf/english/net/conversion-export/convert-pdf-html-net-asposepdf-no-images/)
- [使用 Aspose.PDF .NET 進行 PDF 到 HTML 轉換：將圖像儲存為外部 PNG](/pdf/english/net/conversion-export/pdf-to-html-conversion-external-png-aspose-pdf-net/)
- [使用 Aspose.PDF 將 PDF 儲存為 HTML – 快速 C# 指南](/pdf/english/net/conversion-export/save-pdf-as-html-with-aspose-pdf-quick-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}