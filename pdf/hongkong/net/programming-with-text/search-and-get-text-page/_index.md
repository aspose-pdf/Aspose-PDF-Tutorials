---
"description": "了解如何使用 Aspose.PDF for .NET 搜尋並取得 PDF 檔案中特定頁面的文字。"
"linktitle": "在 PDF 文件中搜尋並獲取文字頁面"
"second_title": "Aspose.PDF for .NET API參考"
"title": "在 PDF 文件中搜尋並獲取文字頁面"
"url": "/zh-hant/net/programming-with-text/search-and-get-text-page/"
"weight": 430
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 文件中搜尋並獲取文字頁面

## 介紹

您是否發現自己需要在 PDF 文件中搜尋特定文字並將其提取以供進一步使用？也許您正在建立一個處理文件並需要精確資料提取的應用程序，或者也許您只是需要有效地解析 PDF。無論您的情況如何，您都來對地方了！在本教程中，我們將深入研究如何使用 Aspose.PDF for .NET 從 PDF 文件中的頁面搜尋和取得文字。無論您是初學者還是經驗豐富的開發人員，本指南都將以對話和引人入勝的方式引導您完成每個步驟。準備好了嗎？讓我們開始吧！

## 先決條件

在開始編碼之前，請確保您已準備好所需的一切：

1. Aspose.PDF for .NET Library：您可以從 [這裡](https://releases.aspose.com/pdf/net/) 或從同一連結取得免費試用版。如欲購買，請前往 [Aspose 商店](https://purchase。aspose.com/buy).
2. .NET Framework：您需要一個可用的 .NET 開發環境，例如 Visual Studio。
3. PDF 文件：您需要一個範例 PDF 文件，我們可以在其中搜尋和提取文字。在本教程中，我們假設文件名為 `SearchAndGetTextPage。pdf`.

## 導入包

首先，我們需要匯入必要的命名空間才能使用 Aspose.PDF for .NET。確保這些內容包含在程式碼的頂部。

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System
```

現在我們已經介紹了先決條件，讓我們逐步分解程式碼。每個步驟都已清晰列出，以便於遵循。

## 步驟 1：設定文檔目錄的路徑

在與您的 PDF 互動之前，您需要定義儲存 PDF 文件的路徑。這確保程式可以存取該文件。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

- dataDir：這是儲存 PDF 檔案的資料夾的路徑。代替 `"YOUR DOCUMENT DIRECTORY"` 與 PDF 所在的實際路徑。

## 第 2 步：載入 PDF 文檔

下一步是將 PDF 文件載入到記憶體中，以便您可以使用它。方法如下：

```csharp
Document pdfDocument = new Document(dataDir + "SearchAndGetTextPage.pdf");
```

- 文件：這是載入 PDF 文件的 Aspose.PDF 類別。
- pdfDocument：載入 PDF 文件後儲存該文件的變數。

## 步驟3：建立文字吸收器對象

這 `TextFragmentAbsorber` 類別允許您在 PDF 中搜尋特定文字。讓我們建立此類的一個實例來尋找給定搜尋字詞的所有實例。

```csharp
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("Figure");
```

- TextFragmentAbsorber：此類負責從 PDF 中尋找和提取文字。
- 「圖形」：將其替換為您想要在 PDF 中搜尋的任何文字。

## 步驟 4：將文字吸收器應用於整個 PDF

一旦設定了文字吸收器，您需要告訴程式搜尋 PDF 的所有頁面。

```csharp
pdfDocument.Pages.Accept(textFragmentAbsorber);
```

- Accept()：此方法將文字吸收器套用至 PDF，掃描每一頁以尋找您指定的文字。

## 步驟 5：檢索並迭代提取的文本

現在我們已經掃描了 PDF，是時候檢索結果並顯示它們了。我們將循環遍歷提取的文字片段。

```csharp
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- TextFragmentCollection：此集合保存文字吸收器發現的所有文字片段實例。

## 步驟 6：循環遍歷每個片段並提取數據

我們現在將循環遍歷 `textFragmentCollection` 並提取每個文字段的各種屬性，例如其位置、字體細節和顏色。

```csharp
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

- TextFragment：每個片段包含找到的文字的部分。
- TextSegment：每個片段可以有多個段落，分別代表文字的不同部分。
- TextState：提供有關文字字體、大小和顏色的詳細資訊。

在這個循環中，我們列印出諸如實際文字、其位置（X 和 Y 座標）、字體、字體是否嵌入在 PDF 中以及文字的前景色等詳細資訊。

## 結論

就是這樣！現在，您已成功使用 Aspose.PDF for .NET 從 PDF 文件中搜尋並提取文字。令人驚訝的是，這個庫具有如此大的靈活性。無論您需要在大型文件中搜尋特定文字、提取文字或分析其屬性，Aspose.PDF 都能讓您輕鬆完成。另外，透過我們提供的程式碼，您可以根據自己的需求進行調整。 

## 常見問題解答

### 我可以一次搜尋多個短語嗎？  
是的，您可以透過建立多個來修改程式碼以搜尋多個短語 `TextFragmentAbsorber` 對象。

### 如何從特定頁面提取文字？  
您可以透過應用 `TextFragmentAbsorber` 到單一頁面而不是整個文件。例如： `pdfDocument。Pages[1].Accept(textFragmentAbsorber);`.

### Aspose.PDF for .NET 免費嗎？  
Aspose.PDF 是一個商業產品，但你可以將它與 [免費試用](https://releases。aspose.com/).

### 我可以使用 Aspose.PDF 從 PDF 中提取圖像嗎？  
是的，Aspose.PDF 允許您除了提取文字之外還提取圖像。檢查 [文件](https://reference.aspose.com/pdf/net/) 了解更多詳情。

### 如果我需要更多幫助或支持怎麼辦？  
您可以隨時從 [Aspose 支援論壇](https://forum。aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}