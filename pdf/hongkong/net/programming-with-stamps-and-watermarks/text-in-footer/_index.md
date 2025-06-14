---
"description": "了解如何使用 Aspose.PDF for .NET 輕鬆地將文字新增至 PDF 檔案的頁尾。包含逐步指南，可實現無縫整合。"
"linktitle": "PDF 檔案頁尾中的文字"
"second_title": "Aspose.PDF for .NET API參考"
"title": "PDF 檔案頁尾中的文字"
"url": "/zh-hant/net/programming-with-stamps-and-watermarks/text-in-footer/"
"weight": 180
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF 檔案頁尾中的文字

## 介紹

您是否希望使用 Aspose.PDF for .NET 在 PDF 檔案的頁尾中新增自訂文字？您來對地方了！無論您想包含頁碼、日期還是任何其他自訂文本，本教程都會引導您完成整個過程。使用 Aspose.PDF（一個強大的 PDF 操作庫），新增頁尾變得非常容易。在本文中，我們將逐步探討在 PDF 檔案的每一頁頁腳中新增文字的過程。它快速、簡單，非常適合想要在 .NET 應用程式中自動化 PDF 客製化的人。


## 先決條件

在開始編碼之前，請確保您已準備好一切：

- Aspose.PDF for .NET：請確定您已安裝 Aspose.PDF for .NET。如果沒有，你可以 [點此下載](https://releases。aspose.com/pdf/net/).
- IDE：您需要一個像 Visual Studio 這樣的開發環境。
- C# 基礎：需要對 C# 和 .NET 有基本的了解。
- 許可證：雖然您可以在評估模式下使用 Aspose.PDF，但為了獲得完整功能，請考慮獲取 [免費試用](https://releases.aspose.com/) 或申請 [臨時執照](https://purchase。aspose.com/temporary-license/).

## 導入包

在開始編碼部分之前，請確保導入必要的命名空間。這將確保 Aspose.PDF 庫中的類別和方法在您的專案中可用。

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

現在您已準備就緒，讓我們將向 PDF 文件頁腳添加文字的過程分解為易於遵循的步驟。

## 步驟 1：初始化項目並設定文件目錄

在處理 PDF 檔案之前，您需要指定文件目錄的路徑。這是您的 PDF 文件所在的位置，也是修改後的文件的保存位置。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

在這裡，替換 `"YOUR DOCUMENT DIRECTORY"` 使用您的資料夾的實際路徑。該資料夾將包含原始 PDF 文件，並將作為修改後文件的輸出位置。

## 第 2 步：載入 PDF 文檔

下一步是將 PDF 文件載入到您的專案中。這 `Document` Aspose.PDF 中的類別可讓您開啟和操作現有的 PDF 文件。

```csharp
// 開啟文件
Document pdfDocument = new Document(dataDir + "TextinFooter.pdf");
```

這裡， `TextinFooter.pdf` 是我們正在處理的文件。您可以用自己的檔案名稱替換它。

## 步驟 3：建立頁尾文本

現在，讓我們建立將印在每頁上的頁腳文字。這是使用 `TextStamp` 班級。您定義的文字將用作所有頁面的頁腳。

```csharp
// 創建頁腳
TextStamp textStamp = new TextStamp("Footer Text");
```

在這種情況下，我們創建了一個簡單的頁腳文本，即「頁腳文本」。請隨意使用您自己的資訊進行客製化。如果您願意，它可以是“機密”或頁碼之類的內容。

## 步驟 4：設定頁尾屬性

為了正確定位頁腳，我們需要調整一些屬性，例如邊距、對齊方式和定位。這 `TextStamp` 這類讓您完全控制頁尾文字的顯示位置和方式。

```csharp
// 設定圖章的屬性
textStamp.BottomMargin = 10;
textStamp.HorizontalAlignment = HorizontalAlignment.Center;
textStamp.VerticalAlignment = VerticalAlignment.Bottom;
```

這裡，我們將底部邊距設定為 10 個單位，將文字水平對齊到中心，並將其垂直放置在頁面底部。您可以根據您的特定佈局需求調整這些值。

## 步驟 5：將頁尾套用至所有頁面

現在到了有趣的部分——將頁腳應用到 PDF 中的每一頁。透過遍歷文件中的所有頁面，我們可以為每個頁面添加頁腳文字。

```csharp
// 在所有頁面上新增頁腳
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(textStamp);
}
```

此循環可確保頁腳被標記在文件的所有頁面上，無論 PDF 有多少頁。

## 步驟6：儲存更新的PDF文件

一旦將頁腳新增到所有頁面後，最後一步就是將修改後的 PDF 檔案儲存到指定的目錄。

```csharp
dataDir = dataDir + "TextinFooter_out.pdf";
// 儲存更新的 PDF 文件
pdfDocument.Save(dataDir);
```

我們正在用新名稱儲存文件， `TextinFooter_out.pdf`，位於同一目錄中。請根據需要隨意重命名。

## 步驟7：確認成功

最後，您可以向控制台列印成功訊息，讓使用者知道 PDF 已成功更新。

```csharp
Console.WriteLine("\nText in footer added successfully.\nFile saved at " + dataDir);
```

就是這樣！您已成功將文字新增至 PDF 中每一頁的頁尾。

## 結論

使用 Aspose.PDF for .NET 為 PDF 文件新增頁尾是自訂 PDF 檔案的簡單且強大的方法。只需幾行程式碼，您就可以在文件的每一頁中添加個人化文本，例如日期、標題或頁碼。透過遵循本指南，您現在就可以掌握在 .NET 應用程式中實現此功能的知識。

## 常見問題解答

### 我可以為 PDF 中的每一頁添加不同的頁尾嗎？  
是的，您可以透過指定不同的頁腳為每個頁面新增唯一的頁腳 `TextStamp` 每個頁面的物件。

### 如何變更頁尾文字的字體樣式？  
您可以使用 `TextStamp.TextState` 屬性來設定字體、大小和顏色。

### 我可以在頁腳中添加圖像而不是文字嗎？  
是的，你可以使用 `ImageStamp` 將圖像新增至 PDF 檔案的頁尾。

### 是否可以僅向特定頁面新增頁尾？  
絕對地！您可以透過定位特定 `Page` 對象。

### 如何從 PDF 中刪除現有的頁尾？  
您可以使用 `Page.DeleteStampById` 方法或使用 `RemoveStamp` 刪除所有郵票。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}