---
"description": "了解如何使用 Aspose.PDF for .NET 從 PDF 檔案中提取文字列。本指南透過程式碼範例和解釋分解每個步驟。"
"linktitle": "提取 PDF 文件中的列文本"
"second_title": "Aspose.PDF for .NET API參考"
"title": "提取 PDF 文件中的列文本"
"url": "/zh-hant/net/programming-with-text/extract-columns-text/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 提取 PDF 文件中的列文本

## 介紹

您是否正在處理 PDF 文件並需要提取特定列格式的文字？無論您處理的是發票、報告還是任何結構化文檔，從 PDF 中準確提取文字都可能是一項棘手的工作。這就是 Aspose.PDF for .NET 介入簡化流程的地方。在本教程中，我們將引導您如何輕鬆地從 PDF 文件中提取文字列。 

## 先決條件

在深入研究程式碼之前，讓我們先介紹一下您需要的基本內容：

- Aspose.PDF for .NET：請確定您已安裝了最新版本的 Aspose.PDF for .NET。如果沒有，你可以 [點此下載](https://releases。aspose.com/pdf/net/).
- 開發環境：您需要 Visual Studio 或其他 .NET 開發環境來處理程式碼。
- PDF 文檔：準備一個範例 PDF 文檔，最好是包含文字列的文檔，因為我們將從中提取文字。

如果你還沒安裝 Aspose.PDF for .NET，你可以取得 [免費試用](https://releases.aspose.com/) 或者 [購買許可證](https://purchase.aspose.com/buy) 了解全部功能。您還可以申請 [臨時執照](https://purchase.aspose.com/temporary-license) 如果需要的話。

## 導入命名空間

要在您的專案中使用 Aspose.PDF for .NET，您需要匯入以下命名空間：

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

## 逐步指南：從 PDF 提取文字列

現在，讓我們分解程式碼的每個部分，以便更好地理解它是如何運作的。請跟隨我們一步一步地解釋該過程的每個部分。

## 步驟 1：載入 PDF 文檔

您需要做的第一件事是將 PDF 文件加載到 `Document` 目的。這就是 Aspose.PDF 與您的文件互動的方式。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document pdfDocument = new Document(dataDir + "ExtractTextPage.pdf");
```

在此步驟中，我們只是定義儲存 PDF 文件的目錄。代替 `"YOUR DOCUMENT DIRECTORY"` 使用本地 PDF 檔案的路徑。這 `Document` 物件將 PDF 載入到記憶體中，以便進行進一步處理。

## 第 2 步：設定文字片段吸收器

接下來，我們將使用 `TextFragmentAbsorber` 吸收或捕獲 PDF 文件中的所有文字。此吸收器類別旨在從 PDF 中的特定區域提取文字片段，這使其成為提取文字列的理想選擇。

```csharp
TextFragmentAbsorber tfa = new TextFragmentAbsorber();
pdfDocument.Pages.Accept(tfa);
TextFragmentCollection tfc = tfa.TextFragments;
```

在這裡，我們建立一個實例 `TextFragmentAbsorber` 並將其應用於 PDF 的所有頁面 `Accept()`。這 `TextFragmentCollection` 儲存提取的文本，從這個集合中，我們可以根據需要操作或提取文本。

## 步驟3：調整擷取文字的字體大小

一旦捕獲了文字片段，您可能會想要減小其字體大小，尤其是當原始文字太大時。在這個例子中，我們將字體大小縮小了 70%。

```csharp
foreach (TextFragment tf in tfc)
{
    // 將字體大小縮小 70%
    tf.TextState.FontSize = tf.TextState.FontSize * 0.7f;
}
```

此程式碼循環遍歷每個 `TextFragment` 並將其字體大小縮小 70%。調整字體大小可以使提取的文字更易於管理，特別是當您為了不同的目的而對其進行格式化時。

## 步驟 4：將文件儲存到記憶體流

修改文字後，我們將 PDF 儲存為 `MemoryStream`。這使得我們可以將文件保存在記憶體中以供進一步處理，而無需將其寫回磁碟。

```csharp
Stream st = new MemoryStream();
pdfDocument.Save(st);
pdfDocument = new Document(st);
```

在這裡，我們將 PDF 儲存到記憶體流中，然後重新載入文件。當您處理大檔案並想要避免不必要的磁碟操作時，此方法很有用。

## 步驟5：使用文本吸收器提取所有文本

現在我們已經準備好 PDF，是時候提取文字了。我們將使用 `TextAbsorber` 從文件中抓取所有文字。

```csharp
TextAbsorber textAbsorber = new TextAbsorber();
pdfDocument.Pages.Accept(textAbsorber);
String extractedText = textAbsorber.Text;
```

在此步驟中， `TextAbsorber` 吸收 PDF 中的所有文本，並將提取的文本儲存在 `extractedText` 細繩。這就是奇蹟發生的地方——您的文字列現在是純文字格式！

## 步驟 6：將提取的文字儲存到文件

最後，我們將提取的文字儲存到 `.txt` 文件以便於存取和進一步使用。

```csharp
dataDir = dataDir + "ExtractColumnsText_out.txt";
System.IO.File.WriteAllText(dataDir, extractedText);
Console.WriteLine("\nColumns text extracted successfully from Pages of PDF Document.\nFile saved at " + dataDir);
```

此程式碼將提取的文字寫入新的 `.txt` 文件並將其保存在指定的目錄中。控制台中將顯示一則訊息，確認流程已成功。

## 結論

就是這樣！使用 Aspose.PDF for .NET 從 PDF 文件中提取文字列比您想像的要容易。只需幾行程式碼，您就可以載入 PDF、提取特定文字、調整格式並將結果儲存到文字檔案中。

此技術對於處理表格、報告或按列組織的任何內容等結構化文件非常有用。無論您需要自動擷取資料或處理批次文檔，Aspose.PDF 都能提供高效率實現此目標的工具。

## 常見問題解答

### 我可以從 PDF 的特定頁面提取文字嗎？  
是的！您可以修改 `TextFragmentAbsorber` 使用 `pdfDocument.Pages[pageIndex].Accept(tfa);` 方法。

### 是否可以從多列 PDF 中的一列中提取文字？  
是的，但您需要使用以下方法處理文字片段的座標 `TextFragment.Rectangle` 針對文檔的特定區域。

### 如何提高文字擷取的準確性？  
為了提高準確性，請確保 PDF 的結構明確，並避免使用佈局複雜的文件。您還可以微調 `TextFragmentAbsorber` 根據字體樣式、大小或區域提取文字。

### Aspose.PDF 是否支援從掃描文件中提取文字？  
是的，但您需要使用 OCR（光學字元辨識）技術。 Aspose 也為此提供了工具。

### 如何處理包含數千頁的大型 PDF 檔案？  
對於大型 PDF，透過一次從幾頁中提取文字來分塊處理文檔，以避免高記憶體佔用。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}