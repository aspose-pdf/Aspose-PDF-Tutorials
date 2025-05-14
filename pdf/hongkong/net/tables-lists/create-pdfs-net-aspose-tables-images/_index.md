---
"date": "2025-04-11"
"description": "學習使用 Aspose.PDF for .NET 建立具有表格和圖像的專業外觀 PDF。本教程涵蓋了從基本設定到高級功能的所有內容。"
"title": "使用 Aspose&#58; 在 .NET 中建立 PDF輕鬆新增表格和圖像"
"url": "/zh-hant/net/tables-lists/create-pdfs-net-aspose-tables-images/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose 在 .NET 中建立 PDF：輕鬆新增表格和圖像

在當今數位時代，高效管理文件工作流程對於各個行業都至關重要。無論是產生報告、發票還是演示文稿，創建帶有表格和圖像等嵌入內容的專業外觀 PDF 通常都是必不可少的。本教學將指導您使用 Aspose.PDF for .NET 輕鬆建立動態 PDF。

## 您將學到什麼
- 如何在 .NET 中實例化和操作 PDF 文件。
- 在 PDF 文件中新增表格的步驟。
- 在表格單元格中將圖像與文字一起嵌入的技術。
- 優化在 .NET 應用程式中使用 Aspose.PDF 時的效能。

在開始創建我們的第一個 PDF 之前，讓我們先回顧一下先決條件！

## 先決條件
在開始之前，請確保您已具備以下條件：
- **Aspose.PDF for .NET函式庫**：安裝此程式庫以處理 PDF 文件。
- **開發環境**：在您的機器上設定C#開發環境。建議使用 Visual Studio。
- **C# 基礎知識**：熟悉 C# 程式設計和物件導向概念將會很有幫助。

## 設定 Aspose.PDF for .NET
要開始建立 PDF，您必須先在專案中安裝 Aspose.PDF 庫。方法如下：

**使用 .NET CLI：**
```bash
dotnet add package Aspose.PDF
```

**使用套件管理器控制台：**
```powershell
Install-Package Aspose.PDF
```

**透過 NuGet 套件管理器 UI：**
1. 在 Visual Studio 中開啟您的專案。
2. 導航至“NuGet 套件管理器”。
3. 搜尋“Aspose.PDF”並安裝最新版本。

### 許可證獲取
為了充分利用 Aspose.PDF 的功能，您可能需要許可證：
- **免費試用**：從免費試用開始測試功能。
- **臨時執照**：獲得臨時許可證以進行擴展測試（對開發有用）。
- **購買**：對於生產用途，請購買完整許可證。

### 基本初始化
以下是如何在專案中初始化 Aspose.PDF 函式庫：
```csharp
using Aspose.Pdf;

// 初始化文檔對象
document doc = new Document();
```

## 實施指南
現在讓我們逐步了解如何使用 Aspose.PDF for .NET 實作 PDF 功能。

### 建立並實例化 PDF 文件和頁面
#### 概述
建立 PDF 首先要實例化 `Document` 類，代表你的整個 PDF。透過利用 `Pages` 收集 `Document`。

**實施步驟：**
##### 步驟 1：建立新的 PDF 文檔
```csharp
// 實例化文檔對象 
document doc = new Document();
```
此步驟初始化一個空白的 PDF 文件。

##### 第 2 步：新增頁面
```csharp
// 在 PDF 中建立頁面 
Page page = doc.Pages.Add();
```
在這裡，我們為文件新增一個新頁面。這 `Pages` 集合可讓您輕鬆管理和操作 PDF 文件中的所有頁面。

##### 步驟3：儲存文檔
```csharp
string outputDirectory = "YOUR_OUTPUT_DIRECTORY";
doc.Save(outputDirectory + "/NewDocumentPage.pdf");
```
最後，將新建立的 PDF 儲存到指定目錄。確保 `outputDirectory` 正確設定以避免錯誤。

### 建立並新增表格至 PDF 頁面
#### 概述
表格對於在文件中系統地顯示資料至關重要。 Aspose.PDF 可讓您建立具有特定屬性的表格，例如列寬、邊距和儲存格填入。

**實施步驟：**
##### 步驟 1：建立文件並新增頁面
```csharp
// 實例化文檔對象 
document doc = new Document();
Page page = doc.Pages.Add();
```
重新建立 PDF 文件並像以前一樣新增初始頁面。

##### 步驟 2：實例化表對象
```csharp
Table table1 = new Table();
page.Paragraphs.Add(table1);
table1.ColumnWidths = "120 270";
```
創建一個 `Table` 對象，設定其列寬，並將其新增至 PDF 頁面。此設定有助於定義表的結構。

##### 步驟 3：配置邊距
```csharp
MarginInfo margin = new MarginInfo() {
    Top = 5f,
    Left = 5f,
    Right = 5f,
    Bottom = 5f
};
table1.DefaultCellPadding = margin;
```
設定邊距可確保表格儲存格內的內容間距適當，進而增強可讀性。

##### 步驟4：儲存文檔
```csharp
string outputDirectory = "YOUR_OUTPUT_DIRECTORY";
doc.Save(outputDirectory + "/DocumentWithTable.pdf");
```
按照先前的操作儲存您的文件。確保更換 `outputDirectory` 具有有效路徑。

### 在表格單元格中新增圖像及其周圍的文本
#### 概述
在表格單元格中嵌入圖像和文字可以使您的 PDF 更具吸引力。本節示範如何在表格單元格中的 HTML 格式的文字旁邊新增圖像。

**實施步驟：**
##### 步驟 1：設定文件、頁面和表格
```csharp
document doc = new Document();
Page page = doc.Pages.Add();

Table table1 = new Table();
page.Paragraphs.Add(table1);
table1.ColumnWidths = "120 270";

MarginInfo margin = new MarginInfo() {
    Top = 5f,
    Left = 5f,
    Right = 5f,
    Bottom = 5f
};
table1.DefaultCellPadding = margin;
```
初始化您的文檔，添加頁面和表格，如前面部分所述。

##### 步驟 2：在表格單元格中新增圖像
```csharp
Row row1 = table1.Rows.Add();
Image logo = new Image();
logo.File = "YOUR_DOCUMENT_DIRECTORY/aspose-logo.jpg";
logo.FixHeight = 120;
logo.FixWidth = 110;

row1.Cells.Add();
row1.Cells[0].Paragraphs.Add(logo);
```
創建一個 `Row`，新增影像對象，並指定其檔案路徑和尺寸等屬性。然後，將圖像新增至表格單元格。

##### 步驟 3：新增 HTML 格式的文本
```csharp
string TitleString = "<font face=\"Arial\" size=6 color=\"#101090\"><b> Aspose.Pdf for .NET</b></font>";
string BodyString1 = "<font face=\"Arial\" size=2><br/>Aspose.Pdf for .NET is a non-graphical PDF document reporting component...</font>";

HtmlFragment TitleText = new HtmlFragment(TitleString + BodyString1);
row1.Cells.Add();
row1.Cells[1].Paragraphs.Add(TitleText);

row1.Cells[1].VerticalAlignment = VerticalAlignment.Top;
```
為文字建立 HTML 字串並使用 `HtmlFragment` 將這些字串新增到同一行中另一個單元格的圖像旁邊。

##### 步驟4：儲存文檔
```csharp
string outputDirectory = "YOUR_OUTPUT_DIRECTORY";
doc.Save(outputDirectory + "/PlacingTextAroundImage.pdf");
```
儲存您的最終文件。確保更換 `outputDirectory` 使用有效路徑以避免文件保存問題。

## 實際應用
Aspose.PDF for .NET 可用於各種實際場景：
1. **自動產生報告**：從資料庫或電子表格等資料來源自動建立 PDF 報告。
2. **發票創建**：產生專業發票，以表格形式嵌入公司商標和詳細的交易記錄。
3. **行銷手冊**：設計具有視覺吸引力的小冊子，其中包含用於產品描述的圖像和表格格式的文字。

整合可能性包括與 CRM 系統連結以將客戶資料直接拉入 PDF 或與電子商務平台整合以獲取訂單摘要。

## 性能考慮
使用 Aspose.PDF 時，請考慮以下技巧來優化效能：
- **簡化記憶體使用**：當不再需要物件時，將其丟棄以釋放記憶體。
- **批次處理**：如果處理大量文件，可以批次處理以提高效率。
- **優化影像尺寸**：在將圖像嵌入 PDF 之前調整其大小，以縮短載入時間並減少檔案大小。

## 結論
一旦了解了基礎知識，使用 Aspose.PDF for .NET 建立包含表格和圖像的 PDF 就非常簡單了。透過遵循本指南，您可以有效率地產生符合您需求的專業文件。探索 Aspose.PDF 的更多功能以增強您的文件處理能力。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}