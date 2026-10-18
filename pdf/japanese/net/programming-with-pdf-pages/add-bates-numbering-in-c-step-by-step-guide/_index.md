---
category: general
date: 2026-03-27
description: C#でバテス番号付けをすばやく追加する。カスタムページ番号の追加方法、連続ページ番号の追加方法、Word文書へのカスタム番号の追加方法を学びましょう。
draft: false
keywords:
- add bates numbering
- how to add bates
- add custom page numbers
- add sequential page numbers
- add custom numbers
language: ja
og_description: C#でベーツ番号付けを追加する、分かりやすい例付き。このガイドでは、カスタムページ番号の追加、連続ページ番号の追加などを紹介します。
og_title: C#でベーツ番号付けを追加 – 完全チュートリアル
tags:
- C#
- Document Processing
- Bates Numbering
title: C#でベーツ番号付けを追加 – ステップバイステップガイド
url: /ja/net/programming-with-pdf-pages/add-bates-numbering-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# でベーツ番号を追加する – ステップバイステップガイド

Word 文書に **ベーツ番号** を追加したいけど、手間がかかって困っていませんか？ 法務やコンプライアンスのプロジェクトでは、ページごとにユニークな識別子が必要になることが多く、手作業で行うのは大変です。  

このチュートリアルでは、**ベーツ番号を追加** する完全な実行可能サンプルを通して、数行のコードで **ベーツを追加** する方法、さらに **カスタムページ番号を追加** したり **連続ページ番号を追加** したりする方法を解説します。最後には、サードパーティツールを使わずに希望の番号が付いた .docx ファイルが手に入ります。

## 学べること

- Aspose.Words for .NET API（または互換ライブラリ）を使って DOCX ファイルを読み込む方法。  
- プレフィックス、開始値、フォントサイズなど **カスタム番号を追加** する設定方法。  
- 1 回の呼び出しで全ページに番号付与を適用する方法。  
- 結果を保存し、番号が期待通りに表示されているか確認する手順。  

ベーツ番号の経験は不要です。C# の基本的な環境とソース文書があればすぐに始められます。さあ、始めましょう。

## 前提条件

- .NET 6+（コードは .NET Core と .NET Framework のどちらでも動作します）。  
- NuGet でインストールした Aspose.Words for .NET（`Install-Package Aspose.Words`）。  
- `input.docx` という名前の Word 文書を、参照できるフォルダー（`YOUR_DIRECTORY`）に配置しておくこと。  
- Visual Studio、VS Code、またはお好みの C# IDE。  

> **プロのコツ:** 別のライブラリ（例: Open XML SDK）を使用する場合でも概念は同じです。API 呼び出しだけ差し替えてください。

## 手順 1: ソース文書を読み込む

まず Word ファイルをメモリにロードします。

```csharp
using Aspose.Words;

// Step 1: Load the source document
Document document = new Document("YOUR_DIRECTORY/input.docx");
```

*重要ポイント:* ファイルを読み込むことで `Document` オブジェクトが生成され、ページやセクション、低レベルのノードツリーにアクセスできるようになります。これがないと番号付与はできません。

## 手順 2: ベーツ番号オプションを設定する

次に、番号の見た目を正確に定義します。ここで **カスタムページ番号を追加** や **連続ページ番号を追加** します。

```csharp
// Step 2: Define Bates numbering options (prefix, start number, font size)
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Prefix that appears before every number, e.g., "ABC"
    Prefix = "ABC",
    // The first number in the sequence; change to 1 if you prefer
    Start = 1000,
    // Font size in points; 9 works well for most legal docs
    FontSize = 9
};
```

*重要ポイント:* `Prefix` でケース ID などの **カスタム番号** を付与でき、`Start` がカウンタの開始値を決めます。`FontSize` を変更すれば、ページ余白に番号がはみ出すのを防げます。

## 手順 3: 全ページにベーツ番号を適用する

オプションが準備できたら、ライブラリに各ページへスタンプを付けるよう指示します。

```csharp
// Step 3: Apply Bates numbering to all pages of the document
document.Pages.AddBatesNumbering(batesOptions);
```

*重要ポイント:* `AddBatesNumbering` メソッドは内部のページコレクションを走査し、デフォルト位置（右下）にテキストボックスを挿入します。これが **ベーツを追加** する際に自前でループを書く必要がない核心部分です。

## 手順 4: 更新された文書を保存する

最後に、変更済みファイルをディスクに書き出します。

```csharp
// Step 4: Save the updated document
document.Save("YOUR_DIRECTORY/output.docx");
```

*重要ポイント:* 保存により新しい `output.docx` が生成され、Word、LibreOffice、または任意のビューアで番号が正しく表示されているか確認できます。

## 期待される結果

`output.docx` を開くと、各ページに次のような表示が出ます。

```
ABC‑1000   (on page 1)
ABC‑1001   (on page 2)
ABC‑1002   (on page 3)
...
```

印刷プレビューで確認すれば、設定したフォントサイズで右下隅に番号が表示されているはずです。

## エッジケースとバリエーション

| 状況 | 変更点 | 理由 |
|-----------|----------------|-----|
| **プレフィックスが不要** | `Prefix = string.Empty` | 「ABC‑」部分が除かれ、数字だけのシーケンスになります。 |
| **開始番号を 1 にしたい** | `Start = 1` | カスタムプレフィックスなしで **連続ページ番号を追加** したいときに便利です。 |
| **大容量文書（>10,000 ページ）** | `FontSize` を大きくするか `Location` を調整（`AddBatesNumbering` のオーバーロード使用） | フッターやヘッダーと重なるのを防げます。 |
| **読み取り専用のソースファイル** | 書き込み可能な `LoadOptions` で開く、または事前にコピーする | `document.Save` が例外を投げるのを回避します。 |
| **配置を変えたい** | `batesOptions.Position = BatesNumberingPosition.TopLeft`（他の enum も可） | 企業によってはページ上部に番号が必要な場合があります。 |

> **注:** すべてのライブラリが `BatesNumberingOptions` クラスを提供しているわけではありません。Open XML SDK を使う場合は `TextBox` を手動で挿入しますが、原理は同じでコード量が増えるだけです。

## 完全動作サンプル

以下が全体プログラムです。コンソールアプリに貼り付けて実行してください。

```csharp
using System;
using Aspose.Words;

class Program
{
    static void Main()
    {
        // Load the source document
        Document document = new Document("YOUR_DIRECTORY/input.docx");

        // Define Bates numbering options
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC",      // custom prefix
            Start = 1000,        // starting number
            FontSize = 9         // font size in points
        };

        // Apply numbering to every page
        document.Pages.AddBatesNumbering(batesOptions);

        // Save the result
        document.Save("YOUR_DIRECTORY/output.docx");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

プログラムを実行し、`output.docx` を開くと、期待通りの位置に番号が付いているはずです 🎉

## よくある質問

**Q: 番号の色を変えることはできますか？**  
A: はい。`AddBatesNumbering` 後に生成された `Shape` オブジェクトを取得し、`FillColor` プロパティを設定します。

**Q: 右側ではなく左側に番号を付けたい場合は？**  
A: `batesOptions.Position = BatesNumberingPosition.BottomLeft`（または `TopLeft`, `TopRight`）を使用します。API は四隅すべてに対応しています。

**Q: PDF 出力でも同様に機能しますか？**  
A: もちろんです。番号付与後に `document.Save("output.pdf")` とすれば、Word と同様に PDF にも番号が描画されます。

## 結論

これで C# を使って Word ファイルに **ベーツ番号を追加** する方法が分かりました。チュートリアルでは、文書の読み込み、**カスタム番号を追加**、**連続ページ番号を追加**、そして最終的な保存までを網羅しました。フルコードサンプルがあるので、任意のプロジェクトにすぐ組み込んで文書にスタンプを押すことができます。

次のステップに挑戦してみませんか？ フォルダー内の複数ファイルを一括処理するバッチプロセッサと組み合わせたり、ヘッダー/フッターに **カスタムページ番号を追加** してより洗練されたレイアウトを実現したりしてください。どちらにしても、法務テックやコンプライアンス自動化タスクの強固な基盤が手に入ります。

質問や面白いユースケースがあればコメントで教えてください。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}