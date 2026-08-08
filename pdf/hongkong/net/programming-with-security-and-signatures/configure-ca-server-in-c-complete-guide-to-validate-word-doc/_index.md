---
category: general
date: 2026-03-27
description: 設定 CA 伺服器，並學習如何使用 C# 驗證 Word 文件中的簽名。包括逐步說明的程式碼，用於檢查簽名有效性及驗證數位簽名（C#）。
draft: false
keywords:
- configure ca server
- how to validate signature
- check signature validity
- verify digital signature c#
- load word document c#
language: zh-hant
og_description: 使用 C# 設定 CA 伺服器並驗證 Word 文件中的數位簽章。一步一步學習如何檢查簽章有效性。
og_title: 在 C# 中設定 CA 伺服器 – 驗證 Word 文件簽章
tags:
- C#
- Digital Signature
- Word Automation
title: 在 C# 中設定 CA 伺服器 – 完整指南：驗證 Word 文件簽署
url: /zh-hant/net/programming-with-security-and-signatures/configure-ca-server-in-c-complete-guide-to-validate-word-doc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中設定 CA 伺服器 – 驗證 Word 文件簽章

是否曾需要 **configure ca server** 以便在程式中驗證 Word 檔案內的簽章？你並非唯一遇到此需求的人。在許多企業工作流程——例如合約審批或法律文件提交——從程式碼檢查 **signature validity** 是必備功能。

在本教學中，我們將完整示範：載入 Word 文件（`.docx`）、將 `SignatureValidator` 指向你的憑證授權中心（CA）端點，最後說明 **how to validate signature** — 全部以乾淨的 C# 程式碼呈現。完成後，你將能以 **verify digital signature c#** 方式驗證數位簽章，而不必在雜亂的文件中搜尋。

## 前置條件

- .NET 6.0 或更新版本（我們使用的 API 目標為 .NET Standard 2.0，舊版框架亦可相容）  
- 參考 `Aspose.Words`（或等效）函式庫，提供 `SignatureValidator`（透過 NuGet 安裝）  
- 可存取提供驗證端點的 CA 伺服器（例如 `https://ca.example.com/validate`）  
- 具備基本的 C# 與 Visual Studio（或其他 IDE）使用經驗  

若上述任一項你不熟悉，別擔心，我們會在教學中逐一說明。

## 解決方案概覽

1. **載入 Word 文件** – 使用 `Document` 讀取 `input.docx`。  
2. **設定 CA 伺服器 URL** – 驗證器需要知道要將憑證送往哪裡進行驗證。  
3. **驗證指定簽章** – 呼叫 `Validate("Sig1")` 並解讀布林結果。  

就這樣。簡單吧？雖然背後涉及憑證鏈、CRL 檢查與可選的時間戳驗證等概念，但都被 API 隱藏，這也是我們喜愛它的原因。

---

![設定 ca 伺服器並驗證 Word 文件簽章的工作流程圖](configure-ca-server-diagram.png)

*圖片說明：設定 ca 伺服器工作流程圖*

## 步驟 1 – 載入 Word 文件（`load word document c#`）

在觸碰任何簽章之前，我們必須先將檔案載入記憶體。`Document` 類別抽象了 Office Open XML 格式，讓我們能像操作其他物件一樣處理檔案。

```csharp
using Aspose.Words;          // NuGet: Aspose.Words
using Aspose.Words.Saving;   // Optional, for saving later

// Path to your .docx file – adjust as needed.
string docPath = Path.Combine(Environment.CurrentDirectory, "input.docx");

// Create a Document instance – this loads the file into memory.
Document doc = new Document(docPath);
```

**為什麼重要：** 載入文件後即可取得其 `Signatures` 集合。若檔案損毀或路徑錯誤，會在早期拋出例外，避免之後出現難以理解的錯誤。

> **小技巧：** 將載入動作包在 `try / catch` 中，並分別記錄 `FileNotFoundException`——當檔案位於網路共享時特別有助於除錯。

## 步驟 2 – 建立並設定 Signature Validator（`configure ca server`）

文件準備好後，我們建立 `SignatureValidator`。此物件負責與你指定的 CA 伺服器通訊。

```csharp
// Instantiate the validator, passing the loaded document.
SignatureValidator signatureValidator = new SignatureValidator(doc);

// Point the validator at your CA's validation endpoint.
signatureValidator.CaServerUrl = "https://ca.example.com/validate";
```

**底層發生了什麼？**  
當稍後呼叫 `Validate` 時，驗證器會抽取簽章的憑證、建立憑證鏈，並將驗證請求（通常是 PKIX‑OCSP 或 CRL 查詢）送至你設定的 URL。CA 回傳「good」或「revoked」狀態，函式庫再將其轉換為布林值。

> **注意：** CA URL 必須能從執行程式的機器連線。防火牆或代理設定可能阻擋請求，導致逾時。若發生逾時，請先使用 `curl` 或 `Invoke-WebRequest` 確認連線。

## 步驟 3 – 驗證特定簽章（`how to validate signature`）

Word 文件可能包含多個簽章（例如每位審閱者各一個）。你需要取得簽章的識別碼——常見為 “Sig1”、 “Sig2” 等——可透過 `Signatures` 集合查詢。

```csharp
// Choose the signature name you want to validate.
// You can enumerate doc.Signatures to find available names.
string signatureName = "Sig1";

// Perform the validation. Returns true if the signature is considered valid.
bool isSignatureValid = signatureValidator.Validate(signatureName);

// Output the result to the console (or log it as needed).
Console.WriteLine($"Signature validation result for '{signatureName}': {isSignatureValid}");
```

**結果解讀：**  
- `true` – 憑證鏈完整，CA 確認簽章，且文件未被竄改。  
- `false` – 可能的原因包括：憑證已撤銷、無法連線至 CA、簽章資料與文件不符，或 CA 回傳負面回應。

> **常見問題：** *如果文件沒有簽章會怎樣？*  
> `Validate` 方法會拋出 `SignatureNotFoundException`。請先做好防護：

```csharp
if (!doc.Signatures.Any())
{
    Console.WriteLine("No signatures found in the document.");
}
else
{
    // Proceed with validation as shown above.
}
```

## 完整範例程式

將所有步驟整合，以下是一個可直接複製貼上的完整程式。內含錯誤處理、簽章列舉以及驗證結果的簡要摘要。

```csharp
using System;
using System.IO;
using Aspose.Words;
using Aspose.Words.Saving;

namespace WordSignatureValidation
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Word document – adjust the path as needed.
            // -----------------------------------------------------------------
            string docPath = Path.Combine(Environment.CurrentDirectory, "input.docx");
            Document doc;
            try
            {
                doc = new Document(docPath);
            }
            catch (FileNotFoundException)
            {
                Console.WriteLine($"File not found: {docPath}");
                return;
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error loading document: {ex.Message}");
                return;
            }

            // -----------------------------------------------------------------
            // 2️⃣ Set up the validator and point it at the CA server.
            // -----------------------------------------------------------------
            SignatureValidator validator = new SignatureValidator(doc)
            {
                // Primary keyword appears here – configure ca server URL.
                CaServerUrl = "https://ca.example.com/validate"
            };

            // -----------------------------------------------------------------
            // 3️⃣ List available signatures (helps with how to validate signature).
            // -----------------------------------------------------------------
            if (!doc.Signatures.Any())
            {
                Console.WriteLine("The document contains no digital signatures.");
                return;
            }

            Console.WriteLine("Available signatures:");
            foreach (var sig in doc.Signatures)
                Console.WriteLine($"- {sig.SignatureName}");

            // For demo purposes we pick the first signature.
            string targetSignature = doc.Signatures[0].SignatureName;

            // -----------------------------------------------------------------
            // 4️⃣ Validate the chosen signature.
            // -----------------------------------------------------------------
            bool isValid;
            try
            {
                isValid = validator.Validate(targetSignature);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Validation failed: {ex.Message}");
                return;
            }

            // -----------------------------------------------------------------
            // 5️⃣ Report the result – this is our check signature validity step.
            // -----------------------------------------------------------------
            Console.WriteLine($"Signature '{targetSignature}' validation result: {isValid}");
        }
    }
}
```

### 預期輸出

```
Available signatures:
- Sig1
- Sig2
Signature 'Sig1' validation result: True
```

如果 CA 回報問題，會顯示 `False`，你可以進一步檢查 CA 的回應（若開啟詳細日誌，函式庫可提供更完整的狀態碼）。

---

## 邊緣案例與變化

| 情境 | 需要調整的地方 |
|----------|----------------|
| **多個 CA 端點** | 依簽章發行的 CA 動態設定 `validator.CaServerUrl`。 |
| **自簽憑證** | 使用 `validator.TrustSelfSigned = true;`（或等效屬性）在測試環境接受。 |
| **離線驗證** | 部分函式庫允許透過 `validator.CrlPath` 提供本機 CRL 檔案。 |
| **含時間戳的簽章** | 驗證後檢查 `signature.SignatureTime`，確保簽章於撤銷前完成。 |
| **非 Aspose 函式庫** | 若使用 `DocX` 或 `Open XML SDK`，流程相似：抽取 `SignaturePart`、將憑證送至 CA，並手動比對雜湊值。 |

請記住，**verify digital signature c#** 不只是回傳 true/false，還需要了解簽章失敗的原因。記錄 CA 的回應碼（例如 `0x800B0100` 代表已撤銷）能在日後節省大量除錯時間。

---

## 常見問答

**Q: 這能支援 `.doc`（二進位）檔案嗎？**  
A: `Document` 類別能開啟舊版 `.doc` 檔，但簽章 API 只保證在 OOXML（`.docx`）格式下正常運作。建議將舊檔轉為 `.docx` 以取得可靠結果。

**Q: 若 CA 需要驗證身份該怎麼辦？**  
A: 在呼叫 `Validate` 前，使用 `validator.CaServerCredentials`（或相應屬性）設定 `NetworkCredential` 物件。

**Q: 能一次驗證所有簽章嗎？**  
A: 可以遍歷 `doc.Signatures`，對每個名稱呼叫 `Validate`，並將結果收集至字典以供報表使用。

---

## 結論

我們已完整說明如何在 C# 中 **configure ca server**、**load word document c#**，以及使用 `SignatureValidator` **check signature validity**。完整程式範例展示了 **how to validate signature**，並解釋每行程式碼背後的原理，為任何以文件為中心的工作流程奠定堅實基礎。

接下來的步驟？可以嘗試將 CA 端點換成回傳模擬回應的測試伺服器，或將此邏輯整合至 ASP.NET Core API，於上傳合約時即時驗證。你也可以探索 **verify digital signature c#** 在 PDF 上的應用（例如使用 `iTextSharp`），概念相當相通。

祝開發順利，願所有簽章皆保持有效！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}