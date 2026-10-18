---
category: general
date: 2026-04-06
description: 快速將 JPG 轉換為 PDF，並學習如何在 PDF 中裁剪圖像、添加新 PDF 頁面，以及使用 C# 進行裁剪後的 JPG 轉 PDF。
draft: false
keywords:
- create pdf from jpg
- crop image in pdf
- how to add new pdf page
- convert jpg to pdf with crop
- insert image into pdf c#
language: zh-hant
og_description: 使用 C# 從 JPG 建立 PDF 並在 PDF 中裁剪圖像。了解如何新增 PDF 頁面以及將 JPG 轉換為帶裁剪的 PDF。
og_title: 在 C# 中將 JPG 轉換為 PDF – 步驟指南
tags:
- Aspose.Pdf
- C#
- PDF generation
title: 在 C# 中從 JPG 建立 PDF – 完整指南，包含裁剪與新增頁面
url: /zh-hant/net/document-conversion/create-pdf-from-jpg-in-c-full-guide-with-cropping-and-new-pa/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 從 JPG 建立 PDF – 完整指南（含裁切與新增頁面）

是否曾需要 **從 JPG 建立 PDF**，卻不確定要如何只保留想要的部分？你並不孤單。在許多應用程式中——例如發票、收據或相簿——開發者必須將圖片轉成 PDF，同時去除不需要的邊緣。

在本教學中，我們將一步步示範一個完整、可直接執行的解決方案，說明如何 **從 JPG 建立 PDF**、如何 **在 PDF 中裁切圖片**，以及在需要多張圖片時 **如何新增 PDF 頁面**。完成後，你也會知道如何 **使用裁切將 JPG 轉成 PDF** 以及 **在 C# 中將圖片插入 PDF**，全部使用 Aspose.Pdf 套件。

## 你將學會

- 在 .NET 專案中設定 Aspose.Pdf（不需繁雜設定）。  
- 載入 JPEG、定義想保留的區域，並在插入 PDF 頁面時同時裁切。  
- 為同一文件新增額外頁面，讓你能從多張圖片建立多頁 PDF。  
- 儲存最終檔案並驗證輸出結果。  

**先備條件：** .NET 6+（或 .NET Framework 4.6+）、Visual Studio 2022 或任何你喜歡的編輯器，並在 NuGet 中加入 `Aspose.Pdf` 參考。無需其他外部服務。

![Create PDF from JPG example](image.jpg){: .align-center alt="建立 PDF 從 JPG 範例，顯示裁切後的圖片放置於 PDF 頁面上"}

---

## 步驟 1：安裝 Aspose.Pdf 並準備專案

首先，加入 Aspose.Pdf 套件。於解決方案資料夾的終端機執行：

```bash
dotnet add package Aspose.Pdf
```

這一行會把所有必需的類別（`Document`、`Rectangle`、`Page` 等）一次拉進來。依我經驗，使用 NuGet 是保持套件最新且不必手動管理 DLL 的最佳方式。

> **專業提示：** 若你是針對 .NET Framework，請改用 `Aspose.Pdf.NET` 套件；API 介面完全相同。

---

## 步驟 2：載入 JPEG 並定義頁面尺寸

我們需要一個畫布，其尺寸與最終 PDF 頁面相符。以下程式碼會建立一個全新的 `Document`，並將來源圖片以串流方式開啟。

```csharp
using Aspose.Pdf;
using System.IO;

// Create a new PDF document – this will hold our pages.
using var pdfDocument = new Document();

// Open the JPEG you want to convert.
using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

// Define the full‑size rectangle (the page) – 600 × 800 points works well for most photos.
var pageBounds = new Rectangle(0, 0, 600, 800);
```

為什麼使用矩形（Rectangle）？在 Aspose.Pdf 中，`Rectangle` 同時代表頁面尺寸與欲顯示的圖片區域。將 *頁面* 與 *裁切區域* 分開，可讓你精細控制最終 PDF 中呈現的內容。

---

## 步驟 3：選取裁切區域（左上四分之一）

假設你只需要照片的左上四分之一。我們會相對於頁面尺寸計算該區域：

```csharp
// Crop the upper‑left quarter of the image.
var cropArea = new Rectangle(
    pageBounds.LLX,                                 // left X (0)
    pageBounds.LLY + pageBounds.Height / 2,         // bottom Y (halfway up)
    pageBounds.LLX + pageBounds.Width / 2,          // right X (halfway across)
    pageBounds.URY);                                // top Y (full height)
```

`Rectangle` 建構子接受 **左下 X/Y** 與 **右上 X/Y** 兩組座標。透過在 `LLY` 上加上高度的一半，我們把裁切的底部往上移，等同於捨棄圖片的下半部。若需其他區塊，請自行調整計算式。

> **為什麼先裁切再加入？**  
> 在 PDF 端裁切可避免在磁碟上產生暫存位圖，省下 I/O 與記憶體開銷。Aspose 會自行處理數學運算，最終產出乾淨且向量友善的 PDF。

---

## 步驟 4：新增頁面並插入裁切後的圖片

現在把圖片放到 PDF 頁面上。這裡正是 **如何新增 PDF 頁面** 發揮作用的地方。

```csharp
// Add a new page to the document.
var page = pdfDocument.Pages.Add();

// Insert the image using both the page bounds and the crop rectangle.
page.AddImage(imageStream, pageBounds, cropArea);
```

`AddImage` 需要三個參數：

1. **Stream** – JPEG 的來源串流。  
2. **Page rectangle** – 定義頁面尺寸（我們的 `pageBounds`）。  
3. **Crop rectangle** – 告訴 Aspose 要渲染圖片的哪一部分。

若需要更多頁面，只要為每次新增的 `imageStream` 重複 `Add` + `AddImage` 的模式即可。這樣即可滿足 **如何新增 PDF 頁面** 的需求，同時保持程式碼簡潔。

---

## 步驟 5：儲存 PDF 並驗證結果

最後一步只需要一行程式碼，但千萬別小看——正確的儲存路徑能確保檔案能被任何 PDF 閱讀器開啟。

```csharp
// Save the PDF to disk.
pdfDocument.Save(@"C:\Output\cropped_image.pdf");

// Optional: open the file automatically (Windows only).
System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
```

開啟 `cropped_image.pdf` 後，你應該會看到單一頁面，僅包含原始 JPEG 的左上四分之一，且完美置中於 600 × 800 的頁面內。

---

## 完整範例（結合所有步驟）

以下是可直接貼到 Console 應用程式的完整程式碼。只要已安裝 Aspose.Pdf 且在指定位置放置 JPEG，即可編譯執行。

```csharp
using Aspose.Pdf;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document.
        using var pdfDocument = new Document();

        // 2️⃣ Open the source JPEG.
        using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

        // 3️⃣ Define the page size (600 × 800 points).
        var pageBounds = new Rectangle(0, 0, 600, 800);

        // 4️⃣ Calculate the crop area – upper‑left quarter.
        var cropArea = new Rectangle(
            pageBounds.LLX,
            pageBounds.LLY + pageBounds.Height / 2,
            pageBounds.LLX + pageBounds.Width / 2,
            pageBounds.URY);

        // 5️⃣ Add a new page and insert the cropped image.
        var page = pdfDocument.Pages.Add();
        page.AddImage(imageStream, pageBounds, cropArea);

        // 6️⃣ Save the resulting PDF.
        pdfDocument.Save(@"C:\Output\cropped_image.pdf");

        // 7️⃣ (Optional) Open the PDF automatically.
        System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
    }
}
```

### 預期輸出

- **檔案：** `cropped_image.pdf`（約 30 KB）。  
- **內容：** 一頁，600 × 800 點，顯示 `photo.jpg` 的左上四分之一。  
- **行為：** 無變形；圖片在裁切範圍內保留原始解析度。

---

## 常見問題與邊緣案例

### 如果我要保留整張圖片，而不是四分之一該怎麼做？

只要把 `cropArea` 設為 `pageBounds` 即可：

```csharp
var cropArea = pageBounds; // No cropping – full image.
```

### 可以改成其他頁面尺寸嗎（例如 A4）？

當然可以。將 `pageBounds` 的值改為 A4 頁面的點數尺寸（595 × 842）：

```csharp
var pageBounds = new Rectangle(0, 0, 595, 842);
```

裁切矩形可以保持不變，或依新比例重新計算。

### 要如何在每一頁放入多張圖片？

對檔案路徑集合做迴圈：

```csharp
foreach (var path in imagePaths)
{
    using var stream = File.OpenRead(path);
    var page = pdfDocument.Pages.Add();
    page.AddImage(stream, pageBounds, pageBounds); // No crop for each image.
}
```

### PNG 或透明度怎麼處理？

Aspose.Pdf 對 PNG 的處理方式與 JPEG 相同。若來源含有 Alpha 通道，只要 PDF 版本支援透明度（預設即可），PDF 會保留該資訊。

### 這在 Linux 上的 .NET Core 可行嗎？

可以。Aspose.Pdf 是跨平台的，只要 `imageStream` 指向目標作業系統上有效的檔案路徑即可。程式碼未使用任何 Windows 專屬 API。

---

## 小技巧與最佳實踐

- **記憶體管理：** 如範例所示，務必將串流包在 `using` 陳述式內，以避免檔案被鎖定。  
- **效能：** 若一次處理大量圖片，考慮重複使用同一個 `Document` 實例，並對每張圖片呼叫 `pdfDocument.Pages.Add()`。  
- **錯誤處理：** 將整段程式碼包在 `try/catch`，捕捉 `PdfException` 以便除錯。  
- **品質控制：** 透過 `ImageFragment` 可設定影像解析度。對高 DPI 掃描，可設定 `ImageFragment.Resolution = 300;`。  
- **安全性：** 若 PDF 需對外分享，可使用 `pdfDocument.Encrypt("ownerPwd", "userPwd", Permission.All);` 加密。

---

## 結論

我們已說明如何在 C# 中 **從 JPG 建立 PDF**、**在 PDF 中裁切圖片**，以及 **新增 PDF 頁面** 以組合多頁文件。同樣的模式也能讓你 **將 JPG 轉成帶裁切的 PDF**，以及 **在 C# 中將圖片插入 PDF**，無論是簡單收據還是複雜相簿，都能輕鬆應對。

不妨試試看：改變裁切邏輯、使用 A4 頁面，或串接多張圖片。Aspose.Pdf 讓這些工作變得毫不費力，而上述程式碼則是一個可靠、可直接引用的範例。

---

### 接下來可以做什麼？

- **在 PDF 加入文字註解**（例如每張圖片下方的說明）。  
- **自動產生目錄**，適用於多頁 PDF。  
- **合併多個 PDF**，使用 `pdfDocument.Pages.AddRange(otherDoc.Pages);`。  

上述主題皆以本章所學為基礎，讓你能順利展開更進階的應用。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}