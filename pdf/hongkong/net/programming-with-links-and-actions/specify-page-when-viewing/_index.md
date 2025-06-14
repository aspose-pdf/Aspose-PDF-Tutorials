---
"description": "了解如何使用 Aspose.PDF for .NET 指定在 PDF 中要查看的頁面。透過這個簡單的指南增強使用者導航。"
"linktitle": "查看時指定頁面"
"second_title": "Aspose.PDF for .NET API參考"
"title": "查看時指定頁面"
"url": "/zh-hant/net/programming-with-links-and-actions/specify-page-when-viewing/"
"weight": 110
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 查看時指定頁面

## 介紹

您是否希望透過在使用者開啟文件時將使用者引導至特定頁面來增強您的 PDF 應用程式？您來對地方了！在本指南中，我們將深入探討使用 Aspose.PDF for .NET 來指定開啟 PDF 時應顯示的頁面的細節。此功能可顯著改善使用者體驗，尤其是當您需要引起人們對文件關鍵部分的注意時。

## 先決條件

在深入編碼之前，讓我們確保您擁有開始所需的一切。以下是您需要的內容：

1. .NET 基礎知識：熟悉 .NET 框架至關重要。如果您熟悉 C# 並且對物件導向程式設計有基本的了解，那麼您就可以了！

2. Aspose.PDF for .NET：您需要在專案中安裝 Aspose.PDF 庫。如果你還沒有安裝，可以下載 [這裡](https://releases。aspose.com/pdf/net/).

3. Visual Studio：本教學假設您使用 Visual Studio 作為您的 IDE。確保您的機器上已安裝它。

4. PDF 檔案：您需要一個現有的 PDF 檔案以供使用。如果您沒有，您可以建立範例文件或使用您選擇的任何 PDF。

一旦滿足了這些先決條件，我們就可以捲起袖子開始編碼了！

## 導入包

現在我們已經完成所有設置，讓我們將必要的套件匯入到我們的專案中。請依照以下步驟操作：

### 啟動 Visual Studio

開啟 Visual Studio 並建立一個新項目或載入一個現有項目，在其中實作 PDF 頁面檢視功能。

### 參考Aspose.PDF

要使用 Aspose.PDF 庫，您需要新增對它的引用：

1. 在解決方案資源管理器中以滑鼠右鍵按一下您的專案。
2. 選擇“管理 NuGet 套件”。
3. 搜尋 `Aspose.PDF` 並安裝該軟體包。

### 導入命名空間

在程式碼檔案頂部新增以下使用指令：

```csharp
using System;
using System.IO;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
```

現在，您已準備好開始建立 PDF 頁面導航邏輯！

讓我們將任務分解為可管理的步驟。我們將編寫程式碼來開啟 PDF 文件、指定檢視時顯示的特定頁面並儲存更新的文件。 

## 步驟1：設定文檔目錄

首先，您需要設定文件的路徑：

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY"; // 替換為您的目錄
```

這條線本質上就是你的路線圖。您正在告訴程式碼在哪裡可以找到 PDF 檔案。確保更換 `YOUR DOCUMENT DIRECTORY` 使用您機器上的實際路徑。

## 步驟2：載入PDF文件

接下來，將 PDF 文件載入到應用程式中：

```csharp
// 載入 PDF 文件
Document doc = new Document(dataDir + "SpecifyPageWhenViewing.pdf");
```

這裡發生的事情是，你正在創建一個新的 `Document` 對象，同時指定 PDF 檔案的路徑。您可以將其想像為打開剛剛放在桌子上的書。

## 步驟3：造訪所需頁面

現在，讓我們訪問文件打開時想要顯示的頁面：

```csharp
// 取得文件第二頁的實例
Page page2 = doc.Pages[2]; // 請記住，索引從 1 開始
```

現在，我們正在存取文件的第二頁。值得注意的是，在這種情況下，頁碼從 1 開始，因此如果您考慮第 2 頁，則需要使用索引 2。

## 步驟 4：設定縮放係數

您可以調整將顯示的頁面的縮放等級：

```csharp
// 建立變數來設定目標頁面的縮放比例
double zoom = 1; // 表示 100% 縮放
```

設定縮放比例有助於確定使用者開啟後可以立即看到的頁面內容。值為 1 表示頁面將以 100% 縮放比例顯示，這通常是一個很好的預設值。

## 步驟 5：建立 GoToAction 實例

讓我們將導航功能付諸實踐：

```csharp
// 建立 GoToAction 實例
GoToAction action = new GoToAction(doc.Pages[2]); 
```

在此步驟中，您將建立一個實例 `GoToAction` 這實質上代表了導航到 PDF 中特定點的操作——在本例中是第二頁。

## 步驟 6：定義目標

現在，您需要定義操作應該導致什麼結果：

```csharp
// 轉至第 2 頁
action.Destination = new XYZExplicitDestination(page2, 0, page2.Rect.Height, zoom);
```

此行就像是為 GoToAction 設定 GPS 目的地。您告訴它要轉到頁面頂部（高度）和指定縮放等級的第 2 頁。

## 步驟 7：設定開啟操作

讓我們確保此操作在開啟文件時發生：

```csharp
// 設定文檔開啟操作
doc.OpenAction = action;
```

這樣，您就聲明了當您的 PDF 開啟時，我們剛剛定義的導航操作就會啟動。就好像您在文件的前門設置了迎賓墊一樣。

## 步驟 8：儲存更新後的文檔

最後，讓我們儲存已做更改的文件：

```csharp
// 儲存更新的文檔
doc.Save(dataDir + "goto2page_out.pdf");
```

這一步完成了你的工作！您將獲得一個名為 `goto2page_out.pdf` 直接開啟您指定的頁面。

這樣，編碼部分就完成了！您已成功編程 Aspose.PDF 以在開啟 PDF 時顯示特定頁面。 

## 結論

在本指南中，我們採用逐步的方法來了解如何使用 Aspose.PDF for .NET 指定 PDF 檔案中的頁面。此功能不僅可以改善使用者的導航，還可以簡化他們與文件中關鍵內容的互動。透過採用這些功能，您可以打造更友善的體驗，讓您的 PDF 應用程式脫穎而出。

## 常見問題解答

### 什麼是 Aspose.PDF for .NET？
Aspose.PDF for .NET 是一個函式庫，可讓開發人員在 .NET 應用程式內建立、修改和管理 PDF 文件。

### 我可以指定要查看多個頁面嗎？
不可以，您只能設定文件在指定的某個頁面開啟。但是，您可以為不同的初始頁面建立不同的文件。

### 如果我想以不同的縮放等級查看頁面怎麼辦？
您可以透過調整 `zoom` 儲存文件之前變數。

### 在哪裡可以找到更多使用 Aspose.PDF 的範例？
您可以檢查 [文件](https://reference.aspose.com/pdf/net/) 了解更多範例和功能。

### Aspose.PDF for .NET 有免費試用版嗎？
是的！您可以下載 Aspose.PDF 的免費試用版 [這裡](https://releases。aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}