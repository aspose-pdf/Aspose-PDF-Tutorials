---
"description": "透過逐步指南了解如何使用 Aspose.PDF for .NET 設定 PDF 中表格行的樣式，輕鬆增強文件格式。"
"linktitle": "樣式表行"
"second_title": "Aspose.PDF for .NET API參考"
"title": "樣式表行"
"url": "/zh-hant/net/programming-with-tagged-pdf/style-table-row/"
"weight": 180
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 樣式表行

## 介紹

當談到創建結構良好、格式精美的 PDF 文件時，Aspose.PDF for .NET 是一個首選解決方案。無論您是自動產生報表、發票或建立動態表格，使用各種樣式來格式化表格都是完善文件的關鍵。在本教學中，我們將深入研究使用 Aspose.PDF for .NET 設定表格行的樣式。別擔心，我會一步一步地指導你，就像喝咖啡時進行的愉快交談一樣！

## 先決條件

在我們討論細節之前，讓我們先確保您已經做好了一切準備。你需要：

1. Aspose.PDF for .NET函式庫  
   如果你還沒有，你可以從 [這裡](https://releases.aspose.com/pdf/net/)。您還可以獲得 [免費試用](https://releases.aspose.com/) 開始吧。
2. 開發環境  
   設定 Visual Studio 或您選擇的任何 C# IDE。您還需要安裝 .NET，但我猜您已經熟悉它了。
3. C# 和 .NET 基礎知識  
   對 C# 的良好理解將使本教程變得輕而易舉。但別擔心，我會詳細解釋每個步驟！

## 導入包

在我們開始使用 Aspose.PDF 之前，我們需要匯入必要的命名空間。在您的 C# 專案中，請確保包含以下內容：

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

這些對於創建和設計表格以及處理標記內容以達到合規性至關重要。

現在讓我們一步一步地分解任務，以便您可以像專業人士一樣設定表格行的樣式！

## 步驟 1：建立新的 PDF 文檔

首先，讓我們建立一個全新的 PDF 文件。該文件將保存所有樣式表行。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";

// 建立文檔
Document document = new Document();
```

這裡我們只是初始化一個新的 `Document` 代表我們的 PDF 文件的對象。確保設定保存輸出檔案的目錄路徑。

## 第 2 步：處理標記內容

為了使您的 PDF 結構更易於訪問，我們將使用標記內容。這有助於建立表格等結構化元素，確保它們符合 PDF/UA 等可訪問性標準。

```csharp
ITaggedContent taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example table row style");
taggedContent.SetLanguage("en-US");
```

在這裡，我們設定 PDF 標記內容的標題和語言。這就像給你的 PDF 一個名字並告訴它應該說什麼語言！

## 步驟3：定義表結構

接下來，讓我們定義即將建立的表的結構。每個表格都需要一個頁眉、正文和頁腳 - 就像一個組織良好的部落格文章一樣！

```csharp
// 取得根結構元素
StructureElement rootElement = taggedContent.RootElement;

// 建立表格結構元素
TableElement tableElement = taggedContent.CreateTableElement();
rootElement.AppendChild(tableElement);
TableTHeadElement tableTHeadElement = tableElement.CreateTHead();
TableTBodyElement tableTBodyElement = tableElement.CreateTBody();
TableTFootElement tableTFootElement = tableElement.CreateTFoot();
```

我們在這裡做的是創建一個帶有標題的表格（`THead`), 身體 (`TBody`) 和頁尾 (`TFoot`）。這些元素將保存我們的行。

## 步驟 4：新增表格頭行

沒有標題的表格就像沒有標題的書。讓我們先建立標題行來提供資料上下文。

```csharp
TableTRElement headTrElement = tableTHeadElement.CreateTR();
headTrElement.AlternativeText = "Head Row";
for (int colIndex = 0; colIndex < 3; colIndex++)
{
    TableTHElement thElement = headTrElement.CreateTH();
    thElement.SetText(String.Format("Head {0}", colIndex));
}
```

在這裡，我們循環並添加三個標題單元格（`TableTHElement`)，並為每個條目提供描述性文字。很簡單，對吧？

## 步驟 5：新增樣式化的正文行

現在到了最有趣的部分——設計行樣式！讓我們建立具有自訂樣式的七行。我們將設定背景顏色、邊框、填滿和文字對齊方式。

```csharp
for (int rowIndex = 0; rowIndex < 7; rowIndex++)
{
    TableTRElement trElement = tableTBodyElement.CreateTR();
    trElement.AlternativeText = String.Format("Row {0}", rowIndex);
    trElement.BackgroundColor = Color.LightGoldenrodYellow;
    trElement.Border = new BorderInfo(BorderSide.All, 0.75F, Color.DarkGray);
    trElement.DefaultCellBorder = new BorderInfo(BorderSide.All, 0.50F, Color.Blue);
    trElement.MinRowHeight = 100.0;
    trElement.FixedRowHeight = 120.0;
    trElement.IsInNewPage = (rowIndex % 3 == 1);
    trElement.IsRowBroken = true;

    for (int colIndex = 0; colIndex < 3; colIndex++)
    {
        TableTDElement tdElement = trElement.CreateTD();
        tdElement.SetText(String.Format("Cell [{0}, {1}]", rowIndex, colIndex));
    }
}
```

- 背景顏色：我們使用了淺金黃色，以營造專業又溫暖的感覺。
- 邊框：每行都有深灰色外邊框和藍色單元格邊框，以獲得清晰的外觀。
- 高度和填充：設定行高，並添加填充以獲得整潔的外觀。
- 分頁符號：為了讓表格更具可讀性，每隔一行就從新的一頁開始。

## 步驟 6：新增頁尾行

與頁首非常相似，頁尾固定表格。讓我們創建一個。

```csharp
TableTRElement footTrElement = tableTFootElement.CreateTR();
footTrElement.AlternativeText = "Foot Row";
for (int colIndex = 0; colIndex < 3; colIndex++)
{
    TableTDElement tdElement = footTrElement.CreateTD();
    tdElement.SetText(String.Format("Foot {0}", colIndex));
}
```

我們只需循環遍歷三個頁腳單元格並添加一些文字。頁腳的替代文字是“Foot Row”，以使其易於存取。

## 步驟 7：儲存 PDF 文檔

現在桌子已經佈置好了，是時候保存你的傑作了！

```csharp
document.Save(dataDir + "StyleTableRow.pdf");
```

就這樣，您的 PDF 就儲存了，其中包含我們剛剛設定樣式的所有漂亮的表格行。

## 步驟 8：驗證 PDF/UA 合規性

為了確保我們的 PDF 符合無障礙標準，我們將驗證其是否符合 PDF/UA 標準。

```csharp
document = new Document(dataDir + "StyleTableRow.pdf");
bool isPdfUaCompliance = document.Validate(dataDir + "StyleTableRow.xml", PdfFormat.PDF_UA_1);
Console.WriteLine(String.Format("PDF/UA compliance: {0}", isPdfUaCompliance));
```

這可確保您的 PDF 符合 PDF/UA 標準，從而使每個人都可以存取。可訪問性是遊戲的名稱！

## 結論

就是這樣！只需幾行程式碼，您就可以使用 Aspose.PDF for .NET 在 PDF 中建立一個完全樣式化的表格。從頁首到頁腳，我們設計了每一行的樣式，並添加了可訪問性元素，甚至驗證了文件的合規性。無論您是在處理公司報告、簡報，還是只是想使用 PDF，本指南都能滿足您的需求。現在，繼續並開始像專業人士一樣設計您的表單！

## 常見問題解答

### 我也可以更改表格的字體樣式嗎？  
是的！您可以使用 `TextState` 每個單元格的對象，允許完全自訂。

### 如何在表中新增更多列？  
只需調整 `colCount` 變數並在頁首、正文和頁尾的循環中加入更多單元格。

### 如果我不設定行高會發生什麼事？  
如果不設定行高，表格將根據內容自動調整。

### 我可以將其用於動態行數嗎？  
絕對地！您可以從資料庫或任何其他來源取得資料並動態調整行數和列數。

### Aspose.PDF for .NET 可以免費使用嗎？  
Aspose.PDF for .NET 是一款授權產品，但您可以使用 [免費試用](https://releases.aspose.com/) 或得到 [臨時執照](https://purchase。aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}