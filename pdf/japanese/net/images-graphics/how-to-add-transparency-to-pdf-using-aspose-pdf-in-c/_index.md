---
category: general
date: 2026-10-17
description: Aspose.PDF for .NET を使用して PDF に透明性を追加し、PDF リソースを編集し、単一の実行可能なサンプルで変更された
  PDF ファイルを保存します。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- save modified pdf
- edit pdf resources
- Aspose.PDF transparency
- C# PDF manipulation
language: ja
lastmod: 2026-10-17
og_description: Aspose.PDF for .NET を使用して PDF に透明性を追加し、PDF リソースを編集し、完全な C# サンプルで変更された
  PDF ファイルを保存します。
og_image_alt: Screenshot showing a PDF with added transparency using Aspose.PDF in
  C#
og_title: Aspose.PDFでPDFに透明性を追加する – ガイド
schemas:
- author: Aspose
  dateModified: '2026-10-17'
  description: Add transparency to PDF with Aspose.PDF for .NET, edit PDF resources,
    and save modified PDF files in a single, runnable example.
  headline: How to add transparency to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- pdf
- aspnet
- csharp
title: C#でAspose.PDFを使用してPDFに透明性を追加する方法
url: /ja/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Aspose.PDF を使用して PDF に透明度を追加する方法

PDF ファイルに **透明度を追加** したい場合は、このガイドで Aspose.PDF for .NET を使った明快なエンドツーエンドの解決策をご紹介します。**PDF リソースの編集**、カスタム グラフィックス ステートの作成、そして **変更した PDF の保存** を C# プロジェクト内だけで完結させる方法を学べます。

PDF の透明度操作は低レベルの PDF 演算子の裏側に隠れていることが多いですが、このチュートリアルを終える頃には、コピー＆ペーストで実行でき、複数ページや別のブレンドモードにも適用できる完全なサンプルが手に入ります。

## 前提条件

- .NET 6.0（またはそれ以降の .NET バージョン）  
- Aspose.PDF for .NET NuGet パッケージ (`Aspose.Pdf`)  
- 基本的な C# の知識  
- `input.pdf` という名前の入力 PDF ファイルを、参照できるフォルダーに配置しておくこと

> **プロのコツ:** 作業を始める前に `dotnet add package Aspose.Pdf` でパッケージをインストールしておきましょう。

## 手順 1: PDF ドキュメントを読み込む

最初の操作はソース PDF を開くことです。Aspose.PDF は PDF を `Document` オブジェクトとして表現し、ページやリソース、低レベルの辞書へアクセスできるようにします。

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Collections;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;   // for graphics‑state objects

// Path to the original PDF
string pdfPath = @"YOUR_DIRECTORY\input.pdf";

// Open the document in a using block so it disposes automatically
using (var document = new Document(pdfPath))
{
    // The rest of the steps are inside this block
```

*ポイント:* この方法でドキュメントを開くと、編集が終わった後にファイルハンドルが解放され、後で **変更した PDF の保存** を行う際のファイルロック問題を防げます。

## 手順 2: 最初のページとそのリソース辞書にアクセスする

PDF ページはグラフィック オブジェクト（フォント、画像、ExtGState エントリ）を *リソース辞書* に格納しています。透明度を変更するには `ExtGState` サブ辞書を操作する必要があります。

```csharp
    // Get the first page (pages are 1‑based in Aspose.PDF)
    Page page = document.Pages[1];

    // Obtain a mutable editor for the page's resources
    var resourcesEditor = new DictionaryEditor(page.Resources);

    // Retrieve the ExtGState dictionary; create it if missing
    var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                         ?? new CosPdfDictionary(document);
```

*ポイント:* 元の PDF にすでに `ExtGState` 辞書が存在すればそれを拡張し、存在しなければ新規に作成して **PDF リソースの編集** を安全に行えるようにします。

## 手順 3: 透明度付きの新しいグラフィックス ステートを構築する

グラフィックス ステート（`ExtGState`）はストローク不透明度 (`CA`)、塗り不透明度 (`ca`)、ブレンドモード (`BM`) などのパラメータを保持します。空の辞書を作成し、目的の値で埋めます。

```csharp
    // Create an empty ExtGState dictionary for the new entry
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

    // Define the transparency entries
    var entries = new[]
    {
        // CA – stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA",
            new CosPdfNumber(1)),

        // ca – fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca",
            new CosPdfNumber(0.5)),

        // BM – blend mode (Normal is the default)
        new KeyValuePair<string, ICosPdfPrimitive>("BM",
            new CosPdfName("Normal"))
    };

    // Add each entry to the new ExtGState dictionary
    foreach (var entry in entries)
        newGraphicsState.Add(entry);
```

*ポイント:* `ca` エントリが **PDF に透明度を追加** する鍵です。数値 (0 – 1) を調整することで、オブジェクトの透過度をコントロールできます。

## 手順 4: グラフィックス ステートをページリソースに挿入する

新しいグラフィックス ステートに名前（例: `"GS0"`）を付ける必要があります。この名前は後でコンテンツ ストリームから参照され、透明度が適用されます。

```csharp
    // Add the new ExtGState under the name "GS0"
    extGStateDict.Add("GS0", newGraphicsState);

    // Ensure the modified ExtGState dictionary is written back to the page
    resourcesEditor["ExtGState"] = extGStateDict;
```

*ポイント:* `"GS0"` を `ExtGState` 辞書に追加することで、このステートを選択した描画操作は定義した不透明度で描画されます。これが **透明度のための PDF リソース編集** の核心です。

## 手順 5: グラフィックス ステートをページコンテンツに適用する（任意）

既存のページコンテンツに自動的に新しい透明度を適用したい場合は、ページのコンテンツ ストリームの先頭にグラフィックス ステート演算子を挿入します。以下のスニペットは、既存コンテンツを `gs`（グラフィックス ステート設定）と `Q`（グラフィックス ステート復元）でラップする方法を示しています。

```csharp
    // Get the current content stream
    var content = page.Contents[1]; // assume a single content stream

    // Build a new stream that sets the graphics state, draws the original content, then restores
    string gsOperator = "/GS0 gs\n"; // select the graphics state we created
    string restoreOperator = "Q\n";   // restore graphics state after drawing

    // Prepend the gs operator and append the restore operator
    string newStream = gsOperator + content.Stream.ToString() + restoreOperator;

    // Replace the original stream with the modified one
    content.Stream = new CosPdfStream(document);
    content.Stream.SetData(newStream);
```

*ポイント:* この手順がないと、ステートは存在しても使用されません。`gs` 演算子を追加することで、PDF レンダラは以降の描画に透明度を適用します。

## 手順 6: **変更した PDF をディスクに保存** する

最後に、変更されたドキュメントを新しいファイルに書き出します。`Save` メソッドがすべての低レベル更新を自動で処理します。

```csharp
    // Path for the output PDF
    string outputPath = @"YOUR_DIRECTORY\output.pdf";

    // Persist the changes
    document.Save(outputPath);
}
```

*ポイント:* `document.Save` 呼び出しにより、更新された **変更した PDF の保存** に新しい `ExtGState` エントリとそれを参照するコンテンツ ストリームが含まれます。結果のファイルでは、1 ページ目の塗りが 50 % の不透明度で表示されます。

## 期待される結果

任意の PDF ビューア（Adobe Reader、Chrome など）で `output.pdf` を開くと、1 ページ目のグラフィックが 50 % の塗り不透明度で描画されているはずです。**PDF‑Tron** や **iText** といったツールで PDF を検査すると、`GS0` という名前の `ExtGState` 辞書エントリがあり、`ca` の値が `0.5` になっていることが確認できます。

## エッジケースとバリエーション

| 状況 | 変更点 |
|-----------|----------------|
| **複数ページ** | `document.Pages` をループし、各ページに対して手順 2‑5 を繰り返す。名前は `GS1`、`GS2` などユニークにする |
| **既存の ExtGState 名が競合** | 追加前に `extGStateDict.ContainsKey("GS0")` をチェックし、存在すれば `("GS" + Guid.NewGuid().ToString("N"))` で新しいキーを生成 |
| **異なるブレンドモード** | `BM` エントリを `"Normal"` から `"Multiply"`、`"Screen"` などに変更 |
| **ストローク不透明度だけが必要** | `ca` エントリを省略するか `1` に設定し、代わりに `CA` を調整 |

## 完全な実行可能サンプル



## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法を基にした関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、API の追加機能を習得したり、独自プロジェクトで代替実装を検討したりするのに役立ちます。

- [Aspose.PDF で PDF に透明度を追加 – 完全 C# ガイド](/pdf/english/net/programming-with-stamps-and-watermarks/add-transparency-to-pdf-with-aspose-pdf-complete-c-guide/)
- [Aspose.PDF for .NET を使用した PDF へのページスタンプ追加方法 – 完全ガイド](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Aspose.PDF for .NET を使用した PDF への画像追加方法 – 完全ガイド](/pdf/english/net/images-graphics/add-images-to-pdfs-using-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}