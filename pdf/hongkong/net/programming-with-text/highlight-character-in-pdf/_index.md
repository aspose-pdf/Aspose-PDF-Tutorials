---
"description": "透過本全面的逐步指南，學習如何使用 Aspose.PDF for .NET 來反白 PDF 中的字元。"
"linktitle": "PDF檔案中的高亮字符"
"second_title": "Aspose.PDF for .NET API參考"
"title": "PDF檔案中的高亮字符"
"url": "/zh-hant/net/programming-with-text/highlight-character-in-pdf/"
"weight": 240
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF檔案中的高亮字符

## 介紹

在處理 PDF 時，經常需要突出顯示文字或字元——無論是出於學術目的、編輯還是僅僅提高可讀性。想像一下，您有一份漂亮的文檔，但您想強調某些部分。這就是突出顯示的作用所在！在本教程中，我們將深入研究如何使用強大的 Aspose.PDF for .NET 庫突出顯示 PDF 文件中的字元。 

## 先決條件

在我們進入程式碼之前，讓我們確保我們擁有所需的一切。以下是您需要的內容：

1. 開發環境：本教學假設您正在使用 Visual Studio 或類似的 .NET IDE。
2. Aspose.PDF for .NET Library：如果您還沒有，您可以 [點此下載](https://releases.aspose.com/pdf/net/) 並將其添加到您的項目中。 
3. C# 基礎知識：C# 程式設計入門將幫助您輕鬆理解實作。
4. PDF 文件：您應該有一個可供使用的範例 PDF 文件。您可以建立一個或使用現有文件。

## 導入包

首先，我們需要導入必要的命名空間。為此，您需要將它們包含在 C# 檔案的頂部：

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Devices;
using Aspose.Pdf.Text;
using System;
using System.Drawing;
```

這些套件對於使用 Aspose 庫建立、操作和處理 PDF 文件至關重要。

現在，讓我們將這個過程分解為易於理解的步驟來突出顯示 PDF 中的字元。 

## 步驟 1：初始化 PDF 文檔

第一步是初始化您的 PDF 文件。這涉及加載您將要使用的 PDF 文件。具體操作如下：

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // 確保設定正確的路徑。
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document(dataDir + "input.pdf");
```
在此程式碼片段中，替換 `YOUR DOCUMENT DIRECTORY` 使用您的機器上輸入 PDF 檔案所在的實際路徑。這 `Aspose.Pdf.Document` 類別被實例化以載入您的 PDF。

## 步驟 2：設定渲染過程

接下來，我們需要為我們的文件準備渲染過程。這對於準確突出顯示頁面上的字元至關重要。

```csharp
int resolution = 150; // 設定影像擷取的解析度。
using (MemoryStream ms = new MemoryStream())
{
    PdfConverter conv = new PdfConverter(pdfDocument);
    conv.Resolution = new Resolution(resolution, resolution);
    conv.GetNextImage(ms, System.Drawing.Imaging.ImageFormat.Png);
    Bitmap bmp = (Bitmap)Bitmap.FromStream(ms);
```
我們為了清晰度定義了一個分辨率，以便正確呈現文字。這 `PdfConverter` 將 PDF 頁面轉換為圖像，以便我們可以在其上繪圖。

## 步驟3：建立用於繪圖的圖形對象

設定繪圖過程後，我們需要建立一個圖形物件來執行突出顯示：

```csharp
using (System.Drawing.Graphics gr = System.Drawing.Graphics.FromImage(bmp))
{
    float scale = resolution / 72f; // 比例因子。
    gr.Transform = new System.Drawing.Drawing2D.Matrix(scale, 0, 0, -scale, 0, bmp.Height);
```
在這裡，我們從點陣圖影像創建圖形物件。轉換有助於調整渲染以正確匹配所需的解析度。

## 步驟 4：循環遍歷每個頁面並突出顯示文本

現在，讓我們循環遍歷 PDF 中的每一頁並找到我們想要突出顯示的文字片段：

```csharp
for (int i = 0; i < pdfDocument.Pages.Count; i++)
{
    Page page = pdfDocument.Pages[i + 1]; // 在 Aspose 中，頁面以 1 為索引。
    TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber(@"[\S]+");
    textFragmentAbsorber.TextSearchOptions.IsRegularExpressionUsed = true;
    page.Accept(textFragmentAbsorber);
```
我們造訪每個頁面並使用 `TextFragmentAbsorber`。正規表示式模式 `@"[\S]+"` 捕獲所有非空白字元。

## 步驟5：提取文字片段並反白顯示

現在是時候提取文字片段並突出顯示它們了。這個過程涉及在我們想要突出顯示的字元周圍繪製矩形：

```csharp
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;

foreach (TextFragment textFragment in textFragmentCollection)
{
    // 在此強調邏輯
    for (int segNum = 1; segNum <= textFragment.Segments.Count; segNum++)
    {
        TextSegment segment = textFragment.Segments[segNum];
        for (int charNum = 1; charNum <= segment.Characters.Count; charNum++)
        {
            CharInfo characterInfo = segment.Characters[charNum];
            gr.DrawRectangle(Pens.Black, 
                (float)characterInfo.Rectangle.LLX, 
                (float)characterInfo.Rectangle.LLY, 
                (float)characterInfo.Rectangle.Width, 
                (float)characterInfo.Rectangle.Height);
        }
    }
}
```
我們循環遍歷每個文字片段、其段落和單個字符，使用先前創建的圖形物件在它們周圍繪製矩形。

## 步驟6：儲存修改後的影像

突出顯示後，您需要將生成的圖像儲存為新的 PNG 檔案：

```csharp
dataDir = dataDir + "HighlightCharacterInPDF_out.png";
bmp.Save(dataDir, System.Drawing.Imaging.ImageFormat.Png);
```
此行將修改後的點陣圖影像作為 PNG 檔案保存在指定目錄中。 

## 步驟 7：結束異常處理

最後，將程式碼包裝在 try-catch 區塊中是一種很好的做法，確保我們能夠優雅地處理任何意外錯誤：

```csharp
catch (Exception ex)
{
    Console.WriteLine(ex.Message + "\nThis example will only work if you apply a valid Aspose License. You can purchase full license or get a 30-day temporary license from [here](https://購買請前往 purchase.aspose.com/temporary-license/。 ");
}
```

此區塊捕獲過程中可能發生的任何異常並向使用者提供資訊回饋。

## 結論

就是這樣！您已成功使用 Aspose.PDF for .NET 反白顯示 PDF 檔案中的字元。這個強大的庫為 PDF 操作打開了無限可能的大門——無論您是處理註釋、表單填寫，還是文件轉換。當您繼續使用 Aspose 時，請記住實踐是關鍵。不斷嘗試不同的功能，您很快就會成為 PDF 專家！

## 常見問題解答

### 什麼是 Aspose.PDF for .NET？
Aspose.PDF for .NET 是一個函式庫，允許在 .NET 應用程式中以程式設計方式建立、操作和轉換 PDF 文件。

### 我可以一次突出顯示多個文字片段嗎？
是的，所提供的程式碼可以透過循環遍歷 PDF 中的所有文字來突出顯示多個片段。

### Aspose.PDF 有免費版嗎？
是的，Aspose 提供免費試用，因此您可以在購買前測試該庫。

### 我需要任何許可證才能使用 Aspose.PDF 嗎？
是的，商業用途需要有效的許可證，但您可以獲得 30 天的臨時許可證進行測試。

### 在哪裡可以找到更多文件？
您可以參考 [Aspose.PDF文檔](https://reference.aspose.com/pdf/net/) 有關實施和功能的更多詳細資訊。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}