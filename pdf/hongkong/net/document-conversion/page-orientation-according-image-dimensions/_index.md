---
"description": "在本逐步指南中了解如何使用 Aspose.PDF for .NET 建立 PDF，並根據影像尺寸設定頁面方向。"
"linktitle": "根據影像尺寸調整頁面方向"
"second_title": "Aspose.PDF for .NET API參考"
"title": "根據影像尺寸調整頁面方向"
"url": "/zh-hant/net/document-conversion/page-orientation-according-image-dimensions/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 根據影像尺寸調整頁面方向

## 介紹

歡迎來到 Aspose.PDF for .NET 的世界！如果您希望以程式設計方式建立、操作或轉換 PDF 文檔，那麼您來對地方了。 Aspose.PDF 是一個功能強大的程式庫，可讓開發人員無縫地處理 PDF 檔案。在本指南中，我們將引導您完成根據圖像尺寸設定頁面方向的過程。無論您是經驗豐富的開發人員還是剛剛入門，本教學都將為您提供使用 Aspose.PDF 所需的知識。

## 先決條件

在深入研究程式碼之前，請確保您已準備好接下來需要的一切：

1. Visual Studio：確保您的機器上安裝了 Visual Studio。它是.NET 開發的最佳 IDE。
2. .NET Framework：本指南假設您使用 .NET Framework。確保您已安裝適當的版本。
3. Aspose.PDF for .NET：您可以從 [Aspose 網站](https://releases.aspose.com/pdf/net/)。如果你想先嘗試一下，你可以得到一個 [免費試用](https://releases。aspose.com/).
4. C# 基礎知識：熟悉 C# 程式設計將幫助您更好地理解範例。

## 導入包

首先，您需要匯入必要的套件。您可以按照以下步驟操作：

1. 開啟您的 Visual Studio 專案。
2. 在解決方案資源管理器中右鍵單擊您的專案並選擇“管理 NuGet 套件”。
3. 搜尋 `Aspose.PDF` 並安裝它。

現在我們已經設定好了一切，讓我們逐步分解這個範例。

## 步驟 1：設定文檔目錄

首先，您需要指定儲存影像的文檔目錄的路徑。 Aspose 將在此尋找 JPG 檔案。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

代替 `"YOUR DOCUMENT DIRECTORY"` 使用影像所在的實際路徑。這很關鍵，因為如果 Aspose 找不到您的映像，它就無法建立 PDF。

## 步驟2：建立新的PDF文檔

接下來，您將建立一個新的 PDF 文件物件。所有圖像都將被添加到這裡。

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

這行初始化了 `Document` 類，代表您的 PDF 文件。

## 步驟3：檢索影像文件

現在，讓我們從指定目錄中檢索所有 JPG 檔案。這是使用 `Directory.GetFiles` 方法。

```csharp
string[] fileEntries = Directory.GetFiles(dataDir, "*.JPG");
```

此行將為您提供與 JPG 格式相符的檔案名稱陣列。確保您的目錄包含一些 JPG 圖像才能使其正常工作！

## 步驟 4：循環遍歷每個影像

您需要循環遍歷每個影像檔案並將其新增至 PDF 文件中。您可以按照以下步驟操作：

```csharp
int counter;
for (counter = 0; counter < fileEntries.Length - 1; counter++)
{
    // 建立頁面對象
    Aspose.Pdf.Page page = doc.Pages.Add();
```

在這個循環中，您將為每個圖像建立一個新頁面。這 `doc.Pages.Add()` 方法將新頁面新增到您的 PDF 文件中。

## 步驟5：建立影像對象

對於每張圖片，您需要建立一個 `Image` 保存影像資料的對象。

```csharp
    Aspose.Pdf.Image image1 = new Aspose.Pdf.Image();
    image1.File = fileEntries[counter];
```

在這裡，您將當前圖像檔案指派給 `Image` 目的。這對於將圖像添加到 PDF 至關重要。

## 步驟6：檢查影像尺寸

在將圖像新增至 PDF 之前，您需要檢查其尺寸以確定頁面方向。

```csharp
    Bitmap myimage = new Bitmap(fileEntries[counter]);
    if (myimage.Width > page.PageInfo.Width)
        page.PageInfo.IsLandscape = true;
    else
        page.PageInfo.IsLandscape = false;
```

此程式碼片段檢查圖像的寬度是否大於頁面寬度。如果是，則將頁面方向設為橫向；否則，它將保持縱向模式。

## 步驟 7：將影像新增至 PDF

現在您已經設定了方向，是時候將圖像新增至 PDF 文件了。

```csharp
    page.Paragraphs.Add(image1);
}
```

此行將圖像新增至目前頁面的段落集合中。就像將一幅畫放在相框裡一樣！

## 步驟 8：儲存 PDF 文檔

最後，您需要將 PDF 文件儲存到指定的目錄中。

```csharp
doc.Save(dataDir + "SetPageOrientation_out.pdf");
```

此行將文件儲存為 `SetPageOrientation_out.pdf`。請務必檢查您的文件目錄中是否有新建立的 PDF！

## 結論

就是這樣！您已成功使用 Aspose.PDF for .NET 建立 PDF 文檔，並根據影像的尺寸設定頁面方向。這個強大的庫為您在應用程式中處理 PDF 文件開闢了無限的可能性。無論您產生報告、發票或任何其他類型的文檔，Aspose.PDF 都能滿足您的需求。

## 常見問題解答

### 什麼是 Aspose.PDF for .NET？
Aspose.PDF for .NET 是一個函式庫，可讓開發人員以程式設計方式建立、操作和轉換 PDF 文件。

### 如何安裝 Aspose.PDF？
您可以透過 Visual Studio 中的 NuGet 套件管理器安裝 Aspose.PDF，或從 [Aspose 網站](https://releases。aspose.com/pdf/net/).

### 我可以免費使用 Aspose.PDF 嗎？
是的，Aspose 提供 [免費試用](https://releases.aspose.com/) 供您在購買之前測試該庫。

### 在哪裡可以找到對 Aspose.PDF 的支援？
您可以在 [Aspose 論壇](https://forum。aspose.com/c/pdf/10).

### 我可以使用 Aspose 將哪些類型的檔案轉換為 PDF？
Aspose.PDF 支援多種文件格式，包括影像、Word 文件、Excel 試算表等。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}