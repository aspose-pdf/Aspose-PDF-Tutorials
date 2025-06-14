---
"description": "使用 Aspose.PDF for .NET 建立包含文字和圖像的 PDF。了解如何逐步新增文字和內嵌影像。"
"linktitle": "PDF 檔案中的文字和圖像作為段落"
"second_title": "Aspose.PDF for .NET API參考"
"title": "PDF 檔案中的文字和圖像作為段落"
"url": "/zh-hant/net/programming-with-text/text-and-image-as-paragraph/"
"weight": 530
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF 檔案中的文字和圖像作為段落

## 介紹

在當今的數位世界中，PDF 是我們大多數人每天都會遇到的通用文件格式。無論是報告、電子書或商業發票，PDF 都可以輕鬆地在各個平台之間共享資訊。但是如果您想以程式設計方式自訂 PDF 怎麼辦？這就是 Aspose.Pdf for .NET 的作用所在。在本教程中，我們將指導您使用 Aspose.Pdf for .NET 將文字和圖像作為內嵌段落插入 PDF 檔案中。

## 先決條件

在深入研究程式碼之前，讓我們確保您擁有順利進行所需的一切：

- Aspose.PDF for .NET 函式庫：您需要安裝 Aspose.PDF for .NET。你可以下載 [這裡](https://releases。aspose.com/pdf/net/).
- Visual Studio：任何支援 .NET 的版本都可以正常運作。
- 對 C# 的基本了解：熟悉一些 C# 將會有所幫助，但別擔心 - 我會引導您完成每一步！
- PDF 文件就緒：如果您想新增自訂影像，請準備好。

您還可以免費試用該庫 [這裡](https://releases.aspose.com/)或者如果你正在從事大型項目，可以考慮購買 [這裡](https://purchase.aspose.com/buy)。需要更多詳細資訊嗎？查看文件 [這裡](https://reference。aspose.com/pdf/net/).

## 導入包

要開始使用 Aspose.PDF for .NET，您需要匯入所需的命名空間。這些命名空間可讓您的 C# 程式碼與 Aspose.PDF 功能互動。

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System;
```

很簡單，對吧？現在讓我們進入有趣的部分——創建您自己的 PDF 文件。

## 逐步指南：建立包含文字和內嵌影像的 PDF

讓我們將其分解為易於理解、易於遵循的步驟。想像你正在拼拼圖；每一步都像是找到並放置正確的碎片。

## 步驟 1：初始化 PDF 文檔

第一步是使用 Aspose.PDF 初始化一個新的 PDF 文件。該文件將作為添加文字和圖像的基礎。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";
// 實例化 Document 實例
Document doc = new Document();
```

這裡發生了什麼事？我們只是使用 `Document` 類別並定義您想要儲存 PDF 的目錄。這就像為您的傑作打開了一塊新的畫布！

## 第 2 步：向 PDF 新增頁面

如果沒有頁面，文檔就沒什麼用，對嗎？讓我們在您的文件中新增一個空白頁。

```csharp
// 將頁面加入到 Document 實例的頁面集合中
Page page = doc.Pages.Add();
```

此程式碼片段將新頁面新增到文件的頁面集合中。想像一下翻開筆記本中的一張空白頁。

## 步驟 3：新增段落文本

接下來，我們將新增一個文字段落。您可以在此處插入您的訊息或標題。

```csharp
// 建立 TextFragment
TextFragment text = new TextFragment("Hello World.. ");
// 將文字片段加入到 Page 物件的段落集合中
page.Paragraphs.Add(text);
```

在這裡，我們創建一個 `TextFragment` 物件來保存文字“Hello World..”，然後將其作為段落新增到頁面中。這就像在 PDF 文件中寫下第一句話一樣。

## 步驟 4：新增圖像作為內聯段落

現在我們已經有了文本，讓我們透過添加圖像作為內聯段落來使內容更有趣。內嵌段落只是意味著圖像將緊接著文字出現，就像圖像在 Word 文件中的顯示方式一樣。

```csharp
// 建立圖像實例
Aspose.Pdf.Image image = new Aspose.Pdf.Image();
// 將圖像設定為內聯段落，以便它出現在 
// 上一段物件（TextFragment）
image.IsInLineParagraph = true;
// 指定影像檔案路徑 
image.File = dataDir + "aspose-logo.jpg";
```

在此程式碼片段中，我們建立了一個 `Image` 對象，告訴它與文字對齊，並指定圖像檔案的路徑。這相當於在文件中的句子後面貼上圖像。您可以用您想要的圖片替換“aspose-logo.jpg”。

## 步驟5：設定影像大小（可選）

想要調整影像大小嗎？沒問題。 Aspose.PDF 可讓您在將影像新增至文件之前調整其高度和寬度。

```csharp
// 設定影像高度（可選）
image.FixHeight = 30;
// 設定圖像寬度（可選）
image.FixWidth = 100;
```

這部分是可選的，但它可以幫助您控制圖像在 PDF 中顯示的大小。這就像在列印照片之前調整其大小一樣。

## 步驟 6：將圖像新增至段落集合

我們已經準備好圖像。現在讓我們將其作為內聯段落插入到文件中。

```csharp
// 將圖像加入頁面物件的段落集合中
page.Paragraphs.Add(image);
```

此行將圖像新增至段落集合中的文字之後。這就像在文字編輯器中點擊“插入圖像”按鈕一樣。

## 步驟 7：新增另一個內嵌文字段落

如果您想在圖像後面添加更多文字怎麼辦？讓我們透過插入另一個內聯文字片段來實現這一點。

```csharp
// 使用不同的內容重新初始化 TextFragment 對象
text = new TextFragment(" Hello Again..");
// 將 TextFragment 設定為內嵌段落
text.IsInLineParagraph = true;
// 將新建立的 TextFragment 加入到頁面的段落集合中
page.Paragraphs.Add(text);
```

我們正在重複使用 `TextFragment` 在此處新增一個帶有新文字（“Hello Again..”）的對象，並將其插入圖像之後的行內。這會讓您的 PDF 看起來流暢、有凝聚力。

## 步驟 8：儲存 PDF 文檔

我們快完成了！現在，讓我們將文件儲存到您指定的目錄。

```csharp
dataDir = dataDir + "TextAndImageAsParagraph_out.pdf";
doc.Save(dataDir);
Console.WriteLine("\nText and image added successfully as inline paragraphs.\nFile saved at " + dataDir);
```

最後一步將文件保存在您的目錄中，名稱為「TextAndImageAsParagraph_out.pdf」。恭喜您—您已經建立了包含文字和內嵌影像的 PDF！

## 結論

就這樣，使用 Aspose.PDF for .NET 建立包含文字和圖像作為內聯段落的 PDF 非常簡單，只需按照以下步驟操作即可。只需幾行程式碼，您就可以為 PDF 檔案添加動態內容，使其更具視覺吸引力和專業性。無論是商業報告還是電子書，控制 PDF 的佈局都會產生很大的不同。

## 常見問題解答

### 我可以添加多個圖像作為內聯段落嗎？  
是的，您可以透過建立單獨的 `Image` 物件並將它們新增至段落集合中。

### 我可以控制 PDF 中文字和圖像的位置嗎？  
是的，使用邊距等屬性，您可以控製文字和圖像的精確位置。

### Aspose.PDF for .NET 免費嗎？  
不，這是授權產品，但你可以得到 [免費試用](https://releases.aspose.com/) 或購買許可證 [這裡](https://purchase。aspose.com/buy).

### 我可以在文字中添加超連結嗎？  
是的，Aspose.PDF 允許您在文字片段中新增超連結。檢查 [文件](https://reference.aspose.com/pdf/net/) 了解更多詳情。

### 我可以自訂文字的字體和樣式嗎？  
絕對地！您可以輕鬆自訂文字片段的字體、顏色和其他樣式屬性。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}