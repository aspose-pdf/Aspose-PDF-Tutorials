---
category: general
date: 2026-03-24
description: 快速且安全地在 C# 載入 PFX 證書，從檔案產生 PKCS7 分離簽章。逐步教學，提供完整程式碼與常見陷阱。
draft: false
keywords:
- load pfx certificate c#
- create pkcs7 detached signature
- pkcs7 signature from file
- c# pkcs7 signing
- digital signature c#
language: zh-hant
og_description: 在 C# 中載入 PFX 憑證，並從檔案產生 PKCS7 分離簽章。完整範例，附說明與邊緣案例處理。
og_title: 載入 PFX 憑證 C# – 建立 PKCS7 分離式簽名
tags:
- C#
- PKCS7
- X509
- Cryptography
title: 載入 PFX 憑證 C# – 建立 PKCS7 分離簽章
url: /zh-hant/net/programming-with-security-and-signatures/load-pfx-certificate-c-create-pkcs7-detached-signature/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 載入 PFX 憑證 C# – 建立 PKCS7 分離簽章

是否曾需要 **在 C# 中載入 PFX 憑證** 以簽署資料，但不知從何開始？你並非唯一遇到此問題的人——許多開發者在首次接觸 X.509 憑證與 PKCS#7 時，都會卡在同一個地方。

好消息是？在本教學中，你將獲得一個即時可執行的解決方案，**在 C# 中載入 PFX 憑證**、建立 **PKCS7 分離簽章**，甚至示範如何從檔案中取出簽章。沒有模糊的參考，只有具體的程式碼與每一行背後的原理。

> **你將學到的內容**  
> * 對憑證載入流程有清晰的了解。  
> * 完整且可編譯的範例，能產生 PKCS7 分離簽章。  
> * 處理常見陷阱的技巧（密碼錯誤、檔案遺失、演算法不匹配）。  

### 前置條件

- .NET 6.0 或更新版本（使用的 API 為基礎類別庫的一部分）。  
- 有效的 `.pfx` 檔案及其密碼。  
- Visual Studio 2022 或任何你喜歡的編輯器——核心範例不需要額外的 NuGet 套件。  

如果你已具備上述條件，讓我們開始吧。

---

## 載入 PFX 憑證 C# – 步驟說明

以下是你需要的最小 `using` 指令集合。請將它們放在檔案的最上方，讓編譯器知道類型的所在位置。

```csharp
using System;
using System.IO;
using System.Security.Cryptography;
using System.Security.Cryptography.X509Certificates;
```

### 1️⃣ 指定憑證路徑與密碼

首先，告訴執行環境 `.pfx` 檔案所在的位置以及其密碼。硬編碼路徑在示範時尚可，但 **絕不可** 在正式程式碼中嵌入密碼。

```csharp
// Step 1: Path to your certificate and its password
string certificatePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "certificate.pfx");
string certificatePassword = "yourPassword"; // <-- replace with a secure source
```

> **專業提示：** 將密碼儲存在 Azure Key Vault、AWS Secrets Manager，或環境變數中——絕不要將其提交至原始碼管理。

### 2️⃣ 安全載入憑證

我們將載入動作包在 `try / catch` 區塊中，以捕捉常見錯誤，例如檔案遺失或密碼不正確。

```csharp
X509Certificate2 LoadCertificate(string path, string password)
{
    try
    {
        // The X509KeyStorageFlags ensure the private key is exportable for signing
        var cert = new X509Certificate2(path, password,
            X509KeyStorageFlags.MachineKeySet |
            X509KeyStorageFlags.PersistKeySet |
            X509KeyStorageFlags.Exportable);

        if (!cert.HasPrivateKey)
            throw new InvalidOperationException("The certificate does not contain a private key.");

        return cert;
    }
    catch (Exception ex) when (ex is CryptographicException || ex is IOException)
    {
        Console.Error.WriteLine($"Failed to load certificate: {ex.Message}");
        throw;
    }
}
```

### 3️⃣ 建立 **PKCS7 分離簽章** 物件

假設你使用的第三方函式庫提供 `PKCS7Detached` 類別（許多商業 SDK 都有），我們會以剛剛載入的憑證來實例化它。

```csharp
// Step 3: Build the signer
var certificate = LoadCertificate(certificatePath, certificatePassword);

var pkcs7Signer = new PKCS7Detached(certificate)
{
    // Provide a custom hash‑signing callback.
    // The library will invoke this delegate for each hash it needs to sign.
    CustomSignHash = (hash, algorithm) => MySigner.Sign(hash, algorithm)
};
```

> **為何需要回呼？** 某些 SDK 允許你接入硬體安全模組 (HSM) 或遠端簽署服務。透過公開 `CustomSignHash`，你可以保持簽署邏輯的彈性。

### 4️⃣ 實作簽署委派

以下是一個簡單的實作，使用已載入憑證的私鑰。若有需要，請將 `MySigner.Sign` 替換為你自己的 HSM 呼叫。

```csharp
static class MySigner
{
    public static byte[] Sign(byte[] hash, HashAlgorithmName algorithm)
    {
        // The certificate's private key is an RSA key in most cases.
        using RSA rsa = certificate.GetRSAPrivateKey()
            ?? throw new InvalidOperationException("RSA private key not available.");

        // RSA-PKCS#1 v1.5 signing – adjust if your policy requires PSS.
        return rsa.SignHash(hash, algorithm, RSASignaturePadding.Pkcs1);
    }
}
```

### 5️⃣ 簽署任意資料並取得分離的 PKCS7 Blob

現在我們真的要簽署一些東西。資料可以是檔案、JSON 負載，或任何你需要保護的內容。

```csharp
// Step 5: Data you want to protect
byte[] dataToSign = File.ReadAllBytes("sample.txt");

// The PKCS7Detached class usually offers a Sign method that returns the raw signature.
byte[] detachedSignature = pkcs7Signer.Sign(dataToSign);

// Save the signature to disk for later verification
File.WriteAllBytes("sample.txt.sig", detachedSignature);

Console.WriteLine("Detached PKCS7 signature created successfully.");
```

**預期輸出**

```
Detached PKCS7 signature created successfully.
```

現在你已擁有一個 **來自檔案的 PKCS7 簽章** (`sample.txt.sig`)，可在不依賴原始資料的情況下進行驗證。

---

## 建立 PKCS7 分離簽章 – 進階選項

雖然基本流程適用於大多數情境，但在正式系統中常需要額外的設定：

| 功能 | 如何啟用 | 何時使用 |
|------|----------|----------|
| **Algorithm selection** | 將 `HashAlgorithmName.SHA256`（或 SHA384/SHA512）傳遞給 `SignHash` | 如果你的合規要求指定使用特定的雜湊演算法 |
| **Timestamping** | 在簽章之後加入 RFC‑3161 時間戳記 | 用於長期驗證 |
| **Multiple signers** | 建立額外的 `PKCS7Detached` 實例並合併 | 當文件需要共同簽署時 |
| **Custom CMS attributes** | 在 `Sign` 之前使用函式庫的 `AddAttribute` 方法 | 以嵌入簽署時間、簽署者 ID 等資訊 |

```csharp
CustomSignHash = (hash, _) => MySigner.Sign(hash, HashAlgorithmName.SHA256)
```

---

## 驗證 PKCS7 分離簽章（可選）

驗證是故事的另一半。大多數函式庫提供 `Verify` 方法，接受原始資料與分離簽章。

```csharp
bool VerifySignature(byte[] originalData, byte[] signature, X509Certificate2 cert)
{
    var verifier = new PKCS7Detached(cert);
    return verifier.Verify(originalData, signature);
}

// Usage
bool isValid = VerifySignature(dataToSign, detachedSignature, certificate);
Console.WriteLine(isValid ? "Signature valid!" : "Signature invalid!");
```

如果你使用其他 SDK，請在 .NET 的 `System.Security.Cryptography.Pkcs` 命名空間中尋找 `CmsSignedData` 或 `SignedCms` 類別——它們同樣能處理分離簽章。

---

## 常見陷阱與避免方法

1. **密碼錯誤** – `CryptographicException` 會顯示 *「指定的網路密碼不正確。」* 請安全地儲存密碼，並在載入憑證前先獨立測試。  
2. **憑證缺少私鑰** – 某些 `.pfx` 檔案在匯出時已移除私鑰。請再次確認 CA 或 Key Vault 的匯出設定。  
3. **演算法不匹配** – 若簽署方預期使用 SHA‑256 而你提供 SHA‑1，驗證將失敗。請在簽署與驗證步驟中保持演算法一致。  
4. **檔案路徑問題** – 相對路徑在開發環境可行，但部署時可能失效。建議使用 `Path.Combine(AppDomain.CurrentDomain.BaseDirectory, ...)` 或以設定檔驅動的絕對路徑。  
5. **平台差異** – Windows 與 Linux 處理私鑰儲存方式不同。使用 `X509KeyStorageFlags.Exportable` 可減少大多數跨平台的問題。

---

## 完整可執行範例（直接複製貼上）

```csharp
using System;
using System.IO;
using System.Security.Cryptography;
using System.Security.Cryptography.X509Certificates;

// ------------------------------------------------------------
// Helper class that encapsulates signing logic
// ------------------------------------------------------------
static class MySigner
{
    private static X509Certificate2 _cert;

    public static void Init(X509Certificate2 cert) => _cert = cert;

    public static byte[] Sign(byte[] hash, HashAlgorithmName algorithm)
    {
        using RSA rsa = _cert.GetRSAPrivateKey()
            ?? throw new InvalidOperationException("RSA private key not available.");

        return rsa.SignHash(hash, algorithm, RSASignaturePadding.Pkcs1);
    }
}

// ------------------------------------------------------------
// Main program
// ------------------------------------------------------------
class Program
{
    static X509Certificate2 LoadCertificate(string path, string password)
    {
        try
        {
            var cert = new X509Certificate2(path, password,
                X509KeyStorageFlags.MachineKeySet |
                X509KeyStorageFlags.PersistKeySet |
                X509KeyStorageFlags.Exportable);

            if (!cert.HasPrivateKey)
                throw new InvalidOperationException("Certificate lacks a private key.");

            return cert;
        }
        catch (Exception ex) when (ex is CryptographicException || ex is IOException)
        {
            Console.Error.WriteLine($"Failed to load certificate: {ex.Message}");
            throw;
        }
    }

    static void Main()
    {
        // 1️⃣ Path & password
        string certPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "certificate.pfx");
        string certPassword = "yourPassword";

        // 2️⃣ Load the cert
        X509Certificate2 cert = LoadCertificate(certPath, certPassword);
        MySigner.Init(cert);

        // 3️⃣ Create PKCS7 signer (replace with your library's class)
        var pkcs7Signer = new PKCS7Detached(cert)
        {
            CustomSignHash = (hash, _) => MySigner.Sign(hash, HashAlgorithmName.SHA256)
        };

        // 4️⃣ Data to sign
        string dataFile = "sample.txt";
        byte[] data = File.ReadAllBytes(dataFile);

        // 5️⃣ Generate detached signature
        byte[] signature = pkcs7Signer.Sign(data);
        File.WriteAllBytes

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}