---
"description": "透過本全面的逐步指南了解如何使用 Aspose.PDF for .NET 在 PDF 中刪除單字。提升您的文檔編輯技能。"
"linktitle": "刪除單字"
"second_title": "Aspose.PDF for .NET API參考"
"title": "刪除單字"
"url": "/zh-hant/net/annotations/strikeoutwords/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 刪除單字

## 介紹

您是否發現自己需要透過刪除 PDF 中的特定文字來強調它？無論您是在審閱文件、標記文本，還是僅僅需要突出顯示某些部分，刪除單字都是有用的工具。在本教學中，我們將探討如何使用 Aspose.PDF for .NET 來實現這一點。本綜合指南將引導您完成每個步驟，確保您擁有在 .NET 應用程式中有效實現此功能所需的所有資訊。 

## 先決條件

在我們進入程式碼之前，您需要滿足一些先決條件才能繼續本教學：

1. Aspose.PDF for .NET 程式庫：請確定您已安裝 Aspose.PDF for .NET 程式庫。你可以 [點此下載](https://releases。aspose.com/pdf/net/).

2. .NET Framework：確保您的機器上安裝了 .NET Framework。本教程專為 .NET 應用程式而設計。

3. 開發環境：您需要一個像 Visual Studio 這樣的 IDE 來編寫和執行您的程式碼。

4. PDF 文件：準備好您想要使用的範例 PDF 文件。我們將在該文件中劃掉其中的文字。

5. 基本 C# 知識：熟悉 C# 程式設計對於理解和實作本教程中的步驟是必要的。

## 導入包

在開始編碼之前，我們需要在 .NET 專案中匯入必要的命名空間。這將使我們能夠存取使用 Aspose.PDF 操作 PDF 文件所需的類別和方法。

```csharp
using System;
using System.IO;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
```

這些命名空間對於處理 PDF 文件、處理文字以及添加刪除線等註釋至關重要。

在本節中，我們將把在 PDF 文件中刪除單字的過程分解為簡單、易於管理的步驟。每個步驟都會附有詳細的解釋，以確保您了解一切的工作原理。

## 步驟 1：載入 PDF 文檔

第一步是載入您想要編輯的 PDF 文件。您將在該文件中劃掉特定的單字或片語。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";

// 開啟 PDF 文檔
Document document = new Document(dataDir + "input.pdf");
```

- `dataDir`：此變數保存您的文件目錄的路徑。代替 `"YOUR DOCUMENT DIRECTORY"` 與您的 PDF 檔案所在的實際路徑。
- `Document`： 這 `Document` 類別代表一個 PDF 文件。透過將文件路徑傳遞給其建構函數，我們打開 PDF 文件進行處理。

## 步驟 2：建立 TextFragment 吸收器來尋找特定文本

接下來，我們將創建一個 `TextFragmentAbsorber` 在 PDF 文件中搜尋特定的文字片段。這使我們能夠找到想要刪除的文字。

```csharp
// 建立 TextFragment Absorber 實例來搜尋特定的文字片段
Aspose.Pdf.Text.TextFragmentAbsorber textFragmentAbsorber = new Aspose.Pdf.Text.TextFragmentAbsorber("Estoque");
```

- `TextFragmentAbsorber`：此類用於尋找和處理 PDF 文件中的特定文字片段。在這個例子中，我們搜尋單字「Estoque」。將“Estoque”替換為您要在文件中尋找的單字或短語。

## 步驟 3：遍歷 PDF 文件的各個頁面

現在我們有了 `TextFragmentAbsorber`，我們需要遍歷PDF文件的每一頁來尋找指定的文字。

```csharp
// 遍歷 PDF 文件的頁面
for (int i = 1; i <= document.Pages.Count; i++)
{
    // 取得PDF文件的當前頁面
    Page page = document.Pages[i];
    page.Accept(textFragmentAbsorber);
}
```

- `for (int i = 1; i <= document.Pages.Count; i++)`：此循環遍歷 PDF 文件的每一頁。
- `document.Pages[i]`：檢索目前正在處理的頁面。
- `page.Accept(textFragmentAbsorber)`：此方法適用於 `TextFragmentAbsorber` 到目前頁面，搜尋指定的文字。

## 步驟4：收集並處理文字片段

遍歷完所有頁面後，我們將收集找到的文字片段並準備進行進一步處理。

```csharp
// 建立吸收的文字片段的集合
Aspose.Pdf.Text.TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- `TextFragmentCollection`：此集合儲存在文件中找到的所有文字片段。下一步我們將使用此集合來刪除文字。

## 步驟 5：遍歷文字片段並將其刪除

在此步驟中，我們將循環遍歷集合中的每個文字片段並對其應用刪除線註釋。

```csharp
// 迭代文字片段的集合
for (int j = 1; j <= textFragmentCollection.Count; j++)
{
	Aspose.Pdf.Text.TextFragment textFragment = textFragmentCollection[j];

    // 取得 TextFragment 物件的矩形尺寸
    Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(
        (float)textFragment.Position.XIndent,
        (float)textFragment.Position.YIndent,
        (float)textFragment.Position.XIndent + (float)textFragment.Rectangle.Width,
        (float)textFragment.Position.YIndent + (float)textFragment.Rectangle.Height);

    // 實例化 StrikeOut Annotation 實例
    StrikeOutAnnotation strikeOut = new StrikeOutAnnotation(textFragment.Page, rect);

    // 設定刪除線註釋的屬性
    strikeOut.Opacity = .80f;
    strikeOut.Border = new Border(strikeOut);
    strikeOut.Color = Aspose.Pdf.Color.Red;

    // 將註釋加入到文字片段頁面的註釋集合中
    textFragment.Page.Annotations.Add(strikeOut);
}
```

- `TextFragment textFragment = textFragmentCollection[j]`：此行檢索目前文字片段。
- `Aspose.Pdf.Rectangle`：我們計算文字片段的矩形尺寸來決定在何處套用刪除線。
- `StrikeOutAnnotation`：此類代表刪除線註釋。我們用計算出的矩形和目前頁面來實例化它。
- `strikeOut.Opacity`：此屬性設定刪除線的不透明度，使其可見度達到 80%。
- `strikeOut.Color`：我們將刪除線的顏色設定為紅色。您可以將其變更為您喜歡的任何顏色。
- `textFragment.Page.Annotations.Add(strikeOut)`：這會將刪除線註解新增至頁面。

## 步驟6：儲存修改後的PDF文檔

最後一步是儲存已修改並套用刪除線的 PDF 文件。

```csharp
// 儲存更新的 PDF 文檔
dataDir = dataDir + "StrikeOutWords_out.pdf";
document.Save(dataDir);
```

- `dataDir + "StrikeOutWords_out.pdf"`：這將為修改後的文件建立一個新的檔案名稱。原始文件保持不變。
- `document.Save(dataDir)`：將帶有刪除線的 PDF 文件儲存到指定位置。

## 結論

恭喜！您已成功使用 Aspose.PDF for .NET 刪除 PDF 文件中的特定單字。透過遵循本逐步指南，您現在可以透過突出顯示或刪除文字來自訂 PDF 文檔，使其更具動態性並更適合您的需求。無論您是在註釋法律文件、準備報告或僅標記文字以供審閱，本教學都將為您提供高效完成這些工作的技能。

## 常見問題解答

### 我可以改變刪除線的顏色嗎？

是的，你可以透過修改 `strikeOut.Color` 財產。例如，您可以將其設定為 `Aspose.Pdf.Color.Blue` 為藍色三振出局。

### 可以一次刪除多個單字嗎？

絕對地！這 `TextFragmentAbsorber` 可用於搜尋文件中的任何單字或短語。您可以透過迭代將刪除線套用至多個實例 `TextFragmentCollection`。

### 如果我只想刪除特定頁面上的文字怎麼辦？

您可以修改遍歷頁面的循環，使其僅包含您想要修改的頁面。例如， `for (int i = 1; i <= 3; i++)` 僅對前三頁套用刪除線。

### 如何調整刪除線的粗細？

您可以透過修改 `Border` 的財產 `StrikeOutAnnotation`。這允許自訂刪除線的外觀。

### 儲存文件後，有沒有辦法撤銷刪除線？

一旦文件被保存，刪除線就是永久性的。如果您需要保留不含刪除線的原始文本，請考慮在套用任何修改之前儲存原始文件的備份。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}