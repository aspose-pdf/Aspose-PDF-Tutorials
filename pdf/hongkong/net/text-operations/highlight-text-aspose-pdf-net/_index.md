---
"date": "2025-04-11"
"description": "透過逐步說明和程式碼範例，了解如何使用 Aspose.PDF .NET 有效地反白顯示 PDF 文件中的文字。"
"title": "如何使用 Aspose.PDF .NET&#58; 反白 PDF 中的文字綜合指南"
"url": "/zh-hant/net/text-operations/highlight-text-aspose-pdf-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 如何使用 Aspose.PDF .NET 高亮 PDF 中的文本

## 介紹
在當今的數位世界中，處理文件是一項日常任務，而且這些文件通常都是 PDF。開發人員面臨的常見挑戰之一是突出顯示這些文件中的文字以提高可讀性或強調性。當處理大量資料且需要突出顯示特定資訊時，這尤其有用。本教學將使用 Aspose.PDF .NET 向您展示如何使用正規表示式有效地搜尋和突出顯示 PDF 文件中的文本，並在找到的文本周圍繪製矩形。

**您將學到什麼：**
- 如何使用 Aspose.PDF .NET 在 PDF 中尋找文字。
- 透過在特定短語或單字周圍繪製矩形來突出顯示它們的技術。
- 配置搜尋選項（例如不區分大小寫）以實現更靈活的文字搜尋。

在深入研究之前，請確保您已具備學習本教程所需的一切。

## 先決條件
首先，您需要：
- **Aspose.PDF for .NET**：該程式庫提供了處理 PDF 所需的功能。確保您使用的版本相容，請檢查其 [官方文檔](https://reference。aspose.com/pdf/net/).
- **開發環境**：Visual Studio 或任何支援 C# 和 .NET 開發的 IDE。
- **基礎知識**：熟悉 C#、.NET 以及在您選擇的環境中處理文件。

## 設定 Aspose.PDF for .NET
首先，讓我們安裝 Aspose.PDF。根據您管理套件的方式，您有多種選擇：

**使用 .NET CLI：**
```bash
dotnet add package Aspose.PDF
```

**使用套件管理器控制台：**
```powershell
Install-Package Aspose.PDF
```

**使用 NuGet 套件管理器 UI：**
- 在 Visual Studio 中開啟您的專案。
- 導航至“工具”>“NuGet 套件管理器”>“管理解決方案的 NuGet 套件...”
- 搜尋“Aspose.PDF”並安裝最新版本。

### 許可證獲取
要使用 Aspose.PDF，您可以先免費試用。參觀他們的 [免費試用頁面](https://releases.aspose.com/pdf/net/) 暫時不受任何限制地下載和測試該庫。如果您認為此工具適合您的長期專案需求，請考慮購買許可證或從他們的 [購買部分](https://purchase。aspose.com/temporary-license/).

## 實施指南
讓我們逐步了解如何使用 Aspose.PDF 實現文字突出顯示功能。

### 功能：搜尋文字並繪製矩形
我們的程式碼的這一部分示範如何使用正規表示式在 PDF 文件中搜尋文字並在其周圍繪製矩形。以下是我們實現這一目標的方法：

#### 開啟文件
首先，將您的 PDF 檔案載入到 `Document` 目的。
```csharp
string dataDir = "YOUR_DOCUMENT_DIRECTORY";
Document document = new Document(dataDir + "SearchAndGetTextFromAll.pdf");
```

#### 使用正規表示式設定文字搜尋
創建一個 `TextFragmentAbsorber` 尋找與指定的正規表示式相符的所有文字。在這裡，我們使用 `[\S]+`，尋找非空白字元序列。
```csharp
TextFragmentAbsorber textAbsorber = new TextFragmentAbsorber(@"[\S]+");
TextSearchOptions textSearchOptions = new TextSearchOptions(true);
textAbsorber.TextSearchOptions = textSearchOptions;
document.Pages.Accept(textAbsorber); 
```
這 `TextSearchOptions` 使用 true 參數會使搜尋不區分大小寫。

#### 在找到的文字周圍繪製一個矩形
接下來循環遍歷每個找到的 `TextFragment`，並在它們周圍繪製矩形。
```csharp
var editor = new PdfContentEditor(document); 

foreach (TextFragment textFragment in textAbsorber.TextFragments)
{
    foreach (TextSegment textSegment in textFragment.Segments)
    {
        DrawBox(editor, textFragment.Page.Number, textSegment, Color.Red);
    }
}
```

#### 儲存文件
最後，將您的變更儲存到新的 PDF 檔案。
```csharp
dataDir = dataDir + "SearchTextAndDrawRectangle_out.pdf";
document.Save(dataDir);
```

### 功能：繪製框
這個輔助函數 `DrawBox` 示範如何在特定文字段周圍繪製多邊形（矩形）。

#### 定義座標並建立多邊形
對於每個 `TextSegment`，定義矩形座標並在指定的PDF頁面上建立多邊形。
```csharp
private static void DrawBox(PdfContentEditor editor, int page, TextSegment segment, Color color)
{
    var lineInfo = new LineInfo();
    lineInfo.VerticeCoordinate = new[] {
        (float)segment.Rectangle.LLX, (float)segment.Rectangle.LLY,
        (float)segment.Rectangle.LLX, (float)segment.Rectangle.URY,
        (float)segment.Rectangle.URX, (float)segment.Rectangle.URY,
        (float)segment.Rectangle.URX, (float)segment.Rectangle.LLY
    };
    lineInfo.Visibility = true;
    lineInfo.LineColor = color;

    editor.CreatePolygon(lineInfo, page, new Rectangle(0, 0, 0, 0), null);
}
```

## 實際應用
在 PDF 中突出顯示文字的功能有多種實際應用：
- **法律文件**：突出顯示需要審查的關鍵條款或術語。
- **教育材料**：強調教科書中的重要概念。
- **數據分析報告**：引起對重要數據點或發現的關注。

將此功能整合到您的文件管理系統中可以使資訊更易於存取和視覺上更清晰，從而增強使用者體驗。

## 性能考慮
處理大型 PDF 檔案時，請考慮以下效能提示：
- 使用更具體的正規表示式來限製文字搜尋的範圍。
- 透過在不再需要時處置物件來優化 .NET 應用程式中的記憶體使用量。
- 使用 Aspose.PDF 內建的方法實現高效率的資源管理。

透過遵循最佳實踐，即使處理大規模 PDF 任務，您也可以確保操作順暢且有效率。

## 結論
在本教程中，我們探討如何使用 Aspose.PDF .NET 透過正規表示式搜尋 PDF 文件中的文字並透過繪製矩形來突出顯示它。此功能對於增強文件的可讀性和使用者互動至關重要。 

為了進一步探索 Aspose.PDF 的功能，請考慮嘗試其他功能，例如合併文件或將其轉換為不同的格式。

## 常見問題部分
**Q：如何確保我的搜尋不區分大小寫？**
答：使用 `TextSearchOptions` 使用 true 參數創建 `TextFragmentAbsorber`。

**Q：我可以不畫矩形就突出顯示 PDF 中的文字嗎？**
答：是的，探索 Aspose.PDF 的註解功能以尋找替代的突出顯示方法。

**Q：如果我突出顯示的部分重疊怎麼辦？**
答：調整正規表示式或對座標進行後處理以避免重疊。

**Q：如何擴充此功能以批次處理多個檔案？**
答：遍歷 PDF 目錄，對每個文件套用相同的邏輯。

**Q：使用 Aspose.PDF 時檔案大小有限制嗎？**
答：雖然 Aspose.PDF 可以很好地處理大型文件，但效能可能會根據系統資源和複雜性而有所不同。

## 資源
- **文件**： [Aspose.PDF for .NET 文檔](https://reference.aspose.com/pdf/net/)
- **下載**： [Aspose.PDF下載](https://releases.aspose.com/pdf/net/)
- **購買**： [購買 Aspose.PDF](https://purchase.aspose.com/buy)
- **免費試用**： [開始免費試用](https://releases.aspose.com/pdf/net/)
- **臨時執照**： [獲得臨時許可證](https://purchase.aspose.com/temporary-license/)
- **支援論壇**： [Aspose 社區支持](https://forum.aspose.com/c/pdf/10)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}