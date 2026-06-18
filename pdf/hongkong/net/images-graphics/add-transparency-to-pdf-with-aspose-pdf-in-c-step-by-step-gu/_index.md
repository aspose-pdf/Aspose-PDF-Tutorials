---
category: general
date: 2026-03-19
description: 使用 Aspose.PDF for C# 為 PDF 添加透明度。只需幾行程式碼，即可學習如何設定不透明度、混合模式和 ExtGState。
draft: false
keywords:
- add transparency to pdf
- Aspose PDF transparency
- C# PDF graphics state
- PDF blend mode
- set PDF opacity
language: zh-hant
og_description: 快速為 PDF 添加透明度。本指南說明如何在 C# 中使用 Aspose.PDF 控制不透明度與混合模式。
og_title: 使用 Aspose PDF 為 PDF 添加透明度 – 完整 C# 教程
tags:
- Aspose.PDF
- C#
title: 在 C# 中使用 Aspose PDF 為 PDF 添加透明度 – 逐步指南
url: /zh-hant/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中使用 Aspose PDF 為 PDF 添加透明度 – 完整教學

有沒有想過 **如何在不與低階 PDF 語法糾纏** 的情況下為 PDF 檔案加入透明度？你並不孤單。許多開發者都需要快速的方式讓圖形或文字呈現半透明——例如浮水印、覆蓋圖形，或文件內的細微 UI 提示。  

在本指南中，我們將逐步說明一個 **完整、可執行的範例**，展示如何使用 Aspose.PDF for .NET 設定填充不透明度、描邊不透明度以及混合模式。完成後，你將得到一個矩形以 50 % 不透明度呈現的 PDF，並了解 ExtGState 字典是實現此效果的關鍵。

我們會涵蓋所有必備項目：所需的 NuGet 套件、程式碼本身、每行說明，以及針對舊版 PDF 閱讀器的少數技巧。沒有外部參考——只要一個可直接複製貼上、立即執行的自包含解決方案。

## 您需要的條件

- **Aspose.PDF for .NET**（v23.12 或更新版本）。透過 NuGet 安裝：`Install-Package Aspose.PDF`。
- .NET 開發環境（Visual Studio、Rider，或 `dotnet` CLI）。
- 一個名為 `input.pdf` 的範例 PDF，放置於你可控制的資料夾（教學中以 `YOUR_DIRECTORY/` 作為佔位符）。

就這樣。如果你已備妥上述項目，讓我們開始吧。

## 為 PDF 添加透明度 – 概覽

在 PDF 中實現透明的核心是 **圖形狀態**（`ExtGState`）。透過將自訂圖形狀態物件加入頁面的資源字典，你可以定義：

| Property | Meaning |
|----------|---------|
| `ca` | 填充不透明度（0 = 完全透明，1 = 不透明）。 |
| `CA` | 描邊不透明度（同樣的比例）。 |
| `BM` | 混合模式（例如 `Normal`、`Multiply`）。 |

我們會建立一個新的圖形狀態，將它插入頁面的 `ExtGState` 字典，然後在之後的繪圖時引用它。以下程式碼片段正是如此操作。

![add transparency to pdf diagram](add_transparency_to_pdf.png){alt="add transparency to pdf"}

## 步驟 1：設定專案並載入 PDF

首先，我們建立一個簡易的主控台應用程式（或任何 C# 專案），並載入來源 PDF。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;          // For low‑level PDF operators
using Aspose.Pdf.Text;               // Optional, if you want to add text later
using Aspose.Pdf.XObjects;          // For image handling, not needed here

// Define the folder that contains the PDF file
string inputDir = @"YOUR_DIRECTORY/";

// Load the PDF document
using (var pdfDocument = new Document(Path.Combine(inputDir, "input.pdf")))
{
    // All subsequent steps go inside this using block
```

**為什麼這很重要：**  
`Document` 是使用 Aspose 進行任何 PDF 操作的入口點。將它包在 `using` 陳述式中，可確保在稍後儲存檔案時所有資源正確釋放。

## 步驟 2：存取第一頁及其資源

我們需要第一頁的資源字典，因為 `ExtGState` 集合就位於此處。

```csharp
    // Grab the first page (pages are 1‑based in Aspose)
    Page firstPage = pdfDocument.Pages[1];

    // Helper to edit dictionaries (resources, etc.)
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);

    // Retrieve the existing ExtGState dictionary, or create a new one if missing
    CosPdfDictionary extGStateDict;
    if (resourcesEditor.ContainsKey("ExtGState"))
    {
        extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
    }
    else
    {
        extGStateDict = new CosPdfDictionary(pdfDocument);
        resourcesEditor.Add("ExtGState", extGStateDict);
    }
```

**說明：**  
如果該頁已經有 `ExtGState` 條目，我們就重複使用；否則建立一個新的字典。此防禦式寫法可避免在缺少圖形狀態的 PDF 中發生空參考錯誤。

## 步驟 3：建立具有所需不透明度的新圖形狀態

現在定義實際的透明度數值。

```csharp
    // Create an empty dictionary that will represent our new graphics state
    CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Stroke opacity – fully opaque (1.0)
    newGraphicsState.Add("CA", new CosPdfNumber(1));

    // Fill opacity – 50 % transparent (0.5)
    newGraphicsState.Add("ca", new CosPdfNumber(0.5));

    // Blend mode – Normal is the default, but you can experiment with Multiply, Screen, etc.
    newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

**為什麼使用這些鍵？**  
- `CA` 控制描邊（線條、邊框）的不透明度。  
- `ca` 控制填充（實心形狀、文字）的不透明度。  
- `BM` 選擇透明物件與底層內容的混合方式。使用 `"Normal"` 可在各閱讀器間保持可預測的視覺結果。

## 步驟 4：在頁面資源中註冊圖形狀態

我們為圖形狀態命名（`GS0`），並將它加入 `ExtGState` 字典。

```csharp
    // Add the graphics state to the ExtGState dictionary with a unique name
    extGStateDict.Add("GS0", newGraphicsState);
```

**提示：**  
若需要多個具有不同不透明度的透明物件，可建立額外條目（`GS1`、`GS2` …），並相應調整 `ca`/`CA` 的數值。

## 步驟 5：使用新圖形狀態繪製透明矩形

圖形狀態就緒後，我們即可繪製實際使用它的圖形。以下程式碼在頁面上加入一個半透明的藍色矩形。

```csharp
    // Prepare a content stream for the page (adds to existing content)
    var canvas = new Aspose.Pdf.Drawing.Graphic(firstPage);

    // Set the graphics state we just created
    canvas.SetGraphicsState("GS0");

    // Choose a fill color (blue) and draw the rectangle
    canvas.SetColor(new Aspose.Pdf.Drawing.Color(0, 0, 255)); // RGB blue
    canvas.Rectangle(100, 500, 200, 100); // x, y, width, height

    // Close the canvas to flush commands
    canvas.Close();
```

**您將看到：**  
開啟產生的 PDF 後，會在指定位置看到藍色矩形，但底層的頁面內容仍可透過它看到，因為填充不透明度為 0.5。若使用 Adobe Acrobat 的「編輯 PDF」功能檢查，你會看到附加在該矩形上的 `ExtGState` 物件（`GS0`）。

## 步驟 6：儲存更新後的 PDF

最後，將修改過的文件寫回磁碟。

```csharp
    // Save the document with a new name so the original stays untouched
    pdfDocument.Save(Path.Combine(inputDir, "ExtGStateAdded.pdf"));
}
```

以上即為完整流程。執行主控台應用程式，開啟 `ExtGStateAdded.pdf`，即可驗證透明覆蓋層。

---

## 完整可執行範例（直接複製貼上）

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class AddTransparencyDemo
{
    static void Main()
    {
        // Step 1: Define the folder that contains the PDF file
        string inputDir = @"YOUR_DIRECTORY/";

        // Step 2: Load the PDF document
        using (var pdfDocument = new Document(Path.Combine(inputDir, "input.pdf")))
        {
            // Step 3: Get the first page and its resource dictionary
            Page firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            CosPdfDictionary extGStateDict;
            if (resourcesEditor.ContainsKey("ExtGState"))
                extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
            else
            {
                extGStateDict = new CosPdfDictionary(pdfDocument);
                resourcesEditor.Add("ExtGState", extGStateDict);
            }

            // Step 4: Create a new graphics state with opacity and blend mode settings
            CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            newGraphicsState.Add("CA", new CosPdfNumber(1));          // stroke opacity (fully opaque)
            newGraphicsState.Add("ca", new CosPdfNumber(0.5));       // fill opacity (50% transparent)
            newGraphicsState.Add("BM", new CosPdfName("Normal"));   // blend mode

            // Step 5: Add the new graphics state to the page resources
            extGStateDict.Add("GS0", newGraphicsState);

            // Step 6: Draw a rectangle using the new graphics state
            var canvas = new Graphic(firstPage);
            canvas.SetGraphicsState("GS0");
            canvas.SetColor(new Color(0, 0, 255)); // blue fill
            canvas.Rectangle(100, 500, 200, 100);
            canvas.Close();

            // Step 7: Save the updated PDF document
            pdfDocument.Save(Path.Combine(inputDir, "ExtGStateAdded.pdf"));
        }

        Console.WriteLine("PDF with transparency created successfully.");
    }
}
```

**預期結果：**  
開啟 `ExtGStateAdded.pdf` 後，會在 (100, 500) 位置看到一個藍色矩形，填充不透明度為 50 %。矩形下方的任何文字或影像仍保持可見。

---

## 常見問題與邊緣案例

### 這在較舊的 PDF 閱讀器上可用嗎？
大多數現代閱讀器（Adobe Reader、Foxit、Chrome）皆支援基本的 `ca`/`CA` 不透明度鍵。非常舊的閱讀器可能會忽略這些鍵，將圖形渲染為完全不透明。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}