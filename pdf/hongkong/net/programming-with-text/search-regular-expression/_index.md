---
"description": "在本逐步教學中學習如何使用 Aspose.PDF for .NET 在 PDF 檔案中搜尋正規表示式。使用正規表示式提高您的工作效率。"
"linktitle": "在 PDF 檔案中搜尋正規表示式"
"second_title": "Aspose.PDF for .NET API參考"
"title": "在 PDF 檔案中搜尋正規表示式"
"url": "/zh-hant/net/programming-with-text/search-regular-expression/"
"weight": 440
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 檔案中搜尋正規表示式

## 介紹

處理大型 PDF 文件時，您可能會發現自己正在搜尋特定的模式或格式，例如日期、電話號碼或其他結構化資料。手動瀏覽 PDF 可能很乏味，對吧？這時使用正規表示式（regex）就派上用場了。在本教學中，我們將探討如何使用 Aspose.PDF for .NET 在 PDF 檔案中搜尋正規表示式模式。本指南將引導您完成每個步驟，以便您可以輕鬆地在 .NET 應用程式中實現它。

## 先決條件

在深入學習逐步教學之前，讓我們先了解您需要準備的內容：

- Aspose.PDF for .NET：您需要安裝此程式庫。如果你還沒有安裝，你可以 [點此下載](https://releases。aspose.com/pdf/net/).
- IDE：Visual Studio 或任何其他與 C# 相容的 IDE。
- .NET Framework：確保您的專案設定了適當版本的 .NET Framework。
- C# 基礎知識：雖然本指南很詳細，但對 C# 有基本的了解將會很有幫助。

### 導入包

首先，您需要將 Aspose.PDF for .NET 中必要的命名空間匯入到您的專案中。這些套件對於處理 PDF 和使用正規表示式執行搜尋操作至關重要。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

讓我們將使用 Aspose.PDF 在 PDF 檔案中搜尋正規表示式的過程分解為多個步驟。

## 步驟 1：設定文檔目錄

每個 PDF 操作都從指定文件的位置開始。您需要定義 PDF 文件的路徑，該文件儲存在 `dataDir` 多變的。

### 步驟 1.1：定義文檔路徑

```csharp
// 定義 PDF 文件的路徑
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

代替 `"YOUR DOCUMENT DIRECTORY"` 使用您的 PDF 檔案的實際路徑。此步驟至關重要，因為它將您的程式碼指向您想要使用的檔案。

### 步驟 1.2：開啟 PDF 文檔

接下來，您需要使用 `Document` 來自 Aspose.PDF 的類別。

```csharp
// 開啟文件
Document pdfDocument = new Document(dataDir + "SearchRegularExpressionAll.pdf");
```

這裡， `"SearchRegularExpressionAll.pdf"` 是我們將執行正規表示式搜尋的範例 PDF 檔案。

## 第 2 步：設定 TextFragmentAbsorber

這就是奇蹟發生的地方！這 `TextFragmentAbsorber` 類別有助於捕獲與特定模式或正規表示式相符的文字片段。

讓我們設定吸收器來使用正規表示式來尋找模式。在這種情況下，我們正在尋找像“1999-2000”這樣的年份模式。

```csharp
// 建立 TextAbsorber 物件來尋找與正規表示式相符的所有短語
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("\\d{4}-\\d{4}"); // 如1999-2000年
```

正規表示式 `\\d{4}-\\d{4}` 找出四位數字後面跟著連字符和另外四位數字的模式，這是年份範圍的典型特徵。

## 步驟 3：啟用正規表示式搜尋

為了確保搜尋操作將模式解釋為正規表示式，您需要使用 `TextSearchOptions` 班級。

```csharp
// 設定文字搜尋選項以指定正規表示式的使用
TextSearchOptions textSearchOptions = new TextSearchOptions(true);
textFragmentAbsorber.TextSearchOptions = textSearchOptions;
```

設定 `TextSearchOptions` 到 `true` 確保吸收器使用基於正規表示式的搜尋而不是純文字。

## 步驟 4：接受文字吸收器

在此階段，您將文字吸收器套用至 PDF 文檔，以便它可以執行搜尋操作。這是透過調用 `Accept` 方法 `Pages` PDF 文件的對象。

```csharp
// 接受所有頁面的吸收器
pdfDocument.Pages.Accept(textFragmentAbsorber);
```

此命令處理 PDF 的所有頁面，尋找與正規表示式相符的任何文字。

## 步驟 5：擷取並顯示結果

搜尋完成後，需要擷取結果。這 `TextFragmentAbsorber` 將這些結果儲存在 `TextFragmentCollection`。您可以循環遍歷該集合來存取和顯示每個符合的文字片段。

### 步驟 5.1：檢索擷取的文字片段

```csharp
// 取得擷取的文字片段
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

現在您已經收集了片段，是時候循環遍歷它們並顯示相關詳細信息，例如文字、位置、字體詳細資訊等。

### 步驟 5.2：循環遍歷片段

```csharp
// 循環遍歷片段
foreach (TextFragment textFragment in textFragmentCollection)
{
    Console.WriteLine("Text : {0} ", textFragment.Text);
    Console.WriteLine("Position : {0} ", textFragment.Position);
    Console.WriteLine("XIndent : {0} ", textFragment.Position.XIndent);
    Console.WriteLine("YIndent : {0} ", textFragment.Position.YIndent);
    Console.WriteLine("Font - Name : {0}", textFragment.TextState.Font.FontName);
    Console.WriteLine("Font - IsAccessible : {0} ", textFragment.TextState.Font.IsAccessible);
    Console.WriteLine("Font - IsEmbedded : {0} ", textFragment.TextState.Font.IsEmbedded);
    Console.WriteLine("Font - IsSubset : {0} ", textFragment.TextState.Font.IsSubset);
    Console.WriteLine("Font Size : {0} ", textFragment.TextState.FontSize);
    Console.WriteLine("Foreground Color : {0} ", textFragment.TextState.ForegroundColor);
}
```

對於每個 `TextFragment`，字體大小、字體名稱、位置等詳細資訊都會列印出來。這不僅有助於查找文本，還可以提供其準確的格式和位置。

## 結論

就是這樣！使用正規表示式在 PDF 檔案中搜尋模式非常強大，特別是對於日期、電話號碼和類似模式等結構化文字。 Aspose.PDF for .NET 提供了一種無縫的方式來輕鬆執行此類操作。現在，您可以利用正規表示式的強大功能來自動化 PDF 文字搜索，從而提高工作流程的效率。

## 常見問題解答

### 我可以在一個 PDF 中搜尋多個圖案嗎？
是的，你可以運行多個 `TextFragmentAbsorber` 對象，每個對像都有不同的正規表示式模式，跨越同一個 PDF。

### Aspose.PDF 是否支援搜尋不區分大小寫的模式？
絕對地！您可以配置 `TextSearchOptions` 使搜尋不區分大小寫。

### 我可以搜尋的 PDF 的大小有限制嗎？
沒有嚴格的限制，但效能可能會根據 PDF 的大小和正規表示式模式的複雜性而有所不同。

### 我可以突出顯示 PDF 中找到的文字嗎？
是的，Aspose.PDF 允許您使用吸收器來反白甚至替換找到的文字。

### 如果找不到模式，我該如何處理錯誤？
如果沒有找到匹配項， `TextFragmentCollection` 將為空。您可以在循環遍歷結果之前透過簡單的檢查來處理這種情況。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}