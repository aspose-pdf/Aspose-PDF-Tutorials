---
"description": "了解如何使用 Aspose.PDF for .NET 將 JavaScript 新增至 PDF 檔案。包含文件和頁面層級腳本程式碼教學的逐步指南。"
"linktitle": "新增 Java 腳本 PDF 文件"
"second_title": "Aspose.PDF for .NET API參考"
"title": "將 Java 腳本新增至 PDF 文件"
"url": "/zh-hant/net/programming-with-document/addjavascripttopage/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 將 Java 腳本新增至 PDF 文件

## 介紹

您是否想過如何使用彈出警報或自動列印功能等互動元素來增強您的 PDF？嗯，好消息——你可以！透過使用 Aspose.PDF for .NET，您可以將 JavaScript 無縫地新增到您的 PDF 文件中。無論您是自動執行任務還是建立動態使用者體驗，在 PDF 中嵌入 JavaScript 都會為您的文件提供額外的功能。

## 先決條件

在進入編碼部分之前，您需要設定一些東西：

- Aspose.PDF for .NET：從下列位置下載資料庫 [Aspose 版本](https://releases.aspose.com/pdf/net/) 或得到 [免費試用](https://releases。aspose.com/).
- 開發環境：任何與 .NET 相容的 IDE，如 Visual Studio。
- 基本 C# 知識：本指南假設您熟悉基本 C# 文法。
- 臨時許可證（可選）：您可以獲得 [臨時執照](https://purchase.aspose.com/temporary-license/) 如果您想避免開發過程中的限制。

## 導入包

在開始編寫程式碼之前，您需要從 Aspose.PDF 庫中匯入必要的命名空間。這些命名空間將允許您輕鬆操作 PDF 和新增 JavaScript 操作。

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
```

現在您已經匯入了正確的命名空間，可以開始編碼了。

## 步驟 1：載入現有 PDF

首先，您需要載入要新增 JavaScript 的 PDF 文件。此步驟為所有進一步的修改奠定了基礎。假設您有一個 PDF，您想透過動態功能來增強它，例如在開啟時自動列印文件。

載入該 PDF 檔案的方法如下：

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";

// 載入現有的 PDF 文件
Document doc = new Document(dataDir + "input.pdf");
```

在此程式碼片段中，我們使用 `Document` 類別從指定目錄載入現有的 PDF 檔案。確保更換 `"YOUR DOCUMENT DIRECTORY"` 使用您的 PDF 檔案的實際路徑。

## 步驟 2：在文件層級新增 JavaScript

現在，讓我們加入一些在文件開啟時觸發的 JavaScript。在這個例子中，我們將編寫一個腳本，當使用者開啟 PDF 時立即開啟列印對話方塊。

文件級 JavaScript 非常適合您想要套用於整個 PDF 的操作。可以將其想像為您的文件設定全域規則。

程式碼如下：

```csharp
// 在文件層級新增 JavaScript
// 使用所需的 JavaScript 語句實例化 JavascriptAction
JavascriptAction javaScript = new JavascriptAction("this.print({bUI:true,bSilent:false,bShrinkToFit:true});");

// 將 JavascriptAction 物件指派給 Document 的 OpenAction
doc.OpenAction = javaScript;
```

在此步驟中，我們建立一個 `JavascriptAction` 定義 JavaScript 函數的對象，用於在開啟文件時開啟列印對話方塊。這 `doc.OpenAction` 然後將屬性指派給此 JavaScript 操作。

## 步驟 3：在頁面層級新增 JavaScript

並非每個操作都需要影響整個文件。有時，您希望在開啟或關閉某些頁面時發生特定的動作。在這裡，我們將設定開啟和關閉特定頁面（假設是第 2 頁）時的 JavaScript 操作。

頁面層級 JavaScript 對於有針對性的互動很有用。它可以是任何內容，從使用者導航到頁面時顯示訊息，到自動填入表單欄位等自訂操作。

具體操作如下：

```csharp
// 在頁面層級新增 JavaScript
doc.Pages[2].Actions.OnOpen = new JavascriptAction("app.alert('Page 2 opened')");
doc.Pages[2].Actions.OnClose = new JavascriptAction("app.alert('Page 2 closed')");
```

在此程式碼片段中，我們新增了兩個 JavaScript 操作：
1. OnOpen 操作：當使用者開啟第 2 頁時顯示一則警告「第 2 頁已開啟」。
2. OnClose 操作：當使用者離開第 2 頁時顯示警告，提示「第 2 頁已關閉」。

這為您的 PDF 增加了一層互動性。想像引導使用者完成不同頁面上的一系列步驟，並在他們進入或離開頁面時彈出警報。

## 步驟 4：儲存 PDF 文檔

現在您已將 JavaScript 新增至文件和特定頁面。最後一步是將修改後的 PDF 儲存到您想要的位置。這部分很簡單但至關重要——不要忘記保存您的工作！

程式碼如下：

```csharp
// 指定輸出檔案路徑
dataDir = dataDir + "JavaScript-Added_out.pdf";

// 儲存更新的 PDF 文檔
doc.Save(dataDir);

Console.WriteLine("\nJavaScript added successfully to the PDF.\nFile saved at " + dataDir);
```

在此程式碼片段中，我們將更新後的文件和新增的 JavaScript 儲存到名為 `"JavaScript-Added_out.pdf"`。這可確保您不會覆蓋原始文件，並為您提供可用的備份。

## 結論

使用 Aspose.PDF for .NET 將 JavaScript 新增至 PDF 檔案是建立互動式動態 PDF 的有效方法。無論您是自動執行列印或建立自訂警報等任務，將 JavaScript 嵌入到 PDF 中的能力都會使您的文件更具吸引力和功能性。

## 常見問題解答

### 我可以為 PDF 中的不同頁面新增多個 JavaScript 操作嗎？
是的，您可以為單一頁面或整個文件指派不同的 JavaScript 操作。

### 添加 JavaScript 後是否可以從 PDF 中刪除它？
是的，您可以透過清除 `Actions` 文檔或頁面的屬性。

### 我可以在 PDF 中使用哪些類型的 JavaScript 函數？
您可以使用 Adobe Acrobat 的 JavaScript 引擎支援的任何 JavaScript，例如列印、警報和表單操作。

### JavaScript 是否適用於所有 PDF 檢視器？
大多數 JavaScript 操作將在支援互動式 PDF 的 PDF 檢視器（如 Adobe Acrobat）中執行。但是，一些基本的 PDF 閱讀器可能不支援 JavaScript。

### 我可以根據 PDF 中的使用者輸入觸發 JavaScript 操作嗎？
是的，您可以將 JavaScript 綁定到表單欄位以根據使用者輸入觸發操作。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}