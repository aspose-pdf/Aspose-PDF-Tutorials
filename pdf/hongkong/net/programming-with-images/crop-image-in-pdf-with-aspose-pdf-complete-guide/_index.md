---
category: general
date: 2026-06-08
description: 使用 Aspose.PDF 於 C# 裁切 PDF 中的圖片。學習如何用幾行程式碼建立含圖片的 PDF、儲存含圖片的 PDF，以及將圖片加入
  PDF。
draft: false
keywords:
- crop image in pdf
- create pdf with image
- save pdf with image
- how to add image to pdf
- how to crop image pdf
language: zh-hant
og_description: 在 C# 中使用 Aspose.PDF 裁切 PDF 圖片。本教學示範如何建立含圖片的 PDF、儲存含圖片的 PDF，以及快速將圖片加入
  PDF。
og_title: 使用 Aspose.PDF 在 PDF 中裁剪圖像 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  headline: Crop Image in PDF with Aspose.PDF – Complete Guide
  type: TechArticle
- description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  name: Crop Image in PDF with Aspose.PDF – Complete Guide
  steps:
  - name: '**Image stream** – the raw bytes of your picture.'
    text: '**Image stream** – the raw bytes of your picture.'
  - name: '**Placement rectangle** – where on the page the image lives.'
    text: '**Placement rectangle** – where on the page the image lives.'
  - name: '**Crop rectangle** – the portion of the image you actually want to render.'
    text: '**Crop rectangle** – the portion of the image you actually want to render.'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
- Image processing
title: 使用 Aspose.PDF 在 PDF 中裁剪圖像 – 完整指南
url: /zh-hant/net/programming-with-images/crop-image-in-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.PDF 在 PDF 中裁剪圖像 – 完整指南

有沒有想過在不打開圖形編輯器的情況下 **在 PDF 中裁剪圖像**？你並不是唯一有此需求的人。在許多報告、發票或電子書中，你只需要圖片的一小塊——可能是標誌的角落或圖表的一段——而且希望直接在 PDF 內完成。  

本指南將完整示範這個過程：我們會 **create PDF with image**、**add image to PDF**，然後使用 Aspose.PDF for C# **crop image in PDF**。最後，你也會知道如何 **save PDF with image**，以便將檔案傳送給任何人。

---

## 需要的環境

- .NET 6.0 或更新版本（程式碼同樣支援 .NET Framework 4.6+）  
- 已授權或試用版的 **Aspose.PDF for .NET**（透過 NuGet `Install-Package Aspose.PDF` 安裝）  
- 磁碟上的圖像檔（JPEG/PNG），此處稱為 `image.jpg`  
- 任意你喜歡的 IDE（Visual Studio、Rider、VS Code）

就這些。無需額外服務或外部工具。

---

## 步驟 1：設定專案與匯入

首先，建立一個 console 應用程式，並匯入我們將使用的命名空間。`using` 陳述式可以讓程式碼保持整潔，也讓後續步驟更易閱讀。

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;   // for text fragments if you want captions later
```

> **Pro tip:** 如果你使用 Visual Studio，右鍵點擊專案 → *Manage NuGet Packages* → 搜尋 “Aspose.PDF” 並安裝。此函式庫在內部同時處理圖像放置與裁剪，無需任何第三方圖像函式庫。

---

## 步驟 2：建立含圖像的 PDF

現在我們實際 **create pdf with image**。以下程式碼片段會建立一個全新的 `Document`，新增一個空白頁，並準備圖像串流。

```csharp
// Initialize a new PDF document
Document pdf = new Document();

// Add a blank page – think of it as a clean canvas
Page page = pdf.Pages.Add();

// Open the source image file
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // We'll place the whole image first; cropping comes next
    // Define where the image should sit on the page (in points; 1 point = 1/72 inch)
    Rectangle placement = new Rectangle(0, 0, 600, 800); // width=600pt, height=800pt

    // Add the image without cropping yet – just to see the full picture
    page.AddImage(imgStream, placement);
}
```

執行此程式碼會產生一個 PDF，圖像會被拉伸至你指定的尺寸。這是開始裁剪前的良好驗證步驟。

---

## 步驟 3：如何將圖像加入 PDF（並為裁剪做準備）

如果你已經知道確切的裁剪區域，可以直接跳過全尺寸步驟，直接進入 **how to add image to pdf** 部分。`AddImage` 方法接受三個參數：

1. **Image stream** – 圖片的原始位元組。  
2. **Placement rectangle** – 圖像在頁面上的放置位置。  
3. **Crop rectangle** – 真正要呈現的圖像區塊。

以下是同時完成放置 **and** 裁剪的緊湊寫法。

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Full‑size placement rectangle (you can adjust X/Y if you need margins)
    Rectangle placement = new Rectangle(0, 0, 600, 800);

    // Crop area: upper‑left quarter of the original image
    Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

    // This single line both adds the image and crops it
    page.AddImage(imgStream, placement, crop);
}
```

> **Why this works:** Aspose.PDF 內部會將裁剪矩形映射到圖像的像素尺寸，然後只在 `placement` 區域內渲染該切片。無需額外的 bitmap 處理，這樣可以保持 PDF 檔案體積小。

---

## 步驟 4：如何裁剪 PDF 圖像 – 進階選項

有時四分之一裁剪不足以滿足需求。你可能需要自訂矩形，或想保留圖像的長寬比。以下提供更彈性的做法：

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Placement on the page (centered, 300pt wide, keep original height)
    Rectangle placement = new Rectangle(150, 400, 450, 1200);

    // Suppose you want a 200 × 150 pixel region starting at (50, 30) in the source image
    // First, convert pixel coordinates to points (assuming 72 DPI)
    float dpi = 72f;
    float left   = 50  / dpi * 72; // = 50 points
    float bottom = 30  / dpi * 72; // = 30 points
    float width  = 200 / dpi * 72; // = 200 points
    float height = 150 / dpi * 72; // = 150 points

    Rectangle crop = new Rectangle(left, bottom, left + width, bottom + height);

    page.AddImage(imgStream, placement, crop);
}
```

**Edge case handling:**  
- **Null streams** – 如範例所示，務必將 `FileStream` 包在 `using` 區塊中，以避免資源泄漏。  
- **Large images** – 若來源圖像過大，建議先縮小 `placement` 矩形；Aspose 會自動降採樣。  
- **Transparent PNGs** – 函式庫會保留 alpha 通道，裁剪後的區域仍保持透明。

---

## 步驟 5：儲存含圖像的 PDF（並驗證）

最後，我們 **save pdf with image**。`Save` 方法會將文件寫入磁碟。若你在開發 API，也可以將其串流回 Web 客戶端。

```csharp
// Save the final PDF to the output folder
pdf.Save("YOUR_DIRECTORY/output.pdf");

// Optional: Open the file automatically (only works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/output.pdf",
    UseShellExecute = true
});
```

開啟 `output.pdf` 後，你應該只會看到 `image.jpg` 的裁剪部分，且位置正好與你定義的相同。如果圖像看起來被拉伸，請調整 `placement` 矩形的寬高，使其與裁剪矩形的長寬比相符。

---

## 常見問題與注意事項

| Question | Answer |
|----------|--------|
| **Can I crop multiple images on the same page?** | Absolutely. Call `page.AddImage` for each image with its own placement and crop rectangles. |
| **What if my image is in a different format (e.g., BMP)?** | Aspose.PDF supports JPEG, PNG, BMP, GIF, and TIFF out of the box. Just change the file extension. |
| **Do I need a license for production use?** | A trial works for up to 5 pages. For real deployments, purchase a license to remove the watermark. |
| **How do I rotate the cropped image?** | After adding the image, retrieve the `Image` object and set its `Rotate` property (`Rotate = RotationAngle.Rotate90`). |
| **Is there a way to crop using percentages instead of absolute points?** | Yes—calculate the rectangle dimensions based on `image.Width * 0.25` etc., then convert to points as shown in Step 4. |

---

## 完整範例（可直接複製貼上）

```csharp
using System;
using System.IO;
using Aspose.Pdf;

namespace CropImageInPdfDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new PDF document and add a blank page
            Document pdf = new Document();
            Page page = pdf.Pages.Add();

            // 2️⃣ Open the image that will be placed on the page
            using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
            {
                // 3️⃣ Define where the image will sit on the page (points)
                Rectangle placement = new Rectangle(0, 0, 600, 800);

                // 4️⃣ Define the crop area – upper‑left quarter of the image
                Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

                // 5️⃣ Add the image using both placement and crop rectangles
                page.AddImage(imgStream, placement, crop);
            }

            // (Optional) Save the PDF to verify the result
            pdf.Save("YOUR_DIRECTORY/output.pdf");

            Console.WriteLine("PDF created and image cropped successfully!");
        }
    }
}
```

執行程式，開啟 `output.pdf`，你會看到 `image.jpg` 的左上四分之一被渲染在頁面的左上角。修改 `crop` 矩形的數值即可嘗試不同的裁剪區塊。

---

## 結論

我們已完整示範如何使用 Aspose.PDF for C# **crop image in pdf**。從全新文件開始，我們 **create pdf with image**、說明 **how to add image to pdf**、套用自訂的 **how to crop image pdf** 矩形，最後 **save pdf with image**。  

現在，你可以在任何產生的 PDF 中嵌入精確裁剪的圖片——非常適合發票、行銷手冊或自動化報告。接下來，可考慮加入文字說明 (`TextFragment`) 或在裁剪圖像周圍繪製形狀以強調重點。  

還有其他情境想了解嗎？歡迎留言，祝開發順利！

## 接下來可以學什麼？

以下教學與本指南所示技巧緊密相關，能幫助你進一步掌握 API 功能，並在專案中探索其他實作方式。

- [如何在 PDF 中使用 Aspose.PDF for .NET 設定圖像大小](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [如何使用 Aspose.PDF for .NET 在 PDF 中加入圖像印章：完整指南](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [如何使用 Aspose.PDF for .NET 從 PDF 中提取圖像資訊](/pdf/english/net/images-graphics/extract-image-info-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}