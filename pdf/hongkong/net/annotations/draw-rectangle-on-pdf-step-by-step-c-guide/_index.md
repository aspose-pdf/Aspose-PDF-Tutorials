---
category: general
date: 2026-08-14
description: 使用 C# 快速在 PDF 上繪製矩形。了解如何定義矩形尺寸，並只需幾行程式碼即可在 PDF 頁面上加入形狀。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- draw rectangle on pdf
- how to define rectangle dimensions
language: zh-hant
lastmod: 2026-08-14
og_description: 在 PDF 上使用 C# 迅速繪製矩形。本指南說明如何設定矩形尺寸、加入形狀，並驗證頁面邊界，以確保 PDF 圖形的可靠性。
og_image_alt: Screenshot of a PDF page showing a black rectangle drawn with C# code
og_title: 在 PDF 上繪製矩形 – 完整 C# 教學
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: draw rectangle on pdf quickly using C#. Learn how to define rectangle
    dimensions and add shapes to a PDF page in just a few lines.
  headline: draw rectangle on pdf – step‑by‑step C# guide
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
- RectangleShape
- Graphics
title: 在 PDF 上繪製矩形 – C# 步驟指南
url: /zh-hant/net/annotations/draw-rectangle-on-pdf-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 上繪製矩形 – 完整 C# 教學

如果您需要 **在 PDF 上繪製矩形**（draw rectangle on pdf）使用 C#，本指南將為您展示一個簡潔、可直接投入生產環境的解決方案。您將會看到 **如何定義矩形尺寸**、驗證形狀是否符合頁面，並透過單一方法呼叫將其加入頁面。

本教學涵蓋從建立 PDF 文件到渲染矩形的全部步驟，您只要把程式碼複製貼上到自己的專案，即可立即看到結果。無需額外文件說明——只要跟隨以下步驟即可。

## 前置條件

開始之前，請確保您已具備：

* .NET 6.0 或更新版本（此程式碼亦相容 .NET Framework 4.7+）
* **Aspose.PDF for .NET** NuGet 套件（`Install-Package Aspose.PDF`）
* 基本的 C# 語法概念
* 如 Visual Studio 或 VS Code 等開發環境

> **專業提示：** 使用 Aspose.PDF 的免費評估授權進行快速實驗；雖會加上小水印，但可測試所有功能。

## 如何使用 C# 在 PDF 上繪製矩形

此任務的核心是建立 `RectangleShape`、設定尺寸與筆劃，並將其附加至 `Page`。以下 H2 標題即包含主要關鍵字，以符合 SEO 需求。

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        Document pdfDoc = new Document();

        // 2️⃣ Add a blank page (default size: A4)
        Page page = pdfDoc.Pages.Add();

        // 3️⃣ Define the rectangle bounds (x, y, width, height)
        //    This demonstrates how to define rectangle dimensions.
        Rectangle rectBounds = new Rectangle(0, 0, 500, 700);

        // 4️⃣ Create the rectangle shape and set its stroke color
        RectangleShape rectangleShape = new RectangleShape(rectBounds)
        {
            StrokeColor = Color.Black   // black outline
        };

        // 5️⃣ Verify that the shape fits within the page boundaries
        page.CheckShapeBoundary(rectangleShape);

        // 6️⃣ Add the shape to the page
        page.Add(rectangleShape);

        // 7️⃣ Save the PDF to disk
        string outPath = "RectangleDemo.pdf";
        pdfDoc.Save(outPath);
        Console.WriteLine($"PDF saved to {outPath}");
    }
}
```

### 各步驟說明

| 步驟 | 為何重要 |
|------|----------|
| **1️⃣ 建立新的 PDF 文件** | 初始化容器，以容納頁面與圖形。 |
| **2️⃣ 新增空白頁面** | 必須先取得 `Page` 物件，因為形狀是附加在頁面上，而非直接附加在文件上。 |
| **3️⃣ 定義矩形邊界** | 這裡說明 **如何定義矩形尺寸**。`Rectangle` 建構子接受 `x`、`y`、`width`、`height`（單位為點，1 pt = 1/72 in）。 |
| **4️⃣ 建立矩形形狀** | `RectangleShape` 為 Aspose 用來繪製矩形的類別。設定 `StrokeColor` 以定義輪廓；亦可設定 `FillColor` 產生實心填色。 |
| **5️⃣ 驗證頁面邊界** | `CheckShapeBoundary` 會在矩形超出頁面尺寸時拋出例外，避免產生格式錯誤的 PDF。 |
| **6️⃣ 將形狀加入頁面** | 形狀會成為頁面內容串流的一部份。 |
| **7️⃣ 儲存 PDF** | 將文件寫入檔案，之後可使用任何 PDF 閱讀器開啟。 |

產生的 `RectangleDemo.pdf` 會在頁面左上角呈現一個寬 500 pt、高 700 pt 的黑色矩形。

![在 PDF 上繪製矩形範例](https://example.com/rectangle-demo.png "在 PDF 上繪製矩形範例")

*圖片替代文字：在 PDF 上繪製矩形範例，顯示 PDF 頁面左上角的黑色矩形。*

## 如何為不同頁面尺寸定義矩形尺寸

上方程式碼使用固定值（`500 x 700`）。在實務應用中，矩形常需要依頁面的寬高自動調整。

```csharp
// Get page dimensions (in points)
float pageWidth = page.PageInfo.Width;
float pageHeight = page.PageInfo.Height;

// Define a rectangle that occupies 80% of the page width and 50% of the height
float rectWidth  = pageWidth * 0.8f;
float rectHeight = pageHeight * 0.5f;

// Center the rectangle on the page
float rectX = (pageWidth - rectWidth) / 2;
float rectY = (pageHeight - rectHeight) / 2;

Rectangle dynamicRect = new Rectangle(rectX, rectY, rectWidth, rectHeight);
RectangleShape dynamicShape = new RectangleShape(dynamicRect)
{
    StrokeColor = Color.DarkBlue,
    FillColor   = Color.LightGray   // optional fill
};

page.CheckShapeBoundary(dynamicShape);
page.Add(dynamicShape);
```

**重點說明：**

* 使用 `page.PageInfo.Width` 與 `Height` 取得實際頁面尺寸。
* 乘上比例因子（例如 `0.8f`）即可將尺寸表達為頁面寬高的百分比。
* 透過將頁面尺寸減去矩形尺寸後除以二，即可將矩形置中。

## 常見陷阱與避免方式

| 陷阱 | 為何會發生 | 解決方法 |
|------|------------|----------|
| 矩形超出頁面 | 使用硬編碼尺寸大於頁面大小。 | 在加入形狀前 **先呼叫** `page.CheckShapeBoundary`；若拋出例外，調整尺寸。 |
| 筆劃不可見 | `StrokeColor` 保持預設 (`Color.Empty`)。 | 明確設定 `StrokeColor`（例如 `Color.Black`）。 |
| 矩形出現在螢幕外 | PDF 座標系統的原點在左下角，使用螢幕式左上角座標會導致翻轉。 | 記得原點 `(0,0)` 位於左下角，需調整 `y` 座標或使用 `pageHeight - desiredY`。 |
| 線條粗細異常 | 預設線寬過細，列印時不易辨識。 | 設定 `rectangleShape.LineWidth = 2;` 以增粗線條。 |

## 延伸範例

一旦您能 **在 PDF 上繪製矩形**，即可輕鬆加入其他形狀：

* **EllipseShape** – 繪製圓形或橢圓。
* **PolygonShape** – 繪製自訂多邊形。
* **TextFragment** – 為矩形加上文字標籤。

所有形狀的工作流程相同：定義邊界、設定外觀、驗證邊界，最後加入頁面。

## 完整可執行程式

以下為結合基礎矩形與動態尺寸範例的完整程式碼。將其貼到新的 Console 專案，還原 `Aspose.PDF` NuGet 套件後即可執行。

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class RectangleDemo
{
    static void Main()
    {
        // Create document and page
        Document doc = new Document();
        Page page = doc.Pages.Add();

        // ==== Fixed‑size rectangle (basic example) ====
        Rectangle fixedRect = new Rectangle(0, 0, 500, 700);
        RectangleShape fixedShape = new RectangleShape(fixedRect)
        {
            StrokeColor = Color.Black,
            LineWidth   = 1
        };
        page.CheckShapeBoundary(fixedShape);
        page.Add(fixedShape);

        // ==== Dynamic rectangle that adapts to page size ====
        float pageW = page.PageInfo.Width;
        float pageH = page.PageInfo.Height;

        float dynWidth  = pageW * 0.6f;
        float dynHeight = pageH * 0.3f;
        float dynX      = (pageW - dynWidth) / 2;
        float dynY      = (pageH - dynHeight) / 2;

        Rectangle dynamicRect = new Rectangle(dynX, dynY, dynWidth, dynHeight);
        RectangleShape dynamicShape = new RectangleShape(dynamicRect)
        {
            StrokeColor = Color.DarkBlue,
            FillColor   = Color.LightYellow,
            LineWidth   = 2
        };
        page.CheckShapeBoundary(dynamicShape);
        page.Add(dynamicShape);

        // Save PDF
        string outFile = "CombinedRectangles.pdf";
        doc.Save(outFile);
        Console.WriteLine($"PDF created: {outFile}");
    }
}
```

**預期結果：**  
開啟 `CombinedRectangles.pdf` 後，您會看到一個位於左下角的黑色矩形，以及一個置中、深藍色外框、淡黃色填色的矩形。兩個矩形皆遵守頁面邊距。

## 結論

現在您已掌握如何使用 C# **在 PDF 上繪製矩形**，以及 **如何定義矩形尺寸**，無論是固定尺寸或響應式布局。此方法利用 Aspose.PDF 的 `RectangleShape`、邊界檢查與簡單算術，即可適應任何頁面大小。

接下來，您可以探索：

* 加入 **填色** 與 **線條樣式**（虛線、點線）— 次要關鍵字：如何以樣式定義矩形尺寸。
* 將多個形狀合併於同一 `Page`，製作圖表或表單。
* 將 PDF 輸出為串流，以供 Web API 使用，而非儲存至磁碟。

多嘗試不同的尺寸、顏色與位置，徹底掌握 .NET 應用程式中的 PDF 圖形繪製。祝您開發順利！

## 接下來該學什麼？

以下教學與本篇內容密切相關，能進一步延伸您所學的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您熟悉更多 API 功能，並探索替代實作方式。

- [如何使用 Aspose.PDF for .NET 自訂 PDF：設定頁面邊距與繪製線條](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [如何在 PDF 中加入頁面印章（Watermark）使用 Aspose.PDF for .NET：完整指南](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [如何在 PDF 中加入頁碼印章（Page Number Stamp）使用 Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}