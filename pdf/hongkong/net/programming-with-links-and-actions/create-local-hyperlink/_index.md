---
"description": "透過我們的逐步指南，了解如何使用 Aspose.PDF for .NET 輕鬆在 PDF 檔案中建立本機超連結。"
"linktitle": "在 PDF 文件中建立本地超鏈接"
"second_title": "Aspose.PDF for .NET API參考"
"title": "在 PDF 文件中建立本地超鏈接"
"url": "/zh-hant/net/programming-with-links-and-actions/create-local-hyperlink/"
"weight": 40
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 文件中建立本地超鏈接

## 介紹

在本指南中，我們將引導您完成使用 Aspose.PDF for .NET 在 PDF 檔案中建立本機超連結的過程。我們將清楚地分解每個步驟，確保即使您是 PDF 操作領域的新手，也能毫不費力地跟上。

## 先決條件

在深入研究程式碼之前，讓我們確保您擁有所需的一切：

1. Visual Studio：您需要它來開發您的 .NET 應用程式。從下載 [網站](https://visualstudio。microsoft.com/).
2. Aspose.PDF for .NET：您可以透過 [下載連結在這裡](https://releases.aspose.com/pdf/net/)。它具有一組豐富的 PDF 操作功能。
3. C# 基礎：稍微熟悉一下 C# 程式設計會有所幫助，但不用擔心；我們將逐行檢查程式碼。
4. .NET Framework：確保您的機器上安裝了 .NET 框架。您可以在 Aspose.PDF 上查看要求 [文件](https://reference。aspose.com/pdf/net/).

設定這些先決條件後，您就可以學習如何在 PDF 文件中建立本機超連結了！

## 導入包

現在您已經做好了一切準備，是時候在您的 C# 專案中匯入必要的套件了。 Aspose.PDF 庫包含我們需要的所有類別。具體操作如下：

### 打開你的專案

開啟現有的 .NET 專案或在 Visual Studio 中建立一個新專案。如果您是剛開始，請從啟動畫面選擇「建立新專案」。

### 新增對 Aspose.PDF 的引用

在解決方案資源管理器中的專案資料夾中右鍵按一下「依賴項」。選擇“管理 NuGet 套件”，然後搜尋 `Aspose.PDF`。安裝最新版本。這將帶來創建和處理 PDF 所需的所有工具。

### 導入命名空間

在 .cs 檔案的頂部，新增 Aspose.PDF 庫的使用指令，如下所示：

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

這樣，您就可以存取圖書館的功能。

讓我們將建立本地超連結的過程分解為簡單的步驟。每個步驟都會得到全面解釋，以幫助您理解背後的邏輯。

## 步驟 1：設定文檔實例

在此步驟中，您將建立 Document 類別的新實例，它代表您將要使用的 PDF 檔案。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // 設定文檔目錄
Document doc = new Document(); // 建立 Document 實例
```
這 `dataDir` 變數是您新建立的 PDF 所在的位置。你需要更換 `"YOUR DOCUMENT DIRECTORY"` 使用系統上的實際路徑。這 `Document` 這個類別會建立一個新的 PDF 文檔，我們可以在其中添加頁面和連結。

## 步驟 2：新增頁面

接下來，您將向 PDF 文件新增一頁。 

```csharp
Page page = doc.Pages.Add(); // 將頁面新增至頁面集合
```
這 `Pages.Add()` 方法會為文件新增一個新頁面。您的所有內容都將儲存在這裡。

## 步驟 3：建立文字片段

現在，讓我們建立一段可作為可點擊連結的文字。

```csharp
Aspose.Pdf.Text.TextFragment text = new Aspose.Pdf.Text.TextFragment("link page number test to page 7");
```
這 `TextFragment` 代表 PDF 中的一段文字。在這裡，我們創建一個鏈接，告訴用戶它將帶他們到第 7 頁。

## 步驟4：建立本地超連結

這就是奇蹟發生的地方！您需要建立一個本地超鏈接，告訴文字片段指向哪裡。

```csharp
Aspose.Pdf.LocalHyperlink link = new Aspose.Pdf.LocalHyperlink(); // 建立本地超連結
link.TargetPageNumber = 7; // 設定連結實例的目標頁面
text.Hyperlink = link; // 設定 TextFragment 超鏈接
```
這 `LocalHyperlink` 類別允許我們指向同一文檔中的其他頁面。透過設定 `TargetPageNumber` 到 7，您告訴超連結在點擊時跳到該特定頁面。

## 步驟 5：將文字片段新增至頁面

設定超連結後，就可以將文字片段加入我們建立的頁面中了。

```csharp
page.Paragraphs.Add(text); // 將文字新增至頁面的段落集合
```
此行將可點擊的文字新增至頁面的段落集合中。

## 步驟 6：建立另一個文字片段（可選）

讓我們新增另一個超連結以導覽回第 1 頁。

```csharp
text = new TextFragment("link page number test to page 1"); // 建立新的 TextFragment
text.IsInNewPage = true; // 將其新增至新頁面
```
創建新的 `TextFragment` 對於第二個鏈接，我們設置 `IsInNewPage` 為 true，表示此文字將出現在新頁面上。

## 步驟7：設定第二個本地超鏈接

與之前一樣，您將為第 1 頁建立另一個本地超連結。

```csharp
link = new LocalHyperlink(); // 建立另一個本地超連結實例
link.TargetPageNumber = 1; // 設定第二個超連結的目標頁面
text.Hyperlink = link; // 設定第二個 TextFragment 的鏈接
```
此超連結指向第 1 頁，允許使用者在到達第二頁時跳轉回來。

## 步驟 8：將第二個文字片段新增至新頁面

現在，讓我們將此文字新增到其頁面中。

```csharp
page.Paragraphs.Add(text); // 將文字加入到頁面物件的段落集合中
```
與步驟 5 類似，此行將新的超連結文字新增至新建立的頁面。

## 步驟9：儲存文檔

最後，是時候保存你的辛勤成果了！ 

```csharp
dataDir = dataDir + "CreateLocalHyperlink_out.pdf"; // 指定輸出檔名
doc.Save(dataDir); // 儲存更新的文檔
Console.WriteLine("\nLocal hyperlink created successfully.\nFile saved at " + dataDir);
```
這會將您的目錄路徑與檔案名稱結合在一起。這 `Save()` 方法保存您的文檔，並且確認訊息會讓您知道一切順利！

## 結論

使用 Aspose.PDF for .NET 在 PDF 檔案中建立本機超連結不僅僅是一個很酷的技巧；這是一個增強導航和使用者體驗的實用功能。現在您已經掌握了相關知識，可以直接向讀者提供他們需要的資訊。回想一下我們最初的比喻——不再有迷失的靈魂在無盡的頁面中徘徊。

## 常見問題解答

### 什麼是 Aspose.PDF for .NET？
Aspose.PDF for .NET 是一個函式庫，可讓開發人員使用 .NET 框架以程式設計方式建立、操作和轉換 PDF 文件。

### 我可以建立指向外部網頁的超連結嗎？
是的，除了 PDF 內的本機超連結之外，Aspose.PDF 還支援建立到外部 URL 的超連結。

### Aspose.PDF 有免費試用版嗎？
絕對地！您可以從 [地點](https://releases。aspose.com/).

### Aspose 支援哪些程式語言？
Aspose 提供各種程式語言的函式庫，包括 Java、C++ 和 Python 等。

### 如何獲得 Aspose 產品的支援？
您可以透過以下方式尋求支持 [Aspose 論壇](https://forum。aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}