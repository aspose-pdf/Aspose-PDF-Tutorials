---
category: general
date: 2026-03-24
description: C#でPFX証明書を迅速かつ安全にロードし、ファイルからPKCS7デタッチド署名を作成する。完全なコードと落とし穴を含むステップバイステップガイド。
draft: false
keywords:
- load pfx certificate c#
- create pkcs7 detached signature
- pkcs7 signature from file
- c# pkcs7 signing
- digital signature c#
language: ja
og_description: C#でPFX証明書をロードし、ファイルからPKCS7デタッチド署名を生成します。説明とエッジケース処理を含む完全な例。
og_title: PFX証明書のロード C# – PKCS7 デタッチド署名の作成
tags:
- C#
- PKCS7
- X509
- Cryptography
title: PFX証明書のロード C# – PKCS7 デタッチド署名の作成
url: /ja/net/programming-with-security-and-signatures/load-pfx-certificate-c-create-pkcs7-detached-signature/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PFX 証明書の読み込み（C#） – PKCS7 デタッチド署名の作成

データに署名するだけのために **C# で PFX 証明書を読み込む** 必要があったことはありませんか？しかし、どこから始めればよいか分からなかったことはありませんか？あなただけではありません—多くの開発者が X.509 証明書や PKCS#7 に初めて触れるときに同じ壁にぶつかります。

良いニュースは？このチュートリアルでは、**C# で PFX 証明書を読み込む**、**PKCS7 デタッチド署名** を作成し、さらにファイルから署名を取り出す方法を示す、すぐに実行できるソリューションを提供します。曖昧な参照はなく、具体的なコードと各行の背後にある理由だけです。

> **得られるもの**  
> * 証明書の読み込みプロセスに関する明確な理解。  
> * PKCS7 デタッチド署名を構築する完全でコンパイル可能なサンプル。  
> * 一般的な落とし穴（パスワード間違い、ファイル欠如、アルゴリズム不一致）への対処法。  

### 前提条件

- .NET 6.0 以降（使用する API は基本クラスライブラリの一部です）。  
- 有効な `.pfx` ファイルとそのパスワード。  
- Visual Studio 2022 またはお好みのエディタ—コア例に特別な NuGet パッケージは不要です。  

これらが揃っていれば、さっそく始めましょう。

---

## PFX 証明書の読み込み（C#） – 手順別解説

以下は必要最低限の `using` ディレクティブです。ファイルの先頭に置いて、コンパイラが型を見つけられるようにします。

```csharp
using System;
using System.IO;
using System.Security.Cryptography;
using System.Security.Cryptography.X509Certificates;
```

### 1️⃣ 証明書のパスとパスワードを指定する

まず、`.pfx` がどこにあるかとパスワードをランタイムに伝えます。デモではパスをハードコーディングしても構いませんが、**決して** 本番コードにパスワードを埋め込んではいけません。

```csharp
// Step 1: Path to your certificate and its password
string certificatePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "certificate.pfx");
string certificatePassword = "yourPassword"; // <-- replace with a secure source
```

> **プロのコツ:** パスワードは Azure Key Vault、AWS Secrets Manager、または環境変数に保存し、ソース管理にコミットしないでください。

### 2️⃣ 証明書を安全に読み込む

`try / catch` ブロックで読み込みをラップし、ファイルが見つからない、パスワードが間違っているといった一般的なエラーを表面化させます。

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

### 3️⃣ **PKCS7 デタッチド署名** オブジェクトを作成する

サードパーティのライブラリで `PKCS7Detached` クラスが公開されていると仮定します（多くの商用 SDK が提供）。先ほど読み込んだ証明書でインスタンス化します。

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

> **なぜコールバックか？** 一部の SDK はハードウェア セキュリティ モジュール（HSM）やリモート署名サービスをプラグインできるようにします。`CustomSignHash` を公開することで、署名ロジックを柔軟に保てます。

### 4️⃣ 署名デリゲートを実装する

以下は、読み込んだ証明書のプライベートキーを使用したシンプルな実装です。必要に応じて `MySigner.Sign` を独自の HSM 呼び出しに置き換えてください。

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

### 5️⃣ 任意のデータに署名し、デタッチド PKCS7 ブロブを取得する

いよいよ実際に署名します。データはファイルでも JSON ペイロードでも、保護したいものなら何でも構いません。

```csharp
// Step 5: Data you want to protect
byte[] dataToSign = File.ReadAllBytes("sample.txt");

// The PKCS7Detached class usually offers a Sign method that returns the raw signature.
byte[] detachedSignature = pkcs7Signer.Sign(dataToSign);

// Save the signature to disk for later verification
File.WriteAllBytes("sample.txt.sig", detachedSignature);

Console.WriteLine("Detached PKCS7 signature created successfully.");
```

**Expected output**

```
Detached PKCS7 signature created successfully.
```

これで **ファイルからの PKCS7 署名**（`sample.txt.sig`）が取得でき、元データとは独立して検証可能になります。

## PKCS7 デタッチド署名の作成 – 詳細オプション

基本的なフローは多くのシナリオで機能しますが、実運用システムでは追加の設定が必要になることがあります。

| 機能 | 有効化方法 | 使用シーン |
|------|------------|------------|
| **アルゴリズム選択** | `HashAlgorithmName.SHA256`（または SHA384/SHA512）を `SignHash` に渡す | コンプライアンスで特定のハッシュが要求される場合 |
| **タイムスタンピング** | 署名後に RFC‑3161 タイムスタンプを付加する | 長期検証のため |
| **複数署名者** | 追加の `PKCS7Detached` インスタンスを作成してマージする | 文書に共同署名が必要なとき |
| **カスタム CMS 属性** | `Sign` 前にライブラリの `AddAttribute` メソッドを使用する | 署名時刻、署名者 ID などを埋め込むため |

以下は SHA‑256 を選択する簡単なスニペットです：

```csharp
CustomSignHash = (hash, _) => MySigner.Sign(hash, HashAlgorithmName.SHA256)
```

## PKCS7 デタッチド署名の検証（オプション）

検証はストーリーのもう片方です。多くのライブラリは元データとデタッチド署名を受け取る `Verify` メソッドを提供しています。

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

別の SDK を使用している場合は、.NET の `System.Security.Cryptography.Pkcs` 名前空間にある `CmsSignedData` または `SignedCms` クラスを探してください—これらもデタッチド署名を扱えます。

## よくある落とし穴と回避方法

1. **パスワードが間違っている** – `CryptographicException` が *“The specified network password is not correct.”* と表示します。パスワードは安全に保管し、証明書を読み込む前に別途テストしてください。  
2. **プライベートキーがない証明書** – `.pfx` がプライベートキーなしでエクスポートされることがあります。CA や Key Vault のエクスポート設定を再確認してください。  
3. **アルゴリズム不一致** – 署名者が SHA‑256 を期待しているのに SHA‑1 を使用すると、検証に失敗します。署名側と検証側でアルゴリズムを揃えてください。  
4. **ファイルパスの問題** – 開発時は相対パスが機能しますが、デプロイ時に壊れやすいです。`Path.Combine(AppDomain.CurrentDomain.BaseDirectory, ...)` や設定駆動の絶対パスを使用することを推奨します。  
5. **プラットフォーム差異** – Windows と Linux ではプライベートキーの保存方法が異なります。`X509KeyStorageFlags.Exportable` を使用すると、ほとんどのクロスプラットフォーム問題を緩和できます。

## 完全動作例（コピー＆ペースト可能）

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