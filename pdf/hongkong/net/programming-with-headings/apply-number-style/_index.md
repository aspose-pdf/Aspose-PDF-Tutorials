---
"description": "透過本逐步指南了解如何使用 Aspose.PDF for .NET 將不同的數字樣式（羅馬數字、信件）套用至 PDF 中的標題。"
"linktitle": "在 PDF 檔案中套用數字樣式"
"second_title": "Aspose.PDF for .NET API參考"
"title": "在 PDF 檔案中套用數字樣式"
"url": "/zh-hant/net/programming-with-headings/apply-number-style/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 檔案中套用數字樣式

## 介紹

您是否曾發現自己需要在 PDF 文件中添加編號精美的清單？無論您要格式化法律文件、報告還是演示文稿，正確的編號樣式對於組織資訊至關重要。使用 Aspose.PDF for .NET，您可以將各種編號樣式套用至 PDF 檔案的標題，從而建立結構良好且專業的文件。 

## 先決條件

在深入編碼之前，讓我們先了解您需要什麼：

1. Aspose.PDF for .NET：從以下位置下載最新版本的 Aspose.PDF [這裡](https://releases。aspose.com/pdf/net/).
2. 開發環境：確保您有 Visual Studio 或任何其他與 .NET 相容的 IDE。
3. .NET Framework：確保您已安裝 .NET Framework 4.0 或更高版本。
4. 許可證：您可以使用臨時許可證 [這裡](https://purchase.aspose.com/temporary-license/) 或探索 [免費試用](https://releases.aspose.com/) 選項。

## 導入包

首先，請確保已在專案中匯入以下命名空間：

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

## 步驟1：設定文檔

讓我們先建立一個新的 PDF 文件並配置其頁面設定。我們將設定頁面大小和邊距來控制內容的佈局。

說明：在此步驟中，我們將設定 PDF 的基本結構，包括定義頁面大小、高度和邊距以實現一致的格式。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document pdfDoc = new Document();

// 設定頁面尺寸和邊距
pdfDoc.PageInfo.Width = 612.0;
pdfDoc.PageInfo.Height = 792.0;
pdfDoc.PageInfo.Margin = new Aspose.Pdf.MarginInfo();
pdfDoc.PageInfo.Margin.Left = 72;
pdfDoc.PageInfo.Margin.Right = 72;
pdfDoc.PageInfo.Margin.Top = 72;
pdfDoc.PageInfo.Margin.Bottom = 72;
```

這樣做之後，您的文件將具有標準頁面大小，相當於 8.5 x 11 英吋的頁面，並且四周的邊距為 72 點（或 1 英吋）。

## 步驟 2：在 PDF 中新增頁面

接下來，我們將在 PDF 文件中新增一個新頁面，稍後我們將在其中套用編號樣式。

說明：每個 PDF 都需要頁面！此步驟為 PDF 新增空白頁並設定其邊距以符合文件層級設定。

```csharp
// 為 PDF 文件新增頁面
Aspose.Pdf.Page pdfPage = pdfDoc.Pages.Add();
pdfPage.PageInfo.Width = 612.0;
pdfPage.PageInfo.Height = 792.0;
pdfPage.PageInfo.Margin = new Aspose.Pdf.MarginInfo();
pdfPage.PageInfo.Margin.Left = 72;
pdfPage.PageInfo.Margin.Right = 72;
pdfPage.PageInfo.Margin.Top = 72;
pdfPage.PageInfo.Margin.Bottom = 72;
```

## 步驟3：建立浮動框

FloatingBox 可讓您將內容（如文字或標題）放置在與頁面流程無關的方塊內。當您想要完全控制內容的佈局時這很有用。

說明：在這裡，我們設定一個 FloatingBox 來包含將套用數字樣式的標題。

```csharp
// 為結構化內容創建 FloatingBox
Aspose.Pdf.FloatingBox floatBox = new Aspose.Pdf.FloatingBox();
floatBox.Margin = pdfPage.PageInfo.Margin;
pdfPage.Paragraphs.Add(floatBox);
```

## 步驟 4：新增第一個帶有羅馬數字的標題

現在到了令人興奮的部分！讓我們加入第一個帶有小寫羅馬數字編號的標題。

說明：我們將 NumberingStyle.NumeralsRomanLowercase 樣式應用於標題，它將以羅馬數字顯示編號（i、ii、iii 等）。

```csharp
// 使用羅馬數字創建第一個標題
Aspose.Pdf.Heading heading = new Aspose.Pdf.Heading(1);
heading.IsInList = true;
heading.StartNumber = 1;
heading.Text = "List 1";
heading.Style = NumberingStyle.NumeralsRomanLowercase;
heading.IsAutoSequence = true;
floatBox.Paragraphs.Add(heading);
```

## 步驟 5：新增第二個羅馬數字標題

為了演示目的，讓我們添加第二個羅馬數字標題，但這次我們將從 13 開始。

說明：StartNumber 屬性可讓您從自訂數字開始編號 - 在本例中，我們從 13 開始。

```csharp
// 從羅馬數字 13 開始創建第二個標題
Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
heading2.IsInList = true;
heading2.StartNumber = 13;
heading2.Text = "List 2";
heading2.Style = NumberingStyle.NumeralsRomanLowercase;
heading2.IsAutoSequence = true;
floatBox.Paragraphs.Add(heading2);
```

## 步驟 6：新增按字母順序編號的標題

為了多樣化，讓我們添加第三個標題，但這次我們將使用小寫字母編號（a、b、c 等）。

說明：將 NumberingStyle 更改為 LettersLowercase 允許我們將字母編號應用於標題。

```csharp
// 建立按字母順序編號的標題
Aspose.Pdf.Heading heading3 = new Aspose.Pdf.Heading(2);
heading3.IsInList = true;
heading3.StartNumber = 1;
heading3.Text = "the value, as of the effective date of the plan, of property to be distributed under the plan on account of each allowed";
heading3.Style = NumberingStyle.LettersLowercase;
heading3.IsAutoSequence = true;
floatBox.Paragraphs.Add(heading3);
```

## 步驟 7：儲存 PDF

最後，套用所有標題和數字樣式後，將 PDF 檔案儲存到您想要的目錄中。

說明：此步驟儲存包含所有格式化標題和套用的編號樣式的 PDF 檔案。

```csharp
// 儲存 PDF 文件
dataDir = dataDir + "ApplyNumberStyle_out.pdf";
pdfDoc.Save(dataDir);
Console.WriteLine("\nNumber style applied successfully in headings.\nFile saved at " + dataDir);
```

## 結論

就是這樣！您已成功使用 Aspose.PDF for .NET 將編號樣式（羅馬數字和信件）套用至 PDF 檔案中的標題。 Aspose.PDF 提供的控制頁面佈局、編號樣式和內容定位的靈活性為您提供了一套強大的工具集，可用於建立組織良好、專業的 PDF 文件。

## 常見問題解答

### 我可以對同一個 PDF 文件套用不同的數位樣式嗎？  
是的，Aspose.PDF for .NET 可讓您在相同文件中混合使用不同的編號樣式，例如羅馬數字、阿拉伯數字和字母編號。

### 如何自訂標題的起始數字？  
您可以使用 `StartNumber` 財產。

### 有沒有辦法重置編號順序？  
是的，您可以透過調整 `StartNumber` 每個標題的屬性。

### 除了編號之外，我還可以對標題套用粗體或斜體樣式嗎？  
絕對地！您可以透過修改字體、大小、粗體和斜體等屬性來自訂標題樣式，使用 `TextState` 目的。

### 如何取得 Aspose.PDF 的臨時授權？  
您可以從 [這裡](https://purchase.aspose.com/temporary-license/) 不受限制地測試 Aspose.PDF。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}