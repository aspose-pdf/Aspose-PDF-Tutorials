---
category: general
date: 2026-11-12
description: Aspose.Pdf を使用して PDF の不透明度を変更し、透明性を追加し、ブレンドモードを設定し、C# で変更された PDF を保存する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF opacity
- how to add transparency
- save modified PDF
- how to set blend mode
- set fill opacity
language: ja
lastmod: 2026-11-12
og_description: Aspose.PdfでPDFの不透明度を変更し、透明性の追加方法、ブレンドモードの設定、そしてC#で変更したPDFファイルを保存する方法を学びましょう。
og_image_alt: Screenshot of a PDF page with altered opacity using Aspose.Pdf
og_title: Aspose.PdfでPDFの不透明度を変更 – 透明度を追加して保存
schemas:
- author: Aspose
  dateModified: '2026-11-12'
  description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  headline: Change PDF opacity with Aspose.Pdf and save the file
  type: TechArticle
- description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  name: Change PDF opacity with Aspose.Pdf and save the file
  steps:
  - name: Load the PDF document
    text: Start by creating a `Document` instance that points to your source file.
      The constructor reads the entire PDF into memory, allowing you to manipulate
      its internal objects.
  - name: Access the first page’s resources
    text: Each PDF page stores a *resource dictionary* that holds objects such as
      fonts, images, and graphics states. You need to edit this dictionary to inject
      a new `ExtGState` entry.
  - name: Ensure an ExtGState dictionary exists
    text: The `ExtGState` dictionary holds custom graphics states. If it does not
      exist, the code creates one automatically.
  - name: Define a new graphics state (ExtGState)
    text: A graphics state defines how drawing operations behave. The following dictionary
      sets stroke opacity (`CA`), fill opacity (`ca`), and blend mode (`BM`).
  - name: Register the graphics state in the resource dictionary
    text: Give the new state a name (e.g., `GS0`) and add it to the `ExtGState` dictionary.
      This name will be referenced later in the page content stream.
  - name: Apply the graphics state to page content
    text: To actually see the opacity effect, insert the `/GS0 gs` operator before
      the drawing commands you want to affect. The example below draws a semi‑transparent
      rectangle.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The `Save` method overwrites
      the target file or creates a new one if it does not exist.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Aspose.PdfでPDFの不透明度を変更し、ファイルを保存する
url: /ja/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-and-save-the-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.PdfでPDFの不透明度を変更し、ファイルを保存する

ドキュメント内の **PDF の不透明度を変更** する必要がある場合、Aspose.Pdf はストロークと塗りの透明度の両方を調整できるシンプルな API を提供します。このチュートリアルでは、**透明度の追加方法**、**ブレンドモードの設定方法**、そして数行の C# コードだけで **変更された PDF を保存** する方法を正確に示します。

既存の PDF を読み込むところから新しいグラフィックスステートを定義し、変更を永続化するまで、すべての手順を順に実行します。このガイドの最後までに、以下ができるようになります：

* ベクターグラフィックや画像の可視性を低減する。
* *Normal* や *Multiply* などのカスタムブレンドモードを適用する。
* 他のコンテンツを失うことなく、更新されたファイルをエクスポートする。

唯一の前提条件は、動作する .NET 開発環境と Aspose.Pdf ライブラリ（バージョン 23.9 以降）への参照です。外部ツールは必要ありません。

## 前提条件

| 要件 | 重要な理由 |
|------|------------|
| .NET 6.0 SDK 以降 | 最新の Aspose.Pdf API との互換性を保証します。 |
| Aspose.Pdf for .NET NuGet パッケージ | `Document`、`CosPdfDictionary`、およびコードで使用される関連クラスを提供します。 |
| 編集対象の PDF ファイル（例: `input.pdf`） | 不透明度変更の元となるファイルです。 |

NuGet パッケージは以下でインストールします：

```bash
dotnet add package Aspose.Pdf
```

## Aspose.PdfでPDFの不透明度を変更する

### 手順 1: PDF ドキュメントを読み込む

`Document` インスタンスを作成し、ソースファイルを指すようにします。コンストラクタは PDF 全体をメモリに読み込み、内部オブジェクトを操作できるようにします。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;

// Load the existing PDF
var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");
```

> **この手順の理由** ファイルを読み込むことで操作可能なオブジェクトモデルが作成されます。その後のすべての変更はこのメモリ上の表現に対して行われ、明示的に保存するまで元のファイルは変更されません。

### 手順 2: 最初のページのリソースにアクセスする

各 PDF ページはフォント、画像、グラフィックスステートなどのオブジェクトを保持する *リソース辞書* を持ちます。この辞書を編集して新しい `ExtGState` エントリを挿入する必要があります。

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor simplifies access to the page's resource dictionary
var resourcesEditor = new DictionaryEditor(page.Resources);
```

> **ヒント**: 同じ不透明度が必要なページが複数ある場合は、各ページでこの手順を繰り返すか、単一の `ExtGState` をページ間で共有してください。

### 手順 3: ExtGState 辞書が存在することを確認する

`ExtGState` 辞書はカスタムグラフィックスステートを保持します。存在しない場合、コードが自動的に作成します。

```csharp
// Get or create the ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                     ?? new CosPdfDictionary(pdfDoc);
resourcesEditor["ExtGState"] = extGStateDict;
```

> **この手順の理由**: `ExtGState` コンテナがないと、新しいグラフィックスステートへの参照が失敗し、PDF が不透明度設定を無視する結果になります。

### 手順 4: 新しいグラフィックスステート (ExtGState) を定義する

グラフィックスステートは描画操作の動作を定義します。以下の辞書はストローク不透明度 (`CA`)、塗り不透明度 (`ca`)、およびブレンドモード (`BM`) を設定します。

```csharp
// Create an empty dictionary for the new graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Set desired parameters
var parameters = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (1 = opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (0.5 = 50% transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var param in parameters)
    newGraphicsState.Add(param);
```

> **塗り不透明度の設定方法**: `ca` エントリは塗りつぶし形状（テキスト、パス）の不透明度を制御します。`0`（完全に透明）から `1`（完全に不透明）までの数値を調整して、デザイン要件に合わせてください。

> **ブレンドモードの設定方法**: `BM` エントリは合成アルゴリズムを選択します。一般的な値には `Normal`、`Multiply`、`Screen`、`Overlay` があります。視覚的意図に合うものを選んでください。

### 手順 5: リソース辞書にグラフィックスステートを登録する

新しいステートに名前（例: `GS0`）を付け、`ExtGState` 辞書に追加します。この名前は後でページのコンテンツストリームで参照されます。

```csharp
// Add the graphics state with a symbolic name
extGStateDict.Add("GS0", newGraphicsState);
```

> **プロのコツ**: 複数のステートを作成する際は `GS0`、`GS1` … のような命名規則を使用してください。名前衝突を防ぎ、デバッグが容易になります。

### 手順 6: ページコンテンツにグラフィックスステートを適用する

不透明度効果を実際に確認するには、対象となる描画コマンドの前に `/GS0 gs` 演算子を挿入します。以下の例は半透明の矩形を描画します。

```csharp
// Build a content stream that uses the new graphics state
var content = new MemoryStream();
var writer = new StreamWriter(content);

// Activate the graphics state
writer.WriteLine("q");                 // Save graphics state
writer.WriteLine("/GS0 gs");           // Apply custom ExtGState
writer.WriteLine("0.2 0.5 0.8 rg");    // Set fill color (RGB)
writer.WriteLine("100 500 200 100 re"); // Rectangle (x y width height)
writer.WriteLine("f");                 // Fill rectangle
writer.WriteLine("Q");                 // Restore graphics state
writer.Flush();

content.Position = 0;
page.Contents.Add(new ContentStream(content));
```

> **`q` と `Q` 演算子の理由**: これらはグラフィックスステートスタックをプッシュ・ポップし、不透明度の変更が矩形のみに適用され、ページの他の部分には影響しないようにします。

### 手順 7: 変更された PDF を保存する

最後に、更新されたドキュメントをディスクに書き込みます。`Save` メソッドは対象ファイルを上書きするか、存在しない場合は新規作成します。

```csharp
// Persist the changes
pdfDoc.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **変更された PDF の保存方法**: `Save` 呼び出しは新しい `ExtGState` を含むすべてのメモリ上の変更を指定されたパスに書き込みます。Web 応答用に結果を `MemoryStream` にストリームすることも可能です。

## 完全な動作例

以下は、上記のすべての手順を組み込んだ単一の自己完結型プログラムです。コンソールアプリケーションにコピーして実行し、不透明度の変更を確認してください。

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Operators;

class ChangePdfOpacityDemo
{
    static void Main()
    {
        // 1. Load the PDF
        var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");

        // 2. Get first page and its resources
        var page = pdfDoc.Pages[1];
        var resourcesEditor = new DictionaryEditor(page.Resources);

        // 3. Ensure ExtGState dictionary exists
        var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                             ?? new CosPdfDictionary(pdfDoc);
        resourcesEditor["Ext


## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.Pdfで変更された PDF を保存し、透明度を追加する方法](/pdf/english/net/document-manipulation/how-to-save-modified-pdf-with-aspose-pdf-and-add-transparenc/)
- [C# で Aspose.PDF を使用して PDF に透明度を追加する方法](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [Aspose.PDF でグラフィックスステートを追加し、透明度を制御する方法](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}