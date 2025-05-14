---
"description": "透過本逐步指南了解如何使用 Aspose.PDF for .NET 指定 PDF 中的行距。非常適合尋求精確文字格式的開發人員。"
"linktitle": "指定 PDF 檔案中的行距"
"second_title": "Aspose.PDF for .NET API參考"
"title": "指定 PDF 檔案中的行距"
"url": "/zh-hant/net/programming-with-text/specify-line-spacing/"
"weight": 510
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 指定 PDF 檔案中的行距

## 介紹

您是否曾為控制 PDF 檔案中的行距而苦惱？也許您的文字看起來過於擁擠，或者看起來不像您想要的那樣精緻。在本教學中，我們將介紹如何使用 Aspose.PDF for .NET 輕鬆指定 PDF 中的行距。我們將使用簡單的逐步指南，幫助您從空白 PDF 轉換為包含自訂行距的 PDF。如果您需要精確佈局報告、發票或證書等文件的文本，那麼這是完美的選擇。

## 先決條件

在我們進入程式碼之前，讓我們確保您已經擁有所需的一切：

1. 已安裝 Aspose.PDF for .NET。如果你沒有，可以從 [Aspose.PDF下載頁面](https://releases。aspose.com/pdf/net/).
2. .NET 開發環境（如 Visual Studio）。
3. TrueType 字型檔（`.ttf`) 我們將在範例中使用它。您可以使用任何字體，但在本指南中，我們將使用 `HPSimplified.TTF` 字體。
4. C# 和 PDF 操作的基本知識。

如果您準備好了，讓我們繼續匯入必要的套件。

## 導入包

在您的 C# 專案中，您需要匯入 Aspose.PDF 命名空間才能使用 PDF 功能。以下是具體操作方法：

```csharp
using Aspose.Pdf.Text;
using System.IO;
```

這些命名空間可讓您建立和操作 PDF 文檔，以及使用文字格式和字型選項。

我們將把它分解成幾個小步驟，以便您可以輕鬆跟進。每個步驟將集中於流程的關鍵部分，從設定 PDF 到指定行距。

## 步驟 1：設定項目並定義文件目錄

我們需要做的第一件事是確定文件的位置。這有助於程式知道在哪裡找到字體以及在哪裡保存生成的 PDF。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string fontFile = dataDir + "HPSimplified.TTF";
```

在此步驟中，您將替換 `"YOUR DOCUMENT DIRECTORY"` 以及您儲存檔案的實際路徑。這將是您放置字體檔案的地方（`HPSimplified.TTF`) 以及 PDF 的保存位置。

## 第 2 步：載入 PDF 文檔

現在，我們需要建立一個新的 PDF 文件。對於本指南，我們將從一個空白文件開始，但您也可以根據需要載入現有的 PDF。

```csharp
Document doc = new Document();
```

這將建立一個新的空 PDF 文件。很簡單，對吧？

## 步驟 3：設定文字格式選項

這就是奇蹟發生的地方。我們將為想要新增到 PDF 的文字指定行距模式。 Aspose.PDF 為我們提供了多種選擇，但在本指南中，我們將使用 `LineSpacingMode.FullSize`，以確保完全遵守行距。

```csharp
TextFormattingOptions formattingOptions = new TextFormattingOptions();
formattingOptions.LineSpacing = TextFormattingOptions.LineSpacingMode.FullSize;
```

此程式碼將行距模式設定為 `FullSize`，確保文字以適當的間距顯示。還有其他選擇，例如 `Proportional` 如果你想要不同的間距行為，但現在，我們先堅持 `FullSize`。

## 步驟 4：建立文字片段

現在，我們將建立放置在 PDF 中的實際文字。該文字將遵循我們定義的行距。

```csharp
TextFragment textFragment = new TextFragment("Hello world");
```

我們創建了一個包含字串的文字片段 `"Hello world"`。當然，您可以根據自己的喜好自訂此文字。

## 步驟 5：載入並套用自訂字體

為了讓文字脫穎而出，我們將從文件中載入自訂 TrueType 字型。此步驟是可選的，但它可以為您的 PDF 增添專業感。

```csharp
if (fontFile != "")
{
    using (FileStream fontStream = System.IO.File.OpenRead(fontFile))
    {
        textFragment.TextState.Font = FontRepository.OpenFont(fontStream, FontTypes.TTF);
```

在這裡，我們加載字體文件並將其應用於文字片段。如果檔案路徑有效，則使用該字體。否則，將套用預設字體。

## 步驟 6：設定文字位置和格式

接下來，我們需要在 PDF 上定位文字。我們還將應用先前建立的格式選項。

```csharp
textFragment.Position = new Position(100, 600);
textFragment.TextState.FormattingOptions = formattingOptions;
```

這 `Position` 方法設定文字在頁面上出現的座標（在本例中，距離左側 100 個單位，距離底部 600 個單位）。格式選項（包括行距模式）都在這裡套用。

## 步驟 7：為 PDF 頁面新增文本

現在我們的文字已經格式化並定位，是時候將其新增至 PDF 文件了。

```csharp
var page = doc.Pages.Add();
page.Paragraphs.Add(textFragment);
```

此程式碼在 PDF 文件中建立一個新頁面並將文字片段新增到其中。

## 步驟 8：儲存 PDF

我們已經到達最後一步！現在一切都已設定完畢，讓我們儲存 PDF。

```csharp
dataDir = dataDir + "SpecifyLineSpacing_out.pdf";
doc.Save(dataDir);
```

這將保存具有指定行距的 PDF，並且您的文件已準備好！

## 結論

就是這樣！您剛剛使用 Aspose.PDF for .NET 建立了具有自訂行距的 PDF 文件。它是一個強大的工具，可讓您控制 PDF 文件的各個方面，這只是您可以實現的功能的一個範例。從文字放置到格式，可能性無窮無盡。

如果您想深入了解 PDF 操作，Aspose.PDF 提供了豐富的功能供您探索。不要猶豫，嘗試並突破您對文件所能做的極限！

## 常見問題解答

### 我可以將行距調整為其他模式嗎？  
是的，您可以使用其他模式，例如 `Prop或者tional` or `Fixed` 取決於您的需求。

### 是否可以從系統而不是文件加載字體？  
是的，你可以使用 `FontRepository`。

### 我可以將 Aspose.PDF for .NET 與其他文件格式一起使用嗎？  
絕對地！ Aspose.PDF for .NET 支援多種格式，如 XML、HTML 等。

### 我需要許可證才能使用 Aspose.PDF for .NET 嗎？  
是的，為了獲得全部功能，您需要許可證，您可以獲得 [這裡](https://purchase。aspose.com/buy).

### 如何設定多個段落的行距？  
您可以申請 `TextFormattingOptions` 對每一個 `TextFragment` 或者 `TextParagraph` 控制多行或段落的間距。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}