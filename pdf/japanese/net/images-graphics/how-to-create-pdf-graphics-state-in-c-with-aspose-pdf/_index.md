---
category: general
date: 2026-11-16
description: Aspose.Pdf を使用して C# で PDF グラフィックスステートの作成方法を学びましょう。このガイドでは不透明度、ブレンドモード、完全なコード例を取り上げています。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf graphics state
- Aspose.Pdf ExtGState
- PDF opacity
- C# PDF manipulation
- PDF blend mode
- Aspose.Pdf graphics state
language: ja
lastmod: 2026-11-16
og_description: Aspose.Pdf を使用して C# で PDF のグラフィックスステートを作成します。プログラムで不透明度とブレンドモードを設定する完全なチュートリアルをご覧ください。
og_image_alt: Illustration of how to create PDF graphics state with Aspose.Pdf in
  C#
og_title: C#でPDFグラフィックスステートを作成する – ステップバイステップ Aspose.Pdf ガイド
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to create PDF graphics state in C# using Aspose.Pdf. This
    guide covers opacity, blend mode, and full code example.
  headline: How to create PDF graphics state in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF
title: Aspose.Pdf を使用して C# で PDF グラフィックスステートを作成する方法
url: /ja/net/images-graphics/how-to-create-pdf-graphics-state-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# と Aspose.Pdf で PDF グラフィックスステートを作成する方法

.NET プロジェクトで **PDF グラフィックスステートを作成** したい場合、このチュートリアルでは Aspose.Pdf を使用した手順を詳しく解説します。不透明度の制御、ブレンドモードの変更、ページ間でカスタムグラフィックスステートを再利用したい場合でも、以下の手順で実行可能な完全なソリューションが得られます。

このガイドでは、ページリソースへのアクセス方法、**ExtGState** エントリの追加方法、変更を新しいファイルに保存する手順を学びます。例は Aspose.Pdf 23.12（以降）で動作し、.NET 6+ を対象としていますが、概念は以前のバージョンでも適用できます。

## 前提条件

開始する前に以下を用意してください。

* .NET 6 SDK がインストールされた Visual Studio 2022（または任意の C# IDE）。  
* Aspose.Pdf for .NET のライセンスまたは一時的な評価キー。  
* コードから参照できるフォルダーに配置した `input.pdf` という名前の PDF ファイル。  

`Aspose.Pdf` 以外の NuGet パッケージは必要ありません。

## チュートリアルでカバーする内容

* 既存の PDF ドキュメントの読み込み。  
* 1 ページ目のリソース辞書へのナビゲーション。  
* ストローク不透明度（`CA`）、塗りつぶし不透明度（`ca`）、ブレンドモード（`BM`）を定義する新しいグラフィックスステート辞書の作成。  
* カスタム名（`GS0`）で **ExtGState** コレクションに新しいグラフィックスステートを追加。  
* 更新した PDF を保存し、以降の描画コマンドで新しいステートを参照できるようにする。

チュートリアルの最後まで実施すれば、**PDF グラフィックスステート** オブジェクトをプログラムで作成し、任意の描画操作で再利用できるようになります。

## 手順 1: プロジェクトのセットアップと名前空間のインポート

新しいコンソールアプリケーションを作成する（または既存プロジェクトにコードを統合する）。Aspose.Pdf への参照を追加し、必要な名前空間をインクルードします。

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Generator;
```

> **プロのコツ:** 無料評価版を使用している場合は、ドキュメントを読み込む前に `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` を追加して、透かしメッセージを回避してください。

## 手順 2: PDF ドキュメントの読み込み

ファイルのオープンはシンプルです。`Document` クラスは PDF 全体を表し、ページやリソースへのアクセスを提供します。

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";

using (var document = new Document(inputPath))
{
    // All subsequent steps run inside this using block
```

`using` ブロック内でコードを実行すると、操作後にファイルハンドルが解放されます。これは本番環境での **C# PDF 操作** において重要です。

## 手順 3: 1 ページ目のリソース辞書を取得

すべての PDF ページは *Resources* 辞書を持ち、フォント、画像、グラフィックスステートなどが格納されています。この構造を編集するには `DictionaryEditor` が必要です。

```csharp
    // Step 3: Get the first page and its resources dictionary
    var page = document.Pages[1];
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

PDF に既に `ExtGState` エントリが存在する場合、`resourcesEditor["ExtGState"]` がそれを返します。存在しない場合は、最初のエントリを追加したときに Aspose.Pdf が空の辞書を自動生成します。

## 手順 4: ExtGState 辞書へのアクセスまたは作成

**ExtGState** 辞書は名前付きグラフィックスステートオブジェクトを保持します。既存のものを取得するか、新しいコンテナを作成します。

```csharp
    // Step 4: Access (or create) the ExtGState dictionary within the resources
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

`ExtGState` が存在しないときは、`resourcesEditor["ExtGState"]` が自動的に空の辞書を返すため、どの PDF に対してもコードが機能します。

## 手順 5: 新しいグラフィックスステート辞書を構築

グラフィックスステートは特定のキーを持つ `CosPdfDictionary` です。

* `CA` – ストローク不透明度（0‑1）  
* `ca` – 塗りつぶし不透明度（0‑1）  
* `BM` – ブレンドモード（`Normal`, `Multiply` など）

空の辞書を作成し、キーと値を設定した後、`ExtGState` に追加します。

```csharp
    // Step 5: Create a new graphics state dictionary with desired parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (50% transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };

    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

`0.5` の部分は `0` から `1` の任意の値に変更でき、`"Normal"` は `"Multiply"` など別の **PDF ブレンドモード** に置き換えられます。この柔軟性が **Aspose.Pdf グラフィックスステート** のハンドリングにおいてカスタムステート作成が強力なテクニックとなる理由です。

## 手順 6: グラフィックスステートに名前を登録

PDF コンテンツストリームは名前でグラフィックスステートを参照します。ここでは `GS0` を使用していますが、ユニークであれば任意の名前で構いません。

```csharp
    // Step 6: Add the new graphics state to the ExtGState dictionary with a name (e.g., GS0)
    extGState.Add("GS0", newGraphicsState);
```

複数のステートが必要な場合は、パラメータを変えて作成手順を繰り返し、`GS1`, `GS2` などとして追加してください。このパターンは、異なるレイヤーで不透明度やブレンド設定を変える複雑なドキュメントに適しています。

## 手順 7: 変更済み PDF の保存

最後に、更新したドキュメントを新しいファイルに書き出します。元のファイルを残しておくことでデバッグが容易になります。

```csharp
    // Step 7: Save the updated PDF document
    string outputPath = @"YOUR_DIRECTORY\output.pdf";
    document.Save(outputPath);
}
```

実行後、`output.pdf` には `GS0` という名前の `ExtGState` エントリが含まれます。以降の描画演算子は `gs` 演算子（例: コンテンツストリーム内の `GS0 gs`）でこのステートを参照できます。  

> **重要性:** 再利用可能なグラフィックスステートを作成することで、各描画コマンドごとに不透明度やブレンド設定を繰り返す必要がなくなり、パフォーマンスと保守性が向上します。

## コンテンツストリームで新しいグラフィックスステートを使用する（任意）

効果をすぐに確認したい場合は、作成したステートを使用したシンプルな矩形を追加できます。

```csharp
using (var document = new Document(outputPath))
{
    var page = document.Pages[1];
    var content = page.Contents[1]; // Get the first content stream

    // Insert graphics state selection and a semi‑transparent rectangle
    var operators = new List<Operator>
    {
        new Operator("GS0", "gs"),                     // Select our custom graphics state
        new Operator("0.5", "w"),                      // Set line width (optional)
        new Operator("100", "100", "200", "150", "re"), // Rectangle (x, y, width, height)
        new Operator("B")                              // Stroke the rectangle
    };

    foreach (var op in operators)
        content.Operators.Add(op);

    document.Save(@"YOUR_DIRECTORY\final_output.pdf");
}
```

この矩形は塗りつぶし不透明度が 50 % で描画され、ストロークは完全に不透明のままです。**PDF グラフィックスステートを作成** した辞書通りの表示になります。

## よくある落とし穴と回避策

| 問題 | 発生理由 | 対策 |
|------|----------|------|
| `ExtGState` エントリが見つからない | 一部の PDF は辞書自体を持たないことがある。 | `DictionaryEditor` は最初のエントリ追加時に自動で辞書を作成するため、追加チェックは不要。 |
| 不透明度の値が 1 より大きい、または 0 未満 | PDF 仕様で不透明度は `[0,1]` に限定されている。 | `CosPdfNumber` を作成する前に値をクランプする。 |
| ブレンドモードのタイプミス | PDF のブレンドモード名は大文字小文字を区別する。 | `"Normal"`, `"Multiply"`, `"Screen"` など正確な名前を使用。 |
| ライセンス透かし | 評価版は最初のページに透かしを付加する。 | ドキュメントを開く前に有効なライセンスファイルを適用する。 |

これらのエッジケースに対処すれば、**PDF グラフィックスステートの作成** 実装はさまざまな PDF ソースで確実に動作します。

## 完全な実行可能サンプル

以下はコピー＆ペーストで実行できる自己完結型プログラムです。`YOUR_DIRECTORY` を実際のフォルダー パスに置き換えてください。



## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、API の追加機能を習得したり、独自プロジェクトで代替実装を検討したりする際に役立ちます。

- [Create custom graphics state in PDF using Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Add graphics state to PDF using Aspose.PDF for .NET (C#)](/pdf/english/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/)
- [How to create empty graphics state in a PDF with C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}