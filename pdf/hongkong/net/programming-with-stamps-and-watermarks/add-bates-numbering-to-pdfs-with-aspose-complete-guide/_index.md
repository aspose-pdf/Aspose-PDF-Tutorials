---
category: general
date: 2026-04-25
description: 使用 Aspose.Pdf 快速為 PDF 添加 Bates 編號。了解如何在 PDF 中加入頁碼、自動調整字體大小，以及在 C# 中加入文字浮水印。
draft: false
keywords:
- add bates numbering
- add page numbers pdf
- auto adjust font size
- how to add bates
- add text watermark
language: zh-hant
og_description: 使用 Aspose.Pdf 為 PDF 添加 Bates 編號。本指南示範如何在單一可執行範例中加入頁碼、自動調整字型大小，以及加入文字浮水印。
og_title: 為 PDF 添加 Bates 編號 – 完整 Aspose C# 教程
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: 使用 Aspose 為 PDF 添加 Bates 編號 – 完整指南
url: /zh-hant/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose 為 PDF 添加 Bates 編號 – 完整指南

是否曾經需要 **為 PDF 添加 Bates 編號**，卻不知從何下手？你並不孤單——法律團隊、稽核人員與開發者每天都會碰到這個問題。好消息是？只要使用 Aspose.Pdf for .NET，你就能在 C# 程式碼中幾行指令完成 Bates 編號的蓋章、字型自動調整，甚至把蓋章當作細微的文字浮水印。

在本教學中，我們將逐步說明如何 **add page numbers pdf**、調整字型避免溢位，並一次解決「how to add bates」的疑問。完成後，你將擁有一個可直接執行的 Console 應用程式，產生專業編號的 PDF，並了解如何將其擴充為完整的浮水印解決方案。

## 前置條件

在開始之前，請確保你已具備：

* **Aspose.Pdf for .NET**（截至 2026 年 4 月的最新 NuGet 套件）。  
* .NET 6.0 SDK 或更新版本——API 在 .NET Framework 上同樣可用，但 .NET 6 提供最佳效能。  
* 一個名為 `input.pdf` 的範例 PDF，放在可供參考的資料夾（例如 `C:\Docs\`）。  

不需要額外設定；此函式庫是自包含的。

---

## 步驟 1 – 載入來源 PDF 文件

首先，我們打開要編號的檔案。Aspose 的 `Document` 類別代表整個 PDF，載入方式只要把路徑傳給建構子即可。

```csharp
using Aspose.Pdf;

string inputPath = @"C:\Docs\input.pdf";
Document pdfDocument = new Document(inputPath);
```

*為什麼重要*：載入文件後即可取得 `Pages` 集合，稍後會在此集合上加上 Bates 蓋章。如果找不到檔案，Aspose 會拋出明確的 `FileNotFoundException`，讓你立即知道問題所在。

---

## 步驟 2 – 建立 Bates 編號的文字蓋章

接下來，我們製作每頁都會出現的視覺元素。`TextStamp` 類別允許嵌入任意字串，我們會使用佔位符 `{page}-{total}`，讓 Aspose 在執行時自動替換。

```csharp
// Create a stamp that will display "Bates: 1-10", "Bates: 2-10", etc.
TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
{
    // Let the stamp automatically adjust its font size to fit the stamp rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Optional: make the stamp look like a subtle watermark
    Opacity = 0.4,
    // Position the stamp at the bottom‑right corner
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Choose a readable font
    Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
};
```

*重點說明*：

* **auto adjust font size** – 將 `AutoAdjustFontSizeToFitStampRectangle` 設為 `true`，可保證文字永不超出矩形範圍，特別適合長度不固定的頁碼。  
* **add text watermark** – 降低 `Opacity` 後，Bates 編號會變成淡淡的浮水印，滿足「add text watermark」的需求，且不需額外步驟。  
* **how to add bates** – `{page}` 與 `{total}` 這兩個 token 是關鍵；Aspose 會在執行時自動替換，你不必自行計算。

---

## 步驟 3 – 將蓋章套用至每一頁

常見的錯誤是只在第一頁加蓋。若要真正 **add page numbers pdf**，必須遍歷整個 `Pages` 集合。

```csharp
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp for each page to avoid shared state issues
    page.AddStamp(batesStamp);
}
```

為什麼要 clone？`AddStamp` 方法內部會自行建立副本，但在迴圈中明確使用新實例，可避免之後若修改蓋章屬性（例如為特定頁面更改顏色）時產生意外的副作用。

---

## 步驟 4 – 儲存更新後的 PDF

蓋章完成後，將變更寫回檔案相當簡單。你可以覆寫原檔或另存新檔——此處示範儲存為 `output.pdf`。

```csharp
string outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

開啟 `output.pdf` 後，你會看到每頁底部右側顯示「Bates: 1‑10」、「Bates: 2‑10」……，且以淡淡的不透明度同時達成 **add text watermark** 的效果。

---

## 完整範例程式

以下是一個完整、可自行編譯的 Console 程式，直接貼到 Visual Studio 即可執行。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        string inputPath = @"C:\Docs\input.pdf";
        Document pdfDocument = new Document(inputPath);

        // 2️⃣ Create a Bates number stamp with auto‑adjusted font size
        TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Opacity = 0.4, // acts as a subtle watermark
            XIndent = 20,
            YIndent = 20,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
        };

        // 3️⃣ Add the stamp to every page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.AddStamp(batesStamp);
        }

        // 4️⃣ Save the result
        string outputPath = @"C:\Docs\output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**預期結果**：在任意 PDF 閱讀器中開啟 `output.pdf`，每頁右下角會出現類似「Bates: 3‑12」的文字，字型大小恰好填滿矩形，且以 40 % 不透明度呈現。這同時滿足法律追蹤需求與視覺浮水印需求。

---

## 常見變形與例外情況

| 情境 | 需要變更的地方 | 原因 |
|-----------|----------------|-----|
| **不同放置位置** | 調整 `HorizontalAlignment` / `VerticalAlignment` 或設定 `XIndent`/`YIndent` | 有些公司偏好左上角或置中顯示。 |
| **自訂前綴** | 把 `"Bates: "` 換成 `"Doc‑ID: "` 或其他字串 | 可能使用不同的命名慣例。 |
| **多重蓋章** | 建立第二個 `TextStamp`（例如機密聲明），在第一個之後再 `AddStamp` | 同時滿足 **add bates numbering** 與其他 **add text watermark** 要求非常簡單。 |
| **大量頁數** | 提升初始字型大小（例如 `14`）——自動調整會在需要時縮小 | 超過 999 頁時字串會變長，auto‑adjust 可防止被截斷。 |
| **加密的 PDF** | 在蓋章前呼叫 `pdfDocument.Decrypt("password")` | 未提供密碼無法修改受保護的檔案。 |

---

## 專業技巧與常見陷阱

* **技巧**：若文字緊貼頁邊，可設定 `batesStamp.Margin = new MarginInfo(5, 5, 5, 5)`。  
* **注意**：預設矩形尺寸為 100 × 30 pt，若需要更大區域，請手動設定 `batesStamp.Width` 與 `batesStamp.Height`。  
* **效能說明**：對上千頁進行蓋章可能需要數秒鐘，但 Aspose 會有效率地串流頁面——不必一次將整份文件載入記憶體。  

---

## 結論

我們已示範如何使用 Aspose.Pdf 為 PDF **add bates numbering**，同時 **add page numbers pdf**、啟用 **auto adjust font size**，並在同一流程中產生 **add text watermark**。上述完整、可執行的範例為你提供了堅實的基礎，能夠輕鬆套用於任何法律文件工作流程或內部報表系統。

想更進一步？可以將此方法與 Aspose 的 PDF 合併 API 結合，批次處理多個檔案；或探索 `TextFragment` 類別，製作更豐富的浮水印（彩色、旋轉或多行）。可能性無窮，而你現在手上的程式碼已是可靠的起點。

如果本指南對你有幫助，歡迎留言、為儲存庫加星或分享你的變形版本。祝開發順利，願你的 PDF 永遠編號正確！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}