---
"description": "透過使用 Aspose.PDF for .NET 新增單選按鈕來釋放互動式 PDF 的潛力。輕鬆建立引人入勝的表格並改善使用者體驗。"
"linktitle": "帶有選項的單選按鈕"
"second_title": "Aspose.PDF for .NET API參考"
"title": "帶有選項的單選按鈕"
"url": "/zh-hant/net/programming-with-forms/radio-button-with-options/"
"weight": 230
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 帶有選項的單選按鈕

## 介紹

建立互動式 PDF 文件可以顯著增強使用者參與度並簡化資料收集。在您可以納入的各種元素中，單選按鈕作為呈現多項選擇選項的使用者友善方法脫穎而出。使用 Aspose.PDF for .NET，您可以輕鬆地將單選按鈕新增至您的 PDF 表單中，讓使用者輕鬆選擇他們的偏好。無論您正在進行調查、反饋表還是應用程序，本指南都將幫助您利用 Aspose.PDF 的強大功能有效地實現單選按鈕。

## 先決條件

在我們開始之前，您需要設定一些內容以確保我們在建立帶有單選按鈕的 PDF 時一切順利：

1. Aspose.PDF for .NET：請確定您的專案中已安裝了 Aspose.PDF 庫。如果你還沒有，你可以從 [發布頁面](https://releases。aspose.com/pdf/net/).
2. .NET 框架：對 .NET 框架的基本了解將幫助您解決在使用過程中遇到的任何問題。
3. 開發環境：您需要一個適合 .NET 的 IDE（如 Visual Studio），您可以在其中編寫和測試程式碼。
4. 熟悉 C#：雖然您不需要成為專業人士，但掌握 C# 程式設計肯定會使這個過程更輕鬆、更愉快。
5. PDF 結構的基本知識：了解 PDF 的結構有助於進一步排除故障或自訂表單。

一旦您完成所有這些整理，您就可以在 PDF 世界中釋放您的創造力了！

## 導入包

要開始使用 Aspose.PDF 中的單選按鈕，您首先需要將必要的套件匯入到您的 C# 專案中。以下是操作方法：

### 開啟程式碼編輯器

開啟您的開發環境（如 Visual Studio）並建立一個新的 C# 專案（如果您還沒有這樣做）。 

### 新增 Aspose.PDF 參考

在解決方案資源管理器中右鍵單擊您的項目，選擇新增>引用，然後在組件部分中尋找 Aspose.PDF。如果您正確安裝了該庫，它應該會出現在清單中。只需將其勾選並單擊“確定”即可。

```csharp
using System;
using System.IO;
using Aspose.Pdf.Forms;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
```

現在，您的專案已準備好利用 Aspose 的強大功能！

一切設定完畢後，讓我們逐步建立一個充滿單選按鈕的 PDF 文件！

## 步驟 1：設定文檔

首先，讓我們建立一個新的 PDF 文件並在其中新增一個頁面。這將是我們繪製單選按鈕選項的畫布。

```csharp
// 文檔目錄的路徑。
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document();
Page page = doc.Pages.Add();
```

在這個片段中，我們建立了一個新的 `Document` 對象並添加 `Page` 以此作為我們的內容。確保更換 `YOUR DOCUMENT DIRECTORY` 以及您想要儲存 PDF 的路徑。

## 步驟 2：建立佈局表

接下來，我們需要為單選按鈕設計一個佈局。使用表格可以更容易地將它們定位好。

```csharp
Aspose.Pdf.Table table = new Aspose.Pdf.Table();
table.ColumnWidths = "120 120 120"; // 定義列寬
page.Paragraphs.Add(table);
```

在這裡，我們創建了一個 `Table` 物件並指定三列的寬度。這為我們的選項創建了一個整潔的佈局。

## 步驟 3：在表格中新增一行

我們現在將在表格中新增一行以及包含單選按鈕的儲存格。

```csharp
Row r1 = table.Rows.Add();
Cell c1 = r1.Cells.Add();
Cell c2 = r1.Cells.Add();
Cell c3 = r1.Cells.Add();
```

我們建立一個新行並在該行中建立三個儲存格。每個儲存格都會包含一個單選按鈕選項。

## 步驟 4：新增單選按鈕字段

樂趣就從這裡開始——讓我們將單選按鈕欄位添加到我們的 PDF 中！

```csharp
RadioButtonField rf = new RadioButtonField(page);
rf.PartialName = "radio";
doc.Form.Add(rf, 1);
```

我們實例化一個 `RadioButtonField`，設定其名稱，然後將其新增至文件表單。該欄位將允許使用者進行選擇。

## 步驟 5：配置單選按鈕選項

是時候建立單選按鈕的選項了！我們將新增三個選項供用戶選擇。

```csharp
RadioButtonOptionField opt1 = new RadioButtonOptionField();
RadioButtonOptionField opt2 = new RadioButtonOptionField();
RadioButtonOptionField opt3 = new RadioButtonOptionField();
opt1.OptionName = "Item1";
opt2.OptionName = "Item2";
opt3.OptionName = "Item3";
```

在這裡，我們創建三個 `RadioButtonOptionField` 為每個選擇建立實例並為其指派名稱。發揮這些名稱的創意可以幫助更好地引導用戶做出選擇。

## 步驟 6：設定選項尺寸

接下來，讓我們設定單選按鈕選項的大小，使其更具視覺吸引力。

```csharp
opt1.Width = 15;
opt1.Height = 15;
opt2.Width = 15;
opt2.Height = 15;
opt3.Width = 15;
opt3.Height = 15;
```

透過此程式碼，我們定義每個單選按鈕的尺寸。如果您想要更大或更小的選項，您可以調整這些值。

## 步驟 7：為單選按鈕欄位新增選項

現在已經建立了選項，我們需要將它們新增到單選按鈕欄位。

```csharp
rf.Add(opt1);
rf.Add(opt2);
rf.Add(opt3);
```

此程式碼不僅添加了選項，還將它們連結到我們的單選按鈕字段，使用戶能夠選擇其中一個選項。

## 步驟 8：設定選項樣式

為了使我們的選擇脫穎而出，讓我們對它們進行設計。我們可以新增邊框並設定顏色。

```csharp
opt1.Border = new Border(opt1);
opt1.Border.Width = 1;
opt1.Border.Style = BorderStyle.Solid;
opt1.Characteristics.Border = System.Drawing.Color.Black;
opt1.DefaultAppearance.TextColor = System.Drawing.Color.Red;
opt1.Caption = new TextFragment("Item1");
```

重複此造型 `opt2` 和 `opt3`，並相應調整字幕。這確保每個選項看起來都專業且引人入勝。

## 步驟 9：為儲存格新增選項

接下來，我們需要將這些單選按鈕放入表格的對應儲存格中。

```csharp
c1.Paragraphs.Add(opt1);
c2.Paragraphs.Add(opt2);
c3.Paragraphs.Add(opt3);
```

此行將樣式選項新增至我們先前建立的儲存格中，並將它們整齊地組織在我們的表格中。

## 步驟 10：儲存 PDF 文檔

最後，是時候保存您的工作了！此步驟將我們所做的一切提交到 PDF 文件中。

```csharp
dataDir = dataDir + "RadioButtonWithOptions_out.pdf";
// 儲存 PDF 文件
doc.Save(dataDir);
Console.WriteLine("\nRadio button field with three options added successfully.\nFile saved at " + dataDir);
```

使用此程式碼，您的文件將保存在指定的目錄中。現在您可以開啟此 PDF 檔案以查看單選按鈕的實際效果。恭喜您實現了您的第一個互動式 PDF！

## 結論

掌握如何使用 Aspose.PDF for .NET 建立單選按鈕等互動元素將為您的 PDF 文件開啟一個全新的可能性領域。透過遵循本指南，您現在應該能夠毫不費力地將單選按鈕合併到您的專案中，從而增強使用者體驗和資料收集流程。無論是簡單的調查還是複雜的表格，您都可以輕鬆建立客製化的互動式 PDF。

## 常見問題解答

### 什麼是 Aspose.PDF for .NET？
Aspose.PDF for .NET 是一個函式庫，可讓開發人員以程式設計方式建立和操作 PDF 文件。

### 如何安裝 Aspose.PDF for .NET？
您可以從 [Aspose 發佈頁面](https://releases.aspose.com/pdf/net/) 並將其添加到您的項目中。

### 我可以使用其他程式語言在 PDF 中建立單選按鈕嗎？
是的，Aspose.PDF 也適用於 Java 和其他語言，並且具有類似的功能。

### Aspose.PDF 有免費試用版嗎？
是的，您可以透過下載 [免費試用版](https://releases。aspose.com/).

### 我可以在哪裡獲得 Aspose.PDF 的支援？
如需支持，您可以訪問 [Aspose 支援論壇](https://forum.aspose.com/c/pdf/10) 尋求專家和社區成員的協助。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}