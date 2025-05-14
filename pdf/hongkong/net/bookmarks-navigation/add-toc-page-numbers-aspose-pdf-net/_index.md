---
"date": "2025-04-11"
"description": "了解如何使用 Aspose.PDF for .NET 在 PDF 文件中有效地新增和自訂帶有頁碼的目錄，從而增強文件導航。"
"title": "如何使用 Aspose.PDF .NET 在 PDF 中新增帶有頁碼的目錄"
"url": "/zh-hant/net/bookmarks-navigation/add-toc-page-numbers-aspose-pdf-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 如何使用 Aspose.PDF .NET 在 PDF 中新增帶有頁碼的目錄

## 介紹

在當今數位時代，有效瀏覽長篇文件至關重要。無論您處理的是報告、手冊還是學術論文，擁有組織良好的目錄 (TOC) 都可以顯著提高可用性。本指南示範如何使用 Aspose.PDF for .NET（一個專為 .NET 應用程式中的 PDF 操作而設計的強大函式庫）在 PDF 檔案中新增和自訂帶有頁碼的目錄。

**您將學到什麼：**
- 設定 Aspose.PDF for .NET
- 將現有的 PDF 文件載入到您的應用程式中
- 建立並自訂帶有頁碼的目錄
- 儲存修改後的 PDF 文件

準備好簡化您的文件管理了嗎？讓我們開始吧！

### 先決條件

在繼續之前，請確保您已：
- **庫和依賴項**：您的專案包含 Aspose.PDF for .NET。
- **環境設定**：.NET 開發環境（例如 Visual Studio）。
- **知識前提**：對 C# 和 .NET 應用程式中的文件處理有基本的了解。

### 設定 Aspose.PDF for .NET

#### 安裝
首先，使用以下方法之一將 Aspose.PDF 庫新增至您的專案：

**.NET CLI：**
```bash
dotnet add package Aspose.PDF
```

**套件管理器：**
```powershell
Install-Package Aspose.PDF
```

**NuGet 套件管理器 UI：**
搜尋“Aspose.PDF”並安裝最新版本。

#### 許可證獲取
您可以從免費試用開始探索 Aspose.PDF 的功能。如需延長使用時間，請考慮取得臨時許可證或購買許可證。訪問 [Aspose 購買](https://purchase.aspose.com/buy) 有關獲取許可證的更多詳細資訊。

### 實施指南

一切設定完成後，讓我們在您的 PDF 文件中添加帶有頁碼的自訂目錄。

#### 載入和修改 PDF 文檔
首先，將現有的 PDF 文件載入到您的應用程式中。然後，我們將在此文件的開頭插入一個新頁面作為目錄。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

string inFile = "YOUR_DOCUMENT_DIRECTORY/42824.pdf";
string outFile = "YOUR_OUTPUT_DIRECTORY/42824_out.pdf";

// 載入 PDF 文件
document doc = new Document(inFile);

// 在目錄開頭插入新頁
Aspose.Pdf.Page tocPage = doc.Pages.Insert(1);
```

#### 建立和配置目錄訊息
接下來，透過設定標題、字體大小、樣式和前綴頁碼來配置目錄。

```csharp
// 設定目錄資訊
tocInfo tocInfo = new TocInfo();
textFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20; // 目錄標題的字體大小
title.TextState.FontStyle = FontStyles.Bold; // 加粗樣式以示強調
tocInfo.Title = title;
tocInfo.PageNumbersPrefix = "P"; // 在頁碼前面加上「P」前綴
tocPage.TocInfo = tocInfo; // 將目錄資訊指派給新頁面
```

#### 向目錄新增條目
現在，用文件中每一頁的條目填入目錄。

```csharp
for (int i = 1; i < doc.Pages.Count; i++) {
    Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
textSegment segment2 = new textSegment();

    // 將標題連結到目錄頁面
    heading2.TocPage = tocPage;

    // 將文字片段新增至標題
    heading2.Segments.Add(segment2); 

    // 為每個條目設定目標頁面和位置
    heading2.DestinationPage = doc.Pages[i + 1];
    heading2.Top = doc.Pages[i + 1].Rect.Height; 
    segment2.Text = "P" + i.ToString(); // 帶有前綴“P”的自訂文本

    // 將標題新增至目錄頁面
    tocPage.Paragraphs.Add(heading2);
}
```

#### 儲存修改後的 PDF 文檔
最後，使用新新增的目錄儲存修改後的文件。

```csharp
doc.Save(outFile);
```

### 實際應用

新增自訂目錄可以顯著增強各種場景下的文件導航：
1. **學術論文**：快速存取長篇研究文件的不同部分。
2. **使用者手冊**：透過允許快速跳到特定說明或主題來改善使用者體驗。
3. **報告和提案**：方便在演示或評論期間輕鬆參考。

### 性能考慮

處理大型 PDF 檔案時，請考慮以下事項以獲得最佳效能：
- **高效率的記憶體管理**：使用後及時處理物品以釋放資源。
- **批次處理**：如果可能的話，分批處理多個文件以簡化處理任務。
- **非同步操作**：在適用的情況下使用非同步方法來避免阻塞操作。

### 結論

在本教學中，您學習如何使用 Aspose.PDF for .NET 新增帶有頁碼的自訂目錄來增強 PDF 文件。此功能不僅改善了文件導航，而且還增強了整體使用者體驗。

為了進一步探索 Aspose.PDF for .NET 的功能，請在熟悉基礎知識後考慮深入研究更複雜的功能和整合。

### 常見問題部分

**1. 我可以進一步自訂目錄的外觀嗎？**
是的，您可以調整字體樣式、顏色，甚至使用自訂編號格式來自訂目錄的外觀。

**2. 如果我的 PDF 已有書籤怎麼辦？**
提供的程式碼重點是新增目錄，但您可以透過相應地修改目標設定將其與現有書籤整合。

**3. 如何處理加密或密碼保護的 PDF？**
在處理此類文件之前，請使用 Aspose.PDF 的解密方法解鎖它們以進行編輯。

**4. 這種方法適合大量處理多個文件嗎？**
絕對地！您可以循環遍歷 PDF 目錄並有效地將相同的邏輯套用至每個文件。

**5. 我可以將此功能整合到 Web 應用程式中嗎？**
是的，Aspose.PDF for .NET 在 ASP.NET 等 Web 環境中運作良好，讓您可以即時處理 PDF。

### 資源
- **文件**： [Aspose.PDF for .NET 文檔](https://reference.aspose.com/pdf/net/)
- **下載**： [Aspose.PDF for .NET 最新版本](https://releases.aspose.com/pdf/net/)
- **購買**： [購買許可證](https://purchase.aspose.com/buy)
- **免費試用**： [從免費試用開始](https://releases.aspose.com/pdf/net/)
- **臨時執照**： [獲得臨時許可證](https://purchase.aspose.com/temporary-license/)
- **支援論壇**： [加入Aspose社區](https://forum.aspose.com/c/pdf/10)

我們希望本指南有助於增強您的 PDF 文件管理能力。編碼愉快！


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}