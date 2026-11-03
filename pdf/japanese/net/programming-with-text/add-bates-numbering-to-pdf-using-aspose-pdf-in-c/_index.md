---
category: general
date: 2026-09-27
description: C#でAspose.PDFを使用してPDFにベーツ番号付けを追加します。PDFドキュメントの読み込み方法、ベーツ番号付けオプションの設定方法、そして更新されたファイルの保存方法を学びます。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- load pdf document
- how to add bates numbering
- Aspose.PDF C#
- PDF Bates numbering example
language: ja
lastmod: 2026-09-27
og_description: C#でAspose.PDFを使用してPDFにベーツ番号を追加します。このチュートリアルでは、PDFドキュメントの読み込み、ベーツ番号の設定、結果の保存方法を示します。
og_image_alt: Screenshot of a PDF page displaying Bates numbers in the footer
og_title: Aspose.PDFでPDFにベーツ番号付けを追加する – C# ガイド
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Add bates numbering to PDF using Aspose.PDF in C#. Learn how to load
    a PDF document, set Bates numbering options, and save the updated file.
  headline: Add bates numbering to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF processing
title: C#でAspose.PDFを使用してPDFにベーツ番号を付ける
url: /ja/net/programming-with-text/add-bates-numbering-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Aspose.PDF を使用して PDF に Bates 番号を追加する

PDF ファイルに **Bates 番号** を追加する必要がある場合、このガイドでは完全で実行可能なソリューションを示します。**PDF ドキュメントの読み込み**、Bates 番号オプションの設定、そして番号付きファイルを書き戻す方法を、すべて Aspose.PDF for .NET を使用して確認できます。

Bates 番号の適用は、法務、法執行機関、アーカイブのワークフローで一般的です。このチュートリアルの最後までに、各ページに連続した識別子を埋め込み、プレフィックスをカスタマイズし、任意の番号からカウントを開始できるようになります。

## 学習内容

* `Aspose.Pdf.Document` オブジェクトに **PDF ドキュメント** の内容をロードする方法。  
* `BatesNumberingOptions` を使用して **Bates 番号を追加する** 正確な手順。  
* 元のレイアウトと品質を保持したまま、変更されたファイルを保存する方法。  

外部ツールは不要です—Aspose.PDF の NuGet パッケージと .NET 開発環境（Visual Studio、VS Code、または Rider）だけで済みます。  

---

## 手順 1: Aspose.PDF for .NET のインストール

ターミナルでプロジェクトフォルダーを開き、次のコマンドを実行します：

```bash
dotnet add package Aspose.PDF
```

このパッケージには `Aspose.Pdf` 名前空間が含まれており、本チュートリアルで使用するすべてのクラスが提供されます。インストール後、IDE が新しい参照を認識できるようにプロジェクトをリロードしてください。

## 手順 2: PDF ドキュメントのロード

ソースファイルのロードは最初の操作です。Bates 番号エンジンは既存の `Document` インスタンス上で動作するためです。

```csharp
using Aspose.Pdf;

// ...

// Replace with the path to your input PDF
string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Load the PDF document into memory
Document doc = new Document(inputPath);
```

**重要な理由:** `Document` クラスは PDF 構造を解析し、ページ、注釈、メタデータへのアクセスを提供します。ファイルを先にロードしなければ、番号付けを適用できません。

## 手順 3: Bates 番号オプションの設定

`BatesNumberingOptions` オブジェクトを作成し、希望するプレフィックス、開始番号、オプションの書式設定パラメータを設定します。

```csharp
using Aspose.Pdf;

// ...

BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Text that appears before the numeric part
    Prefix = "CASE01",

    // First number to use (1 means the first page gets CASE01-1)
    StartNumber = 1,

    // Optional: customize the appearance
    // The default places the number in the footer, centered.
    // You can change Font, FontSize, Color, and Position if needed.
    // Example:
    // Font = FontRepository.FindFont("Arial"),
    // FontSize = 10,
    // Color = Color.Black,
    // Margin = new Margin(0, 0, 0, 20)
};
```

**重要な理由:** `BatesNumberingOptions` は Aspose.PDF に各ページのラベル生成方法を指示します。`Prefix` は関連するケースをグループ化するのに役立ち、`StartNumber` は前回のバッチからシーケンスを継続することを可能にします。

## 手順 4: Bates 番号を適用した PDF の保存

オプションオブジェクトを `Save` メソッドに渡します。Aspose.PDF は番号を各ページに直接書き込みます。

```csharp
// Replace with the desired output path
string outputPath = @"YOUR_DIRECTORY\output.pdf";

// Save the document, applying the Bates numbering
doc.Save(outputPath, batesOptions);
```

**重要な理由:** オーバーロード `Save(string, BatesNumberingOptions)` はレンダリング工程と番号付けプロセスを組み合わせ、出力ファイルに可視の識別子が含まれることを保証します。

## 完全な例 – すべてをまとめて

以下は、コピーして貼り付け、実行できる単一の自己完結型プログラムです。**Bates 番号を最初から最後まで追加する方法** を示しています。

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the PDF document
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Set up Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                Prefix = "CASE01",
                StartNumber = 1,
                // Optional appearance tweaks:
                // Font = FontRepository.FindFont("Times New Roman"),
                // FontSize = 9,
                // Color = Color.DarkBlue,
                // Margin = new Margin(0, 0, 0, 15)
            };

            // 3️⃣ Save the document with Bates numbers
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath, batesOptions);

            Console.WriteLine($"Bates numbering added. Output saved to: {outputPath}");
        }
    }
}
```

### 期待される出力

プログラムを実行すると、各ページに次のようなラベルが表示された `output.pdf` が生成されます。

```
CASE01-1
CASE01-2
CASE01-3
...
```

番号はデフォルトでフッターに表示されますが、`BatesNumberingOptions` の `Margin` プロパティを調整することで位置を変更できます。

## エッジケースと一般的なバリエーション

| Situation | What to adjust |
|-----------|----------------|
| **バッチごとに異なるプレフィックス** | `Save` を呼び出す前に `Prefix` を変更します。異なるプレフィックスを持つ複数のドキュメントをループ処理できます。 |
| **前のファイルから番号付けを継続** | `StartNumber` を最後に使用した番号 + 1 に設定します。 |
| **ヘッダーに番号を配置** | `batesOptions.Margin = new Margin(20, 0, 0, 0);`（上マージン）を使用するか、`batesOptions.Position` をカスタマイズします。 |
| **カスタムフォントまたはカラー** | コメントセクションに示すように `Font`、`FontSize`、`Color` プロパティを割り当てます。 |
| **大規模 PDF（1000 ページ以上）** | この操作はメモリ効率が高いですが、ファイルサイズを削減するために保存前に `doc.OptimizeResources()` を有効にした方が良い場合があります。 |

**プロのコツ:** ワークフローでドキュメントごとに異なる番号付けスキームが必要な場合、ロジックをヘルパーメソッドにカプセル化します：

```csharp
static void ApplyBatesNumbering(string src, string dst, string prefix, int start)
{
    var doc = new Document(src);
    var opts = new BatesNumberingOptions { Prefix = prefix, StartNumber = start };
    doc.Save(dst, opts);
}
```

## 結論

これで、C# で Aspose.PDF を使用して任意の PDF に **Bates 番号を追加する方法** が分かりました。このチュートリアルでは、PDF ドキュメントのロード、番号オプションの設定、最終ファイルの保存を、単一の実行可能プログラムで行う方法をカバーしました。  

ここからは、**透かしの追加**、**複数 PDF の結合**、または **テキスト抽出** など、Aspose.PDF を使用した関連トピックを探求できます。組織の書式基準に合わせて、さまざまなフォント、色、位置を試してみてください。  

法務文書のワークフローを自動化する準備はできましたか？コードをビルドパイプラインに追加し、ファイルのバッチに対して実行すれば、Aspose.PDF が重い処理を担当します。コーディングを楽しんでください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックをカバーしています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [PDF ドキュメント作成 C# – Bates 番号の追加](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/)
- [PDF に Bates 番号を追加 – PDF ページに番号付けするステップバイステップガイド](/pdf/english/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/)
- [Aspose PDF チュートリアル – 空白ページの挿入と Bates 番号の更新](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}