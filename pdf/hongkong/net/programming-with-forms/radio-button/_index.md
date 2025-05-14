---
"description": "透過本逐步教學了解如何使用 Aspose.PDF for .NET 在 PDF 文件中建立互動式單選按鈕。"
"linktitle": "單選按鈕"
"second_title": "Aspose.PDF for .NET API參考"
"title": "單選按鈕"
"url": "/zh-hant/net/programming-with-forms/radio-button/"
"weight": 220
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 單選按鈕

## 介紹

建立互動式 PDF 可以顯著增強使用者體驗，尤其是在表單方面。最常見的互動元素之一是單選按鈕，它允許使用者從一組選項中選擇一個。在本教學中，我們將探討如何使用 Aspose.PDF for .NET 在 PDF 文件中建立單選按鈕。無論您是經驗豐富的開發人員還是剛入門，本指南都會逐步引導您完成整個過程，確保您了解程式碼的每個部分及其用途。

## 先決條件

在深入研究程式碼之前，您需要滿足一些先決條件：

1. Visual Studio：確保您的機器上安裝了 Visual Studio。這將是您的開發環境。
2. Aspose.PDF for .NET：您需要有 Aspose.PDF 函式庫。您可以從 [地點](https://releases。aspose.com/pdf/net/).
3. C# 基礎知識：熟悉 C# 程式設計將幫助您更好地理解程式碼片段。

## 導入包

首先，您需要在 C# 專案中匯入必要的套件。您可以按照以下步驟操作：

### 建立新專案

開啟 Visual Studio 並建立一個新的 C# 專案。為了簡單起見，您可以選擇控制台應用程式。

### 新增 Aspose.PDF 參考

1. 在解決方案資源管理器中以滑鼠右鍵按一下您的專案。
2. 選擇“管理 NuGet 套件”。
3. 搜尋“Aspose.PDF”並安裝最新版本。

現在您已完成所有設置，讓我們深入研究在 PDF 中建立單選按鈕的程式碼。

## 步驟 1：設定文檔目錄

首先，您需要指定儲存 PDF 的目錄。這對於組織您的文件至關重要。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

代替 `"YOUR DOCUMENT DIRECTORY"` 使用您想要儲存 PDF 檔案的實際路徑。

## 步驟2：實例化文檔對象

接下來，您需要建立一個 `Document` 班級。此類代表您的 PDF 文件。

```csharp
Document pdfDocument = new Document();
```

此行初始化您將要使用的新的 PDF 文件。

## 步驟 3：在 PDF 中新增頁面

每個 PDF 文件都由頁面組成。您需要在文件中新增至少一頁。

```csharp
pdfDocument.Pages.Add();
```

此行將新頁面新增至您的 PDF 文檔，使其準備好顯示內容。

## 步驟 4：建立單選按鈕字段

現在，是時候建立單選按鈕欄位了。您將實例化一個 `RadioButtonField` 物件並指定放置它的頁碼。

```csharp
RadioButtonField radio = new RadioButtonField(pdfDocument.Pages[1]);
```

在這裡，我們將單選按鈕新增到 PDF 的第一頁。

## 步驟 5：為單選按鈕新增選項

您可以為單選按鈕新增多個選項。每個選項都是一個可選項目。

```csharp
radio.AddOption("Test", new Rectangle(0, 0, 20, 20));
radio.AddOption("Test1", new Rectangle(20, 20, 40, 40));
```

在這個例子中，我們新增了兩個選項：「Test」和「Test1」。這 `Rectangle` 物件指定每個選項的位置和大小。

## 步驟 6：將單選按鈕新增至文件表單

一旦定義了單選按鈕及其選項，就需要將其新增至文件表單。

```csharp
pdfDocument.Form.Add(radio);
```

此行將單選按鈕整合到 PDF 表單中，使其具有互動性。

## 步驟 7：儲存 PDF 文檔

最後，您需要將 PDF 文件儲存到指定的目錄。

```csharp
dataDir = dataDir + "RadioButton_out.pdf";
pdfDocument.Save(dataDir);
```

此程式碼將文件以「RadioButton_out.pdf」的名稱儲存在您指定的目錄中。

## 步驟 8：處理異常

處理程式碼執行期間可能發生的異常始終是一個好的做法。

```csharp
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
}
```

這將捕獲任何錯誤並顯示訊息，幫助您在出現問題時進行偵錯。

## 結論

使用 Aspose.PDF for .NET 在 PDF 中建立單選按鈕是一個簡單的過程，可以大幅增強文件的互動性。透過遵循本教學中概述的步驟，您可以輕鬆地在 PDF 表單中實現單選按鈕，使其更加用戶友好且更具吸引力。請記住，熟能生巧，所以不要猶豫嘗試不同的選項和配置！

## 常見問題解答

### 什麼是 Aspose.PDF for .NET？
Aspose.PDF for .NET 是一個強大的程式庫，可讓開發人員以程式設計方式建立、操作和轉換 PDF 文件。

### 我可以免費使用 Aspose.PDF 嗎？
是的，Aspose 提供免費試用版，您可以使用它來探索該程式庫的功能。你可以下載 [這裡](https://releases。aspose.com/).

### 如何獲得 Aspose.PDF 的支援？
您可以透過訪問 [Aspose 論壇](https://forum。aspose.com/c/pdf/10).

### 是否可以使用 Aspose.PDF 建立其他表單欄位？
絕對地！ Aspose.PDF 支援各種表單字段，包括文字字段、複選框和下拉式選單。

### 哪裡可以購買 Aspose.PDF for .NET？
您可以購買 Aspose.PDF 的許可證 [這裡](https://purchase。aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}