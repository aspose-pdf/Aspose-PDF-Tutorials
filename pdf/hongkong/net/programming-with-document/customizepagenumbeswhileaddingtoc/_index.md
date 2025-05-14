---
"description": "在本綜合教學中學習如何使用 Aspose.PDF for .NET 為 PDF 文件新增目錄並自訂頁碼。"
"linktitle": "新增目錄時自訂頁碼"
"second_title": "Aspose.PDF for .NET API參考"
"title": "新增目錄時自訂頁碼"
"url": "/zh-hant/net/programming-with-document/customizepagenumbeswhileaddingtoc/"
"weight": 100
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 新增目錄時自訂頁碼

## 介紹

在文件管理領域，PDF 佔據主導地位。它們是跨各種平台共享和保存文件的首選格式。但是，當您想要使用目錄 (TOC) 等功能來增強 PDF 文件時會發生什麼？這就是 Aspose.PDF for .NET 發揮作用的地方！這個強大的程式庫允許開發人員輕鬆地操作 PDF 文件，使他們能夠毫不費力地添加、修改和自訂內容。在本教學中，我們將深入研究如何使用 Aspose.PDF for .NET 在向 PDF 文件新增目錄的同時自訂頁碼。那麼，戴上你的編碼帽，讓我們開始吧！

## 先決條件

在我們進入程式碼之前，您需要做好以下幾件事：

1. Visual Studio：確保您的機器上安裝了 Visual Studio。這將是我們的開發環境。
2. Aspose.PDF for .NET：您需要下載並安裝 Aspose.PDF 庫。你可以找到它 [這裡](https://releases。aspose.com/pdf/net/).
3. C# 基礎知識：熟悉 C# 程式設計將幫助您更好地理解程式碼片段。
4. 範例 PDF 檔案：準備好我們可以使用的範例 PDF 檔案。您可以建立一個簡單的或下載一個現有的 PDF。

## 導入包

首先，我們需要導入必要的套件。開啟您的 Visual Studio 專案並新增對 Aspose.PDF 庫的參考。您可以使用 NuGet 套件管理器來執行此操作：

1. 在解決方案資源管理器中以滑鼠右鍵按一下您的專案。
2. 選擇“管理 NuGet 套件”。
3. 搜尋“Aspose.PDF”並安裝。

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

一旦安裝了庫，您就可以開始編碼！

## 步驟 1：設定文檔目錄

首先，我們需要設定我們的文件目錄。這是我們儲存輸入和輸出 PDF 檔案的地方。 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string inFile = dataDir + "42824.pdf";
string outFile = dataDir + "42824_out.pdf";
```

在此程式碼片段中，替換 `YOUR DOCUMENT DIRECTORY` 與您的 PDF 檔案所在的實際路徑。這將幫助我們載入現有的 PDF 並保存修改後的版本。

## 步驟2：載入現有PDF文件

現在我們已經設定了文檔目錄，讓我們載入現有的 PDF 文件。 

```csharp
Document doc = new Document(inFile);
```

在這裡，我們創建一個新的 `Document` 透過傳遞輸入檔路徑來獲取物件。這使我們能夠以程式設計方式操作 PDF 內容。

## 步驟 3：為目錄插入新頁面

接下來，我們需要在 PDF 中建立一個新頁面，用於存放目錄。

```csharp
Aspose.Pdf.Page tocPage = doc.Pages.Insert(1);
```

此行在文件開頭插入一個新頁面。目錄將顯示在此頁面。

## 步驟4：建立目錄訊息

現在，讓我們建立一個物件來表示目錄資訊。

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocInfo.PageNumbersPrefix = "P";
tocPage.TocInfo = tocInfo;
```

在此步驟中，我們建立一個 `TocInfo` 物件並將其標題設為“目錄”。我們也客製了字體大小和样式。這 `PageNumbersPrefix` 設定為“P”，它將作為目錄中頁碼的前綴。

## 步驟 5：將標題新增至目錄

現在到了有趣的部分！我們將循環瀏覽文件的各個頁面並將標題新增至目錄。

```csharp
for (int i = 1; i < doc.Pages.Count; i++)
{
    Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
    TextSegment segment2 = new TextSegment();
    heading2.TocPage = tocPage;
    heading2.Segments.Add(segment2);
    heading2.DestinationPage = doc.Pages[i + 1];
    heading2.Top = doc.Pages[i + 1].Rect.Height;
    segment2.Text = "Page " + i.ToString();
    tocPage.Paragraphs.Add(heading2);
}
```

在這個循環中，我們創造一個新的 `Heading` 每個頁面的物件。我們為每個標題設定目標頁面並指定要顯示的文本，即“第 X 頁”，其中 X 是頁碼。最後，我們將標題新增到目錄頁。

## 步驟6：儲存更新後的文檔

在新增所有必要的標題後，就可以儲存更新後的文件了。

```csharp
doc.Save(outFile);
```

此行保存了包含目錄的修改後的 PDF。現在您可以打開輸出檔案並查看自訂的目錄！

## 結論

就是這樣！您已成功使用 Aspose.PDF for .NET 為 PDF 文件新增目錄並自訂頁碼。這個強大的庫使得操作 PDF 文件變得容易，只需幾行程式碼，您就可以顯著增強您的文件。無論您建立的是報告、電子書或任何其他類型的 PDF，目錄都可以大大改善讀者的導航。那麼，您還在等什麼呢？深入了解 Aspose.PDF 並立即開始建立精彩的 PDF！

## 常見問題解答

### 什麼是 Aspose.PDF for .NET？
Aspose.PDF for .NET 是一個函式庫，可讓開發人員以程式設計方式建立、操作和轉換 PDF 文件。

### 我可以免費使用 Aspose.PDF 嗎？
是的，Aspose 提供免費試用版，您可以使用它來探索該程式庫的功能。你可以下載 [這裡](https://releases。aspose.com/).

### 如何獲得 Aspose.PDF 的支援？
您可以透過造訪 Aspose 論壇獲得支持 [這裡](https://forum。aspose.com/c/pdf/10).

### 有臨時執照嗎？
是的，您可以申請 Aspose.PDF 的臨時許可證。 [這裡](https://purchase。aspose.com/temporary-license/).

### 哪裡可以購買 Aspose.PDF for .NET？
您可以購買 Aspose.PDF for .NET [這裡](https://purchase。aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}