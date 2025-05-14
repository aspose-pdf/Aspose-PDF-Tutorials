---
"description": "透過本詳細的逐步教學了解如何使用 Aspose.PDF for .NET 將網頁轉換為 PDF。"
"linktitle": "網頁轉 PDF"
"second_title": "Aspose.PDF for .NET API參考"
"title": "網頁轉 PDF"
"url": "/zh-hant/net/document-conversion/web-page-to-pdf/"
"weight": 320
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 網頁轉 PDF

## 介紹

在當今數位時代，將網頁轉換為 PDF 文件的能力非常有價值。無論您是想保存文章以供離線閱讀、建立報告還是存檔來自網路的內容，擁有合適的工具都會帶來很大的不同。其中一個工具是 Aspose.PDF for .NET，它是一個功能強大的程式庫，允許開發人員無縫地建立和操作 PDF 文件。在本指南中，我們將引導您完成使用 Aspose.PDF for .NET 將網頁轉換為 PDF 的過程，並將其分解為易於管理的步驟。

## 先決條件

在深入研究程式碼之前，請確保您擁有開始所需的一切：

1. Visual Studio：確保您的機器上安裝了 Visual Studio。您可以在此處編寫和執行 .NET 程式碼。
2. Aspose.PDF for .NET：您需要 Aspose.PDF 函式庫。您可以從下載 [這裡](https://releases。aspose.com/pdf/net/).
3. C# 基礎知識：熟悉 C# 程式設計將幫助您更好地理解範例。
4. 網路存取：由於我們將從網頁取得內容，請確保您的開發環境可以存取網路。

## 導入包

首先，您需要在 C# 專案中匯入必要的套件。方法如下：

### 建立新專案

首先，開啟 Visual Studio 並建立一個新的 C# 控制台應用程式專案。 

### 新增 Aspose.PDF 參考

接下來，新增對 Aspose.PDF 庫的引用。您可以透過 NuGet 套件管理器執行此操作：

1. 在解決方案資源管理器中以滑鼠右鍵按一下您的專案。
2. 選擇“管理 NuGet 套件”。
3. 搜尋“Aspose.PDF”並點選“安裝”。

### 導入所需的命名空間

添加庫後，打開 `Program.cs` 文件並在文件頂部導入必要的命名空間：

```csharp
using System.IO;
using System;
using System.Net;
using Aspose.Pdf;
```

現在我們已經完成所有設置，讓我們逐步分解將網頁轉換為 PDF 文件的過程。

## 步驟1：定義文檔目錄

首先，您需要定義輸出 PDF 的儲存位置。這是透過指定文檔目錄的路徑來完成的。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // 替換為您的路徑
```

## 步驟 2：建立 Web 請求

接下來，您需要建立一個請求來從要轉換的網頁中取得內容。以下是操作方法：

```csharp
WebRequest request = WebRequest.Create("https://參見 wikipedia.org/wiki/Main_Page”);
request.Credentials = CredentialCache.DefaultCredentials;
```

在這段程式碼中，我們正在創建對維基百科主頁的請求。您可以用您選擇的任何網頁替換該 URL。

## 步驟 3：取得響應

一旦設定了請求，就可以從伺服器取得回應了。這涉及發送請求和讀取回應流：

```csharp
HttpWebResponse response = (HttpWebResponse)request.GetResponse();
Stream dataStream = response.GetResponseStream();
StreamReader reader = new StreamReader(dataStream);
string responseFromServer = reader.ReadToEnd();
reader.Close();
dataStream.Close();
response.Close();
```

這裡，我們將伺服器傳回的全部內容讀入一個字串變數中。這是我們將轉換為 PDF 的內容。

## 步驟4：將HTML內容載入到記憶體中

現在我們有了 HTML 內容，我們需要將其載入到 `MemoryStream` 以便我們可以用 Aspose.PDF 來處理它：

```csharp
MemoryStream stream = new MemoryStream(System.Text.Encoding.UTF8.GetBytes(responseFromServer));
HtmlLoadOptions options = new HtmlLoadOptions("https://en.wikipedia.org/wiki/”);
```

在此步驟中，我們將字串回應轉換為位元組數組並將其載入到 `MemoryStream`。這 `HtmlLoadOptions` 允許我們為 HTML 中的任何相對連結指定基本 URL。

## 步驟5：建立PDF文檔

載入 HTML 內容後，我們現在可以從中建立 PDF 文件：

```csharp
Document pdfDocument = new Document(stream, options);
```

這行程式碼初始化了一個新的 `Document` 對象，代表我們要建立的 PDF。

## 步驟 6：設定頁面方向

如果您想要自訂 PDF 的佈局，例如將其設定為橫向模式，則可以使用以下程式碼來實現：

```csharp
options.PageInfo.IsLandscape = true;
```

這是可選的，但根據您要轉換的內容可能會很有用。

## 步驟 7：儲存 PDF

最後，將 PDF 文件儲存到指定目錄：

```csharp
pdfDocument.Save(dataDir + "WebPageToPDF_out.pdf");
```

此行將 PDF 儲存為以下名稱 `WebPageToPDF_out.pdf` 在您指定的文檔目錄中。

## 步驟 8：處理異常

處理過程中可能發生的異常始終是一種很好的做法。您可以將程式碼包裝在 try-catch 區塊中：

```csharp
try
{
    // 之前的所有程式碼都在這裡
}
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
}
```

這樣，如果出現問題，您將收到一條訊息，指示發生了什麼。

## 結論

就是這樣！您已成功使用 Aspose.PDF for .NET 將網頁轉換為 PDF。只需幾行程式碼，您就可以自動儲存 Web 內容以供日後使用。對於希望建立報告、檔案或僅保存文章以供離線閱讀的開發人員來說，這非常有用。 

## 常見問題解答

### 什麼是 Aspose.PDF for .NET？
Aspose.PDF for .NET 是一個函式庫，可讓開發人員以程式設計方式建立、操作和轉換 PDF 文件。

### 我可以將任何網頁轉換為 PDF 嗎？
是的，只要網頁是公開存取的，您就可以使用 Aspose.PDF 將其轉換為 PDF。

### 有免費試用嗎？
是的，您可以從以下網址下載 Aspose.PDF for .NET 的免費試用版 [這裡](https://releases。aspose.com/).

### 我可以在哪裡獲得 Aspose.PDF 的支援？
您可以從 Aspose 社區獲得支持 [支援論壇](https://forum。aspose.com/c/pdf/10).

### 我如何取得臨時執照？
您可以在 [Aspose 網站](https://purchase。aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}