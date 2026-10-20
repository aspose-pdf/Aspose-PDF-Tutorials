---
category: general
date: 2026-08-14
description: C#でデジタル署名を適用するための署名オプションを作成します。署名の設定方法、カスタムハッシュ関数の実装方法、そしてプログラムで文書に署名する方法を学びます。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create signature options
- custom hash function
- apply digital signature
- how to sign document
- how to configure signature
language: ja
lastmod: 2026-08-14
og_description: C#で署名オプションを作成し、デジタル署名を適用します。このチュートリアルでは、署名の設定、カスタムハッシュ関数の追加、そしてドキュメントへの署名方法をステップバイステップで解説します。
og_image_alt: Code editor view showing C# creation of signature options and document
  signing
og_title: C#で署名オプションを作成 – ステップバイステップのデジタル署名ガイド
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
title: C#で署名オプションを作成する – デジタル署名の完全ガイド
url: /ja/net/programming-with-security-and-signatures/create-signature-options-in-c-full-guide-to-digital-signing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で署名オプションを作成する – デジタル署名の完全ガイド

C# で署名オプションを作成してデジタル署名ワークフローを構成します。このチュートリアルでは、デジタル署名の適用方法、カスタムハッシュ関数の実装方法、そして `SignatureOptions` クラスを使用してドキュメントに署名する方法を示します。.NET アプリケーションから PDF、XML、または任意のバイナリペイロードに署名する必要がある場合、以下の手順で即座に実行可能なソリューションが得られます。

以下を学びます：

* カスタムハッシュアルゴリズムで `SignatureOptions` を構成する方法
* 署名メソッドを正しく呼び出す方法
* 署名が適用されたことを検証する方法
* 署名を構成する際の一般的な落とし穴を回避する方法

必要な前提条件は、最新の .NET SDK（≥ .NET 6）と `SignatureOptions` を提供する署名ライブラリ（例: **GroupDocs.Signature**、**Aspose.Signature**、または類似の API）だけです。外部ツールは必要ありません。

---

## 前提条件

| 要件 | 重要な理由 |
|------|------------|
| .NET 6 SDK or later | サンプルで使用される最新の言語機能を提供します。 |
| A signing‑library NuGet package (e.g., `GroupDocs.Signature`) | `SignatureOptions` 型と `Sign` 拡張メソッドを提供します。 |
| Access to a private key or certificate | 検証可能なデジタル署名を生成するために必要です。 |

標準 CLI でライブラリをインストールします：

```bash
dotnet add package GroupDocs.Signature
```

---

## 手順 1: 署名オプションを作成する

最初のステップは `SignatureOptions` のインスタンスを作成し、署名プロセスを制御するプロパティを設定することです。このオブジェクトはライブラリに対して、*何を* 署名し、*どのように* 署名するかを指示します。

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

**この重要性:** `SignatureOptions` はコードと署名エンジン間の契約として機能します。事前に設定しておくことで、複数のドキュメントに署名する際に繰り返しの定型コードを回避できます。

---

## 手順 2: カスタムハッシュ関数を実装する

*カスタムハッシュ関数* を使用すると、署名アルゴリズムが署名するダイジェストを完全に制御できます。デフォルトのハッシュ（SHA‑256）がコンプライアンス要件を満たさない場合や、ドキュメントの一部だけをハッシュ化したい場合に便利です。

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

**この重要性:** `CustomSignHash` に割り当てることで、ライブラリ内部のハッシュ処理を `MyHash` に置き換えます。署名エンジンは現在、関数が返すバイト列に対して署名を行い、任意のカスタムポリシーへの準拠を保証します。

---

## 手順 3: ドキュメントを読み込みデジタル署名を適用する

オプションが準備できたら、対象ファイルを開き、署名メソッドを呼び出します。`Sign` メソッドはライブラリが提供し、設定された `SignatureOptions` を使用します。

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

**この重要性:** `Sign` の呼び出しは内部で次の 3 つの処理を行います。

1. **ハッシュ計算** – これがカスタムハッシュ関数に委任されます。  
2. **署名生成** – ライブラリの設定で提供されたプライベートキーを使用します。  
3. **埋め込み** – 生成された署名が出力ファイルに付加されます。

いずれかのステップが失敗した場合、メソッドは `false` を返し、エラーを適切に処理できるようにします。

---

## 手順 4: ドキュメントが署名されていることを検証する

簡単な検証により、署名が正しく適用されたことを確認できます。ほとんどのライブラリは署名されたファイルの整合性をチェックする `Verify` メソッドを提供しています。

```csharp
using var verifier = new Signature(outputPath);
var verificationResult = verifier.Verify();

Console.WriteLine(verificationResult
    ? "Signature verified successfully."
    : "Signature verification failed.");
```

**この重要性:** 検証により、署名後にドキュメントが改ざんされていないこと、そしてカスタムハッシュが互換性のあるダイジェストを生成したことが保証されます。

---

## ファイルタイプ別の署名設定方法

同じ `SignatureOptions` オブジェクトを PDF、Word 文書、画像、または単純なバイナリに対して再利用できます。必要な変更は、特定のオプションクラス（例: `PdfSignatureOptions`、`WordSignatureOptions`）だけです。以下は JPEG 画像の簡単な例です。

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

**この重要性:** 各フォーマットごとに *署名を設定* する方法を理解すれば、ハッシュロジックを書き直すことなく、同じコードベースを複数のドキュメントタイプに拡張できます。

---

## よくある落とし穴とベストプラクティス

| 落とし穴 | 推奨される対策 |
|----------|----------------|
| `SignatureOptions` 作成後に `CustomSignHash` を設定し忘れる | オプションオブジェクトを構築した直後にデリゲートを割り当てる。 |
| 署名証明書がサポートしないハッシュアルゴリズムを使用する | 証明書のキー使用目的がハッシュ長と一致しているか確認する（例: RSA‑2048 と SHA‑512）。 |
| `Signature` オブジェクトの破棄が必要であることを見落とす | `Signature` インスタンスを `using` ブロックでラップしてファイルハンドルを解放する。 |
| 署名済みファイルを元のソースに上書き保存する | 常に新しいファイルパス（`outputPath`）に書き込み、元のドキュメントを保持する。 |

---

## 完全な動作例

以下は、すべての要素を組み合わせた自己完結型プログラムです。新しいコンソールプロジェクトにコピーして実行してください。コンソールに成功または失敗が報告されます。

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

**期待される出力**

```
Signature verified successfully.
```

コンソールに “Signing failed.” または “Signature verification failed.” と表示された場合は、証明書の設定を再確認し、カスタムハッシュが期待サイズのバイト配列を返すことを確認してください。

---

## 結論

これで C# で **署名オプションを作成**し、**カスタムハッシュ関数を付与**し、任意のサポート対象ドキュメントに **デジタル署名を適用**する方法が分かりました。本チュートリアルでは、オプションの設定、ファイルへの署名、結果の検証というフルライフサイクルをカバーしました。同じ `SignatureOptions` インスタンスを再利用することで、画像、Word ファイル、または生バイナリに対しても **署名の設定方法** を行うことができます。

---

## 次にやることは？

* `SignatureOptions` の追加プロパティ（ビジュアルスタンプ、タイムスタンプサーバー、証明書チェーンなど）を調査してください – これらは **apply digital signature** キーワードに対応します。  
* `MyHash` 内の実装を差し替えて、他のハッシュアルゴリズム（例: Blake2b）を試してみてください。  
* 署名フローを Web API に統合し、オンザフライでのドキュメント署名を可能にします – これは **how to sign document** のサービス指向アーキテクチャでの自然な拡張です。

ご自身のセキュリティポリシーに合わせてコードを自由に適応させ、コメントで体験を共有してください。署名を楽しんでください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.PDF for .NET で PDF 署名言語を変更する方法](/pdf/english/net/digital-signatures/change-pdf-signature-language-aspose-net/)
- [Aspose PDF .NET デジタル署名チュートリアル（ドイツ語）](/pdf/german/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)
- [Aspose PDF .NET デジタル署名チュートリアル（フランス語）](/pdf/french/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}