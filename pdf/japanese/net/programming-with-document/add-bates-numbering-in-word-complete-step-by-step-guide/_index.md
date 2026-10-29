---
category: general
date: 2026-06-21
description: Wordでベーツ番号付けをすばやく追加。ベーツ番号の付け方を学び、法務文書にベーツ番号を適用し、C#で番号付けを自動化する方法。
draft: false
keywords:
- add bates numbering
- how to add bates
- bates numbering in word
- bates numbering for legal
- apply bates numbering
language: ja
og_description: C# を使用して Word にベーツ番号を追加する。このガイドでは、ベーツ番号の追加方法、法的文書へのベーツ番号の適用方法、そしてプロセスの自動化について説明します。
og_title: Wordでベーツ番号付けを追加 – 完全プログラミング解説
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  headline: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  name: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: '| Page | Bates Number | |------|--------------| | 1 | ABC-1000 | | 2 |
      ABC-1001 | | … | … | | N | ABC‑(1000 + N‑1) |'
  - name: What if the document already contains page numbers?
    text: The `AddBatesNumbering` method will **not** overwrite existing page number
      fields; it simply adds a new field. If you want to replace the existing numbers,
      remove them first or set `batesOptions.Position` to the same location as the
      current page numbers.
  - name: Can I skip pages (e.g., exclude a cover page)?
    text: 'Yes. Use the overload that accepts a `PageRange`:'
  - name: How do I change the numbering format (Roman numerals, letters)?
    text: 'The `BatesNumberingOptions` class supports a `NumberFormat` property:'
  - name: What about performance on huge files?
    text: Loading a 2‑GB Word file can consume a lot of RAM. To mitigate, process
      the document in chunks using the `DocumentSplitter` utility, apply Bates numbering
      to each chunk, then merge the parts back together. This pattern keeps memory
      usage under control while still letting you **apply bates numbering*
  type: HowTo
tags:
- document‑automation
- csharp
- legal‑tech
title: Wordでベーツ番号付けを追加する – 完全ステップバイステップガイド
url: /ja/net/programming-with-document/add-bates-numbering-in-word-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wordでベーツ番号付与を追加 – 完全ステップバイステップガイド

Wordファイルにベーツ番号を手動で入力せずに追加する方法を考えたことはありませんか？ あなたは一人ではありません。多くの弁護士、パラリーガル、e‑discovery の専門家は、数百ページに **ベーツ番号を追加** する信頼できる方法を必要としており、手作業は悪夢です。

このチュートリアルでは、`.docx` ファイルに **ベーツ番号を適用** するクリーンな C# ソリューションを解説し、各行がなぜ重要かを説明し、法務向けのニーズに合わせてコードを調整する方法を示します。最後まで読めば、プラグイン不要で数秒で完璧に番号付けされた文書を生成できるようになります。

## 学べること

- Word 文書に **ベーツ番号を追加** するために必要な正確なコード。
- `BatesNumberingOptions` クラスの仕組みと、プレフィックスや開始値を調整する理由。
- 大規模な訴訟ファイルでこの手法を使用する際のメモリ上の考慮点。
- 前提条件の簡単な概要。コピー＆ペーストしてすぐに実行可能です。

**前提条件**  
- .NET 6+（または旧ランタイムを好む場合は .NET Framework 4.7.2+）。  
- Aspose.Words for .NET ライブラリへの参照（または `AddBatesNumbering` を提供する類似 API）。  
- C# と Visual Studio（またはお好みの IDE）に関する基本的な知識。

これらに慣れているなら、さっそく始めましょう。

## 手順 1: プロジェクトのセットアップとライブラリのインポート

まず、コンソールアプリを新規作成（または既存サービスに統合）し、Aspose.Words の NuGet パッケージを追加します。

```bash
dotnet add package Aspose.Words
```

> **プロのコツ:** テスト用には無料評価ライセンスを使用してください。小さな透かしが入りますが、機能はフルバージョンと同等です。

```csharp
using Aspose.Words;
using Aspose.Words.BatesNumbering;
```

これらの `using` 文は、後で **ベーツ番号を適用** する際に必須となる `Document` と `BatesNumberingOptions` クラスをスコープに持ち込みます。

## 手順 2: ソース文書の読み込み

作業対象となる Word ファイルが必要です。以下のコードは、指定したフォルダーから `input.docx` を読み込みます。`"YOUR_DIRECTORY"` を実際のパスに置き換えてください。

```csharp
// Step 1: Load the source document
var document = new Document("YOUR_DIRECTORY/input.docx");
```

なぜ最初にファイルを読み込むのか？ `Document` オブジェクトは Word パッケージ全体をメモリに展開し、ヘッダー・フッターやページレイアウトを保存前に操作できるようにします。もしファイルが巨大（例: 10,000 ページ）であれば、`LoadOptions` と `LoadFormat.Docx` を使用してセクション単位でストリーミングすることを検討してください。

## 手順 3: ベーツ番号オプションの設定

ここが魔法の部分です。プレフィックス（例では `"ABC-"`）と開始番号（`1000`）をライブラリに指示します。両方とも自由にカスタマイズ可能です。

```csharp
// Step 2: Define Bates numbering options (prefix and starting number)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",
    Start = 1000,
    // Optional: set the position, alignment, and font if you need legal‑specific styling
    // Position = BatesNumberingPosition.Footer,
    // Alignment = BatesNumberingAlignment.Right,
    // Font = new Font("Times New Roman", 10, FontStyle.Bold)
};
```

**プレフィックスが必要な理由** は、法務実務ではケースや作成者を識別するために使用されます（例: `"ABC-"` は *Acme Bank Corp.* を表すことがあります）。開始番号を `1000` にするのは、内部ドラフト用に最初の 999 番号を確保する企業が多いためです。

**法務文書向けのベーツ番号** を扱う場合は、`batesOptions.Position` を `Header` または `Footer` に設定し、裁判所の規則に合わせて配置を調整するとよいでしょう。これらの調整はライブラリが標準でサポートしています。

## 手順 4: 文書全体にベーツ番号を適用

いよいよ番号を注入します。`AddBatesNumbering` メソッドはすべてのページを走査し、フォーマットされた文字列を挿入し、内部ページカウントを更新します。

```csharp
// Step 3: Apply Bates numbering to the entire document
document.AddBatesNumbering(batesOptions);
```

内部的には、Aspose.Words が各ページに隠しフィールドを作成し、`ABC-1000`、`ABC-1001` といった形で表示します。フィールドなので、後からプレフィックスや開始番号を変更してもファイル全体を再生成する必要がなく、**discovery 要求が変わった後のベーツ番号追加** に便利です。

## 手順 5: 変更後の文書を保存

最後に、出力を新しいファイルに書き出します。元のファイルをそのまま残すことは、証拠としての完全性を保つ上でベストプラクティスです。

```csharp
// Step 4: Save the modified document
document.Save("YOUR_DIRECTORY/output.docx");
```

これで `output.docx` に、すべてのページに連番ベーツ番号が付与されました。Word で開くと、指定した位置（デフォルトはフッター）に番号が表示されます。フィールドが追加されるためファイルサイズは若干増加しますが、メリットに比べれば無視できる程度です。

### 期待される出力

| ページ | ベーツ番号 |
|------|--------------|
| 1    | ABC-1000     |
| 2    | ABC-1001     |
| …    | …            |
| N    | ABC‑(1000 + N‑1) |

Word の「フィールドコード」ビュー（`Alt+F9`）を開くと、各ページに `{ BATES \* MERGEFORMAT ABC-1000 }` のようなコードが表示されます。

## 境界ケースとよくある質問

### 文書にすでにページ番号がある場合は？

`AddBatesNumbering` メソッドは既存のページ番号フィールドを上書きせず、単に新しいフィールドを追加します。既存の番号を置き換えたい場合は、事前に削除するか、`batesOptions.Position` を現在のページ番号と同じ位置に設定してください。

### 特定のページ（例: 表紙）を除外したい場合は？

はい。`PageRange` を受け取るオーバーロードを使用します：

```csharp
var range = new PageRange(2, document.PageCount); // start at page 2
document.AddBatesNumbering(batesOptions, range);
```

タイトルページ以降で **法務ブリーフ向けベーツ番号** を付与したいときに便利です。

### 番号形式（ローマ数字、アルファベット）を変更したい場合は？

`BatesNumberingOptions` クラスは `NumberFormat` プロパティを提供しています：

```csharp
batesOptions.NumberFormat = BatesNumberFormat.RomanUpper;
```

`AddBatesNumbering` を呼び出す前に設定してください。裁判所が特定のスタイルを要求する場合に役立ちます。

### 超大型ファイルのパフォーマンスは？

2 GB の Word ファイルを読み込むと大量の RAM を消費します。対策としては、`DocumentSplitter` ユーティリティで文書をチャンクに分割し、各チャンクにベーツ番号を適用してから再度結合する方法があります。このパターンによりメモリ使用量を抑えつつ、**ベーツ番号を効率的に適用** できます。

## 完全動作サンプル

すべてをまとめた、すぐに実行できるコンソールプログラムは以下です：

```csharp
using System;
using Aspose.Words;
using Aspose.Words.BatesNumbering;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            var inputPath = @"C:\Docs\input.docx";
            var document = new Document(inputPath);

            // 2️⃣ Define Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                // Optional styling for legal compliance
                Position = BatesNumberingPosition.Footer,
                Alignment = BatesNumberingAlignment.Right,
                Font = new Font("Times New Roman", 9, FontStyle.Bold)
            };

            // 3️⃣ Apply Bates numbering across all pages
            document.AddBatesNumbering(batesOptions);

            // 4️⃣ Save the result
            var outputPath = @"C:\Docs\output.docx";
            document.Save(outputPath);

            Console.WriteLine($"✅ Bates numbering applied! Saved to {outputPath}");
        }
    }
}
```

プログラムを実行し、`output.docx` を開くと、提出・ディスカバリー・裁判所への提出に適したクリーンな番号列が確認できます。

## 結論

C# を使って Word 文書に **ベーツ番号を追加** する方法が完全に理解できました。ロード、設定、適用、保存のステップはシンプルでありながら、**法務向けベーツ番号** のワークフロー、カスタムプレフィックス、さらには大規模バッチ処理にも柔軟に対応できます。

さらに踏み込むなら、次のような拡張を検討してください：

- 同僚がファイルをアップロードして即座に番号付き PDF を受け取れるよう、コードを Web API に統合。  
- ファイル未存在や権限エラーに対するエラーハンドリング（`Document.Load` を `try/catch` で囲む）を追加。  
- Aspose.Words の透かしや赤字消去機能を活用し、フルスイートの e‑discovery ツールキットを構築。

プレフィックスや開始番号を変えてみたり、同一文書内で複数の番号付与スキームを組み合わせてみたり、自由に実験してみてください。**ベーツ番号の適用** は、コアロジックを手に入れれば意外に多彩に活用できます。

質問や難しいシナリオがあれば、下のコメントで教えてください。一緒にトラブルシュートしましょう。ハッピーコーディング！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法を応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、API の追加機能や代替実装アプローチをマスターするのに役立ちます。

- [Java で PDF の見出しに番号スタイルを適用](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Java で PDF の見出しに番号スタイルを適用（ドイツ語）](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Java で PDF の見出しに番号スタイルを適用（フランス語）](/pdf/french/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}