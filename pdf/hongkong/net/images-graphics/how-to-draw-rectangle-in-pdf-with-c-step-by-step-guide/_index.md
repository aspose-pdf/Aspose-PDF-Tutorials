---
category: general
date: 2026-03-27
description: 學習如何使用 Aspose.Pdf for C# 在 PDF 中繪製矩形。將矩形加入 PDF、將形狀加入 PDF，並以清晰的程式碼範例在
  PDF 上繪製形狀。
draft: false
keywords:
- how to draw rectangle
- add rectangle to pdf
- add shape to pdf
- draw shape on pdf
- draw rectangle in pdf
language: zh-hant
og_description: 掌握如何使用 Aspose.Pdf 在 PDF 中繪製矩形。本教學一步步示範如何在 PDF 中加入矩形、加入形狀，以及繪製形狀。
og_title: 如何使用 C# 在 PDF 中繪製矩形 – 完整指南
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: 如何使用 C# 在 PDF 中繪製矩形 – 逐步指南
url: /zh-hant/net/images-graphics/how-to-draw-rectangle-in-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 PDF 中使用 C# 繪製矩形 – 步驟指南

有沒有想過 **how to draw rectangle** 在 PDF 中，而不必與低層 PDF 語法糾纏？你並非唯一。許多開發者在需要在產生的文件中視覺化邊框、突出區域或簡單裝飾元素時會卡住。好消息是？使用 Aspose.Pdf for .NET，這個過程輕而易舉。

在本教學中，我們將逐步說明如何 **add rectangle to PDF**、**add shape to PDF**，以及最終使用乾淨、慣用的 C# **draw rectangle in PDF**。完成後，你將擁有一個可執行的程式，產生包含清晰矩形的 PDF 檔案——不需要任何外部工具。

## 前置條件

- .NET 6.0 或更新版本（程式碼同樣適用於 .NET Core 與 .NET Framework）
- Aspose.Pdf for .NET NuGet 套件（`Install-Package Aspose.Pdf`）
- 基本的 C# 開發環境（Visual Studio、VS Code、Rider 等）

不需要其他函式庫；其餘全部由 Aspose.Pdf 自行處理。

## 步驟 1：設定專案並匯入命名空間

首先，建立一個新的主控台應用程式，並引用 Aspose.Pdf 命名空間。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the rest of the code here.
        }
    }
}
```

**Why this matters:** 匯入 `Aspose.Pdf.Drawing` 後，即可取得我們將用來 **draw shape on PDF** 的 `Rectangle` 形狀類別。保持入口點整潔，能讓後續步驟更易於理解。

## 步驟 2：建立新的 PDF 文件與頁面

沒有頁面的 PDF 是沒有意義的，因此我們先建立文件物件，並新增一個頁面。

```csharp
// Step 2: Initialize a new PDF document
Document pdfDoc = new Document();

// Add a blank page to the document (size defaults to A4)
Page page = pdfDoc.Pages.Add();
```

**Explanation:** `Document` 類別代表整個檔案，而 `Pages.Add()` 會回傳一個全新的 `Page` 物件，之後我們會 **add rectangle to PDF**。預設的 A4 大小適用於大多數情況，若需要自訂畫布，可自行傳入寬度/高度。

## 步驟 3：定義矩形形狀

現在進入 **how to draw rectangle** 的核心——定義位置與尺寸。

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
// Coordinates are measured from the lower‑left corner of the page.
var rectangleShape = new Rectangle(100, 500, 300, 200)
{
    // Optional: set line color and fill color
    BorderColor = Color.Black,
    BorderWidth = 2,
    FillColor = Color.LightGray
};
```

**Why we set these properties:**  
- `BorderColor` 與 `BorderWidth` 控制輪廓，使矩形可見。  
- `FillColor` 為其提供淡淡的背景，適合用來突顯區域。  
- 建構子 `(x, y, width, height)` 讓你 **draw rectangle in PDF** 時能精確定位。

## 步驟 4：將矩形加入頁面

形狀準備好後，我們現在透過將它附加到頁面的 `Annotations` 集合來 **add shape to PDF**。Aspose.Pdf 會自動驗證邊界，無需擔心溢位問題。

```csharp
// Step 4: Add the rectangle shape to the page
page.Annotations.Add(rectangleShape);
```

**What happens under the hood:** `Annotations` 集合會將矩形視為向量圖形。當 PDF 被渲染時，函式庫會將我們的座標轉換成 PDF 內容串流。

## 步驟 5：儲存文件

最後，將 PDF 寫入磁碟，讓你可以在任何檢視器中開啟。

```csharp
// Step 5: Save the PDF file
string outputPath = "RectangleDemo.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

**Result:** 開啟 `RectangleDemo.pdf` 後會看到一個淡灰色矩形，黑色邊框位於頁面左側 100 pts、底部 500 pts 的位置。這就是使用 C# **how to draw rectangle** 的完整解決方案。

## 完整範例

將所有片段組合起來，以下是完整、可直接執行的程式碼：

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize a new PDF document
            Document pdfDoc = new Document();

            // Add a blank page (A4 by default)
            Page page = pdfDoc.Pages.Add();

            // Define a rectangle shape (x, y, width, height)
            var rectangleShape = new Rectangle(100, 500, 300, 200)
            {
                BorderColor = Color.Black,
                BorderWidth = 2,
                FillColor = Color.LightGray
            };

            // Add the rectangle to the page
            page.Annotations.Add(rectangleShape);

            // Save the document
            string outputPath = "RectangleDemo.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved to {outputPath}");
        }
    }
}
```

**Expected output:** 產生一個名為 `RectangleDemo.pdf` 的檔案，內含單一頁面，中央有一個淡灰色、黑色邊框的矩形。你可以使用 Adobe Reader、Chrome 或任何 PDF 檢視器開啟。

## 常見變化與邊緣情況

### 1. 繪製多個矩形

如果需要 **add rectangle to PDF** 超過一次，只要再建立額外的 `Rectangle` 物件，並將每個物件加入 `page.Annotations`。對座標集合進行迴圈即可輕鬆完成。

```csharp
foreach (var rectInfo in rectangles)
{
    var rect = new Rectangle(rectInfo.X, rectInfo.Y, rectInfo.Width, rectInfo.Height)
    {
        BorderColor = Color.Blue,
        BorderWidth = 1,
        FillColor = Color.Transparent
    };
    page.Annotations.Add(rect);
}
```

### 2. 使用不同單位

Aspose.Pdf 以點為單位（1 pt = 1/72 inch）。若偏好使用公釐，請先自行轉換：

```csharp
double mmToPt = 72.0 / 25.4;
float x = (float)(20 * mmToPt); // 20 mm from left
float y = (float)(150 * mmToPt);
```

### 3. 將矩形作為表單欄位加入

當需要互動式矩形（例如可點擊區域）時，請改用 `LinkAnnotation` 取代普通的 `Rectangle`。程式碼類似，只是會加入 URL 或 JavaScript 動作。

### 4. 相容性考量

Aspose.Pdf 版本 23.9（2026 年初發布）完整支援上述 API。較舊版本可能需要使用 `page.AddAnnotation(rectangleShape)` 取代 `page.Annotations.Add`。若遇到編譯錯誤，請務必檢查發行說明。

## 專業技巧與陷阱

- **Pro tip:** 若只需要輪廓，將 `FillColor = Color.Transparent`，可稍微減少檔案大小。  
- **Watch out for:** 使用超出頁面尺寸的座標。Aspose.Pdf 會靜默裁切形狀，除錯時可能會感到困惑。  
- **Performance note:** 加入數千個矩形是可行的，但若產生大型報表，建議將形狀批次寫入單一 `Graphics` 物件，以降低開銷。

## 視覺參考

以下是一張快速截圖，展示產生的 PDF（矩形以淡灰色標示）。alt 文字已包含主要關鍵字以利 SEO。

![how to draw rectangle in PDF example](https://example.com/images/rectangle-demo.png "how to draw rectangle in PDF example")

## 結論

我們已說明如何使用 Aspose.Pdf for C# **how to draw rectangle** 在 PDF 中。透過建立 `Document`、加入 `Page`、定義 `Rectangle` 形狀，最後 **add shape to PDF**，即可僅用幾行程式碼產生向量圖形。無論是 **add rectangle to pdf** 用於突顯、版面除錯或 UI 疊加，此方法都具備良好擴充性。

接下來，你可以探索 **draw shape on pdf** 超出矩形的應用——例如圓形、多段線，甚至自訂 SVG 路徑。亦可深入文字渲染、影像插入與 PDF 表單操作，打造完整報表。Aspose.Pdf 函式庫提供豐富 API，掌握本篇基礎後，即可盡情實驗。

祝程式開發順利，願你的 PDF 永遠呈現出你所想像的樣子！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}