---
"description": "透過我們的逐步教學學習如何使用 Aspose.PDF for .NET 在 PDF 中搜尋文字和新增超連結。"
"linktitle": "搜尋文字並添加超鏈接"
"second_title": "Aspose.PDF for .NET API參考"
"title": "搜尋文字並添加超鏈接"
"url": "/zh-hant/net/programming-with-text/search-text-and-add-hyperlink/"
"weight": 450
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 搜尋文字並添加超鏈接

## 介紹

您是否正在尋找一種不僅可以操作 PDF 還可以透過插入超連結來增強 PDF 功能的方法？嗯，您來對地方了！透過強大的 Aspose.PDF for .NET 程式庫，您可以在 PDF 文件中搜尋文字模式並無縫新增超連結。想像一下，有一份文件不僅傳達訊息，而且只需點擊連結即可將讀者連接到相關資源。聽起來不錯，對吧？在本教程中，我們將逐步指導您如何使用正規表示式搜尋文字並在 PDF 中新增超連結。無論您是經驗豐富的開發人員還是剛起步，您都會發現這個過程簡單且有益。

## 先決條件

在我們深入討論細節之前，讓我們確保您已準備好接下來需要的一切。以下是一份便捷的清單：

- .NET Framework：您的機器上應該安裝 .NET Framework（4.0 或更高版本）。
- Aspose.PDF for .NET 函式庫：不要忘記在您的專案下載並新增對 Aspose.PDF 庫的參考。你可以找到它 [這裡](https://releases。aspose.com/pdf/net/).
- IDE：您需要一個像 Visual Studio 這樣的整合開發環境 (IDE) 來編寫和執行程式碼。
- 範例 PDF 文件：取得一個範例 PDF 文件，您可以在其上測試程式碼。您可以建立一個簡單的 PDF 或使用您現有的文件之一。

一旦您完成清單上的所有內容，我們就可以開始了！

## 導入包

我們旅程的第一步是導入必要的套件。在這裡我們告訴我們的專案我們將使用什麼工具。您可以按照以下步驟操作：

在您的 C# 檔案中，首先在頂部包含以下命名空間：

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System;
```

透過匯入這些命名空間，您的程式可以存取 Aspose.PDF 提供的所有酷炫功能。

現在我們已經準備好了，是時候開始行動了。我們將透過一系列步驟來完成此操作，因此請密切注意！

### 步驟 1：設定文檔目錄

首先，您需要指定 PDF 檔案的儲存位置。修改 `dataDir` 變數指向您的文件的目錄。以下是操作方法：

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

確保更換 `"YOUR DOCUMENT DIRECTORY"` 與您的文件的實際路徑。

### 第 2 步：建立 TextFragmentAbsorber

接下來，我們需要一個工具來尋找我們想要連結的文字。輸入 `TextFragmentAbsorber`。這個小傢伙將幫助我們在 PDF 中搜尋特定的文字模式。

```csharp
TextFragmentAbsorber absorber = new TextFragmentAbsorber("\\d{4}-\\d{4}");
```

在這裡，我們正在尋找一種特定的模式：四位數字、一個破折號，後面跟著另外四位數字（如電話號碼或年份）。

### 步驟 3：啟用正規表示式搜尋

我們已經使用正規表示式來尋找文字模式，但我們需要確保我們的 `absorber` 知道它已啟用。這對於正確搜索至關重要。

```csharp
absorber.TextSearchOptions = new TextSearchOptions(true);
```

### 步驟4：初始化PdfContentEditor

現在我們已經準備好了吸收器，我們需要一個 `PdfContentEditor` 處理我們的 PDF 文件。這個類別讓我們綁定到我們的 PDF 並對其進行操作。

```csharp
PdfContentEditor editor = new PdfContentEditor();
```

### 步驟5：綁定來源PDF文件

我們的內容編輯器準備好後，就該將其綁定到我們要處理的實際 PDF 檔案了。

```csharp
editor.BindPdf(dataDir + "SearchRegularExpressionPage.pdf");
```

確保更換 `"SearchRegularExpressionPage.pdf"` 與您的 PDF 檔案的名稱相同。

### 步驟 6：接受頁面的吸收器

我們需要讓編輯知道我們想要在文件的特定頁面上搜尋。在這種情況下，讓我們轉到第 1 頁。

```csharp
editor.Document.Pages[1].Accept(absorber);
```

### 步驟 7：準備循環遍歷文字片段

現在，我們準備好循環遍歷吸收器發現的所有文字片段。我們將調整它們的外觀並設定我們的超連結。

```csharp
int[] dashArray = { };
String[] LEArray = { };
Color blue = Color.Blue;
```

在這裡，我們設定一些參數，例如超連結的顏色。

### 步驟 8：循環遍歷每個文字片段

對於符合我們搜尋的每個文字片段，我們將改變其顏色並建立超連結。它看起來是這樣的：

```csharp
foreach (TextFragment textFragment in absorber.TextFragments)
{
    textFragment.TextState.ForegroundColor = Aspose.Pdf.Color.Blue;
    Rectangle rect = new Rectangle((int)textFragment.Rectangle.LLX,
        (int)Math.Round(textFragment.Rectangle.LLY), (int)Math.Round(textFragment.Rectangle.Width + 2),
        (int)Math.Round(textFragment.Rectangle.Height + 1));
    Enum[] actionName = new Enum[2] { Aspose.Pdf.Annotations.PredefinedAction.Document_AttachFile, Aspose.Pdf.Annotations.PredefinedAction.Document_ExtractPages };
    
    editor.CreateWebLink(rect, "http://www.aspose.com", 1, 藍色, 動作名稱);
    editor.CreateLine(rect, "", (float)textFragment.Rectangle.LLX + 1, (float)textFragment.Rectangle.LLY - 1,
        (float)textFragment.Rectangle.URX, (float)textFragment.Rectangle.LLY - 1, 1, 1, blue, "S", dashArray, LEArray);
}
```

### 步驟9：儲存編輯後的PDF

我們快完成了！現在是時候將我們的變更儲存到新的 PDF 檔案了。

```csharp
dataDir = dataDir + "SearchTextAndAddHyperlink_out.pdf";
editor.Save(dataDir);
```

### 步驟 10：關閉編輯器

最後，別忘了關閉文件以釋放資源！

```csharp
editor.Close();
Console.WriteLine("\nText replaced and hyperlink added successfully based on a regular expression.\nFile saved at " + dataDir);
```

現在，您剛剛建立了一個基於搜尋結果動態產生的超連結的 PDF。那有多酷？

## 結論

就是這樣！透過遵循這些步驟，您已經學習如何使用 Aspose.PDF for .NET 庫搜尋 PDF 並新增超連結。這可以開啟一個充滿可能性的世界，特別是當您處理需要互動性的文件時。想像一下，只需幾行程式碼即可添加相關資源、參考網站甚至內部頁面的連結！
## 常見問題解答

### 什麼是 Aspose.PDF for .NET？  
Aspose.PDF for .NET 是一個函式庫，可讓開發人員在 .NET 應用程式中建立、操作和管理 PDF 文件。

### 如何下載適用於 .NET 的 Aspose.PDF？  
您可以下載庫 [這裡](https://releases。aspose.com/pdf/net/).

### 我可以免費試用 Aspose.PDF 嗎？  
絕對地！您可以免費試用 [這裡](https://releases。aspose.com/).

### 是否支援 Aspose 產品？  
是的，您可以找到支持和社區討論 [這裡](https://forum。aspose.com/c/pdf/10).

### 如何取得 Aspose.PDF 的臨時授權？  
您可以申請臨時駕照 [這裡](https://purchase。aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}