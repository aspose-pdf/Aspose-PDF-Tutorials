---
"description": "透過我們的逐步指南學習如何使用 Aspose.PDF for .NET 在 PDF 文件中新增文字標記並提升您的文件簡報效果。"
"linktitle": "在 PDF 檔案中加入文字印章"
"second_title": "Aspose.PDF for .NET API參考"
"title": "在 PDF 檔案中加入文字印章"
"url": "/zh-hant/net/programming-with-stamps-and-watermarks/add-text-stamp/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 檔案中加入文字印章

## 介紹

在當今數位時代，PDF 是共享和傳遞文件的常用格式。無論您是開發人員、內容創作者，還是只是想增強其 PDF 文件的人，了解如何以程式設計方式操作 PDF 都可能改變遊戲規則。您可能想要利用的一個巧妙功能是在 PDF 文件中添加文字標記。添加文字印章可以為您的文件增添專業氣息或傳達重要訊息，例如“樣本”、“機密”，甚至是浮水印。

## 先決條件

在我們進入程式碼之前，需要滿足一些先決條件以確保所有設定都正確。您需要準備以下物品：

1. Aspose.PDF for .NET：請確定您的專案中已安裝了 Aspose.PDF 庫。如果你還沒有這樣做，你可以從 [Aspose 網站](https://releases。aspose.com/pdf/net/).
2. Visual Studio 或相容 IDE：您將需要一個開發環境來編寫和執行您的 .NET 程式碼。 Visual Studio 是開發人員最常見的選擇。
3. C# 基礎知識：熟悉 C# 和物件導向程式設計原理將幫助您更好地理解範例。
4. 範例 PDF 檔案：您應該有一個可以使用的 PDF 檔案。您可以建立一個基本的 PDF 或使用任何現有的 PDF 來測試其功能。

一旦解決了這些先決條件，我們就可以繼續編碼了！

## 導入包

現在，讓我們導入必要的套件。此步驟至關重要，因為它使 Aspose 庫中的類別和方法在您的專案中可用。

### 匯入 Aspose.PDF 程式集

首先，您需要匯入 Aspose.PDF 命名空間。在 C# 檔案的頂部，加入以下 using 指令：

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

這將使您能夠存取建立和操作 PDF 文件所必需的類別。

現在，讓我們進入本教學的重點。我們將把這個過程分解為清晰、簡潔的步驟。每個步驟都會引導您完成在 PDF 檔案中新增文字標記的程式碼。

## 步驟 1：設定文檔目錄

首先，您需要建立儲存 PDF 文件的目錄。這意味著您的程式碼需要知道在哪裡找到您想要編輯的 PDF 檔案。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

解釋：替換 `"YOUR DOCUMENT DIRECTORY"` 與您的 PDF 檔案的實際路徑（`AddTextStamp.pdf`) 被儲存。此路徑稍後用於開啟和儲存修改後的 PDF。

## 第 2 步：開啟 PDF 文檔

接下來，我們將使用 `Document` 來自 Aspose.PDF 命名空間的類別。

```csharp
// 開啟文件
Document pdfDocument = new Document(dataDir + "AddTextStamp.pdf");
```

解釋：在這裡，我們正在創建一個 `Document` 類別並將路徑傳遞給我們的 PDF 文件。這將加載 PDF，以便我們可以對其進行操作。

## 步驟 3：建立文字印章

現在，我們將建立一個文字印章，稍後將其應用到我們的 PDF 文件中。

```csharp
// 建立文字戳
TextStamp textStamp = new TextStamp("Sample Stamp");
```

解釋： `TextStamp` 物件是使用您想要顯示的文字建立的。在這種情況下，我們使用「樣本印章」作為印章的文字。

## 步驟4：設定圖章屬性

為了自訂您的印章，我們可以設定各種屬性，例如背景顏色、位置和旋轉。現在就開始吧：

```csharp
// 設定圖章是否為背景
textStamp.Background = true;

// 設定原點
textStamp.XIndent = 100;
textStamp.YIndent = 100;

// 旋轉印章
textStamp.Rotate = Rotation.on90;
```

解釋：
- 背景：將其設定為 `true` 表示印章將出現在 PDF 內容的後方。
- XIndent 和 YIndent：這些屬性決定了頁面上印章的位置。在此範例中，郵票將放置在距離頁面左邊緣和上緣 100 個單位的位置。
- 旋轉：將圖章旋轉 90 度。您可以根據您的設計要求選擇不同的旋轉選項。

## 步驟5：自訂文字屬性

接下來，讓我們發揮創意，自訂圖章內文本的外觀：

```csharp
// 設定文字屬性
textStamp.TextState.Font = FontRepository.FindFont("Arial");
textStamp.TextState.FontSize = 14.0F;
textStamp.TextState.FontStyle = FontStyles.Bold | FontStyles.Italic;
textStamp.TextState.ForegroundColor = Aspose.Pdf.Color.FromRgb(Color.Aqua);
```

解釋：
- 字體：我們使用 Arial 字體並將其設為粗體和斜體。
- FontSize：設定為14點。
- ForegroundColor：使用 RGB 將文字顏色設定為 Aqua。請隨意更改顏色以滿足您的品牌或設計需求！

## 步驟 6：在 PDF 頁面上新增圖章

現在是時候將印章添加到 PDF 文件的特定頁面了。

```csharp
// 將圖章加入特定頁面
pdfDocument.Pages[1].AddStamp(textStamp);
```

說明：在此範例中，印章被加入到 PDF 的第一頁（頁以 1 為索引）。根據文檔的需要調整頁碼。

## 步驟 7：儲存修改後的 PDF

最後，讓我們儲存帶有新新增的文字戳記的文檔。

```csharp
dataDir = dataDir + "AddTextStamp_out.pdf";

// 儲存輸出文檔
pdfDocument.Save(dataDir);
Console.WriteLine("\nText stamp added successfully.\nFile saved at " + dataDir);
```

解釋：我們為輸出檔案定義一個新路徑，然後儲存修改後的文件。儲存後，路徑會列印到控制台，確認操作成功。

## 結論

恭喜！您已成功使用 Aspose.PDF for .NET 將文字標記新增至 PDF 檔案。這種方法可以讓您有效地註釋您的文檔，從而提高其專業性和可用性。無論您添加浮水印、簽名還是簡單註釋，Aspose 庫都提供了強大的工具來輕鬆操作您的 PDF。

## 常見問題解答

### PDF 中的文字標記是什麼？
文字圖章是一種包含文字的圖形覆蓋，可以放置在 PDF 文件上，通常用於註釋或浮水印。

### 我可以用圖像客製郵票嗎？
是的，Aspose.PDF 也支援添加圖像印章，提供更多的設計彈性。

### 我可以與 Aspose.PDF 一起使用哪些程式語言？
Aspose.PDF 主要專注於 .NET，但也有 Java 和 Python 等其他語言的版本。

### 如何取得 Aspose.PDF 的臨時授權？
您可以透過訪問申請臨時駕照 [購買連結](https://purchase.aspose.com/temporary-license/) 在他們的網站上。

### 在哪裡可以找到對 Aspose.PDF 的支援？
Aspose.PDF 支持 [支援論壇](https://forum。aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}