---
"description": "了解如何使用 Aspose.PDF for .NET 建立多層 PDF。按照我們的逐步指南，您可以輕鬆地將文字、圖像和圖層新增到您的 PDF 檔案。"
"linktitle": "建立多層 PDF 檔案第二種方法"
"second_title": "Aspose.PDF for .NET API參考"
"title": "建立多層 PDF 檔案第二種方法"
"url": "/zh-hant/net/programming-with-document/createmultilayerpdfsecondapproach/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 建立多層 PDF 檔案第二種方法

## 介紹

在當今的數位文件世界中，創建專業、分層的 PDF 的能力非常有價值。無論您是添加浮水印、在圖像上插入文字還是創建複雜的佈局，您都需要一個強大的解決方案來讓您完全控制 PDF 圖層。 Aspose.PDF for .NET 是一個強大的工具，可以讓這個過程變得順暢和直接。

## 先決條件

在開始之前，請確保您具備以下條件：

- Aspose.PDF for .NET Library：如果您尚未安裝，請下載 [最新版本在這裡](https://releases。aspose.com/pdf/net/).
- .NET 開發環境：您可以使用 Visual Studio 或任何其他支援 .NET 的 IDE。
- 對 C# 的基本了解：您應該熟悉 C# 程式設計才能跟上。
- 測試圖片檔案：您需要一個映像檔（例如“test_image.png”）來在本教學中使用。

如果您還沒有 Aspose.PDF for .NET 許可證，您可以申請 [臨時執照](https://purchase.aspose.com/temporary-license/)。如需更多資源，請查看 [文件](https://reference.aspose.com/pdf/net/) 或伸手 [支援](https://forum。aspose.com/c/pdf/10).

## 導入必要的套件

要開始建立多層 PDF，您需要匯入適當的命名空間。這些套件支援使用所有必需的類，例如 `Document`， `Page`， `TextFragment`， 和 `FloatingBox`。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System.Drawing;
```

現在先決條件已經滿足，讓我們進入主要部分：建立多層 PDF 檔案。

本指南旨在以詳細且適合初學者的方式引導您完成每個步驟。那麼，讓我們捲起袖子開始行動吧！

## 步驟 1：初始化文件並設定路徑

我們首先需要的是 PDF 文件物件和一種引用我們保存最終 PDF 的位置的方法。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

在這個程式碼片段中，我們創建了一個 `Document` 代表我們的 PDF 的對象。這 `dataDir` 變數應該設定為您想要儲存產生的 PDF 檔案的目錄。

## 步驟 2：為 PDF 文件新增頁面

每個 PDF 文件由一個或多個頁面組成。讓我們在文件中新增一個頁面。

```csharp
Aspose.Pdf.Page page = doc.Pages.Add();
```

此程式碼會為文件新增一個空白頁。很簡單，對吧？現在讓我們繼續在此頁面上新增圖層。

## 步驟 3：建立並自訂文字片段

接下來，我們將建立一個文字片段。這是一段我們可以按照顏色、大小和位置進行操作的文字。

```csharp
Aspose.Pdf.Text.TextFragment t1 = new Aspose.Pdf.Text.TextFragment("paragraph 3 segment");
t1.TextState.ForegroundColor = Color.Red;
t1.IsInLineParagraph = true;
t1.TextState.FontSize = 12;
```

以下是正在發生的事情：
- 這 `TextFragment` 目的 `t1` 使用文字“第 3 段”進行初始化。
- 我們使用 `ForegroundColor` 財產。
- 文字大小設定為 12 磅，並使用 `IsInLineParagraph`。

## 步驟 4：將文字片段新增至 FloatingBox

現在我們有了文字片段，我們需要將其放置在 PDF 中。我們不會直接將其添加到頁面，而是使用 `FloatingBox` 給它一個特定的位置。

```csharp
Aspose.Pdf.FloatingBox TextFloatingBox1 = new Aspose.Pdf.FloatingBox(117, 21);
TextFloatingBox1.ZIndex = 1;
TextFloatingBox1.Left = -4;
TextFloatingBox1.Top = -4;
page.Paragraphs.Add(TextFloatingBox1);
TextFloatingBox1.Paragraphs.Add(t1);
```

讓我們來分析一下：
- 我們創建了一個 `FloatingBox` 並定義其尺寸（117x21）。
- 這 `ZIndex` 屬性設為 1，表示它將位於底層。
- 這 `Left` 和 `Top` 屬性定義框在頁面上的確切位置。
- 最後，文字片段 `t1` 新增到浮動框內，然後新增到頁面中。

## 步驟 5：將影像插入另一個 FloatingBox

接下來，我們將向 PDF 添加圖像。就像文本一樣，我們將它放在 `FloatingBox`。

```csharp
Aspose.Pdf.Image image1 = new Aspose.Pdf.Image();
image1.File = dataDir + "test_image.png";
Aspose.Pdf.FloatingBox ImageFloatingBox = new Aspose.Pdf.FloatingBox(117, 21);
ImageFloatingBox.Left = -4;
ImageFloatingBox.Top = -4;
ImageFloatingBox.ZIndex = 2;
ImageFloatingBox.Paragraphs.Add(image1);
page.Paragraphs.Add(ImageFloatingBox);
```

具體如下：
- 我們創建了一個 `Image` 物件並分配圖像檔案的路徑。
- 一個新的 `FloatingBox` 為圖像創建，與文字浮動框大小相同。
- 圖像浮動框透過設定其 `ZIndex` 至 2。
- 這 `Left` 和 `Top` 屬性將圖像精確定位到我們想要的位置。
- 圖像被加入到浮動框中，然後加入到頁面中。

## 步驟6：儲存PDF文檔

最後，我們將新建立的多層PDF儲存到指定的目錄中。

```csharp
doc.Save(dataDir + @"Multilayer-2ndApproach_out.pdf");
```

此行將把您的 PDF 檔案以「Multilayer-2ndApproach_out.pdf」的名稱儲存在您指定的目錄中。恭喜，您已成功使用 Aspose.PDF for .NET 建立了多層 PDF！

## 結論

使用 Aspose.PDF for .NET 建立多層 PDF 檔案既靈活又強大。無論您想要疊加文字、圖像或其他元素，這種方法都可以讓您完全控製文件的結構和呈現方式。

## 常見問題解答

### 我可以使用 Aspose.PDF for .NET 建立多頁 PDF 嗎？  
是的，您可以撥打電話新增任意數量的頁面 `doc.Pages.Add()` 每頁。

### 如何在 PDF 中分層添加更多元素（例如形狀或註釋）？  
您可以使用 `FloatingBox` 適用於任何類型的內容，包括形狀、註釋甚至表格。

### Aspose.PDF for .NET 支援哪些影像格式？  
Aspose.PDF 支援各種影像格式，包括 PNG、JPEG、GIF 和 BMP。

### 我可以更改 PDF 中元素的不透明度嗎？  
是的，你可以透過調整 `Alpha` 的組成部分 `Color` 目的。

### 如何將元素移到 PDF 中的不同位置？  
您可以調整 `Left` 和 `Top` 的屬性 `FloatingBox` 重新定位任何元素。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}