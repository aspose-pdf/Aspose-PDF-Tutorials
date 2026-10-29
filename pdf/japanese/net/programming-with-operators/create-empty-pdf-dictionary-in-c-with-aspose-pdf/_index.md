---
category: general
date: 2026-08-14
description: Aspose.Pdf を使用して C# で空の PDF 辞書を作成 – ExtGState コレクションにグラフィックスステートを追加し、プログラムで
  PDF を変更する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.Pdf Document
- PDF graphics state
- ExtGState dictionary
- CosPdfDictionary usage
language: ja
lastmod: 2026-08-14
og_description: C# と Aspose.Pdf を使用して空の PDF 辞書を作成します。この完全ガイドに従い、PDF の ExtGState コレクションにカスタム
  グラフィックス ステートを追加してください。
og_image_alt: Screenshot showing C# code that creates an empty PDF dictionary with
  Aspose.Pdf
og_title: C#で空のPDFディクショナリを作成 – Aspose.Pdfステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  headline: Create empty PDF dictionary in C# with Aspose.Pdf
  type: TechArticle
- description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  name: Create empty PDF dictionary in C# with Aspose.Pdf
  steps:
  - name: Create a new **Console App** project in Visual Studio.
    text: Create a new **Console App** project in Visual Studio.
  - name: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
    text: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
  - name: 'Add the following `using` directives at the top of `Program.cs`:'
    text: 'Add the following `using` directives at the top of `Program.cs`:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Aspose.Pdf を使用して C# で空の PDF 辞書を作成する
url: /ja/net/programming-with-operators/create-empty-pdf-dictionary-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# と Aspose.Pdf で空の PDF 辞書を作成する

PDF ファイルを扱う際に **空の PDF 辞書** オブジェクトを作成する必要がある場合、このガイドでは Aspose.Pdf ライブラリを使用して C# で実際に行う方法を示します。カスタムのグラフィックス状態を構築したり、新しいリソースを追加したり、後で使用するテンプレートを準備したりする際に、以下の手順で完全に実行可能なソリューションを提供します。

PDF を読み込み、最初のページのリソース辞書にアクセスし、全く新しい `CosPdfDictionary` を作成して `ExtGState` コレクションに挿入する方法を学びます。チュートリアルの最後まで実行すれば、作成した辞書が含まれた `output.pdf` が生成されます。

## 前提条件

開始する前に、以下が揃っていることを確認してください。

- .NET 6.0 以降（コードは .NET Framework 4.6+ でも動作します）
- Visual Studio 2022 またはお好みの C# IDE
- Aspose.Pdf for .NET のライセンス（または一時評価キー）
- 任意のフォルダーに配置した **input.pdf** というサンプル PDF（フォルダーのパスは `dataDir` として使用します）

`Aspose.Pdf` 以外に追加の NuGet パッケージは必要ありません。

## 手順 1: プロジェクトを作成し Aspose.Pdf を参照する

1. Visual Studio で新しい **Console App** プロジェクトを作成します。  
2. **NuGet パッケージ マネージャー** を開き、`Aspose.Pdf` をインストールします：

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. `Program.cs` の先頭に以下の `using` ディレクティブを追加します：

   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Text;
   using Aspose.Pdf.Operators;
   using Aspose.Pdf.Facades;
   using Aspose.Pdf.InteractiveFeatures;
   using Aspose.Pdf.Xmp;
   using Aspose.Pdf.Operators.Filters;
   using Aspose.Pdf.Operators.Gfx;
   ```

   *なぜこれらの名前空間が必要か？* `Aspose.Pdf` にはコアの `Document` クラスが含まれ、`Aspose.Pdf.Operators.Gfx` には **空の PDF 辞書** 構造を作成するために必要な `CosPdfDictionary`、`CosPdfNumber` などの低レベル PDF オブジェクトが提供されています。

## 手順 2: ソース PDF を読み込む

最初の操作は既存の PDF ファイルを `Document` インスタンスに読み込むことです。これにより、すべてのページ、リソース、低レベル辞書へアクセスできるようになります。

```csharp
// Step 2: Load the PDF document
string dataDir = @"C:\MyPdfFolder\";               // Change to your folder
using var pdfDocument = new Document(dataDir + "input.pdf");
```

*解説*: `Document` はファイルをメモリに読み込み、内部構造を準備します。`using` 文は処理終了後にファイルハンドルを解放することを保証します。

## 手順 3: 最初のページのリソース辞書にアクセスする

各 PDF ページには **Resources** 辞書があり、フォント、画像、ExtGState オブジェクト、その他の共有リソースがまとめられています。新しいグラフィックス状態を挿入するには、この辞書を編集する必要があります。

```csharp
// Step 3: Get the first page and its Resources dictionary
Page firstPage = pdfDocument.Pages[1];                     // PDF pages are 1‑based
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` は PDF 辞書を C# の `Dictionary<string, object>` のように扱えるヘルパークラスです。

## 手順 4: ExtGState コレクションを取得（または作成）する

`ExtGState` には不透明度、ブレンドモード、線幅などのグラフィックス状態オブジェクトが格納されます。ソース PDF に既に `ExtGState` エントリが存在すればそれを再利用し、存在しなければ新しい空の辞書を作成します。

```csharp
// Step 4: Ensure an ExtGState dictionary exists
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a brand‑new ExtGState dictionary and add it to Resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*なぜこのチェックが必要か？* PDF によっては `ExtGState` エントリ自体が省略されていることがあります。両方のケースに対応することで、任意の入力ファイルに対して堅牢なチュートリアルになります。

## 手順 5: 新しいグラフィックス状態用に **空の PDF 辞書** を作成する

ここで実際に **空の PDF 辞書** オブジェクトを作成し、グラフィックス状態パラメータを定義します。辞書は最初は空で、必要なキーを追加していきます。

```csharp
// Step 5: Build a new graphics state dictionary (empty PDF dictionary + entries)
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Stroke opacity (CA) – 1 means fully opaque strokes
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes semi‑transparent fills
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default compositing mode
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

### 各エントリの意味

| キー | 型 | 意味 |
|-----|------|---------|
| **CA** | `CosPdfNumber` | ストロークの不透明度（範囲 0‑1）。 |
| **ca** | `CosPdfNumber` | 塗りつぶしの不透明度（範囲 0‑1）。 |
| **BM** | `CosPdfName`   | ブレンドモード；最も一般的なのは `"Normal"`。 |

**空の PDF 辞書** から始めたため、追加するエントリを完全にコントロールできます。必要に応じて `LW`（線幅）や `LC`（線端）などの追加パラメータを拡張してください。

## 手順 6: 新しいグラフィックス状態を ExtGState に挿入する

`ExtGState` 辞書は名前（例: `GS0`、`GS1`）で識別されるマップのように機能します。作成した辞書を一意のキーの下に追加します。

```csharp
// Step 6: Add the graphics state to the ExtGState collection
extGStateDict.Add("GS0", newGraphicsState);
```

複数の状態を追加する場合は、接尾辞（`GS1`、`GS2` …）をインクリメントして名前衝突を防ぎます。

## 手順 7: 変更後の PDF を保存する

最後に、変更をディスクに書き出します。`Save` メソッドは更新された辞書を自動的にシリアライズします。

```csharp
// Step 7: Persist the changes
pdfDocument.Save(dataDir + "output.pdf");
```

任意の PDF ビューアで `output.pdf` を開き、**Resources → ExtGState** エントリを確認してください（多くのビューアは非表示にしますが、Adobe Acrobat Preflight や PDF‑Tron などのツールで確認可能です）。`GS0` エントリに、設定した不透明度とブレンドモードの値が含まれているはずです。

## 完全な動作例

すべてをまとめたプログラムは以下の通りです。`Program.cs` にコピーして実行できます。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators.Gfx;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string dataDir = @"C:\MyPdfFolder\"; // <-- change to your folder
        using var pdfDocument = new Document(dataDir + "input.pdf");

        // -----------------------------------------------------------------
        // 2️⃣ Access the first page’s Resources dictionary
        // -----------------------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // -----------------------------------------------------------------
        // 3️⃣ Retrieve or create the ExtGState dictionary
        // -----------------------------------------------------------------
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

        // -----------------------------------------------------------------
        // 4️⃣ **Create empty PDF dictionary** for a new graphics state
        // -----------------------------------------------------------------
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode

        // -----------------------------------------------------------------
        // 5️⃣ Add the graphics state to ExtGState
        // -----------------------------------------------------------------
        extGStateDict.Add("GS0", newGraphicsState);

        // -----------------------------------------------------------------
        // 6️⃣ Save the modified PDF
        // -----------------------------------------------------------------
        pdfDocument.Save(dataDir + "output.pdf");

        Console.WriteLine("PDF saved with new empty dictionary at: " + dataDir + "output.pdf");
    }
}
```

**期待される出力** – コンソールに確認メッセージが表示され、`output.pdf` には `ExtGState` 配下に新しい `GS0` エントリが含まれます。ページのコンテンツストリームで `gs` 演算子を使って `GS0` を参照すれば、ストロークは完全に不透明、塗りは 50 % 透明になることが確認できます。

## よくある質問とエッジケースの対処

| 質問 | 回答 |
|----------|--------|
| *PDF に複数ページがある場合はどうすればよいですか？* | 本例は最初のページ（`Pages[1]`）を対象としています。すべてのページに適用したい場合は `pdfDocument.Pages` をループし、各ページのリソースに対して手順 3‑5 を繰り返してください。 |
| *既に “GS0” という名前の ExtGState エントリがあるページに辞書を追加できますか？* | 可能ですが、既存エントリを上書きしないように別のキー（`GS1`、`GS2` …）を使用する必要があります。 |
| *保存後に辞書を変更するのは安全ですか？* | `Save` を呼び出した後も、メモリ上の `Document` オブジェクトはファイルから切り離されています。必要に応じてさらに編集し、再度 `Save` することができます。 |
| *Aspose.Pdf のライセンスは必要ですか？* | はい、評価キーでも機能しますが、評価期間が過ぎると機能が制限されます。商用利用の場合は正式ライセンスをご購入ください。 |

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法に密接に関連するトピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能を習得したり、独自プロジェクトで代替実装を検討したりするのに役立ちます。

- [How to Create Dashed Lines in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [How to Remove Graphics from PDFs Using Aspose.PDF .NET&#58; A Complete Guide](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [How to Create Multi-Layer PDFs Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/advanced-features/create-multi-layer-pdfs-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}