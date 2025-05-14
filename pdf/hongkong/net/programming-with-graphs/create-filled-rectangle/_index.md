---
"description": "透過本逐步教學了解如何使用 Aspose.PDF for .NET 在 PDF 中建立填滿矩形。適合各個層級的開發人員。"
"linktitle": "建立填滿矩形"
"second_title": "Aspose.PDF for .NET API參考"
"title": "建立填滿矩形"
"url": "/zh-hant/net/programming-with-graphs/create-filled-rectangle/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 建立填滿矩形

## 介紹

您是否曾經想過以程式設計方式建立具有視覺吸引力的 PDF？如果是這樣，那麼您來對地方了！在本教學中，我們將深入了解 Aspose.PDF for .NET 的世界，這是一個功能強大的程式庫，可讓您輕鬆操作 PDF 文件。今天，我們將重點介紹如何在 PDF 文件中建立填充矩形。無論您是經驗豐富的開發人員還是剛起步，本指南都將以友好且引人入勝的方式引導您完成每個步驟。那麼，戴上你的編碼帽，讓我們開始吧！

## 先決條件

在我們進入程式碼之前，您需要做好以下幾件事：

1. Visual Studio：確保您的機器上安裝了 Visual Studio。這是一個出色的 .NET 開發 IDE。
2. Aspose.PDF for .NET：您需要下載並安裝 Aspose.PDF 庫。你可以找到它 [這裡](https://releases。aspose.com/pdf/net/).
3. C# 基礎知識：稍微熟悉一下 C# 程式設計將有助於您更好地理解程式碼片段。

## 導入包

首先，您需要在 C# 專案中匯入必要的套件。您可以按照以下步驟操作：

### 建立新專案

開啟 Visual Studio 並建立一個新的 C# 專案。為了簡單起見，您可以選擇控制台應用程式。

### 新增 Aspose.PDF 參考

1. 在解決方案資源管理器中以滑鼠右鍵按一下您的專案。
2. 選擇“管理 NuGet 套件”。
3. 搜尋“Aspose.PDF”並安裝最新版本。

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

現在我們已經設定好了一切，讓我們深入研究程式碼！

## 步驟 1：設定文檔目錄

首先，您需要指定儲存 PDF 的路徑。這很關鍵，因為它告訴程式在哪裡建立文件。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

代替 `"YOUR DOCUMENT DIRECTORY"` 使用您想要儲存 PDF 的機器上的實際路徑。

## 步驟 2：建立文件實例

接下來，我們將創建一個 `Document` 班級。此類代表您將要處理的 PDF 文件。

```csharp
// 建立 Document 實例
Document doc = new Document();
```

此行初始化一個我們可以操作的新 PDF 文件。

## 步驟 3：新增頁面

現在，讓我們為文件新增一個頁面。每個 PDF 至少需要一頁，對嗎？

```csharp
// 將頁面新增至 PDF 檔案的頁面集合
Page page = doc.Pages.Add();
```

此程式碼為文件新增了一個新頁面，允許我們在其上繪製形狀。

## 步驟 4：建立圖形實例

要繪製形狀，我們需要建立一個 `Graph` 實例。可以將圖表想像成一塊畫布，您可以在上面繪製各種形狀。

```csharp
// 建立 Graph 實例
Aspose.Pdf.Drawing.Graph graph = new Aspose.Pdf.Drawing.Graph(100.0, 400.0);
```

這裡，我們建立一個寬度為 100、高度為 400 的圖表。

## 步驟 5：將圖表新增至頁面

現在我們有了圖表，讓我們將其添加到我們之前創建的頁面中。

```csharp
// 將圖形物件加入到頁面實例的段落集合中
page.Paragraphs.Add(graph);
```

此行將圖形附加到頁面上，以便可以進行繪製。

## 步驟 6：建立矩形實例

接下來，我們將建立一個想要填滿顏色的矩形。

```csharp
// 建立 Rectangle 實例
Aspose.Pdf.Drawing.Rectangle rect = new Aspose.Pdf.Drawing.Rectangle(100, 100, 200, 120);
```

在這段程式碼中，我們定義了矩形的位置和大小。參數代表 x 和 y 座標、寬度和高度。

## 步驟 7：指定填滿顏色

現在，讓我們為矩形選擇一種顏色。在這個例子中，我們將用紅色填滿它。

```csharp
// 指定圖形物件的填滿顏色
rect.GraphInfo.FillColor = Aspose.Pdf.Color.Red;
```

此行將矩形的填滿顏色設定為紅色。您可以選擇任何您喜歡的顏色！

## 步驟 8：將矩形加入圖形中

矩形準備好後，就可以將其添加到圖表中了。

```csharp
// 將矩形物件新增至圖形物件的形狀集合中
graph.Shapes.Add(rect);
```

此程式碼將矩形新增到圖形中，使其成為我們繪圖的一部分。

## 步驟9：儲存PDF文檔

最後，我們需要將文檔儲存到指定的目錄。

```csharp
dataDir = dataDir + "CreateFilledRectangle_out.pdf";
// 儲存 PDF 文件
doc.Save(dataDir);
```

此代碼將 PDF 檔案儲存為 `CreateFilledRectangle_out.pdf` 在您之前指定的目錄中。

## 步驟10：確認訊息

為了讓我們知道一切進展順利，我們可以列印一條確認訊息。

```csharp
Console.WriteLine("\nFilled rectangle object created successfully.\nFile saved at " + dataDir);
```

此行將在控制台中輸出一條訊息，確認已成功建立填充矩形。

## 結論

就是這樣！您已成功使用 Aspose.PDF for .NET 在 PDF 文件中建立了一個填滿矩形。這個強大的函式庫為 PDF 操作開闢了無限可能，讓您能夠以程式設計方式建立令人驚嘆的文件。無論您產生報告、發票或任何其他類型的 PDF，Aspose.PDF 都能滿足您的需求。

## 常見問題解答

### 什麼是 Aspose.PDF for .NET？
Aspose.PDF for .NET 是一個函式庫，可讓開發人員以程式設計方式建立、操作和轉換 PDF 文件。

### 我可以免費使用 Aspose.PDF 嗎？
是的，Aspose 提供免費試用版，您可以使用它來探索該程式庫的功能。你可以下載 [這裡](https://releases。aspose.com/).

### 有沒有辦法獲得對 Aspose.PDF 的支援？
絕對地！您可以透過 Aspose 論壇獲得支持 [這裡](https://forum。aspose.com/c/pdf/10).

### 我該如何購買 Aspose.PDF？
您可以透過造訪購買頁面購買 Aspose.PDF [這裡](https://purchase。aspose.com/buy).

### 我可以使用 Aspose.PDF 建立哪些類型的形狀？
您可以使用 Aspose.PDF 庫建立各種形狀，包括矩形、圓形、線條等。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}