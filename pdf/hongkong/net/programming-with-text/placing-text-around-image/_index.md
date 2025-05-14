---
"description": "了解如何使用 Aspose.PDF for .NET 在 PDF 中的圖像周圍放置文字。請按照我們的逐步指南建立包含並排圖像和文字的專業 PDF。"
"linktitle": "在 PDF 文件中的圖像周圍放置文本"
"second_title": "Aspose.PDF for .NET API參考"
"title": "在 PDF 文件中的圖像周圍放置文本"
"url": "/zh-hant/net/programming-with-text/placing-text-around-image/"
"weight": 260
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 文件中的圖像周圍放置文本

## 介紹

您是否曾嘗試在 PDF 文件中的圖像周圍放置文本，但發現這很困難？如果是這樣，那麼您來對地方了！ Aspose.PDF for .NET 讓這個過程變得簡單，您只需幾行程式碼就可以將文字放在圖像旁邊。無論您創建的是報告、文件還是演示文稿，此功能都是增強內容佈局並使其更具視覺吸引力的絕佳方式。今天，我們將介紹如何使用 Aspose.PDF for .NET 在 PDF 文件中的圖像周圍放置文字。

## 先決條件

在我們進入代碼之前，讓我們確保一切都已設定好。您需要準備以下物品：

- Aspose.PDF for .NET：您可以從 [這裡](https://releases。aspose.com/pdf/net/).
- Visual Studio：確保您已安裝最新版本，以便順利進行。
- .NET Framework：此範例使用 .NET，因此請確保您的環境已設定為適合 .NET 開發。
- 臨時駕照：您可以申請臨時駕照 [這裡](https://purchase.aspose.com/temporary-license/) 如果您正在評估該產品。

如果您尚未設定 Aspose.PDF for .NET，請依照 [文件](https://reference。aspose.com/pdf/net/).

## 導入命名空間

在開始編碼之前，我們需要導入必要的命名空間。以下是實現該功能的程式碼片段：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

這些命名空間至關重要，因為它們提供了對以下類別的存取： `Document`， `Page`， `Image`， 和 `HtmlFragment`，我們將使用它來建立和操作 PDF。

現在我們已經做好了準備，讓我們來分解如何使用 Aspose.PDF for .NET 在 PDF 文件中的圖像周圍放置文字。我們將逐步指導您完成此操作。

## 步驟 1：實例化文檔對象

首先，您需要建立一個 PDF 文件。在 Aspose.PDF 中，這是透過實例化 `Document` 目的。該物件將作為我們添加的所有內容的基礎。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

在這裡，我們建立了一個空的 PDF 文件。它還沒有任何頁面，但別擔心，我們將在下一步添加一個。

## 步驟 2：新增頁面

現在我們已經有了文檔，是時候新增頁面了。可以將其想像為創建一張空白紙，您可以在其中添加內容。

```csharp
Aspose.Pdf.Page page = doc.Pages.Add();
```

此程式碼為文件新增了一個新頁面。預設情況下，頁面是空白的，但我們即將改變這一點。

## 步驟 3：建立表格來組織內容

為了使我們的圖像和文字保持正確對齊，我們將使用表格。 PDF 中的表格可以幫助您建立佈局，就像在 Word 文件或 HTML 中一樣。

```csharp
Aspose.Pdf.Table table1 = new Aspose.Pdf.Table();
page.Paragraphs.Add(table1);
```

此程式碼片段建立一個表格並將其新增至頁面。將表格視為對齊圖像和文字的框架。

## 步驟 4：設定表格的列寬

現在我們已經新增了一個表格，我們需要定義列的寬度。這可確保圖像和文字在頁面上的大小合適。

```csharp
table1.ColumnWidths = "120 270";
```

此行設定兩列的寬度 - 一列用於圖像，一列用於文字。如果您的圖像或文字需要更多或更少的空間，請調整這些值。

## 步驟 5：定義邊距和填充

為了確保一切看起來整潔，讓我們為表格添加一些邊距和填充。

```csharp
Aspose.Pdf.MarginInfo margin = new Aspose.Pdf.MarginInfo();
margin.Top = 5f;
margin.Left = 5f;
margin.Right = 5f;
margin.Bottom = 5f;
table1.DefaultCellPadding = margin;
```

這些設定可確保您的表格具有一致的間距，使內容具有視覺吸引力。

## 步驟 6：將影像插入表格

現在，讓我們進入有趣的部分——添加圖像。在這種情況下，我們將添加 Aspose 徽標，但您可以隨意使用任何您喜歡的圖像。

```csharp
Aspose.Pdf.Row row1 = table1.Rows.Add();
Aspose.Pdf.Image logo = new Aspose.Pdf.Image();
logo.File = dataDir + "aspose-logo.jpg";
logo.FixHeight = 120;
logo.FixWidth = 110;
row1.Cells.Add();
row1.Cells[0].Paragraphs.Add(logo);
```

以下是正在發生的事情：
- 我們從您指定的目錄載入圖片。
- 我們設定圖像的高度和寬度。
- 最後，我們將圖像新增到表格中的第一個單元格。

## 步驟 7：在圖像旁邊新增文本

現在圖像已經就位，讓我們在它旁邊添加一些文字。對於此範例，我們將使用 HTML 格式的文字來設定內容樣式。

```csharp
string TitleString = "<font face=\"Arial\" size=6 color=\"#101090\"><b> Aspose.Pdf for .NET</b></font>";
string BodyString1 = "<font face=\"Arial\" size=2><br/>Aspose.Pdf for .NET is a non-graphical PDF document reporting component that enables .NET applications to <b>create PDF documents from scratch</b> without utilizing Adobe Acrobat.</font>";

Aspose.Pdf.HtmlFragment TitleText = new Aspose.Pdf.HtmlFragment(TitleString + BodyString1);
row1.Cells.Add();
row1.Cells[1].Paragraphs.Add(TitleText);
```

此區塊在圖像旁邊的儲存格中新增樣式標題和描述。您可以使用 HTML 標籤來格式化文本，以實現更多自訂。

## 步驟 8：調整垂直對齊

預設情況下，表格儲存格中的內容可能不會按照您想要的方式對齊。在這種情況下，我們要確保文字與儲存格的頂部對齊。

```csharp
row1.Cells[1].VerticalAlignment = Aspose.Pdf.VerticalAlignment.Top;
```

這確保文字位於單元格的頂部，保持佈局整潔和專業。

## 步驟9：在圖片和描述下方添加更多文本

您可能希望在圖像和文字下方包含更多內容。為此，我們在表中添加另一行。

```csharp
Aspose.Pdf.Row SecondRow = table1.Rows.Add();
SecondRow.Cells.Add();
SecondRow.Cells[0].ColSpan = 2;
SecondRow.Cells[0].VerticalAlignment = Aspose.Pdf.VerticalAlignment.Top;

string SecondRowString = "<font face=\"Arial\" size=2>Aspose.Pdf for .NET supports the creation of PDF files through API and XML or XSL-FO templates.</font>";
Aspose.Pdf.HtmlFragment SecondRowText = new Aspose.Pdf.HtmlFragment(SecondRowString);
SecondRow.Cells[0].Paragraphs.Add(SecondRowText);
```

在這裡，我們添加了另一行附加文本，跨越兩列以保持佈局平衡。

## 步驟 10：儲存 PDF 文檔

最後，我們需要儲存文檔，以便您可以查看變更。

```csharp
doc.Save(dataDir + "PlacingTextAroundImage_out.pdf");
```

這將保存 PDF，其中圖像和文字的格式正如我們想要的那樣。

## 結論

在 PDF 中的圖像周圍放置文字似乎是一項艱鉅的任務，但 Aspose.PDF for .NET 簡化了這個過程。透過利用表格、圖像和樣式文本，您可以用最少的努力創建具有專業外觀的 PDF。只需幾行程式碼，您就可以將內容準確地放置在您想要的位置，使您的文件看起來更加精緻和井然有序。

## 常見問題解答

### 我可以使用此方法放置多張帶有文字的圖像嗎？
是的，只需在表中添加更多行和單元格即可包含更多圖像和文字。

### 我可以改變影像的對齊方式嗎？
絕對地！您可以透過調整儲存格的對齊屬性來修改影像對齊。

### 我該如何進一步設計文字樣式？
您可以在 `HtmlFragment` 物件套用各種樣式，如粗體、斜體或不同的字體。

### 我可以控製文字和圖像之間的間距嗎？
是的，使用 `MarginInfo` 物件可讓您控制元素之間的填充和邊距。

### 可以添加文字連結嗎？
確實！您可以使用 `<a>` 標籤。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}