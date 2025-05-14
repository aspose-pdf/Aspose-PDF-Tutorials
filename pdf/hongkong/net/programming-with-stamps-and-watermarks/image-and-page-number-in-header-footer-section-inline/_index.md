---
"description": "透過本逐步指南了解如何使用 Aspose.PDF for .NET 在 PDF 的頁首部分內嵌新增圖像和頁碼。"
"linktitle": "頁眉頁腳部分內嵌中的圖像和頁碼"
"second_title": "Aspose.PDF for .NET API參考"
"title": "頁眉頁腳部分內嵌中的圖像和頁碼"
"url": "/zh-hant/net/programming-with-stamps-and-watermarks/image-and-page-number-in-header-footer-section-inline/"
"weight": 120
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 頁眉頁腳部分內嵌中的圖像和頁碼

## 介紹

Aspose.PDF for .NET 是一個功能強大的工具，它提供了處理和產生 PDF 檔案的廣泛功能。無論您需要新增圖像、自訂頁首和頁尾或管理文本，Aspose.PDF 都能滿足您的需求。在本教學中，我們將探討如何在 PDF 文件的頁首或頁尾中內嵌添加圖像和頁碼。讓我們深入研究並逐步分解該過程。

## 先決條件

在我們進入程式碼之前，讓我們確保您已準備好一切以便繼續操作：

- Aspose.PDF for .NET：從下載最新版本 [Aspose PDF下載頁面](https://releases。aspose.com/pdf/net/).
- 開發環境：您需要一個 C# IDE，例如 Visual Studio。
- 許可證：如果您還沒有許可證，您可以申請 [此處為臨時駕照](https://purchase.aspose.com/temporary-license/) 或者從 [Aspose 商店](https://purchase。aspose.com/buy).

現在您已經準備好了先決條件，讓我們開始吧。

## 導入包

在開始編碼之前，請確保導入必要的命名空間：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

這些軟體包可讓您處理 PDF 文件和文字操作。

## 步驟 1：設定文檔目錄

我們需要做的第一件事是定義保存 PDF 檔案的目錄的路徑。此路徑可以自訂為您的專案資料夾或機器上的任何位置。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

此變數保存了文件的儲存位置。代替 `"YOUR DOCUMENT DIRECTORY"` 與實際路徑。

## 步驟2：實例化PDF文檔

在此步驟中，我們建立一個新的實例 `Aspose.Pdf.Document` 目的。該物件將作為 PDF 文件的骨幹。

```csharp
// 透過呼叫其空建構函數來實例化 Document 對象
Aspose.Pdf.Document pdf1 = new Aspose.Pdf.Document();
```

在這裡，我們創建一個空白的 PDF 文件，稍後我們可以在其中填充內容。

## 步驟 3：在 PDF 中新增頁面

您的 PDF 至少需要一頁來新增頁首、頁尾和內容。讓我們在文件中新增一個空白頁。

```csharp
// 在 Pdf 物件中建立一個頁面
Aspose.Pdf.Page page = pdf1.Pages.Add();
```

透過調用 `pdf1.Pages.Add()`，新的頁面將被添加到文件中，可供自訂頁首和頁尾。

## 步驟 4：建立並設定標題

現在是時候建立文件的標題了。我們將在這裡添加文字、圖像和頁碼。

```csharp
// 建立文件的頁首部分
Aspose.Pdf.HeaderFooter header = new Aspose.Pdf.HeaderFooter();
// 設定 PDF 文件的頁眉
page.Header = header;
```

我們創建了一個 `HeaderFooter` 對象並將其分配給 `Header` 頁面的屬性，確保我們新增到頁首的任何內容都會出現在頁面的頂部。

## 步驟 5：在頁首新增內聯文本

新增文字就像創建 `TextFragment` 並指定其屬性。讓我們在標題中添加一些彩色文字。

```csharp
// 建立文字對象
Aspose.Pdf.Text.TextFragment txt1 = new Aspose.Pdf.Text.TextFragment("Aspose.Pdf is a Robust component by");
// 指定顏色
txt1.TextState.ForegroundColor = Color.Blue;
txt1.IsInLineParagraph = true;
```

在此步驟中，我們建立一個 `TextFragment` 內容為“Aspose.Pdf is a Robust component by”，並將其顏色設為藍色。這 `IsInLineParagraph` 屬性確保文字是內聯的，這意味著它將與其他元素（如圖像和附加文字）出現在同一行上。

## 步驟 6：在頁首中插入內嵌影像

為了使標題更具視覺吸引力，您可以添加與文字同框的圖像。這可以是您的公司徽標或任何其他圖形。

```csharp
// 在部分中建立圖像對象
Aspose.Pdf.Image image1 = new Aspose.Pdf.Image();
// 設定圖片檔案路徑
image1.File = dataDir + "aspose-logo.jpg";
// 設定圖片寬度資訊
image1.FixWidth = 50;
image1.FixHeight = 20;
// 表示 seg1 的 InlineParagraph 是一張圖片。
image1.IsInLineParagraph = true;
```

在這裡，我們透過創建 `Image` 對象，設定其路徑，並調整寬度和高度。這 `IsInLineParagraph` 確保圖像與文字對齊。

## 步驟 7：新增其他內嵌文字以完成頁眉

讓我們添加一些文字來完成內聯標題。

```csharp
Aspose.Pdf.Text.TextFragment txt2 = new Aspose.Pdf.Text.TextFragment(" Pty Ltd.");
txt2.IsInLineParagraph = true;
txt2.TextState.ForegroundColor = Color.Maroon;
header.Paragraphs.Add(txt1);
header.Paragraphs.Add(image1);
header.Paragraphs.Add(txt2);
```

在這一部分中，我們創建另一個 `TextFragment` 內容為“Pty Ltd.”並將其顏色設為栗色。文字片段和圖像均新增至頁首。

## 步驟 8：儲存 PDF

設定好頁首後，就可以儲存 PDF 了。

```csharp
// 儲存 PDF
pdf1.Save(dataDir + "ImageAndPageNumberInHeaderFooter_UsingInlineParagraph_out.pdf");
```

這 `Save` 方法將最終的PDF文件寫入指定位置。

## 結論

恭喜！您已成功使用 Aspose.PDF for .NET 將圖像和文字新增至 PDF 文件的標題。本教學將引導您完成基本步驟，包括建立文件、新增頁面、插入頁首以及放置文字和圖像等內嵌內容。 Aspose.PDF 為您提供了令人難以置信的靈活性來管理您的 PDF，無論是操作頁首、頁尾還是複雜內容。 

## 常見問題解答

### 我可以在頁眉中加入頁碼嗎？
是的！您可以使用 `TextFragment` 類別並根據需要對其進行格式化。只需將其作為內聯內容插入到標題部分即可。

### 如何在頁眉中設定背景圖像？
您可以使用 `BackgroundImage` 的財產 `HeaderFooter` 類別來設定背景圖像。但是，這不是內聯內容，它將覆蓋整個標題區域。

### 除了 JPEG 之外，是否可以使用其他影像格式？
絕對地！ Aspose.PDF 支援各種圖片格式，如 PNG、BMP 和 GIF。

### 我可以自訂頁首文字的字體嗎？
是的，您可以使用 `TextState` 物件來更改文字的字體、大小和樣式。

### 我需要許可證才能使用 Aspose.PDF for .NET 嗎？
是的，Aspose.PDF 需要生產使用許可證，但你可以從 [點此免費試用](https://releases。aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}