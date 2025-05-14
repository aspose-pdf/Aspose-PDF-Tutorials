---
"description": "透過本逐步教學了解如何使用 Aspose.PDF for .NET 在 PDF 文件中建立分組複選框（單選按鈕）。"
"linktitle": "PDF 文件中的分組複選框"
"second_title": "Aspose.PDF for .NET API參考"
"title": "PDF 文件中的分組複選框"
"url": "/zh-hant/net/programming-with-forms/grouped-check-boxes/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF 文件中的分組複選框

## 介紹

建立互動式 PDF 並不像聽起來那麼困難，特別是當您擁有像 Aspose.PDF for .NET 這樣的強大工具時。您可能需要新增至 PDF 文件的互動元素之一是分組複選框，或者更具體地說，是允許使用者從一組選項中選擇一個選項的單選按鈕。本教學將引導您完成使用 Aspose.PDF for .NET 為 PDF 文件新增分組複選框（單選按鈕）的過程。無論您是初學者還是經驗豐富的開發人員，您都會發現本指南引人入勝、內容詳細且易於遵循。

## 先決條件

在深入了解逐步指南之前，讓我們先介紹一些必要的先決條件：

1. Aspose.PDF for .NET：請確定您已安裝 Aspose.PDF 庫。如果沒有，你可以 [點此下載](https://releases。aspose.com/pdf/net/).
2. IDE：您應該設定一個開發環境，例如 Visual Studio。
3. .NET Framework：此專案應針對與 Aspose.PDF 相容的 .NET Framework 版本。
4. 基本 C# 知識：需要熟悉 C# 和 PDF 操作才能順利跟進。
5. 許可證：Aspose.PDF 需要許可證才能實現全部功能。你可以 [取得臨時執照](https://purchase.aspose.com/temporary-license/) 如果需要的話。

## 導入包

在開始之前，請確保已將必要的命名空間匯入到專案中：

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Forms;
```

這些套件將使您能夠存取操作 PDF 文件所需的所有類別和方法，包括建立單選按鈕和定義其屬性。

在本節中，我們將建立分組複選框（單選按鈕）的過程分解為清晰、易於遵循的步驟。

## 步驟 1：建立新的 PDF 文檔

第一步是創建 `Document` 對象，它將代表您的 PDF 文件。然後，在文件中新增一個空白頁，用於放置分組複選框。

```csharp
// 實例化 Document 對象
Document pdfDocument = new Document();

// 在 PDF 文件中新增頁面
Page page = pdfDocument.Pages.Add();
```

這為為 PDF 添加任何元素（例如單選按鈕）奠定了基礎。

## 步驟 2：初始化單選按鈕字段

接下來，我們需要建立一個 `RadioButtonField` 對象，它將保存分組的複選框（單選按鈕）。此欄位被加入到複選框出現的特定頁面。

```csharp
// 實例化 RadioButtonField 物件並將其分配給第一頁
RadioButtonField radio = new RadioButtonField(pdfDocument.Pages[1]);
```

將其視為將各個單選按鈕選項組合在一起的容器。

## 步驟 3：新增單選按鈕選項

現在，讓我們將單獨的單選按鈕選項新增到該欄位。在此範例中，我們將新增兩個單選按鈕並使用 `Rectangle` 目的。

```csharp
// 新增第一個單選按鈕選項並使用矩形指定其位置
RadioButtonOptionField opt1 = new RadioButtonOptionField(page, new Aspose.Pdf.Rectangle(0, 0, 20, 20));
RadioButtonOptionField opt2 = new RadioButtonOptionField(page, new Aspose.Pdf.Rectangle(100, 0, 120, 20));

// 設定選項名稱以便識別
opt1.OptionName = "Option1";
opt2.OptionName = "Option2";
```

在這裡， `Rectangle` 物件定義頁面上每個單選按鈕的座標和大小。

## 步驟 4：自訂單選按鈕的樣式

您可以透過設定單選按鈕的 `Style` 財產。例如，您可能需要方形複選框或十字形複選框。

```csharp
// 設定單選按鈕的樣式
opt1.Style = BoxStyle.Square;
opt2.Style = BoxStyle.Cross;
```

這使您可以控制複選框的外觀和感覺，使它們更加用戶友好且更具視覺吸引力。

## 步驟5：配置邊框屬性

邊框在使復選框易於識別方面起著至關重要的作用。在這裡，我們將在每個單選按鈕選項周圍添加實線邊框並定義它們的寬度和顏色。

```csharp
// 配置第一個單選按鈕的邊框
opt1.Border = new Border(opt1);
opt1.Border.Style = BorderStyle.Solid;
opt1.Border.Width = 1;
opt1.Characteristics.Border = Color.Black;

// 配置第二個單選按鈕的邊框
opt2.Border = new Border(opt2);
opt2.Border.Style = BorderStyle.Solid;
opt2.Border.Width = 1;
opt2.Characteristics.Border = Color.Black;
```

此步驟可確保每個單選按鈕都有明確的邊框，從而提高文件的可讀性。

## 步驟 6：為表單新增單選按鈕選項

現在，我們將單選按鈕新增到文件的表單中。這是將複選框分組到單一欄位下的最後一步。

```csharp
// 將單選按鈕欄位新增至文件的表單對象
pdfDocument.Form.Add(radio);
```

表單物件充當所有互動元素的容器，包括我們的分組複選框。

## 步驟 7：儲存 PDF 文檔

最後，一切設定完成後，您可以將 PDF 文件儲存到所需的位置。

```csharp
// 定義輸出檔案路徑
string dataDir = "YOUR DOCUMENT DIRECTORY" + "GroupedCheckBoxes_out.pdf";

// 儲存 PDF 文件
pdfDocument.Save(dataDir);

// 確認創建成功
Console.WriteLine("Grouped checkboxes added successfully. File saved at " + dataDir);
```

就是這樣！您已成功使用 Aspose.PDF for .NET 建立了具有分組複選框的 PDF。

## 結論

在 PDF 文件中添加諸如分組複選框之類的交互元素一開始可能看起來很棘手，但使用 Aspose.PDF for .NET，這變得輕而易舉。透過遵循本逐步指南，您將了解如何設定基本的 PDF 文件、新增分組單選按鈕、自訂其外觀以及儲存最終結果。無論您是建立表單、調查或任何其他類型的互動式 PDF，本指南都能為您提供堅實的基礎。

## 常見問題解答

### 我可以為一個群組中新增兩個以上的單選按鈕嗎？
絕對地！只需實例化附加 `RadioButtonOptionField` 對象並將它們添加到 `RadioButtonField` 如教程所示。

### 如何處理一個文件中的多組複選框？
若要建立多個群組，請實例化單獨的 `RadioButtonField` 每個組別的物件。

### 我可以添加的複選框數量有限制嗎？
不，Aspose.PDF for .NET 對您可以新增到 PDF 的複選框數量沒有任何限制。

### 添加複選框後我可以更改其外觀嗎？
是的，新增複選框後，您可以修改邊框樣式、寬度和顏色等屬性。

### 可以使用圖像作為單選按鈕嗎？
是的，Aspose.PDF 允許您使用自訂圖像作為單選按鈕，只需設定 `Appearance` 每個單選按鈕選項的屬性。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}