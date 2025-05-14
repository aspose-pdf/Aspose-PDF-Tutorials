---
"description": "透過本包含實際範例的逐步指南，了解如何使用 Aspose.PDF for .NET 輕鬆地在 PDF 檔案中填入描邊文字。"
"linktitle": "在 PDF 檔案中填入描邊文本"
"second_title": "Aspose.PDF for .NET API參考"
"title": "在 PDF 檔案中填入描邊文本"
"url": "/zh-hant/net/programming-with-stamps-and-watermarks/fill-stroke-text/"
"weight": 90
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 PDF 檔案中填入描邊文本

## 介紹

您是否曾經想修改 PDF 文件以使其脫穎而出？也許您需要添加醒目的水印或粗體印章，以使重要文件毫無疑問地屬於您。使用 Aspose.PDF for .NET，您可以輕鬆地在 PDF 文件中填充描邊文本，增添引人注目的藝術氣息。在今天的教學中，我們將逐步介紹使用 C# 在 PDF 中填入描邊文字的過程。最後，您將掌握如何像專業人士一樣操作 PDF 文件。

## 先決條件

在我們深入研究編碼之前，您需要做好幾件事才能使本教程變得輕鬆：

1. Visual Studio：確保您的機器上安裝了 Visual Studio，因為我們將編寫 C# 程式碼。
2. Aspose.PDF 庫：請確定您已下載 Aspose.PDF for .NET 庫。你可以抓住它 [這裡](https://releases。aspose.com/pdf/net/).
3. C# 基礎知識：熟悉 C# 程式設計將幫助您更輕鬆地理解本教學。
4. 範例 PDF 檔案：您需要一個範例 PDF 檔案（`input.pdf`）用於測試目的。您可以建立一個簡單的或使用任何現有的 PDF。

現在我們已經準備好一切，讓我們深入了解如何在 PDF 文件中填充描邊文字。

## 導入包

首先，我們需要導入必要的套件。以下是我們專案基本導入內容的簡要概述：

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

這些套件將允許我們使用 Aspose.PDF 庫的強大功能。

讓我們將主要任務分解為清晰的步驟。按照這些步驟，您可以輕鬆地將描邊文字填入 PDF 檔案中。 

## 步驟 1：設定您的環境

首先，請確保您的 Visual Studio 專案中的所有內容都已正確設定。建立新項目或選擇現有項目。如果您需要協助，請按以下步驟操作：

1. 開啟 Visual Studio。
2. 建立一個新的 C# 專案（例如，控制台應用程式）。
3. 在解決方案資源管理器中以滑鼠右鍵按一下項目，選擇「管理 NuGet 套件」。
4. 搜尋 `Aspose.PDF` 並安裝它。

## 第 2 步：定義文檔目錄

每個旅程都需要一個起點，在我們的例子中，它是輸入和輸出檔案所在的文件目錄。 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

代替 `"YOUR DOCUMENT DIRECTORY"` 使用輸入 PDF 檔案所在的實際路徑。 

## 步驟3：建立TextState對象

此步驟是您開始定義要新增的文字的屬性的地方。 

```csharp
TextState ts = new TextState();
```

這 `TextState` 物件將保存描邊文字的樣式選項。

## 步驟 4：設定描邊顏色

接下來，您需要定義文字描邊的顏色。 

```csharp
ts.StrokingColor = Color.Gray;
```

在這段程式碼中，我們使用灰色作為描邊。請隨意更改顏色以滿足您的需求！

## 步驟5：配置渲染模式

為確保您的文字按預期顯示，請設定渲染模式：

```csharp
ts.RenderingMode = TextRenderingMode.StrokeText;
```

這指示 Aspose 庫我們正在處理描邊文字。

## 步驟6：載入輸入PDF文檔

現在是時候載入您要修改的 PDF 檔案了。 

```csharp
Facades.PdfFileStamp fileStamp = new Facades.PdfFileStamp(new Aspose.Pdf.Document(dataDir + "input.pdf"));
```

確保您輸入的 PDF (`input.pdf`) 位於前面步驟中定義的文檔目錄中。

## 步驟 7：建立印章對象

接下來，建立一個可以容納筆畫文字的印章。 

```csharp
Aspose.Pdf.Facades.Stamp stamp = new Aspose.Pdf.Facades.Stamp();
```

此印章將用於將您的文字覆蓋在 PDF 上。

## 步驟8：定義要蓋章的文本

您需要指定要新增到 PDF 的文字：

```csharp
stamp.BindLogo(new Facades.FormattedText("PAID IN FULL", System.Drawing.Color.Gray, "Arial", Facades.EncodingType.Winansi, true, 78));
```

這裡，「PAID IN FULL」是我們要新增的文本，以及它的樣式屬性。根據您的要求進行客製化！

## 步驟 9：綁定文字狀態

現在，綁定 `TextState` 您先前定義的印章。 

```csharp
stamp.BindTextState(ts);
```

此步驟將所有樣式（例如顏色和渲染模式）套用至您的文字。

## 步驟10：設定印章的位置

確定您的印章在 PDF 中出現的位置：

```csharp
stamp.SetOrigin(100, 100);
```

論點 `(100, 100)` 表示文本原點的 X 和 Y 座標（以點為單位）。調整這些值以完美定位您的文字！

## 步驟 11：配置不透明度和旋轉

您可以在這裡嘗試改變文字的外觀：

```csharp
stamp.Opacity = 5;
stamp.BlendingSpace = Facades.BlendingColorSpace.DeviceRGB;
stamp.Rotation = 45.0F;
```

在這種情況下，不透明度值和 45 度的旋轉角度為您的文字增添了獨特的魅力。請隨意修改這些設定以獲得不同的效果。

## 步驟 12：將圖章加入 PDF

這是至關重要的一步，我們最終將包含筆畫文字的印章添加到 PDF 中：

```csharp
fileStamp.AddStamp(stamp);
```

就這樣，您的文字就可以發表聲明了！

## 步驟13：儲存並關閉文檔

最後，儲存您的變更並確保一切都已正確清理。 

```csharp
fileStamp.Save(dataDir + "output_out.pdf");
fileStamp.Close();
```

您新修改的包含描邊文字的 PDF 檔案將會儲存為 `output_out.pdf` 在您的文件目錄中。 

## 結論

就是這樣！遵循這些簡單的步驟，您可以使用 Aspose.PDF for .NET 輕鬆地在 PDF 檔案中填入描邊文字。無論是商業文件還是個人項目，此技術都可以讓您為 PDF 添加獨特的風格，使其在任何一疊文件中脫穎而出。

## 常見問題解答

### 什麼是 Aspose.PDF for .NET？
Aspose.PDF for .NET 是一個函式庫，可讓開發人員以程式設計方式建立、操作和轉換 PDF 檔案。

### 我可以免費使用 Aspose.PDF 嗎？
是的，Aspose 提供免費試用。你可以得到它 [這裡](https://releases。aspose.com/).

### 我需要支付許可證費用嗎？
雖然圖書館有免費試用，但也可以購買臨時許可證 [此連結](https://purchase。aspose.com/temporary-license/).

### 在哪裡可以找到該文件？
您可以存取完整的文檔 [這裡](https://reference。aspose.com/pdf/net/).

### 如果我遇到問題，可以獲得支援嗎？
絕對地！您可以在 Aspose 論壇上獲得支持 [這裡](https://forum。aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}