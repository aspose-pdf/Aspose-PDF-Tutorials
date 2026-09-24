---
category: general
date: 2026-03-27
description: Aspose.Pdf for C# を使用して PDF に矩形を描く方法を学びましょう。PDF に矩形を追加し、形状を追加して、明確なコード例で
  PDF 上に形状を描画します。
draft: false
keywords:
- how to draw rectangle
- add rectangle to pdf
- add shape to pdf
- draw shape on pdf
- draw rectangle in pdf
language: ja
og_description: Aspose.Pdf を使用して PDF に矩形を描く方法をマスターしましょう。このチュートリアルでは、PDF に矩形を追加する方法、PDF
  に図形を追加する方法、そして PDF 上に図形を描く手順をステップバイステップで示します。
og_title: C#でPDFに矩形を描く方法 – 完全ガイド
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: C#でPDFに矩形を描く方法 – ステップバイステップガイド
url: /ja/net/images-graphics/how-to-draw-rectangle-in-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で PDF に矩形を描く方法 – ステップバイステップガイド

PDF の低レベル構文と格闘せずに **矩形の描き方** を疑問に思ったことはありませんか？ あなただけではありません。多くの開発者が、生成されたドキュメント内でバウンディングボックスやハイライト領域、あるいはシンプルな装飾要素を可視化する必要があるときに壁にぶつかります。良いニュースは、Aspose.Pdf for .NET を使えばこのプロセスはとても簡単です。

このチュートリアルでは、**PDF に矩形を追加する**、**PDF にシェイプを追加する**、そして最終的に **PDF に矩形を描く** ために必要なすべてを、クリーンで慣用的な C# を使って解説します。最後まで読むと、外部ツールを必要とせずに鮮明な矩形を含む PDF ファイルを生成する実行可能なプログラムが手に入ります。

## 前提条件

- .NET 6.0 以降（コードは .NET Core および .NET Framework でも動作します）
- Aspose.Pdf for .NET NuGet パッケージ（`Install-Package Aspose.Pdf`）
- 基本的な C# 開発環境（Visual Studio、VS Code、Rider など）

他のライブラリは不要です。残りはすべて Aspose.Pdf が処理します。

## 手順 1: プロジェクトの設定と名前空間のインポート

まず、新しいコンソール アプリケーションを作成し、Aspose.Pdf 名前空間をインポートします。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the rest of the code here.
        }
    }
}
```

**なぜ重要か:** `Aspose.Pdf.Drawing` をインポートすると、**PDF 上にシェイプを描く**ために使用する `Rectangle` シェイプ クラスにアクセスできます。エントリ ポイントを整理しておくことで、後続の手順が追いやすくなります。

## 手順 2: 新しい PDF ドキュメントとページの作成

ページのない PDF は意味がないため、まずドキュメント オブジェクトを作成し、単一のページを追加します。

```csharp
// Step 2: Initialize a new PDF document
Document pdfDoc = new Document();

// Add a blank page to the document (size defaults to A4)
Page page = pdfDoc.Pages.Add();
```

**説明:** `Document` クラスはファイル全体を表し、`Pages.Add()` は新しい `Page` オブジェクトを返します。このページに後で **PDF に矩形を追加** します。デフォルトの A4 サイズはほとんどのケースで機能しますが、カスタムキャンバスが必要な場合は幅/高さを指定できます。

## 手順 3: 矩形シェイプの定義

ここからが **矩形の描き方** の核心です — 位置とサイズを定義します。

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
// Coordinates are measured from the lower‑left corner of the page.
var rectangleShape = new Rectangle(100, 500, 300, 200)
{
    // Optional: set line color and fill color
    BorderColor = Color.Black,
    BorderWidth = 2,
    FillColor = Color.LightGray
};
```

**これらのプロパティを設定する理由:**  
- `BorderColor` と `BorderWidth` は輪郭を制御し、矩形を可視化します。  
- `FillColor` は控えめな背景色を付与し、領域をハイライトしたいときに便利です。  
- コンストラクタ `(x, y, width, height)` を使用すると、必要な場所に正確に **PDF に矩形を描く** ことができます。

## 手順 4: 矩形をページに追加

シェイプの準備ができたので、ページの `Annotations` コレクションに添付して **PDF にシェイプを追加** します。Aspose.Pdf が自動的に境界を検証するため、オーバーフローを心配する必要はありません。

```csharp
// Step 4: Add the rectangle shape to the page
page.Annotations.Add(rectangleShape);
```

**内部で何が起きているか:** `Annotations` コレクションは矩形をベクター グラフィックとして扱います。PDF がレンダリングされると、ライブラリは座標を PDF コンテンツ ストリームに変換します。

## 手順 5: ドキュメントの保存

最後に、PDF をディスクに書き出すので、任意のビューアで開くことができます。

```csharp
// Step 5: Save the PDF file
string outputPath = "RectangleDemo.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

**結果:** `RectangleDemo.pdf` を開くと、左端から 100 pt、ページ下端から 500 pt の位置に、黒い枠線と薄いグレーの塗りつぶしの矩形が表示されます。これが C# を使用して PDF に **矩形の描き方** の完全なソリューションです。

## 完全な動作例

すべての要素を組み合わせた、完全で実行可能なプログラムは以下の通りです：

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize a new PDF document
            Document pdfDoc = new Document();

            // Add a blank page (A4 by default)
            Page page = pdfDoc.Pages.Add();

            // Define a rectangle shape (x, y, width, height)
            var rectangleShape = new Rectangle(100, 500, 300, 200)
            {
                BorderColor = Color.Black,
                BorderWidth = 2,
                FillColor = Color.LightGray
            };

            // Add the rectangle to the page
            page.Annotations.Add(rectangleShape);

            // Save the document
            string outputPath = "RectangleDemo.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved to {outputPath}");
        }
    }
}
```

**期待される出力:** `RectangleDemo.pdf` という名前のファイルで、1 ページに中央に配置された薄いグレーの矩形が黒枠で囲まれています。Adobe Reader、Chrome、または任意の PDF ビューアで開くことができます。

## 一般的なバリエーションとエッジケース

### 1. 複数の矩形を描く

複数回 **PDF に矩形を追加** する必要がある場合は、追加の `Rectangle` オブジェクトを作成し、各々を `page.Annotations` に追加するだけです。座標のコレクションをループすれば簡単に実装できます。

```csharp
foreach (var rectInfo in rectangles)
{
    var rect = new Rectangle(rectInfo.X, rectInfo.Y, rectInfo.Width, rectInfo.Height)
    {
        BorderColor = Color.Blue,
        BorderWidth = 1,
        FillColor = Color.Transparent
    };
    page.Annotations.Add(rect);
}
```

### 2. 異なる単位の使用

Aspose.Pdf はポイント単位で動作します（1 pt = 1/72 インチ）。ミリメートル単位が好みの場合は、先に変換してください：

```csharp
double mmToPt = 72.0 / 25.4;
float x = (float)(20 * mmToPt); // 20 mm from left
float y = (float)(150 * mmToPt);
```

### 3. 矩形をフォームフィールドとして追加

インタラクティブな矩形（例: クリック領域）が必要な場合は、単純な `Rectangle` の代わりに `LinkAnnotation` を使用します。コードは似ていますが、URL や JavaScript アクションを追加します。

### 4. 互換性の懸念

Aspose.Pdf バージョン 23.9（2026 年初頭リリース）は、上記の API を完全にサポートしています。古いバージョンでは `page.Annotations.Add` の代わりに `page.AddAnnotation(rectangleShape)` が必要になる場合があります。コンパイルエラーが発生した場合は、必ずリリースノートを確認してください。

## プロのコツと落とし穴

- **プロのコツ:** アウトラインだけが必要な場合は `FillColor = Color.Transparent` を設定します。これによりファイルサイズが若干削減されます。
- **注意点:** ページ寸法を超える座標を使用しないこと。Aspose.Pdf は形状を静かにクリップするため、デバッグ時に混乱することがあります。
- **パフォーマンスに関する注意:** 数千個の矩形を追加するのは問題ありませんが、大規模なレポートを生成する場合は、オーバーヘッドを減らすために形状を単一の `Graphics` オブジェクトにバッチ処理することを検討してください。

## ビジュアルリファレンス

以下は生成された PDF の簡単なスクリーンショットです（矩形は薄いグレーでハイライトされています）。alt テキストには SEO 用の主要キーワードが含まれています。

![PDF で矩形を描く例](https://example.com/images/rectangle-demo.png "PDF で矩形を描く例")

## 結論

本稿では、Aspose.Pdf for C# を使用して PDF に **矩形の描き方** を解説しました。`Document` を作成し、`Page` を追加し、`Rectangle` シェイプを定義し、最終的に **PDF にシェイプを追加** することで、数行のコードだけでベクター グラフィックを生成できます。ハイライト、レイアウトデバッグ、UI オーバーレイのために **PDF に矩形を追加** したい場合でも、このアプローチはスケーラブルです。

次のステップとして、矩形以外の **PDF 上にシェイプを描く** 方法を探求できます—円やポリライン、カスタム SVG パスなどを考えてみてください。また、テキスト描画、画像挿入、PDF フォーム操作に取り組めば、フル機能のレポートを構築できます。Aspose.Pdf ライブラリは豊富な API を提供しており、ここで基礎を学んだので、自由に実験できます。

コーディングを楽しんで、作成する PDF が常に思い描いた通りになることを願っています！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}