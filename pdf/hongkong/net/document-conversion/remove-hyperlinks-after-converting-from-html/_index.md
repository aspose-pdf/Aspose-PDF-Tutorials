---
"description": "在本逐步指南中了解如何使用 Aspose.PDF for .NET 將 HTML 文件轉換為 PDF 後從 HTML 文件中刪除超連結。"
"linktitle": "從 HTML 轉換後刪除超鏈接"
"second_title": "Aspose.PDF for .NET API參考"
"title": "從 HTML 轉換後刪除超鏈接"
"url": "/zh-hant/net/document-conversion/remove-hyperlinks-after-converting-from-html/"
"weight": 250
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 從 HTML 轉換後刪除超鏈接

## 介紹

在數位時代，將 HTML 文件轉換為 PDF 是一項常見的任務。但是，有時您可能出於各種原因想要從轉換後的 PDF 中刪除超鏈接，例如增強可讀性或防止不必要的導航。在本教學中，我們將探討如何使用 Aspose.PDF for .NET 來實現這一點。 

## 先決條件

在深入研究程式碼之前，請確保您符合以下先決條件：

1. Visual Studio：確保您的機器上安裝了 Visual Studio。這將是您的開發環境。
2. Aspose.PDF for .NET：您需要有 Aspose.PDF 函式庫。您可以從下載 [這裡](https://releases。aspose.com/pdf/net/).
3. C# 基礎知識：熟悉 C# 程式設計將幫助您更好地理解程式碼。

## 導入包

首先，您需要在 C# 專案中匯入必要的套件。您可以按照以下步驟操作：

1. 開啟您的 Visual Studio 專案。
2. 在解決方案資源管理器中右鍵單擊您的專案並選擇“管理 NuGet 套件”。
3. 搜尋 `Aspose.PDF` 並安裝它。

```csharp
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
using System.IO;
```

現在您已完成所有設置，讓我們分解一下將 HTML 文件轉換為 PDF 後從中刪除超連結的過程。

## 步驟 1：設定文檔目錄

首先，您需要指定文檔目錄的路徑。這是您的 HTML 檔案所在的位置，也是輸出 PDF 的儲存位置。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

代替 `"YOUR DOCUMENT DIRECTORY"` 使用儲存 HTML 檔案的實際路徑。

## 步驟2：載入HTML文檔

接下來，您將使用 `Document` 來自 Aspose.PDF 的類別。該類別允許您輕鬆處理 PDF 文件。

```csharp
Document doc = new Document(dataDir + "SampleHtmlFile.html", new HtmlLoadOptions());
```

這裡，我們加載名為 `SampleHtmlFile.html`。確保該檔案存在於您指定的目錄中。

## 步驟3：將文件儲存到記憶體流

在開始處理註解之前，我們需要將文件儲存到記憶體流中。此步驟至關重要，因為它為文件的進一步操作做好了準備。

```csharp
doc.Save(new MemoryStream());
```

此行將文件保存在記憶體中，使我們能夠使用它而無需將其寫入磁碟。

## 步驟 4：迭代註釋

現在，我們將遍歷文件中的註釋。註釋是類似連結、評論和突出顯示的元素。我們對連結註釋特別感興趣。

```csharp
foreach (Annotation a in doc.Pages[1].Annotations)
{
    if (a.AnnotationType == AnnotationType.Link)
    {
        // 處理連結註釋
    }
}
```

在這個循環中，我們檢查註解類型是否是連結。如果是，我們繼續下一步。

## 步驟5：刪除超連結操作

對於每個連結註釋，我們需要檢查它是否具有超連結動作。如果是，我們將透過將其 URI 設為空字串來刪除超連結。

```csharp
LinkAnnotation la = (LinkAnnotation)a;
if (la.Action is GoToURIAction)
{
    GoToURIAction gta = (GoToURIAction)la.Action;
    gta.URI = "";
```

此程式碼片段確保有效刪除超連結操作。

## 步驟6：吸收文字片段

接下來，我們將吸收與連結註釋相關的文字片段。這使我們能夠操縱文字的外觀。

```csharp
TextFragmentAbsorber tfa = new TextFragmentAbsorber();
tfa.TextSearchOptions = new TextSearchOptions(a.Rect);
doc.Pages[a.PageIndex].Accept(tfa);
```

在這裡，我們創建一個 `TextFragmentAbsorber` 並將其搜尋選項設為註釋的矩形。這有助於我們找到連結的文字。

## 步驟 7：修改文字外觀

一旦我們有了文字片段，我們就可以修改它們的外觀。在這種情況下，我們將刪除下劃線並將文字顏色變更為黑色。

```csharp
foreach (TextFragment tf in tfa.TextFragments)
{
    tf.TextState.Underline = false;
    tf.TextState.ForegroundColor = Color.Black;
}
```

此步驟透過刪除超連結樣式來增強文字的可讀性。

## 步驟 8：刪除註釋

修改文字後，我們可以安全地從文件中刪除連結註解。

```csharp
doc.Pages[a.PageIndex].Annotations.Delete(a);
}
```

此行從 PDF 中刪除超鏈接，確保它不再存在於最終輸出中。

## 步驟9：儲存修改後的文檔

最後，我們需要將修改後的文件儲存為新的PDF檔案。這是我們流程的最後一步。

```csharp
doc.Save(dataDir + "RemoveHyperlinksFromText_out.pdf");
```

此行保存文件並刪除超鏈接，建立一個名為 `RemoveHyperlinksFromText_out。pdf`.

## 結論

就是這樣！使用 Aspose.PDF for .NET 將 HTML 文件轉換為 PDF 後，您已成功從中刪除超連結。此過程不僅可以增強 PDF 的可讀性，還可以讓您控制所呈現的內容。 

## 常見問題解答

### 我可以從任何 PDF 文件中刪除超連結嗎？
是的，您可以使用 Aspose.PDF for .NET 從任何 PDF 文件中刪除超連結。

### Aspose.PDF 可以免費使用嗎？
Aspose.PDF 提供免費試用，但要使用全部功能，您需要購買授權。檢查 [購買頁面](https://purchase。aspose.com/buy).

### 如果我在使用 Aspose.PDF 時遇到問題怎麼辦？
您可以在 [支援論壇](https://forum。aspose.com/c/pdf/10).

### 我可以使用 Aspose 將其他文件格式轉換為 PDF 嗎？
是的，Aspose 支援各種文件格式轉換為 PDF。

### 哪裡可以下載 Aspose.PDF for .NET？
您可以從 [下載連結](https://releases。aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}