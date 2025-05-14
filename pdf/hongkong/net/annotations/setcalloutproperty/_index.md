---
"description": "透過本詳細的逐步教學，了解如何使用 Aspose.PDF for .NET 設定 PDF 檔案中的標註屬性。"
"linktitle": "在 PDF 檔案中設定標註屬性"
"second_title": "Aspose.PDF for .NET API參考"
"title": "在 PDF 檔案中設定標註屬性"
"url": "/zh-hant/net/annotations/setcalloutproperty/"
"weight": 130
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 檔案中設定標註屬性

## 介紹

創建專業且具有視覺吸引力的 PDF 文件通常需要添加註釋來吸引人們對特定內容的注意。其中一種註釋是標註，就像您在漫畫中看到的氣泡一樣。它們有助於澄清或強調 PDF 中的文字。 Aspose.Pdf for .NET 使得在您的文件中添加此類註釋變得非常容易，在本教程中，我們將介紹如何使用這個強大的庫在 PDF 文件中設定標註屬性。無論您是經驗豐富的開發人員還是剛起步，在閱讀完本指南後，您將清楚地了解如何處理 PDF 文件中的標註。

## 先決條件

在深入研究程式碼之前，讓我們先介紹一下入門所需的基本知識。

1. Aspose.PDF for .NET：請確定您已安裝 Aspose.PDF for .NET 程式庫。您可以從下載 [這裡](https://releases。aspose.com/pdf/net/).
2. IDE：開發環境，例如 Visual Studio。
3. .NET Framework：確保您的機器上安裝了 .NET。
4. 臨時許可證：如果您想不受限制地試用 Aspose.PDF 的全部功能，請取得 [臨時執照](https://purchase。aspose.com/temporary-license/).

## 導入包

在開始編寫程式碼之前，您需要匯入必要的套件，以便處理 PDF 文件和註釋。

```csharp
using Aspose.Pdf.Annotations;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
```

這些匯入將為您提供操作 PDF 文件和建立標註等註釋所需的所有類別和方法。

## 步驟 1：初始化 PDF 文檔

我們旅程的第一步是初始化一個新的 PDF 文檔，我們將在其中添加標註註釋。可以將其視為設定空白畫布，您可以在其中開始添加元素。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";

// 初始化新的 PDF 文檔
Document doc = new Document();
```
在這裡，我們正在創建一個新的 `Document` 物件將作為我們的 PDF 文件。這 `dataDir` 變數設定為完成後您想要儲存 PDF 檔案的目錄。

## 步驟 2：為文件新增頁面

PDF 文件可以有多個頁面，在此步驟中，我們將在文件中新增一個新頁面。此頁面將是放置我們的標註註釋的地方。

```csharp
// 新增頁面
Page page = doc.Pages.Add();
```
這 `Pages.Add()` 方法用於向 `doc` 目的。新頁面儲存在 `page` 變量，我們稍後在添加註釋時會用到它。

## 步驟 3：定義預設外觀

註釋（例如標註）具有可自訂的視覺外觀。在此步驟中，我們將定義標註內的文字的外觀。

```csharp
// 定義註釋的預設外觀
DefaultAppearance da = new DefaultAppearance();
da.TextColor = System.Drawing.Color.Red;
da.FontSize = 10;
```
我們創建了一個 `DefaultAppearance` 定義文字顏色和字體大小的物件。此處，文字將為紅色，字體大小設定為 10。此外觀將應用於標註註釋。

## 步驟 4：建立自由文字註釋

現在是時候創建實際的註釋了。自由文字註釋允許我們添加帶有特定文字和樣式的標註。

```csharp
// 建立帶有標註的 FreeTextAnnotation
FreeTextAnnotation fta = new FreeTextAnnotation(page, new Rectangle(422.25, 645.75, 583.5, 702.75), da);
fta.Intent = FreeTextIntent.FreeTextCallout;
fta.EndingStyle = LineEnding.OpenArrow;
```
我們創建了一個 `FreeTextAnnotation` 具有特定座標的對象，定義其在頁面上的位置。這 `Intent` 設定為 `FreeTextCallout`，表示這是一個標註註釋。這 `EndingStyle` 設定為 `OpenArrow`，這意味著標註線將以開放的箭頭結束。

## 步驟 5：定義標註線點

標註註釋有一條指向感興趣區域的線。在這裡，我們將定義構成這條線的點。

```csharp
// 定義標註線的點
fta.Callout = new Point[]
{
    new Point(428.25, 651.75), 
    new Point(462.75, 681.375), 
    new Point(474, 681.375)
};
```
這 `Callout` 屬性是一個數組 `Point` 對象，每個對象代表頁面上的一個座標。這些點定義了標註線的路徑，使其具有經典的氣泡外觀。

## 步驟 6：在頁面上新增註釋

建立和配置我們的註釋後，下一步是將其新增至頁面。

```csharp
// 將註釋新增至頁面
page.Annotations.Add(fta);
```
這 `Annotations.Add()` 方法用於將註釋放置在我們之前建立的頁面上。此步驟有效地在 PDF 頁面上「繪製」標註。

## 步驟 7：設定富文本內容

標註註釋可以包含富文本，允許在氣泡內格式化內容。讓我們添加一些範例文字。

```csharp
// 設定註釋的富文本
fta.RichText = "<body xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:xfa=\"http://www.xfa.org/schema/xfa-data/1.0/\" xfa:APIVersion=\"Acrobat:11.0.23\" xfa:spec=\"2.0.2\" style=\"color:#FF0000;font-weight:normal;font-style:normal;font-stretch:normal\"><p dir=\"ltr\"><span style=\"font-size:9.0pt;font-family:Helvetica\">這是一個例子></bodyspan></p></pbody>;
```
這 `RichText` 屬性是用 HTML 內容設定的。這允許在標註內進行詳細的格式化，例如指定字體大小、顏色和樣式。

## 步驟 8：儲存 PDF 文檔

最後，設定完一切後，我們需要儲存文件。此步驟完成了帶有標註註釋的 PDF 的建立。

```csharp
// 儲存文件
doc.Save(dataDir + "SetCalloutProperty.pdf");
```
這 `Save()` 方法將文件儲存到指定目錄，檔案名稱為「SetCalloutProperty.pdf」。此步驟結束了我們的 PDF 建立流程。

## 結論

就是這樣！您剛剛使用 Aspose.PDF for .NET 建立了一個帶有標註的 PDF 文件。此註釋對於突出顯示或解釋文件的特定部分非常有用。 Aspose.PDF 提供了強大的 API，讓 PDF 操作變得簡單又靈活。無論您是新增註解、轉換文件還是處理複雜的 PDF 任務，Aspose.PDF 都能滿足您的需求。

## 常見問題解答

### 我可以進一步自訂標註的外觀嗎？

絕對地！您可以自訂線條顏色、粗細以及文字的字體系列和樣式等各個方面。

### 是否可以在單一頁面上新增多個標註？

是的，您可以透過對每個註釋重複這些步驟來新增所需數量的標註。

### 如何更改標註的位置？

只需修改 `Rectangle` 和 `Callout` 屬性來重新定位註釋。

### 我可以使用 Aspose.PDF 新增其他類型的註解嗎？

是的，Aspose.PDF 支援各種註解類型，包括高亮、圖章和文件附件。

### 富文本內容是否僅限於 HTML？

這 `RichText` 屬性支援 HTML 子集，可讓您包含樣式文字和基本格式。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}