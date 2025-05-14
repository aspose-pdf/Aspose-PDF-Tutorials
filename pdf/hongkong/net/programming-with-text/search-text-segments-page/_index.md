---
"description": "透過本詳細的逐步指南了解如何使用 Aspose.PDF for .NET 搜尋 PDF 檔案中的文字段。提取文字、分析片段等等。"
"linktitle": "在 PDF 檔案中搜尋文字片段頁面"
"second_title": "Aspose.PDF for .NET API參考"
"title": "在 PDF 檔案中搜尋文字片段頁面"
"url": "/zh-hant/net/programming-with-text/search-text-segments-page/"
"weight": 470
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 檔案中搜尋文字片段頁面

## 介紹

有沒有想過如何使用 Aspose.PDF for .NET 在 PDF 文件中定位特定的文字區段？嗯，你很幸運！在本指南中，我們將以簡單的逐步形式引導您完成整個過程。無論您是想提取資訊、分析文本，還是僅瀏覽複雜的 PDF 操作，Aspose.PDF for .NET 都能滿足您的需求。讓我們開始吧！

## 先決條件

在我們開始之前，讓我們確保您已準備好所需的一切：

- Aspose.PDF for .NET：請確定您已安裝程式庫。您可以從 [這裡](https://releases。aspose.com/pdf/net/).
- .NET Framework：確保您的機器上安裝了 .NET。
- 開發環境：建議使用 Visual Studio 或任何支援 .NET 的 IDE。
- PDF 文件：您將在其中搜尋文字片段的 PDF 文件。

如果您還沒有 Aspose.PDF for .NET，請別擔心！您可以從 [這裡](https://releases.aspose.com/) 或購買 [這裡](https://purchase。aspose.com/buy).

## 導入包

在我們開始編碼之前，將必要的套件匯入到您的專案中至關重要。這確保所有必需的類別和方法都可用於您的 PDF 操作任務。

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

了解了基本知識後，讓我們直接進入逐步指南。


## 步驟 1：載入 PDF 文檔

過程的第一步是將您的 PDF 檔案載入到程式中。如果沒有載入文檔，就沒有什麼可搜尋的，對嗎？以下是操作方法。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";
// 開啟文件
Document pdfDocument = new Document(dataDir + "SearchTextSegmentsPage.pdf");
```

- `dataDir`：此變數保存您的 PDF 檔案的路徑。代替 `"YOUR DOCUMENT DIRECTORY"` 與儲存檔案的實際目錄。
- `pdfDocument`：使用 `Document` 類，我們將 PDF 載入到記憶體中。

## 第 2 步：設定文字搜尋

現在您的文件已加載，下一步是建立一個 `TextFragmentAbsorber` 對象，它允許我們在文件中搜尋特定文字。

```csharp
// 建立 TextAbsorber 物件來尋找輸入搜尋短語的所有實例
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("text");
```

- `TextFragmentAbsorber`：此物件用於捕獲您正在搜尋的文字的所有出現情況。代替 `"text"` 使用您想要搜尋的實際文字。

## 步驟 3：接受特定頁面的吸收器

您可能不會總是想搜尋整個 PDF 文件。在這個例子中，我們將其縮小到特定的頁面。

```csharp
// 接受所有頁面的吸收器
pdfDocument.Pages[2].Accept(textFragmentAbsorber);
```

- `pdfDocument.Pages[2]`：這表示我們只搜尋文件的第二頁。您可以修改索引以定位其他頁面。
- `Accept()`：此方法允許 `TextFragmentAbsorber` 處理指定頁面內的文字。

## 步驟4：提取文字片段

搜尋頁面後，我們將找到的文字片段提取到一個集合中。

```csharp
// 取得擷取的文字片段
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- `TextFragmentCollection`：此集合包含在搜尋過程中找到的所有文字片段實例。

## 步驟 5：循環文字片段並擷取數據

現在，讓我們循環遍歷每個文字片段並提取其詳細信息，例如位置、字體和顏色。

```csharp
// 循環遍歷片段
foreach (TextFragment textFragment in textFragmentCollection)
{
    foreach (TextSegment textSegment in textFragment.Segments)
    {
        Console.WriteLine("Text : {0} ", textSegment.Text);
        Console.WriteLine("Position : {0} ", textSegment.Position);
        Console.WriteLine("XIndent : {0} ", textSegment.Position.XIndent);
        Console.WriteLine("YIndent : {0} ", textSegment.Position.YIndent);
        Console.WriteLine("Font - Name : {0}", textSegment.TextState.Font.FontName);
        Console.WriteLine("Font - IsAccessible : {0} ", textSegment.TextState.Font.IsAccessible);
        Console.WriteLine("Font - IsEmbedded : {0} ", textSegment.TextState.Font.IsEmbedded);
        Console.WriteLine("Font - IsSubset : {0} ", textSegment.TextState.Font.IsSubset);
        Console.WriteLine("Font Size : {0} ", textSegment.TextState.FontSize);
        Console.WriteLine("Foreground Color : {0} ", textSegment.TextState.ForegroundColor);
    }
}
```

- `foreach (TextFragment textFragment in textFragmentCollection)`：我們循環遍歷每一個 `TextFragment` 在收藏中。
- `foreach (TextSegment textSegment in textFragment.Segments)`：每個片段內部都有多個段落。我們循環遍歷它們以收集所有相關資訊。
- 各種屬性 `textSegment`：這些為我們提供了有關文字的詳細信息，例如其位置（X 和 Y）、字體細節、大小和顏色。

## 步驟6：輸出結果

最後，提取所有資訊後，在控制台中列印出結果。這可以幫助您準確地看到文字的位置及其格式細節。

為了清楚起見，這裡有一個範例輸出：

```
Text : text
Position : X: 45.0, Y: 75.0
XIndent : 45.0
YIndent : 75.0
Font - Name : Arial
Font - IsAccessible : True
Font - IsEmbedded : False
Font - IsSubset : False
Font Size : 12.0
Foreground Color : System.Drawing.Color [Black]
```

- 此輸出為您提供了指定頁面上文字「text」的確切位置和格式資訊。

## 結論

就是這樣！您剛剛學習如何使用 Aspose.PDF for .NET 在 PDF 文件中搜尋特定的文字段。處理大型 PDF 時，此過程非常方便，可讓您有效率地精確定位和提取關鍵文字。無論是分析資料、提取資訊或簡單地瀏覽文檔，Aspose.PDF 都能為您提供強大的工具來完成工作。

## 常見問題解答

### 我可以搜尋多個單字或短語嗎？
是的，您可以修改 `TextFragmentAbsorber` 透過改變輸入字串來搜尋不同的文字。

### 是否可以跨多個頁面進行搜尋？
絕對地！您可以透過迭代來遍歷 PDF 中的所有頁面 `pdfDocument。Pages`.

### 如何搜尋不區分大小寫的文字？
您可以使用 `TextSearchOptions` 啟用不區分大小寫的搜尋。

### 找到文字後我可以修改它嗎？
是的，一旦你找到了 `TextFragment`，即可修改其文字屬性。

### 此方法適用於加密的PDF嗎？
是的，只要您使用正確的密碼解鎖 PDF。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}