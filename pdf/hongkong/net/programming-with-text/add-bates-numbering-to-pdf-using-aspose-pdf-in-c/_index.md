---
category: general
date: 2026-09-27
description: 使用 Aspose.PDF 在 C# 中為 PDF 添加 Bates 編號。了解如何載入 PDF 文件、設定 Bates 編號選項，並儲存更新後的檔案。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- load pdf document
- how to add bates numbering
- Aspose.PDF C#
- PDF Bates numbering example
language: zh-hant
lastmod: 2026-09-27
og_description: 使用 Aspose.PDF 於 C# 為 PDF 加入 Bates 編號。本教學示範如何載入 PDF 文件、設定 Bates 編號，並儲存結果。
og_image_alt: Screenshot of a PDF page displaying Bates numbers in the footer
og_title: 使用 Aspose.PDF 為 PDF 添加 Bates 編號 – C# 指南
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Add bates numbering to PDF using Aspose.PDF in C#. Learn how to load
    a PDF document, set Bates numbering options, and save the updated file.
  headline: Add bates numbering to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF processing
title: 使用 Aspose.PDF 在 C# 中為 PDF 添加 Bates 編號
url: /zh-hant/net/programming-with-text/add-bates-numbering-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中使用 Aspose.PDF 為 PDF 添加 Bates 編號

如果您需要 **為 PDF 檔案添加 Bates 編號**，本指南將為您展示一個完整、可直接執行的解決方案。您將看到如何 **載入 PDF 文件**、設定 Bates 編號選項，並將編號後的檔案寫回磁碟——全部使用 Aspose.PDF for .NET。

在法律、執法及檔案管理工作流程中，套用 Bates 編號是常見需求。完成本教學後，您即可在每一頁嵌入連續的識別碼、客製化前綴，並從任意數字開始計數。

## 您將學會

* 如何將 **PDF 文件** 內容載入 `Aspose.Pdf.Document` 物件。  
* 使用 `BatesNumberingOptions` **添加 Bates 編號** 的完整步驟。  
* 如何在保留原始版面與品質的情況下儲存已修改的檔案。  

不需要任何外部工具——只需 Aspose.PDF NuGet 套件以及 .NET 開發環境（Visual Studio、VS Code 或 Rider）。  

---

## 步驟 1：安裝 Aspose.PDF for .NET

在終端機中開啟您的專案資料夾，執行以下指令：

```bash
dotnet add package Aspose.PDF
```

此套件包含 `Aspose.Pdf` 命名空間，提供本教學中使用的所有類別。安裝完成後，重新載入專案，使 IDE 能偵測到新的參考。

## 步驟 2：載入 PDF 文件

載入來源檔案是第一步，因為 Bates 編號引擎是基於已存在的 `Document` 例項運作。

```csharp
using Aspose.Pdf;

// ...

// Replace with the path to your input PDF
string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Load the PDF document into memory
Document doc = new Document(inputPath);
```

**為何重要：** `Document` 類別會解析 PDF 結構，讓您能存取頁面、註解與中繼資料。若未先載入檔案，就無法套用任何編號。

## 步驟 3：設定 Bates 編號選項

建立 `BatesNumberingOptions` 物件，並設定所需的前綴、起始編號以及其他可選的格式參數。

```csharp
using Aspose.Pdf;

// ...

BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Text that appears before the numeric part
    Prefix = "CASE01",

    // First number to use (1 means the first page gets CASE01-1)
    StartNumber = 1,

    // Optional: customize the appearance
    // The default places the number in the footer, centered.
    // You can change Font, FontSize, Color, and Position if needed.
    // Example:
    // Font = FontRepository.FindFont("Arial"),
    // FontSize = 10,
    // Color = Color.Black,
    // Margin = new Margin(0, 0, 0, 20)
};
```

**為何重要：** `BatesNumberingOptions` 告訴 Aspose.PDF 如何為每頁產生標籤。`Prefix` 可協助您將相關案件分組，而 `StartNumber` 則允許您從先前批次的編號繼續。

## 步驟 4：儲存套用 Bates 編號的 PDF

將選項物件傳遞給 `Save` 方法。Aspose.PDF 會直接在每頁寫入編號。

```csharp
// Replace with the desired output path
string outputPath = @"YOUR_DIRECTORY\output.pdf";

// Save the document, applying the Bates numbering
doc.Save(outputPath, batesOptions);
```

**為何重要：** 重載的 `Save(string, BatesNumberingOptions)` 同時執行渲染與編號程序，確保輸出檔案中包含可見的識別碼。

## 完整範例 – 整合所有步驟

以下是一個完整、獨立的程式，您可以直接複製、貼上並執行。它示範了 **如何從頭到尾添加 Bates 編號**。

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the PDF document
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Set up Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                Prefix = "CASE01",
                StartNumber = 1,
                // Optional appearance tweaks:
                // Font = FontRepository.FindFont("Times New Roman"),
                // FontSize = 9,
                // Color = Color.DarkBlue,
                // Margin = new Margin(0, 0, 0, 15)
            };

            // 3️⃣ Save the document with Bates numbers
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath, batesOptions);

            Console.WriteLine($"Bates numbering added. Output saved to: {outputPath}");
        }
    }
}
```

### 預期輸出

執行程式後會產生 `output.pdf`，每一頁都會顯示類似以下的標籤：

```
CASE01-1
CASE01-2
CASE01-3
...
```

編號預設顯示在頁腳，您也可以透過調整 `BatesNumberingOptions` 中的 `Margin` 屬性來變更位置。

## 邊緣情況與常見變化

| 情況 | 調整方式 |
|-----------|----------------|
| **每批次不同的前綴** | 在呼叫 `Save` 前變更 `Prefix`。您可以針對多個文件以不同前綴進行迴圈處理。 |
| **從先前檔案繼續編號** | 將 `StartNumber` 設為上一次使用的編號 + 1。 |
| **將編號放置於頁首** | 使用 `batesOptions.Margin = new Margin(20, 0, 0, 0);`（上邊距）或自訂 `batesOptions.Position`。 |
| **自訂字型或顏色** | 如註解區段所示，設定 `Font`、`FontSize` 與 `Color` 屬性。 |
| **大型 PDF（1000 頁以上）** | 此操作具備記憶體效能；但您可能想在儲存前啟用 `doc.OptimizeResources()` 以減少檔案大小。 |

**小技巧：** 若您的工作流程需要針對每個文件使用不同的編號規則，請將邏輯封裝於輔助方法中：

```csharp
static void ApplyBatesNumbering(string src, string dst, string prefix, int start)
{
    var doc = new Document(src);
    var opts = new BatesNumberingOptions { Prefix = prefix, StartNumber = start };
    doc.Save(dst, opts);
}
```

## 結論

您現在已了解 **如何使用 Aspose.PDF 在 C# 中為任意 PDF 添加 Bates 編號**。本教學涵蓋了載入 PDF 文件、設定編號選項以及儲存最終檔案——全部於一個可執行的程式中完成。

接下來，您可以探索相關主題，例如 **添加浮水印**、**合併多個 PDF**，或使用 Aspose.PDF **擷取文字**。嘗試不同的字型、顏色與位置，以符合貴組織的格式標準。

準備好自動化您的法律文件工作流程了嗎？將程式碼加入建置管線，對批次檔案執行，即可讓 Aspose.PDF 處理繁重工作。祝開發愉快！

## 接下來您可以學習什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上延伸。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索其他實作方式。

- [建立 PDF 文件 C# – 添加 Bates 編號](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/)
- [添加 Bates 編號 PDF – 步驟說明指南：為 PDF 頁面編號](/pdf/english/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/)
- [Aspose PDF 教學 – 插入空白頁並更新 Bates 編號](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}