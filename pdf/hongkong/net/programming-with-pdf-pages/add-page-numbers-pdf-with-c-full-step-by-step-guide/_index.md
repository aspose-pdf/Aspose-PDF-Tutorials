---
category: general
date: 2026-01-02
description: 使用 Aspose.Pdf 於 C# 快速為 PDF 添加頁碼。學習如何加入 Bates 編號、頁腳文字、自訂浮水印，並在單一腳本中遍歷
  PDF 頁面。
draft: false
keywords:
- add page numbers pdf
- add bates numbering
- add footer text
- add custom watermark
- loop through pdf pages
language: zh-hant
og_description: 使用 Aspose.Pdf 即時為 PDF 添加頁碼。本指南亦涵蓋添加 Bates 編號、頁腳文字、自訂浮水印，以及遍歷 PDF 頁面。
og_title: 使用 C# 為 PDF 添加頁碼 – 完整程式設計教學
tags:
- C#
- Aspose.Pdf
- PDF manipulation
title: 使用 C# 為 PDF 添加頁碼 – 完整逐步指南
url: /zh-hant/net/programming-with-pdf-pages/add-page-numbers-pdf-with-c-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 為 PDF 加入頁碼 – 完整程式教學

有沒有曾經需要 **為 PDF 加入頁碼** 卻不知從何下手？你並非唯一遇到這個問題的人——開發者常常詢問如何在 PDF 的每一頁上蓋上編號、頁腳，甚至是 Bates 風格的識別碼。

在本教學中，你將看到一個可直接執行的 C# 範例，會 **loop through pdf pages**，在每頁加上頁碼頁腳，並（如果需要）加入自訂浮水印。我們也會示範如何將印章切換成 Bates 編號，這只不過是法律或鑑識文件中「add bates numbering」的說法而已。完成後，你將擁有一個單一、可重複使用的方法，輕鬆處理上述所有工作。

## Add page numbers pdf – Overview

在深入程式碼之前，先釐清在 Aspose.Pdf 世界裡「add page numbers pdf」究竟是什麼意思。這個函式庫會將你放在頁面上的任何文字視為 **TextStamp**。只要建立一個帶有頁碼佔位符（`{page}`）的印章，並套用到每一頁，就會自動產生連續編號。同一個印章還可以攜帶額外文字，讓你 **add footer text** 如「Confidential」或特定案件的識別碼。

> **為什麼使用印章而不是直接編輯 PDF 內容串流？**  
> 印章是高階物件，會自動考慮頁邊距、旋轉角度以及既有圖形。維護起來也更簡單——只要調整幾個屬性，再重新執行腳本即可。

## Loop through PDF pages to apply stamps

第一個實作步驟是開啟來源 PDF，並對其頁面進行迭代。這就是大多數 Aspose 範例使用的 **loop through pdf pages** 模式。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Paths – change these to match your environment
string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // The loop – every Page object lives in pdfDocument.Pages
    foreach (Page page in pdfDocument.Pages)
    {
        // We'll attach a stamp later (see next section)
    }

    // Save the modified document
    pdfDocument.Save(outputPdfPath);
}
```

> **小技巧：** 若你的 PDF 非常龐大（上百頁），建議分批處理以降低記憶體使用量。Aspose.Pdf 會延遲載入頁面，因此迴圈本身已相當有效率。

## Add bates numbering and footer text

現在我們可以逐頁走訪，接下來建立一個 **reusable TextStamp**，同時帶有頁碼與可選的頁腳文字。`{page}` 佔位符會自動被當前頁碼取代。

```csharp
// Create a stamp that will be reused for every page
var batesStamp = new TextStamp("Bates-{page} – Confidential")
{
    // Position the stamp 20 points from the left and bottom edges
    XIndent = 20,
    YIndent = 20,
    // Align left‑bottom so it behaves like a traditional footer
    HorizontalAlignment = HorizontalAlignment.Left,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Font styling – Times New Roman, 10pt, bold, gray
    Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Gray }
};

// Attach the stamp to every page
foreach (Page page in pdfDocument.Pages)
    page.AddStamp(batesStamp);
```

### 為什麼這樣可行

* **`Bates-{page}`** – Aspose 會把 `{page}` 取代為實際頁碼，從而自動產生傳統的 Bates 編號。  
* **`Confidential`** – 這就是 **add footer text** 的部分。你可以換成任何字串，甚至從資料庫抓取資料。  
* **樣式設定** – 使用 `TextState` 可以調整顏色、不透明度，甚至旋轉角度，而不必觸碰 PDF 內部的內容串流。

如果只需要純數字，只要去掉「Bates‑」前綴與額外文字即可：

```csharp
var simpleStamp = new TextStamp("{page}")
{
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    Font = new Font(FontFamily.Helvetica, 12, FontStyle.Regular),
    TextState = { ForegroundColor = Color.Black }
};
```

## Add a custom watermark (optional)

有時候你需要的不只是頁腳——可能要在整頁加上半透明的商標或「DRAFT」覆蓋層。這時 **add custom watermark** 就派上用場。只要重新設定 `TextStamp` 的對齊方式與不透明度，即可重新利用同一個類別。

```csharp
var watermark = new TextStamp("DRAFT")
{
    // Center it both horizontally and vertically
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Center,
    // Make it big and light
    Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Red, FontSize = 72, FontStyle = FontStyle.Bold, 
                  Transparency = 0.5f }   // 50% transparent
};

// Apply the watermark on top of the page‑number stamp
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(watermark);   // watermark on top
    page.AddStamp(batesStamp);  // then the footer
}
```

> **注意：** 執行順序很重要。先加入浮水印可以確保頁碼在半透明文字之上仍保持可讀。

## Save the PDF and verify results

印章完成後，最後一步是將變更寫回磁碟。先前放置的 `Save` 呼叫已負責大部分工作，這裡再加上一段簡易驗證程式碼，會開啟新檔並印出已處理的頁數。

```csharp
pdfDocument.Save(outputPdfPath);

// Quick verification
using (var resultDoc = new Document(outputPdfPath))
{
    Console.WriteLine($"✅ Successfully added page numbers to {resultDoc.Pages.Count} pages.");
}
```

執行完整程式後，你應該會看到每一頁的結尾類似 **「Bates‑3 – Confidential」**（若使用簡易印章則只會是「3」），若啟用了浮水印，則會在頁面中間看到淡淡的「DRAFT」字樣。

### Expected output

| Page | Footer (example) |
|------|------------------|
| 1    | Bates‑1 – Confidential |
| 2    | Bates‑2 – Confidential |
| …    | … |
| N    | Bates‑N – Confidential |

若在檢視器中開啟檔案，頁碼會距左邊與底部邊距各 20 pts，符合一般法律文件的慣例。

## Full working example (copy‑paste ready)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // ---------- Create the page‑number/footer stamp ----------
    var batesStamp = new TextStamp("Bates-{page} – Confidential")
    {
        XIndent = 20,
        YIndent = 20,
        HorizontalAlignment = HorizontalAlignment.Left,
        VerticalAlignment   = VerticalAlignment.Bottom,
        Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Gray }
    };

    // ---------- Optional watermark ----------
    var watermark = new TextStamp("DRAFT")
    {
        HorizontalAlignment = HorizontalAlignment.Center,
        VerticalAlignment   = VerticalAlignment.Center,
        Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Red, Transparency = 0.5f }
    };

    // ---------- Apply stamps to every page ----------
    foreach (Page page in pdfDocument.Pages)
    {
        page.AddStamp(watermark);   // comment out if you don't need a watermark
        page.AddStamp(batesStamp);
    }

    // ---------- Save and verify ----------
    pdfDocument.Save(outputPdfPath);
    Console.WriteLine($"✅ Added page numbers and watermark to {pdfDocument.Pages.Count} pages.");
}
```

將此檔案存為 `AddPageNumbers.cs`，還原 Aspose.Pdf NuGet 套件（`Install-Package Aspose.Pdf`），然後執行。你將得到一個 **add page numbers pdf** 檔案，同時示範 **add bates numbering**、**add footer text**、**add custom watermark**，以及經典的 **loop through pdf pages** 模式——全部集中在一個整潔的腳本裡。

![add page numbers pdf example](https://example.com/images/add-page-numbers-pdf.png "Screenshot showing numbered PDF pages with footer and watermark")

## Conclusion

我們已完整說明如何使用 Aspose.Pdf 於 C# **add page numbers pdf**。從逐頁迭代、蓋上 Bates 編號、加入自訂頁腳文字，到疊加半透明浮水印，程式碼足夠精簡，能直接嵌入任何既有專案。

接下來，你可以探索更進階的情境——例如從資料庫取得頁腳文字、依段落套用不同字型，或產生一份列出所有 Bates 編號的索引 PDF。所有這些延伸功能皆建立在本教學的核心概念上，讓你在需求成長時能輕鬆擴充解決方案。

試著動手改寫、調整樣式，並在留言區分享你的使用心得。祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}