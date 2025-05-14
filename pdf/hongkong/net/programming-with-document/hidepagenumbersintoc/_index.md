---
"description": "了解如何使用 Aspose.PDF for .NET 隱藏目錄中的頁碼。依照包含程式碼範例的詳細指南來建立專業的 PDF。"
"linktitle": "隱藏目錄中的頁碼"
"second_title": "Aspose.PDF for .NET API參考"
"title": "隱藏目錄中的頁碼"
"url": "/zh-hant/net/programming-with-document/hidepagenumbersintoc/"
"weight": 220
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 隱藏目錄中的頁碼

## 介紹

當您處理 PDF 時，有時您可能想要產生目錄 (TOC)，但透過隱藏頁碼來保持內容的簡潔。也許沒有它們文件會運行得更好，也許這是一種美學選擇。無論出於何種原因，如果您使用 Aspose.PDF for .NET，本教學將向您展示如何在目錄中隱藏頁碼。

## 先決條件

在我們開始之前，您需要準備好一些東西。以下是一份快速清單：

- 已安裝 Visual Studio：您需要一個可運行的 Visual Studio 版本來編寫程式碼。
- Aspose.PDF for .NET 函式庫：請確定您已經安裝了 Aspose.PDF for .NET 函式庫。
  - 下載連結： [Aspose.PDF for .NET](https://releases.aspose.com/pdf/net/)
- 臨時許可證：如果您正在測試這些功能，那麼擁有臨時許可證會很有幫助。
  - 臨時執照： [在這裡獲取](https://purchase.aspose.com/temporary-license/)

## 導入包

在進入程式碼之前，請確保在 C# 專案中匯入以下命名空間。這些將提供處理 PDF 文件和建立目錄 (TOC) 所需的類別和方法。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

現在您的環境已經準備就緒並且套件已匯入，讓我們分解流程的每個步驟。我們將涵蓋代碼的每個部分以確保清晰度，以便您可以輕鬆跟進。

## 步驟 1：初始化您的 PDF 文檔

我們需要做的第一件事是建立一個新的 PDF 文件並新增一個目錄 (TOC) 頁面。


```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "HiddenPageNumbers_out.pdf";
Document doc = new Document();
Page tocPage = doc.Pages.Add();
```

- dataDir：這是保存輸出檔的目錄。
- Document()：初始化一個新的PDF文件。
- Pages.Add()：在文件中新增一個新的空白頁，該頁面稍後將儲存您的目錄。

## 第 2 步：設定目錄資訊和標題

接下來，我們將定義目錄訊息，包括設定將顯示在目錄頂部的標題。

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocPage.TocInfo = tocInfo;
```

- TocInfo：此物件保存有關 TOC 的所有資訊。
- TextFragment：代表TOC標題的文本，這裡我們將其設定為「Table Of Contents」。
- FontStyle：我們將 TOC 標題的大小設為 20 並將其設為粗體，以設定其樣式。
- tocPage.TocInfo：我們將目錄資訊指派給將顯示目錄的頁面。

## 步驟 3：隱藏目錄中的頁碼

現在到了有趣的部分！在這裡我們配置目錄以隱藏頁碼。

```csharp
tocInfo.IsShowPageNumbers = false;
tocInfo.FormatArrayLength = 4;
```

- IsShowPageNumbers：這是隱藏頁碼的神奇開關。將其設定為 `false`，且頁碼不會出現在目錄中。
- FormatArrayLength：我們將其設為 4，表示我們要為四個層級的 TOC 標題定義格式。

## 步驟 4：自訂目錄格式

為了在您的目錄中添加更多樣式，我們現在將為不同等級的標題定義格式。

```csharp
tocInfo.FormatArray[0].Margin.Right = 0;
tocInfo.FormatArray[0].TextState.FontStyle = FontStyles.Bold | FontStyles.Italic;
tocInfo.FormatArray[1].Margin.Left = 30;
tocInfo.FormatArray[1].TextState.Underline = true;
tocInfo.FormatArray[1].TextState.FontSize = 10;
tocInfo.FormatArray[2].TextState.FontStyle = FontStyles.Bold;
tocInfo.FormatArray[3].TextState.FontStyle = FontStyles.Bold;
```

- FormatArray：此陣列控制 TOC 項目的格式。每個索引代表不同的標題層級。
- 邊距和文字樣式：我們為每個標題等級設定邊距並套用粗體、斜體和底線等字體樣式。

## 步驟 5：為文件新增標題

最後，讓我們添加將成為目錄一部分的實際標題。

```csharp
Page page = doc.Pages.Add();
for (int Level = 1; Level != 5; Level++)
{ 
    Heading heading2 = new Heading(Level); 
    TextSegment segment2 = new TextSegment(); 
    heading2.TocPage = tocPage; 
    heading2.Segments.Add(segment2); 
    heading2.IsAutoSequence = true; 
    segment2.Text = "this is heading of level " + Level; 
    heading2.IsInList = true; 
    page.Paragraphs.Add(heading2); 
}
```

- 標題和文字段：這些代表將出現在目錄中的標題。每個關卡都有自己的標題。
- IsAutoSequence：自動對標題進行編號。
- IsInList：確保每個標題都出現在目錄中。

## 步驟6：儲存文檔

一切設定完成後，將 PDF 文件儲存到指定的輸出檔案。

```csharp
doc.Save(outFile);
```

就是這樣！您已成功建立帶有目錄的 PDF，並且頁碼已被隱藏！

## 結論

在 PDF 中建立目錄並隱藏頁碼可能看起來很棘手，但使用 Aspose.PDF for .NET，這一切都變得輕而易舉。透過遵循本逐步指南，您將了解如何自訂目錄格式、隱藏頁碼以及對標題套用不同的樣式。現在您可以建立根據您的確切需求量身定制的專業 PDF。

## 常見問題解答

### 我可以顯示目錄中特定標題的頁碼嗎？
不，Aspose.PDF 隱藏或顯示整個目錄的頁碼。您無法選擇性地隱藏特定條目。

### 是否可以為 TOC 增加更多等級？
是的，你可以增加 `FormatArrayLength` 定義更多層級的 TOC 標題。

### 如何更改所有目錄條目的字型？
您可以透過修改 `TextState.Font` 每個等級的屬性 `FormatArray`。

### 我可以在目錄中插入超連結嗎？
是的，您可以使用 `Heading.TocPage` 財產。

### 我需要 Aspose.PDF 的授權嗎？
是的，生產使用需要有效的許可證。您可以獲得臨時駕照 [這裡](https://purchase.aspose.com/temporary-license/) 測試功能。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}