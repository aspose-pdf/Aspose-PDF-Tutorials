---
"description": "了解如何使用 Aspose.PDF for .NET 在 PDF 中設定單選按鈕標題。本逐步指南將引導您載入、修改和儲存 PDF 表單。"
"linktitle": "設定單選按鈕標題"
"second_title": "Aspose.PDF for .NET API參考"
"title": "設定單選按鈕標題"
"url": "/zh-hant/net/programming-with-forms/set-radio-button-caption/"
"weight": 280
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 設定單選按鈕標題

## 介紹

如果您正在使用 Aspose.PDF for .NET 進行 PDF 操作，那麼您將獲得巨大的成功！今天，我們重點介紹一個實用功能：在 PDF 表單中設定單選按鈕標題。對於需要從一組選項中進行選擇的使用者表單來說，單選按鈕至關重要。把它們想像成只允許一個答案的選擇題。本教學將引導您完成更新 PDF 表單中單選按鈕標題的過程，以便您的文件既具有互動性又具有使用者友善性。 

## 先決條件

在深入研究程式碼之前，您需要確保已做好以下幾件事：

1. Aspose.PDF for .NET：請確定您已安裝 Aspose.PDF 庫。該庫將幫助您以程式設計方式操作 PDF 文件。
2. 開發環境：您應該設定一個 .NET 開發環境，例如 Visual Studio。
3. 範例 PDF 表單：對於本教學課程，您需要一個帶有單選按鈕的範例 PDF 表單。您可以使用任何現有的 PDF 表單或建立一個帶有單選按鈕的新表單。
4. C# 基礎：本指南假設您對 C# 和 .NET 程式設計概念有基本的了解。

如果您尚未安裝 Aspose.PDF for .NET 或需要臨時許可證，您可以 [點此下載](https://releases.aspose.com/pdf/net/) 或者 [取得臨時執照](https://purchase。aspose.com/temporary-license/).

## 導入包

首先，您需要在 C# 專案中匯入必要的套件。以下是包含 Aspose.PDF 庫的方法：

```csharp
using System;
using Aspose.Pdf.Forms;
using System.Collections.Generic;
using Aspose.Pdf.Text;
```

確保您已透過 NuGet 或您喜歡的方法將這些套件新增至您的專案中。

## 步驟 1：載入 PDF 表單

首先，您需要載入包含單選按鈕的 PDF 表單。這 `Aspose.Pdf.Facades.Form` 類別就是用於此目的的。以下是操作方法：

```csharp
// 定義文檔目錄的路徑
string dataDir = "YOUR DOCUMENT DIRECTORY";

// 載入來源 PDF 表單
Aspose.Pdf.Facades.Form form1 = new Aspose.Pdf.Facades.Form(dataDir + "RadioButtonField.pdf");
Document PDF_Template_PDF_HTML = new Document(dataDir + "RadioButtonField.pdf");
```

在此程式碼片段中：
- `dataDir` 指定 PDF 所在的路徑。
- `Form` 類別用於與 PDF 中的表單欄位進行互動。
- `Document` 該類別提供對 PDF 文件頁面的存取。

## 步驟 2：遍歷單選按鈕字段

接下來，您需要遍歷表單中的欄位來識別和操作單選按鈕欄位：

```csharp
foreach (var item in form1.FieldNames)
{
    Console.WriteLine(item.ToString());
    Dictionary<string, string> radioOptions = form1.GetButtonOptionValues(item);
```

在這個循環中：
- `FieldNames` 提供 PDF 中所有欄位名稱的清單。
- `GetButtonOptionValues(item)` 檢索每個單選按鈕可用的選項。

## 步驟 3：修改單選按鈕選項

一旦確定了單選按鈕字段，您就可以修改其選項。為此，您需要將欄位轉換為 `RadioButtonField` 並更新其選項：

```csharp
    if (item.Contains("radio1"))
    {
        Aspose.Pdf.Forms.RadioButtonField field0 = PDF_Template_PDF_HTML.Form[item] as Aspose.Pdf.Forms.RadioButtonField;
        Aspose.Pdf.Forms.RadioButtonOptionField fieldoption = new Aspose.Pdf.Forms.RadioButtonOptionField();
        fieldoption.OptionName = "Yes";
        fieldoption.PartialName = "Yesname";
```

這裡：
- 我們檢查欄位名稱是否包含「radio1」來識別我們要修改的特定單選按鈕欄位。
- `RadioButtonField` 是從表單欄位轉換而來，進行特定的修改。

## 步驟 4：設定單選按鈕的標題

要設定或更新單選按鈕的標題，您需要建立一個 `TextFragment` 並使用 `TextBuilder` 將其放置在所需位置：

```csharp
        var updatedFragment = new Aspose.Pdf.Text.TextFragment("test123");
        updatedFragment.TextState.Font = FontRepository.FindFont("Arial");
        updatedFragment.TextState.FontSize = 10;
        updatedFragment.TextState.LineSpacing = 6.32f;

        // 建立 TextParagraph 對象
        TextParagraph par = new TextParagraph();
        // 設定段落位置
        par.Position = new Position(field0.Rect.LLX, field0.Rect.LLY + updatedFragment.TextState.FontSize);
        // 指定自動換行模式
        par.FormattingOptions.WrapMode = TextFormattingOptions.WordWrapMode.ByWords;
        // 將新的 TextFragment 加入段落
        par.AppendLine(updatedFragment);
        // 使用 TextBuilder 新增 TextParagraph
        TextBuilder textBuilder = new TextBuilder(PDF_Template_PDF_HTML.Pages[1]);
        textBuilder.AppendParagraph(par);
```

在這一部分中：
- `TextFragment` 用於定義文字及其外觀。
- `TextParagraph` 幫助定位和格式化文字。
- `TextBuilder` 將文字新增至 PDF 的指定頁面。

## 步驟5：儲存更新後的PDF

最後，將更新後的 PDF 儲存到新文件：

```csharp
        field0.DeleteOption("item1");
    }
}
PDF_Template_PDF_HTML.Save(dataDir + "RadioButtonField_out.pdf");
```

這將確保：
- 更改已套用至 PDF。
- 依照指定的方式刪除原來的單選按鈕選項。

## 結論

使用 Aspose.PDF for .NET 修改 PDF 表單中的單選按鈕標題可以大幅增強文件的互動性和可用性。透過本教學中概述的步驟，您可以輕鬆載入 PDF、更新單選按鈕選項並儲存變更。這種方法對於表單管理非常方便，並確保您的 PDF 滿足使用者的確切需求。深入研究 Aspose.PDF 並探索其其他 PDF 操作功能！

## 常見問題解答

### 我可以一次更新多個單選按鈕欄位嗎？
是的，您可以遍歷所有單選按鈕欄位並根據需要套用變更。

### 我需要許可證才能使用 Aspose.PDF 嗎？
您可以先免費試用，但長期使用則需要授權。 [在這裡獲得許可證](https://purchase。aspose.com/buy).

### 如何在儲存 PDF 之前測試變更？
您可以在開發環境中預覽 PDF 或使用 PDF 檢視器檢查修改。

### Aspose.PDF 是否與所有版本的 .NET 相容？
Aspose.PDF 支援各種版本的 .NET。確保檢查與特定 .NET 版本的兼容性。

### 我可以類似地操作其他表單欄位嗎？
是的，類似的技術可以應用於 PDF 文件中其他類型的表單欄位。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}