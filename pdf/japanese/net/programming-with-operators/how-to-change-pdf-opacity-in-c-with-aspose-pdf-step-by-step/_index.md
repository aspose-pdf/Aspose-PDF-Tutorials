---
category: general
date: 2026-10-23
description: C#でAspose.Pdfを使用してPDFの不透明度を変更する方法。ExtGStateを編集し、ストローク/塗りの不透明度を設定し、数行のコードでブレンドモードを適用する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to change PDF opacity
- Aspose.Pdf opacity
- PDF graphics state
- ExtGState dictionary
- C# PDF manipulation
- PDF blend mode
language: ja
lastmod: 2026-10-23
og_description: C#でAspose.Pdfを使用してPDFの不透明度を変更する方法。ストロークと塗りの不透明度を調整し、ブレンドモードを設定して、更新されたドキュメントを保存する簡潔なガイドです。
og_image_alt: Screenshot of a PDF page with semi‑transparent graphics created by Aspose.Pdf
  in C#
og_title: C#でPDFの不透明度を変更する方法 – 完全なAspose.Pdfチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: How to change PDF opacity using Aspose.Pdf in C#. Learn to edit ExtGState,
    set stroke/fill opacity, and apply blend modes in just a few lines of code.
  headline: How to change PDF opacity in C# with Aspose.Pdf – step‑by‑step guide
  type: TechArticle
- description: How to change PDF opacity using Aspose.Pdf in C#. Learn to edit ExtGState,
    set stroke/fill opacity, and apply blend modes in just a few lines of code.
  name: How to change PDF opacity in C# with Aspose.Pdf – step‑by‑step guide
  steps:
  - name: Load the PDF document
    text: '```csharp using Aspose.Pdf;'
  - name: Get the first page and its resource dictionary
    text: '```csharp // Step 2: Get the first page and its resource dictionary var
      firstPage = pdfDocument.Pages[1]; var resourcesEditor = new DictionaryEditor(firstPage.Resources);
      ```'
  - name: Retrieve (or create) the ExtGState dictionary
    text: '```csharp // Step 3: Retrieve the ExtGState dictionary from the page resources
      // If ExtGState does not exist, create an empty one. CosPdfDictionary extGStateDict;
      if (resourcesEditor.ContainsKey("ExtGState")) { extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
      } else { extGStateDic'
  - name: Create a new graphics state dictionary and define opacity entries
    text: '```csharp // Step 4: Create a new graphics state dictionary and define
      its entries var graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
      var graphicsStateEntries = new[] { new KeyValuePair<string, ICosPdfPrimitive>("CA",
      new CosPdfNumber(1.0)), // Stroke opacity (fully opaque)'
  - name: Add the new graphics state to the ExtGState dictionary
    text: '```csharp // Step 5: Add the new graphics state to the ExtGState dictionary
      (named "GS0") extGStateDict.Add("GS0", graphicsStateDict); ```'
  - name: Save the updated PDF document
    text: '```csharp // Step 6: Save the updated PDF document pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
      } ```'
  type: HowTo
tags:
- PDF
- C#
- Aspose.Pdf
- Opacity
- GraphicsState
title: C# と Aspose.Pdf で PDF の不透明度を変更する方法 – ステップバイステップガイド
url: /ja/net/programming-with-operators/how-to-change-pdf-opacity-in-c-with-aspose-pdf-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# と Aspose.Pdf で PDF の透明度を変更する方法 – ステップバイステップガイド

特定の要素の **PDF の透明度を変更する方法** が必要な場合、このチュートリアルでは完全な実行可能なソリューションを示します。ExtGState 辞書の編集、ストロークと塗りの透明度の設定、ブレンドモードの選択方法を、数行の C# コードで確認できます。

PDF の透明度を変更すると、透かしやオーバーレイ画像、微妙な視覚効果を文書全体を作り直すことなく実現できます。本ガイドは、基本的な C# 環境と Aspose.Pdf for .NET ライブラリがインストールされていることを前提としています。

![C# で Aspose.Pdf を使用した PDF 透明度の変更方法](https://example.com/og-image.png)

## 前提条件

* .NET 6.0 以降（コードは .NET Framework 4.7+ でも動作します）
* **Aspose.Pdf for .NET** のライセンス版（無料トライアルでもテスト可能）
* コードから参照できるフォルダーにある入力 PDF ファイル
* Visual Studio 2022 またはお好みの C# エディタ

追加の NuGet パッケージは不要です — Aspose.Pdf には本チュートリアルで使用するすべての型が含まれています。

## PDF グラフィックス状態の理解

PDF ページは描画パラメータを **graphics state** オブジェクトに保存します。**ExtGState** 辞書には次のようなエントリが含まれます。

* **CA** – ストロークの透明度 (0 = 透明, 1 = 不透明)
* **ca** – 塗りの透明度
* **BM** – ブレンドモード (例: *Normal*, *Multiply*, *Screen*)

新しいグラフィックス状態辞書を作成し、ページの ExtGState コレクションに追加することで、後からコンテンツストリームでその状態を参照できます。この手法により、ページ全体を書き換えることなく既存の PDF に適用でき、どの PDF にも対応します。

## Aspose.Pdf を使用した PDF 透明度の変更方法

以下の 6 つの手順で、ドキュメントの読み込みから変更後の保存までの全工程をカバーします。各手順には必要なコードと、なぜその手順が重要かの説明が含まれています。

### 手順 1: PDF ドキュメントの読み込み

```csharp
using Aspose.Pdf;

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

**この点が重要な理由** – `Aspose.Pdf.Document` でファイルを開くと、内部 PDF 構造全体に完全にアクセスでき、**ExtGState** 辞書が存在するページリソースも取得できます。

### 手順 2: 最初のページとそのリソース辞書を取得

```csharp
// Step 2: Get the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

**この点が重要な理由** – 各ページにはフォント、画像、グラフィックス状態をまとめた *Resources* 辞書があります。`DictionaryEditor` はそのコレクションへの読み書きを便利に行えるようにします。

### 手順 3: ExtGState 辞書を取得（または作成）

```csharp
// Step 3: Retrieve the ExtGState dictionary from the page resources
// If ExtGState does not exist, create an empty one.
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

**この点が重要な理由** – 一部の PDF にはすでに **ExtGState** エントリが存在しますが、存在しない場合もあります。条件分岐により、どちらの場合でもチュートリアルが機能し、実務的なファイルにも強固に対応できます。

### 手順 4: 新しいグラフィックス状態辞書を作成し、透明度エントリを定義

```csharp
// Step 4: Create a new graphics state dictionary and define its entries
var graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // Fill opacity (50 % transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

**この点が重要な理由** – 以下の 3 つのキーエントリが描画コマンドの描画方法を制御します。

* `CA = 1.0` はストローク線を完全に表示します。
* `ca = 0.5` は塗りつぶし形状を半透明にします。
* `BM = Normal` はデフォルトのブレンドモードを使用します。クリエイティブな効果を得るには `"Normal"` を `"Multiply"` や `"Screen"` に置き換えることができます。

### 手順 5: 新しいグラフィックス状態を ExtGState 辞書に追加

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary (named "GS0")
extGStateDict.Add("GS0", graphicsStateDict);
```

**この点が重要な理由** – エントリ名を `"GS0"` とすることで、後でコンテンツストリーム内で `/GS0 gs` と参照できるようになります。複数の透明度バリエーションが必要な場合は、`"GS1"`、`"GS2"` など別名で追加し、`CA`/`ca` の値を変えてください。

### 手順 6: 更新された PDF ドキュメントを保存

```csharp
// Step 6: Save the updated PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

**この点が重要な理由** – 変更を永続化することで、修正された **ExtGState** 辞書がファイルに書き込まれます。結果として生成された PDF には、任意の描画コマンドが呼び出せる再利用可能なグラフィックス状態が含まれます。

## 新しいグラフィックス状態をページコンテンツに適用

上記の手順はグラフィックス状態を作成するだけです。実際にページのコンテンツストリームで参照する必要があります。以下は、先ほど追加した状態を使用して半透明の矩形を描画する簡単な例です。

```csharp
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    var page = pdfDocument.Pages[1];
    var content = new PageContentEditor(page);
    // Begin the graphics state GS0
    content.InsertContent(0, "q /GS0 gs\n"); // Save graphics state and apply GS0
    // Draw a rectangle (100,100) to (300,300)
    content.InsertContent(0, "0.2 0.6 0.8 rg\n"); // Set fill color (light blue)
    content.InsertContent(0, "100 100 200 200 re\n");
    content.InsertContent(0, "f\n"); // Fill rectangle with current fill opacity
    // Restore graphics state
    content.InsertContent(0, "Q\n");
    pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

**説明** – `q` 演算子で現在のグラフィックス状態を保存し、`/GS0 gs` で透明度設定を適用、矩形を描画し、`Q` で元の状態に復元します。このスニペットはページ上の任意の位置（既存コンテンツの前後）に配置でき、必要なビジュアルレイヤリングに合わせて使用できます。

## よくある落とし穴と回避方法

| 症状 | 原因 | 対策 |
|---------|-------|-----|
| 透明度が変わらない | ページに ExtGState エントリがない、またはコンテンツが新しい状態を参照していない | `ExtGState` が存在すること、コンテンツストリームに `/GS0 gs`（または選択した名前）が含まれていることを確認してください。 |
| ブレンドモードが効果を示さない | 互換性のないカラースペースまたは PDF バージョンを使用している | PDF バージョンが少なくとも 1.4（透明度が必要）であること、スポットカラーとブレンドモードを混在させていないことを確認してください。 |
| 古いビューアでドキュメントが開けない | PDF 1.3 以前では透明度がサポートされていない | 保存前に `pdfDocument.Version = 1.4;` を設定するか、PDF バージョンを明示的にアップグレードしてください。 |

## 結果のテスト

`output.pdf` を Adobe Acrobat Reader、Foxit、または任意の最新 PDF ビューアで開きます。矩形が塗りの 50 % 透明度で描画され、枠線は完全に不透明であることが確認できるはずです。*Edit → Preferences → Accessibility* のオプションで「高コントラスト色を使用する」を切り替えて、半透明効果が持続するかどうかも確認してください。

プログラムで検証したい場合は、Aspose.Pdf を使ってグラフィックス状態を再取得できます。

```csharp
var gs = pdfDocument.Pages[1].Resources["ExtGState"]["GS0"].ToCosPdfDictionary();
var fillOpacity = ((CosPdfNumber)gs["ca"]).Value; // Should be 0.5
```

## 手法の拡張

* **複数の透明度レベル** – `"GS1"`、`"GS2"` など別エントリを追加し、`ca` の値を変えて必要に応じて参照します。  
* **異なるブレンドモード** – `"Normal"` を `"Multiply"` や `"Screen"` に置き換えて、芸術的なオーバーレイ効果を実現します。  
* **画像への適用** – XObject 画像を描画する `Do` 演算子の直前で同じグラフィックス状態を使用します。

これらのバリエーションにより、ラスタライズせずに透かしやハイライト、複雑なビジュアルデザインを PDF に組み込むことができます。

## 結論

これで **C# で Aspose.Pdf を使用して PDF の透明度を変更する方法** が分かりました。カスタムグラフィックス状態を作成し、ページの ExtGState 辞書に追加し、コンテンツストリームで呼び出すことで、ストロークと塗りの透明度およびブレンドモードを細かく制御できます。完全なサンプルはそのままコピーして実行でき、あらゆる PDF 操作シナリオに適用可能です。

次のチャレンジに挑みますか？この手法を画像の **Aspose.Pdf opacity** と組み合わせたり、**PDF blend mode** 効果を探求してプロフェッショナルなオーバーレイを作成してみてください。ハッピーコーディング！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、追加の API 機能を習得したり、プロジェクトで代替実装を検討したりするのに役立ちます。

- [Aspose.PDF で PDF の透明度を変更 – 完全な C# ガイド](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Aspose.Pdf を使用した C# で PDF の透明度を変更 – ステップバイステップガイド](/pdf/english/net/programming-with-pdf-pages/change-opacity-pdf-in-c-with-aspose-pdf-step-by-step-guide/)
- [Aspose.Pdf を使用した C# で PDF の透明度を変更する方法](/pdf/english/net/programming-with-operators/how-to-change-pdf-transparency-in-c-using-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}