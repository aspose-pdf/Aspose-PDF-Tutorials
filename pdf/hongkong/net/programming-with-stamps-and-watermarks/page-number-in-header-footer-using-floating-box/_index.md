---
"description": "在本逐步教學中，使用 Aspose.PDF for .NET 的浮動框輕鬆在 PDF 頁首和頁尾中新增頁碼。"
"linktitle": "使用浮動框在頁首頁腳中顯示頁碼"
"second_title": "Aspose.PDF for .NET API參考"
"title": "使用浮動框在頁首頁腳中顯示頁碼"
"url": "/zh-hant/net/programming-with-stamps-and-watermarks/page-number-in-header-footer-using-floating-box/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用浮動框在頁首頁腳中顯示頁碼

## 介紹

當談到以程式設計方式管理 PDF 文件時，Aspose.PDF for .NET 是一款出色的工具。它簡化了我們在 .NET 應用程式中建立、編輯和操作 PDF 文件的方式。無論您產生發票、報告或任何類型的文檔，優雅地添加頁碼都可以提高 PDF 的專業性和組織性。在本教程中，我們將深入研究如何使用浮動框在 PDF 的頁首和頁尾中添加頁碼。準備好開始了嗎？我們走吧！

## 先決條件

在我們開始這段令人興奮的 PDF 操作之旅之前，您需要先做好以下幾件事：

### .NET 環境設定
確保您有一個.NET開發環境。您可以使用 Visual Studio，它是 .NET 應用程式開發人員的熱門選擇。

### Aspose.PDF庫
安裝 Aspose.PDF 庫。您可以從以下網站輕鬆下載：

- [下載 Aspose.PDF for .NET](https://releases.aspose.com/pdf/net/)

### C# 程式設計基礎知識
對 C# 的基本了解將幫助您掌握本教程中介紹的概念和編碼片段。

### 存取文件
擁有 [Aspose.PDF文檔](https://reference.aspose.com/pdf/net/) 方便參考和深入探索任何附加功能。

## 導入包

首先，您需要在專案中匯入必要的套件。這確保了 Aspose.PDF 組件可以在您的程式碼中使用。具體操作如下：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

現在，讓我們將使用浮動框添加頁碼的過程分解為易於管理的步驟。請跟著我們一起走過去。

## 步驟 1：設定文檔環境

讓我們先指定儲存 PDF 文件的目錄。這很關鍵，因為它決定了輸出檔案的保存位置。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

代替 `YOUR DOCUMENT DIRECTORY` 選擇要儲存輸出 PDF 檔案的路徑。

## 步驟 2：實例化文檔

下一步是建立一個新的 PDF 文件。這涉及使用 `Document` Aspose.PDF 庫中的類別。

```csharp
// 實例化 Document 實例
Aspose.Pdf.Document pdf = new Aspose.Pdf.Document();
```
在這裡，我們建立一個新的實例 `Document` 類，它是我們進行操作的畫布。

## 步驟 3：新增頁面

現在，讓我們為我們的 PDF 文件新增一個頁面。每個 PDF 至少需要一頁，對嗎？

```csharp
// 在 PDF 文件中新增頁面
Aspose.Pdf.Page page = pdf.Pages.Add();
```
此程式碼片段為我們的文件添加了一個新頁面，使其準備好接收內容，包括帶有頁碼的浮動框。

## 步驟 4：建立浮動框

接下來，是時候建立用於儲存頁碼的浮動框了。這 `FloatingBox` 類別允許我們在頁面上自由定位內容。

```csharp
// 初始化 FloatingBox 類別的新實例
Aspose.Pdf.FloatingBox box1 = new Aspose.Pdf.FloatingBox(140, 80);
```
這裡，參數 `(140, 80)` 指定浮動框的寬度和高度。您可以根據您的佈局偏好調整這些值。

## 步驟5：定位浮動框

定位是關鍵！您要確定頁碼在頁面上出現的位置。你將與 `Left` 和 `Top` 屬性來指定位置。

```csharp
// 表示段落左側位置的浮點數值
box1.Left = 2;
// 表示段落頂部位置的浮點數值
box1.Top = 10;
```
這些值決定了浮動框在頁面上的位置。請隨意嘗試它們，看看哪種方式最適合您的文件。

## 步驟 6：使用頁碼巨集新增文本

現在，我們將新增一個動態顯示頁碼的字串。這就是奇蹟發生的地方！

```csharp
// 將巨集加入到 FloatingBox 的段落集合中
box1.Paragraphs.Add(new Aspose.Pdf.Text.TextFragment("Page: ($p/ $P )"));
```
在這種情況下， `($p/ $P)` 是一個顯示目前頁碼的巨集（`$p`) 和總頁數 (`$P`）。因此，它將文字格式化為類似「Page: 1/5」的內容。

## 步驟 7：將浮動框新增至頁面

現在是時候將浮動框連同頁碼文字新增到我們新建立的頁面了。

```csharp
// 在頁面上新增一個floatingBox
page.Paragraphs.Add(box1);
```
此行實質上將浮動框嵌入到頁面中，使其成為文件佈局的一部分。 

## 步驟8：儲存文檔

最後，別忘了保存你的工作！最後一步是使用適當的檔案名稱來儲存您的 PDF 文件。

```csharp
// 儲存文件
pdf.Save(dataDir + "PageNumberinHeaderFooterUsingFloatingBox_out.pdf");
```
確保指定的路徑包含您想要的檔案名稱。現在，帶有頁碼的精彩 PDF 已建立！ 

## 結論

各位，就是這樣！使用 Aspose.PDF for .NET 將頁碼加入 PDF 的頁首和頁尾就是這麼簡單。只需幾行程式碼，您就踏上了掌握應用程式中文件處理的旅程。不要猶豫嘗試不同的佈局和格式——畢竟，創造力是無止境的！準備好產生專業文件了嗎？戴上你的編碼帽並開始實驗。

## 常見問題解答

### 我可以自訂頁碼文字的外觀嗎？  
是的，您可以透過調整 `TextFragment` 特性。

### Aspose.PDF 可以免費使用嗎？  
雖然 Aspose.PDF 提供免費試用，但它是用於生產用途的付費產品。你可以 [在這裡購買](https://purchase。aspose.com/buy).

### 在哪裡可以找到更詳細的文件？  
您可以找到有關 [Aspose.PDF 文件網站](https://reference。aspose.com/pdf/net/).

### 如何將頁首和頁尾套用至多個頁面？  
您可以循環遍歷文件中的所有頁面，並以類似的方式將浮動框套用到每個頁面。

### 如果我需要附加功能的支援怎麼辦？  
如有任何其他問題或需要支持，您可以訪問 [Aspose 論壇](https://forum。aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}