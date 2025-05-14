---
"description": "了解如何使用 Aspose.PDF for .NET 將 Excel 工作表資料匯出到 PDF 資料表。包含程式碼範例、先決條件和有用提示的逐步教學。"
"linktitle": "將 Excel 工作表資料匯出到表格"
"second_title": "Aspose.PDF for .NET API參考"
"title": "將 Excel 工作表資料匯出到表格"
"url": "/zh-hant/net/programming-with-tables/export-excel-worksheet-data-to-table/"
"weight": 70
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 將 Excel 工作表資料匯出到表格

## 介紹

您是否需要將 Excel 工作表中的資料匯出到 PDF 文件中，並以表格格式整齊排列？想像一下，Excel 中有一堆數據，但需要將其作為專業的 PDF 共享。聽起來很複雜，對吧？但是使用 Aspose.PDF for .NET，您可以輕鬆完成這項任務。在本教學中，我們將引導您完成使用 Aspose.PDF for .NET 將 Excel 工作表資料匯出到 PDF 文件內的表格中的過程。我們將一步一步地指導您，分解所有內容，以便即使您是新手，到最後您也會感覺自己像個專業人士。

## 先決條件

在深入編碼之前，讓我們先設定一些東西：

1. Aspose.PDF for .NET Library – 請確定您已安裝了最新版本。你可以 [點此下載](https://releases。aspose.com/pdf/net/).
2. Aspose.Cells for .NET Library – 您需要它來處理 Excel 操作。從下載 [這裡](https://releases。aspose.com/cells/net/).
3. .NET 開發環境 – 像 Visual Studio 這樣的工具可以完美地用於編碼。
4. Excel 檔案 – 準備好包含要匯出的資料的 Excel 檔案。

如果您沒有 Aspose.PDF 和 Aspose.Cells 庫，您可以從 [免費試用](https://releases。aspose.com/).

## 導入包

首先，請確保您已在專案中安裝了 Aspose.PDF 和 Aspose.Cells 庫。您可以使用 Visual Studio 中的 NuGet 套件管理器來安裝它們。

以下是如何在 C# 程式碼中匯入必要的套件：

```csharp
using System.Data;
using System.IO;
using System.Linq;
```

現在已經設定了先決條件，讓我們逐步了解將資料從 Excel 表匯出到 PDF 文件中的表格的過程。

## 步驟 1：載入 Excel 工作簿

首先，您需要將 Excel 工作簿載入到程式中。在此步驟中，我們將使用 Aspose.Cells 開啟 Excel 檔案。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";

// 載入 Excel 工作簿
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(new FileStream(dataDir + "newBook1.xlsx", FileMode.Open));
```

說明：在這裡，我們指定 Excel 檔案所在的目錄路徑，並使用 `Aspose.Cells.Workbook`。確保調整 `"YOUR DOCUMENT DIRECTORY"` 指向您的文件位置。

## 第 2 步：存取第一個工作表

載入工作簿後，我們需要存取儲存資料的第一個工作表。

```csharp
// 存取 Excel 文件中的第一個工作表
Aspose.Cells.Worksheet worksheet = workbook.Worksheets[0];
```

說明：這一步驟很簡單－我們從工作簿中取得第一個工作表，其中包含要匯出的資料。

## 步驟3：將資料匯出到DataTable

現在，讓我們將 Excel 表中的資料匯出到 DataTable 物件中，該物件將充當將資料傳輸到 PDF 的中介。

```csharp
// 將從第一個單元格開始的7行2列的內容匯出到DataTable
DataTable dataTable = worksheet.Cells.ExportDataTable(0, 0, worksheet.Cells.MaxRow + 1, worksheet.Cells.MaxColumn + 1, true);
```

解釋： `ExportDataTable` 方法從工作表的第一個單元格開始提取數據，跨越所有行和列。然後將該數據儲存在 `DataTable` 以供進一步使用。

## 步驟 4：建立新的 PDF 文檔

接下來，我們需要使用 Aspose.PDF 建立一個新的 PDF 文件。

```csharp
// 實例化 Document 實例
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document();

// 在文件實例中建立頁面
Aspose.Pdf.Page page = pdfDocument.Pages.Add();
```

解釋：在這裡，我們初始化一個新的 `Aspose.Pdf.Document` 並在其中新增一個頁面。該頁面稍後將包含我們根據 Excel 資料建立的表格。

## 步驟 5：在 PDF 中建立表格對象

讓我們繼續在 PDF 文件中建立表格。

```csharp
// 建立表對象
Aspose.Pdf.Table table = new Aspose.Pdf.Table();

// 將 Table 物件新增至頁面的段落集合中
page.Paragraphs.Add(table);
```

解釋：我們創建一個 `Aspose.Pdf.Table` 物件並將其新增至頁面的段落集合中，以確保表格顯示在頁面上。

## 步驟 6：設定列寬和邊框

PDF 中的表格需要定義列寬。我們還將添加邊框以使表格更易讀。

```csharp
// 設定表格的列寬
table.ColumnWidths = "40 100 100";

// 設定預設單元格邊框
table.DefaultCellBorder = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 0.1F);
```

解釋：我們設定三列的寬度，並為所有儲存格設定一個厚度為的預設邊框 `0。1F`.

## 步驟 7：將資料從 DataTable 匯入 PDF 表

現在，是時候將 DataTable 中的資料匯入到我們的 PDF 表中了。

```csharp
// 從 DataTable 匯入資料到 Table 對象
table.ImportDataTable(dataTable, true, 0, 0, dataTable.Rows.Count + 1, dataTable.Columns.Count);
```

解釋： `ImportDataTable` 方法將所有數據從 `DataTable` 到 PDF 表。這將使用 Excel 表中的資料填充表格。

## 步驟 8：設定標題行的樣式

讓我們透過更改背景顏色、字體和對齊方式來設定表格標題行的樣式。

```csharp
// 取得表中的第一行
Aspose.Pdf.Row headerRow = table.Rows[0];

// 設定標題行的樣式
foreach (Aspose.Pdf.Cell cell in headerRow.Cells)
{
    cell.BackgroundColor = Color.Blue;
    cell.DefaultCellTextState.Font = Aspose.Pdf.Text.FontRepository.FindFont("Helvetica-Oblique");
    cell.DefaultCellTextState.ForegroundColor = Color.Yellow;
    cell.DefaultCellTextState.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center;
}
```

說明：我們循環遍歷第一行（標題）中的所有單元格，並將它們的背景顏色設為藍色，文字顏色設為黃色，並將文字對齊到中心。

## 步驟 9：設定剩餘行的樣式

為了區分標題和其餘行，讓我們為其餘行添加不同的樣式。

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++)
{
    foreach (Aspose.Pdf.Cell cell in table.Rows[i].Cells)
    {
        cell.BackgroundColor = Color.Gray;
        cell.DefaultCellTextState.ForegroundColor = Color.White;
    }
}
```

說明：對於標題以外的所有行，我們設定灰色背景和白色文字顏色。

## 步驟 10：儲存 PDF 文檔

最後，將表格儲存為PDF文件。

```csharp
// 儲存 PDF
pdfDocument.Save(dataDir + "Exceldata_toPdf_table.pdf");
```

解釋：我們將 PDF 儲存到指定的目錄。瞧！您的 Excel 資料現在位於格式精美的 PDF 表格中。

## 結論

就是這樣！只需幾個步驟，您就可以使用 Aspose.PDF for .NET 將資料從 Excel 工作表匯出到 PDF 內的表格中。透過分解流程並在整個過程中進行樣式設計，您可以自訂輸出並確保資料看起來乾淨、專業。因此，下次有人遞給您 Excel 檔案並要求提供 PDF 報表時，您就知道該怎麼做了。

## 常見問題解答

### 我可以進一步自訂表格嗎？
絕對地！您可以修改顏色、字型、對齊方式，甚至為特定儲存格新增邊框。

### Aspose.PDF for .NET 免費嗎？
它提供免費試用，但要延長使用時間，您需要許可證。你可以 [在這裡購買](https://purchase。aspose.com/buy).

### 我可以只匯出特定的行和列嗎？
是的，您可以修改 `ExportDataTable` 方法導出特定範圍。

### 這適用於大型 Excel 文件嗎？
是的，Aspose.Cells 旨在高效處理大型 Excel 檔案。

### 如何為 PDF 新增更多頁面？
您可以使用 `pdfDocument.Pages.Add()` 新增所需數量的頁面。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}