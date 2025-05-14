---
"description": "透過本逐步教學（附有詳細的程式碼範例），了解如何使用 Aspose.PDF for .NET 從 PDF 中的印章註解中提取文字。"
"linktitle": "從圖章註釋中提取文本"
"second_title": "Aspose.PDF for .NET API參考"
"title": "從圖章註釋中提取文本"
"url": "/zh-hant/net/programming-with-stamps-and-watermarks/extract-text-from-stamp-annotation/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 從圖章註釋中提取文本

## 介紹

處理 PDF 文件時，從註釋中提取文字等特定資料非常方便。在本教學中，我們將逐步指導您如何使用 Aspose.PDF for .NET 從 PDF 文件中的印章註釋中提取文字。這個強大的函式庫允許開發人員操作 PDF 文件，實現文字擷取、註解管理等任務。讓我們深入了解細節並將其全部分解！

## 先決條件

在開始本教學之前，您需要準備一些東西：

- Aspose.PDF for .NET：您需要安裝 Aspose.PDF for .NET。你可以 [點此下載最新版本](https://releases。aspose.com/pdf/net/).
- Visual Studio：本指南假設您使用 Visual Studio 作為整合開發環境 (IDE)。
- C# 基礎知識：您應該對 C# 程式設計有基本的了解。

確保您已設定這些工具，以便您可以按照本教學進行操作。

## 導入包

任何 .NET 專案的第一步都是導入必要的命名空間。使用 Aspose.PDF，您只需要匯入幾個關鍵檔案即可開始使用：

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
```

這些匯入帶來了處理 PDF 文件、註釋和文字擷取所需的功能。

讓我們來看看從郵票註釋中提取文字的過程。這將涉及加載 PDF 文件、識別印章註釋以及提取文字內容。

## 步驟 1：載入 PDF 文檔

您需要做的第一件事是載入印章註釋所在的 PDF 檔案。在此範例中，我們將從您的本機目錄載入範例 PDF 檔案。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document(dataDir + "test.pdf");
```

這裡我們使用 `Document` Aspose.PDF 提供的類別來開啟 PDF 檔案並與之互動。這 `dataDir` 變數代表檔案的路徑。代替 `"YOUR DOCUMENT DIRECTORY"` 使用您的 PDF 儲存的實際路徑。

## 第 2 步：辨識圖章註釋

PDF 註釋透過其類型和文件中的位置來識別。在我們的例子中，我們想要在特定頁面上找到印章註釋。具體操作如下：

```csharp
StampAnnotation annot = doc.Pages[1].Annotations[3] as StampAnnotation;
```

在這行程式碼中：
- `doc.Pages[1]`：存取文件的第一頁。
- `Annotations[3]`：指的是頁面上的第四個註釋（因為索引從 0 開始）。
- `as StampAnnotation`：將註釋轉換為 `StampAnnotation` 對象，這是我們正在處理的註釋的特定類型。

## 步驟3：建立文字吸收器

要從印章註釋中提取文本，我們需要使用文本吸收器。此工具將幫助我們吸收或捕獲 PDF 特定區域的文本，在本例中為註釋。

```csharp
TextAbsorber ta = new TextAbsorber();
```

這 `TextAbsorber` 該類別用於從文件的任何部分提取文本，我們將使用它來定位註釋的外觀。

## 步驟4：提取印章註釋的外觀

PDF 中的印章註釋具有相關外觀，通常以 XForm 的形式儲存。我們需要檢索此外觀以存取郵票內的實際文字。

```csharp
XForm ap = annot.Appearance["N"];
```

這裡：
- `annot.Appearance["N"]`：檢索名為“N”的外觀流（代表註釋的正常外觀）。

## 步驟5：提取文字內容

現在我們有了外觀，我們可以使用 `TextAbsorber` 參觀外觀並捕獲文字。

```csharp
ta.Visit(ap);
```

這 `Visit` 方法允許 `TextAbsorber` 分析外觀並提取其中嵌入的任何文字內容。

## 步驟6：顯示提取的文本

最後，一旦提取了文本，我們就可以將其輸出到控制台或儲存以供進一步使用。

```csharp
Console.WriteLine(ta.Text);
```

這行簡單的程式碼在控制台視窗中顯示提取的文字。您也可以根據需要將其儲存到文件中或進一步操作。

## 結論

使用 PDF 文件中的註釋（尤其是圖章註釋）可以為您的應用程式添加重要的功能。使用 Aspose.PDF for .NET，您將擁有一套強大的工具，可以輕鬆提取資料、操作註釋以及以有意義的方式與 PDF 互動。在本教程中，我們向您展示瞭如何透過幾個簡單的步驟從印章註釋中提取文字。現在輪到您在專案中試驗這些功能了！

## 常見問題解答

### 我可以使用 Aspose.PDF 從其他類型的註解中提取文字嗎？  
是的，Aspose.PDF 允許您從各種類型的註釋中提取文本，例如文本註釋、自由文本註釋等，而不僅僅是圖章註釋。

### Aspose.PDF 是否支援新增自訂註解？  
絕對地！ Aspose.PDF 支援為 PDF 文件建立和新增自訂註釋，讓您可以靈活地管理和呈現資料。

### 我可以從郵票註釋中提取圖像嗎？  
是的，您可以透過存取外觀和檢索圖像數據，使用類似的方法從印章註釋中提取圖像。

### Aspose.PDF for .NET 也提供哪些其他功能？  
Aspose.PDF for .NET 提供了廣泛的功能，包括文字操作、表單欄位處理、文件轉換等等。

### Aspose.PDF for .NET 免費嗎？  
Aspose.PDF for .NET 提供免費試用，但要存取全套功能，您需要購買許可證。您還可以申請 [臨時執照](https://purchase。aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}