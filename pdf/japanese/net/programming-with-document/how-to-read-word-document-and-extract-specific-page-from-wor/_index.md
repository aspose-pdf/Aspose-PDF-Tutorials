---
category: general
date: 2026-04-12
description: C# を使用して Word 文書を読み込み、特定のページを抽出する方法。ステップバイステップのコードで .docx をロードし、ページ 2
  を取得し、ベーツ・アーティファクトを読み取ります。
draft: false
keywords:
- how to read word document
- extract specific page from word
- C# Word processing
- read .docx page
- document artifact extraction
language: ja
og_description: Word文書の読み取り方法と、特定のページを抽出する完全なC#例。.docxをロードし、ページ2を対象にしてベーツ番号を取得する方法を学びます。
og_title: Word文書の読み取り方法 – C#でWordから特定のページを抽出する
tags:
- C#
- Word
- Document Automation
title: Word文書の読み取りと特定ページの抽出方法 – C#ガイド
url: /ja/net/programming-with-document/how-to-read-word-document-and-extract-specific-page-from-wor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Word ドキュメントの読み取りと特定ページの抽出 – 完全 C# チュートリアル  

プログラムで **Word ドキュメントの読み取り** を行い、必要な部分だけを取得したいと思ったことはありませんか？たとえば、法的ブリーフの 2 ページ目にあるベーツ番号を取得しなければならないケース管理システムを構築しているとします。そのようなシナリオでは、**Word から特定ページを抽出** する際に、毎回ファイル全体をメモリに読み込まないようにする必要があります。  

このガイドでは、実際のシナリオとして `.docx` を読み込み、2 ページ目を選択し、最初の「Bates」アーティファクトを見つけてテキストを出力する方法をステップバイステップで解説します。最終的に、任意の .NET プロジェクトに貼り付けられる自己完結型の実行可能スニペットが手に入ります。曖昧な「ドキュメント参照」ではなく、具体的なコードと *なぜその行が重要か* の説明だけです。

> **学べること**  
> * C# で一般的な SDK を使って Word ドキュメントを読む方法。  
> * **Word から特定ページを抽出** する方法（ゼロベースインデックス使用）。  
> * アーティファクト（例：Bates 番号）を検索し、データが欠落している場合に優雅に対処する方法。  
> * エッジケース、パフォーマンス、さらなる拡張に関するヒント。

## 前提条件  

本題に入る前に、以下を用意してください。

| 要件 | 重要な理由 |
|------|------------|
| .NET 6.0 以上（または .NET Framework 4.7 以上） | 使用する SDK は .NET Standard 2.0+ を対象としています。 |
| Visual Studio 2022（またはお好みの IDE） | デバッグと IntelliSense が容易になります。 |
| **GroupDocs.Annotation for .NET**（または Aspose.Words）を NuGet 経由でインストール | サンプルで使用する `Document`、`Page`、`Artifact` クラスを提供します。 |
| `YOUR_DIRECTORY` フォルダー内に配置したサンプル Word ファイル（`input.docx`） | チュートリアルはこのファイルの存在を前提としています。任意のパスに置き換えても構いません。 |

パッケージは次のように追加できます:

```bash
dotnet add package GroupDocs.Annotation --version 23.10
```

Aspose.Words を選択した場合、API は若干異なりますが、ドキュメントの読み込み、ページコレクションへのアクセス、アーティファクトの走査というコアコンセプトは同じです。

![Word ドキュメントを読み取り、単一ページを抽出する方法を示す図](/images/read-word-document.png){: .center alt="Word ドキュメントを読み取り、単一ページを抽出する方法を示す図"}

## ステップバイステップ実装  

以下では、解決策を論理的なチャンクに分割して説明します。各チャンクは明確な見出し（AI インデックスに最適）と、前のコードに続く短いコードスニペットで構成されています。  

### 1. Word ドキュメントの読み取り – ファイルのロード  

ドキュメント処理コードが最初に行うことは、ファイルを開くことです。GroupDocs.Annotation では、`.docx` のフルパスを渡して `Document` オブジェクトをインスタンス化します。  

```csharp
using GroupDocs.Annotation;
using GroupDocs.Annotation.Models;

// Load the source document (replace YOUR_DIRECTORY with your actual path)
string docPath = Path.Combine("YOUR_DIRECTORY", "input.docx");
Document doc = new Document(docPath);
```

**重要なポイント:**  
* コンストラクタは Word ファイルを解析し、ページ、アノテーション、アーティファクトのインメモリ表現を構築します。  
* ファイルが存在しない、または破損している場合、SDK は説明的な `FileNotFoundException` または `AnnotationException` をスローし、後でキャッチできます。

### 2. Word から特定ページを抽出 – 目的のページへアクセス  

Word ドキュメントはレイアウト依存のため、ネイティブな「ページ」オブジェクトを公開していません。しかし SDK はロード時にドキュメントを `Page` オブジェクトのコレクションにレンダリングします。ページはゼロベースなので、ページ 2 はインデックス 1 です。  

```csharp
// Retrieve the second page (zero‑based index)
int pageIndex = 1; // page 2 in human terms
Page secondPage = doc.Pages[pageIndex];
```

**この処理が必要な理由:**  
* `doc.Pages[1]` に直接アクセスすることで、全体を走査せずに必要なスライスだけを取得できます。  
* ドキュメントのページ数が足りない場合は `IndexOutOfRangeException` がスローされます。後述の「エラーハンドリング」で対策してください。

### 3. Bates アーティファクトの検索 – ページ内を走査  

アーティファクトはページに付随するメタデータオブジェクトで、Bates 番号、コメント、カスタムタグなどの隠しメモと考えてください。ここでは、`Subtype` が `"Bates"` に等しい最初のアーティファクトを探します。

```csharp
// Find the first artifact with subtype "Bates"
Artifact batesArtifact = secondPage.Artifacts
    .FirstOrDefault(a => a.Subtype.Equals("Bates", StringComparison.OrdinalIgnoreCase));
```

**このステップが重要な理由:**  
* `FirstOrDefault` を使用すると、Bates アーティファクトが存在しない場合に安全に `null` が返ります。これにより、ログ出力やデフォルト値設定などの処理を自由に決められます。  
* `StringComparison.OrdinalIgnoreCase` によって、ソース文書内の大文字小文字の違いに対しても堅牢になります。

### 4. アーティファクトテキストの出力 – 安全なコンソール書き込み  

Bates アーティファクトが取得できた（または取得できなかった）ら、テキストをコンソールに表示します。実際のアプリではこのテキストをデータベースに保存したり、別サービスへ送信したりすることになるでしょう。

```csharp
if (batesArtifact != null)
{
    Console.WriteLine($"Current Bates: {batesArtifact.Text}");
}
else
{
    Console.WriteLine("No Bates artifact found on page 2.");
}
```

**期待される結果:**  
ページ 2 に Bates 番号が含まれるドキュメントでプログラムを実行すると、次のように表示されます。

```
Current Bates: 2023-00123
```

アーティファクトが見つからない場合はフォールバックメッセージが表示され、`NullReferenceException` の発生を防ぎます。

### 5. 完全動作サンプル – すべてをまとめる  

以下はコンソールアプリの完全版です。新しい C# プロジェクトにコピー＆ペーストし、NuGet パッケージを復元して **F5** を押すだけで動作します。

```csharp
using System;
using System.IO;
using System.Linq;
using GroupDocs.Annotation;
using GroupDocs.Annotation.Models;

namespace WordPageExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                // 1️⃣ Load the source document
                string docPath = Path.Combine("YOUR_DIRECTORY", "input.docx");
                Document doc = new Document(docPath);

                // 2️⃣ Extract specific page from word (page 2 = index 1)
                int pageIndex = 1;
                if (pageIndex >= doc.Pages.Count)
                {
                    Console.WriteLine($"Document only has {doc.Pages.Count} page(s). Cannot access page {pageIndex + 1}.");
                    return;
                }
                Page secondPage = doc.Pages[pageIndex];

                // 3️⃣ Locate the first Bates artifact on that page
                Artifact batesArtifact = secondPage.Artifacts
                    .FirstOrDefault(a => a.Subtype.Equals("Bates", StringComparison.OrdinalIgnoreCase));

                // 4️⃣ Output the result
                if (batesArtifact != null)
                {
                    Console.WriteLine($"Current Bates: {batesArtifact.Text}");
                }
                else
                {
                    Console.WriteLine("No Bates artifact found on page 2.");
                }
            }
            catch (Exception ex)
            {
                // Pro tip: Log the exception details for troubleshooting
                Console.Error.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

**追加コードの解説:**  

* **境界チェック** – `pageIndex` を `doc.Pages.Count` と比較し、ページ数が足りない場合のクラッシュを防止します。  
* **try‑catch ブロック** – ファイルアクセスエラー、権限問題、SDK 固有例外を捕捉し、ハンドルしやすいエラーメッセージを出力します。  
* **コメント** – インラインコメント（`// 1️⃣`）は視覚的なアンカーとして機能し、コードをざっと見る新人にとって有益です。

### 6. よくあるバリエーションとエッジケース  

| 状況 | コードの適応方法 |
|------|-------------------|
| 同一ページに複数の Bates 番号がある | `Where(...).Select(a => a.Text)` を使ってすべて取得し、ループまたは結合して処理します。 |
| ページ 5 を取得したい | `int pageIndex = 4;` に変更します（ゼロベースであることを忘れずに）。 |
| 別のアーティファクトサブタイプ（例: “Comment”）を使用する | `FirstOrDefault` の述語内の `"Bates"` を `"Comment"` に置き換えます。 |
| 超大型ドキュメントでのパフォーマンス | SDK が遅延ロードをサポートしている場合は `Document.LoadPage(pageIndex)` を使用して必要なページだけを読み込みます。 |
| .NET Core on Linux で実行 | GroupDocs.Annotation のネイティブ依存関係（画像レンダリング用 `libgdiplus` など）をインストールしてください。 |

### 7. Tips & Gotchas  

* **プロのコツ:** バッチ処理で多数のドキュメントを扱う場合、`Annotation` ライセンスインスタンスを 1 つだけ再利用して、ライセンスチェックのオーバーヘッドを削減しましょう。  
* **注意点:** Word ファイルに隠しセクション（例: フットノート）が含まれると、ページインデックスが期待とずれることがあります。  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}