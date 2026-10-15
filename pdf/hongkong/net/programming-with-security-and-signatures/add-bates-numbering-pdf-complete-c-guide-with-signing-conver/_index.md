---
category: general
date: 2026-06-21
description: 在單一步驟教學中加入 PDF 的 Bates 編號，學習如何添加 Bates 編號、將 PDF 轉換為 PDF/X-4、將 PDF 轉換為
  PDF/A-4，以及使用 C# 進行 PDF 數位簽署。
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbers
- digitally sign pdf c#
- convert pdf to pdf/x-4
- convert pdf to pdfa-4
language: zh-hant
og_description: 為 PDF 加上 Bates 編號，了解如何添加 Bates 編號，將 PDF 轉換為 PDF/X-4，將 PDF 轉換為 PDF/A-4，並使用
  Aspose.Pdf 以 C# 進行 PDF 數位簽署。
og_title: 在 PDF 中加入 Bates 編號 – C# 逐步教學
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add bates numbering pdf and learn how to add bates numbers, convert
    pdf to pdf/x-4, convert pdf to pdfa-4, and digitally sign pdf c# in a single walkthrough.
  headline: Add Bates Numbering PDF – Complete C# Guide with Signing & Conversion
  type: TechArticle
- questions:
  - answer: Yes. Use `BatesNumberingOptions` properties such as `Location` and `FontSize`
      to fine‑tune placement.
    question: Can I change the position of the Bates numbers?
  - answer: Switch `PdfFormat.PDF_X_4` to `PdfFormat.PDFA_4` in the conversion options.
      That satisfies the **convert pdf to pdfa-4** requirement.
    question: What if I need PDF/A‑4 instead of PDF/X‑4?
  - answer: Absolutely. Replace `DigestHashAlgorithm.Sha384` with `DigestHashAlgorithm.Sha256`
      (or any supported algorithm).
    question: My certificate uses a different hash algorithm—can I use SHA‑256?
  - answer: 'Not strictly. In this flow we save after conversion and after Bates numbering
      to give you intermediate files. You could defer saving until the end if you
      prefer a single write operation. ## Wrap‑Up We’ve just demonstrated a practical,
      end‑to‑end solution that **add bates numbering pdf**, explains **'
    question: Do I need to call `document.Save` after each step?
  type: FAQPage
tags:
- Aspose.Pdf
- C#
- PDF processing
- Bates numbering
title: 為 PDF 添加 Bates 編號 – 完整 C# 指南（含簽署與轉換）
url: /zh-hant/net/programming-with-security-and-signatures/add-bates-numbering-pdf-complete-c-guide-with-signing-conver/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 新增 Bates 編號 PDF – 完整 C# 指南，含簽署與轉換

有沒有想過 **add bates numbering pdf** 卻不想抓狂？你並不是唯一的。法律團隊、稽核人員以及所有需要可追溯文件的人，常常會問 *how to add bates numbers* 到 PDF，且還需要檔案符合 PDF/X‑4 或 PDF/A‑4 標準並進行數位簽署。

在本教學中，我們將一步步說明——使用 Aspose.Pdf for .NET，我們會 **add bates numbering pdf**、展示 **how to add bates numbers**、**convert pdf to pdf/x-4**、**convert pdf to pdfa-4**，最後 **digitally sign pdf c#**。完成後，你將擁有一個可直接執行的程式，產生三個精緻的 PDF：PDF/X‑4 版、已加 Bates 編號的版，以及已數位簽署的版。

![add bates numbering pdf 範例](image-placeholder.png "顯示 add bates numbering pdf 執行畫面的螢幕擷圖")

## 您需要的環境

- **.NET 6+**（或 .NET Framework 4.6+）。Aspose.Pdf 兩者皆支援。  
- 一份 **有效的 Aspose.Pdf for .NET 授權**（或使用評估版，但會出現浮水印）。  
- 一個 **PKCS#7 憑證檔案**（`.pfx`）及其密碼，用於簽署。  
- 你想要處理的 **範例 PDF**（放在自己可控制的資料夾中）。  
- Visual Studio、Rider，或任何你喜歡的 C# IDE。

就這樣——除了 `Aspose.Pdf` 之外不需要額外的 NuGet 套件。如果還沒加入程式庫，執行：

```bash
dotnet add package Aspose.Pdf
```

現在讓我們深入程式碼。

## 步驟 1：載入來源 PDF 文件

首先，我們需要將原始檔案載入記憶體。這是所有後續操作的基礎。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

// Load the source PDF – adjust the path to your environment
var document = new Document("YOUR_DIRECTORY/sample.pdf");
```

> **為什麼重要：** 載入 PDF 後會產生一個 `Document` 物件，代表整個檔案，讓我們可以使用轉換、表單欄位與安全性 API。

## 步驟 2：將 PDF 轉換為 PDF/X‑4（符合 PDF/A‑4 標準）

如果你的工作流程需要檔案具備保存品質，PDF/X‑4（PDF/A‑4 的子集）就是最佳選擇。以下示範如何使用 Aspose **convert pdf to pdf/x-4**。

```csharp
// Set conversion options – PDF/X‑4 is the target format
var conversionOptions = new PdfFormatConversionOptions(PdfFormat.PDF_X_4, ConvertErrorAction.Delete);

// Perform the conversion
document.Convert(conversionOptions);
```

> **小技巧：** `ConvertErrorAction.Delete` 旗標會移除任何會破壞合規性的內容，確保輸出為乾淨的 PDF/X‑4。

## 步驟 3：儲存 PDF/X‑4 版本

現在文件已符合 PDF/X‑4，我們將它寫入磁碟。

```csharp
document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");
```

你現在擁有一個 **convert pdf to pdfa-4** 相容的檔案（PDF/X‑4 為 PDF/A‑4 系列的一員）。可在 Acrobat 中開啟，驗證合規徽章。

## 步驟 4：新增 Bates 編號 – “Add Bates Numbering PDF” 的核心

Bates 編號是依序放在每一頁的識別碼。這正是 *how to add bates numbers* 的程式化解答。

```csharp
// Configure Bates numbering options
var batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",   // Optional prefix
    Start = 5000        // Starting number
};

// Apply Bates numbering to the document
document.AddBatesNumbering(batesOptions);
```

> **為什麼有效：** `AddBatesNumbering` 會逐頁走訪，並在預設位置（右下角）蓋上編號。若有需要，可透過 `BatesNumberingOptions` 調整位置。

## 步驟 5：儲存已加 Bates 編號的 PDF

在 **add bates numbering pdf** 完成後，我們需要一個保留編號的獨立檔案。

```csharp
document.Save("YOUR_DIRECTORY/sample_bates.pdf");
```

開啟檔案，你應該會在每頁底部看到 “CASE‑5000”、 “CASE‑5001” 等字樣。

## 步驟 6：數位簽署 PDF – “Digitally Sign PDF C#” 實作

數位簽章可保證文件的真實性與完整性。以下示範如何使用 SHA‑384 雜湊 **digitally sign pdf c#**。

```csharp
// Prepare the signature handler
var signature = new PdfFileSignature(document);

// Load the PKCS#7 certificate (adjust password)
var pkcs7 = new PKCS7Detached(
    "YOUR_DIRECTORY/mycert.pfx", // Path to .pfx
    "pwd",                       // Certificate password
    DigestHashAlgorithm.Sha384   // Strong hashing algorithm
);

// Sign page 1, place signature rectangle at (100,100)-(200,150)
signature.Sign(
    pageNumber: 1,
    signatureAppearance: true,
    rectangle: new Rectangle(100, 100, 200, 150),
    pkcs7: pkcs7
);
```

> **專業提示：** `Rectangle` 定義了可見簽章出現的位置。若不需要視覺提示，將 `signatureAppearance` 設為 `false` 即可。

## 步驟 7：儲存已數位簽署的 PDF

最後，將簽署後的文件寫入磁碟。

```csharp
signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
```

現在你擁有一個 **digitally sign pdf c#** 檔案，任何支援數位簽章的 PDF 閱讀器都能驗證其有效性。

## 完整原始碼 – 一站式解決方案

以下是完整、可直接執行的程式碼範例。複製貼上、調整路徑後按 **F5** 即可。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source PDF document
        // -------------------------------------------------
        var document = new Document("YOUR_DIRECTORY/sample.pdf");

        // -------------------------------------------------
        // Step 2: Convert the document to PDF/X‑4 format
        // (PDF/A‑4 compliance)
        // -------------------------------------------------
        var conversionOptions = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_4,
            ConvertErrorAction.Delete);
        document.Convert(conversionOptions);

        // -------------------------------------------------
        // Step 3: Save the PDF/X‑4 version
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");

        // -------------------------------------------------
        // Step 4: Add Bates numbering – how to add bates numbers
        // -------------------------------------------------
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 5000
        };
        document.AddBatesNumbering(batesOptions);

        // -------------------------------------------------
        // Step 5: Save the Bates‑numbered PDF
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_bates.pdf");

        // -------------------------------------------------
        // Step 6: Sign the document using SHA‑384 hashing
        // -------------------------------------------------
        var signature = new PdfFileSignature(document);
        var pkcs7 = new PKCS7Detached(
            "YOUR_DIRECTORY/mycert.pfx",
            "pwd",
            DigestHashAlgorithm.Sha384);
        signature.Sign(
            pageNumber: 1,
            signatureAppearance: true,
            rectangle: new Rectangle(100, 100, 200, 150),
            pkcs7: pkcs7);

        // -------------------------------------------------
        // Step 7: Save the digitally signed PDF
        // -------------------------------------------------
        signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
    }
}
```

### 預期輸出

| 檔案 | 用途 | 主要功能 |
|------|------|----------|
| `sample_pdfx4.pdf` | PDF/X‑4 版本 | 符合 PDF/A‑4 標準 |
| `sample_bates.pdf` | 已加 Bates 編號的 PDF | **add bates numbering pdf** 已套用 |
| `sample_signed.pdf` | 已數位簽署的 PDF | **digitally sign pdf c#** 使用 SHA‑384 |

在 Adobe Acrobat Reader 開啟任一檔案；第二個檔案會顯示 Bates 編號，第三個檔案則會出現簽章欄位。

## 常見問題 (FAQ)

**Q: 可以變更 Bates 編號的位置嗎？**  
A: 可以。使用 `BatesNumberingOptions` 的 `Location`、`FontSize` 等屬性即可微調放置位置。

**Q: 若需要 PDF/A‑4 而非 PDF/X‑4，該怎麼做？**  
A: 在轉換選項中將 `PdfFormat.PDF_X_4` 改為 `PdfFormat.PDFA_4`。這樣即可滿足 **convert pdf to pdfa-4** 的需求。

**Q: 我的憑證使用不同的雜湊演算法，能改用 SHA‑256 嗎？**  
A: 完全可以。只要把 `DigestHashAlgorithm.Sha384` 換成 `DigestHashAlgorithm.Sha256`（或其他支援的演算法）即可。

**Q: 每個步驟都需要呼叫 `document.Save` 嗎？**  
A: 不一定。在此流程中，我們在轉換與加 Bates 編號後各存一次，以便取得中間檔案。若你想一次寫入，也可以等到最後一次 `Save`。

## 總結

我們剛剛示範了一個實用的端對端解決方案，能 **add bates numbering pdf**、說明 **how to add bates numbers**、展示 **convert pdf to pdf/x-4**，並涵蓋

## 接下來該學什麼？

以下教學與本指南的技術緊密相關，能幫助你進一步掌握 API 功能並探索其他實作方式：

- [Aspose Pdf .NET 新增附件 轉換 Pdfa](/pdf/german/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf .NET 新增附件 轉換 Pdfa](/pdf/french/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf .NET 新增附件 轉換 Pdfa](/pdf/japanese/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}