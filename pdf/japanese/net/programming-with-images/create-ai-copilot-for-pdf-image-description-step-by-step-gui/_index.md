---
category: general
date: 2026-08-04
description: PDFファイルの画像説明を生成するAIコパイロットを作成します。OpenAI の画像オプションの設定方法と、画像説明を効率的に抽出する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create AI copilot
- generate image description
- image description PDF
- OpenAI image options
- extract image description
language: ja
lastmod: 2026-08-04
og_description: PDFファイルの画像説明を生成するAIコパイロットを作成します。このチュートリアルでは、OpenAI の画像オプションを設定し、コパイロットを実行して、C#
  で画像説明を抽出する方法を示します。
og_image_alt: Screenshot of C# code that creates an AI copilot for PDF image description
og_title: PDF画像説明用AIコパイロットの作成 – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create AI Copilot to generate image description for PDF files. Learn
    how to configure OpenAI image options and extract image description efficiently.
  headline: Create AI Copilot for PDF image description – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Pdf.AI
- C#
- PDF processing
title: PDF画像説明用AIコパイロットの作成 – ステップバイステップガイド
url: /ja/net/programming-with-images/create-ai-copilot-for-pdf-image-description-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF 画像説明用 AI コパイロットの作成 – 完全ガイド

PDF に埋め込まれた画像の説明文を自動で生成する **AI コパイロット** を作成したい方へ。本ガイドでは、OpenAI の画像オプションの設定方法、コパイロットの実行方法、そして **画像説明の抽出** を C# プロジェクト内で完結させる手順を詳しく解説します。

PDF 画像のテキスト化は、アクセシビリティ向上、コンテンツインデックス作成、レポート自動化などでよく求められる要件です。本チュートリアルを終える頃には、任意の PDF に対して **画像説明を生成** できる再利用可能コンポーネントが手に入ります。

## 前提条件

開始する前に、以下を用意してください。

* .NET 6.0 以降がインストール済み  
* Aspose.Pdf.AI のライセンス（または無料トライアル）  
* Aspose クライアントが使用できる OpenAI API キー  
* Visual Studio 2022（または C# に対応した任意の IDE）  

`Aspose.Pdf.AI` 以外に追加の NuGet パッケージは必要ありません。

## 手順 1: Aspose.Pdf.AI クライアントの設定

まず、認証情報を使って AI クライアントをインスタンス化します。クライアントは裏で OpenAI サービスとの通信を担当します。

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual credentials
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    // Optional: set a custom endpoint if you use Azure OpenAI
    // Endpoint = "https://my-openai-instance.openai.azure.com/"
});
```

**ポイント:** `AiClient` はリクエストレベルの設定（API キー、タイムアウト、リトライポリシー）をすべてカプセル化します。一度作成して複数のコパイロットで再利用すれば、オーバーヘッドが削減され、認証が一貫します。

## 手順 2: 画像説明コパイロットの作成

次に、PDF を読み取り各画像の説明を生成する **AI コパイロット** を作成します。`CreateImageDescriptionCopilot` ファクトリーメソッドは、クライアントと説明生成のオプションを受け取ります。

```csharp
// Configure OpenAI image options – this is where you control model, temperature, etc.
var imageOptions = OpenAIImageDescriptionOptions.Create()
    .WithModel("gpt-4o-mini")           // Choose a model that balances cost and quality
    .WithTemperature(0.7)               // Controls creativity; 0 = deterministic
    .WithMaxTokens(150);                // Maximum length of each description

// Point the copilot at the PDF you want to process
var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
    client,
    imageOptions.WithDocument(@"C:\Reports\AnnualReport.pdf"));
```

**ポイント:**  
* `OpenAIImageDescriptionOptions`（**OpenAI 画像オプション**）で言語モデルを細かく調整できます。温度やモデルを変更すれば、技術図と自然写真で適切な関連性が得られます。  
* ドキュメントパスを指定すると、コパイロットはどの PDF を走査すべきか把握します。コパイロットはすべてのラスター画像を抽出し、モデルに送信して人間が読める説明を返します。

## 手順 3: 非同期で生成された説明を取得

画像データは数メガバイトになることがあり、モデルの応答を待つ必要があるため、コパイロットは非同期で動作します。`await` を使って呼び出しが完了するまで待ち、結果にアクセスしてください。

```csharp
try
{
    // Get a dictionary where the key is the page number and the value is the description
    var descriptionMap = await imgCopilot.GetDescriptionAsync();

    // Example: iterate over each image description
    foreach (var entry in descriptionMap)
    {
        Console.WriteLine($"Page {entry.Key}: {entry.Value}");
    }
}
catch (AiException ex)
{
    Console.Error.WriteLine($"AI service error: {ex.Message}");
}
```

**ポイント:** メソッドは `Dictionary<int, string>` を返し、ページ（または画像インデックス）と説明文を紐付けます。`AiException` を捕捉すれば、ネットワークエラーやクォータ超過をアプリケーションのクラッシュなしにハンドリングできます。

## 手順 4: 説明文の表示または保存

説明文はコンソール、ログファイル、あるいはアクセシビリティ用の alt‑text として PDF に埋め込むことが可能です。以下は出力を JSON ファイルに書き出す簡易例です。

```csharp
using System.Text.Json;

// Serialize the map to JSON
var json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
File.WriteAllText(@"C:\Reports\ImageDescriptions.json", json);

Console.WriteLine("Image descriptions saved to ImageDescriptions.json");
```

**ポイント:** JSON で保存すれば、ページと説明の対応関係が保持され、検索インデックスや UI 表示などの下流プロセスがデータを容易に利用できます。

## ページ内に複数画像がある場合の処理

1 ページに複数画像が含まれると、コパイロットは改行で区切った結合説明を返します。`\n\n`（ダブル改行）で分割すれば個別の説明に分離できます。以下はヘルパーメソッドの例です。

```csharp
static IEnumerable<string> SplitDescriptions(string combined)
{
    return combined.Split(new[] { "\n\n" }, StringSplitOptions.RemoveEmptyEntries);
}
```

必要に応じて各画像説明を個別に処理・保存できます。

## エッジケース: 大容量 PDF とタイムアウト管理

100 MB 超の PDF はデフォルトの HTTP タイムアウトを超える可能性があります。`AiClient` 作成時にタイムアウト設定を伸ばしましょう。

```csharp
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    Timeout = TimeSpan.FromMinutes(5)   // Increase timeout for heavy workloads
});
```

タイムアウトを延長すれば、高解像度画像が多数ある場合でもサービス側での処理が途中で中断されません。

## プロのコツ: 結果をキャッシュしてコスト削減

OpenAI はトークン単位で課金されますが、同一レポートのバージョン間で画像説明が重複することがあります。JSON 出力をハッシュと共に保存し、PDF のハッシュが既存と一致したら AI 呼び出しをスキップすることで費用と実行時間を削減できます。

```csharp
static string ComputeFileHash(string path)
{
    using var sha256 = System.Security.Cryptography.SHA256.Create();
    using var stream = File.OpenRead(path);
    var hash = sha256.ComputeHash(stream);
    return Convert.ToHexString(hash);
}
```

ハッシュと JSON をペアで保存し、次回以降同じハッシュが検出されたらキャッシュ結果を再利用します。

## 完全に動作するサンプル

すべてを統合した、.NET プロジェクトに貼り付け可能なコンソールアプリの例です。

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Text.Json;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

class Program
{
    static async Task Main()
    {
        // 1️⃣ Initialize AI client
        var client = new AiClient(new AiClientOptions
        {
            ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
            Timeout = TimeSpan.FromMinutes(5)
        });

        // 2️⃣ Configure OpenAI image options and create copilot
        var imageOptions = OpenAIImageDescriptionOptions.Create()
            .WithModel("gpt-4o-mini")
            .WithTemperature(0.7)
            .WithMaxTokens(150);

        string pdfPath = @"C:\Reports\AnnualReport.pdf";

        var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
            client,
            imageOptions.WithDocument(pdfPath));

        // 3️⃣ Retrieve descriptions
        Dictionary<int, string> descriptionMap;
        try
        {
            descriptionMap = await imgCopilot.GetDescriptionAsync();
        }
        catch (AiException ex)
        {
            Console.Error.WriteLine($"Error from AI service: {ex.Message}");
            return;
        }

        // 4️⃣ Output results
        foreach (var entry in descriptionMap)
        {
            Console.WriteLine($"Page {entry.Key}:");
            Console.WriteLine(entry.Value);
            Console.WriteLine(new string('-', 40));
        }

        // 5️⃣ Save to JSON for later use
        string json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
        string jsonPath = Path.ChangeExtension(pdfPath, ".descriptions.json");
        await File.WriteAllTextAsync(jsonPath, json);
        Console.WriteLine($"Descriptions saved to {jsonPath}");
    }
}
```

**期待される出力（抜粋）**

```
Page 2:
A bar chart showing quarterly revenue growth, with blue bars representing Q1–Q4.
----------------------------------------
Page 5:
A high‑resolution photograph of the new manufacturing facility, showing the assembly line in operation.
...
Descriptions saved to C:\Reports\AnnualReport.descriptions.json
```

このプログラムは `AnnualReport.pdf` を読み込み、**AI コパイロット** を作成し、各ページの生成された説明を JSON ファイルに書き出します。

## よくある質問

* **暗号化された PDF でも動作しますか？**  
  はい。コパイロット作成時にパスワードを指定してください:  
  `imageOptions.WithPassword("mySecret")`。

* **特定のページだけを処理したい場合は？**  
  `imageOptions.WithPageRange(1, 10)` を使用すれば、1〜10 ページに限定できます。

* **画像にテキストが含まれている場合は？**  
  モデルは視覚的内容の説明を試みます。OCR のようにテキスト抽出が必要な場合は `CreateTextExtractionCopilot` を利用してください。

## 結論

これで **AI コパイロット** を作成し、PDF ファイル向けに **画像説明を生成** し、**OpenAI 画像オプション** を設定し、C# で **画像説明を抽出** する方法が分かりました。サンプルは非同期処理、エラーハンドリング、結果キャッシュといったベストプラクティスを示しています。

次に挑戦できること:

* 生成した説明を PDF の alt‑text として埋め込み、アクセシビリティを向上させる（`PdfDocument` → `PdfImage.AlternativeText`）。  
* 同様のコパイロットパターンでバッチ処理向け **画像説明 PDF レポート** を生成する。  
* 異なる OpenAI モデルや温度設定を試し、説明スタイルを微調整する。

コードを自由にカスタマイズし、大容量ドキュメントで実験し、インデックスパイプラインに組み込んでみてください。Happy coding!

## 次に学ぶべきこと

本ガイドで示したテクニックを応用できる、関連チュートリアルをご紹介します。各リソースは完全なコード例とステップバイステップの解説を含んでおり、API の追加機能習得や代替実装アプローチの探求に役立ちます。

- [Create Pdf With Tagged Image In Java](/pdf/hindi/java/pdf-structure-elements/create-pdf-with-tagged-image-in-java/)
- [Create Pdf With Tagged Image](/pdf/hindi/net/programming-with-tagged-pdf/create-pdf-with-tagged-image/)
- [Create Tagged Pdf Image Dotnet](/pdf/hindi/net/images-graphics/create-tagged-pdf-image-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}