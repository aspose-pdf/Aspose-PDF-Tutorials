---
"description": "了解如何使用 Aspose.PDF for .NET 在 PDF 文件的頁首/頁尾部分新增表格。"
"linktitle": "頁首頁尾部分中的表格"
"second_title": "Aspose.PDF for .NET API參考"
"title": "頁首頁尾部分中的表格"
"url": "/zh-hant/net/programming-with-stamps-and-watermarks/table-in-header-footer-section/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 頁首頁尾部分中的表格

## 介紹

您是否曾經盯著一份普通的 PDF 文檔，希望它能有額外的亮點？嗯，你很幸運！ Aspose.PDF for .NET 可讓您像專業人士一樣建立和操作 PDF 檔案。今天，我們將深入研究一項便利的功能，它可讓您在 PDF 文件的標題中新增表格。您不僅會學到如何做，而且我還會一步一步地指導您，使整個過程變得非常順利。 🎉

## 先決條件

在我們進入實際編碼部分之前，讓我們確保您擁有開始所需的一切。以下是您需要的：

1. Visual Studio：確保您的電腦上安裝了 Visual Studio。如果你還沒有，你可以從 [微軟網站](https://visualstudio。microsoft.com/).
2. Aspose.PDF 庫：您必須擁有適用於 .NET 的 Aspose.PDF 庫。您可以使用以下連結獲取 [Aspose.PDF for .NET 軟體包](https://releases。aspose.com/pdf/net/).
3. C# 基礎知識：您至少應該對 C# 有基本的了解。如果您仍在學習，請不要擔心；我會盡量保持簡單！

## 導入包

好了，現在該捲起袖子開始編碼了！但首先，我們需要透過導入必要的套件來設定我們的環境。以下是操作方法：

###  打開你的專案
開啟您將要進行 PDF 建立的 Visual Studio 專案。 

###  新增對 Aspose.PDF 的引用
1. NuGet 套件管理器：在解決方案資源管理器中以滑鼠右鍵按一下您的專案並選擇「管理 NuGet 套件」。
2. 搜尋 Aspose.PDF：在搜尋欄中輸入「Aspose.PDF」並安裝該套件。

完成此步驟後，您應該已設定好一切並準備開始編碼！

現在，讓我們開始寫一些程式碼吧！請依照以下步驟在 PDF 的標題部分建立表格：

## 步驟 1：設定文檔目錄的路徑

在開始建立 PDF 之前，我們需要定義文件的儲存位置。以下是操作方法：

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY"; // 將其變更為您的實際目錄
```

代替 `YOUR DOCUMENT DIRECTORY` 以及您想要儲存 PDF 的路徑。這可以在您的系統上的任何位置 - 只要確保它可以訪問！

## 步驟 2：實例化文檔

接下來，我們將建立一個新的 PDF 文件。

```csharp
// 透過呼叫空建構函式來實例化 Document 實例
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document();
```

我們在這裡所做的是建立一個空的 PDF 文檔，我們將在其中添加所有有用內容。

## 步驟3：建立新頁面

讓我們在文件中新增一個頁面。 

```csharp
// 在pdf文件中建立一個頁面
Aspose.Pdf.Page page = pdfDocument.Pages.Add();
```

將此頁視為一塊空白畫布，我們可以在上面繪製我們的傑作！

## 步驟 4：建立標題部分

現在我們將為我們的 PDF 建立一個標題。

```csharp
// 建立 PDF 文件的頁首部分
Aspose.Pdf.HeaderFooter header = new Aspose.Pdf.HeaderFooter();
```

這個標題將包含我們的表格。 

## 步驟 5：將頁首分配給頁面

接下來，我們要確保頁首出現在頁面上。

```csharp
// 設定 PDF 檔案的奇數頁眉
page.Header = header;
```

## 步驟 6：設定上邊距

為了確保我們的標題頂部有一定的空間，讓我們調整邊距。

```csharp
// 設定頁首部分的上邊距
header.Margin.Top = 20;
```

設定邊距就像給你的文字一些個人空間 - 沒有人喜歡擁擠！

## 步驟 7：建立表

現在，是時候建立放入標題中的表格了。

```csharp
// 實例化表對象
Aspose.Pdf.Table tab1 = new Aspose.Pdf.Table();
```

## 步驟 8：將表格新增至標題

我們將把新建立的表格加入到標題的段落集合中。

```csharp
// 在所需部分的段落集合中新增表格
header.Paragraphs.Add(tab1);
```

## 步驟 9：設定單元格邊框

讓我們透過定義預設儲存格邊框來為表格提供一些結構。

```csharp
// 使用 BorderInfo 物件設定預設儲存格邊框
tab1.DefaultCellBorder = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 0.1F);
```

## 步驟 10：定義列寬

您可以指定表格每列的寬度。

```csharp
// 設定表格的列寬
tab1.ColumnWidths = "60 300";
```

這些值表示每列的寬度（以點為單位）。請隨意調整它們以滿足您的需求！

## 步驟 11：建立行並新增儲存格

現在是時候添加一些行和單元格了！ 

```csharp
// 在表格中建立行，然後在行中建立儲存格
Aspose.Pdf.Row row1 = tab1.Rows.Add();
row1.Cells.Add("Table in Header Section");
row1.BackgroundColor = Color.Gray;
```

這將創建第一行，其中單元格包含文本，並將其背景顏色設為灰色。

## 步驟 12：設定行距和文字樣式

您想讓您的行跨越多列嗎？方法如下：

```csharp
// 將第一行的行跨距值設為 2
tab1.Rows[0].Cells[0].ColSpan = 2;
tab1.Rows[0].Cells[0].DefaultCellTextState.ForegroundColor = Color.Cyan;
tab1.Rows[0].Cells[0].DefaultCellTextState.Font = FontRepository.FindFont("Helvetica");
```

這一步驟不僅設定了行跨度，還改變了文字的顏色和字體。

## 步驟 13：新增第二行

我們在表中添加另一行，好嗎？

```csharp
// 在表中建立另一行
Aspose.Pdf.Row row2 = tab1.Rows.Add();

// 設定 Row2 的背景顏色
row2.BackgroundColor = Color.White;
```

## 步驟 14：將影像新增至第二行

現在我們將添加一個標誌來讓我們的桌子看起來更漂亮！

```csharp
// 新增儲存影像的儲存格
Aspose.Pdf.Image img = new Aspose.Pdf.Image();
img.File = dataDir + "aspose-logo.jpg"; // 確保將圖像放在你的目錄中
```

不要忘記更換 `"aspose-logo.jpg"` 用您的圖像的實際名稱！

## 步驟15：調整影像寬度

設定圖像寬度以確保它在單元格中看起來恰到好處。

```csharp
// 將影像寬度設定為 60
img.FixWidth = 60;

// 將圖像新增至表格單元格
Aspose.Pdf.Cell cell2 = row2.Cells.Add();
cell2.Paragraphs.Add(img);
```

## 步驟 16：在第二個儲存格中新增文本

是時候在我們的標誌旁邊添加一些文字了！

```csharp
row2.Cells.Add("Logo is looking fine !");
row2.Cells[1].DefaultCellTextState.Font = FontRepository.FindFont("Helvetica");
```

## 步驟17：垂直和水平對齊文本

確保一切看起來整潔。對齊你的文字！

```csharp
// 將文字的垂直對齊方式設定為居中對齊
row2.Cells[1].VerticalAlignment = Aspose.Pdf.VerticalAlignment.Center;
row2.Cells[1].Alignment = Aspose.Pdf.HorizontalAlignment.Center;
```

## 步驟18：儲存PDF文檔

最後但同樣重要的是，讓我們保存我們的創作！

```csharp
// 儲存 PDF 文件
pdfDocument.Save(dataDir + "TableInHeaderFooterSection_out.pdf");
```

瞧！您已經創建了一個令人驚嘆的 PDF，並在標題部分帶有表格！

## 結論

就是這樣！您已成功使用 Aspose.PDF for .NET 將表格新增至 PDF 文件的標題。令人驚訝的是，只需幾行程式碼就可以將簡單的 PDF 轉換為具有專業外觀的文件。無論您準備的是報告、發票還是演示文稿，添加一點創造力都會產生很大的不同。 

## 常見問題解答

### 什麼是 Aspose.PDF for .NET？
Aspose.PDF for .NET 是一個強大的程式庫，可讓開發人員以程式設計方式建立和操作 PDF 文件。

### 我需要許可證才能使用 Aspose.PDF 嗎？
雖然您可以在試用期間免費使用庫，但延長使用期限則需要許可證。您可以獲得 [臨時執照](https://purchase.aspose.com/temporary-license/) 以供評估。

### 在哪裡可以找到該文件？
您可以在 [Aspose.PDF 文件頁面](https://reference。aspose.com/pdf/net/).

### 我該如何聯絡支援人員解決技術問題？
您可以透過以下方式尋求支持 [Aspose 論壇](https://forum。aspose.com/c/pdf/10).

### 我可以在 PDF 的其他部分建立表格嗎？
絕對地！您也可以在頁腳和正文部分建立表格；只需按照類似的步驟即可。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}