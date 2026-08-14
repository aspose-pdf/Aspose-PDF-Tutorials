---
category: general
date: 2026-08-14
description: 在 C# 中建立簽署選項以套用數位簽章。了解如何設定簽章、實作自訂雜湊函式，並以程式方式簽署文件。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create signature options
- custom hash function
- apply digital signature
- how to sign document
- how to configure signature
language: zh-hant
lastmod: 2026-08-14
og_description: 在 C# 中建立簽章選項並套用數位簽章。本教學將逐步說明如何設定簽章、加入自訂雜湊函式，以及對文件簽名。
og_image_alt: Code editor view showing C# creation of signature options and document
  signing
og_title: 在 C# 中建立簽名選項 – 一步一步的數位簽署指南
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: Create signature options in C# to apply digital signature. Learn how
    to configure signature, implement a custom hash function, and sign documents programmatically.
  headline: Create signature options in C# – full guide to digital signing
  type: TechArticle
- description: Create signature options in C# to apply digital signature. Learn how
    to configure signature, implement a custom hash function, and sign documents programmatically.
  name: Create signature options in C# – full guide to digital signing
  steps:
  - name: '**Hash calculation** – now delegated to your custom hash function.'
    text: '**Hash calculation** – now delegated to your custom hash function.'
  - name: '**Signature generation** – using the private key supplied to the library’s
      configuration.'
    text: '**Signature generation** – using the private key supplied to the library’s
      configuration.'
  - name: '**Embedding** – the generated signature is attached to the output file.'
    text: '**Embedding** – the generated signature is attached to the output file.'
  type: HowTo
tags:
- digital signature
- C#
- security
title: 在 C# 中建立簽名選項 – 完整的數位簽署指南
url: /zh-hant/net/programming-with-security-and-signatures/create-signature-options-in-c-full-guide-to-digital-signing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中建立簽章選項 – 數位簽署完整指南

在 C# 中建立簽章選項以配置數位簽章工作流程。本教學說明如何套用數位簽章、實作自訂雜湊函式，並使用 `SignatureOptions` 類別簽署文件。若您曾需要從 .NET 應用程式簽署 PDF、XML 或任何二進位資料，以下步驟提供即用的解決方案。

您將學會：

* 使用自訂雜湊演算法設定 `SignatureOptions`
* 正確呼叫簽署方法
* 驗證簽章已正確套用
* 避免在設定簽章時的常見陷阱

唯一的先決條件是近期的 .NET SDK（≥ .NET 6）以及提供 `SignatureOptions` 的簽章函式庫（例如 **GroupDocs.Signature**、**Aspose.Signature** 或其他類似 API）。不需要任何外部工具。

---

## 前置條件

| 需求 | 為何重要 |
|------|----------|
| .NET 6 SDK or later | 提供範例中使用的現代語言功能。 |
| A signing‑library NuGet package (e.g., `GroupDocs.Signature`) | 提供 `SignatureOptions` 類型與 `Sign` 擴充方法。 |
| Access to a private key or certificate | 需要用於產生可驗證的數位簽章。 |

```bash
dotnet add package GroupDocs.Signature
```

---

## 步驟 1：建立簽章選項

第一步是實例化 `SignatureOptions` 並設定控制簽署流程的屬性。此物件告訴函式庫 *簽什麼* 以及 *如何* 簽署。

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Options;

// Create a new SignatureOptions instance
var signatureOptions = new SignatureOptions
{
    // The signing algorithm (e.g., RSA‑SHA256) is defined by the library.
    // You can also set visual appearance, page number, etc., here.
    // For this tutorial we focus on the custom hash function.
};
```

**為何重要**：`SignatureOptions` 作為您的程式碼與簽署引擎之間的合約。提前配置可避免在簽署多個文件時重複樣板程式碼。

---

## 步驟 2：實作自訂雜湊函式

*自訂雜湊函式* 讓您完整掌控簽章演算法所簽署的摘要。當預設雜湊（SHA‑256）不符合合規需求，或需要對文件的部分內容進行雜湊時，此方式非常有用。

```csharp
using System.Security.Cryptography;
using System.Text;

// Define a delegate that matches the library’s expected signature
Func<byte[], byte[]> MyHash = data =>
{
    // Example: compute SHA‑512 and then truncate to 256 bits
    using var sha512 = SHA512.Create();
    var fullHash = sha512.ComputeHash(data);

    // Truncate to the first 32 bytes (256 bits)
    var truncated = new byte[32];
    Buffer.BlockCopy(fullHash, 0, truncated, 0, truncated.Length);
    return truncated;
};

// Attach the custom hash to the options
signatureOptions.CustomSignHash = hash => MyHash(hash);
```

**為何重要**：透過指派 `CustomSignHash`，您將函式庫內部的雜湊步驟替換為 `MyHash`。簽署引擎現在會簽署您函式回傳的位元組，確保符合任何自訂政策。

---

## 步驟 3：載入文件並套用數位簽章

準備好選項後，您即可開啟目標檔案並呼叫簽署方法。`Sign` 方法由函式庫提供，並使用已配置的 `SignatureOptions`。

```csharp
using System.IO;

// Path to the file you want to sign
string inputPath = @"C:\Docs\contract.pdf";
string outputPath = @"C:\Docs\contract.signed.pdf";

// Load the document into the Signature object
using var signature = new Signature(inputPath);

// Sign the document using the previously created options
bool result = signature.Sign(outputPath, signatureOptions);

if (!result)
{
    throw new InvalidOperationException("The document could not be signed.");
}
```

**為何重要**：呼叫 `Sign` 會在內部執行三項動作：

1. **雜湊計算** – 現在委派給您的自訂雜湊函式。  
2. **簽章產生** – 使用函式庫設定提供的私鑰。  
3. **嵌入** – 產生的簽章會附加到輸出檔案。

若任一步驟失敗，該方法會回傳 `false`，讓您能優雅地處理錯誤。

---

## 步驟 4：驗證文件是否已簽署

快速驗證可確認簽章已正確套用。大多數函式庫提供 `Verify` 方法，用以檢查已簽署檔案的完整性。

```csharp
using var verifier = new Signature(outputPath);
var verificationResult = verifier.Verify();

Console.WriteLine(verificationResult
    ? "Signature verified successfully."
    : "Signature verification failed.");
```

**為何重要**：驗證可確保簽署後文件未被竄改，且自訂雜湊產生了相容的摘要。

---

## 如何為不同檔案類型設定簽章

相同的 `SignatureOptions` 物件可重複用於 PDF、Word 文件、影像或純二進位檔案。唯一需要變更的是特定的選項類別（例如 `PdfSignatureOptions`、`WordSignatureOptions`）。以下是一個 JPEG 影像的快速範例：

```csharp
using GroupDocs.Signature.Options;

var imageOptions = new ImageSignatureOptions
{
    // Position the signature on the image
    Left = 100,
    Top = 50,
    Width = 150,
    Height = 50,
    CustomSignHash = hash => MyHash(hash)   // reuse the same custom hash
};

using var imgSignature = new Signature(@"C:\Images\photo.jpg");
imgSignature.Sign(@"C:\Images\photo.signed.jpg", imageOptions);
```

**為何重要**：了解如何為每種格式*設定簽章*，即可在多種文件類型間共用相同程式碼基礎，而不必重新編寫雜湊邏輯。

---

## 常見陷阱與最佳實踐

| 陷阱 | 建議解決方案 |
|------|--------------|
| 忘記在建立 `SignatureOptions` 後設定 `CustomSignHash` | 在建構選項物件後立即指派委派。 |
| 使用簽章憑證不支援的雜湊演算法 | 確認憑證的金鑰用途與雜湊長度相符（例如 RSA‑2048 搭配 SHA‑512）。 |
| 忽略釋放 `Signature` 物件的需求 | 將 `Signature` 實例包在 `using` 區塊中，以釋放檔案句柄。 |
| 將已簽署的檔案覆寫原始來源 | 始終寫入新檔案路徑（`outputPath`），以保留原始文件。 |

---

## 完整可執行範例

以下是一個獨立的程式，將所有步驟整合在一起。將其複製到新的 Console 專案並執行；主控台會回報成功或失敗。

```csharp
using System;
using System.IO;
using System.Security.Cryptography;
using GroupDocs.Signature;
using GroupDocs.Signature.Options;

class Program
{
    // Custom hash implementation (SHA‑512 truncated to 256 bits)
    private static byte[] MyHash(byte[] data)
    {
        using var sha512 = SHA512.Create();
        var full = sha512.ComputeHash(data);
        var truncated = new byte[32];
        Buffer.BlockCopy(full, 0, truncated, 0, truncated.Length);
        return truncated;
    }

    static void Main()
    {
        // Paths
        string input = @"C:\Docs\contract.pdf";
        string output = @"C:\Docs\contract.signed.pdf";

        // Step 1: create signature options
        var signatureOptions = new SignatureOptions
        {
            CustomSignHash = hash => MyHash(hash)
        };

        // Step 2: sign the document
        using var signer = new Signature(input);
        bool signed = signer.Sign(output, signatureOptions);
        if (!signed)
        {
            Console.WriteLine("Signing failed.");
            return;
        }

        // Step 3: verify the signature
        using var verifier = new Signature(output);
        bool verified = verifier.Verify();
        Console.WriteLine(verified
            ? "Signature verified successfully."
            : "Signature verification failed.");
    }
}
```

**預期輸出**

```
Signature verified successfully.
```

如果主控台顯示 “Signing failed.” 或 “Signature verification failed.”，請再次檢查憑證設定，並確保自訂雜湊回傳的位元組陣列大小符合預期。

---

## 結論

您現在已了解如何在 C# 中**建立簽章選項**、附加**自訂雜湊函式**，以及對任何支援的文件**套用數位簽章**。本教學涵蓋完整生命週期：配置選項、簽署檔案、驗證結果。透過重複使用相同的 `SignatureOptions` 實例，您亦可**設定簽章**於影像、Word 檔或原始二進位檔案。

---

## 接下來可以做什麼？

* 探索額外的 `SignatureOptions` 屬性，例如視覺印章、時間戳伺服器與憑證鏈——這些與 **apply digital signature** 關鍵字相呼應。  
* 透過在 `MyHash` 內替換實作，試驗其他雜湊演算法（例如 Blake2b）。  
* 將簽署流程整合至 Web API，以實現即時文件簽署——這是 **how to sign document** 在服務導向架構中的自然延伸。

歡迎依照您的安全政策調整程式碼，並在留言中分享您的使用經驗。祝簽署順利！

## 接下來應該學什麼？

以下教學涵蓋與本指南技術緊密相關的主題。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [How to Change PDF Signature Language with Aspose.PDF for .NET](/pdf/english/net/digital-signatures/change-pdf-signature-language-aspose-net/)
- [Digital Signature Aspose Pdf Net Tutorial](/pdf/german/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)
- [Digital Signature Aspose Pdf Net Tutorial](/pdf/french/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}