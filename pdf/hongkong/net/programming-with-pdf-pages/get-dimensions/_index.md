---
"description": "在本教學中，我們將解釋如何取得 PDF 頁面尺寸並使用 Aspose.PDF for .NET 執行操作。提供了詳細的步驟來引導您完成整個過程。"
"linktitle": "取得 PDF 頁面尺寸"
"second_title": "Aspose.PDF for .NET API參考"
"title": "取得 PDF 頁面尺寸"
"url": "/zh-hant/net/programming-with-pdf-pages/get-dimensions/"
"weight": 60
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 取得 PDF 頁面尺寸

## 介紹

您是否曾經需要操縱 PDF 文件的頁面尺寸？也許您想調整頁面大小或旋轉頁面以滿足您的需求？如果是這樣，那麼您來對地方了！在本教學中，我們將引導您使用 Aspose.PDF for .NET 擷取和修改 PDF 頁面尺寸。無論您是初學者還是經驗豐富的開發人員，您都會發現本指南簡單易懂。

Aspose.PDF for .NET 是一個功能強大的程式庫，可讓您輕鬆建立、操作和轉換 PDF 檔案。這就像是 PDF 的瑞士軍刀——您可以調整每一個小細節以滿足您的確切要求。那麼，讓我們深入學習如何使用這個很棒的工具來獲取和更新 PDF 頁面尺寸！

## 先決條件

在開始之前，您需要做好一些準備才能順利完成本教學：

1. Aspose.PDF for .NET：您可以 [點此下載最新版本](https://releases.aspose.com/pdf/net/)。如果您沒有許可證，請不要擔心！您可以請求 [免費試用](https://releases.aspose.com/)或選擇 [臨時執照](https://purchase。aspose.com/temporary-license/).
2. Visual Studio：用於編寫和執行程式碼的開發環境。
3. C# 的基礎知識：雖然我們會讓事情變得簡單，但熟悉 C# 會使過程更加順暢。
4. 要使用的 PDF 檔案：取得任何範例 PDF 檔案或建立一個新的 PDF 檔案進行測試。

## 導入包

要使用 Aspose.PDF for .NET，您需要匯入一些基本命名空間。這為與 PDF 文件的交互奠定了基礎。具體操作如下：

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

這些匯入可確保您可以存取操作 PDF 文件所需的核心類，特別是管理頁面和檢索其尺寸。

現在我們已經準備好一切，讓我們將流程分解為易於遵循的步驟。

## 步驟 1：定義文件路徑並載入文檔

第一步是指定 PDF 文件的路徑並使用 Aspose.PDF 載入它。這將允許您與 PDF 文件中的頁面進行互動。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";

// 開啟文件
Document pdfDocument = new Document(dataDir + "UpdateDimensions.pdf");
```

在此步驟中，您實際上是開啟要處理的 PDF 檔案。如果您曾經打開過一本書的某個特定頁面，那麼這非常相似 - 但您打開的是 PDF 文件來訪問其頁面。

## 步驟 2：如果不存在頁面，則新增空白頁

如果您的文件沒有頁面怎麼辦？不用擔心！我們可以在文件中新增一個空白頁並對其進行處理。檢查頁面是否存在並在必要時新增頁面的方法如下：

```csharp
// 在 PDF 文件中新增空白頁
Page page = pdfDocument.Pages.Count > 0 ? pdfDocument.Pages[1] : pdfDocument.Pages.Add();
```

這行程式碼檢查文件中是否已經有頁面。如果是，則選擇第一頁（`Pages[1]`）。否則，它會建立一個空白頁並將其新增到 PDF 中。

想像打開一本空白筆記本，如果上面什麼都沒有就在第一頁上寫字——很簡單，對吧？

## 步驟3：取得頁面高度和寬度信息

現在我們有了一個可以使用的頁面，讓我們檢索頁面的尺寸。我們將使用 `GetPageRect()` 方法來取得高度和寬度。

```csharp
// 取得頁面高度和寬度信息
Console.WriteLine(page.GetPageRect(true).Width.ToString() + ":" + page.GetPageRect(true).Height.ToString());
```

這裡， `GetPageRect(true)` 傳回一個包含頁面高度和寬度的矩形。這就像用尺測量一張紙。輸出將顯示在控制台中，為您提供目前頁面尺寸。

## 步驟 4：將頁面旋轉 90 度

您想旋轉頁面嗎？沒問題！使用一個簡單的屬性，您可以將頁面旋轉 90 度。

```csharp
// 將頁面旋轉 90 度
page.Rotate = Rotation.on90;
```

此步驟將頁面順時針旋轉 90 度。想像一下，您正在桌上翻轉一張列印的紙張 - 現在它處於橫向模式！

## 步驟 5：旋轉後重新檢查頁面尺寸

旋轉頁面後，最好再次檢查尺寸。為什麼？因為旋轉會影響您對高度和寬度的解釋。

```csharp
// 取得頁面高度和寬度信息
Console.WriteLine(page.GetPageRect(true).Width.ToString() + ":" + page.GetPageRect(true).Height.ToString());
```

現在，頁面尺寸將根據新的方向進行更新。這就像在手機上旋轉照片一樣——突然，寬度變成了高度，反之亦然。


## 結論

恭喜！您已成功學習如何使用 Aspose.PDF for .NET 擷取並修改 PDF 頁面的尺寸。現在，您應該能夠加載 PDF、檢查其頁面尺寸，甚至根據需要旋轉頁面。

操作 PDF 不一定很複雜。使用 Aspose.PDF，只需按照幾個步驟並使用直覺的方法即可。因此，下次您需要處理 PDF 頁面尺寸時，您就會確切地知道該怎麼做！

## 常見問題解答

### 除了 90 度以外，我還可以用其他角度旋轉頁面嗎？
是的，Aspose.PDF 允許您使用 `Rotation` 財產。

### 如果我的 PDF 沒有頁面會怎麼樣？
如果您的 PDF 沒有頁面，您可以使用 `Pages.Add()` 方法，如本教學所示。

### 我可以同時操作多個頁面嗎？
是的，您可以循環遍歷多個頁面並對所有頁面套用轉換，例如調整大小或旋轉。

### 頁面尺寸會影響 PDF 中的內容嗎？
頁面尺寸只會改變畫布的大小，而不會改變內容。但是，調整大小可能會改變頁面上內容的顯示方式。

### 在哪裡可以找到有關 Aspose.PDF for .NET 的更多資訊？
您可以訪問 [文件在這裡](https://reference.aspose.com/pdf/net/) 了解更多詳細資訊和進階用例。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}