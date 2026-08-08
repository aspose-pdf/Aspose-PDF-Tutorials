---
category: general
date: 2026-04-10
description: 快速使用 C# 建立 PDF 文件。學習如何新增空白頁、繪製矩形、加入矩形形狀，並以清晰的程式碼將矩形加入 PDF。
draft: false
keywords:
- create pdf document c#
- add blank page pdf
- draw rectangle pdf
- add rectangle shape
- add rectangle to pdf
language: zh-hant
og_description: 在數分鐘內使用 C# 建立 PDF 文件。本指南示範如何新增空白頁 PDF、繪製矩形 PDF，以及以簡易程式碼加入矩形形狀。
og_title: 建立 PDF 文件 C# – 完整教學
tags:
- C#
- PDF
- Aspose.PDF
- Document Generation
title: C# 建立 PDF 文件 – 步驟指南：新增空白頁並繪製矩形
url: /zh-hant/net/document-creation/create-pdf-document-c-step-by-step-guide-to-add-a-blank-page/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 PDF 文件 C# – 完整教學

是否曾經需要 **create PDF document C#** 來實作報告功能，但不知從何開始？你並不孤單。在許多專案中，第一個障礙就是取得一個乾淨的空白頁 PDF，然後繪製簡單的圖形，例如矩形。  

在本教學中，我們將立即解決此問題：您將看到如何新增空白頁 PDF、繪製矩形 PDF，最後將矩形形狀加入檔案——全部只需幾行 C# 程式碼。完成後，您將擁有一個可直接開啟的 `shapes.pdf`，可於任何檢視器中查看。

## 您將學習到

- 如何使用 Aspose.PDF for .NET 初始化 PDF 文件。  
- 執行 **add blank page pdf** 並在其中定位矩形的完整步驟。  
- `Rectangle` 類別為何是繪製形狀的正確選擇。  
- 常見的陷阱，例如頁面尺寸不匹配，以及如何避免。  

不需要外部工具，也不需要魔法——只要純粹的 C# 程式碼，您可以直接複製貼上到 Console 應用程式中。

## 前置條件

- .NET 6.0 或更新版本（此程式碼亦可於 .NET Framework 4.6+ 執行）。  
- **Aspose.PDF for .NET** NuGet 套件（`Install-Package Aspose.PDF`）。  
- 具備基本的 C# 語法概念（變數、`using` 陳述式等）。  

> **專業提示：** 若您使用 Visual Studio，NuGet 套件管理員可讓安裝 Aspose.PDF 只需一次點擊。

## 步驟 1：初始化 PDF 文件

建立 PDF 需要先建立 `Document` 物件。可將其視為畫布，之後會放入所有頁面、圖像或形狀。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Initialise a new PDF document – this is the core of create pdf document c#
var pdfDocument = new Document();
```

`Document` 類別讓您存取 `Pages` 集合，我們稍後會在此 **add blank page pdf**。

## 步驟 2：將空白頁加入文件

沒有頁面的 PDF 本質上是空的。加入頁面只要呼叫 `pdfDocument.Pages.Add()` 即可。新頁面會繼承預設尺寸（A4），除非您另行指定。

```csharp
// Add a fresh, blank page – this satisfies the add blank page pdf requirement
Page page = pdfDocument.Pages.Add();
```

**為什麼重要：** 先加入頁面可確保後續的繪圖指令有可渲染的表面。若跳過此步驟，當您嘗試繪製矩形時會發生執行時錯誤。

## 步驟 3：定義矩形邊界

現在我們將透過建立 `Rectangle` 物件來 **draw rectangle pdf**。建構子接受左下角的 X/Y 座標，接著是寬度與高度。在本例中，我們希望矩形能舒適地位於頁面內部，並保留少量邊距。

```csharp
// Rectangle coordinates: (0,0) is the lower‑left corner of the page
// Width = 500, Height = 700 – fits comfortably on an A4 page
var rectangle = new Rectangle(0, 0, 500, 700);
```

若需要不同尺寸，只要調整寬度/高度的數值即可。矩形的原點 (0,0) 與頁面的左下角對齊，這是新手常犯的混淆點。

## 步驟 4：將矩形形狀加入頁面

當矩形物件準備好後，我們即可 **add rectangle shape** 到頁面。`AddRectangle` 方法會使用目前的圖形狀態繪製輪廓（預設為細黑線）。

```csharp
// Add the rectangle shape – this completes the add rectangle to pdf step
page.AddRectangle(rectangle);
```

您可以在呼叫 `AddRectangle` 前修改 `Graphics` 物件以自訂外觀，例如設定 `LineWidth` 或 `Color`。若要填滿實心，則可使用 `page.AddAnnotation(new SquareAnnotation(...))`，但這已超出本簡易指南的範圍。

## 步驟 5：儲存 PDF 檔案

最後，將文件寫入磁碟。選擇您有寫入權限的資料夾，並為檔案取一個有意義的名稱，例如 `shapes.pdf`。

```csharp
// Save the PDF – you’ll find shapes.pdf in the specified directory
pdfDocument.Save(@"C:\Temp\shapes.pdf");
```

**注意：** 原始程式碼片段中的 `using` 陳述式在此並非必要，因為 `Document` 已實作 `IDisposable`。不過，在較大型的應用程式中，將其包在 `using` 內仍是資源清理的好習慣。

## 完整範例

將上述步驟整合起來，以下是一個可立即執行的獨立 Console 程式範例：

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
            // Step 1: Create a new PDF document
            using (var pdfDocument = new Document())
            {
                // Step 2: Add a blank page to the document
                Page page = pdfDocument.Pages.Add();

                // Step 3: Define a rectangle that fits inside the page bounds (0,0 to 500,700)
                var rectangle = new Rectangle(0, 0, 500, 700);

                // Step 4: Add the rectangle shape to the page
                page.AddRectangle(rectangle);

                // Step 5: Save the PDF file
                string outputPath = @"C:\Temp\shapes.pdf";
                pdfDocument.Save(outputPath);

                Console.WriteLine($"PDF created successfully at {outputPath}");
            }
        }
    }
}
```

**預期輸出：** 執行程式後，開啟 `C:\Temp\shapes.pdf`。您會看到單一頁面，左下角有一個黑色輪廓的矩形，尺寸正好為 500 × 700 點。

## 常見問題與邊緣案例

| Question | Answer |
|----------|--------|
| *我可以在加入矩形之前變更頁面尺寸嗎？* | 可以。建立具有自訂尺寸的 `Page`：`var page = pdfDocument.Pages.Add(); page.PageInfo.Width = 600; page.PageInfo.Height = 800;` |
| *如果需要填滿的矩形該怎麼辦？* | 使用 `Graphics` 物件：`page.Canvas.Rectangle(rectangle, Color.Blue, Color.LightBlue);` |
| *Aspose.PDF 是免費的嗎？* | 它提供具完整功能的 **免費試用**；商業授權則需於正式環境使用。 |
| *如何加入多個矩形？* | 只要以不同的 `Rectangle` 實例或調整座標，重複步驟 3‑4 即可。 |

## 往後步驟

既然您已了解如何 **create pdf document c#**、**add blank page pdf**，以及 **draw rectangle pdf**，接下來或許想探索：

- 在矩形內加入文字（`TextFragment`、`page.Paragraphs.Add`）。  
- 插入圖像（`page.Resources.Images.Add`）以建立更豐富的報告。  
- 使用 Aspose 的轉換 API，將 PDF 匯出為 PNG 或 DOCX 等其他格式。  

所有這些主題皆自然延伸自我們在此建立的 **add rectangle to pdf** 基礎。

---

*祝開發順利！* 若遇到任何問題，歡迎在下方留言。記住——一旦掌握基礎，產生複雜的 PDF 將變得輕而易舉。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}