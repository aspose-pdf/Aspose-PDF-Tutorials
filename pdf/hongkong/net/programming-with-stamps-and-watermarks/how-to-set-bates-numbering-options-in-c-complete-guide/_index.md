---
category: general
date: 2026-08-14
description: 如何在 C# 中使用 GroupDocs 設定 Bates 編號選項。請依照此步驟教學，在將 Word 轉換為 PDF 時加入自訂前綴與起始編號。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set bates numbering options
- Bates numbering C#
- GroupDocs API
- document conversion C#
- AddBatesNumbering method
- C# PDF generation
language: zh-hant
lastmod: 2026-08-14
og_description: 如何在 C# 中快速設定 Bates 編號選項。本指南示範在將 Word 轉換為 PDF 時，如何加入自訂前綴與起始編號。
og_image_alt: Screenshot of C# code applying Bates numbering to a PDF
og_title: 如何在 C# 中設定 Bates 編號選項 – 步驟教學
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  headline: How to set bates numbering options in C# – complete guide
  type: TechArticle
- description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  name: How to set bates numbering options in C# – complete guide
  steps:
  - name: '`Document` – loads the source file.'
    text: '`Document` – loads the source file.'
  - name: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
    text: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
  - name: '`AddBatesNumbering` – the method that injects the numbering into each page.'
    text: '`AddBatesNumbering` – the method that injects the numbering into each page.'
  type: HowTo
tags:
- Bates numbering
- C#
- .NET
- GroupDocs
- PDF conversion
title: 如何在 C# 中設定 Bates 編號選項 – 完整指南
url: /zh-hant/net/programming-with-stamps-and-watermarks/how-to-set-bates-numbering-options-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中設定 Bates 編號選項 – 完整指南

如果您需要 **設定 Bates 編號選項**，本指南將逐步說明確切步驟。您將學習如何設定起始編號、加入前綴，並在使用 GroupDocs API 將 Word 文件轉換為 PDF 時套用編號。

文件處理常常需要在每一頁加上唯一識別碼，以符合法律或歸檔需求。完成本教學後，您將擁有一段可重複使用的程式碼片段，能直接放入任何 .NET 專案，無論是建置訴訟支援工具或自動化報告產生器。無需額外工具——只要使用 GroupDocs.Conversion 套件與少量 C# 程式碼即可。

## 您需要的環境

* .NET 6.0 SDK 或更新版本已安裝  
* Visual Studio 2022（或任何支援 .NET 的 IDE）  
* 有效的 GroupDocs.Conversion 授權（免費試用版可用於測試）  
* 一個您想要編號的範例 Word 文件（`input.docx`）  

這些前置條件可確保程式碼在不需額外設定的情況下執行。

## 設定 Bates 編號選項概覽

**設定 Bates 編號選項** 的核心在於三個物件：

1. `Document` – 載入來源檔案。  
2. `BatesNumberingOptions` – 保存起始編號、前綴及其他格式設定。  
3. `AddBatesNumbering` – 將編號注入每一頁的方法。

了解每個部件的作用，有助於您將解決方案套用到更複雜的情境，例如自訂字型或多語系編號。

## 步驟 1：安裝 GroupDocs.Conversion NuGet 套件

在解決方案資料夾的終端機中執行：

```bash
dotnet add package GroupDocs.Conversion
```

**GroupDocs API** 提供了稍後教學中會使用的 `Document` 類別與 `AddBatesNumbering` 擴充方法。

## 步驟 2：載入來源文件

```csharp
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;

// Step 2: Load the source Word document
Document document = new Document(@"C:\Docs\input.docx");
```

*為什麼需要這一步？*  
載入檔案會在記憶體中建立可供轉換引擎操作的表示。沒有 `Document` 實例，就無法套用 Bates 編號或其他轉換。

## 步驟 3：建立 Bates 編號選項

```csharp
// Step 3: Configure Bates numbering
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // The first page will be numbered 1000
    StartNumber = 1000,
    // Each page will be prefixed with "CASE-"
    Prefix = "CASE-",
    // Optional: set the number format (e.g., 4 digits)
    NumberFormat = "#0000",
    // Optional: choose where the number appears (header/footer)
    Position = BatesNumberingPosition.FooterRight
};
```

*為什麼需要這一步？*  
`BatesNumberingOptions` 包含了在 **設定 Bates 編號選項** 時可能需要的所有設定。調整 `StartNumber` 與 `Prefix` 可讓輸出與您的案件管理系統保持一致。`Position` 屬性控制視覺位置，這往往是合規需求。

## 步驟 4：將 Bates 編號套用至文件

```csharp
// Step 4: Apply the numbering to every page
document.AddBatesNumbering(batesOptions);
```

`AddBatesNumbering` 方法會遍歷已載入的 `Document` 每一頁，插入先前設定好的字串。因為此方法作用於記憶體表示，您可以在儲存前串接其他處理步驟（例如加入浮水印）。

## 步驟 5：將結果轉換並儲存為 PDF

```csharp
// Step 5: Define PDF conversion options (optional)
PdfConvertOptions pdfOptions = new PdfConvertOptions
{
    // Preserve original layout
    EmbedStandardFonts = true
};

// Save the numbered document as PDF
document.Save(@"C:\Docs\output.pdf", pdfOptions);
```

*為什麼需要這一步？*  
PDF 是法律文件常見的最終格式。`PdfConvertOptions` 物件允許您微調輸出，但對於基本編號而言並非必須。`Save` 呼叫會將完整編號的 PDF 寫入磁碟。

## 完整、可執行的範例

將所有步驟整合起來，以下是一個自包含的主控台應用程式，您可以直接編譯執行：

```csharp
using System;
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;
using GroupDocs.Conversion.Options.Convert.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the source Word document
            Document document = new Document(@"C:\Docs\input.docx");

            // Configure Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1000,
                Prefix = "CASE-",
                NumberFormat = "#0000",
                Position = BatesNumberingPosition.FooterRight
            };

            // Apply numbering to each page
            document.AddBatesNumbering(batesOptions);

            // Optional: set PDF conversion preferences
            PdfConvertOptions pdfOptions = new PdfConvertOptions
            {
                EmbedStandardFonts = true
            };

            // Save the numbered PDF
            document.Save(@"C:\Docs\output.pdf", pdfOptions);

            Console.WriteLine("Bates numbering applied successfully. Output saved to output.pdf");
        }
    }
}
```

**預期輸出**

執行程式後會產生 `output.pdf`，每一頁皆顯示類似 `CASE-1000`、`CASE-1001` 等標籤，位於右側頁腳。使用任何 PDF 閱讀器開啟即可驗證編號是否正確顯示。

## 常見問題與最佳實踐

| 問題 | 發生原因 | 避免方法 |
|------|----------|----------|
| **相對路徑導致 `FileNotFoundException`** | Console 應用程式的工作目錄可能與 Visual Studio 不同。 | 使用絕對路徑或 `Path.Combine(AppContext.BaseDirectory, "input.docx")`。 |
| **編號與現有頁腳重疊** | 如果來源文件在選定的頁腳區域已有內容，新編號可能會被隱藏。 | 選擇其他 `Position`（例如 `HeaderLeft`）或調整來源範本。 |
| **大型文件處理緩慢** | Bates 編號會遍歷每一頁，隨著檔案大小記憶體使用量會增加。 | 如果超過 500 頁，可使用 `Document.Split` 將文件分塊處理。 |
| **授權過期** | GroupDocs 的免費試用版在 30 天後會過期，導致在呼叫 `AddBatesNumbering` 時拋出例外。 | 在載入文件之前套用有效的授權金鑰：`License license = new License(); license.SetLicense("license.lic");`。 |

**小技巧：** 如果您需要依案件使用不同的編號格式（例如 `2023-CASE-001`），可在建立 `BatesNumberingOptions` 前動態組合前綴。

## 擴充解決方案

相同的 **Bates 編號 C#** 方法同樣適用於 `.txt`、`.html` 或甚至影像等其他來源格式。只要在建立 `Document` 物件時更改檔案副檔名，轉換引擎即可自行處理其餘工作。

您也可以將 **document conversion C#** 與 OCR 結合，處理掃描版 PDF：

```csharp
// Example: add OCR before numbering (requires GroupDocs.Viewer)
using GroupDocs.Viewer;
using GroupDocs.Viewer.Options;

Document scannedPdf = new Document(@"C:\Docs\scanned.pdf");
var viewer = new Viewer(scannedPdf);
var viewOptions = new HtmlViewOptions();
viewer.View(viewOptions); // OCR step
// Then apply Bates numbering as shown earlier
```

## 結論

現在您已掌握 **如何在 C# 中設定 Bates 編號選項** 的完整流程：建立 `BatesNumberingOptions` 物件、使用 `AddBatesNumbering` 套用，最後儲存為 PDF，即可自動產出符合法律規範、具唯一識別碼的文件。

接下來，您可以探索 **C# PDF 產生**、**document conversion C#**，或進階的 **GroupDocs API** 功能，如浮水印與數位簽章。試著變換前綴、位置與編號格式，以符合您的工作流程。

祝編程愉快！

## 接下來該學什麼？

以下教學與本指南緊密相關，能在您已掌握的技巧上再度深化。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您熟悉更多 API 功能，或在專案中嘗試不同的實作方式。

- [在 C# 中加入 Bates 編號 PDF – 完整指南](/pdf/english/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/)
- [如何在 PDF 中使用 Aspose.PDF for .NET 添加與自訂頁碼 | 文件操作指南](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [如何在 PDF 中使用 Aspose.PDF for .NET 添加文字印章頁腳：逐步指南](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}