---
"description": "了解如何使用 Aspose.PDF for .NET 為 PDF 檔案中的文字新增工具提示。輕鬆使用資訊豐富的懸停文字增強您的 PDF。"
"linktitle": "在 PDF 檔案中的文字中新增工具提示"
"second_title": "Aspose.PDF for .NET API參考"
"title": "在 PDF 檔案中的文字中新增工具提示"
"url": "/zh-hant/net/programming-with-text/add-tooltip-to-text/"
"weight": 90
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 檔案中的文字中新增工具提示

## 介紹

在創建引人入勝且具有互動性的 PDF 時，工具提示非常有價值。您知道那些當您將滑鼠懸停在某個東西上時會向您提供額外資訊的小彈出框嗎？它們可以提供背景、描述，甚至一些建議，而不會使您的文件變得混亂。在本教學中，我們將介紹如何使用 Aspose.PDF for .NET 函式庫為 PDF 檔案中的文字新增工具提示。無論您是經驗豐富的開發人員還是剛剛涉足 PDF 世界，您都來到了正確的地方！讓我們開始吧！

## 先決條件

在我們進入編碼部分之前，讓我們確保您擁有順利進行所需的一切。

### Visual Studio 已安裝
必須在您的機器上安裝 Visual Studio，因為它將成為 .NET 應用程式的主要開發環境。

### Aspose.PDF for .NET函式庫
您還需要擁有 Aspose.PDF 庫。你可以 [點此下載](https://releases.aspose.com/pdf/net/)。確保將其包含在您的項目參考中。

### C# 基礎知識
由於我們將使用該語言進行編碼，因此 C# 的背景將會有很大幫助。但別擔心——我會指導您完成每一步！

### 要處理的 PDF 文檔
您可以從空白 PDF 文件開始，就像我們在此範例中所做的那樣，或者如果願意，可以使用現有的文件。

現在，讓我們繼續編碼部分！

## 導入包 

我們的編碼冒險的第一步是導入必要的套件。開啟 Visual Studio 項目，然後在 C# 檔案的頂部新增以下內容 `using` 指令：

```csharp
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
```

這些套件可讓您存取建立和處理 PDF 文件所需的所有類別和功能。

## 步驟 1：設定文檔目錄

首先，我們需要設定保存文檔的路徑。想像一下，在您的檔案系統中找到一個舒適的位置，您的所有創作都將駐留在其中。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outputFile = dataDir + "Tooltip_out.pdf";
```

確保更換 `YOUR DOCUMENT DIRECTORY` 使用您機器上的實際路徑。

## 步驟 2：建立範例 PDF 文檔

接下來，是時候建立一個包含一些文字的簡單 PDF 了。這就是我們開始創作過程的地方！

```csharp
// 建立帶有文字的範例文檔
Document doc = new Document();
doc.Pages.Add().Paragraphs.Add(new TextFragment("Move the mouse cursor here to display a tooltip"));
doc.Pages[1].Paragraphs.Add(new TextFragment("Move the mouse cursor here to display a very long tooltip"));
doc.Save(outputFile);
```

這一步驟我們建立一個文檔，新增兩個文字片段，並將其儲存到我們之前指定的路徑。

## 步驟3：開啟文件進行處理

現在我們已經建立了文檔，讓我們打開它以便我們可以處理那些工具提示！

```csharp
// 開啟包含文字的文檔
Document document = new Document(outputFile);
```

這裡我們只需載入剛剛建立的文檔。

## 步驟 4：建立文字吸收器來尋找文字片段

我們需要找到想要新增工具提示的文字片段。這就像使用放大鏡突出顯示大地圖上的特定部分一樣！ 

```csharp
// 建立 TextAbsorber 物件來尋找與正規表示式相符的所有短語
TextFragmentAbsorber absorber = new TextFragmentAbsorber("Move the mouse cursor here to display a tooltip");
document.Pages.Accept(absorber);
```

## 步驟5：擷取文字片段

接下來，我們提取上一個步驟中找到的文字片段。

```csharp
// 取得擷取的文字片段
TextFragmentCollection textFragments = absorber.TextFragments;
```

此程式碼片段使我們能夠保留我們感興趣的文本片段的引用。

## 步驟 6：循環遍歷片段並新增工具提示

現在到了有趣的部分！我們將循環遍歷每個文字片段並為每個文字片段添加一個工具提示。想像一下將小禮物（工具提示）包裹在特定物品（文字片段）周圍。

```csharp
// 循環遍歷片段
foreach (TextFragment fragment in textFragments)
{
	// 在文字片段位置建立不可見按鈕
	ButtonField field = new ButtonField(fragment.Page, fragment.Rectangle);
	// AlternateName 值將由檢視器應用程式顯示為工具提示
	field.AlternateName = "Tooltip for text.";
	// 在文件中新增按鈕字段
	document.Form.Add(field);
}
```

在每次迭代中，我們建立一個與文字片段的位置相對應的按鈕字段，並將工具提示文字指派給它。

## 步驟 7：重複以上步驟，即可獲得長工具提示

就像我們添加了一個簡單的工具提示一樣，我們可以對較長的文字執行相同的操作。讓我們擴展我們的創造力吧！

```csharp
// 接下來是很長的工具提示範例
absorber = new TextFragmentAbsorber("Move the mouse cursor here to display a very long tooltip");
document.Pages.Accept(absorber);
textFragments = absorber.TextFragments;
foreach (TextFragment fragment in textFragments)
{
	ButtonField field = new ButtonField(fragment.Page, fragment.Rectangle);
	// 設定非常長的文字
	field.AlternateName = "Lorem ipsum dolor sit amet, consectetur adipiscing elit," +
							" sed do eiusmod tempor incididunt ut labore et dolore magna" +
							" aliqua. Ut enim ad minim veniam, quis nostrud exercitation" +
							" ullamco laboris nisi ut aliquip ex ea commodo consequat." +
							" Duis aute irure dolor in reprehenderit in voluptate velit" +
							" esse cillum dolore eu fugiat nulla pariatur. Excepteur sint" +
							" occaecat cupidatat non proident, sunt in culpa qui officia" +
							" deserunt mollit anim id est laborum.";
	document.Form.Add(field);
}
```

在這裡，我們做著與以前相同的工作，但工具提示更加豐富。

## 步驟8：儲存文檔

最後一步是保存帶有所有這些閃亮的新工具提示的文件。 

```csharp
// 儲存文件
document.Save(outputFile);
```

就這樣，您就完成了！您已向 PDF 添加了工具提示，使其更加用戶友好且具有互動性。

## 結論

這就是您所需要的—一個簡單易懂的指南，介紹如何使用 Aspose.PDF for .NET 在 PDF 文件中的文字中新增工具提示。這種技術可以顯著增強使用者體驗，使您的文件更具資訊量，而不會讓讀者一次閱讀過多的文字。 

只需將滑鼠懸停在單字或短語上，讀者就能獲得相關資訊，這些資訊既有價值又不會造成混亂。所以，捲起袖子嘗試一下吧！在您不知不覺中，您就可以創建各種引人注目的引人入勝的文檔。

## 常見問題解答

### 什麼是 Aspose.PDF for .NET？
Aspose.PDF for .NET 是一個函式庫，可讓開發人員在 .NET 應用程式中建立、操作和轉換 PDF 文件。

### 我可以免費使用 Aspose.PDF 嗎？
是的，Aspose 提供免費試用版供您探索其功能！你可以找到它 [這裡](https://releases。aspose.com/).

### Aspose.PDF 是否有可用的授權選項？
是的，您可以購買許可證或獲得臨時許可證。查看選項 [這裡](https://purchase。aspose.com/).

### 我可以使用 Aspose.PDF 新增工具提示以外的互動元素嗎？
絕對地！ Aspose.PDF 允許新增各種互動元素，如超連結、按鈕和表單。

### 在哪裡可以找到有關 Aspose.PDF 的更多文件？
您可以查看文檔 [這裡](https://reference.aspose.com/pdf/net/) 以獲得更深入的指導。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}