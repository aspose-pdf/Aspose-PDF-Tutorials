---
category: general
date: 2026-10-13
description: Aspose.Pdf for C# を使用して PDF の透明度を設定する方法を学びます。また、変更した PDF の保存方法と塗りつぶしアルファの変更方法もご覧ください。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set transparency
- save modified pdf
- change fill alpha
- set fill opacity
- edit pdf resources
language: ja
lastmod: 2026-10-13
og_description: Aspose.Pdf for C# を使用して PDF の透明度を設定する方法。PDF リソースを編集し、塗りつぶしのアルファ値を変更し、変更された
  PDF ファイルを保存する手順をご覧ください。
og_image_alt: Screenshot of a PDF page showing transparent graphics applied with Aspose.Pdf
  in C#
og_title: Aspose.Pdf C# を使用して PDF の透明度を設定する方法 – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  headline: How to set transparency in a PDF with Aspose.Pdf C#
  type: TechArticle
- description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  name: How to set transparency in a PDF with Aspose.Pdf C#
  steps:
  - name: Load the PDF document
    text: '```csharp using Aspose.Pdf; using System.Collections.Generic;'
  - name: Edit PDF resources to add a graphics state
    text: '```csharp // Get the first page (pages are 1‑based) Page firstPage = pdfDocument.Pages[1];'
  - name: Change fill alpha and set fill opacity
    text: '```csharp // Create an empty graphics state dictionary CosPdfDictionary
      newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);'
  - name: Add the new graphics state to the ExtGState dictionary
    text: '```csharp // Register the new state under the name "GS0" extGStateDict.Add("GS0",
      newGraphicsState); ```'
  - name: (Optional) Apply the graphics state in a content stream
    text: 'If you want to draw a rectangle using the new fill opacity, add the following
      after the previous steps:'
  - name: Save modified PDF
    text: '```csharp // Persist the changes to a new file pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
      ```'
  - name: Next steps
    text: '* Explore other blend modes (`Multiply`, `Screen`, etc.) by changing the
      `BM` entry. * Adjust stroke alpha (`CA`) to create semi‑transparent outlines.
      * Combine multiple graphics states to build a library of reusable visual effects.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- Transparency
title: Aspose.Pdf C# を使用して PDF の透明度を設定する方法
url: /ja/net/images-graphics/how-to-set-transparency-in-a-pdf-with-aspose-pdf-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf C# で PDF の透明度を設定する方法

C# を使用して PDF の透明度を設定する必要がある場合、このチュートリアルでは正確な手順を示します。また、Aspose.Pdf 環境から離れることなく、変更した PDF ファイルの保存方法や塗りつぶしアルファの変更方法も学べます。

このガイドでは、ドキュメントの読み込み、PDF リソースの編集、塗りつぶし不透明度を定義するグラフィックスステートの作成、そして変更の永続化までを順に解説します。外部ツールは不要で、すべて標準的な .NET プロジェクト内で実行できます。

## 前提条件

* .NET 6.0 以降がインストールされていること  
* 有効な Aspose.Pdf for .NET ライセンス（または無料評価キー）  
* 既知のディレクトリに配置された入力 PDF ファイル  

NuGet を使用して Aspose.Pdf パッケージを追加できます:

```bash
dotnet add package Aspose.Pdf
```

## PDF で透明度を設定する方法

このセクションではコア実装を示します。各ステップはコードが必要な **理由** を説明し、単に **何を** するかだけではありません。

### 手順 1: PDF ドキュメントをロードする

```csharp
using Aspose.Pdf;
using System.Collections.Generic;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*このステップの理由は？*  
`Document` はメモリ上の PDF 全体を表します。ファイルを開くことで、ページ、リソース、そして変更対象となる低レベルオブジェクトにアクセスできます。

### 手順 2: PDF リソースを編集してグラフィックスステートを追加する

```csharp
// Get the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];

// Create an editor for the page's resource dictionary
DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);

// Retrieve the ExtGState dictionary; it holds graphics state objects
CosPdfDictionary extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
```

*このステップの理由は？*  
PDF ページは、フォント、画像、グラフィックスステートなどの再利用可能オブジェクトをリソース辞書に格納します。`ExtGState` エントリには透明度設定が含まれます。この辞書を編集することで、ページが参照できる新しいステートを導入できます。

### 手順 3: 塗りつぶしアルファを変更し、塗りつぶし不透明度を設定する

```csharp
// Create an empty graphics state dictionary
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the graphics state entries
var graphicsStateEntries = new[]
{
    // Stroke alpha (CA) – fully opaque
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    // Fill alpha (ca) – 50 % transparent
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // Blend mode (BM) – normal composition
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

// Populate the new graphics state
foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*このステップの理由は？*  
`ca` は **塗りつぶし不透明度** を制御し、`CA` は **線の不透明度** を制御します。`ca` を `0.5` に設定すると、塗りつぶされた形状が 50 % 透明になります。`BM` エントリはブレンドモードを選択し、標準的な透明度では `"Normal"` が最も一般的です。

### 手順 4: 新しいグラフィックスステートを ExtGState 辞書に追加する

```csharp
// Register the new state under the name "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

*このステップの理由は？*  
グラフィックスステートに名前（`"GS0"`）を付けることで、ページ上のコンテンツストリームが `gs` 演算子で参照できるようになります。この登録後、ページは先ほど定義した透明度を適用できます。

### 手順 5: (オプション) コンテンツストリームでグラフィックスステートを適用する

新しい塗りつぶし不透明度で矩形を描画したい場合は、前の手順の後に以下を追加します:

```csharp
// Create a content stream that uses the new graphics state
string cs = @"
q               % Save graphics state
/GS0 gs         % Apply the graphics state defined earlier
0 0 200 100 re  % Define a rectangle (x, y, width, height)
0.2 0.6 0.8 rg  % Set fill color (RGB)
f               % Fill the rectangle using the current graphics state
Q               % Restore graphics state
";

firstPage.Contents.Add(new Aspose.Pdf.Operator.GsContent(cs));
```

*このステップの理由は？*  
`q`/`Q` 演算子はグラフィックスステートを保存・復元し、透明度が意図した描画コマンドにのみ影響するようにします。`gs` 演算子は `"GS0"` という名前のグラフィックスステートに切り替えます。

### 手順 6: 変更された PDF を保存する

```csharp
// Persist the changes to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*このステップの理由は？*  
保存により、更新されたリソース辞書と新しいコンテンツストリームがディスクに書き込まれます。結果として得られるファイル（`output.pdf`）には、前のステップで定義した透明な矩形が含まれます。

## 完全に実行可能なサンプル

部品を組み合わせた完全なプログラムは以下のとおりです。コンパイルして実行できます:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using System.Collections.Generic;

class SetTransparencyDemo
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Access the first page and its resources
        Page firstPage = pdfDocument.Pages[1];
        var resourceEditor = new DictionaryEditor(firstPage.Resources);
        var extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();

        // Create a new graphics state with 50 % fill opacity
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var graphicsStateEntries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke alpha
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill alpha
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var entry in graphicsStateEntries)
            newGraphicsState.Add(entry);

        // Register the graphics state as "GS0"
        extGStateDict.Add("GS0", newGraphicsState);

        // Optional: draw a rectangle using the new transparency
        string cs = @"
q
/GS0 gs
0 0 200 100 re
0.2 0.6 0.8 rg
f
Q
";
        firstPage.Contents.Add(new GsContent(cs));

        // Save the modified PDF
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

**期待される結果** – `output.pdf` は、薄い紫色で塗りつぶされた矩形が 50 % 透明で表示され、背景のコンテンツが部分的に見えるようになります。

## よくある質問とエッジケース

* **塗りつぶし不透明度ではなく線の不透明度を変更できますか？**  
  `CA`（大文字）の値を `0`（完全に透明）から `1`（完全に不透明）の間の数値に設定します。この例ではすでに `CA` が `1` に設定されているため、線は不透明のままです。

* **ページに ExtGState 辞書が存在しない場合はどうなりますか？**  
  `resourceEditor["ExtGState"]` は自動的に空の辞書を作成します。`"GS0"` を追加しても同様に機能します。

* **グラフィックスステートは複数のページで再利用できますか？**  
  はい。ドキュメントのリソース辞書にエントリを追加すれば、`"GS0"` を参照するすべてのページが同じ透明度設定を継承します。

* **このアプローチは高レベルの `Graphics` API を使用する場合とどう違うのですか？**  
  低レベルのリソース辞書を編集することで、PDF の内部を正確に制御でき、余分なオブジェクトを埋め込まないためファイルサイズが小さくなります。

## 結論

これで **C# 用 Aspose.Pdf で PDF の透明度を設定する方法** を習得しました。このチュートリアルでは、PDF リソースの編集、塗りつぶしアルファの変更、塗りつぶし不透明度の設定、そして変更した PDF の保存について解説しました。この基礎をもとに、さまざまなブレンドモードを試したり、テキストに透明度を適用したり、複雑な文書向けに再利用可能なグラフィックスステートを作成したりできます。

### 次のステップ

* `BM` エントリを変更して、他のブレンドモード（`Multiply`、`Screen` など）を試す。  
* 線のアルファ（`CA`）を調整して、半透明のアウトラインを作成する。  
* 複数のグラフィックスステートを組み合わせて、再利用可能なビジュアルエフェクトのライブラリを構築する。

結果を共有したり、コメントで質問したりしてください。コーディングを楽しんでください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を応用した、密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説付きの完全なコード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [How to Customize PDFs with Aspose.PDF for .NET&#58; Set Page Margins and Draw Lines](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [How to Set Image Size in a PDF Using Aspose-PDF for .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [How to Set PDF Permissions Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/security-permissions/set-pdf-privileges-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}