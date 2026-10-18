---
title: 使用 Aspose.PDF for .NET 將單一 PDF 頁面旋轉 180 度。
weight: 260
limit:
description: 了解如何使用 Aspose.PDF for .NET 將 PDF 的第三頁旋轉 180°。
keywords: [rotate pdf page, Aspose.PDF for .NET, PDF page rotation .NET, rotate third page pdf, PDF SDK rotate page]
url: /net/programming-with-pdf-pages/rotate-pdf-page/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: 了解如何使用 Aspose.PDF for .NET 將 PDF 的第三頁旋轉 180°。
  headline: 使用 Aspose.PDF for .NET 將單一 PDF 頁面旋轉 180 度。
  type: TechArticle
- description: 了解如何使用 Aspose.PDF for .NET 將 PDF 的第三頁旋轉 180°。
  name: 使用 Aspose.PDF for .NET 將單一 PDF 頁面旋轉 180 度。
  steps:
  - name: 此檔案僅包含說明性註解，沒有可執行程式碼，作為原始範例的佔位符。
    text: 此檔案僅包含說明性註解，沒有可執行程式碼，作為原始範例的佔位符。
  type: HowTo
- questions:
  - answer: 使用 SDK 的頁面集合並採用零基索引，例如 `pdfDocument.Pages[2]`，因為索引 2 代表第三頁。
    question: 我要如何指定 PDF 的第三頁進行旋轉？
  - answer: 旋轉屬性僅接受四個標準值 0、90、180 和 270 度；其他任何值都會四捨五入為最近的允許角度。
    question: 我可以將頁面旋轉成除 180 度以外的角度嗎？
  - answer: 旋轉僅套用於記憶體中的 `PdfDocument`；必須呼叫 `pdfDocument.Save("output.pdf")`（或其他類似的儲存方法）才能將變更寫入新檔案，原始檔案將保持不變。
    question: 旋轉頁面會自動修改原始檔案嗎？
  - answer: SDK 會自動重新計算註解和表單欄位的位置，使其在新方向下保持正確對齊。
    question: 頁面旋轉後，註解或表單欄位會發生什麼情況？
  type: FAQPage
images:
- /net/programming-with-pdf-pages/rotate-pdf-page/og-image.png
og_title: 使用 Aspose.PDF 將 PDF 頁面旋轉 180°。
og_description: 只需幾行 Aspose.PDF for .NET 程式碼，即可快速將 PDF 的第三頁上下顛倒。
og_image_alt: 本指南展示使用 Aspose.PDF for .NET 將 PDF 第三頁旋轉 180 度的程式碼。
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.PDF for .NET 將單一 PDF 頁面旋轉 180 度。
在本教學中，您將學習如何使用 Aspose.PDF for .NET 將 PDF 文件的第三頁旋轉 180 度。範例說明了載入 PDF、選取第 3 頁、套用旋轉以及儲存更新後檔案的步驟。此方法可讓您翻轉特定頁面，而不會改變其餘頁面的方向。

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/rotate-pdf-page" >}}


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

**Q: 我要如何指定 PDF 的第三頁進行旋轉？**  
A: 使用 SDK 的頁面集合並採用零基索引，例如 `pdfDocument.Pages[2]`，因為索引 2 代表第三頁。

**Q: 我可以將頁面旋轉成除 180 度以外的角度嗎？**  
A: 旋轉屬性僅接受四個標準值 0、90、180 和 270 度；其他任何值都會四捨五入為最近的允許角度。

**Q: 旋轉頁面會自動修改原始檔案嗎？**  
A: 旋轉僅套用於記憶體中的 `PdfDocument`；必須呼叫 `pdfDocument.Save("output.pdf")`（或其他類似的儲存方法）才能將變更寫入新檔案，原始檔案將保持不變。

**Q: 頁面旋轉後，註解或表單欄位會發生什麼情況？**  
A: SDK 會自動重新計算註解和表單欄位的位置，使其在新方向下保持正確對齊。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}