---
"description": "透過本簡單易懂的教學學習如何使用 Aspose.PDF for .NET 從 PDF 檔案中擷取段落。適合各個層級的開發人員。"
"linktitle": "提取 PDF 檔案中的段落"
"second_title": "Aspose.PDF for .NET API參考"
"title": "提取 PDF 檔案中的段落"
"url": "/zh-hant/net/programming-with-text/extract-paragraphs/"
"weight": 160
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 提取 PDF 檔案中的段落

## 介紹

當處理 PDF 時，提取資訊有時就像大海撈針。您是否曾經打開過 PDF 並想過“我只需要那一段文字？”嗯，你很幸運！在本指南中，我們將引導您完成使用 Aspose.PDF for .NET 從 PDF 中提取段落的過程。這個強大的程式庫為您提供了有效處理 PDF 文件所需的功能。準備好了嗎？我們走吧！

## 先決條件

在我們開始之前，讓我們確保您已準備好接下來需要的一切。以下是一份清單：

1. .NET 環境：確保您已設定 .NET 開發環境。這可以是 Visual Studio 或您選擇的任何其他 IDE。 
2. Aspose.PDF 函式庫：您需要 .NET 函式庫的 Aspose.PDF。您可以從下載 [這裡](https://releases。aspose.com/pdf/net/).
3. PDF 檔案：準備一個範例 PDF 文件以供測試。如果您沒有，請建立一個簡單的文字 PDF 或從網路上下載範例。
4. 基本 C# 知識：熟悉 C# 程式設計將幫助您更好地理解程式碼片段。

## 導入包

在開始編碼之前，我們需要導入必要的套件。這至關重要，因為它允許您的應用程式利用 Aspose.PDF 功能。具體操作如下：

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

確保將這些內容包含在 C# 檔案的頂部。這些命名空間將使您能夠處理 PDF 文件並存取文字功能。

現在我們已經設定了先決條件並導入了必要的套件，讓我們逐步分解提取過程。

## 步驟 1：設定文檔目錄的路徑

首先，我們需要指定 PDF 檔案的位置。這就像告訴你的程式碼，“嘿，我的 PDF 在這裡。”

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

代替 `"YOUR DOCUMENT DIRECTORY"` 使用儲存 PDF 文件的資料夾的實際路徑。這可能是這樣的 `"C:\\Users\\YourName\\Documents\\"`。

## 步驟2：開啟現有的PDF文件

設定路徑後，下一步是開啟要處理的 PDF 檔案。這是透過以下程式碼完成的：

```csharp
Document doc = new Document(dataDir + "input.pdf");
```

在這一行中，我們創建一個新的 `Document` 例如，提供 PDF 檔案的完整路徑。確保您的檔案命名正確（在本例中為「input.pdf」）並且位於指定的目錄中。

## 步驟 3：實例化 ParagraphAbsorber

接下來，我們將使用 `ParagraphAbsorber`，一個方便的工具，可以讓我們吸收（或抓取）PDF 中的所有段落。以下是操作方法：

```csharp
ParagraphAbsorber absorber = new ParagraphAbsorber();
```

想想 `ParagraphAbsorber` 就像一個吸塵器，從您的 PDF 中吸取所有相關文本，以便我們以後使用。

## 步驟 4：存取文檔

現在是時候使用我們的 `absorber`。這告訴我們的程式碼開始探索 PDF 的頁面和章節。

```csharp
absorber.Visit(doc);
```

這句話就是魔法開始的地方！這 `Visit` 方法遍歷文件並準備要提取的段落資料。

## 步驟 5：循環遍歷頁面標記

偉大的！現在我們已經加載了資訊。下一步是循環遍歷每個頁面標記。這是我們提取實際段落的地方：

```csharp
foreach (PageMarkup markup in absorber.PageMarkups)
{
    int i = 1;
    foreach (MarkupSection section in markup.Sections)
    {
        int j = 1;
        foreach (MarkupParagraph paragraph in section.Paragraphs)
        {
            StringBuilder paragraphText = new StringBuilder();
            foreach (List<TextFragment> line in paragraph.Lines)
            {
                foreach (TextFragment fragment in line)
                {
                    paragraphText.Append(fragment.Text);
                }
                paragraphText.Append("\r\n");
            }
            paragraphText.Append("\r\n");
            Console.WriteLine("Paragraph {0} of section {1} on page {2}:", j, i, markup.Number);
            Console.WriteLine(paragraphText.ToString());
            j++;
        }
        i++;
    }
}
```

讓我們分析一下這段程式碼中發生的事情：

- 外循環：我們循環遍歷每個頁面的標記以獲取部分。
- 中間循環：對於每個部分，我們訪問段落。
- 內循環：我們循環遍歷每個段落內的文字行以提取文字片段。
- StringBuilder：我們使用它來有效地建構段落文字。

最後，我們列印出各段落及其章節和頁碼。這有助於使輸出中的內容保持井然有序並且引用清晰。

## 步驟 6：編譯並執行您的應用程式

最後一步是編譯您的應用程式並運行它以查看結果。如果一切設定正確，當您執行程式碼時，您應該會在控制台視窗中看到從 PDF 中提取的段落。

## 結論

就是這樣！您剛剛使用 Aspose.PDF for .NET 從 PDF 中提取了段落。這個過程乍看之下可能很複雜，但透過將其分解為易於管理的步驟，您可以像專業人士一樣處理 PDF 操作。無論您處理的是操作文件、報告，甚至是小說摘錄，有效地提取文字都是一項寶貴的技能。 Aspose.PDF 的功能不僅限於文字擷取，我們鼓勵您進一步探索其文件。

## 常見問題解答

### 我可以使用 Aspose.PDF 從 PDF 中提取圖像嗎？
是的，Aspose.PDF 支援影像擷取和文字擷取。

### Aspose.PDF 是否與所有版本的 .NET 相容？
Aspose.PDF相容於多個版本，包括.NET Framework和.NET Core。

### 我可以使用臨時許可證進行測試嗎？
絕對地！您可以申請臨時駕照 [這裡](https://purchase。aspose.com/temporary-license/).

### 如果在提取段落時遇到錯誤怎麼辦？
您可以在 Aspose 支援論壇尋求協助 [這裡](https://forum。aspose.com/c/pdf/10).

### Aspose.PDF 有免費試用版嗎？
是的，您可以從 Aspose 網站下載免費試用版 [這裡](https://releases。aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}