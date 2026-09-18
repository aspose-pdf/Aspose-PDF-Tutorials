---
category: general
date: 2026-09-18
description: Aspose.PDF を使用して C# で空の PDF 辞書を作成する方法を学びます。このステップバイステップガイドでは、ExtGState、グラフィックス状態、および
  CosPdfDictionary の操作について解説します。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.PDF
- ExtGState dictionary
- graphics state
- CosPdfDictionary
- PDF manipulation C#
language: ja
lastmod: 2026-09-18
og_description: C# と Aspose.PDF を使用して空の PDF 辞書を作成します。この包括的なチュートリアルに従って ExtGState とグラフィックスステート辞書を編集してください。
og_image_alt: Screenshot showing creation of an empty PDF dictionary in C#
og_title: C#で空のPDFディクショナリを作成する – 完全なAspose.PDFガイド
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn to create empty PDF dictionary in C# using Aspose.PDF. This step‑by‑step
    guide covers ExtGState, graphics state, and CosPdfDictionary manipulation.
  headline: How to create empty PDF dictionary with Aspose.PDF in C#
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: C#でAspose.PDFを使って空のPDFディクショナリを作成する方法
url: /ja/net/programming-with-document/how-to-create-empty-pdf-dictionary-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.PDF for C#で空のPDF辞書を作成する方法

PDFファイルを処理中に **空のPDF辞書を作成** する必要がある場合、本ガイドでは Aspose.PDF for .NET を使用してその手順を正確に示します。透過性やブレンドモード、あるいはカスタムのグラフィックスステートを調整する場合でも、以下の手順で `ExtGState` 辞書を安全かつ効率的に編集できます。

このチュートリアルで学べること:

* Aspose.PDF を使用して PDF ドキュメントを読み込む方法。
* 最初のページのリソースと既存の `ExtGState` 辞書にアクセスする方法。
* 新しい空の `CosPdfDictionary` を作成し、グラフィックスステート エントリを追加する方法。
* 元のコンテンツを失うことなく、変更した PDF を保存する方法。

このソリューションは、少なくとも 1 ページが含まれる任意の PDF で動作し、Aspose.PDF ライブラリ（バージョン 23.10 以降）だけが必要です。

## 前提条件

* .NET 6.0 以降（コードは .NET Framework 4.8 でも動作します）。
* **Aspose.PDF** NuGet パッケージへの参照。
* `YOUR_DIRECTORY/input.pdf` に配置された入力 PDF ファイル。
* C# と PDF のリソースやグラフィックスステートといった概念に関する基本的な知識。

> **プロのコツ:** 大きな PDF を扱う場合は、`Document` オブジェクトを `using` ブロックでラップして、ファイルハンドルが速やかに解放されるようにしましょう。

## Step 1: PDF ドキュメントを読み込む

最初の操作でソース ファイルを開きます。Aspose.PDF はドキュメント全体をメモリに読み込み、内部オブジェクトの編集を可能にします。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

*Why this matters*: ドキュメントを読み込むことで変更可能なオブジェクトモデルが生成されます。このステップがなければ、辞書操作に必要なページリソースに到達できません。

## Step 2: 最初のページのリソースを取得する

各ページはフォント、画像、グラフィックスステートを保持する `Resources` 辞書を持っています。これにアクセスすると、読み書きを簡素化する `DictionaryEditor` が取得できます。

```csharp
// Step 2: Get the resources of the first page
Page firstPage = pdfDocument.Pages[1];
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Why this matters*: `ExtGState` 辞書はページリソース内に存在します。誤った辞書を編集しても描画には影響しません。

## Step 3: 既存の ExtGState 辞書を探す

`ExtGState` エントリにはすでにグラフィックスステート オブジェクトが含まれている場合があります。新しいエントリを追加できるよう、`CosPdfDictionary` として取得します。

```csharp
// Step 3: Access the existing ExtGState dictionary
CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

`ExtGState` エントリが存在しない場合、後で新しい辞書を割り当てたときに Aspose.PDF が自動的に空の辞書を作成します。

## Step 4: **Create empty PDF dictionary** for a new graphics state

ここでは全く新しい `CosPdfDictionary` を構築します—これは **create empty PDF dictionary** 操作の核心です。その後、標準的なグラフィックスステート キーで辞書を埋めます。

* `CA` – ストロークの不透明度。
* `ca` – 塗りつぶしの不透明度。
* `BM` – ブレンドモード。

```csharp
// Step 4: Create a new graphics state dictionary and define its entries
CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

KeyValuePair<string, ICosPdfPrimitive>[] graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),          // Stroke opacity
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),       // Fill opacity
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))    // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

*Why this matters*: 各エントリを明示的に定義することで、ページ上のオブジェクトがどのようにブレンド・描画されるかを制御できます。辞書は **空** の状態からこれらのキーを追加するまで **空** であり、**create empty PDF dictionary** の要件を満たします。

## Step 5: 新しいグラフィックスステートを ExtGState 辞書に追加する

各グラフィックスステートは一意の名前（例: `GS0`）を持つ必要があります。その名前で新しく作成した辞書を挿入します。

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary with a unique name
extGStateDict.Add("GS0", graphicsStateDict);
```

複数のステートが必要な場合は、`GS1`、`GS2` などのエントリを追加し、`ExtGState` 辞書内で名前が重複しないようにしてください。

## Step 6: 更新された PDF ドキュメントを保存する

最後に、変更をディスクに書き戻します。元のファイルはそのままで、新しいパスに保存するため影響を受けません。

```csharp
// Step 6: Save the updated PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

結果として生成された `output.pdf` には、追加されたグラフィックスステート (`GS0`) が含まれます。ページのコンテンツ ストリームからは `/GS0` 演算子で参照できます。

## 完全な動作例

すべての手順を組み合わせると、すぐに実行できる自己完結型プログラムが完成します。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources
            Page firstPage = pdfDocument.Pages[1];
            DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Get (or create) ExtGState dictionary
            CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Build a new empty PDF dictionary for graphics state
            CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var entry in entries)
                graphicsStateDict.Add(entry);

            // Insert the new graphics state with a unique name
            extGStateDict.Add("GS0", graphicsStateDict);

            // Save the modified document
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

**Expected output**: プログラム実行後、`output.pdf` は `input.pdf` と同じ視覚コンテンツを保持します。Adobe Acrobat や PDF‑Tron などのツールで PDF を確認すると、最初のページの `ExtGState` 辞書に新しいエントリ `GS0` が表示されます。

## よくあるバリエーションとエッジケース

| Situation | What to adjust |
|-----------|----------------|
| **No existing ExtGState entry** | `resourcesEditor["ExtGState"]` を `new CosPdfDictionary(pdfDocument)` に置き換え、`firstPage.Resources["ExtGState"]` に再度割り当てます。 |
| **Multiple pages need the same state** | 各ページの `ExtGState` 辞書に同じ `GS0` エントリを追加するか、共有リソース オブジェクトから辞書を参照します。 |
| **Different blend mode** | `CosPdfName` の値を `"Normal"` から `"Multiply"`、`"Screen"` など、目的の効果に合わせて変更します。 |
| **Higher opacity values** | `ca` または `CA` に `new CosPdfNumber(0.8)` を使用して、塗りつぶしまたはストロークの不透明度を上げます。 |
| **Using a stream operator** | コンテンツ ストリーム内で描画操作の前に `"/GS0 gs"` と記述し、新しいグラフィックスステートを適用します。 |

## パフォーマンス上の考慮点

* **Memory usage** – 非常に大きな PDF を読み込むと、ページ数に比例したメモリが消費されます。最初のページだけを編集する場合は、処理後に `pdfDocument.Pages.Delete(pageNumber)` を使用してリソースを解放することを検討してください。
* **Thread safety** – Aspose.PDF オブジェクトはスレッドセーフではありません。辞書の編集は単一スレッドで行うか、スレッドごとに別々の `Document` インスタンスを作成してください。

## 結論

これで、Aspose.PDF を使って **create empty PDF dictionary** オブジェクトを作成し、グラフィックスステート エントリで埋め、ページの `ExtGState` 辞書に添付する方法が分かりました。この手法により、C# から不透明度、ブレンドモード、その他の描画パラメータを細かく制御できます。

次は、**PDF manipulation C#**、高度な透過効果のためのカスタム **ExtGState dictionary** エントリの追加、または **CosPdfDictionary** を使用したフォントや XObject など他のリソースタイプの変更など、関連トピックを探求してください。複数のグラフィックスステートを試して、PDF に高度なビジュアル エフェクトを構築しましょう。

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示したテクニックを基にした、密接に関連するトピックを取り上げています。各リソースには、完全なコード例とステップバイステップの解説が含まれており、API の追加機能を習得したり、プロジェクトで代替実装アプローチを検討したりするのに役立ちます。

- [Create & Fill Rectangles in PDFs Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)
- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [How to Add an Empty Page at the End of a PDF Using Aspose.PDF for .NET | Step-by-Step Guide](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}