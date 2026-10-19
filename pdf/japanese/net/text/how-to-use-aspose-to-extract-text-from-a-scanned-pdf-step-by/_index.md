---
category: general
date: 2026-08-04
description: Aspose を使用してスキャンされた PDF のテキストを抽出し、C# で PDF をテキストに変換する方法。スキャンされた PDF ファイルの読み取り方法と、信頼できる
  OCR 結果の取得方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use aspose
- extract scanned pdf text
- convert pdf to text
- read scanned pdf
- how to extract text
language: ja
lastmod: 2026-08-04
og_description: Aspose を使用してスキャンされた PDF ファイルを読み取り、テキストを抽出し、PDF をテキストに変換する完全な実行可能サンプル。
og_image_alt: Screenshot showing how to use Aspose OCR copilot to extract text from
  a scanned PDF
og_title: Asposeの使い方 – C#でスキャンされたPDFからテキストを抽出する
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: How to use Aspose to extract scanned PDF text and convert PDF to text
    with C#. Learn to read scanned PDF files and get reliable OCR results.
  headline: How to use Aspose to extract text from a scanned PDF – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: Yes. Add `.WithPassword("yourPassword")` to the options builder before
      creating the copilot.
    question: Does this work with password‑protected PDFs?
  - answer: Use `GetTextStructureAsync()` instead of `GetTextAsync()`. The method
      returns a JSON payload that includes page indices, bounding boxes, and confidence
      scores.
    question: Can I extract text in a structured format (e.g., JSON with page numbers)?
  - answer: 'The plain‑text extraction flattens tables into line‑break‑separated rows.
      For richer data, request the PDF‑to‑HTML conversion (`GetHtmlAsync`) and parse
      the HTML table elements. ## Conclusion You now know **how to use Aspose** to
      read a scanned PDF, extract scanned PDF text, and **convert PDF to tex'
    question: What if the PDF contains tables?
  type: FAQPage
tags:
- Aspose.PDF.AI
- OCR
- C#
- PDF processing
title: Aspose を使用してスキャンされた PDF からテキストを抽出する方法 – ステップバイステップガイド
url: /ja/net/text/how-to-use-aspose-to-extract-text-from-a-scanned-pdf-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose を使ってスキャンされた PDF からテキストを抽出する方法 – ステップバイステップガイド

OCR 用に **Aspose の使い方** が必要な場合、このガイドでは数行の C# でスキャン PDF のテキストを抽出する方法を示します。ドキュメントアーカイブサービスやレガシー書類の検索インデックスを構築する場合でも、Aspose.Pdf.AI サービスに渡す任意のスキャン PDF で動作します。

このチュートリアルで行うこと：

* スキャン PDF を読み取る OCR コパイロットを作成する。
* 認識されたテキストを非同期で抽出する。
* 抽出した文字列を表示またはさらに処理する。

前提条件は、アクティブな Aspose.Pdf.AI サブスクリプションと .NET 6（以降）開発環境があれば完了です。

## 前提条件

| 必要条件 | 理由 |
|-------------|----------------|
| .NET 6 SDK 以上 | `async Main` や最新の言語機能を利用できるため。 |
| Aspose.Pdf.AI NuGet パッケージ（`Aspose.Pdf.AI`） | `AICopilotFactory` と OCR オプションが含まれている。 |
| 有効な Aspose.Pdf.AI `client` インスタンス（API キー） | クラウドサービスへのリクエストを認証するため。 |
| スキャン PDF ファイル（例: `Scanned.pdf`） | テキスト抽出対象となる元ドキュメント。 |

.NET CLI でパッケージをインストールします：

```bash
dotnet add package Aspose.Pdf.AI
```

## 手順 1: Aspose.Pdf.AI クライアントの設定

OCR エンドポイントを呼び出す前に、API 資格情報を保持するクライアントを作成する必要があります。クライアントはスレッドセーフで、複数のドキュメントで再利用できます。

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual API key and base URL if you use a private cloud.
var client = new PdfAiClient(new PdfAiConfiguration
{
    ApiKey = "YOUR_API_KEY",
    // BaseUrl = "https://api.aspose.cloud" // default, change only if needed
});
```

**この手順が必要な理由** – Aspose のサービスは各リクエストをサブスクリプションと照合します。クライアントを一度作成すれば、ネットワークハンドシェイクが繰り返されず、コードもすっきりします。

## 手順 2: スキャン PDF 用 OCR コパイロットの作成

`AICopilotFactory` は、指定したファイルを処理できる専門的な OCR コパイロットを構築します。`client` と PDF パスを指す `OpenAIOcrOptions` オブジェクトを渡します。

```csharp
using Aspose.Pdf.AI;

// Step 2: Build the OCR copilot
var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
    client,                                   // Your Aspose.Pdf.AI client instance
    OpenAIOcrOptions.Create()
        .WithDocument("YOUR_DIRECTORY/Scanned.pdf") // Path to the scanned PDF
);
```

**解説** – `CreateOcrCopilot` は低レベルの HTTP 呼び出しをすべてカプセル化します。`WithDocument` メソッドはサービスに解析対象のファイルを指示します。PDF がメモリ上にある場合は `Stream` を渡すことも可能です。

## 手順 3: 認識テキストを非同期で抽出

`GetTextAsync` を呼び出すと、クラウド上で OCR が実行され、プレーンテキストの結果が返ります。処理に数秒かかる可能性があるため、メソッドは非同期です。

```csharp
// Step 3: Perform OCR and get the text
string ocrText = await ocrCopilot.GetTextAsync();
```

**なぜ非同期か？** – ネットワーク遅延や OCR 処理時間は予測できません。`await` を使用することでメインスレッドがブロックされず、UI や Web サービスシナリオで特に重要です。

## 手順 4: 抽出したテキストの利用

ここまでで、スキャン PDF の全文を書き起こした .NET の `string` が手に入ります。コンソールに出力したり、データベースに保存したり、検索エンジンに投入したりできます。

```csharp
// Step 4: Display the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrText);
```

### 期待される出力

`Scanned.pdf` に「Hello, world!」という文が 1 ページだけ含まれている場合、コンソールは次のように表示します：

```
=== OCR Result ===
Hello, world!
```

複数ページのドキュメントでは、各ページのテキストが連結され、改行が保持されます。

## 完全な実行可能サンプル

以下は新規コンソールプロジェクト（`dotnet new console`）に貼り付けて実行できる完全プログラムです。**Aspose の使い方** を最初から最後まで示し、一般的な落とし穴に対するエラーハンドリングも含んでいます。

```csharp
using System;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

namespace AsposeOcrDemo
{
    class Program
    {
        static async Task Main(string[] args)
        {
            // 1️⃣ Initialize the Aspose.Pdf.AI client
            var client = new PdfAiClient(new PdfAiConfiguration
            {
                ApiKey = "YOUR_API_KEY"
                // BaseUrl = "https://api.aspose.cloud" // optional
            });

            // 2️⃣ Build the OCR copilot for the target PDF
            var pdfPath = "YOUR_DIRECTORY/Scanned.pdf";
            var ocrCopilot = AICopilotFactory.CreateOcrCopilot(
                client,
                OpenAIOcrOptions.Create().WithDocument(pdfPath)
            );

            try
            {
                // 3️⃣ Extract text asynchronously
                string ocrText = await ocrCopilot.GetTextAsync();

                // 4️⃣ Use the extracted text (display in console)
                Console.WriteLine("=== OCR Result ===");
                Console.WriteLine(ocrText);
            }
            catch (Exception ex)
            {
                // Common errors: invalid API key, missing file, unsupported PDF version
                Console.Error.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

**サンプルの重要ポイント**

* `await` によるノンブロッキング実行。
* `try/catch` ブロックでネットワークやサービスエラーを捕捉。大量のスキャン PDF を処理する際に必須です。
* 実行前に `YOUR_API_KEY` と `YOUR_DIRECTORY/Scanned.pdf` を実際の値に置き換えてください。

## エッジケースとベストプラクティス

| シチュエーション | 推奨アプローチ |
|-----------|----------------------|
| **大容量 PDF（ > 50 MB ）** | クライアント側でドキュメントを小さなチャンクに分割し、各チャンクを別々のコパイロットで処理します。メモリ負荷が減り、信頼性が向上します。 |
| **低品質スキャン** | `OpenAIOcrOptions` に `.WithLanguage("eng")` や `.WithEnhanceImage(true)` を追加して OCR 品質を調整します。言語ヒントを指定すると精度が上がります。 |
| **複数言語** | カンマ区切りで指定、例: `.WithLanguage("eng,spa")`。OCR エンジンが両方の言語を検出・文字起こしします。 |
| **PDF 以外の画像ファイル** | まず画像を PDF に変換（`Aspose.Pdf` ライブラリ）するか、`OpenAIOcrOptions.WithImage` で画像を直接送信します。 |
| **レートリミット超過** | 指数バックオフとリトライロジックを実装します。Aspose API はクオータ超過時に HTTP 429 を返します。 |

### プロのコツ

`ocrText` の結果をキャッシュしておくと、後で再利用する際に OCR 処理を繰り返す必要がなくなり、クレジットを節約できます。

## FAQ（よくある質問）

**Q: パスワード保護された PDF でも動作しますか？**  
A: はい。コパイロット作成前にオプションビルダーに `.WithPassword("yourPassword")` を追加してください。

**Q: テキストを構造化フォーマット（例: ページ番号付き JSON）で取得できますか？**  
A: `GetTextAsync` の代わりに `GetTextStructureAsync()` を使用します。ページインデックス、バウンディングボックス、信頼度スコアを含む JSON が返ります。

**Q: PDF に表が含まれている場合はどうなりますか？**  
A: プレーンテキスト抽出では表が改行で区切られた行に平坦化されます。よりリッチなデータが必要な場合は PDF→HTML 変換 (`GetHtmlAsync`) を呼び出し、HTML の table 要素を解析してください。

## 結論

これで **Aspose の使い方** をマスターし、スキャン PDF を読み取り、テキストを抽出し、最小限の C# プログラムで **PDF をテキストに変換** できるようになりました。手順は OCR コパイロットの作成、`GetTextAsync` の呼び出し、取得した文字列の処理です。エッジケースの推奨事項に従えば、大量バッチ、マルチリンガル、セキュア PDF などにもスケールできます。

次に試すべきこと：

* レイアウト保持付きテキスト抽出（`GetHtmlAsync`）  
* Aspose.Pdf.AI を使って **表を抽出** し CSV にエクスポート  
* OCR 出力を Azure Cognitive Search と統合し、検索可能なドキュメントアーカイブを構築  

Happy coding, and enjoy the accuracy that Aspose’s AI‑powered OCR brings to your scanned‑PDF workflows!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法を基にした関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能を習得したり、独自プロジェクトで代替実装を検討したりするのに役立ちます。

- [Extract Text from PDF Files Using Aspose.PDF for .NET](/pdf/english/net/text-operations/extract-text-pdf-aspose-dotnet/)
- [How to Extract Text from Specific Regions in PDFs Using Aspose.PDF for .NET](/pdf/english/net/text-operations/extract-text-specific-region-aspose-pdf-net/)
- [How to Extract Highlighted Text from PDFs Using Aspose.PDF for .NET](/pdf/english/net/text-operations/extract-highlighted-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}