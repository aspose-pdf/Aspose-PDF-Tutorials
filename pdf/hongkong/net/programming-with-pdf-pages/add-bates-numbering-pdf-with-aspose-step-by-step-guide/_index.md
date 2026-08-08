---
category: general
date: 2026-08-08
description: 使用 Aspose.Pdf 在 C# 中為 PDF 添加 Bates 編號。本教程亦示範如何新增空白頁 PDF 以及以程式方式產生 PDF。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering pdf
- add blank page pdf
- generate pdf programmatically
- create pdf aspose
language: zh-hant
lastmod: 2026-08-08
og_description: 使用 Aspose.Pdf 在 C# 中為 PDF 添加 Bates 編號。學習如何添加空白頁 PDF、以程式方式生成 PDF，並在幾分鐘內儲存最終文件。
og_image_alt: Screenshot of C# code adding Bates numbering and a blank page to a PDF
  using Aspose.Pdf
og_title: 使用 Aspose 為 PDF 添加 Bates 編號 – 完整 C# 教學
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  headline: Add bates numbering pdf with Aspose – step‑by‑step guide
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  name: Add bates numbering pdf with Aspose – step‑by‑step guide
  steps:
  - name: What if I need a different font or position?
    text: 'The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`,
      `HorizontalAlignment`, and `VerticalAlignment`. For example:'
  - name: How do I exclude a specific page from numbering?
    text: Create a separate `BatesNumberingArtifact` for the pages you want to number
      and add it only to those pages. Pages without an attached artifact will remain
      unnumbered.
  - name: Does this work with existing PDFs?
    text: 'Yes. Instead of `new Document()`, load an existing file:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF generation
- Bates numbering
title: 使用 Aspose 為 PDF 添加 Bates 編號 – 步驟教學
url: /zh-hant/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose 為 PDF 添加 bates 編號 – 步驟指南

使用 Aspose.Pdf 為 PDF 添加 bates 編號一旦了解核心步驟就相當簡單。如果您還需要添加空白頁 PDF 或以程式方式產生 PDF，本指南將涵蓋所有需求。

在本教學中，您將會：

* 從頭建立新的 PDF 文件。  
* 新增一個將容納 Bates 編號的空白頁 PDF。  
* 使用自訂前綴設定 Bates 編號工件。  
* 儲存 PDF，使編號顯示在產生的檔案上。  

完成後，您將擁有一個完整的 C# 主控台應用程式，能產生包含 Bates 編號（如 **CASE‑1000**、**CASE‑1001** …）的 PDF——這是法律與電子發現工作流程的常見需求。

## 前置條件

* .NET 6.0 SDK 或更新版本（程式碼亦可於 .NET Framework 4.8 上執行）。  
* Visual Studio 2022 或任何相容 C# 的 IDE。  
* 有效的 Aspose.Pdf for .NET 授權（或免費評估金鑰）。  
* 具備基本的 C# 語法知識。

> **專業提示：** 若在未授權的情況下執行程式碼，Aspose 會在輸出 PDF 上加上小型浮水印。

## 步驟 1：設定專案並匯入 Aspose.Pdf

建立新的主控台專案，並加入 Aspose.Pdf NuGet 套件：

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

範例所需的 `using` 指示如下：

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
```

這些命名空間讓您能存取稍後會使用的 `Document`、`Page` 與 `BatesNumberingArtifact` 類別。

## 步驟 2：新增空白頁 PDF

Bates 編號必須附加於頁面上，因此我們先建立一個將接收編號工件的空白頁。

```csharp
// Step 2: Add a blank page pdf
Document pdfDocument = new Document();          // creates an empty PDF
Page pdfPage = pdfDocument.Pages.Add();         // adds the first (blank) page
```

`Document` 類別代表整個 PDF 檔案，而 `Pages.Add()` 會在文件的頁面集合末端插入一個新的空白頁。由於文件起始為空，此呼叫同時會建立第一頁。

## 步驟 3：設定 Bates 編號工件

現在我們定義 Bates 編號的外觀。`BatesNumberingArtifact` 允許您設定起始編號、前綴、後綴以及格式化選項。

```csharp
// Step 3: Define Bates numbering settings
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
{
    StartNumber = 1000,          // first number in the sequence
    Prefix = "CASE-",            // custom prefix before each number
    // Optional: you can also set Suffix, FontSize, FontColor, etc.
};
```

**為何這很重要：**  
將 `StartNumber` 設為 **1000** 符合一般法律案件檔案的慣例。`Prefix` 確保每個編號顯示為 **CASE‑1000**、**CASE‑1001** …，便於搜尋與排序。

## 步驟 4：將工件附加至頁面

必須將工件加入頁面的 `Artifacts` 集合，讓 Aspose 在儲存時於每一頁渲染它。

```csharp
// Step 4: Attach the Bates numbering artifact to the PDF page
pdfPage.Artifacts.Add(batesArtifact);
```

當文件儲存時，Aspose 會自動在所有頁面重複此工件，並為每一後續頁面遞增編號。

## 步驟 5：（可選）新增其他頁面

若需要更多頁面，只需重複呼叫 `pdfDocument.Pages.Add()`。先前步驟中附加的 Bates 編號工件會自動出現在每個新頁面上。

```csharp
// Example: add two more pages
pdfDocument.Pages.Add();
pdfDocument.Pages.Add();
```

## 步驟 6：儲存 PDF – 以程式方式產生 PDF

最後，將文件寫入磁碟。此時 Bates 編號會被渲染至各頁面上。

```csharp
// Step 6: Save the PDF – generate pdf programmatically
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumberedDocument.pdf");

// Ensure the directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);

pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to: {outputPath}");
```

**預期結果：**  
開啟 *BatesNumberedDocument.pdf*，您會看到一個三頁的 PDF。每頁在右下角顯示 Bates 編號：

* 第 1 頁 → **CASE‑1000**  
* 第 2 頁 → **CASE‑1001**  
* 第 3 頁 → **CASE‑1002**

由於工件已附加於頁面集合，編號會自動遞增。

## 完整、可執行範例

將上述所有步驟整合起來，以下是一個完整的主控台程式，您可以直接複製、貼上並執行：

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new PDF document
            Document pdfDocument = new Document();

            // Add a blank page pdf
            Page pdfPage = pdfDocument.Pages.Add();

            // Define Bates numbering settings (add bates numbering pdf)
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
            {
                StartNumber = 1000,
                Prefix = "CASE-"
            };

            // Attach the artifact to the page
            pdfPage.Artifacts.Add(batesArtifact);

            // (Optional) add more pages to see incremented numbers
            pdfDocument.Pages.Add(); // page 2
            pdfDocument.Pages.Add(); // page 3

            // Save the PDF – generate pdf programmatically
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "BatesNumberedDocument.pdf");

            Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);
            pdfDocument.Save(outputPath);

            Console.WriteLine($"PDF saved to: {outputPath}");
        }
    }
}
```

使用 `dotnet run` 執行程式。執行完畢後，於桌面找到檔案並驗證 Bates 編號。

![Add bates numbering pdf example](/images/bates-numbering.png "Add bates numbering pdf example")

## 常見問題與邊緣案例

### 如果需要不同的字型或位置該怎麼辦？

`BatesNumberingArtifact` 提供 `FontSize`、`FontColor`、`HorizontalAlignment`、`VerticalAlignment` 等屬性。例如：

```csharp
batesArtifact.FontSize = 12;
batesArtifact.FontColor = Color.Blue;
batesArtifact.HorizontalAlignment = HorizontalAlignment.Left;
batesArtifact.VerticalAlignment = VerticalAlignment.Top;
```

### 如何排除特定頁面不編號？

為您想編號的頁面建立單獨的 `BatesNumberingArtifact`，僅將其加入那些頁面。未附加工件的頁面將保持不編號。

### 這能套用於已有的 PDF 嗎？

可以。將 `new Document()` 改為載入現有檔案：

```csharp
Document pdfDocument = new Document("input.pdf");
```

然後將工件附加至目標頁面並儲存。

## 結論

您現在已了解如何使用 Aspose.Pdf **為 PDF 添加 bates 編號**、如何 **新增空白頁 PDF**，以及如何在乾淨、可重用的 C# 解決方案中 **以程式方式產生 PDF**。此方法支援任意頁數、自訂前綴與樣式選項，讓您完整掌控最終文件。

接下來您可以探索以下步驟：

* Use **create pdf as

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上延伸。每個資源皆提供完整可執行的程式碼範例與步驟說明，協助您精通其他 API 功能，並在專案中探索替代實作方式。

- [如何使用 Aspose.PDF for .NET 為 PDF 添加與自訂頁碼 | 文件操作指南](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [如何使用 Aspose.PDF for .NET 在 PDF 結尾添加空白頁 | 步驟指南](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)
- [使用 Aspose.PDF 建立 PDF 文件 – 添加頁面、圖形與儲存](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}