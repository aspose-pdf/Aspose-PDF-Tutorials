---
category: general
date: 2026-10-26
description: Aspose.PDF for C# を使用して、空の PDF 辞書を作成し、PDF リソースを編集する方法を学びます。ステップバイステップのガイドと完全なコード例付き。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- edit PDF resources
- Aspose.PDF C#
- PDF manipulation C#
- PDF graphics state
language: ja
lastmod: 2026-10-26
og_description: Aspose.PDF for C# を使用して空の PDF 辞書を作成し、PDF リソースを編集します。この完全なチュートリアルに従って、PDF
  のグラフィックスステートを変更しましょう。
og_image_alt: Screenshot showing creation of empty PDF dictionary in Aspose.PDF
og_title: C#で空のPDF辞書を作成し、PDFリソースを編集する – Aspose.PDFガイド
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  headline: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  type: TechArticle
- description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  name: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  steps:
  - name: Populate the graphics state entries
    text: 'Add the standard keys:'
  - name: Register the new graphics state in the resource dictionary
    text: Give the state a name (`GS0`) and add it to the `ExtGState` dictionary that
      lives inside the page resources.
  - name: Expected output
    text: 'Running the program prints:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF
title: C# で Aspose.PDF を使って空の PDF 辞書を作成し、PDF リソースを編集する方法
url: /ja/net/programming-with-document/how-to-create-empty-pdf-dictionary-and-edit-pdf-resources-wi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Aspose.PDF を使用して空の PDF 辞書を作成し、PDF リソースを編集する方法

If you need to **create empty PDF dictionary** and then **edit PDF resources** in a C# application, this guide shows you the exact steps. You’ll see a complete, runnable example that adds a custom graphics state to the first page of an existing PDF.

C# アプリケーションで **空の PDF 辞書を作成** し、続いて **PDF リソースを編集** する必要がある場合、本ガイドでは正確な手順を示します。既存の PDF の最初のページにカスタム グラフィックス ステートを追加する、完全に実行可能なサンプルをご覧いただけます。

Working with low‑level PDF objects can feel daunting, but Aspose.PDF provides a clear API for dictionary manipulation. By the end of this tutorial you will understand why each operation matters and how to adapt the code for other resource types.

低レベルの PDF オブジェクトを扱うのは敷居が高く感じられることがありますが、Aspose.PDF は辞書操作用の明確な API を提供しています。このチュートリアルを終える頃には、各操作がなぜ重要なのか、そして他のリソースタイプにコードを適用する方法が理解できるようになります。

## 前提条件

* .NET 6.0（またはそれ以降）がインストールされていること。
* **Aspose.PDF for .NET** のライセンス版 – 無料トライアルでもテストに使用可能。
* Visual Studio 2022 などの IDE。
* `input.pdf` という名前の PDF ファイルを、コードから参照できるフォルダーに配置すること。

`Aspose.Pdf` 以外に追加の NuGet パッケージは必要ありません。

## 手順 1: プロジェクトのセットアップと名前空間のインポート

新しいコンソール プロジェクトを作成し、Aspose.PDF パッケージを追加します：

```bash
dotnet new console -n PdfDictionaryDemo
cd PdfDictionaryDemo
dotnet add package Aspose.Pdf
```

`Program.cs` で使用する名前空間をインポートします：

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
```

これらのインポートにより、`Document`、`DictionaryEditor`、および COS（Canonical Object Structure）クラスが利用可能になり、**空の PDF 辞書を作成** するオブジェクトや既存のリソース辞書の変更が可能になります。

## 手順 2: PDF ファイルが格納されているフォルダーを定義する

`input.pdf` が格納されているディレクトリを指定します。絶対パスを使用することで、プログラムが別の作業ディレクトリから実行された場合でも曖昧さを回避できます。

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfDemo\";
```

`C:\PdfDemo\` をご使用のマシンのパスに置き換えてください。パスを変数に保持することで、入力ファイルと出力ファイルの両方で簡単に再利用できます。

## 手順 3: ソース PDF ドキュメントを開く

変更したい PDF を `using` ブロック内で読み込み、ファイルハンドルが自動的に解放されるようにします。

```csharp
// Step 2: Open the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // The rest of the workflow lives inside this block
}
```

ドキュメントを開くことで、ページコレクション、リソース辞書、低レベルの COS オブジェクトにアクセスできるようになります。

## 手順 4: 最初のページとそのリソース辞書にアクセスする

最初のページは `1` でインデックス付けされます（PDF のページは 1 から始まります）。ページの `Resources` 辞書を取得し、`DictionaryEditor` でラップして安全に編集できるようにします。

```csharp
// Step 3: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` は基盤となる COS 構造を抽象化し、PDF を破損させることなくエントリの読み取りや作成が可能です。

## 手順 5: 新しいグラフィックス ステート用に **空の PDF 辞書を作成**

グラフィックス ステートは透明度、ブレンドモード、その他の描画パラメータを制御します。カスタム ステートを追加するには、まず空の辞書が必要で、次に必要なエントリを設定します。

```csharp
// Step 4: Retrieve the ExtGState dictionary and add a new graphics state
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

// Create an empty dictionary that will hold the graphics state parameters
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
```

`CreateEmptyDictionary` の呼び出しが **空の PDF 辞書を作成** するオブジェクトの核心です。これにより、同一ドキュメントに属する COS 辞書が返され、クロスリファレンスの整合性が保たれます。

### グラフィックス ステート エントリの設定

標準キーを追加します：

* `CA` – ストローク時のアルファ定数（範囲 0 – 1）。
* `ca` – 非ストローク時のアルファ定数。
* `BM` – ブレンドモード名。

```csharp
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

各エントリは先ほど作成した空の辞書に追加されます。定義と挿入ループを分離することで、コードの可読性が保たれ、後で追加のキーを拡張しやすくなります。

### 新しいグラフィックス ステートをリソース辞書に登録する

ステートに名前（`GS0`）を付け、ページリソース内にある `ExtGState` 辞書に追加します。

```csharp
// Name the new graphics state "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

これでページのリソース辞書にカスタム グラフィックス ステートへの参照が含まれ、後でコンテンツ ストリームに適用できるようになります。

## 手順 6: 更新された PDF を保存する

最後に、変更されたドキュメントを新しいファイルに書き出します。元のファイルをそのまま残すことで、変更を検証しやすくなります。

```csharp
// Step 5: Save the updated PDF
pdfDocument.Save(dataDir + "output.pdf");
```

`output.pdf` をグラフィックス ステートの検査に対応したビューア（例: Adobe Acrobat Pro）で開くと、`ExtGState` 辞書に `GS0` という名前のエントリが、定義した値とともに含まれていることが確認できます。

## 完全なソースコード

すべての要素を組み合わせると、自己完結型のプログラムが完成します：

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

class Program
{
    static void Main()
    {
        // Step 1: Define the folder that contains the PDF files
        string dataDir = @"C:\PdfDemo\"; // adjust to your environment

        // Step 2: Open the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Step 3: Access the first page and its resource dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 4: Retrieve the ExtGState dictionary and add a new graphics state
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // **Create empty PDF dictionary** for the new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateEntries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };

            foreach (var entry in graphicsStateEntries)
                newGraphicsState.Add(entry);

            // Register the new graphics state as "GS0"
            extGStateDict.Add("GS0", newGraphicsState);

            // Step 5: Save the updated PDF
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

### 期待される出力

プログラムを実行すると次のように出力されます：

```
PDF updated successfully.
```

そして同じフォルダーに `output.pdf` が作成されます。ファイルを開くと、**Resources → ExtGState → GS0** の下に、設定したパラメータを持つ新しいエントリが表示されます。

## 一般的なバリエーションとエッジケース

| Situation | How to adapt the code |
|-----------|-----------------------|
| **複数ページ** で同じグラフィックス ステートが必要な場合 | 辞書を一度だけ作成し、各ページの `ExtGState` 辞書に同じ `GS0` 参照を追加します。 |
| **異なるブレンドモード**（例: `Multiply`） | `CosPdfName("Normal")` の値を `CosPdfName("Multiply")` に変更します。 |
| **ExtGState 辞書が存在しない** 場合 | `resourcesEditor["ExtGState"]` にアクセスする前に `resourcesEditor.ContainsKey("ExtGState")` を確認します。存在しない場合は新しい空の辞書を作成し、`firstPage.Resources` に追加します。 |
| **大きな PDF** でメモリ負荷が発生する場合 | ページをストリーミングする `PdfDocument.Load` のオーバーロードを使用するか、`using` ブロック内でページを1つずつ処理します。 |
| **他のリソース（フォント、XObject）を編集する必要がある** 場合 | `resourcesEditor` の検索で `"ExtGState"` を `"Font"` または `"XObject"` に置き換え、同様に空の辞書を作成して内容を設定するパターンに従います。 |

これらのバリエーションは、同じ **空の PDF 辞書を作成** パターンが、**PDF リソースを編集** したい任意のリソースタイプにどのように適用できるかを示しています。

## プロのコツ

* **結果を検証する** – 保存後、RAW リソース辞書を表示できるツール（例: PDF‑Box の `PDFDebugger`）で PDF を開き、エントリが存在することを確認します。
* **辞書を再利用する** – 同じグラフィックス ステートを多数のページに追加する場合、辞書を変数に保持して参照し、毎回再作成しないようにします。
* **バージョン互換性** – このコードは Aspose.PDF 23.12 以降で動作します。以前のバージョンでは `CosPdfDictionary` の代わりに `CosDictionary` が必要になる場合があります。

## 結論

これで、Aspose.PDF for C# を使用して **空の PDF 辞書** オブジェクトを **作成** し、**PDF リソースを編集**する方法が分かりました。本チュートリアルでは、ドキュメントのオープン、ページのリソース辞書へのアクセス、カスタム グラフィックス ステートの構築、登録、結果の保存までを扱いました。ここからは、他のリソースタイプを試したり、複数のグラフィックス ステートを組み合わせたり、より大規模な PDF 処理パイプラインにこの手法を組み込んだりできます。

---

*さらに探求したいですか？ カスタム **ExtGState** をコンテンツ ストリームに追加したり、**Font** 辞書を操作して新しいフォントを埋め込んだりしてみてください。どちらも空の辞書を作成し、PDF リソースを編集する同じパターンに従います。*

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説とともに完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.PDF を使用した PDF リソース辞書の編集 – C# ガイド](/pdf/english/net/programming-with-operators/edit-pdf-resource-dictionary-with-aspose-pdf-c-guide/)
- [Aspose.Pdf を使用した PDF のカスタム グラフィックス ステートの作成](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [C# で PDF の空のグラフィックス ステートを作成する方法](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}