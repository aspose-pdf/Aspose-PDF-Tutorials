---
"description": "釋放 Aspose.PDF for .NET 的強大功能。透過我們的逐步指南了解如何在表單欄位上設定 JavaScript。"
"linktitle": "設定 Java 腳本"
"second_title": "Aspose.PDF for .NET API參考"
"title": "設定 Java 腳本"
"url": "/zh-hant/net/programming-with-forms/set-java-script/"
"weight": 270
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 設定 Java 腳本

## 介紹

建立動態和互動式 PDF 可以顯著增強使用者體驗，尤其是在文件中整合表單和欄位時。實現這一目標的一個強大的程式庫是 Aspose.PDF for .NET。在本文中，我們將深入研究使用 Aspose.PDF 為表單欄位設定 JavaScript，確保您的 PDF 不僅外觀美觀，而且功能強大。

## 先決條件

在我們開始編碼之前，讓我們確保您擁有順利進行所需的一切：

- Visual Studio（或任何 .NET IDE）：確保已正確安裝和設定。
  
- Aspose.PDF 函式庫：您會需要這個函式庫的最新版本。你可以下載 [這裡](https://releases。aspose.com/pdf/net/).

- C# 基礎知識：熟悉 C# 程式設計將幫助您更好地理解程式碼片段。

- PDF 檔案：您應該準備好一個可供測試的 PDF 檔案。在我們的範例中，我們將使用名為 `SetJavaScript。pdf`.

- 您的文件目錄：了解您的文件檔案的儲存位置。我們將在程式碼中引用此路徑。

一旦準備好這些先決條件，我們將利用哪些工具？讓我們來探索一下 Aspose.PDF 可以做些什麼。

## 導入包

首先，您需要在 C# 專案中包含必要的命名空間。開啟主 C# 檔案並新增以下導入語句：

```csharp
using System;
using System.IO;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
```

這些命名空間提供對 Aspose.PDF 庫中的 PDF 和表單相關功能的存取。

準備好讓您的 PDF 具有互動性了嗎？拿起你的編碼帽，讓我們一步一步地分解它！

## 步驟 1：定義文檔路徑

首先，我們需要指定 PDF 檔案的位置。這為接下來的一切奠定了基礎。以下是操作方法：

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

代替 `"YOUR DOCUMENT DIRECTORY"` 與您的 PDF 檔案所在的實際路徑。將其想像為設定藏寶圖的座標 - 您需要知道「X」標記的位置！

## 第 2 步：載入 PDF 文檔

一旦我們定義了目錄，我們就會載入我們的 PDF 檔案。 

```csharp
Document doc = new Document(dataDir + "SetJavaScript.pdf");
```

此行打開您指定的 PDF 文件並準備對其進行操作。 

## 步驟 3：存取表單字段

接下來，我們要存取將套用 JavaScript 的表單欄位。 

```csharp
TextBoxField field = (TextBoxField)doc.Form["textbox1"];
```

這裡，我們假設你的 PDF 中有一個名為 `textbox1`。如果您沒有具有此名稱的字段，您可以重新命名它或相應地調整代碼。 

## 步驟 4：設定 JavaScript 操作

現在，讓我們為文字方塊添加一些功能！我們將設定在某些事件上觸發的 JavaScript 操作。 

```csharp
field.Actions.OnModifyCharacter = new JavascriptAction("AFNumber_Keystroke(2, 1, 1, 0, \"\", true)");
field.Actions.OnFormat = new JavascriptAction("AFNumber_Format(2, 1, 1, 0, \"\", true)");
```

以下是正在發生的事情：
- OnModifyCharacter：此 JavaScript 函數指定當字元被修改時欄位應如何表現。在這種情況下，允許數字後面有兩個小數點，且沒有分隔符號。
- OnFormat：這確保當使用者格式化數字時，它遵循相同的規則。

透過設定這些動作，我們本質上賦予了文字框個性——就像教它舞蹈動作一樣！

## 步驟5：初始化欄位值

接下來，讓我們透過設定初始值來為文字方塊提供一個起點。 

```csharp
field.Value = "123";
```

此行將「123」設定為文字方塊中的預填值。這就像為表演準備舞台一樣。

## 步驟6：儲存修改後的PDF

最後，完成所有這些變更後，我們需要儲存文件。

```csharp
dataDir = dataDir + "Restricted_out.pdf";
doc.Save(dataDir);
```

這將使用您的變更更新原始檔案並將其儲存為 `Restricted_out.pdf`。將此視為決定我們 PDF 的命運 - 一旦保存，它就可以面向世界了！

## 步驟7：確認成功

最後，讓我們檢查一下一切是否順利。 

```csharp
Console.WriteLine("\nJavaScript on form field setup successfully.\nFile saved at " + dataDir);
```

運行此訊息將向您保證操作已成功完成，就像在精彩的表演後收到觀眾的掌聲一樣。

## 結論

恭喜！您已成功使用 Aspose.PDF for .NET 為 PDF 中的表單欄位設定 JavaScript。本教學不僅為您提供了增強使用者互動的工具，還使您能夠像專業人士一樣個性化您的文件。無論您處理的是發票、調查或其他互動式 PDF 中的表格，可能性都是無窮無盡的。

### 常見問題解答

### 什麼是 Aspose.PDF for .NET？  
Aspose.PDF 是一個用於在 .NET 應用程式中建立、編輯和操作 PDF 檔案的程式庫，提供強大的 PDF 功能。

### 我需要許可證才能使用 Aspose.PDF 嗎？  
雖然可以免費試用，但需要許可證才能不受限制地全面使用。您可以購買許可證 [這裡](https://purchase。aspose.com/buy).

### 我可以在其他類型的表單欄位上設定 JavaScript 嗎？  
絕對地！ Aspose.PDF 允許對各種表單欄位（例如複選框、單選按鈕和下拉式選單）執行 JavaScript 操作。

### 我如何獲得 Aspose.PDF 問題的支援？  
您可以透過他們的 [論壇](https://forum.aspose.com/c/pdf/10) 如有任何疑問或問題。

### 有沒有辦法在不購買的情況下測試 Aspose.PDF？  
是的！ Aspose 提供 [免費試用](https://releases.aspose.com/) 在購買之前測試圖書館的功能。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}