---
"description": "使用 Aspose.PDF for .NET 渲染表格，輕鬆建立專業的 PDF。按照我們的逐步指南來掌握文件生成。"
"linktitle": "在 PDF 文件中渲染表格"
"second_title": "Aspose.PDF for .NET API參考"
"title": "在 PDF 文件中渲染表格"
"url": "/zh-hant/net/programming-with-tables/render-table/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 文件中渲染表格

## 介紹

以程式設計方式建立具有專業外觀的 PDF 似乎是一項艱鉅的任務，但使用 Aspose.PDF for .NET，它變得輕而易舉。無論您產生報表、發票或任何其他需要表格資料的文件類型，Aspose.PDF 都能提供您所需的工具。在本教學中，我們將逐步探討如何在 PDF 文件中呈現表格。最後，您將對如何輕鬆操作表格、管理頁面屬性和保存 PDF 文件有深入的了解。

## 先決條件

在深入研究程式碼之前，您需要做以下準備：

- Visual Studio：確保您的機器上安裝了 Visual Studio。你可以下載 [這裡](https://visualstudio。microsoft.com/downloads/).
- Aspose.PDF for .NET：您可以從 [Aspose 發佈頁面](https://releases。aspose.com/pdf/net/).
- C# 基礎知識：了解 C# 的基礎知識將幫助您更好地跟進。
- .NET Framework：理想情況下，請確保您在相容的 .NET 環境中運作。

一旦設定了這些先決條件，您就可以開始建立 PDF 文件了！

## 導入包

在 C# 檔案的開頭，您需要匯入必要的 Aspose.PDF 命名空間。這使您可以利用我們專案中的庫功能。

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

請確定您已在專案中新增了對 Aspose.PDF 庫的必要引用。如果您使用 NuGet，則可以透過搜尋輕鬆新增 `Aspose。PDF`.

現在我們已經完成了所有設置，讓我們將流程分解為可管理的步驟，以便在 PDF 文件中呈現表格。不用擔心;我將透過清晰的說明引導您完成每個步驟！

## 步驟 1：設定文件和頁面訊息

首先，我們需要建立一個新文件並配置其頁面設定。具體操作如下：

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document();
PageInfo pageInfo = doc.PageInfo;
Aspose.Pdf.MarginInfo marginInfo = pageInfo.Margin;

marginInfo.Left = 37;
marginInfo.Right = 37;
marginInfo.Top = 37;
marginInfo.Bottom = 37;

pageInfo.IsLandscape = true;
```

解釋： 
- 我們先定義文檔的保存位置（`dataDir`）。 
- 然後，我們建立一個新的實例 `Document` 班級。 
- 我們配置頁邊距以在表格周圍創建一些喘息空間。
- 最後，我們將文件設為橫向，這有助於顯示更寬的表格。

## 步驟 2：建立第一個表

接下來，讓我們建立第一個表並用一些範例資料填充它：

```csharp
Aspose.Pdf.Table table = new Aspose.Pdf.Table();
table.ColumnWidths = "50 100"; // 定義列寬
```

解釋：在這裡，我們實例化 `Table` 類別並設定列寬。第一列寬度為 50 個單位，第二列寬度為 100 個單位。

## 步驟 3：用行填滿表

現在，讓我們循環向表中新增行：

```csharp
Page curPage = doc.Pages.Add(); // 新增頁面
for (int i = 1; i <= 120; i++)
{
    Aspose.Pdf.Row row = table.Rows.Add();
    row.FixedRowHeight = 15; // 設定固定行高
    
    Aspose.Pdf.Cell cell1 = row.Cells.Add();
    cell1.Paragraphs.Add(new TextFragment("Content 1"));
    
    Aspose.Pdf.Cell cell2 = row.Cells.Add();
    cell2.Paragraphs.Add(new TextFragment("HHHHH"));
}
```

解釋： 
- 這裡我們建立一個新頁面來新增我們的表單。
- 我們使用 `for` 循環向我們的表格添加 120 行。每行的固定高度為 15 個單位。
- 在每一行內，我們添加兩個單元格並用文字填充它們。

## 步驟 4：將第一個表格新增至頁面

一旦我們填充了表格，我們就會將其添加到當前頁面：

```csharp
Aspose.Pdf.Paragraphs paragraphs = curPage.Paragraphs;
paragraphs.Add(table);
```

說明：此步驟只是將我們建立的表格新增至目前頁面的段落中，使表格在 PDF 文件中可見。

## 步驟 5：建立第二個表

現在，讓我們製作具有不同內容的第二個表格並將其添加到新頁面：

```csharp
Aspose.Pdf.Table table1 = new Aspose.Pdf.Table();
table1.ColumnWidths = "100 100";
for (int i = 1; i <= 10; i++)
{
    Aspose.Pdf.Row row = table1.Rows.Add();
    Aspose.Pdf.Cell cell1 = row.Cells.Add();
    cell1.Paragraphs.Add(new TextFragment("LAAAAAAA"));
    
    Aspose.Pdf.Cell cell2 = row.Cells.Add();
    cell2.Paragraphs.Add(new TextFragment("LAAGGGGGG"));
}
table1.IsInNewPage = true; // 設定第二個表格出現在新頁面上
paragraphs.Add(table1);
```

解釋： 
- 此程式碼片段建立了一個具有兩個欄位的新表，寬度均為 100 個單位。
- 一個 `for` 循環新增 10 行包含範例內容的行。
- 透過設定 `table1.IsInNewPage` 為真，我們確保此表出現在新頁面上，使內容保持井然有序。

## 步驟6：儲存文檔

現在我們的表格已經準備好了，讓我們儲存我們的文件：

```csharp
dataDir = dataDir + "IsNewPageProperty_Test_out.pdf";
doc.Save(dataDir);
```

說明：我們指定檔案名稱並將文件保存在定義的目錄中。運行此程式碼時，將產生一個標題為 `IsNewPageProperty_Test_out.pdf` 將在您指定的位置建立。

## 步驟7：確認訊息

最後，為了讓用戶知道一切順利，我們可以添加一個友善的控制台訊息：

```csharp
Console.WriteLine("\nTable rendered successfully on a page.\nFile saved at " + dataDir);
```

說明：這是一種確認操作是否成功以及用戶可以在哪裡找到他們的新 PDF 文件的簡單方法。

## 結論

就是這樣！您已成功使用 Aspose.PDF for .NET 在 PDF 文件中呈現表格。只需幾行程式碼，您就可以以有組織的格式處理和呈現大量數據，使您的文件既資訊豐富又具有視覺吸引力。無論您處理的是庫存清單、財務報告還是教育文件，表格都是一目了然地傳達複雜訊息的絕佳方式。

## 常見問題解答

### 我可以自訂 Aspose.PDF 中表格的外觀嗎？  
絕對地！您可以調整顏色、邊框、字體樣式和其他屬性來增強表格的外觀。

### Aspose.PDF 可以免費使用嗎？  
Aspose.PDF 提供免費試用版，但用於商業用途則需購買。您可以查看定價 [這裡](https://purchase。aspose.com/buy).

### 我如何獲得 Aspose.PDF 問題的支援？  
您可以從 Aspose 支援論壇尋求協助 [這裡](https://forum。aspose.com/c/pdf/10).

### 免費試用版有什麼限制嗎？  
是的，試用版可能有一定的限制，例如在生成的文件上添加浮水印。為了獲得完整功能，請考慮取得臨時許可證 [這裡](https://purchase。aspose.com/temporary-license/).

### 在哪裡可以找到有關 Aspose.PDF 功能的更多資訊？  
您可以探索可用的綜合文檔 [這裡](https://reference。aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}