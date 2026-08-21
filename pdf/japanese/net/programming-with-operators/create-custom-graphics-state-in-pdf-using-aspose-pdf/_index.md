---
category: general
date: 2026-08-20
description: Aspose.Pdf を使用して PDF にカスタム グラフィックス状態を作成します。PDF のリソースを編集し、数ステップで透過 PDF
  を追加する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom graphics state
- edit pdf resources
- add transparency pdf
- Aspose.Pdf graphics state
- PDF resource dictionary
language: ja
lastmod: 2026-08-20
og_description: Aspose.Pdf を使用して PDF にカスタム グラフィックス ステートを作成します。このチュートリアルでは、PDF リソースの編集方法と透明度を迅速に追加する方法を示します。
og_image_alt: Screenshot of C# code that creates a custom graphics state in a PDF
og_title: PDFでカスタム グラフィックス ステートを作成 – Aspose.Pdf ガイド
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create custom graphics state in PDF with Aspose.Pdf. Learn how to edit
    PDF resources and add transparency PDF in just a few steps.
  headline: Create custom graphics state in PDF using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- Aspose.Pdf
- C#
- Graphics state
title: Aspose.Pdf を使用して PDF にカスタム グラフィックス ステートを作成する
url: /ja/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf を使用して PDF でカスタム グラフィックス ステートを作成する

PDF で **カスタム グラフィックス ステートを作成** する必要がある場合、このガイドでは Aspose.Pdf for .NET を使用して正確に行う方法を示します。チュートリアルの最後までに、**PDF リソースを編集** し、新しいグラフィックスステート辞書を注入し、C# プロジェクトから離れることなく **透明度 PDF を追加** できるようになります。

完全な実行可能サンプル、各行が重要である理由の説明、マルチページ文書や異なるブレンドモードの処理に関するヒントが確認できます。外部ツールは不要で、Aspose.Pdf ライブラリと基本的な .NET 開発環境だけで済みます。

## 前提条件

* .NET 6.0 以降（コードは .NET Framework 4.7+ でも動作します）
* ライセンス版 **Aspose.Pdf for .NET**（無料トライアルはテストに使用可能）
* `input.pdf` という名前の入力 PDF ファイルを、コードから参照できるフォルダーに配置します
* Visual Studio 2022 または C# 開発をサポートする任意の IDE

このチュートリアルは、基本的な C# 構文と PDF ページの概念に慣れていることを前提としています。

## 手順 1: ソース PDF を読み込み、最初のページにアクセスする

最初の操作は PDF ファイルを開き、リソースを変更したいページを取得することです。Aspose.Pdf は各ページを `Page` オブジェクトとして表し、各ページにはグラフィックスステート、フォント、XObject などを格納する **リソース辞書** が含まれています。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

// Load the PDF you want to edit
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Get the first page (pages are 1‑based in Aspose.Pdf)
    Page firstPage = pdfDocument.Pages[1];
```

*重要性:* `Document` クラスはファイルをメモリにロードし、`Pages[1]` は最初のページのリソース辞書へ直接アクセスでき、そこにグラフィックスステートが格納されています。

## 手順 2: リソース辞書を編集用に開く

Aspose.Pdf は `DictionaryEditor` ヘルパーを提供し、リソース辞書を通常の .NET `Dictionary` のように扱うことができます。これにより、`ExtGState` などのエントリを読み取り、追加、または置換することが簡単になります。

```csharp
    // Create an editor for the page’s resources
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*重要性:* `DictionaryEditor` は低レベルの COS オブジェクトを抽象化し、PDF の準拠性を保ちつつ、慣れ親しんだキー/バリューのペアで作業できるようにします。

## 手順 3: ExtGState 辞書を取得（または作成）

**ExtGState** エントリはページのすべての外部グラフィックスステートオブジェクトを保持します。辞書が存在しない場合、Aspose.Pdf が空の辞書を作成します。

```csharp
    // Ensure the ExtGState dictionary exists
    var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
        ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
        : new CosPdfDictionary(pdfDocument);
```

*重要性:* `ExtGState` エントリが欠如していると、後で `KeyNotFoundException` が発生します。このチェックにより、これまでカスタムグラフィックスステートを定義したことがない PDF に対してもコードが動作し、**edit PDF resources** の堅牢性の重要な部分となります。

## 手順 4: カスタム グラフィックス ステート辞書を構築する

グラフィックスステートは描画操作がどのようにレンダリングされるかを記述します。**add transparency PDF** を行うには、`ca`（塗りつぶし不透明度）と `CA`（ストローク不透明度）エントリを設定し、必要に応じてブレンドモード（`BM`）を指定します。以下のコードはこれらのパラメータで新しい辞書を構築します。

```csharp
    // Create an empty dictionary that will become the new graphics state
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Define the parameters you want for the custom state
    var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
    {
        // Stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        // Fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        // Blend mode – "Normal" is the default, but you can use "Multiply", "Screen", etc.
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };

    // Populate the dictionary with the parameters
    foreach (var param in graphicsStateParams)
        newGraphicsState.Add(param);
```

*重要性:* `ca` と `CA` エントリはそれぞれ塗りつぶしとストローク操作の透明度を制御します。`BM` を設定すると、さまざまな合成効果を試すことができ、後で半透明の形状や画像などの **add transparency PDF** コンテンツを追加する際に便利です。

## 手順 5: 新しいグラフィックスステートを一意の名前で登録する

`ExtGState` 辞書内のすべてのグラフィックスステートは一意の名前（例: `GS0`、`GS1`）を持つ必要があります。既存のエントリと衝突しない任意の名前を選択できます。

```csharp
    // Choose a name that is unlikely to collide with existing states
    const string graphicsStateName = "GS0";

    // Add the new graphics state to the ExtGState dictionary
    extGStateDict.Add(graphicsStateName, newGraphicsState);

    // If the ExtGState entry was missing, attach it back to the page resources
    if (!resourcesEditor.ContainsKey("ExtGState"))
        resourcesEditor["ExtGState"] = extGStateDict;
```

*重要性:* 新しい辞書を `GS0` の下に挿入することで、ページのコンテンツストリームからステートにアクセスできるようになります。条件ブロックは、最初に `ExtGState` が存在しなかった PDF に対してもエントリが確実に存在するようにし、**edit PDF resources** のもう一つの保護策となります。

## 手順 6: ページコンテンツでカスタム グラフィックスステートを使用する（オプション）

前の手順はグラフィックスステートを *定義* しただけです。実際に効果を確認するには、ページのコンテンツストリームでそれを参照する必要があります。以下は、先ほど作成したステートを使用して半透明の矩形を描画する簡単な例です。

```csharp
    // Get the page’s content stream (or create a new one if empty)
    var content = firstPage.Contents[1];
    var graphics = new ContentWriter(content);

    // Save current graphics state
    graphics.WriteOperator(OperatorName.SaveState);
    // Set the custom graphics state we just defined
    graphics.WriteOperand($"/{graphicsStateName}");
    graphics.WriteOperator(OperatorName.SetExtGState);
    // Draw a rectangle (coordinates are in points)
    graphics.WriteOperand(100);   // lower‑left x
    graphics.WriteOperand(500);   // lower‑left y
    graphics.WriteOperand(200);   // width
    graphics.WriteOperand(100);   // height
    graphics.WriteOperator(OperatorName.Rectangle);
    // Fill the rectangle using the current fill opacity (ca = 0.5)
    graphics.WriteOperator(OperatorName.Fill);
    // Restore the previous graphics state
    graphics.WriteOperator(OperatorName.RestoreState);
```

*重要性:* `SetExtGState` 演算子（`gs`）は PDF レンダラに `GS0` で定義されたパラメータを適用するよう指示します。矩形は塗りつぶし不透明度 50 % で表示され、ストロークは完全に不透明のままです。

## 手順 7: 変更された PDF を保存する

最後に、変更をディスクに書き戻します。元のファイルを上書きすることも、新しいファイルを作成することもできます。

```csharp
    // Save the updated PDF
    pdfDocument.Save("YOUR_DIRECTORY/output_with_custom_gs.pdf");
}
```

`output_with_custom_gs.pdf` を PDF ビューアで開くと、最初のページに半透明の矩形が表示されます。これは、**create custom graphics state**、**edit PDF resources**、**add transparency PDF** のコンテンツを正常に実行できたことを確認するものです。

## 一般的なバリエーションとエッジケース

| 状況 | 調整方法 |
|-----------|----------------|
| **複数ページで同じステートが必要** | グラフィックスステートを一度だけ登録（手順 1‑5）し、任意のページのコンテンツストリームで `GS0` を参照します。 |
| **要素ごとに異なる不透明度** | 異なる `ca`/`CA` 値を持つ追加のステート（`GS1`、`GS2`、…）を定義し、`SetExtGState` を使用してそれらを切り替えます。 |
| **Normal 以外のブレンドモード** | `BM` エントリで `"Normal"` を `"Multiply"`、`"Screen"`、または任意の PDF 標準ブレンドモードに置き換えます。 |
| **名前の衝突** | 追加する前に `extGStateDict.ContainsKey(yourName)` を確認し、必要に応じて一意のサフィックスを選択します。 |
| **PDF にすでに ExtGState 辞書が存在する** | 手順 3 のコードは既存の辞書を再利用しているため、追加の処理は不要です。 |

**Pro tip:** 大きな PDF を扱う場合は、`Document` の使用を `using` ブロックでラップ（上記参照）してネイティブリソースを速やかに解放してください。また、リソース編集後に PDF/A や PDF/X の適合性を保証する必要がある場合は、Aspose.Pdf の `PdfCompliance` プロパティを有効にすることを検討してください。

## 完全な動作例



## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説付きの完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose で PDF を作成する方法 – フォームフィールドとページの追加](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Aspose.PDF .NET を使用して PDF にカスタムテーブルを作成する方法](/pdf/english/net/tables-lists/create-custom-tables-in-pdfs-aspose-pdf-dot-net/)
- [Aspose Pdf Net でカスタム PDF スタンプを作成する](/pdf/hongkong/net/images-graphics/create-custom-pdf-stamps-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}