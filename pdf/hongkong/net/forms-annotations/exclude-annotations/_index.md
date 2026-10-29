---
title: 使用 Aspose.Pdf for .NET 進行排除註解的並排 PDF 比較
weight: 101
limit:
description: 使用 Aspose.Pdf for .NET 比較 PDF 並排除註解區域的逐步指南。
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: 使用 Aspose.Pdf for .NET 比較 PDF 並排除註解區域的逐步指南。
  headline: 使用 Aspose.Pdf for .NET 進行排除註解的並排 PDF 比較
  type: TechArticle
- description: 使用 Aspose.Pdf for .NET 比較 PDF 並排除註解區域的逐步指南。
  name: 使用 Aspose.Pdf for .NET 進行排除註解的並排 PDF 比較
  steps:
  - name: 定義主要 PDF、次要 PDF 以及輸出差異 PDF 的檔案路徑。
    text: 定義主要 PDF、次要 PDF 以及輸出差異 PDF 的檔案路徑。
  - name: 檢查兩個輸入 PDF 檔案是否皆存在，若任一缺失則以錯誤訊息中止。
    text: 檢查兩個輸入 PDF 檔案是否皆存在，若任一缺失則以錯誤訊息中止。
  - name: 在 using 區塊中將兩個 PDF 檔案以 Document 物件（pdfA 與 pdfB）開啟，使其自動釋放資源。
    text: 在 using 區塊中將兩個 PDF 檔案以 Document 物件（pdfA 與 pdfB）開啟，使其自動釋放資源。
  - name: 收集 pdfA 中每個註解的邊界矩形，並存入 ignoredRectsA。
    text: 收集 pdfA 中每個註解的邊界矩形，並存入 ignoredRectsA。
  - name: 收集 pdfB 中每個註解的邊界矩形，並存入 ignoredRectsB。
    text: 收集 pdfB 中每個註解的邊界矩形，並存入 ignoredRectsB。
  - name: 建立 SideBySideComparisonOptions 物件，並將先前收集的註解矩形分別指派給 ExcludeAreas1 與 ExcludeAreas2，使比較時忽略這些區域。
    text: 建立 SideBySideComparisonOptions 物件，並將先前收集的註解矩形分別指派給 ExcludeAreas1 與 ExcludeAreas2，使比較時忽略這些區域。
  - name: 使用兩個 Document 物件與已設定的選項執行並排 PDF 比較，並將結果寫入 outputPdf。
    text: 使用兩個 Document 物件與已設定的選項執行並排 PDF 比較，並將結果寫入 outputPdf。
  - name: 釋放 Document 物件並結束 using 區塊。
    text: 釋放 Document 物件並結束 using 區塊。
  - name: 印出確認訊息，指出比較已完成以及差異 PDF 的儲存位置。
    text: 印出確認訊息，指出比較已完成以及差異 PDF 的儲存位置。
  type: HowTo
- questions:
  - answer: 會。程式碼只是不會向相應的 `ignoredRects` 清單加入矩形，因此 `ExcludeAreas1`/`ExcludeAreas2`
      會收到空陣列，比較器會處理整個頁面。
    question: 如果 PDF 頁面沒有任何註解，會發生什麼情況——比較仍會正常運作嗎？
  - answer: 將 `ExcludeAreas1`（或 `ExcludeAreas2`）設定為收集到的矩形，並將另一屬性保留為空陣列；比較器只會在指定的文件中忽略這些區域。
    question: 我能只排除其中一個文件的註解，而在差異中保留另一個文件的註解嗎？
  - answer: 比較器會在內部合併重疊的矩形，因而安全地排除重疊的註解範圍，不會重複計算。
    question: 重疊的註解矩形會對 `ExcludeAreas` 造成任何問題嗎？
  - answer: 可以，將 `compareOpts.ExcludeTables = true;` 設為 true——此旗標會與 `ExcludeAreas1`/`ExcludeAreas2`
      一起作用，亦可排除表格區域。
    question: 是否可以使用相同的選項物件，同時排除表格與註解？
  - answer: 程式碼在加入清單前會檢查 `if (a != null && a.Rect != null)`，因此會直接跳過 null 矩形，不會拋出例外。
    question: 如果註解的 `Rect` 屬性為 null，程式碼會拋出例外嗎？
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: 比較不含註解的 PDF
og_description: 執行跳過所有註解標記的並排 PDF 差異比較。
og_image_alt: 說明使用 Aspose.Pdf for .NET 進行排除註解區域的並排 PDF 比較的指南。
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Pdf for .NET 進行排除註解的並排 PDF 比較
本教學說明如何使用 Aspose.Pdf for .NET 比較兩個 PDF 檔案，同時忽略所有註解內容。它會從每個文件擷取所有註解的邊界框，將這些區域傳入 SideBySideComparisonOptions，然後執行並排比較。最終產生的差異 PDF 僅標示非註解的變更。

---

{{< tutorial-widget sourcePath="pdf/net/forms-annotations/exclude-annotations" >}}


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

**Q: 如果 PDF 頁面沒有任何註解，會發生什麼情況——比較仍會正常運作嗎？**  
A: 會。程式碼只是不會向相應的 `ignoredRects` 清單加入矩形，因此 `ExcludeAreas1`/`ExcludeAreas2` 會收到空陣列，比較器會處理整個頁面。

**Q: 我能只排除其中一個文件的註解，而在差異中保留另一個文件的註解嗎？**  
A: 將 `ExcludeAreas1`（或 `ExcludeAreas2`）設定為收集到的矩形，並將另一屬性保留為空陣列；比較器只會在指定的文件中忽略這些區域。

**Q: 重疊的註解矩形會對 `ExcludeAreas` 造成任何問題嗎？**  
A: 比較器會在內部合併重疊的矩形，因而安全地排除重疊的註解範圍，不會重複計算。

**Q: 是否可以使用相同的選項物件，同時排除表格與註解？**  
A: 可以，將 `compareOpts.ExcludeTables = true;` 設為 true——此旗標會與 `ExcludeAreas1`/`ExcludeAreas2` 一起作用，亦可排除表格區域。

**Q: 如果註解的 `Rect` 屬性為 null，程式碼會拋出例外嗎？**  
A: 程式碼在加入清單前會檢查 `if (a != null && a.Rect != null)`，因此會直接跳過 null 矩形，不會拋出例外。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}