---
"description": "了解如何使用 Aspose.PDF for .NET 在 PDF 檔案中設定到期日。透過本逐步指南增強文件安全性。"
"linktitle": "在 PDF 文件中設定到期日期"
"second_title": "Aspose.PDF for .NET API參考"
"title": "在 PDF 文件中設定到期日期"
"url": "/zh-hant/net/programming-with-document/setexpirydate/"
"weight": 300
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 文件中設定到期日期

## 介紹

在當今數位時代，管理和保護文件比以往任何時候都更加重要。想像發送一份 PDF 文件，該 PDF 在某個日期之後將自動變得無法存取。聽起來很神奇，對吧？好吧，使用 Aspose.PDF for .NET，您可以輕鬆地為您的 PDF 檔案設定到期日。此功能對於需要在一定時間後限制的敏感檔案特別有用。在本教學中，我們將逐步指導您完成在 PDF 檔案中設定到期日的過程。所以，戴上你的編碼帽，讓我們開始吧！

## 先決條件

在我們開始之前，您需要做好以下幾點：

1. 開發環境：確保您已設定 .NET 開發環境。這可以是 Visual Studio 或任何其他支援 .NET 的 IDE。
2. Aspose.PDF for .NET：您需要安裝 Aspose.PDF 庫。如果你還沒有這樣做，你可以從 [這裡](https://releases。aspose.com/pdf/net/).
3. C# 基礎知識：本教學假設您對 C# 程式設計有基本的了解。如果您是 C# 新手，請不要擔心！我們將保持其簡單和直接。

## 導入包

要開始使用 Aspose.PDF，您需要在 C# 專案中匯入必要的命名空間。你可以這樣做：

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
```

這些命名空間可讓您存取在 Aspose.PDF 中處理 PDF 文件所需的核心功能。

## 步驟 1：設定文檔目錄

首先，您需要指定文檔目錄的路徑。這是您的輸出 PDF 的儲存位置。 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

代替 `"YOUR DOCUMENT DIRECTORY"` 使用您想要儲存 PDF 檔案的實際路徑。這就像告訴你的程序，“嘿，這是我保存文件的地方！”

## 步驟2：實例化文檔對象

接下來，您需要建立一個新的實例 `Document` 班級。這是您建立 PDF 的畫布。

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

想想 `Document` 對象就像一張白紙。您可以隨意添加內容！

## 步驟 3：在 PDF 中新增頁面

現在您已經設定好了文檔，接下來就可以新增頁面了。這是您的內容將要存放的地方。

```csharp
doc.Pages.Add();
```

您剛剛在 PDF 中建立了一個新頁面。這就像在筆記本中添加一個新頁面，您可以在其中記下您的想法。

## 步驟 4：為頁面新增文本

讓我們透過添加一些文字使這個頁面變得更有趣一些。我們將添加一個簡單的「Hello World」訊息。

```csharp
doc.Pages[1].Paragraphs.Add(new TextFragment("Hello World..."));
```

這行程式碼將文字片段加入 PDF 的第一頁。這就像在頁面頂部寫一個標題！

## 步驟 5：建立到期日的 JavaScript

現在到了有趣的部分！您將建立一個 JavaScript 操作來檢查 PDF 的到期日。如果目前日期超過到期日期，則會顯示一則訊息提醒使用者。

```csharp
JavascriptAction javaScript = new JavascriptAction(
"var year=2017;"
+ "var month=5;"
+ "today = new Date(); today = new Date(today.getFullYear(), today.getMonth());"
+ "expiry = new Date(year, month);"
+ "if (today.getTime() > expiry.getTime())"
+ "app.alert('The file is expired. You need a new one.');");
```

以下是正在發生的事情：
- 您定義到期年份和月份。
- 您將獲得今天的日期。
- 您將今天的日期與到期日進行比較。
- 如果今天的日期已過有效期，則會彈出一則訊息！

## 步驟 6：將 JavaScript 設定為 PDF 開啟操作

現在，您需要將 JavaScript 操作設定為 PDF 文件的開啟操作。這意味著 JavaScript 將在 PDF 開啟後立即運行。

```csharp
doc.OpenAction = javaScript;
```

這一行告訴 PDF 在有人打開它時執行 JavaScript。這就像設定一個提醒，當您打開日曆時它就會響起！

## 步驟 7：儲存 PDF 文檔

最後，是時候使用到期日功能來儲存您的 PDF 文件了。 

```csharp
dataDir = dataDir + "SetExpiryDate_out.pdf";
doc.Save(dataDir);
```

此行將您的 PDF 儲存到指定目錄，名稱為「SetExpiryDate_out.pdf」。這就像將完成的藝術品放入框架中一樣！

## 結論

就是這樣！您已成功使用 Aspose.PDF for .NET 建立了具有到期日的 PDF 檔案。此功能不僅增強了安全性，而且還確保了敏感資訊的受控。無論您發送的是合約、報告或任何其他重要文件，設定到期日都可能產生重大影響。

## 常見問題解答

### 什麼是 Aspose.PDF for .NET？
Aspose.PDF for .NET 是一個強大的程式庫，可讓開發人員在 .NET 應用程式中建立、操作和轉換 PDF 文件。

### 我可以免費使用 Aspose.PDF 嗎？
是的，您可以使用 Aspose.PDF 的免費試用版。你可以下載 [這裡](https://releases。aspose.com/).

### 如何購買 Aspose.PDF？
您可以透過造訪購買 Aspose.PDF [購買頁面](https://purchase。aspose.com/buy).

### 如果我需要支援怎麼辦？
如果您有任何疑問或需要協助，您可以訪問 [Aspose 支援論壇](https://forum。aspose.com/c/pdf/10).

### 我可以取得 Aspose.PDF 的臨時授權嗎？
是的，您可以申請臨時駕照 [這裡](https://purchase。aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}