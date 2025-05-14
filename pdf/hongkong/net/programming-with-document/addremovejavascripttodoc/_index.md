---
"description": "了解如何使用 Aspose.PDF for .NET 為 PDF 文件新增和刪除 JavaScript。帶有文檔級腳本代碼教程的逐步指南。"
"linktitle": "新增刪除 Javascript 到文檔"
"second_title": "Aspose.PDF for .NET API參考"
"title": "在 PDF 文件中新增刪除 Javascript"
"url": "/zh-hant/net/programming-with-document/addremovejavascripttodoc/"
"weight": 30
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 文件中新增刪除 Javascript

## 介紹

在本指南中，我們將介紹如何使用 Aspose.PDF for .NET 將 JavaScript 插入 PDF 檔案以及如何在必要時將其刪除。在本教程結束時，您將清楚地了解如何輕鬆地操作 PDF 中的 JavaScript。

## 先決條件

在深入研究程式碼之前，您需要設定一些東西：

1. Aspose.PDF for .NET：您需要在專案中安裝 Aspose.PDF for .NET 程式庫。如果你還沒有，可以從 [Aspose.PDF for .NET下載頁面](https://releases。aspose.com/pdf/net/).
2. IDE 或文字編輯器：您可以使用任何與 .NET 相容的 IDE，例如 Visual Studio。
3. 基本 C# 知識：本教學假設您熟悉 C# 並熟悉 PDF 操作。
4. 許可證：確保應用有效的許可證以避免限制。您可以從 [這裡](https://purchase。aspose.com/temporary-license/).

## 導入包

要開始使用 Aspose.PDF for .NET，您需要將必要的命名空間匯入到您的專案中。方法如下：

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
using System.Collections;
```

這兩個命名空間至關重要。 `Aspose.Pdf` 允許您處理 PDF 文檔，同時 `System.Collections` 將用於處理 JavaScript 鍵。

讓我們將 PDF 中新增和刪除 JavaScript 的整個過程分解為易於遵循的步驟。

## 步驟 1：初始化新的 PDF 文檔

您需要做的第一件事是建立一個新的 PDF 文件。該文件將作為我們添加 JavaScript 的空白畫布。

```csharp
Document doc = new Document();
doc.Pages.Add();
```

在這裡，我們正在初始化一個新的 `Document` 物件並向其中添加空白頁。將其視為 PDF 的基礎。

## 步驟 2：將 JavaScript 新增到 PDF

現在我們有了一個文檔，是時候在其中添加一些 JavaScript 了。 PDF 中的 JavaScript 可用於新增自訂行為，例如警報或表單驗證。

```csharp
doc.JavaScript["func1"] = "function func1() { hello(); }";
doc.JavaScript["func2"] = "function func2() { hello(); }";
```

在此程式碼片段中，我們新增了兩個 JavaScript 函數（`func1` 和 `func2`到 PDF。根據您的需要，這些功能可以執行各種任務。這裡我們只是呼叫了一個名為 `hello()`。

## 步驟 3：使用 JavaScript 儲存 PDF

新增所需的 JavaScript 後，就可以儲存 PDF 了。

```csharp
doc.Save(dataDir + "AddJavascript.pdf");
```

這將使用 JavaScript 將文件保存在以下名稱下 `AddJavascript.pdf` 在指定目錄中（`dataDir`）。

## 步驟 4：在現有 PDF 中載入並檢視 JavaScript

假設您需要檢查或修改現有 PDF 中的 JavaScript 函數。第一步是載入 PDF 檔案並存取 JavaScript 鍵。

```csharp
Document doc1 = new Document(dataDir + "AddJavascript.pdf");
IList keys = (System.Collections.IList)doc1.JavaScript.Keys;
```

我們正在加載現有的 `AddJavascript.pdf` 並將 JavaScript 鍵儲存在清單中。這 `Keys` 屬性傳回附加到文件的所有 JavaScript 函數的名稱。

## 步驟 5：顯示 JavaScript 函數

接下來，我們可以遍歷 JavaScript 函數來查看文件中可用的內容。

```csharp
Console.WriteLine("=============================== ");
foreach (string key in keys)
{
    Console.WriteLine(key + " ==> " + doc1.JavaScript[key]);
}
```

這會將每個 JavaScript 函數名稱及其對應的程式碼列印到控制台。如果您想驗證文件中目前有哪些功能，它很有用。

## 步驟 6：從 PDF 刪除 JavaScript

現在，假設你想要刪除一個特定的 JavaScript 函數，例如 `func1`。您可以按照以下步驟操作：

```csharp
doc1.JavaScript.Remove("func1");
Console.WriteLine("Key 'func1' removed ");
```

這 `Remove` 方法將 JavaScript 函數的名稱作為參數並將其從文件中刪除。

## 步驟 7：驗證 JavaScript 刪除

刪除 JavaScript 後，您可以重新列印剩餘的函數來確認 `func1` 已成功刪除。

```csharp
Console.WriteLine("=============================== ");
foreach (string key in keys)
{
    Console.WriteLine(key + " ==> " + doc1.JavaScript[key]);
}
Console.WriteLine("Javascript added/removed successfully.");
```

程式碼的最後一部分確保一切就緒並且 JavaScript 函數得到正確更新。

## 結論

恭喜！您剛剛學習如何使用 Aspose.PDF for .NET 在 PDF 文件中新增和刪除 JavaScript。此強大功能可用於各種任務，從新增動態訊息到執行自訂計算或驗證。透過在 PDF 中操作 JavaScript，您可以顯著增強使用者體驗。

## 常見問題解答

### 我可以為單一 PDF 新增多個 JavaScript 函數嗎？
絕對地！您可以根據需要使用以下方式新增任意數量的 JavaScript 函數 `doc.JavaScript` 收藏。

### 如果我嘗試刪除不存在的 JavaScript 函數會發生什麼？
如果該函數不存在，則 `Remove` 方法不會引發錯誤，但也不會刪除任何內容。

### PDF 開啟後是否可以立即執行 JavaScript？
是的！您可以設定 JavaScript 在某些觸發器上執行，例如開啟文件或按一下按鈕。

### 將 JavaScript 添加到 PDF 後我可以編輯它嗎？
是的，您可以載入現有的 PDF，存取其 JavaScript，修改程式碼，然後再次儲存文件。

### 刪除 JavaScript 是否會影響 PDF 的其餘內容？
不，刪除 JavaScript 只會影響腳本。 PDF 的內容保持不變。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}