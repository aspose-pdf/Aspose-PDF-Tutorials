---
"description": "透過本逐步教學學習如何使用 Aspose.PDF for .NET 在 PDF 中建立水平和垂直對齊的單選按鈕。"
"linktitle": "水平和垂直單選按鈕"
"second_title": "Aspose.PDF for .NET API參考"
"title": "水平和垂直單選按鈕"
"url": "/zh-hant/net/programming-with-forms/horizontally-and-vertically-radio-buttons/"
"weight": 180
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 水平和垂直單選按鈕

## 介紹

建立互動式 PDF 表單可以顯著增強使用者體驗，尤其是在收集資訊時。最常見的表單元素之一是單選按鈕，它允許使用者從一組選項中選擇一個。在本教學中，我們將探討如何使用 Aspose.PDF for .NET 建立水平和垂直對齊的單選按鈕。無論您是經驗豐富的開發人員還是剛起步，本指南都會逐步引導您完成整個過程，確保您清楚地了解每個部分。

## 先決條件

在深入研究程式碼之前，您應該滿足一些先決條件：

1. Aspose.PDF for .NET：請確定您已安裝 Aspose.PDF 庫。您可以從 [地點](https://releases。aspose.com/pdf/net/).
2. Visual Studio：一個可以編寫和測試程式碼的開發環境。
3. C# 基礎知識：熟悉 C# 程式設計將幫助您更好地理解程式碼片段。

## 導入包

首先，您需要在 C# 專案中匯入必要的套件。您可以按照以下步驟操作：

### 建立新專案

開啟 Visual Studio 並建立一個新的 C# 專案。為了簡單起見，您可以選擇控制台應用程式。

### 新增 Aspose.PDF 參考

1. 在解決方案資源管理器中以滑鼠右鍵按一下您的專案。
2. 選擇“管理 NuGet 套件”。
3. 搜尋“Aspose.PDF”並安裝最新版本。

```csharp
using System;
using System.IO;
using Aspose.Pdf.Facades;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
```

現在您已完成所有設置，讓我們分解程式碼以建立水平和垂直對齊的單選按鈕。

## 步驟 1：設定文檔目錄

在此步驟中，我們將定義儲存 PDF 文件的目錄的路徑。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

代替 `"YOUR DOCUMENT DIRECTORY"` 使用您想要儲存 PDF 檔案的實際路徑。這很關鍵，因為它告訴程式在哪裡尋找輸入檔案以及在哪裡保存輸出。

## 步驟2：載入現有PDF文檔

接下來，我們需要載入我們將要處理的 PDF 文件。這是使用 `FormEditor` 班級。

```csharp
FormEditor formEditor = new FormEditor();
formEditor.BindPdf(dataDir + "input.pdf");
```

在這裡，我們建立一個實例 `FormEditor` 並將其綁定到名為 `input.pdf`。確保該檔案存在於您指定的目錄中。

## 步驟 3：配置單選按鈕屬性

現在，讓我們為單選按鈕設定一些屬性。這包括按鈕之間的間隙、按鈕的方向和按鈕的大小。

```csharp
formEditor.RadioGap = 4; // 單選按鈕選項之間的距離
formEditor.RadioHoriz = true; // 設定為 true 以進行水平對齊
formEditor.RadioButtonItemSize = 20; // 單選按鈕的大小
formEditor.Facade.BorderWidth = 1; // 邊框寬度
formEditor.Facade.BorderColor = System.Drawing.Color.Black; // 邊框顏色
```

這些屬性將有助於定義單選按鈕在 PDF 中的顯示方式。這 `RadioGap` 屬性控制按鈕之間的空間，而 `RadioHoriz` 決定了它們的佈局。

## 步驟 4：新增水平單選按鈕

現在，讓我們將水平單選按鈕新增至 PDF。

```csharp
formEditor.Items = new string[] { "First", "Second", "Third" };
formEditor.AddField(FieldType.Radio, "NewField1", 1, 40, 600, 120, 620);
```

在此程式碼中，我們定義單選按鈕的項目並將其新增至 PDF。這 `AddField` 方法採用幾個參數，包括欄位類型、欄位名稱和放置座標。

## 步驟 5：新增垂直單選按鈕

接下來，我們將新增垂直單選按鈕。為此，我們需要將方向改回垂直。

```csharp
formEditor.RadioHoriz = false; // 設定為 false 以進行垂直對齊
formEditor.Items = new string[] { "First", "Second", "Third" };
formEditor.AddField(FieldType.Radio, "NewField2", 1, 40, 500, 60, 550);
```

就像以前一樣，我們定義項目並將它們添加到 PDF，但這次它們將垂直對齊。

## 步驟6：儲存PDF文檔

最後，我們需要儲存修改後的PDF文件。

```csharp
dataDir = dataDir + "HorizontallyAndVerticallyRadioButtons_out.pdf";
formEditor.Save(dataDir);
Console.WriteLine("\nHorizontally and vertically laid out radio buttons successfully.\nFile saved at " + dataDir);
```

此程式碼保存了帶有新新增的單選按鈕的 PDF。確保檢查指定目錄中的輸出檔案。

## 結論

使用 Aspose.PDF for .NET 在 PDF 中建立單選按鈕是一個簡單的過程。按照本教學中概述的步驟，您可以輕鬆地將水平和垂直對齊的單選按鈕新增至 PDF 表單中。這不僅增強了文件的互動性，而且還改善了整體使用者體驗。所以，繼續嘗試吧！

## 常見問題解答

### 什麼是 Aspose.PDF for .NET？
Aspose.PDF for .NET 是一個強大的程式庫，可讓開發人員以程式設計方式建立、操作和轉換 PDF 文件。

### 我可以免費使用 Aspose.PDF 嗎？
是的，Aspose 提供免費試用版，您可以使用它來評估該程式庫。你可以下載 [這裡](https://releases。aspose.com/).

### 如何獲得 Aspose.PDF 的支援？
您可以透過訪問 [Aspose 論壇](https://forum。aspose.com/c/pdf/10).

### 是否可以使用 Aspose.PDF 建立其他表單元素？
絕對地！ Aspose.PDF 支援各種表單元素，包括文字欄位、複選框和下拉式選單。

### 我可以在哪裡購買 Aspose.PDF for .NET？
您可以從 [購買頁面](https://purchase。aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}