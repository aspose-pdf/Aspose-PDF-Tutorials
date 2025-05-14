---
"description": "在本逐步教學中學習如何使用 Aspose.PDF for .NET 將圖像和頁碼新增至 PDF 的頁首和頁尾。"
"linktitle": "頁眉頁尾部分中的圖像和頁碼"
"second_title": "Aspose.PDF for .NET API參考"
"title": "頁眉頁尾部分中的圖像和頁碼"
"url": "/zh-hant/net/programming-with-stamps-and-watermarks/image-and-page-number-in-header-footer-section/"
"weight": 110
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 頁眉頁尾部分中的圖像和頁碼

## 介紹

在建立專業級 PDF 文件時，控制頁首和頁尾等細節至關重要。您希望您的文件看起來精美且井然有序，對嗎？好吧，使用 Aspose.PDF for .NET，您可以將圖像和頁碼無縫添加到文件的頁首和頁尾部分。在本教程中，我們將指導您完成每個步驟，讓您輕鬆跟進。

## 先決條件

在深入了解本教學的細節之前，請確保您已完成以下事項：

1. .NET Framework：您需要在電腦上安裝任意版本的 .NET Framework。如果您沒有，您可以從 Microsoft 網站輕鬆下載它。
2. Aspose.PDF for .NET：由於我們將使用 Aspose.PDF，請確保您的專案中已安裝它。您可以下載試用版 [這裡](https://releases。aspose.com/pdf/net/).
3. C# 基礎知識：熟悉基本的 C# 程式設計肯定會幫助您輕鬆理解程式碼。
4. 圖像檔案：您需要一張想要放在 PDF 文件頁眉中的圖像，例如徽標。將其保存在可存取的目錄中。 
5. IDE：使用您選擇的整合開發環境 (IDE)（如 Visual Studio）來處理您的 .NET 專案。

一旦準備好先決條件，您就可以建立精彩的 PDF 檔案了！

## 導入包

要開始使用 Aspose.PDF for .NET，您需要匯入必要的命名空間。在您的 C# 檔案的頂部，您需要新增：

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Image;
```

這些命名空間將為您提供操作 PDF 檔案所需的類別的存取權限。

現在讓我們開始真正的交易吧！請依照下列步驟建立 PDF 文檔，在頁首中加入影像，在頁尾中加入頁碼。

## 步驟 1：設定文檔目錄

每個好的項目都始於組織。定義您將儲存檔案和影像的文件目錄。具體操作如下：

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

記得更換 `"YOUR DOCUMENT DIRECTORY"` 使用您想要儲存 PDF 和影像所在的實際路徑。

## 步驟2：建立新的PDF文檔

接下來，我們將建立一個新的 PDF 文檔，所有神奇的事情都會在這裡發生：

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

此時，您已經建立了一個空的 PDF 文件。很令人興奮，不是嗎？

## 步驟 3：新增頁面

PDF 的全部內容都是頁面。讓我們使用以下命令為我們的文件新增一個新頁面：

```csharp
Aspose.Pdf.Page page = doc.Pages.Add();
```

現在您已經擁有了可以開始設計的畫布！

## 步驟 4：建立標題部分

您的標題將包含您想要顯示的圖像（如徽標）。使用以下程式碼建立標題部分：

```csharp
Aspose.Pdf.HeaderFooter header = new Aspose.Pdf.HeaderFooter();
page.Header = header;
```

現在您有一個可以自訂的標題！

## 步驟 5：為頁首新增圖像

現在我們進入有趣的部分！您需要將圖像新增至標題。首先，建立一個影像物件：

```csharp
Aspose.Pdf.Image image1 = new Aspose.Pdf.Image();
```

設定影像的檔案路徑：

```csharp
image1.File = dataDir + "aspose-logo.jpg";
```

最後，將圖像新增至標題：

```csharp
header.Paragraphs.Add(image1);
```

恭喜！您剛剛在 PDF 頁眉中新增了一張圖片。

## 步驟 6：建立頁尾部分

現在讓我們來處理頁腳。與頁首流程類似，建立頁尾物件：

```csharp
Aspose.Pdf.HeaderFooter footer = new Aspose.Pdf.HeaderFooter();
page.Footer = footer;
```

這是您放置頁碼的地方。 

## 步驟 7：為頁尾新增文本

建立一個儲存頁碼的文字片段：

```csharp
Aspose.Pdf.Text.TextFragment txt = new Aspose.Pdf.Text.TextFragment("Page: ($p of $P ) ");
```

然後將此文字片段新增至頁尾：

```csharp
footer.Paragraphs.Add(txt);
```

看看這有多簡單？您已動態設定頁碼！

## 步驟 8：儲存 PDF 文檔

我們冒險的最後一步是儲存文件。使用此命令儲存新建立的 PDF：

```csharp
doc.Save(dataDir + "ImageAndPageNumberInHeaderFooter_out.pdf");
```

就這樣，您的 PDF 已準備就緒，並在頁腳中加載了頁眉圖像和頁碼！

## 結論

就是這樣！您剛剛使用 Aspose.PDF for .NET 建立了一個 PDF，其中頁首中有圖像，頁腳中有動態頁碼。令人驚訝的是，僅用幾行程式碼就能產生如此完美的輸出。無論是公司報告還是個人化文檔，添加這些元素都會改變 PDF 的基調和專業性。

## 常見問題解答

### 我可以在任何 .NET 平台上使用 Aspose.PDF 嗎？
是的，Aspose.PDF for .NET 支援多個 .NET 平台，包括 .NET Framework、.NET Core 等。

### Aspose.PDF 有免費試用版嗎？
絕對地！您可以下載免費試用版 [這裡](https://releases。aspose.com/).

### 標題支援哪些圖像格式？
Aspose.PDF 支援大多數常見的圖片格式，如頁首和頁尾的 JPG、PNG 和 BMP。

### 我可以自訂頁碼格式嗎？
是的，您可以根據需要輕鬆自訂頁腳文字和格式。

### 有技術支援嗎？
是的，Aspose 透過其論壇提供專門支援。您可以尋求協助 [這裡](https://forum。aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}