---
"description": "了解如何使用 Aspose.PDF for .NET 中的文字裝置從 PDF 文件中擷取文字。"
"linktitle": "使用文本設備提取文本"
"second_title": "Aspose.PDF for .NET API參考"
"title": "使用文本設備提取文本"
"url": "/zh-hant/net/programming-with-text/extract-text-using-text-device/"
"weight": 210
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用文本設備提取文本

## 介紹

從 PDF 中提取文字可能很棘手，尤其是在處理具有各種格式、嵌入字體或複雜佈局的文件時。但有了 Aspose.PDF for .NET，這個過程就變得輕而易舉了！無論您想將 PDF 頁面轉換為純文字以便進一步分析，還是僅需要提取特定部分，Aspose.PDF 都能滿足您的需求。在本教學中，我們將逐步介紹如何使用 Aspose.PDF 中的 TextDevice 類別從 PDF 中提取文字。我們還將提供清晰的解釋，以便您可以輕鬆地將相同的方法應用到您自己的專案中。

## 先決條件

在我們進入程式碼之前，請確保您已準備好一切可以繼續進行的操作。您需要準備以下物品：

1. Aspose.PDF for .NET：從下載最新版本 [Aspose.PDF for .NET下載頁面](https://releases。aspose.com/pdf/net/).
2. 開發環境：Visual Studio 或任何其他 C# 開發環境。
3. .NET Framework：確保您的專案針對的是 .NET Framework 4.x 或更高版本。
4. 輸入 PDF 檔案：用於文字擷取的 PDF 檔案。將其放在你的機器上的目錄中（我們稱之為 `YOUR DOCUMENT DIRECTORY`）。

## 導入包

在程式碼頂部，您需要匯入必要的命名空間才能使用 Aspose.PDF：

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Devices;
using System;
using System.Text;
```

## 步驟 1：載入 PDF 文檔

在提取文字之前，我們需要將 PDF 文件載入到記憶體中。在此步驟中，您將使用 Aspose.PDF 的 `Document` 班級。這將允許您存取文件中的所有頁面和內容。

```csharp
// 定義 PDF 文件的路徑
string dataDir = "YOUR DOCUMENT DIRECTORY";

// 載入 PDF 文件
Document pdfDocument = new Document(dataDir + "input.pdf");
```

這裡我們使用 `Document pdfDocument = new Document(dataDir + "input.pdf");` 加載 PDF。這 `dataDir` 變數保存 PDF 檔案的目錄路徑。這將使我們能夠訪問整個文檔，從而允許我們循環瀏覽頁面並提取內容。

## 步驟 2：設定用於文字儲存的字串產生器

現在文檔已加載，我們需要一種方法來儲存提取的文字。為此，我們將使用 `StringBuilder` 這允許高效的字串連接。

```csharp
// StringBuilder 保存提取的文本
StringBuilder builder = new StringBuilder();
```

我們初始化一個 `StringBuilder` 實例，它將收集從每個頁面提取的文字。與循環中的常規字串連接相比，這是一種處理大字串的更有效的方法。

## 步驟 3：循環遍歷 PDF 頁面

接下來，我們循環遍歷 PDF 文件的每一頁來提取文字。我們將使用 `TextDevice` 類，負責將PDF內容轉換為文字格式。

```csharp
// 循環遍歷 PDF 中的所有頁面
foreach (Page pdfPage in pdfDocument.Pages)
{
    // 處理每個頁面以提取文本
}
```

此循環遍歷 PDF 的每一頁（`pdfDocument.Pages`）。對於每個頁面，我們將提取文字並將其添加到我們的 `StringBuilder`。

## 步驟 4：從每個頁面提取文本

現在，我們為每個頁面設定文字擷取過程。在這裡，我們將創建一個 `TextDevice` 物件並使用它來處理 PDF 頁面。這 `TextDevice` 根據我們設定的提取選項提取原始或格式化的文字。

```csharp
using (MemoryStream textStream = new MemoryStream())
{
    // 建立用於文字擷取的文字設備
    TextDevice textDevice = new TextDevice();
    
    // 將文字擷取選項設定為“純”模式
    TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);
    textDevice.ExtractionOptions = textExtOptions;

    // 從當前頁面中提取文字並儲存到記憶體流中
    textDevice.Process(pdfPage, textStream);

    // 將記憶體流轉換為文字
    string extractedText = Encoding.Unicode.GetString(textStream.ToArray());

    // 將提取的文字附加到 StringBuilder
    builder.Append(extractedText);
}
```

- `TextDevice textDevice = new TextDevice();`： 這 `TextDevice` 類別用於從 PDF 中提取文字。
- `TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);`：此選項提取原始文字而不保留任何格式，如字體或位置。您也可以使用 `TextFormattingMode.Raw` 如果您需要對格式進行更多的控制。
- `textDevice.Process(pdfPage, textStream);`：這將處理 PDF 的每一頁並將提取的文字儲存在 `MemoryStream`。
- 最後，我們將文本從 `MemoryStream` 到一個字串並將其附加到 `StringBuilder`。

## 步驟 5：將提取的文字儲存到文件

處理完所有頁面後，文字將儲存在 `StringBuilder`。最後一步是將提取的文字儲存到文件中。

```csharp
// 定義文字檔案的輸出路徑
dataDir = dataDir + "input_Text_Extracted_out.txt";

// 將提取的文字儲存到文件中
File.WriteAllText(dataDir, builder.ToString());

Console.WriteLine("\nText extracted successfully from PDF document.\nFile saved at " + dataDir);
```

- `File.WriteAllText(dataDir, builder.ToString());`：這將寫入 `StringBuilder` 存入文本文件。
- 輸出檔案的路徑是透過附加檔案名稱來設定的（`"input_Text_Extracted_out.txt"`）到 `dataDir` 小路。

## 結論

使用 Aspose.PDF for .NET 從 PDF 中提取文字是一個簡單而有效率的過程。按照本指南中概述的步驟，您可以輕鬆開啟 PDF 文件、循環瀏覽頁面並將文字提取到文字檔案中。這對於處理大量 PDF 資料、執行文字分析或轉換文件以進行進一步操作特別有用。

使用 Aspose.PDF，您不僅限於文字擷取 - 您還可以處理註釋，操作圖像，甚至將 PDF 轉換為其他格式，如 HTML 或 Word。該程式庫的靈活性和強大功能使其成為 .NET 應用程式中 PDF 管理的寶貴工具。

## 常見問題解答

### Aspose.PDF 可以從基於圖像的 PDF 中提取文字嗎？
不，Aspose.PDF 旨在從基於內容的 PDF 中提取文字。對於基於影像的PDF，需要OCR技術。

### 擷取文字時 Aspose.PDF 是否保留格式？
預設情況下，提取的文字沒有格式，但如果您想保留一些格式，可以調整提取選項。

### 我可以從特定頁面範圍中提取文字嗎？
是的，您可以修改程式碼以循環遍歷特定範圍的頁面而不是所有頁面。

### Aspose.PDF 中的文字擷取模式有哪些？
Aspose.PDF提供兩種模式：Raw和Pure。原始模式嘗試保留原始佈局，而純模式僅提取不帶格式的文字。

### Aspose.PDF for .NET 是否與 .NET Core 相容？
是的，Aspose.PDF for .NET 與 .NET Core 和 .NET Framework 完全相容。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}