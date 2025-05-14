---
"description": "透過本完整的逐步指南了解如何使用 Aspose.PDF for .NET 將影像儲存在 XImage 集合中。"
"linktitle": "將影像儲存在 XImage 集合中"
"second_title": "Aspose.PDF for .NET API參考"
"title": "將影像儲存在 XImage 集合中"
"url": "/zh-hant/net/programming-with-images/store-image-in-ximage-collection/"
"weight": 290
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 將影像儲存在 XImage 集合中

## 介紹

在當今的數位時代，以程式設計方式處理和操作文件對於許多應用程式來說至關重要。 Aspose.PDF for .NET 可讓開發人員輕鬆處理 PDF 文件，增強工作流程並支援建立動態內容。在本指南中，我們將深入研究將影像儲存在 XImage 集合中的流程，這是一項重要功能，可讓您將視覺效果直接嵌入到 PDF 中。準備踏上創造精彩內容的旅程。

## 先決條件

在深入研究程式碼和流程之前，您需要確保已做好以下幾件事：

- .NET 環境：您的機器上應該安裝 .NET Framework。根據您的專案要求選擇適當的版本。
- Aspose.PDF for .NET：請確定您有 Aspose.PDF 庫。您可以從下載 [這裡](https://releases.aspose.com/pdf/net/) 或開始免費試用 [這裡](https://releases。aspose.com/).
- 圖像檔案：您還需要一個想要儲存在 PDF 中的圖像檔案（如 JPG 或 PNG）。對於此範例，我們將使用名為“aspose-logo.jpg”的檔案。
- 對 C# 的基本了解：熟悉 C# 程式設計將幫助您順利完成。

## 導入包

要開始使用 Aspose.PDF for .NET，您需要匯入所需的命名空間。此步驟為利用庫提供的所有功能奠定了基礎。

```csharp
using System;
using System.IO;
using Aspose.Pdf.Operators;
```

透過匯入這些命名空間，您可以啟用 Aspose.PDF 中的各種功能，包括文件建立、影像處理等。

讓我們將其分解為易於管理的步驟，以便您更輕鬆地遵循。

## 步驟 1：設定文檔目錄

你需要做的第一件事是什麼？定義您的文件存放的位置。您需要設定一個變數來保存文檔目錄的路徑。這是您的 PDF 的保存位置。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // 替換為您的實際文件目錄。
```

## 第 2 步：初始化文檔

現在，是時候建立一個新的 PDF 文件了。這一步讓您的 PDF 變得生動起來。 

```csharp
Aspose.Pdf.Document document = new Document();
```

在這裡，我們實例化一個新的 Document 物件作為我們的畫布。

## 步驟 3：新增頁面

每個傑作都需要一塊畫布，對嗎？在我們的例子中，我們需要在文件中處理一個頁面。

```csharp
document.Pages.Add();
Page page = document.Pages[1]; // 取得第一頁。
```

我們正在為文件新增頁面。現在我們就對這個頁面進行操作。

## 步驟4：載入圖片文件

接下來，您需要將圖像載入到程式中。這一步和打開一本書閱讀很相似；您需要先訪問該內容，然後才能使用它。

```csharp
using (FileStream imageStream = new FileStream(dataDir + "aspose-logo.jpg", FileMode.Open))
{
```

此行將圖像檔案作為流打開，這使我們能夠操作它並將其嵌入到 PDF 中。

## 步驟5：將圖像新增至頁面資源

現在您已經準備好圖像，是時候將其添加到頁面資源中了，本質上就是告訴 PDF，“嘿，我有一張很酷的圖像希望你記住！”

```csharp
page.Resources.Images.Add(imageStream, ImageFilterType.Flate);
XImage ximage = page.Resources.Images[page.Resources.Images.Count];
```

此程式碼負責將圖像新增至 PDF 並將其分配給 `XImage` 我們稍後可以引用的變數。

## 步驟6：準備繪製影像

接下來是有趣的部分——在頁面上定位圖像。您需要設定座標，以便將圖像準確地放置在您想要的位置。

```csharp
page.Contents.Add(new GSave());
```

此行保存圖形狀態以供稍後恢復。這就像在我們改變任何事情之前拍攝事物設定情況的快照。

## 步驟 7：定義影像位置和大小

現在，定義您想要放置影像的大小和位置：

```csharp
int lowerLeftX = 0;
int lowerLeftY = 0;
int upperRightX = 600;
int upperRightY = 600;
Aspose.Pdf.Rectangle rectangle = new Aspose.Pdf.Rectangle(lowerLeftX, lowerLeftY, upperRightX, upperRightY);
```

此程式碼區塊設定了影像所適合的矩形的尺寸，本質上是為影像在頁面上提供了一個位置。

## 步驟 8：建立變換矩陣 

為了控制影像的放置方式，我們將定義一個變換矩陣。這決定了圖像在目標座標上的顯示方式。

```csharp
Matrix matrix = new Matrix(new double[] { rectangle.URX - rectangle.LLX, 0, 0, rectangle.URY - rectangle.LLY, rectangle.LLX, rectangle.LLY });
```

可以把這想像成在您踏上旅程之前繪製一張地圖。它有助於確定圖像在頁面上的顯示方式。

## 步驟 9：將圖像放置在頁面上

現在，是時候真正告訴 PDF 將圖像放在哪裡了。

```csharp
page.Contents.Add(new ConcatenateMatrix(matrix));
page.Contents.Add(new Do(ximage.Name));
page.Contents.Add(new GRestore());
```

在這裡，我們為 PDF 的內容流添加命令，這些命令將根據我們剛剛建立的矩陣實際繪製圖像。

## 步驟10：儲存文檔

最後，我們可以儲存我們的傑作了！這是您所有的辛勤工作匯聚成有形成果的時刻。

```csharp
document.Save(dataDir + "FlateDecodeCompression.pdf");
```

您已告訴 Aspose.PDF 使用提供的檔案名稱儲存文件。執行此程式碼時，您會在指定目錄中找到新建立的 PDF 文件，其中包含嵌入的圖像。

## 結論

就是這樣！您已經了解如何使用 Aspose.PDF for .NET 將影像逐點儲存在 XImage 集合中。看到自己的程式碼成形並產生一些有用的東西，難道不令人欣慰嗎？無論您是建立應用程式還是僅希望自動化報告，本指南都是很好的基礎。請記住，Aspose.PDF 的強大功能可以幫助您完成以外的多項任務，因此請繼續探索！

## 常見問題解答

### Aspose.PDF 支援哪些影像檔案格式？
Aspose.PDF 支援各種影像格式，包括 JPG、PNG、BMP 和 GIF。

### 將圖像新增至 PDF 時我可以更改其大小嗎？
是的，透過調整矩形中定義的座標，您可以變更 PDF 中顯示的圖像的大小。

### 我需要許可證才能使用 Aspose.PDF 嗎？
Aspose 提供免費試用和多種購買選擇。你可以找到它們 [這裡](https://purchase。aspose.com/buy).

### 如果我遇到問題，如何獲得支援？
您可以向 Aspose 社群尋求協助 [這裡](https://forum。aspose.com/c/pdf/10).

### 有沒有辦法對新增到 PDF 的影像套用壓縮？
是的，當向 PDF 新增圖像時，您可以指定圖像過濾器類型以使用 Flate 等壓縮方法。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}