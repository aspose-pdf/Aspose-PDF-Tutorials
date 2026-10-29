---
category: general
date: 2026-08-17
description: C# と Aspose.Pdf を使用して PDF に空のグラフィックス状態を作成します。このステップバイステップガイドに従って、ExtGState
  リソースを安全に編集してください。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty graphics state
- Aspose PDF graphics state
- C# modify PDF resources
- add ExtGState dictionary
- PDF page resources editing
language: ja
lastmod: 2026-08-17
og_description: C# を使用して PDF に空のグラフィックス状態を作成します。このチュートリアルでは、信頼性の高い PDF 変更のために Aspose.Pdf
  で ExtGState リソースを編集する方法を示します。
og_image_alt: Screenshot of C# code that adds an empty graphics state to a PDF document
og_title: C#でPDFに空のグラフィックスステートを作成する – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Create empty graphics state in a PDF using C# and Aspose.Pdf. Follow
    this step‑by‑step guide to edit ExtGState resources safely.
  headline: How to create empty graphics state in a PDF with C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: C#でPDFの空のグラフィックス状態を作成する方法
url: /ja/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で PDF に空のグラフィックスステートを作成する方法

PDF に **空のグラフィックスステートを作成** する必要がある場合、このガイドでは C# と Aspose.Pdf を使用して正確にその方法を示します。ページの ExtGState 辞書に新しいエントリを追加し、既存のコンテンツに影響を与えない完全な実行可能サンプルをご覧いただけます。

PDF のグラフィックスステートを操作することは、透明度、ブレンドモード、またはオブジェクト単位でのその他の描画パラメータを制御したいときに一般的な要件です。以下のコードは推奨されるアプローチを示し、各ステップが重要である理由を説明し、遭遇しうる典型的なバリエーションもカバーします。

## 前提条件

開始する前に、以下を確認してください。

* .NET 6.0 以降（サンプルは .NET Core でもコンパイル可能です）。
* Aspose.Pdf for .NET のライセンス（または一時的な評価キー）。
* 修正したい `input.pdf` ファイルが格納されたフォルダー。
* C# の構文と、リソース辞書などの PDF 概念に関する基本的な知識。

## 手順 1: プロジェクトをセットアップし名前空間をインポートする

新しいコンソール アプリケーションを作成するか、既存プロジェクトにコードを統合します。Aspose.Pdf NuGet パッケージを追加します。

```bash
dotnet add package Aspose.Pdf
```

次に、必要な名前空間をインポートします。

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
```

これらのインポートにより、**空のグラフィックスステート** エントリを作成するために必要な `Document`、`DictionaryEditor`、PDF プリミティブ クラスにアクセスできます。

## 手順 2: PDF ファイルが格納されたフォルダーを定義する

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfSamples\";
```

パスはご自身の PDF ファイルがある場所に置き換えてください。ディレクトリを変数に保持しておくことで、コードの再利用性とテストの容易さが向上します。

## 手順 3: ソース PDF ドキュメントを読み込む

```csharp
// Step 2: Load the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // All subsequent operations happen inside this using block
```

`using` ステートメント内でドキュメントを開くことで、変更を保存した後にファイルハンドルが自動的に解放されます。

## 手順 4: 最初のページとその Resources 辞書にアクセスする

```csharp
    // Step 3: Get the first page and its Resources dictionary
    var firstPage = pdfDocument.Pages[1];
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
    var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

* `Pages[1]` は最初のページを取得します（PDF のページ番号は 1 から始まります）。
* `DictionaryEditor` は PDF 辞書の読み書きを便利に行うためのクラスです。
* `ExtGState` エントリはページのすべてのグラフィックスステート オブジェクトを保持します。キーが存在しない場合、Aspose.Pdf は自動的に空の辞書を作成します。

## 手順 5: 新しい空のグラフィックスステート辞書を構築する

追加するグラフィックスステートは空でも、透明度 (`CA`, `ca`) やブレンドモード (`BM`) などのパラメータで事前に設定しても構いません。このチュートリアルでは **空のグラフィックスステート** を作成し、辞書の動作を示すためにいくつかの典型的な値を設定します。

```csharp
    // Step 4: Create a new empty graphics‑state dictionary and set its parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // Stroke opacity
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };
    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

* `CosPdfDictionary.CreateEmptyDictionary` は、任意のグラフィックスステート キーを格納できるクリーンなコンテナを作成します。
* `CA`、`ca`、`BM` の追加はオプションです。真に空のステートが必要な場合は省略できます。コードは、後で描画を制御したいときにエントリを追加する方法を示しています。

## 手順 6: 新しいグラフィックスステートを ExtGState 辞書に挿入する

```csharp
    // Step 5: Add the new graphics state to the page's ExtGState dictionary (e.g., name it "GS0")
    extGStateDict.Add("GS0", newGraphicsState);
```

エントリ名を `"GS0"` とするのは、グラフィックスステート名に “GS” プレフィックスを付ける一般的な慣例に従っています。既存のキーと衝突しない有効な PDF 名であれば任意の名前を使用できます。

## 手順 7: 変更した PDF ドキュメントを保存する

```csharp
    // Step 6: Save the modified PDF document
    pdfDocument.Save(dataDir + "output.pdf");
}
```

`Save` 呼び出しにより、更新されたファイルが `output.pdf` に書き込まれます。このファイルを PDF ビューアで開くと、新しいグラフィックスステートが存在することが確認でき、コンテンツ ストリーム内で `gs` 演算子を使用して後から参照できます。

### 完全なソース リスティング

すべてをまとめると、完全なプログラムは次のようになります。

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;

class Program
{
    static void Main()
    {
        // Define the folder that contains the PDF files
        string dataDir = @"C:\PdfSamples\";

        // Load the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Get the first page and its Resources dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create a new empty graphics‑state dictionary and set its parameters
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters)
                newGraphicsState.Add(p);

            // Add the new graphics state to the page's ExtGState dictionary (name it "GS0")
            extGStateDict.Add("GS0", newGraphicsState);

            // Save the modified PDF document
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("Empty graphics state created and saved to output.pdf");
    }
}
```

プログラムを実行すると確認メッセージが出力され、`output.pdf` に新たに追加されたグラフィックスステートが含まれます。

## このアプローチが最適な理由

* **辞書の直接編集** – `DictionaryEditor` を使用することで、コンテンツ ストリーム全体を解析する必要がなく、必要なリソースだけを変更できます。
* **型安全な PDF プリミティブ** – `CosPdfNumber`、`CosPdfName`、`CosPdfDictionary` により、生成された PDF が PDF 1.7 仕様に準拠していることが保証されます。
* **安全性** – `using` ブロックにより `Document` オブジェクトが確実に破棄され、ファイルロックやビルド時の破損を防止します。
* **拡張性** – 空のグラフィックスステートが作成されたら、任意のコンテンツ 演算子 (`gs`) から参照して、透明度、ブレンドモード、その他のパラメータを選択的に変更できます。

## 一般的なバリエーションとエッジケース

| 状況 | 推奨の調整 |
|-----------|-------------------|
| **複数ページ** | `pdfDocument.Pages` をループし、変更が必要な各ページに対して辞書挿入を繰り返します。 |
| **ExtGState エントリが存在しない** | `resourcesEditor["ExtGState"]` は存在しない場合に自動で空の辞書を作成します。追加コードは不要です。 |
| **異なるグラフィックスステート名** | `"GS0"` を、たとえば `"MyTransparentState"` のように命名規則に合わせた名前に置き換えます。 |
| **空のステートだけを追加** | `parameters` 配列と `foreach` ループを省略すれば、辞書は空のままになります。 |
| **暗号化された PDF の取り扱い** | リソースを編集する前に `new Document(path, password)` でパスワードを渡します。 |

## 結果の検証

**PDF‑Tron** や **iText Sharp** などの低レベルビューアで PDF を調べることで、グラフィックスステートが追加されたか確認できます。以下のようなエントリを探してください。

```
/ExtGState << /GS0 << /CA 1 /ca 0.5 /BM /Normal >> >>
```

エントリが表示されていれば、**空のグラフィックスステートを作成** する操作は成功しています。

## 結論

これで C# と Aspose.Pdf を使用して PDF に **空のグラフィックスステートを作成** する方法が分かりました。チュートリアルでは、ドキュメントの読み込みから `ExtGState` 辞書の編集、結果の保存までのすべての手順をカバーし、各操作の根拠も解説しました。

今後は次のことが可能です。

* コンテンツ ストリームで新しいグラフィックスステートを使用する（例: `gs /GS0`）。
* `/SM`（ストローク調整）や `/OPM`（オーバープリントモード）などの追加キーを試す。
* 同様の手法を `/XObject` や `/ColorSpace` など他のリソースタイプにも適用する。

PDF ハッキングを楽しんでください。また、**Aspose PDF グラフィックスステート** に関する他のシナリオ（動的透明度変更やカスタムブレンドモードなど）もぜひ探求してください！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、ステップバイステップの説明と完全なコード例が含まれており、API の追加機能を習得したり、独自プロジェクトで代替実装を検討したりするのに役立ちます。

- [Aspose.PDF for .NET を使用して PDF に破線を作成する方法：ステップバイステップ ガイド](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Aspose.PDF .NET を使用して PDF からグラフィックスを削除する方法：完全ガイド](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Aspose.PDF for .NET を使用して PDF に矩形を作成・塗りつぶす方法：ステップバイステップ ガイド](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}