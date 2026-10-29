---
category: general
date: 2026-09-12
description: C# で Aspose.PDF を使用して PDF に透過性を追加し、矩形を描画し、透過性付きで PDF を保存する方法をステップバイステップで学ぶガイド。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- draw rectangle on pdf
- save pdf with transparency
language: ja
lastmod: 2026-09-12
og_description: Aspose.PDF for C# を使用して PDF に透明度を追加し、PDF 上に矩形を描画し、透明度付きで PDF を保存します。この完全なチュートリアルに従ってください。
og_image_alt: Screenshot of a PDF page showing a semi‑transparent rectangle drawn
  with Aspose.PDF
og_title: PDFに透明度を追加し、矩形を描画する – 完全なC#ガイド
schemas:
- author: Aspose
  dateModified: '2026-09-12'
  description: Learn how to add transparency to PDF, draw a rectangle on PDF, and
    save PDF with transparency using Aspose.PDF in C# – step‑by‑step guide.
  headline: How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Aspose.PDFでPDFに透明度を追加し、矩形を描画する方法
url: /ja/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDFに透明度を追加し、Aspose.PDFで矩形を描画する方法

PDFファイルに**透明度を追加**する必要がある場合、このガイドではC#でその方法を正確に示します。また、**PDFに矩形を描画**する方法と、最終的に**透明度付きPDFを保存**する方法も学べます。結果はレポートや請求書、またはあらゆる文書自動化ワークフローで再利用できます。

このチュートリアルで学べること:

* 既存の PDF ドキュメントを読み込む。
* ストロークと塗りの不透明度を定義するカスタム グラフィックス ステートを作成する。
* そのグラフィックス ステートをキャンバスに適用し、矩形を描画する。
* 透明度設定を保持したまま変更後のファイルを保存する。

Aspose.PDF for .NET ライブラリ以外に外部ツールは不要で、コードの各行がなぜ必要かを説明しています。

## Prerequisites

* .NET 6.0 以降（コードは .NET Framework 4.7+ でも動作します）。
* **Aspose.PDF for .NET** のライセンス版または評価版。NuGet でインストールします:

```bash
dotnet add package Aspose.Pdf
```

* プロジェクトから参照できるフォルダーに配置した入力 PDF（`input.pdf`）。

## Step 1: Load the PDF document

最初の操作はソース ファイルを開くことです。`using` ステートメントを使用すると、ドキュメントが適切に破棄され、後で保存しようとしたときのファイル ロック問題を防止できます。

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";
using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

*Why this matters*: ドキュメントを読み込むことで、描画に必要なページ コレクション、リソース ディクショナリ、キャンバス オブジェクトにアクセスできるようになります。

## Step 2: Access the first page’s resource dictionary

すべての PDF ページは **リソース ディクショナリ** を持ち、フォント、画像、グラフィックス ステートなどのオブジェクトが格納されています。新しい透明度設定を導入するには、`ExtGState` エントリを編集する必要があります。

```csharp
// Step 2: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

*Why this matters*: `DictionaryEditor` を使用すると、ドキュメント構造を壊さずに低レベルの PDF オブジェクトを読み書きできます。

## Step 3: Create a custom graphics state with transparency values

グラフィックス ステート（`ExtGState`）は描画操作のレンダリング方法を制御します。ここでは 2 つの不透明度パラメータを定義します:

* **CA** – ストローク（輪郭）の不透明度。
* **ca** – 塗り（内部）の不透明度。

さらにブレンドモード（`BM`）を “Normal” に設定します。これは最も一般的な合成操作です。

```csharp
// Step 3: Create a custom graphics state (ExtGState) with transparency settings
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
var customGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "CA", new Aspose.Pdf.Cos.CosPdfNumber(1)),          // stroke opacity = 100 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),        // fill opacity = 50 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))      // normal blend mode
};

foreach (var p in parameters)
    customGs.Add(p);

// Register the new graphics state under the name "GS0"
extGStateDict.Add("GS0", customGs);
```

*Why this matters*: `GS0` を `ExtGState` ディクショナリに追加することで、キャンバスが描画前に有効化できる再利用可能な参照が作成されます。`0.5` の塗り不透明度により矩形が半透明になり、**PDF に透明度を追加**する目的が達成されます。

## Step 4: Apply the graphics state and draw a rectangle

ページのキャンバスに先ほど作成したグラフィックス ステートを使用させ、矩形を描画します。座標は PDF の座標系（左下が原点）に従います。

```csharp
// Step 4: Apply the custom graphics state and draw a rectangle
var canvas = firstPage.Canvas;

// Activate the transparency graphics state
canvas.SetGraphicsState("GS0");

// Draw a rectangle from (100, 500) to (200, 600)
canvas.Rectangle(100, 500, 200, 600);

// Render the rectangle outline using the current graphics state
canvas.Stroke();
```

*Why this matters*: `SetGraphicsState("GS0")` は描画コンテキストを先に定義した透明度設定に切り替えます。`Rectangle` メソッドで形状を定義し、`Stroke` が指定した不透明度で輪郭を描画します。塗りつぶし矩形が必要な場合は `Stroke()` を `FillAndStroke()` に置き換えてください。

## Step 5: Save the modified PDF while preserving transparency

最後にドキュメントをディスクに書き戻します。出力ファイルには新しいグラフィックス ステート、描画した矩形、そして透明度情報が含まれます。

```csharp
// Step 5: Save the modified PDF
string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
pdfDocument.Save(outputPath);
```

*Why this matters*: ドキュメントを保存することで全ての変更が確定します。生成されたファイルは任意の PDF ビューアで開くことができ、矩形は 50 % の塗り不透明度で表示されます。

### Expected result

`output_with_extgstate.pdf` を開くと、枠線は完全に不透明で内部が半透明の矩形が表示され、下にあるページ コンテンツが透けて見えるはずです。

## Edge cases and practical tips

| 状況 | 推奨調整 |
|-----------|------------------------|
| **複数ページ** | `pdfDocument.Pages` をループし、各対象ページで手順 2‑4 を繰り返します。 |
| **異なる不透明度の値** | `CA`（ストローク）と `ca`（塗り）の `CosPdfNumber` の値を `0`（完全に透明）から `1`（完全に不透明）の間の任意の数に変更します。 |
| **カスタムブレンドモード** | `"Normal"` を `"Multiply"`、`"Screen"`、またはビューアがサポートする任意の PDF 標準ブレンドモードに置き換えます。 |
| **塗りつぶし矩形** | `canvas.Stroke()` の代わりに `canvas.FillAndStroke()` を呼び出して、塗りと輪郭の両方を適用します。 |
| **同じグラフィックスステートの再利用** | 同じページ上で任意の数の図形を描画する前に `canvas.SetGraphicsState("GS0")` を呼び出すことができます。 |

**Pro tip:** 新しい `ExtGState` を追加した後は必ずリソース ディクショナリを確認してください。ディクショナリが存在しない場合は、まず作成します:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
    resourcesEditor.Add("ExtGState", new Aspose.Pdf.Cos.CosPdfDictionary(pdfDocument));
```

## Full, runnable example

以下は自己完結型のプログラムです。コンソール アプリケーションにコピーしてすぐに実行できます（`YOUR_DIRECTORY` を実際のパスに置き換えてください）。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF document
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Access the first page’s resources
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        if (!resourcesEditor.ContainsKey("ExtGState"))
            resourcesEditor.Add("ExtGState", new CosPdfDictionary(pdfDocument));

        // 3️⃣ Create a custom graphics state with transparency
        var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        var customGs = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };

        foreach (var p in parameters)
            customGs.Add(p);

        extGStateDict.Add("GS0", customGs);

        // 4️⃣ Apply the graphics state and draw a rectangle
        var canvas = firstPage.Canvas;
        canvas.SetGraphicsState("GS0");
        canvas.Rectangle(100, 500, 200, 600);
        canvas.Stroke(); // use FillAndStroke() for a filled shape

        // 5️⃣ Save the PDF with transparency
        string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine("PDF saved with a transparent rectangle at: " + outputPath);
    }
}
```

プログラムを実行すると `output_with_extgstate.pdf` が生成され、**PDF に透明度を追加**、**PDF に矩形を描画**、**透明度付き PDF を保存** がすべて一連の流れでデモンストレーションされます。

## Conclusion

これで Aspose.PDF for .NET を使用して **PDF に透明度を追加**し、**PDF に矩形を描画**し、**透明度付き PDF を保存**する方法が分かりました。プロセスはカスタム `ExtGState` を作成し、キャンバスに適用し、変更を永続化することに集約されます。この基本ブロックを活用すれば、他の形状や複数ページ、動的な不透明度値にも応用できます。

**Next steps**

* `canvas.Ellipse`、`canvas.Path`、`canvas.TextFragment` などの他の描画プリミティブを同じグラフィックス ステートで試す。
* 透明度と画像オーバーレイを組み合わせて透かし（`canvas.Image` + カスタム `ExtGState`）を作成する。
* 高度な合成効果のために **graphics state parameters** に関する Aspose.PDF ドキュメントを確認する。

Happy coding, and enjoy the visual flexibility that transparency brings to your PDF workflows!

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [C#でPDFを作成する方法 – ページ追加、矩形描画 & 保存](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [Aspose.PDF for .NETでPDFに線オブジェクトを追加する方法: ステップバイステップガイド](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Aspose.PDF for .NETでPDFに画像スタンプを追加する方法: ステップバイステップガイド](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}