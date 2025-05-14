---
"description": "了解如何使用 Aspose.PDF for .NET 在 PDF 文件中新增重複列。帶有範例和程式碼的逐步指南。非常適合開發人員。"
"linktitle": "在 PDF 文件中新增重複列"
"second_title": "Aspose.PDF for .NET API參考"
"title": "在 PDF 文件中新增重複列"
"url": "/zh-hant/net/programming-with-tables/add-repeating-column/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 文件中新增重複列

## 介紹

如果您正在處理 PDF 文件並需要新增重複列，那麼您來對地方了！使用 Aspose.PDF for .NET，您可以輕鬆管理 PDF 中的表單和內容。無論您建立的是動態報告、發票或任何其他結構化文檔，重複列都可以改變資料組織方式。讓我們深入了解如何在 PDF 文件中新增重複列的逐步指南。

## 先決條件

在我們進入程式碼之前，讓我們確保您已設定好一切：

- Aspose.PDF for .NET：您需要在專案中安裝 Aspose.PDF for .NET 程式庫。
- [下載 Aspose.PDF for .NET](https://releases.aspose.com/pdf/net/)
- [免費試用](https://releases.aspose.com/)
- 開發環境：確保您安裝了與 .NET 相容的 IDE，例如 Visual Studio。
- 對 C# 的基本了解：雖然我們會將所有內容分解，但對 C# 的基本了解將幫助您順利跟進。
  
如果您還沒有 Aspose.PDF for .NET，您可以取得 [臨時執照](https://purchase.aspose.com/temporary-license/) 開始探索其功能。

## 導入包

首先，您需要從 Aspose.PDF for .NET 匯入必要的命名空間。以下是操作方法：

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

這些套件提供了處理 PDF 文件和操作表格所需的基本類別和方法。

現在，讓我們將流程分解為多個步驟，以將重複列新增至 PDF 文件。繼續跟進！

## 步驟 1：設定文檔目錄的路徑

在建立或操作任何文件之前，我們需要定義生成的 PDF 的保存路徑。在您的 C# 專案中，設定檔案所在目錄的路徑：

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "AddRepeatingColumn_out.pdf";
```

此路徑指向將儲存輸出 PDF 的目錄。代替 `"YOUR DOCUMENT DIRECTORY"` 使用您機器上的實際路徑。

## 步驟2：建立新的PDF文檔

首先，實例化一個新的 `Document` 目的。這將作為 PDF 中所有頁面和內容的容器。

```csharp
Document doc = new Document();
Aspose.Pdf.Page page = doc.Pages.Add();
```

在這裡，我們建立了一個新的 PDF 文件並向其中添加了一個空白頁。這 `doc.Pages.Add()` 方法將新頁面插入文件中。

## 步驟 3：實例化外表

接下來，我們創造一個外表。該表將跨越整個頁面的寬度，並作為其他表的容器，包括包含重複列的表。

```csharp
Aspose.Pdf.Table outerTable = new Aspose.Pdf.Table();
outerTable.ColumnWidths = "100%";
outerTable.HorizontalAlignment = HorizontalAlignment.Left;
```

我們設定了 `ColumnWidths` 屬性為“100%”，表示表格將延伸至整個頁面寬度。

## 步驟 4：建立內部表

現在，讓我們建立具有重複列的內部表。這裡的關鍵屬性是 `Broken`，允許表格延續到同一頁，並且 `ColumnAdjustment`，它會自動調整列寬以適應內容。

```csharp
Aspose.Pdf.Table mytable = new Aspose.Pdf.Table();
mytable.Broken = TableBroken.VerticalInSamePage;
mytable.ColumnAdjustment = ColumnAdjustment.AutoFitToContent;
```

該內表將嵌套在外表內。

## 步驟 5：為頁面新增表格

現在我們已經準備好了外表和內表，讓我們將它們添加到頁面中。此步驟確保表格包含在文件的結構中。

```csharp
page.Paragraphs.Add(outerTable);
var bodyRow = outerTable.Rows.Add();
var bodyCell = bodyRow.Cells.Add();
bodyCell.Paragraphs.Add(mytable);
mytable.RepeatingColumnsCount = 5;
```

在這裡，我們添加了 `outerTable` 到頁面，然後在外部表格中，我們嵌套了 `mytable`。此外，我們設置 `RepeatingColumnsCount` 到 5，指定新增資料時應重複多少列。

## 步驟 6：新增標題行

現在是時候將標題添加到表中了。標題行提供了資料的背景並有助於建立列。 

```csharp
Aspose.Pdf.Row row = mytable.Rows.Add();
row.Cells.Add("header 1");
row.Cells.Add("header 2");
row.Cells.Add("header 3");
row.Cells.Add("header 4");
row.Cells.Add("header 5");
row.Cells.Add("header 6");
row.Cells.Add("header 7");
row.Cells.Add("header 11");
row.Cells.Add("header 12");
row.Cells.Add("header 13");
row.Cells.Add("header 14");
row.Cells.Add("header 15");
row.Cells.Add("header 16");
row.Cells.Add("header 17");
```

此程式碼片段新增第一行（我們將使用它作為標題），並用包含「標題 1」、「標題 2」等文字的儲存格填滿它。

## 步驟 7：新增資料行

最後，我們可以在表中添加一些資料。此循環動態建立行並用內容填充單元格：

```csharp
for (int RowCounter = 0; RowCounter <= 5; RowCounter++)
{
    Aspose.Pdf.Row row1 = mytable.Rows.Add();
    row1.Cells.Add("col " + RowCounter.ToString() + ", 1");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 2");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 3");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 4");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 5");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 6");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 7");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 11");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 12");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 13");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 14");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 15");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 16");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 17");
}
```

循環迭代六次，添加行並用相應的列資料填充每個單元格（例如，“col 1, 1”，“col 2, 2”等）。

## 步驟8：儲存文檔

新增完所有行和列後，最後一步是將文件儲存到指定的檔案路徑。

```csharp
doc.Save(outFile);
```

您的文件現已儲存，其中包含重複的列！

## 結論

就是這樣！透過這些簡單的步驟，您可以使用 Aspose.PDF for .NET 建立具有重複列的 PDF 文件。透過利用巢狀表的靈活性，您可以實現複雜的佈局，使您的 PDF 看起來專業且井然有序。在您的下一個專案中嘗試一下，並探索 Aspose.PDF 的全部潛力來滿足您的 PDF 生成需求。

## 常見問題解答

### 什麼是 Aspose.PDF for .NET？
Aspose.PDF for .NET 是一個強大的程式庫，可讓開發人員以程式設計方式建立、編輯和管理 PDF 文件。

### 我可以動態調整重複列的數量嗎？
是的，您可以透過修改 `RepeatingColumnsCount` 財產。

### 如何向 Aspose.PDF for .NET 申請許可證？
您可以按照以下步驟從文件或流中套用許可證 [文件](https://reference。aspose.com/pdf/net/).

### 是否可以為表格單元格新增圖像？
是的，Aspose.PDF for .NET 支援在表格單元格中新增各種類型的內容，包括圖片。

### 我可以進一步自訂表格佈局嗎？
絕對地！ Aspose.PDF 提供了用於自訂表格樣式的廣泛功能，包括邊框、填充、對齊等。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}