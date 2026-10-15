---
title: 使用 Aspose.Pdf for .NET 自訂 PDF 中表格儲存格的背景、邊框與內距
weight: 101
limit:
description: 了解如何使用 Aspose.Pdf for .NET 建立帶有兩欄表格的 PDF，並為每個儲存格套用自訂背景色、邊框與內距。
keywords: [Aspose.Pdf for .NET, style table cells pdf, pdf table cell background, pdf table cell border, pdf cell padding, Aspose PDF table styling]
url: /net/tables-lists/style-table-cells/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: 了解如何使用 Aspose.Pdf for .NET 建立帶有兩欄表格的 PDF，並為每個儲存格套用自訂背景色、邊框與內距。
  headline: 使用 Aspose.Pdf for .NET 自訂 PDF 中表格儲存格的背景、邊框與內距
  type: TechArticle
- description: 了解如何使用 Aspose.Pdf for .NET 建立帶有兩欄表格的 PDF，並為每個儲存格套用自訂背景色、邊框與內距。
  name: 使用 Aspose.Pdf for .NET 自訂 PDF 中表格儲存格的背景、邊框與內距
  steps:
  - name: 在 using 區塊中建立一個新的空白 PDF 文件。
    text: 在 using 區塊中建立一個新的空白 PDF 文件。
  - name: 向 PDF 文件新增一個空白頁面。
    text: 向 PDF 文件新增一個空白頁面。
  - name: 實例化一個 Table 物件，包含兩個寬度為 200 點的欄位、細黑色外框，以及預設儲存格內距 5 點。
    text: 實例化一個 Table 物件，包含兩個寬度為 200 點的欄位、細黑色外框，以及預設儲存格內距 5 點。
  - name: 將第一列加入表格。
    text: 將第一列加入表格。
  - name: 建立第一個儲存格，插入文字「First cell」，設定淡黃色背景、紅色 2 點邊框，以及 4 點邊距。
    text: 建立第一個儲存格，插入文字「First cell」，設定淡黃色背景、紅色 2 點邊框，以及 4 點邊距。
  - name: 建立第二個儲存格，加入文字「Second cell」，設定淡綠色背景、藍色 2 點邊框，以及 4 點邊距。
    text: 建立第二個儲存格，加入文字「Second cell」，設定淡綠色背景、藍色 2 點邊框，以及 4 點邊距。
  - name: 將第二列加入表格。
    text: 將第二列加入表格。
  - name: 建立第三個儲存格，插入「Third cell」，設定淡青色背景、深灰色 2 點邊框，以及 4 點邊距。
    text: 建立第三個儲存格，插入「Third cell」，設定淡青色背景、深灰色 2 點邊框，以及 4 點邊距。
  - name: 建立第四個儲存格，加入「Fourth cell」，設定淡粉色背景、紫色 2 點邊框，以及 4 點邊距。
    text: 建立第四個儲存格，加入「Fourth cell」，設定淡粉色背景、紫色 2 點邊框，以及 4 點邊距。
  - name: 將完整樣式的表格加入頁面，使其在 PDF 中可見。
    text: 將完整樣式的表格加入頁面，使其在 PDF 中可見。
  - name: 將 PDF 文件儲存至檔案，並關閉 using 區塊。
    text: 將 PDF 文件儲存至檔案，並關閉 using 區塊。
  - name: 在主控台印出確認訊息。
    text: 在主控台印出確認訊息。
  type: HowTo
- questions:
  - answer: '`DefaultCellPadding` 為每個儲存格提供基礎內距，但若您指定 `Margin`（例如 `cellA1.Margin =
      new MarginInfo(...)`），該邊距值會覆蓋該儲存格的預設內距。'
    question: 在 `Table` 上設定的 `DefaultCellPadding` 會影響同時定義了 `Margin` 的儲存格嗎？
  - answer: 若未設定 `Table.Border`，整個表格的外框矩形將不會顯示；僅會看到您為各儲存格設定的邊框（例如 `cellA2.Border`）。
    question: 如果我從 `Table` 物件移除 `Border` 屬性，PDF 會是什麼樣子？
  - answer: 可以，建立帶有特定 `BorderSide` 的 `BorderInfo`（例如 `new BorderInfo(BorderSide.Left,
      3, Aspose.Pdf.Color.Black)`），並將其指派給儲存格的 `Border` 屬性。
    question: 我可以為儲存格的每一側設定不同的邊框寬度嗎？
  - answer: 使用 `Row newRow = dataTable.Rows.Add();` 實例化新 `Row`，然後像先前的列一樣向 `newRow.Cells`
      新增儲存格。
    question: 在上述程式碼之後，如何為表格新增第三列？
  type: FAQPage
images:
- /net/tables-lists/style-table-cells/og-image.png
og_title: PDF 表格儲存格樣式 – 背景、邊框、內距
og_description: 使用 Aspose.Pdf for .NET 快速為 PDF 中的表格儲存格套用自訂顏色、邊框與間距。
og_image_alt: 指南說明如何使用 Aspose.Pdf for .NET 為 PDF 中的表格儲存格設定背景色、邊框與內距
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Pdf for .NET 自訂 PDF 中表格儲存格的背景、邊框與內距
在本教學中，您將看到如何產生 PDF 文件、加入兩欄表格，並精確控制每個儲存格的外觀。透過設定背景色、定義邊框與調整內距，您可以讓表格資料更突出且更具質感。範例使用 Aspose.Pdf Document 與 Table 類別示範各種樣式設定。

---

{{< tutorial-widget sourcePath="pdf/net/tables-lists/style-table-cells" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: 在 `Table` 上設定的 `DefaultCellPadding` 會影響同時定義了 `Margin` 的儲存格嗎？**  
A: `DefaultCellPadding` 為每個儲存格提供基礎內距，但若您指定 `Margin`（例如 `cellA1.Margin = new MarginInfo(...)`），該邊距值會覆蓋該儲存格的預設內距。

**Q: 如果我從 `Table` 物件移除 `Border` 屬性，PDF 會是什麼樣子？**  
A: 若未設定 `Table.Border`，整個表格的外框矩形將不會顯示；僅會看到您為各儲存格設定的邊框（例如 `cellA2.Border`）。

**Q: 我可以為儲存格的每一側設定不同的邊框寬度嗎？**  
A: 可以，建立帶有特定 `BorderSide` 的 `BorderInfo`（例如 `new BorderInfo(BorderSide.Left, 3, Aspose.Pdf.Color.Black)`），並將其指派給儲存格的 `Border` 屬性。

**Q: 在上述程式碼之後，如何為表格新增第三列？**  
A: 使用 `Row newRow = dataTable.Rows.Add();` 實例化新 `Row`，然後像先前的列一樣向 `newRow.Cells` 新增儲存格。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}