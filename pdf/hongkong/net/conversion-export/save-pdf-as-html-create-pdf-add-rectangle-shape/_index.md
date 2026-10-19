---
category: general
date: 2026-07-14
description: 使用 Aspose.Pdf 將 PDF 另存為 HTML – 學習如何建立 PDF 文件、加入矩形形狀，並匯出為不含圖片的純淨 HTML。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save pdf as html
- how to create pdf document
- add rectangle shape pdf
language: zh-hant
lastmod: 2026-07-14
og_description: 使用 Aspose.Pdf 將 PDF 另存為 HTML。了解如何建立 PDF 文件、繪製矩形形狀 PDF，並在數分鐘內產生不含圖片的
  HTML。
og_image_alt: Screenshot of a PDF saved as HTML showing a rectangle shape
og_title: 將 PDF 儲存為 HTML – 快速指南：建立 PDF 並新增矩形形狀
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Save PDF as HTML using Aspose.Pdf – learn how to create PDF document,
    add rectangle shape PDF, and export to clean HTML without images.
  headline: Save PDF as HTML – Create PDF, add rectangle shape
  type: TechArticle
tags:
- pdf
- aspnet
- csharp
- html-export
title: 將 PDF 另存為 HTML – 建立 PDF，新增矩形形狀
url: /zh-hant/net/conversion-export/save-pdf-as-html-create-pdf-add-rectangle-shape/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將 PDF 另存為 HTML – 建立 PDF，加入矩形形狀

有沒有想過在仍然能夠於原始 PDF 上繪製圖形的同時，**將 PDF 另存為 HTML**？你並非唯一有此需求的人。在許多內部工具中，我們需要一個乾淨的 HTML 預覽，顯示包含自訂形狀的 PDF，而一般的轉換器要麼嵌入龐大的點陣圖，要麼完全去除向量資料。  

在本教學中，我們將逐步說明如何使用 Aspose.Pdf 程式化**建立 PDF 文件**、繪製**矩形形狀 PDF**、設定 Bates 編號，最後**將 PDF 另存為 HTML**且不包含點陣圖。完成後，你將擁有一個可直接執行的 C# 主控台應用程式，產生的 HTML 檔案可在任何瀏覽器開啟——不需要額外的圖像檔案。

> **專業提示：** Aspose.Pdf 支援 .NET 6+、.NET Framework 4.6+ 以及 .NET Core，因此你可以將它嵌入舊有的 Windows 服務或全新的微服務中使用。

---

## Prerequisites

- **Visual Studio 2022**（Community 或更高版）或任何相容 C# 的 IDE。  
- **Aspose.Pdf for .NET** NuGet 套件（版本 23.11 或更新）。透過套件管理員主控台安裝：

```powershell
Install-Package Aspose.Pdf
```

- 具備基本的 C# 語法概念；不需要先前的 PDF 經驗。

---

## Save PDF as HTML with Aspose.Pdf

以下提供完整、可直接複製貼上的程式碼。它遵循原始範例的每一步，同時加入註解、錯誤處理，以及一個小型輔助方法，以保持主要流程的可讀性。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

namespace PdfToHtmlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a fresh PDF document.
            Document pdfDoc = new Document();
            Page pdfPage = pdfDoc.Pages.Add();

            // 2️⃣ Draw a rectangle shape on the page.
            //    This demonstrates the "add rectangle shape pdf" requirement.
            var rectangle = new Rectangle(100, 500, 300, 700)
            {
                // Optional visual tweaks
                FillColor = Color.GetYellow(),
                Border = new Border
                {
                    Width = 2,
                    Color = Color.GetRed()
                }
            };
            pdfPage.Paragraphs.Add(rectangle);
            pdfPage.ValidateGraphicsState(); // Ensures the shape fits within page bounds

            // 3️⃣ Configure Bates numbering – useful for legal documents.
            var bates = new BatesNumbering { StartNumber = 1, Prefix = "DOC-" };
            pdfDoc.BatesNumbering = bates;

            // 4️⃣ Add a tagged element with an explicit position.
            //    Tagging is important for accessibility (PDF/UA).
            var taggedElement = new TagStructure();
            taggedElement.PositionSettings = new TagPositionSettings { X = 150, Y = 600 };
            pdfPage.TagStructure.Add(taggedElement);

            // 5️⃣ Enable detection of compromised signatures.
            pdfDoc.SecurityOptions.DetectCompromisedSignatures = true;
            bool hasCompromisedSignature = pdfDoc.SecurityOptions.HasCompromisedSignature;
            Console.WriteLine($"Compromised signature? {hasCompromisedSignature}");

            // 6️⃣ Finally, save the PDF as HTML *without* embedding raster images.
            var htmlOptions = new HtmlSaveOptions
            {
                SkipImages = true,               // Removes <img> tags for raster data
                FixedLayout = true,              // Preserves the original page layout
                ExportEmbeddedFonts = false      // Keeps the HTML lightweight
            };

            string outputPath = @"output.html";
            pdfDoc.Save(outputPath, htmlOptions);
            Console.WriteLine($"✅ PDF successfully saved as HTML at: {outputPath}");
        }
    }
}
```

### What the code does, step by step

| 步驟 | 為何重要 |
|------|----------|
| **建立 PDF 文件** | 這是基礎——若沒有 `Document` 物件就無法加入任何內容。 |
| **加入矩形形狀 PDF** | 示範向量繪圖；矩形是最簡單的形狀，但相同的 API 也支援圓形、多邊形等。 |
| **設定 Bates 編號** | 在訴訟或批次處理情境中常需用以唯一識別頁面。 |
| **標籤結構** | 提升可及性；螢幕閱讀器依賴標籤來傳達閱讀順序。 |
| **偵測受損的簽章** | 注重安全的應用程式需要知道數位簽章是否被竄改。 |
| **將 PDF 另存為 HTML** | 最終目標——產生與 PDF 版面相符且不含龐大圖像檔的乾淨 HTML。 |

> **為何設定 `SkipImages = true`？**  
> 當你轉換包含向量圖形（如本例的矩形）的 PDF 時，通常不需要點陣圖備援。將 `SkipImages` 設為 true 會移除 `<img>` 元素，避免引用 base‑64 資料，讓 HTML 檔案保持在數 KB 以內。

---

## How to create PDF document with Aspose.Pdf

如果你是 Aspose 新手，該函式庫將 PDF 視為類似 Word 文件：先加入**頁面**，再於頁面上加入**段落**、**形狀**或**註解**。`Document` 類別是入口點，每個 `Page` 都有一個名為 `Paragraphs` 的集合。任何繼承自 `TextFragmentAbsorber`、`Image`、`Rectangle` 等的物件，都可以插入該集合中。

以下是一段最小化的程式碼片段，只會建立空白 PDF——適合從頭開始時使用：

```csharp
Document emptyPdf = new Document();
Page firstPage = emptyPdf.Pages.Add();   // Adds a default‑size A4 page
emptyPdf.Save("empty.pdf");
```

你可以使用簡單的 `for` 迴圈串接額外頁面，或透過 `PageInfo` 設定頁面的屬性（如邊距、尺寸）。這種彈性使得 Aspose.Pdf 成為伺服器端 PDF 產生的首選。

---

## Add rectangle shape PDF – drawing graphics

`Rectangle` 類別位於 `Aspose.Pdf.Annotations` 命名空間。它接受四個座標：**左下 X**、**左下 Y**、**右上 X**、**右上 Y**。可將 PDF 的座標系統想像成

## 接下來你可以學什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上延伸。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [使用 Aspose.PDF 建立 PDF 文件 – 新增頁面、形狀與儲存](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [使用 Aspose.PDF 在 .NET 中將 PDF 轉換為 HTML（不儲存圖像）](/pdf/english/net/conversion-export/convert-pdf-html-net-asposepdf-no-images/)
- [使用 Aspose.PDF .NET 進行 PDF 轉 HTML 轉換：將圖像儲存為外部 PNG](/pdf/english/net/conversion-export/pdf-to-html-conversion-external-png-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}