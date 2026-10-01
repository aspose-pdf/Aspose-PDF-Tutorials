---
category: general
date: 2026-02-10
description: C# と Aspose.Pdf を使用して PDF ドキュメントを作成します。PDF にページを追加する方法と、境界チェックを利用して矩形を安全に
  PDF に追加する方法を学びます。
draft: false
keywords:
- create pdf document
- add page to pdf
- how to add rectangle pdf
language: ja
og_description: Aspose.Pdf を使用して C# で PDF ドキュメントを作成します。このガイドでは、PDF にページを追加する方法と、境界を確認しながら矩形を
  PDF に追加する方法を示します。
og_title: C#でPDFドキュメントを作成 – PDFにページを追加 & 矩形
tags:
- pdf
- csharp
- aspose
title: C#でPDFドキュメントを作成 – PDFにページを追加＆矩形
url: /ja/net/programming-with-pdf-pages/create-pdf-document-in-c-add-page-to-pdf-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で PDF ドキュメントを作成 – PDF にページを追加 & 四角形を描画

Ever needed to **create pdf document** in C# and weren’t sure where to start? You’re not alone—most developers hit the same roadblock when they first dabble with PDF generation libraries. The good news is that with Aspose.Pdf you can spin up a PDF, add a page to PDF, and even draw shapes like a rectangle without breaking a sweat.

このチュートリアルでは、**creates a PDF document**（PDF ドキュメントの作成）だけでなく、グローバルな境界チェックを有効にして **how to add rectangle pdf**（四角形 PDF オブジェクトの追加）を安全に行う方法を示す、完全で実行可能なサンプルを順に解説します。最後まで読むと API をしっかり理解でき、各ステップの重要性が分かり、期待すべき正確な出力を確認できます。

## 必要なもの

- .NET 6+（または .NET Framework 4.6+）。コードはどちらでも同じように動作します。
- Aspose.Pdf for .NET NuGet パッケージ（`Aspose.Pdf`） – `dotnet add package Aspose.Pdf` でインストールします。
- 任意の C# エディタ（Visual Studio、VS Code、Rider など）を使用してください。

追加の設定は不要です。ライブラリには PDF の生成をすぐに開始するために必要なものがすべて含まれています。

## 手順 1: PDF ドキュメントを作成し、境界チェックを有効化

最初に行うのは `Document` オブジェクトのインスタンス化です。これは **create pdf document**（PDF ドキュメント作成）のための白紙キャンバスと考えてください。その直後に、ライブラリがすべてのグラフィックオブジェクトがページ領域内に収まっているかを検証するグローバル設定を有効にします。後でページ端からはみ出す可能性のある図形を描画しようとする際に非常に重要です。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Initialise a new PDF document
using var document = new Document();

// Step 1b: Turn on boundary checking for all graphics objects
document.FileStructureSettings.CheckGraphicsObjectBoundaries = true;
```

*なぜ境界チェックを有効にするのか？*  
矩形を誤ってページ外に配置すると、Aspose は `PdfException` をスローします。早期に捕捉することで、一部のビューアが開くことさえ拒否するような破損した PDF を防げます。

## 手順 2: PDF にページを追加

ページのない PDF は、ページのない本と同じでほとんど役に立ちません。ページを追加するには `Pages.Add()` を呼び出すだけです。このメソッドはコンテンツを配置するために使用する `Page` オブジェクトを返します。

```csharp
// Step 2: Add a new page (this is the “add page to pdf” part)
Page page = document.Pages.Add();
```

> **プロのコツ:** Aspose のデフォルトページサイズは 595 × 842 ポイント（A4）です。別のサイズが必要な場合は、コンテンツを追加する前に `page.PageInfo.Width` と `page.PageInfo.Height` を設定できます。

## 手順 3: ページ外になる矩形を定義

ここで **how to add rectangle pdf**（四角形 PDF オブジェクトの追加）の核心に入ります。ページサイズを超える矩形を意図的に作成し、例外がどのように発生するかを確認します。`Rectangle` コンストラクタは 4 つの引数を取ります：*左下 X、左下 Y、右上 X、右上 Y*。

```csharp
// Step 3: Create a rectangle that goes beyond the page edges
// Page size: 595x842, so X=800 and Y=900 are out of bounds
var outOfBoundsRect = new Rectangle(400, 750, 800, 900);
```

境界チェックを無効にした状態でコードを実行すると、矩形は単にクリップされます。チェックを有効にすると、Aspose はエラーを発生させます。これは堅牢な PDF 生成パイプラインにとって望ましい動作です。

## 手順 4: シェイプを作成し、見える枠線を付ける

矩形単体では枠線や塗りつぶしが無い限り目に見えません。ここでは `Rectangle` を `Rectangle` シェイプオブジェクトでラップし（クラス名が少し紛らわしいですが）、細い黒枠を設定します。

```csharp
// Step 4: Turn the rectangle into a shape and add a border
var rectangleShape = new Rectangle(outOfBoundsRect)
{
    Border = new BorderInfo(BorderSide.All, 1f)   // 1‑point black border
};
```

*なぜ枠線が必要か？*  
枠線が無いとページ上に何も見えず、デバッグが困難になります。細い枠線にすることで、シェイプがページ外にあるかどうかが一目で分かります。

## 手順 5: シェイプをページに追加 – 例外が発生することを期待

ここで実際にシェイプをページに配置します。矩形がページの限界を超えており、境界チェックが有効になっているため、Aspose は `PdfException` をスローします。エラー処理を優雅に示すために、呼び出しを `try/catch` ブロックでラップします。

```csharp
// Step 5: Attempt to add the shape – this will raise an exception
try
{
    page.Paragraphs.Add(rectangleShape);
}
catch (PdfException ex)
{
    Console.WriteLine("Caught PdfException: " + ex.Message);
    // Handle the error – maybe adjust the rectangle or log the issue
}
```

手順 1 の `CheckGraphicsObjectBoundaries` 行をコメントアウトすれば、コードは正常に実行され、矩形はページ端でクリップされます。この動作は簡易プロトタイプ作成には便利ですが、本番環境では通常、安全ネットを有効にしたいでしょう。

## 手順 6: PDF を保存

最後に、ドキュメントをディスクに保存します。ファイルは指定したフォルダーに作成されますので、パスが存在することを確認するか、`Environment.CurrentDirectory` と `Path.Combine` を使用してください。

```csharp
// Step 6: Save the resulting PDF
string outputPath = Path.Combine(Environment.CurrentDirectory, "checked_shapes.pdf");
document.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

`checked_shapes.pdf` を開くと空白ページが表示されます（矩形が拒否されたため）。境界チェックを外すと、右側と上側でクリップされた部分的な矩形が描画されているのが見えます。

![矩形の境界チェックを示す PDF ドキュメント作成例](https://example.com/images/checked_shapes.png "矩形の境界チェック付き PDF ドキュメント作成例")

*上のスクリーンショットは、境界チェックを無効にした状態でチュートリアルを実行した後の PDF を示しています（矩形がクリップされています）。チェックを有効にすると、シェイプは省略され、例外が記録されます。*

## まとめ: 完全動作サンプル

すべてをまとめると、以下が完全な実行可能プログラムです。

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise document and enable boundary checking
        using var document = new Document();
        document.FileStructureSettings.CheckGraphicsObjectBoundaries = true;

        // 2️⃣ Add a page (add page to pdf)
        Page page = document.Pages.Add();

        // 3️⃣ Define an out‑of‑bounds rectangle (how to add rectangle pdf)
        var outOfBoundsRect = new Rectangle(400, 750, 800, 900);

        // 4️⃣ Create shape with a visible border
        var rectangleShape = new Rectangle(outOfBoundsRect)
        {
            Border = new BorderInfo(BorderSide.All, 1f)
        };

        // 5️⃣ Try to add the shape – expect an exception
        try
        {
            page.Paragraphs.Add(rectangleShape);
        }
        catch (PdfException ex)
        {
            Console.WriteLine("Caught PdfException: " + ex.Message);
        }

        // 6️⃣ Save the PDF
        string outputPath = Path.Combine(Environment.CurrentDirectory, "checked_shapes.pdf");
        document.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

プログラムを実行すると、例外が捕捉されたかどうかを示すコンソール出力が表示されます。生成された PDF を開いて結果を確認してください。

## よくある質問とエッジケース

- **別のページサイズが必要な場合は？**  
  シェイプを追加する前に `page.PageInfo.Width` と `page.PageInfo.Height` を設定します。境界チェッカーは自動的に新しい寸法を使用します。

- **単一のシェイプだけ境界チェックを無効にできますか？**  
  直接的にはできません。この設定はグローバルです。ただし、一時的にオフにしてシェイプを追加し、再びオンにすることは可能です。その操作では安全ネットが失われることに注意してください。

- **例外メッセージは有用ですか？**  
  はい、Aspose は問題の座標を含めてくれるので、プログラムで矩形を調整したり、詳細な診断情報をログに記録したりできます。

- **Linux 上の .NET Core でも動作しますか？**  
  完全に動作します。Aspose.Pdf はプラットフォームに依存せず、参照するフォントファイルが対象 OS に存在することを確認すれば問題ありません。

## 次のステップ

これで **how to add rectangle pdf**（四角形 PDF オブジェクトの追加） と **add page to pdf**（PDF にページを追加） の方法が分かったので、以下を検討してみてください：

- 同じ境界チェックを使って他のグラフィックタイプ（楕円、線など）を追加する。
- テキスト、画像、テーブルの挿入—Aspose はそれぞれにリッチな API を提供しています。
- `Document.Save` のオーバーロードを使用して、Web API 用に `MemoryStream` へ直接出力する。

さまざまな矩形座標、枠線、塗りつぶし色で実験してみてください。試せば試すほど、Aspose.P の動作をより深く理解できるでしょう。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}