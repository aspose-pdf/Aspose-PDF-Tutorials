---
category: general
date: 2026-02-12
description: 快速為 PDF 檔案添加 Bates 編號。了解如何使用 Aspose.PDF 為 PDF 添加文字欄位、表單欄位以及頁碼。
draft: false
keywords:
- add bates numbers
- add text field pdf
- add form field pdf
- add page numbers pdf
- how to add bates
language: zh-hant
og_description: 在 C# 中為 PDF 文件添加 Bates 編號。本指南說明如何使用 Aspose.PDF 為 PDF 添加文字欄位、表單欄位以及頁碼。
og_title: 為 PDF 添加 Bates 編號 – 完整 C# 教程
tags:
- PDF
- C#
- Aspose.PDF
title: 為 PDF 添加 Bates 編號 – 步驟式 C# 指南
url: /zh-hant/net/programming-with-forms/add-bates-numbers-to-pdfs-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 中加入 Bates Numbers – 完整 C# 指南

有沒有曾經需要 **add bates numbers** 到一堆法律 PDF，但不知從何下手？你並不孤單。在許多律師事務所和電子發現（e‑discovery）專案中，為每一頁加上唯一識別碼是日常工作，手動操作更是噩夢。  

好消息是？只要幾行 C# 程式碼加上 Aspose.PDF，就能自動化整個流程。在本教學中，我們將逐步說明 **how to add bates** numbers，於每頁灑入文字欄位，並儲存為乾淨、可搜尋的 PDF——全程毫不費力。  

> **What you’ll get:** 完整可執行的程式碼範例、每行程式意義說明、邊緣案例的技巧，以及快速核對清單，以驗證輸出結果。  

我們也會提及相關任務，如 **add text field pdf**、**add form field pdf** 與 **add page numbers pdf**，讓你擁有一套工具箱，應付任何文件自動化挑戰。

---

## 前置條件

- .NET 6.0 或更新版本（此程式碼亦相容 .NET Framework 4.6 以上）  
- Visual Studio 2022（或任何你偏好的 IDE）  
- 有效的 Aspose.PDF for .NET 授權（免費試用版可用於測試）  
- 一個名為 `source.pdf` 的來源 PDF，放置於可參考的資料夾中  

如果上述任一項目你不熟悉，請先暫停並安裝缺少的部分再繼續。以下步驟假設你已經加入 Aspose.PDF NuGet 套件：

```bash
dotnet add package Aspose.Pdf
```

---

## 使用 Aspose.PDF 為 PDF 加入 Bates Numbers

以下為完整、可直接複製貼上的程式。它會載入 PDF，在每頁建立 **text box field**，寫入格式化的 Bates number，最後將修改後的檔案寫出。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 👉 Step 1: Load the source PDF document
        using (var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf"))
        {
            // 👉 Step 2: Add a Bates number text field to each page
            for (int pageNumber = 1; pageNumber <= pdfDocument.Pages.Count; pageNumber++)
            {
                // Define the rectangle where the field will appear (10,10) = lower‑left corner
                var fieldRect = new Rectangle(10, 10, 150, 30);

                // Create the TextBoxField – this is the “add text field pdf” part
                var batesField = new TextBoxField(pdfDocument.Pages[pageNumber], fieldRect)
                {
                    // Format the number: BATES-00001, BATES-00002, …
                    Value = $"BATES-{pageNumber:D5}"
                };

                // Register the field with the form collection – “add form field pdf”
                pdfDocument.Form.Add(batesField, $"Bates_{pageNumber}", pageNumber);
            }

            // 👉 Step 3: Save the modified PDF with Bates numbers
            pdfDocument.Save(@"YOUR_DIRECTORY\bates.pdf");
        }

        Console.WriteLine("✅ Bates numbers added successfully!");
    }
}
```

### 為什麼這樣可行

- **`Document`** 是入口點；它代表整個 PDF 檔案。  
- **`Rectangle`** 定義欄位在頁面上的位置。數值以點 (point) 為單位 (1 pt ≈ 1/72 in)。若需將編號放在其他角落，請調整座標。  
- **`TextBoxField`** 是 *form field*，可容納任何字串。透過設定 `Value`，我們實際上 **add page numbers pdf** 並加上自訂前綴。  
- **`pdfDocument.Form.Add`** 將欄位註冊至 PDF 的 AcroForm，使其在 Adobe Acrobat 等檢視器中可見。  

如果你需要變更外觀（字型、顏色、大小），可以調整 `TextBoxField` 的屬性——請參閱 Aspose 文件中的 `DefaultAppearance` 與 `Border`。

---

## 為每個 PDF 頁面加入文字欄位（“add text field pdf” 步驟）

有時你只想要一個可見的標籤，而非互動式表單欄位。此時可將 `TextBoxField` 換成 `TextFragment`，直接加入頁面的 `Paragraphs` 集合。以下是一個快速的替代方案：

```csharp
var fragment = new TextFragment($"BATES-{pageNumber:D5}")
{
    // Position the text using a TextState (font, size, color)
    TextState = new TextState
    {
        Font = FontRepository.FindFont("Arial"),
        FontSize = 12,
        ForegroundColor = Color.Black
    }
};

// Set the fragment’s rectangle (same coordinates as before)
fragment.Position = new Position(10, 10);
pdfDocument.Pages[pageNumber].Paragraphs.Add(fragment);
```

**add text field pdf** 方法適用於最終文件為唯讀時，而 **add form field pdf** 方法則可在之後保持編號可編輯。

---

## 儲存帶有 Bates Numbers 的 PDF（“add page numbers pdf” 時刻）

迴圈結束後，呼叫 `pdfDocument.Save` 會將所有內容寫入磁碟。若需保留原始檔案，只要更改輸出路徑，或使用 `pdfDocument.Save` 的多載將結果直接串流至 Web API 的回應。

```csharp
// Example: stream to HTTP response (ASP.NET Core)
Response.ContentType = "application/pdf";
pdfDocument.Save(Response.Body);
```

這就是精髓所在——不需要暫存檔案，也不需額外函式庫，全部交由 Aspose 處理。

---

## 預期結果與快速驗證

在任何 PDF 檢視器中開啟 `bates.pdf`。你應該會在每頁左下角看到一個小方框，內容如下：

```
BATES-00001
BATES-00002
…
```

若檢查文件屬性，你會發現 AcroForm 包含名稱為 `Bates_1`、`Bates_2` 等的欄位。這證明 **add form field pdf** 步驟已成功。

---

## 常見陷阱與專業技巧

| 問題 | 為何發生 | 解決方案 |
|-------|----------------|-----|
| 編號出現偏離中心 | Rectangle 座標是相對於頁面的左下角。 | 將 Y 值反轉（`pageHeight - marginTop`）或使用 `page.PageInfo.Height` 計算上邊距位置。 |
| 欄位在 Adobe Reader 中不可見 | 預設邊框設定為 “No”。 | 設定 `batesField.Border = new Border { Width = 0.5f, Color = Color.Black };` |
| 大型 PDF 造成記憶體壓力 | `using` 只在迴圈結束後才釋放文件。 | 將頁面分批處理，或使用 `pdfDocument.Save` 搭配支援串流的 `SaveOptions`。 |
| 授權未套用 | Aspose 會在第一頁印上浮水印。 | 早期註冊授權：`License lic = new License(); lic.SetLicense("Aspose.Pdf.lic");` |

---

## 擴充解決方案

- **自訂前綴**：將 `"BATES-"` 替換為任何字串（如 `"DOC-"`、`"CASE-"` …）。  
- **零填充長度**：將 `{pageNumber:D5}` 改為 `{pageNumber:D3}` 以使用三位數。  
- **動態定位**：使用 `pdfDocument.Pages[pageNumber].PageInfo.Width` 將欄位放置於右側。  
- **條件編號**：透過檢查 `pdfDocument.Pages[pageNumber].IsBlank` 來跳過空白頁。  

所有這些變化皆保留 **add bates numbers**、**add text field pdf** 與 **add form field pdf** 的核心模式。

---

## 完整範例（全功能版）

以下為最終、可直接執行的程式，已整合上述技巧。將其複製到新的 Console 應用程式中，然後按 F5 執行。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;

class AddBatesNumbers
{
    static void Main()
    {
        // Register your license here (optional for trial)
        // var license = new License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        using (var pdfDocument = new Document(inputPath))
        {
            int totalPages = pdfDocument.Pages.Count;

            for (int i = 1; i <= totalPages; i++)
            {
                // Position the field 10 pts from left and 10 pts from bottom
                var rect = new Rectangle(10, 10, 150, 30);

                var batesField = new TextBoxField(pdfDocument.Pages[i], rect)
                {
                    Value = $"BATES-{i:D5}"
                };

                // Optional: make the field look nicer
                batesField.Border = new Border
                {
                    Width = 0.5f,
                    Color = Color.Gray
                };
                batesField.DefaultAppearance = new DefaultAppearance
                {
                    Font = FontRepository.FindFont("Arial"),
                    FontSize = 10,
                    ForegroundColor = Color.DarkBlue
                };

                pdfDocument.Form.Add(batesField, $"Bates_{i}", i);
            }

            pdfDocument.Save(outputPath);
        }

        Console.WriteLine($"✅ Finished! Bates numbers saved to: {outputPath}");
    }
}
```

執行後，開啟結果檔案，你會在每頁看到專業外觀的識別碼——正是訴訟支援專員所期待的。

---

## 結論

我們剛剛示範了如何使用 C# 與 Aspose.PDF 為任何 PDF **add bates numbers**。透過在每頁建立 **text box field**，我們同時在一次處理中完成 **add text field pdf**、**add form field pdf** 與 **add page numbers pdf**。此方法快速、具擴充性，且易於針對自訂前綴、不同版面或條件邏輯進行調整。  

準備好接受下一個挑戰了嗎？試著嵌入指向原始案件檔案的 QR code，或產生一個列出所有 Bates Numbers 及其對應頁面標題的索引頁。相同的 API 也能合併 PDF、抽取頁面，甚至遮蔽敏感資訊——無所不能。  

如果遇到問題，請在下方留言或參考 Aspose 官方文件以深入了解。祝程式開發順利，願你的 PDF 永遠編號完整！  

---  

![add bates numbers screenshot](https://example.com/images/add-bates-numbers.png "add bates numbers example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}