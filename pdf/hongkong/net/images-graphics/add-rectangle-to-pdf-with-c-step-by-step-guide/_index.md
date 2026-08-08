---
category: general
date: 2026-08-04
description: 使用 C# 為 PDF 添加矩形。學習如何在 C# 中使用 Aspose.Pdf 繪製 PDF 形狀，提供清晰完整的範例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to pdf
- how to draw shape in pdf c#
language: zh-hant
lastmod: 2026-08-04
og_description: 使用 C# 為 PDF 加入矩形。本教學示範如何快速且可靠地在 PDF 中使用 C# 繪製形狀。
og_image_alt: Screenshot of a PDF page with a blue rectangle drawn by C# code
og_title: 使用 C# 為 PDF 添加矩形 – 完整程式設計指南
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  headline: Add rectangle to PDF with C# – step‑by‑step guide
  type: TechArticle
- description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  name: Add rectangle to PDF with C# – step‑by‑step guide
  steps:
  - name: '**Create a new console project**'
    text: '**Create a new console project**'
  - name: '**Add the Aspose.Pdf package**'
    text: '**Add the Aspose.Pdf package**'
  - name: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
    text: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: 使用 C# 為 PDF 加入矩形 – 步驟說明指南
url: /zh-hant/net/images-graphics/add-rectangle-to-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中向 PDF 添加矩形 – 步驟指引

如果您需要在 C# 應用程式中**向 PDF 添加矩形**，本指南將精確說明如何操作。您將看到一個完整且可執行的範例，使用 Aspose.Pdf 函式庫在 PDF C# 中繪製圖形，並了解每行程式碼的意義。

在 PDF 中繪製圖形是報表產生器、發票範本以及自訂文件品牌化的常見需求。完成本教學後，您可以插入任何矩形註解、變更其大小、顏色或位置，並在不遺失既有內容的情況下儲存修改後的文件。

**您將學習**

* 如何使用 Aspose.Pdf 載入既有 PDF。
* 如何定義矩形邊界並建立矩形圖形。
* 如何將矩形加入頁面的段落集合。
* 如何儲存更新後的 PDF 並驗證結果。
* 多頁、透明度與自訂線條樣式的變化寫法。

**先決條件**

* .NET 6.0 或更新版本（程式碼亦相容 .NET Framework 4.7+）。
* Visual Studio 2022 或任何 C# IDE。
* 以 NuGet 參考 `Aspose.Pdf`（免費試用版或授權版）。
* 名為 `input.pdf` 的輸入 PDF 檔案，放置於您可控制的資料夾中。

---

## 如何在 PDF C# 中繪製圖形 – 設定專案

1. **建立新的主控台專案**  

   ```bash
   dotnet new console -n PdfRectangleDemo
   cd PdfRectangleDemo
   ```

2. **加入 Aspose.Pdf 套件**  

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. **將 `input.pdf`** 放置於專案目錄（或任何稍後會參考的資料夾）。

專案現在已可編譯能**向 PDF 添加矩形**的程式碼。

---

## Step 1: Load the PDF document

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // Load the existing PDF file.
        Document pdfDoc = new Document("input.pdf");
```

*`Document` 類別會解析檔案並公開 `Pages` 集合。載入是任何繪圖操作之前的第一步必須執行的動作。*

---

## Step 2: Choose the target page

```csharp
        // Get the first page (pages are 1‑based).
        Page firstPage = pdfDoc.Pages[1];
```

*如果您需要將矩形加入其他頁面，請將索引替換為目標頁碼。當索引超出範圍時，函式庫會拋出例外，因此請確保 PDF 內有足夠的頁數。*

---

## Step 3: Define rectangle bounds

```csharp
        // Define the rectangle's position and size (points).
        // (left, bottom, right, top) – origin is bottom‑left.
        Rectangle bounds = new Rectangle(50, 700, 300, 800);
```

*座標系統使用點 (1 pt = 1/72 英吋)。本範例在頁面上方建立一個寬 250 pt、高 100 pt 的矩形。請依需求調整數值以符合版面配置。*

---

## Step 4: Create the rectangle shape

```csharp
        // Create a rectangle shape with the defined bounds.
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            // Optional styling – a semi‑transparent blue fill.
            FillColor = Color.FromRgb(0, 120, 215),
            FillOpacity = 0.4,

            // Optional border – 2 pt thick, dark gray.
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };
```

*`Rectangle` 類別繼承自 `GraphicalObject`。設定 `FillColor` 與 `Border` 為可選項目，但它示範了在**如何在 PDF C# 中繪製圖形**時，如何控制外觀超越單純輪廓。*

---

## Step 5: Add the rectangle to the page

```csharp
        // Add the rectangle shape to the page's paragraph collection.
        firstPage.Paragraphs.Add(rectangleShape);
```

*段落是任何可繪製物件的容器。將圖形插入 `Paragraphs` 後，Aspose.Pdf 會在文件儲存時將其渲染。*

---

## Step 6: Save the modified PDF

```csharp
        // Save the updated PDF to a new file.
        pdfDoc.Save("output.pdf");

        // Inform the user.
        Console.WriteLine("Rectangle added and saved to output.pdf");
    }
}
```

*儲存會產生新檔案，讓原始的 `input.pdf` 保持不變。您也可以傳入相同路徑覆寫來源檔案，但保留備份是最佳實踐。*

---

## Full source code (runnable)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color struct

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document
        Document pdfDoc = new Document("input.pdf");

        // Step 2: Get the first page (pages are 1‑based)
        Page firstPage = pdfDoc.Pages[1];

        // Step 3: Define rectangle bounds (left, bottom, right, top)
        Rectangle bounds = new Rectangle(50, 700, 300, 800);

        // Step 4: Create a rectangle shape with optional styling
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            FillColor = Color.FromArgb(102, 0, 120, 215), // 40 % opacity blue
            FillOpacity = 0.4,
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };

        // Step 5: Add the rectangle shape to the page
        firstPage.Paragraphs.Add(rectangleShape);

        // Step 6: Save the modified PDF
        pdfDoc.Save("output.pdf");

        Console.WriteLine("Rectangle added to PDF successfully.");
    }
}
```

**預期輸出** – 在任何 PDF 檢視器中開啟 `output.pdf`。您應該會看到第一頁右上角附近有一個藍色填滿的矩形，外框為深灰色線條。

---

## How to draw shape in PDF C# on multiple pages

如果您需要在每一頁**向 PDF 添加矩形**，可遍歷 `Pages` 集合：

```csharp
foreach (Page page in pdfDoc.Pages)
{
    Rectangle rect = new Rectangle(50, 700, 300, 800);
    Rectangle shape = new Rectangle(rect)
    {
        FillColor = Color.FromArgb(80, 255, 0, 0), // semi‑transparent red
        Border = new Border { Width = 1, Color = Color.Black }
    };
    page.Paragraphs.Add(shape);
}
```

*此模式在每頁使用相同的邊界。若需不同位置，請依頁面自行調整座標。*

---

## Common pitfalls and best‑practice tips

| 問題 | 為何會發生 | 解決方式 |
|------|------------|----------|
| 矩形出現在頁面外 | 座標是以左下角為原點測量；使用自上而下的座標系統會造成混淆。 | 記得 Y 軸向上增長。使用符合頁面尺寸 (`page.PageInfo.Width`, `page.PageInfo.Height`) 的數值。 |
| 圖形不可見 | `FillOpacity` 設為 `0` 或邊框寬度設為 `0`。 | 確保 `FillOpacity` 大於 `0`，且 `Border.Width` 至少為 `0.5`。 |
| 儲存拋出 `AccessDeniedException` | 輸出檔案正被其他程式開啟。 | 執行程式前關閉所有檢視器，或改存至其他路徑。 |
| 矩形覆蓋既有內容 | 未設定圖層順序。 | 如需控制層級，可使用 `ZIndex` 屬性（數值越高越在上層）。 |

---

## Extending the rectangle – gradients, rotation, and transparency

Aspose.Pdf 支援進階圖形。若要建立帶線性漸層的旋轉矩形：

```csharp
Rectangle gradientRect = new Rectangle(bounds)
{
    // Gradient fill from left (blue) to right (green)
    FillColor = Color.Blue,
    FillColor2 = Color.Green,
    FillMode = FillMode.LinearGradient,
    // Rotate 45 degrees around the rectangle's center
    Rotation = 45
};
firstPage.Paragraphs.Add(gradientRect);
```

*相同的程式碼範例示範了**如何在 PDF C# 中繪製圖形**以獲得更豐富的視覺效果。*

---

## Verify the result programmatically

您可以透過檢查頁面的段落數量來確認矩形是否已加入：

```csharp
int shapeCount = firstPage.Paragraphs.Count;
Console.WriteLine($"Page 1 now contains {shapeCount} paragraph objects.");
```

若插入後段落數增加一筆，表示操作成功。

---

## Conclusion

您現在已掌握使用 C# **向 PDF 添加矩形** 的方法。本教學涵蓋了載入文件、定義邊界、建立矩形圖形、插入頁面以及儲存結果的全流程。您亦了解了多頁處理、避免常見錯誤以及套用進階樣式的技巧。

接下來，可探索相關主題，例如**如何在 PDF C# 中繪製圖形**以製作圓形、多邊形或自由形狀路徑，並學習將圖形與文字、圖片結合，打造功能完整的 PDF 報表。

Happy coding!

## What Should You Learn Next?

以下教學與本指南所示技巧密切相關，能進一步擴充您的應用。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索替代實作方式。

- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds Guide](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)
- [How to Add an Image Stamp to a PDF Using Aspose.PDF for .NET: A Comprehensive Guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [How to Add a Rotating Image Watermark to PDFs Using Aspose.PDF for .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}