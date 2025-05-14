---
"description": "按照本逐步指南，使用 Aspose.PDF for .NET 輕鬆地將自訂註解新增至您的 PDF 中。使用特定細節和圖示自訂您的註釋。"
"linktitle": "新增註釋"
"second_title": "Aspose.PDF for .NET API參考"
"title": "新增 PDF 註釋"
"url": "/zh-hant/net/annotations/addannotation/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 新增 PDF 註釋

## 介紹

註釋是豐富 PDF 文件的好方法，使其具有互動性和資訊量。無論您是為合作者留下註釋還是為讀者添加額外信息，註釋都是必不可少的。在本教學中，我們將深入研究使用 Aspose.PDF for .NET 新增 PDF 註解的過程。我們將分解每個步驟，以便在完成本指南後，您將能夠在 PDF 文件中嵌入註釋。讓我們開始吧！

## 先決條件

在深入研究程式碼之前，請確保您擁有所需的一切：

- Aspose.PDF for .NET：請確定您已安裝 Aspose.PDF 庫。您可以從 [Aspose.PDF for .NET下載頁面](https://releases。aspose.com/pdf/net/).
- 開發環境：Visual Studio 或您選擇的任何其他 C# IDE。
- C# 基礎知識：本指南假設您熟悉 C# 程式設計。
- PDF 文件：您將新增註釋的範例 PDF 文件。

如果你還沒有 Aspose.PDF 庫，你可以從上面的連結取得它並開始 [免費試用](https://releases.aspose.com/) 或購買 [執照](https://purchase。aspose.com/buy). 

## 導入包

在開始編碼之前，請確保已匯入必要的命名空間：

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
```

這些命名空間提供對 PDF 操作和註釋所需的類別和方法的存取。

## 步驟 1：載入 PDF 文檔

首先，您需要載入您計劃新增註釋的 PDF 文件。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DATA DIRECTORY";
// 開啟文件
Document pdfDocument = new Document(dataDir + "AddAnnotation.pdf");
```

事情是這樣的：你指定 PDF 檔案的儲存目錄，然後使用 `Document` Aspose.PDF 提供的類別。這一步至關重要，因為如果不載入文檔，您就無法對其進行任何更改。

## 步驟 2：建立註釋

### 定義註釋屬性
現在，讓我們建立註釋本身。我們將使用 `TextAnnotation`，非常適合為您的 PDF 添加評論或註釋。

```csharp
// 建立註釋
TextAnnotation textAnnotation = new TextAnnotation(pdfDocument.Pages[1], new Aspose.Pdf.Rectangle(200, 400, 400, 600));
textAnnotation.Title = "Sample Annotation Title";
textAnnotation.Subject = "Sample Subject";
textAnnotation.Contents = "Sample contents for the annotation";
textAnnotation.Open = true;
textAnnotation.Icon = TextIcon.Key;
```

在此程式碼片段中：
- 位置和大小： `Rectangle` 類別定義註解在頁面上出現的位置及其尺寸。
- 標題、主題和內容：這些屬性可讓您指定註釋的內容和內容。
- 圖示: `TextIcon.Key` 為註釋設定圖標，使其更具視覺吸引力。

## 步驟 3：自訂註解的外觀

接下來，讓我們透過添加邊框並調整其外觀來使該註釋脫穎而出。

```csharp
Border border = new Border(textAnnotation);
border.Width = 5;
border.Dash = new Dash(1, 1);
textAnnotation.Border = border;
textAnnotation.Rect = new Aspose.Pdf.Rectangle(200, 400, 400, 600);
```

以下是正在發生的事情的詳細說明：
- 邊界：我們創建一個 `Border` 物件並將其寬度設為 5，為我們的註釋提供突出的輪廓。
- 虛線圖案： `Dash` 屬性可讓您建立虛線邊框，為註解添加一點樣式。

## 步驟 4：將註解新增至 PDF 頁面

建立和自訂註釋後，就可以將其新增至您的 PDF 頁面了。

```csharp
// 將註釋加入到頁面的註釋集合中
pdfDocument.Pages[1].Annotations.Add(textAnnotation);
```

此程式碼將註解新增至 PDF 的第一頁。這 `Annotations` 集合包含特定頁面的所有註釋，此步驟可確保您的新註釋是該集合的一部分。

## 步驟5：儲存更新的PDF文檔

最後，讓我們保存文檔，以便永久添加您的註釋。

```csharp
// 儲存輸出檔案
dataDir = dataDir + "AddAnnotation_out.pdf";
pdfDocument.Save(dataDir);
Console.WriteLine("\nAnnotation added successfully.\nFile saved at " + dataDir);
```

透過使用新名稱儲存文件（`AddAnnotation_out.pdf`)，則保留原始文件並產生一個新增了註釋的新文件。控制台訊息確認一切成功，您現在可以在指定的目錄中找到帶有註釋的 PDF。

## 結論

在 PDF 中加入註解不只是一個強大的功能；使用 Aspose.PDF for .NET 也非常簡單。無論您是在標記文件以供審閱還是添加註釋以供將來參考，本指南都涵蓋了您需要了解的所有內容。透過遵循這些步驟，您可以建立自訂註釋來豐富您的 PDF，使其更加實用和互動。

## 常見問題解答

### 我可以使用 Aspose.PDF for .NET 新增哪些類型的註解？
您可以新增各種類型的註釋，包括文字、連結、突出顯示和圖章註釋等。

### 我可以自訂註釋的外觀嗎？
絕對地！您可以自訂註釋的大小、顏色、邊框甚至圖示。

### 是否可以在單一頁面上新增多個註解？
是的，您可以根據需要在 PDF 中的任何頁面中添加任意數量的註釋。

### 新增註釋後可以刪除嗎？
是的，可以使用 `Annotations.Delete` Aspose.PDF 提供的方法。

### 我需要許可證才能使用 Aspose.PDF for .NET 嗎？
是的，要解鎖所有功能並避免任何限制，您需要 [執照](https://purchase.aspose.com/buy)。您還可以獲得 [臨時執照](https://purchase.aspose.com/temporary-license/) 以供評估。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}