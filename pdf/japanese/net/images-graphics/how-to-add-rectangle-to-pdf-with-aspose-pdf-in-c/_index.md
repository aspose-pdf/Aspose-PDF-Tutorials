---
category: general
date: 2026-10-10
description: Aspose.PDF を使用して PDF に矩形を追加し、図形を描画し、変更された PDF を保存する方法を学びます。特定の PDF ページにアクセスするためのステップバイステップガイドが含まれています。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to PDF
- draw shape on PDF
- save modified PDF
- add shape to PDF
- access specific PDF page
language: ja
lastmod: 2026-10-10
og_description: C#でAspose.PDFを使用してPDFに矩形を追加する。このチュートリアルでは、PDFに図形を描画し、特定のPDFページにアクセスし、変更されたPDFを保存する方法を示します。
og_image_alt: Screenshot of a PDF page with a blue rectangle overlay created by Aspose.PDF
og_title: Aspose.PDFでPDFに矩形を追加する – 完全なC#ガイド
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  headline: How to add rectangle to PDF with Aspose.PDF in C#
  type: TechArticle
- description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  name: How to add rectangle to PDF with Aspose.PDF in C#
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: What if the PDF has only one page?
    text: Attempting to access `pdfDocument.Pages[1]` throws an `ArgumentOutOfRangeException`.
      Guard against this by checking `pdfDocument.Pages.Count` before indexing.
  - name: How to add multiple rectangles on different pages?
    text: Repeat Steps 2‑4 for each target page, adjusting the rectangle’s coordinates
      as needed. You can place the logic inside a loop that iterates over `pdfDocument.Pages`.
  - name: Can I use other shapes such as circles or polygons?
    text: Yes. Aspose.PDF provides `Ellipse`, `Polygon`, and `Polyline` classes that
      follow the same pattern as `Rectangle`. Replace the `new Aspose.Pdf.Drawing.Rectangle`
      call with the desired shape class.
  - name: Does the library support PDFs with rotated pages?
    text: Aspose.PDF automatically respects page rotation when rendering shapes. The
      rectangle’s coordinates are interpreted in the page’s native coordinate system,
      so no extra transformation is required.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: C#でAspose.PDFを使用してPDFに矩形を追加する方法
url: /ja/net/images-graphics/how-to-add-rectangle-to-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.PDF for .NET を使用して C# で PDF に矩形を追加する方法

PDF ファイルに **矩形を追加** したい場合、このガイドで手順をすべて解説します。**PDF に図形を描画** し、特定のページを対象にし、**変更した PDF をエラーなく保存** する方法を学びます。

PDF 文書の操作は、レポート作成、請求書発行、文書への注釈付けなどで一般的な要件です。このチュートリアルを終える頃には、**PDF に図形を追加** でき、範囲外エラーの処理や任意の .NET プロジェクトへの組み込みが自信を持って行えるようになります。

## 前提条件

開始する前に、以下が揃っていることを確認してください。

* .NET 6.0 SDK 以降がインストール済み  
* Visual Studio 2022（または任意の C# IDE）  
* Aspose.PDF for .NET のライセンスまたは無料評価キー – API の動作は両モードで同一です  
* `input.pdf` という名前の PDF ファイルを、コードから参照できるフォルダーに配置  

これらがサンプルで必要となる唯一の外部依存項目です。

## 手順 1: Aspose.PDF NuGet パッケージをインストール

Aspose.PDF ライブラリは、`Document`、`Rectangle` など、必要な描画クラスを提供します。

```bash
dotnet add package Aspose.PDF
```

このコマンドを実行すると、最新の安定版 Aspose.PDF がプロジェクトに追加され、PDF クラスがコンパイル時に利用可能になります。

## 手順 2: PDF 文書を読み込む

最初の操作はソースファイルをロードすることです。これにより、メモリ上に変更可能な表現が作成されます。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;

class PdfRectangleExample
{
    static void Main()
    {
        // Load the PDF document from disk
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

*なぜ重要か*: 文書をロードすると、ページコレクションへアクセスできるようになり、後で **特定の PDF ページにアクセス** できるようになります。

## 手順 3: 2 ページ目（ゼロベースインデックス）にアクセス

PDF のページは `0` からインデックス付けされます。2 ページ目に矩形を配置するには、インデックス `1` のページを取得します。

```csharp
        // Access the second page (pages are zero‑based)
        var page = pdfDocument.Pages[1];
```

文書に 2 ページ未満しかない場合、`ArgumentOutOfRangeException` がスローされます。実運用コードではガード句が必要です。

## 手順 4: 矩形形状を作成

`Rectangle` 構造体で矩形の位置とサイズを定義し、Aspose の描画オブジェクトでラップします。

```csharp
        // Define rectangle bounds: (x, y, width, height)
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            // Optional visual styling
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };
```

*なぜ重要か*: `BorderInfo` と `FillColor` プロパティを使うことで、**PDF に図形を描画** でき、輪郭と任意の塗りつぶしで矩形を目立たせられます。

## 手順 5: 矩形をページの段落コレクションに追加

Aspose.PDF は描画オブジェクトを段落要素として扱います。矩形をページの `Paragraphs` コレクションに追加すると、ページ上に描画されます。

```csharp
        // Add the rectangle shape to the page
        page.Paragraphs.Add(rectangleShape);
```

この時点でメモリ上の PDF 文書には新しい図形が含まれますが、ディスク上のファイルは保存するまで変更されません。

## 手順 6: 変更した PDF を保存し、範囲外エラーに対処

`Save` を呼び出すと、更新された文書が新しいファイルに書き込まれます。矩形がページサイズを超えると Aspose は `PdfException` をスローします。この例外を捕捉して問題を適切に報告できます。

```csharp
        try
        {
            // Save the altered PDF to a new file
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            // Handle shape that does not fit on the page
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

*なぜ重要か*: `try/catch` ブロックにより、アプリケーションは **変更した PDF を安全に保存** でき、エラーメッセージで矩形座標の調整が容易になります。

## 完全な動作サンプル

すべての手順をまとめた、実行可能な完全プログラムは以下の通りです。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;
using System.Drawing; // Required for Color

class PdfRectangleExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // Step 2: Access the second page (zero‑based)
        var page = pdfDocument.Pages[1];

        // Step 3: Create a rectangle shape positioned at (100,100) with width 300 and height 200
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };

        // Step 4: Add the rectangle shape to the page's paragraph collection
        page.Paragraphs.Add(rectangleShape);

        // Step 5: Save the modified PDF, handling out‑of‑bounds cases
        try
        {
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

### 期待される出力

プログラムを実行すると次のように表示されます。

```
PDF saved successfully with rectangle added.
```

そして `output.pdf` が生成され、元のコンテンツに加えて 2 ページ目の指定座標に青い矩形が描画されます。

矩形がページより大きい場合は、次のような例外メッセージが表示されます。

```
Shape out of bounds: The shape exceeds page margins.
```

## よくある質問とエッジケース

### PDF が 1 ページしかない場合は？

`pdfDocument.Pages[1]` にアクセスすると `ArgumentOutOfRangeException` がスローされます。インデックス付けする前に `pdfDocument.Pages.Count` を確認してガードしてください。

```csharp
if (pdfDocument.Pages.Count < 2)
{
    Console.WriteLine("Document does not contain a second page.");
    return;
}
```

### 複数ページに複数の矩形を追加したい場合は？

対象ページごとに手順 2‑4 を繰り返し、座標を調整します。`pdfDocument.Pages` を走査するループにロジックを組み込むと便利です。

### 円や多角形など他の形状は使えるか？

はい。Aspose.PDF には `Ellipse`、`Polygon`、`Polyline` クラスがあり、`Rectangle` と同様のパターンで使用できます。`new Aspose.Pdf.Drawing.Rectangle` の呼び出しを目的の形状クラスに置き換えてください。

### 回転ページを含む PDF に対応しているか？

Aspose.PDF はページ回転を自動的に考慮して形状を描画します。矩形の座標はページのネイティブ座標系で解釈されるため、追加の変換は不要です。

## パフォーマンス上の考慮点

* **メモリ使用量** – 数百 MB の大容量 PDF を読み込むと比例したメモリが必要です。単一ページだけを変更する場合は `PdfFileInfo` で対象ページを抽出し、変更後に結合する方法を検討してください。  
* **バッチ処理** – 多数の文書に図形を追加する際は、`License` インスタンスを 1 つだけ再利用してライセンス検証のオーバーヘッドを削減しましょう。

## 次のステップ

**PDF に矩形を追加**できたら、以下の関連トピックも学んでみてください。

* **draw shape on PDF** – テキスト、画像、透かしのオーバーレイ方法  
* **add shape to PDF** – 複数の図形を単一の注釈レイヤーに統合  
* **save modified PDF** – `MemoryStream` を使って Web API から直接 PDF を返す方法  
* **access specific PDF page** – カスタムレポート用にページ範囲抽出を実装  

さまざまな色、線種、透明度を試して、ブランドガイドラインに合わせた見た目を実現しましょう。

---

*Happy coding! If this tutorial helped you **add rectangle to PDF**, consider sharing it with teammates or contributing improvements back to the community.*

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、API の追加機能を習得したり、プロジェクトで代替実装を検討したりするのに役立ちます。

- [Aspose.PDF for .NET を使用して C# で PDF に図形を追加する方法 – ステップバイステップガイド](/pdf/english/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Aspose.PDF for .NET で PDF に直線オブジェクトを追加する方法 – ステップバイステップガイド](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [C# で PDF を作成する – ページ追加、矩形描画、保存](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}