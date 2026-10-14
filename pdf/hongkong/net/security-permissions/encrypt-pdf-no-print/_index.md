---
title: 使用 Aspose.PDF for .NET 加密 PDF（不允許列印）
weight: 101
limit:
description: 了解如何使用 Aspose.PDF for .NET 以 AES‑256 加密 PDF 並停用列印。
keywords: [Aspose.PDF for .NET, pdf encryption aes-256, disable pdf printing, pdf password protection, no print permission pdf]
url: /net/security-permissions/encrypt-pdf-no-print/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: 了解如何使用 Aspose.PDF for .NET 以 AES‑256 加密 PDF 並停用列印。
  headline: 使用 Aspose.PDF for .NET 加密 PDF（不允許列印）
  type: TechArticle
- description: 了解如何使用 Aspose.PDF for .NET 以 AES‑256 加密 PDF 並停用列印。
  name: 使用 Aspose.PDF for .NET 加密 PDF（不允許列印）
  steps:
  - name: 定義來源 PDF 的路徑、輸出受保護檔案的名稱，以及檢視密碼與擁有者密碼。
    text: 定義來源 PDF 的路徑、輸出受保護檔案的名稱，以及檢視密碼與擁有者密碼。
  - name: 檢查來源檔案是否存在，若不存在則以錯誤訊息中止程式。
    text: 檢查來源檔案是否存在，若不存在則以錯誤訊息中止程式。
  - name: 開啟原始 PDF，設定無權限，使用指定的密碼以 AES‑256 加密，並儲存受保護的檔案。
    text: 開啟原始 PDF，設定無權限，使用指定的密碼以 AES‑256 加密，並儲存受保護的檔案。
  - name: 使用檢視密碼重新開啟已加密的 PDF，並將其 IsEncrypted 屬性寫入主控台，以確認已受保護。
    text: 使用檢視密碼重新開啟已加密的 PDF，並將其 IsEncrypted 屬性寫入主控台，以確認已受保護。
  - name: 輸出最終訊息，指出加密已完成並顯示輸出檔案名稱。
    text: 輸出最終訊息，指出加密已完成並顯示輸出檔案名稱。
  type: HowTo
- questions:
  - answer: '`Permissions` 為旗標列舉；將其賦值為 `0` 代表未設定任何權限位元，因而 Aspose.Pdf 不會授予 PrintDocument
      權限，檢視器無法列印 PDF。'
    question: 為什麼設定 `Permissions rights = 0;` 會停用列印？
  - answer: 可以，將 `pdfDoc.Encrypt` 呼叫中的 `CryptoAlgorithm.AESx256` 替換為 `CryptoAlgorithm.AESx128`（或其他支援的列舉值），其餘程式碼保持不變。
    question: 我可以使用其他加密演算法（例如 AES‑128）而不更改程式碼嗎？
  - answer: Aspose.Pdf 會接受相同的密碼，但擁有者密碼將不再提供額外權限；PDF 仍會被加密，且您所指定的權限（無）仍會生效。
    question: 如果檢視密碼與主密碼（擁有者密碼）相同，會發生什麼情況？
  - answer: 使用檢視密碼開啟受保護的檔案（`new Document(securedFile, viewerPwd)`），然後在 PDF 檢視器中嘗試列印；由於未設定
      `PrintDocument` 權限，檢視器會拒絕列印指令。
    question: 如何確認加密後列印確實被阻止？
  - answer: 程式碼會先檢查 `File.Exists(sourceFile)`，若不存在則寫入錯誤訊息至 `Console.Error` 後返回，從而避免
      `Document` 建構函式拋出 `FileNotFoundException`。
    question: 如果 `original.pdf` 不存在，會拋出什麼錯誤，應該如何處理？
  type: FAQPage
images:
- /net/security-permissions/encrypt-pdf-no-print/og-image.png
og_title: 加密 PDF 並阻止列印
og_description: 使用 AES‑256 加密保護您的 PDF，並確保其無法列印——一步一步的指南。
og_image_alt: 螢幕截圖顯示 Aspose.PDF for .NET 程式碼，用於加密 PDF 並停用列印。
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.PDF for .NET 加密 PDF（不允許列印）
本教學說明如何使用 Aspose.PDF for .NET 開啟現有 PDF，套用 AES‑256 加密且不授予任何權限——實際上會停用列印，儲存已保護的文件，並透過使用檢視密碼開啟來確認保護。請依照逐步程式碼操作，以確保 PDF 在加密後無法列印。

---

{{< tutorial-widget sourcePath="pdf/net/security-permissions/encrypt-pdf-no-print" >}}


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

**Q: 為什麼設定 `Permissions rights = 0;` 會停用列印？**  
A: `Permissions` 為旗標列舉；將其賦值為 `0` 代表未設定任何權限位元，因而 Aspose.Pdf 不會授予 PrintDocument 權限，檢視器無法列印 PDF。

**Q: 我可以使用其他加密演算法（例如 AES‑128）而不更改程式碼嗎？**  
A: 可以，將 `pdfDoc.Encrypt` 呼叫中的 `CryptoAlgorithm.AESx256` 替換為 `CryptoAlgorithm.AESx128`（或其他支援的列舉值），其餘程式碼保持不變。

**Q: 如果檢視密碼與主密碼（擁有者密碼）相同，會發生什麼情況？**  
A: Aspose.Pdf 會接受相同的密碼，但擁有者密碼將不再提供額外權限；PDF 仍會被加密，且您所指定的權限（無）仍會生效。

**Q: 如何確認加密後列印確實被阻止？**  
A: 使用檢視密碼開啟受保護的檔案（`new Document(securedFile, viewerPwd)`），然後在 PDF 檢視器中嘗試列印；由於未設定 `PrintDocument` 權限，檢視器會拒絕列印指令。

**Q: 如果 `original.pdf` 不存在，會拋出什麼錯誤，應該如何處理？**  
A: 程式碼會先檢查 `File.Exists(sourceFile)`，若不存在則寫入錯誤訊息至 `Console.Error` 後返回，從而避免 `Document` 建構函式拋出 `FileNotFoundException`。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}