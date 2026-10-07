---
category: general
date: 2026-10-07
description: 學習如何使用 C# 為 PDF 加入 Bates 編號。本一步一步的指南亦涵蓋 PDF 頁碼編號及其他編號技巧。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- pdf page numbering
- number pdf pages
- how to add bates
- bates numbering pdf
language: zh-hant
lastmod: 2026-10-07
og_description: 快速為 PDF 添加 Bates 編號。跟隨本教程，掌握 PDF 頁碼編排、為 PDF 頁面編號，並自動化文件追蹤。
og_image_alt: Screenshot of a PDF with Bates numbers added using Aspose.Pdf
og_title: 在 C# 中為 PDF 添加 Bates 編號 – 完整 Aspose 指南
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  headline: How to add bates numbering to a PDF with Aspose.Pdf
  type: TechArticle
- description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  name: How to add bates numbering to a PDF with Aspose.Pdf
  steps:
  - name: 1. Can I change the location of the numbers?
    text: Yes. Set `batesOptions.Position = new Position(10, 10, 10, 10);` where the
      four values represent margins from the top, bottom, left, and right edges. Aspose
      also provides predefined enums such as `BatesNumberingPosition.BottomCenter`.
  - name: 2. What if my PDF already contains page numbers?
    text: Adding Bates numbers will **stack** on top of existing numbers. To avoid
      visual clutter, either hide the original numbers (if they are part of a text
      layer) or adjust the `batesOptions` font size and position.
  - name: 3. Does this work with encrypted PDFs?
    text: 'Aspose can open password‑protected PDFs if you supply the password:'
  - name: 4. How do I **number pdf pages** with a simple sequential counter (no prefix/suffix)?
    text: 'Just set `Prefix = string.Empty` and `Suffix = string.Empty`:'
  - name: 5. Can I use this approach in ASP.NET Core to serve PDFs on‑the‑fly?
    text: 'Absolutely. Load the document, apply the numbering, then write the stream
      to the HTTP response:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: 如何使用 Aspose.Pdf 為 PDF 添加 Bates 編號
url: /zh-hant/net/programming-with-pdf-pages/how-to-add-bates-numbering-to-a-pdf-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 PDF 中加入 Bates 編號（使用 Aspose.Pdf）

如果您需要 **在 PDF 中加入 Bates 編號**，本指南將示範如何在 C# 中完成。無論是製作法律文件、管理案件檔案，或只是想要可靠的 **pdf 頁碼編號**，以下步驟提供完整且可直接執行的解決方案。

在本教學中您將學會：

* 載入現有的 PDF 檔案。
* 設定 Bates 編號選項，如前綴、起始號碼、位數填充、分隔符與後綴。
* 將編號套用至每一頁。
* 儲存更新後的文件。

不需要任何外部工具，只要使用 Aspose.Pdf for .NET 套件，且程式碼相容於 .NET 6+ 以及 .NET Framework 4.7.2+。

---

## 前置條件

開始之前，請確保您具備以下項目：

| 前置條件 | 為何重要 |
|----------|----------|
| **Aspose.Pdf for .NET**（NuGet 套件 `Aspose.Pdf`） | 提供程式碼中使用的 `Document` 與 `BatesNumberingOptions` 類別。 |
| **.NET SDK**（建議 6.0 以上） | 讓您能編譯與執行 C# 主控台應用程式。 |
| **欲編號的來源 PDF** | 教學範例使用 `source.pdf`，請自行替換為實際檔案路徑。 |
| **寫入權限**至輸出資料夾 | `Save` 方法需要寫入新檔案。 |

您可以使用以下 CLI 指令安裝套件：

```bash
dotnet add package Aspose.Pdf
```

---

## 第一步：建立新的主控台專案

在終端機執行：

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
```

此指令會建立一個最小的 C# 專案，我們接下來會在其中加入 **加入 Bates 編號** 所需的程式碼。

---

## 第二步：加入必要的 `using` 指令

開啟 `Program.cs`，在檔案頂部加入以下命名空間：

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

* `Aspose.Pdf` 讓您可以使用 `Document` 類別來載入與儲存 PDF。  
* `Aspose.Pdf.Text` 包含 `BatesNumberingOptions`，此物件定義編號的外觀。

---

## 第三步：載入來源 PDF

以下程式碼會載入您要編號的 PDF。請將 `"YOUR_DIRECTORY/source.pdf"` 替換為實際路徑。

```csharp
// Load the source PDF
Document pdf = new Document("YOUR_DIRECTORY/source.pdf");
```

若找不到檔案，Aspose 會拋出 `FileNotFoundException`。為避免此情況，您可以先驗證路徑：

```csharp
if (!System.IO.File.Exists("YOUR_DIRECTORY/source.pdf"))
{
    Console.WriteLine("Source PDF not found.");
    return;
}
```

---

## 第四步：定義 Bates 編號選項

`BatesNumberingOptions` 讓您掌控編號的每一個視覺元素。以下範例示範法律案件檔案的常見設定：

```csharp
// Define Bates numbering options
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",          // Text before the numeric part
    StartNumber = 1000,       // First number to use
    Digits = 6,               // Pad with leading zeros (e.g., 001000)
    Separator = "-",          // Character between prefix, number, and suffix
    Suffix = "-2025"          // Text after the numeric part
};
```

**各屬性說明**

| 屬性 | 目的 |
|------|------|
| `Prefix` | 方便依專案、客戶或案件分組文件。 |
| `StartNumber` | 設定起始計數；當已有編號檔案時特別有用。 |
| `Digits` | 保持統一寬度，便於排序。 |
| `Separator` | 提升可讀性，特別是結合前綴與後綴時。 |
| `Suffix` | 可加入年份、版本或其他尾隨識別碼。 |

您亦可透過 `batesOptions.Position` 與 `batesOptions.Font` 調整位置（上、下、左、右）與字型樣式。大多數情況下，預設的右下角、12 點 Times New Roman 已足夠。

---

## 第五步：將編號套用至每一頁

呼叫 `pdf.BatesNumbering.Add` 會依頁面順序插入編號。

```csharp
// Apply Bates numbering to every page
pdf.BatesNumbering.Add(batesOptions);
```

若只想在部分頁面（例如跳過封面）加入編號，可傳入 `PageCollection`：

```csharp
// Example: skip the first page
pdf.BatesNumbering.Add(batesOptions, pdf.Pages.Skip(1));
```

---

## 第六步：儲存更新後的 PDF

最後，將修改過的文件寫入磁碟。檔名通常會顯示已加入 Bates 編號的事實。

```csharp
// Save the PDF with Bates numbers applied
pdf.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering added successfully.");
```

若輸出資料夾不存在，Aspose 會自動建立。但請確保您具有寫入權限，以免拋出 `UnauthorizedAccessException`。

---

## 完整可執行範例

將所有片段組合起來，即成為您可以直接複製、貼上並執行的完整程式：

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source PDF
        // -------------------------------------------------
        const string inputPath = "YOUR_DIRECTORY/source.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        Document pdf = new Document(inputPath);

        // -------------------------------------------------
        // 2️⃣ Configure Bates numbering
        // -------------------------------------------------
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            Digits = 6,
            Separator = "-",
            Suffix = "-2025"
        };

        // -------------------------------------------------
        // 3️⃣ Apply the numbering to every page
        // -------------------------------------------------
        pdf.BatesNumbering.Add(batesOptions);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";
        pdf.Save(outputPath);
        Console.WriteLine($"Bates numbering added. Saved to {outputPath}");
    }
}
```

**預期輸出**（主控台）：

```
Bates numbering added. Saved to YOUR_DIRECTORY/bates_numbered.pdf
```

開啟 `bates_numbered.pdf`，您會看到每頁顯示類似 `CASE-001000-2025`、`CASE-001001-2025` 等編號，預設位於右下角。

---

## 常見問題 (FAQ)

### 1. 我可以變更編號的位置嗎？
可以。設定 `batesOptions.Position = new Position(10, 10, 10, 10);`，四個數值分別代表距離上、下、左、右邊緣的邊距。Aspose 也提供預設列舉，如 `BatesNumberingPosition.BottomCenter`。

### 2. 若我的 PDF 已有頁碼，會怎樣？
加入 Bates 編號會 **疊加** 在原有頁碼上。若想避免視覺雜亂，可隱藏原始頁碼（若屬於文字層）或調整 `batesOptions` 的字型大小與位置。

### 3. 這能處理加密的 PDF 嗎？
Aspose 能在提供密碼的情況下開啟受保護的 PDF：

```csharp
Document pdf = new Document("source.pdf", new LoadOptions { Password = "mySecret" });
```

之後即可照常套用 Bates 編號。

### 4. 如何使用純數字的 **number pdf pages**（不帶前綴/後綴）？
只要將 `Prefix = string.Empty` 與 `Suffix = string.Empty`：

```csharp
BatesNumberingOptions simple = new BatesNumberingOptions
{
    StartNumber = 1,
    Digits = 4   // 0001, 0002, …
};
pdf.BatesNumbering.Add(simple);
```

### 5. 能否在 ASP.NET Core 中即時產生並傳送 PDF？
絕對可以。載入文件、套用編號後，將串流寫入 HTTP 回應：

```csharp
using (var ms = new MemoryStream())
{
    pdf.Save(ms);
    ms.Position = 0;
    return File(ms, "application/pdf", "bates_numbered.pdf");
}
```

---

## 邊緣情況與最佳實踐

| 情境 | 推薦做法 |
|------|----------|
| **大型 PDF（數百頁）** | 在完成所有頁面層級的轉換後，再呼叫 `pdf.BatesNumbering.Add`，避免重複處理同一頁面。 |
| **自訂字型** | 設定 `batesOptions.Font = FontRepository.FindFont("Arial")`，並調整 `batesOptions.FontSize`，提升掃描文件的可讀性。 |
| **效能關鍵的批次作業** | 在迴圈處理多個檔案時，重複使用同一個 `Document` 實例，處理完畢後釋放以節省記憶體。 |
| **國際字符** | 使用支援 Unicode 的字型（如 `Times New Roman Unicode`），確保前綴或後綴正確顯示。 |
| **版本相容性** | 此程式碼適用於 Aspose.Pdf 23.10 及更新版本。若使用較舊版本，請參考 API 文件確認屬性名稱是否變更。 |

---

## 結論

現在您已掌握如何使用 Aspose.Pdf for .NET 為 PDF 加入 **Bates 編號**。本教學涵蓋載入 PDF、設定 `BatesNumberingOptions`、將編號套用至每頁以及儲存結果。憑藉這些基礎，您也能實作通用的 **pdf 頁碼編號**、自訂格式的 **number pdf pages**，並將此流程整合至更大的自動化管線。

**後續步驟**

* 深入探索 **bates numbering pdf** API，以自訂字型、顏色與位置。  
* 結合 **數位簽章**，打造防篡改的法律文件。  
* 若需先合併多個案件檔案再編號，可參考 Aspose 的 **PDF 合併** 功能。

歡迎嘗試不同的前綴、後綴與位數長度，以符合貴組織的檔案編號標準。祝開發順利！

## 接下來該學什麼？

以下教學與本篇內容密切相關，能進一步擴展您的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能或探索其他實作方式。

- [Create PDF Document C# – Add Bates Numbering Guide](/pdf/english/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/)
- [How to Add Bates Numbering in PDF with C# – Complete Guide](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-c-complete-guide/)
- [Aspose PDF Tutorial – Insert a Blank Page and Update Bates Numbering](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}