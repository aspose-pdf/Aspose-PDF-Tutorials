---
"description": "透過本教學學習如何使用 Aspose.PDF for .NET 從 PDF 檔案有效地提取突出顯示的文字。非常適合數據分析和內容審查。"
"linktitle": "提取 PDF 文件中突出顯示的文本"
"second_title": "Aspose.PDF for .NET API參考"
"title": "提取 PDF 文件中突出顯示的文本"
"url": "/zh-hant/net/annotations/extracthighlightedtext/"
"weight": 60
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 提取 PDF 文件中突出顯示的文本

## 介紹

處理 PDF 文件時，提取突出顯示的文本可能是一項至關重要的任務，無論是為了進行數據分析、內容審查，還是簡單地組織筆記。如果您使用 Aspose.PDF for .NET，這個過程簡單又有效率。在本教學中，我們將引導您了解如何使用 Aspose.PDF for .NET 從 PDF 文件中提取突出顯示的文字。我們將涵蓋從先決條件到逐步指導的所有內容，確保您最終全面了解。

## 先決條件

在深入研究程式碼之前，您需要做好以下幾點：

- Aspose.PDF for .NET 函式庫：請確定您已安裝 Aspose.PDF 函式庫。如果沒有，您可以從 [發布頁面](https://releases。aspose.com/pdf/net/).
- 開發環境：您應該設定一個可用的開發環境，例如 Visual Studio。
- C# 基礎知識：熟悉 C# 程式語言和物件導向程式設計至關重要。
- 有效的 Aspose 許可證：雖然您可以免費試用，但請考慮獲取 [臨時執照](https://purchase.aspose.com/temporary-license/) 或從 [這裡](https://purchase.aspose.com/buy) 不受限制地使用。

## 導入包

首先，您需要在 C# 專案中匯入必要的命名空間。這對於存取 Aspose.PDF for .NET 提供的類別和方法至關重要。

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

現在，讓我們分解使用 Aspose.PDF for .NET 從 PDF 文件中提取突出顯示文字的過程。每個步驟都進行了詳細解釋，以幫助您理解底層概念和實現。

## 步驟 1：設定項目目錄

首先，您需要設定 PDF 檔案所在的專案目錄。這就是奇蹟發生的地方。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

代替 `"YOUR DOCUMENT DIRECTORY"` 使用 PDF 檔案所在目錄的實際路徑。該目錄是應用程式獲取 PDF 進行處理的地方。

## 第 2 步：載入 PDF 文檔

接下來，您需要載入要從中提取突出顯示的文字的 PDF 文件。這是使用 `Document` Aspose.PDF 提供的類別。

```csharp
Document doc = new Document(dataDir + "ExtractHighlightedText.pdf");
```

這 `Document` 該類別透過 PDF 檔案的路徑進行實例化。這裡， `"ExtractHighlightedText.pdf"` 是包含突出顯示文字的 PDF 檔案的名稱。確保該檔案存在於指定的目錄中。

## 步驟 3：存取註解集合

一旦 PDF 文件被加載，下一步就是訪問文檔第一頁上的註釋。 PDF 中使用註釋來添加附加信息，例如突出顯示、評論等。

```csharp
foreach (Annotation annotation in doc.Pages[1].Annotations)
{
```

這 `Annotations` 的財產 `Page` 物件提供對 PDF 特定頁面上的所有註釋的存取。在這裡，我們循環遍歷第一頁上的每個註釋。

## 步驟 4：篩選突出顯示的文字註釋

現在我們可以存取所有註釋，我們需要僅過濾掉突出顯示的文字註釋。這是透過檢查每個註釋的類型來實現的。

```csharp
if (annotation is TextMarkupAnnotation)
{
    TextMarkupAnnotation highlightedAnnotation = annotation as TextMarkupAnnotation;
```

這 `TextMarkupAnnotation` 類別用於表示文字標記註釋，包括突出顯示。這 `is` 關鍵字檢查註釋是否屬於類型 `TextMarkupAnnotation`，如果是，則將註釋轉換為 `TextMarkupAnnotation`。

## 步驟5：提取突出顯示的文本

確定突出顯示的註釋後，下一步是提取與突出顯示相關的文字。

```csharp
TextFragmentCollection collection = highlightedAnnotation.GetMarkedTextFragments();
foreach (TextFragment tf in collection)
{
    Console.WriteLine(tf.Text);
}
```

這 `GetMarkedTextFragments()` 方法返回 `TextFragment` 對象，每個對象代表突出顯示的文字的一部分。我們循環遍歷這個集合並將每個片段的文字列印到控制台。

## 結論

使用 Aspose.PDF for .NET 從 PDF 中提取突出顯示的文字是一項強大的功能，可以簡化您的工作流程，特別是在處理大型文件時。透過遵循本教學中概述的步驟，您可以輕鬆地在自己的專案中實現此功能。無論您是整理筆記、準備報告還是進行資料分析，此方法都為提取和利用突出顯示的文字提供了無縫的解決方案。

## 常見問題解答

### 我可以使用此方法提取其他類型的註釋嗎？  
是的，您可以透過修改 `if` 檢查不同註釋類型的條件，例如 `TextAnnotation`， `StampAnnotation`， ETC。

### 是否可以從 PDF 的所有頁面中提取突出顯示的文字？  
絕對地！您可以循環遍歷 PDF 文件的每一頁，並應用相同的提取邏輯來收集每一頁的突出顯示的文字。

### 我需要許可證才能使用 Aspose.PDF for .NET 嗎？  
雖然你可以從免費試用開始，但建議獲取 [臨時執照](https://purchase.aspose.com/temporary-license/) 或購買完整許可證以無限制存取所有功能。

### 我可以將提取的文字儲存到文件而不是將其列印到控制台嗎？  
是的，您可以輕鬆修改程式碼，將提取的文字儲存為文字檔案或任何其他所需格式。

### Aspose.PDF 除了 .NET 之外還支援其他平台嗎？  
是的，Aspose.PDF 也支援 Java 和其他平台，在不同的環境中提供類似的功能。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}