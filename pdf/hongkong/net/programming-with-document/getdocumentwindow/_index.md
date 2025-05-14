---
"description": "了解如何使用 Aspose.PDF for .NET 的 GetDocumentWindow 功能來擷取 PDF 文件視窗屬性的資訊。"
"linktitle": "取得文檔視窗"
"second_title": "Aspose.PDF for .NET API參考"
"title": "取得文檔視窗"
"url": "/zh-hant/net/programming-with-document/getdocumentwindow/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 取得文檔視窗

# 介紹

您是否正在使用 PDF 並希望更好地控制其開啟時的顯示方式？無論是隱藏功能表列或調整視窗大小以適合第一頁，Aspose.PDF for .NET 都為您提供了自訂 PDF 在檢視器中開啟時的行為所需的所有工具。在本教學中，我們將詳細介紹如何在 Aspose.PDF for .NET 中擷取和操作文件視窗設定。


# 先決條件

在深入學習本教程之前，請確保您已滿足以下先決條件：

- 在您的開發環境中安裝 Aspose.PDF for .NET。
  - [下載 Aspose.PDF for .NET](https://releases.aspose.com/pdf/net/)
- Aspose.PDF 的有效許可證，或者您可以獲得 [免費試用](https://releases.aspose.com/) 或者 [臨時執照](https://purchase。aspose.com/temporary-license/).
- 對 .NET 和 C# 有基本的了解。
- Visual Studio 或其他適合的 IDE。

# 導入包

在開始編寫任何程式碼之前，您需要匯入必要的套件。打開您的項目，然後在 C# 檔案的頂部添加以下命名空間：

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

這將使您能夠存取使用 Aspose.PDF for .NET 處理 PDF 文件所需的所有類別和方法。

現在讓我們分解檢索不同文件視窗設定的過程。在本例中，我們將使用名為 `GetDocumentWindow。pdf`.

## 步驟1：設定文檔目錄路徑

首先，我們需要定義 PDF 檔案的路徑。擁有正確的文件路徑至關重要，以避免執行期間出現任何錯誤。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

在這裡，替換 `"YOUR DOCUMENT DIRECTORY"` 與您的 PDF 檔案所在的實際目錄。這是您的工作目錄，您將從這裡載入 PDF 文件。

## 第 2 步：開啟 PDF 文檔

現在已經設定了檔案路徑，下一步是使用 Aspose.PDF 開啟 PDF 文件。這會將文件載入到記憶體中，允許您檢索其屬性。

```csharp
Document pdfDocument = new Document(dataDir + "GetDocumentWindow.pdf");
```

透過這行簡單的程式碼，您已成功將 PDF 檔案載入到 `pdfDocument` 對象，現在您可以存取其所有屬性。

## 步驟 3：檢索視窗居中狀態

接下來我們檢查一下文檔視窗開啟時是否應該居中。預設值為 `false`。

```csharp
Console.WriteLine("CenterWindow : {0}", pdfDocument.CenterWindow);
```

如果輸出是 `true`，文檔視窗將在螢幕中央開啟。否則，它將在其預設位置打開。

## 步驟 4：檢查文字方向

PDF 外觀的另一個重要方面是文字方向，它決定了文字是從左到右（L2R）閱讀還是從右到左（R2L）閱讀。您可以使用以下程式碼檢索此資訊：

```csharp
Console.WriteLine("Direction : {0}", pdfDocument.Direction);
```

輸出將是 `L2R` 對於從左到右的文字和 `R2L` 適用於從右到左的文字。此設定對於阿拉伯語或希伯來語等語言的文檔特別有用。

## 步驟5：在視窗中顯示文件標題

下一個屬性可讓您控制是否在視窗的標題列上顯示文件標題或檔案名稱。預設情況下，此設定為 `false`，表示將顯示檔案名稱。

```csharp
Console.WriteLine("DisplayDocTitle : {0}", pdfDocument.DisplayDocTitle);
```

如果您希望顯示文件的標題而不是文件名，則必須啟用此設定。

## 步驟 6：調整視窗大小以適合第一頁

有時，您可能希望文件視窗在開啟時自動調整大小以適合 PDF 的第一頁。檢查該功能是否啟用的方法如下：

```csharp
Console.WriteLine("FitWindow : {0}", pdfDocument.FitWindow);
```

預設情況下，此設定為 `false`，這意味著無論第一頁的大小如何，視窗大小都將保持原樣。

## 步驟 7：隱藏功能表列

為了獲得更專注的閱讀體驗，您可能需要隱藏檢視器應用程式的功能表列。您可以使用以下行檢索此設定：

```csharp
Console.WriteLine("HideMenuBar : {0}", pdfDocument.HideMenubar);
```

這將返回 `true` 如果功能表列被隱藏，並且 `false` 否則。

## 步驟 8：隱藏工具列

同樣，您可能還想隱藏 PDF 檢視器中的工具欄，以獲得更簡潔的使用者介面。可以如下擷取此設定：

```csharp
Console.WriteLine("HideToolBar : {0}", pdfDocument.HideToolBar);
```

如果啟用此設置，則開啟 PDF 時工具列將被隱藏。

## 步驟 9：隱藏捲軸和 UI 元素

如果您希望僅顯示頁面內容而不顯示任何其他 UI 元素（如捲軸），則此設定可以控制該行為：

```csharp
Console.WriteLine("HideWindowUI : {0}", pdfDocument.HideWindowUI);
```

當設定為 `true`，PDF 檢視器將隱藏捲軸和其他使用者介面元素，只留下文件內容。

## 步驟10：設定非全螢幕頁面模式

您可以使用 `NonFullScreenPageMode` 財產。此設定有助於定義使用者在非全螢幕模式下如何與文件互動。

```csharp
Console.WriteLine("NonFullScreenPageMode : {0}", pdfDocument.NonFullScreenPageMode);
```

輸出可以設定為不同的模式，如縮圖、輪廓或附件面板。

## 步驟 11：定義頁面佈局

此設定可讓您控製文件頁面的佈局方式。例如，您可以選擇單頁視圖或連續列視圖：

```csharp
Console.WriteLine("PageLayout : {0}", pdfDocument.PageLayout);
```

這使得使用者可以靈活地閱讀或查看文件內容。

## 步驟 12：指定頁面模式

最後， `PageMode` 屬性定義文件開啟時應如何顯示。選項包括顯示縮圖、進入全螢幕模式或顯示附件面板。

```csharp
Console.WriteLine("PageMode : {0}", pdfDocument.PageMode);
```

根據您的需要，您可以將其設定為適合您的 PDF 用途的任何模式。

## 結論

如您所見，Aspose.PDF for .NET 提供了一個全面的工具來控制 PDF 文件在各種 PDF 檢視器中的顯示方式。無論您想隱藏工具列、讓視窗居中或控製文字方向，Aspose.PDF 都能靈活地增強使用者的觀看體驗。

# 常見問題解答

### 我可以自訂 PDF 的初始縮放等級嗎？
是的，Aspose.PDF 允許您在開啟文件時設定縮放等級。

### 如何鎖定 PDF 的視窗大小？
您可以設定 `FitWindow` 屬性以防止視窗調整大小。

### Aspose.PDF 是否支援不同的閱讀模式？
是的，它支援全螢幕、縮圖和配件等不同模式。

### 是否可以隱藏 PDF 檢視器中的捲軸？
當然，你可以透過設定 `HideWindowUI` 財產 `true`。

### 開啟文件視窗時可以將其置於中心嗎？
是的，您可以透過設定來控制 `CenterWindow` 財產。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}