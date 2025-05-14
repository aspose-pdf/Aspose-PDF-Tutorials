---
"description": "透過本逐步指南了解如何使用 Aspose.PDF for .NET 為 PDF 檔案新增日期和時間戳記。非常適合增強文件的真實性。"
"linktitle": "在 PDF 檔案中新增日期時間戳"
"second_title": "Aspose.PDF for .NET API參考"
"title": "在 PDF 檔案中新增日期時間戳"
"url": "/zh-hant/net/programming-with-stamps-and-watermarks/add-date-time-stamp/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 檔案中新增日期時間戳

## 介紹

在管理文件（尤其是 PDF）時，新增日期和時間戳記可能會改變遊戲規則。無論您處理的是法律文件、專案報告或發票，時間戳不僅可以增加真實性，還可以提供文件建立或修改時間的清晰記錄。在本指南中，我們將引導您完成使用 .NET 的 Aspose.PDF 庫為 PDF 檔案新增日期和時間戳記的過程。 

本文旨在簡單易懂，因此即使您是程式設計或 Aspose.PDF 庫的新手，您也能夠自信地實現此功能。讓我們開始吧！

## 先決條件

在我們開始之前，您需要滿足一些先決條件：

1. Visual Studio：確保您的機器上安裝了 Visual Studio。這是您編寫和執行程式碼的地方。
2. Aspose.PDF for .NET：您需要下載並安裝 Aspose.PDF 庫。你可以找到最新版本 [這裡](https://releases。aspose.com/pdf/net/).
3. C# 基礎知識：熟悉 C# 程式設計將幫助您更好地理解範例，但如果您剛開始，請不要擔心；我們將逐步解釋一切。
4. PDF 檔案：準備好範例 PDF 檔案。在我們的例子中，我們將使用一個名為 `AddTextStamp。pdf`.

一旦滿足這些先決條件，您就可以開始在 PDF 文件中新增日期和時間戳記！

## 導入包

首先，您需要在 C# 專案中匯入必要的命名空間。具體操作如下：

### 建立新專案

1. 開啟 Visual Studio：啟動您的 Visual Studio 應用程式。
2. 建立新項目：從開始畫面選擇「建立新項目」。
3. 選擇控制台應用程式：從專案範本清單中選擇“控制台應用程式（.NET Framework）”。
4. 命名您的項目：為您的項目命名，例如， `PDFDateTimeStamp`。

### 新增 Aspose.PDF 參考

1. 右鍵點選「引用」：在解決方案資源管理器中，右鍵點選專案的「引用」資料夾。
2. 選擇“新增引用”：從上下文選單中選擇“新增引用”。
3. 瀏覽 Aspose.PDF：導航到下載 Aspose.PDF 的位置並選擇它。按一下「確定」將其新增至您的專案。

### 導入所需的命名空間

在你的頂部 `Program.cs` 文件，您需要匯入以下命名空間：

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
using Aspose.Pdf.Annotations;
```

現在我們已經完成所有設置，讓我們將向 PDF 文件添加日期和時間戳記的過程分解為清晰、易於管理的步驟。

## 步驟1：設定文檔目錄

首先，您需要指定 PDF 檔案所在的目錄。這很關鍵，因為程式碼將在此目錄中找到 PDF。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY"; // 替換為你的實際路徑
```

確保更換 `YOUR DOCUMENT DIRECTORY` 使用您的 PDF 檔案的實際路徑。

## 第 2 步：開啟 PDF 文檔

接下來，您將開啟要新增時間戳記的 PDF 文件。 

```csharp
// 開啟文件
Document pdfDocument = new Document(dataDir + "AddTextStamp.pdf");
```

這行程式碼初始化 `Document` 類別並將您的 PDF 文件加載到 `pdfDocument` 目的。

## 步驟 3：建立日期時間戳

現在是時候產生日期和時間戳記了。您將對其進行格式化以便以特定方式顯示。 

```csharp
string annotationText = DateTime.Now.ToString("MM/dd/yy hh:mm:ss tt ");
```

這裡， `DateTime.Now` 取得當前日期和時間，並 `ToString` 將其格式化為您想要的格式。

## 步驟 4：建立文字印章

準備好日期和時間字串後，您現在可以建立將新增到 PDF 的文字戳記。

```csharp
// 建立文字戳
TextStamp textStamp = new TextStamp(annotationText);
```

這行創建了一個新實例 `TextStamp` 使用格式化的日期和時間字串。

## 步驟5：設定圖章的屬性

您可以自訂印章的外觀和位置。設定其屬性的方法如下：

```csharp
// 設定圖章的屬性
textStamp.BottomMargin = 10;
textStamp.RightMargin = 20;
textStamp.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Right;
textStamp.VerticalAlignment = VerticalAlignment.Bottom;
```

在此步驟中，我們設定邊距並將印章與 PDF 頁面的右下角對齊。

## 步驟 6：將圖章加入 PDF

現在是時候將文字標記新增至您的 PDF 文件了。 

```csharp
// 在集郵冊上新增郵票
pdfDocument.Pages[1].AddStamp(textStamp);
```

此行將印章新增至 PDF 的第一頁。如果您想將其放在不同的頁面上，您可以更改頁碼。

## 步驟 7：建立自由文字註釋（可選）

如果您想為圖章添加註釋，您可以建立 `FreeTextAnnotation` 如下：

```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 6, System.Drawing.Color.Black);
FreeTextAnnotation textAnnotation = new FreeTextAnnotation(pdfDocument.Pages[1], new Aspose.Pdf.Rectangle(0, 0, 0, 0), default_appearance);
textAnnotation.Name = "Stamp";
textAnnotation.Accept(new AnnotationSelector(textAnnotation));
textAnnotation.Contents = textStamp.Value;
```

此可選步驟可建立一個自由文字註釋，可提供有關郵票的額外背景或資訊。

## 步驟8：配置註解邊框

如果您想自訂註解的邊框，也可以這樣做：

```csharp
Border border = new Border(textAnnotation);
border.Width = 0;
border.Dash = new Dash(1, 1);
textAnnotation.Border = border;
textAnnotation.Rect = new Aspose.Pdf.Rectangle(0, 0, 0, 0);
pdfDocument.Pages[1].Annotations.Add(textAnnotation);
```

此程式碼片段將邊框寬度設為 0，使其不可見，並將註解新增至 PDF。

## 步驟9：儲存PDF文檔

最後，需要儲存修改後的PDF文件。 

```csharp
dataDir = dataDir + "AddDateTimeStamp_out.pdf"; // 指定輸出檔名
pdfDocument.Save(dataDir);
Console.WriteLine("\nDate time stamp added successfully.\nFile saved at " + dataDir);
```

此行將新增時間戳記的 PDF 儲存到新文件。您可以檢查指定的目錄來查看輸出。

## 結論

恭喜！您已成功使用 Aspose.PDF for .NET 為 PDF 檔案新增日期和時間戳記。這個簡單而有效的功能可以增強您的文檔，使其更加專業，並提供創建或修改時間的清晰記錄。 

## 常見問題解答

### 我可以自訂時間戳中的日期格式嗎？
是的，您可以修改 `ToString` 方法將日期格式變更為您喜歡的格式。

### Aspose.PDF 可以免費使用嗎？
Aspose.PDF 提供免費試用，但要使用全部功能，您需要購買授權。您可以獲得臨時駕照 [這裡](https://purchase。aspose.com/temporary-license/).

### 我可以在 PDF 中新增多個時間戳記嗎？
絕對地！您可以建立多個 `TextStamp` 實例並將它們新增至 PDF 中的不同頁面或位置。

### 如果我沒有 Visual Studio 怎麼辦？
您可以使用任何 C# IDE 或文字編輯器，但為了執行和偵錯您的項目，建議使用 Visual Studio。

### 在哪裡可以找到更多使用 Aspose.PDF 的範例？
您可以在 [Aspose.PDF文檔](https://reference。aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}