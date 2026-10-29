---
category: general
date: 2026-08-04
description: 在 C# 中建立新 PDF 文件，並使用 Aspose.Pdf 快速加入 Bates 編號 – 學習如何加入空白頁及自訂頁碼。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new pdf document
- add bates numbering pdf
- how to add bates
- add blank page pdf
- add custom page numbers
language: zh-hant
lastmod: 2026-08-04
og_description: 在 C# 中建立新 PDF 文件，並自動為法律案件管理加入 Bates 編號 – 附完整程式碼範例。
og_image_alt: Screenshot of a C# program creating a PDF document with Bates numbers
  applied
og_title: 在 C# 中建立帶有 Bates 編號的新 PDF 文件
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create new PDF document in C# and add Bates numbering pdf quickly using
    Aspose.Pdf – learn to add blank page pdf and custom page numbers.
  headline: Create new PDF document with Bates numbering in C#
  type: TechArticle
tags:
- C#
- PDF
- Aspose.Pdf
- Bates numbering
title: 在 C# 中建立帶有 Bates 編號的新 PDF 文件
url: /zh-hant/net/document-creation/create-new-pdf-document-with-bates-numbering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中建立帶 Bates 編號的 PDF 文件

如果你需要在 C# 中 **建立新 PDF 文件**，本指南將示範如何使用 Aspose.Pdf **加入 Bates 編號**。你將學會 **新增空白頁 PDF**、設定 **自訂頁碼**，並儲存最終檔案。

本教學涵蓋從安裝函式庫到產生符合法律案件檔案標準的 PDF 的每一步。完成後，你即可產生 PDF、插入空白頁、套用 Bates 編號，並自訂編號格式——全部只需一個可執行的程式。

## 前置條件

* .NET 6.0 SDK 或更新版本已安裝  
* Visual Studio 2022（或任何 C# IDE）  
* 有效的 Aspose.Pdf for .NET 授權或免費評估金鑰  

你不需要額外的 NuGet 套件；本教學會自動安裝所有必要的元件。

## 第一步：透過 NuGet 安裝 Aspose.Pdf

在專案資料夾中開啟終端機並執行以下指令：

```bash
dotnet add package Aspose.Pdf
```

此指令會將最新的穩定版 Aspose.Pdf 加入你的專案，提供 `Document`、`BatesNumbering` 以及其他 PDF 操作類別供你使用。

## 第二步：建立新 PDF 文件 – 初始設定

建立 PDF 檔案是之後所有操作的基礎。`Document` 類別代表整個 PDF 容器。

```csharp
using Aspose.Pdf;

// Step 2: Create a new PDF document
using var doc = new Document();
```

*為什麼這很重要*：實例化 `Document` 會配置頁面、字型與圖形所需的內部結構。使用 `using var` 可確保檔案在儲存後正確釋放。

## 第三步：新增空白頁 PDF

PDF 必須至少有一頁才能放置內容。新增空白頁可為 Bates 編號提供乾淨的畫布。

```csharp
// Step 3: Add a blank page to the document
Page page = doc.Pages.Add();
```

`Pages.Add()` 方法會在文件的頁面集合末端加入一個新的空白頁。如果之後需要在多頁上 **新增自訂頁碼**，可重複呼叫此方法。

## 第四步：設定 Bates 編號 – 如何加入 Bates

Bates 編號是一種常用於法律文件的連續識別碼。你可透過 `BatesNumbering` 類別進行設定。

```csharp
// Step 4: Set up Bates numbering options
var bates = new BatesNumbering
{
    StartNumber = 1000,      // Starting number for the sequence
    Prefix = "CaseA-",       // Text to prepend to each number
    Increment = 1,           // Increment between consecutive numbers
    // Optional: Set the location, font size, etc.
};
```

*為什麼這很重要*：`StartNumber` 定義起始編號，`Prefix` 加上可讀的前綴，`Increment` 控制遞增幅度。你亦可調整 `HorizontalAlignment`、`VerticalAlignment`、`FontSize` 與 `Margins`，以控制每頁編號的顯示方式。

## 第五步：將 Bates 編號套用至頁面

現在編號選項已設定完畢，將它們套用至頁面（或整份文件）。

```csharp
// Step 5: Apply the Bates numbering to the page
bates.Apply(page);
```

呼叫 `Apply` 會預設將格式化的編號插入頁面的頁腳。若需將編號放置於其他位置，請在呼叫 `Apply` 前設定 `bates.Position`。

## 第六步：儲存套用 Bates 編號的 PDF

最後，將記憶體中的文件寫入磁碟。

```csharp
// Step 6: Save the PDF with Bates numbers applied
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumbered.pdf");

doc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

儲存後的檔案會在底部顯示 **CaseA-1000** 的 Bates 編號（僅一頁）。使用任何 PDF 檢視器開啟即可驗證編號。

## 預期輸出

開啟 `BatesNumbered.pdf` 時，你應該會看到：

* 一個空白頁（若你新增了其他頁面則會更多）  
* 文字 **CaseA-1000** 位於頁面底部（預設位置）  

若你新增更多頁面且重複使用相同的 `BatesNumbering` 實例，編號會自動遞增（CaseA-1001、CaseA-1002，…）。

## 專業提示：在 Bates 編號之外加入自訂頁碼

有時你需要同時保留 Bates 編號與傳統頁碼。可在套用 Bates 編號後加入 `TextFragment` 來結合兩者：

```csharp
// Add a traditional page number in the header
var pageNumber = new TextFragment($"Page {page.Number}")
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Top,
    FontSize = 12,
    Font = FontRepository.FindFont("Arial")
};
page.Paragraphs.Add(pageNumber);
```

此程式碼片段示範了在保留 Bates 標籤的同時 **新增自訂頁碼**。

## 邊緣案例：將 Bates 編號套用至多頁

若文件包含多個頁面，你可以在迴圈中將相同的 `BatesNumbering` 實例套用至每一頁：

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    bates.Apply(doc.Pages[i]);
}
```

此迴圈會確保每頁皆依你設定的 `StartNumber` 與 `Increment` 取得連續編號。

## 常見陷阱與避免方法

| 問題 | 發生原因 | 解決方式 |
|------|----------|----------|
| 編號顯示偏離中心 | 預設對齊方式可能不符合你的版面配置 | 明確設定 `bates.HorizontalAlignment` 與 `bates.VerticalAlignment` |
| 編號與現有內容重疊 | 未定義邊距 | 調整 `bates.Margin` 或使用 `bates.Position` 移動編號 |
| 執行時出現授權例外 | 評估版限制輸出 | 在建立文件前套用有效的 Aspose.Pdf 授權 (`License license = new License(); license.SetLicense("Aspose.Pdf.lic");`) |

## 完整範例程式

以下是一個可直接複製、貼上並執行的完整程式範例。



## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，進一步延伸所示技巧。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在專案中探索其他實作方式。

- [如何使用 Aspose.PDF for .NET 在 PDF 中新增與自訂頁碼 | 文件操作指南](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF .NET：使用 FloatingBox 為 PDF 新增頁碼](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [使用 Aspose.PDF 建立 PDF 文件 – 新增頁面、圖形與儲存](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}