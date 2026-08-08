---
category: general
date: 2026-06-18
description: C#でAspose.PDFを使用してPDFに図形を追加する方法 – PDFを読み込み、矩形を描画し、保存する。
draft: false
keywords:
- how to add shape to pdf
- load pdf document in c#
- how to draw shapes in pdf
- aspose pdf add rectangle
language: ja
og_description: C#でAspose.PDFを使用してPDFに図形を追加する方法。PDFドキュメントを読み込み、矩形を描画し、更新されたファイルを保存する手順を学びます。
og_title: C#でAspose.PDFを使用してPDFに図形を追加する方法
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: How to add shape to PDF using Aspose.PDF in C# – load a PDF, draw a
    rectangle, and save it.
  headline: How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide
  type: TechArticle
- description: How to add shape to PDF using Aspose.PDF in C# – load a PDF, draw a
    rectangle, and save it.
  name: How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide
  steps:
  - name: What if I need to draw on multiple pages?
    text: Simply loop over `pdfDoc.Pages` and call `AddRectangle` (or any other shape)
      for each page. Remember to adjust coordinates if pages have different sizes.
  - name: Can I fill the rectangle with a color?
    text: Absolutely. Change `FillColor` from `Transparent` to any `Color` you like,
      e.g., `Color.Yellow`. The shape will appear as a solid block.
  - name: Does this work with password‑protected PDFs?
    text: 'Aspose.PDF can open encrypted files if you supply the password:'
  - name: How to add a rectangle with rounded corners?
    text: Use the `RoundedRectangle` class instead of `Rectangle`. The rest of the
      steps stay identical.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: C#でAspose.PDFを使用してPDFに図形を追加する方法 – ステップバイステップガイド
url: /ja/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Aspose.PDF を使用して PDF に形状を追加する方法 – 完全チュートリアル

低レベルのバイトストリームと格闘せずに **PDF に形状を追加する方法** を考えたことはありませんか？実際のアプリケーションでは、領域をハイライトしたり、条項に下線を引いたり、署名フィールドのために単にバウンディングボックスを描いたりする必要があります。良いニュースは、Aspose.PDF を使えばこれがとても簡単になることです。このガイドでは、C# で PDF ドキュメントを読み込み、矩形を描画し、結果を保存します—それ以上でもそれ以下でもありません。

コードの各行を順に解説し、各要素が *なぜ* 必要なのかを説明し、形状が期待通りの位置に描画されたことをすぐに確認する方法もお見せします。最後まで読むと、**PDF に形状を描く方法** に慣れ、任意の .NET プロジェクトに貼り付けて使える再利用可能なスニペットを手に入れられます。

## 前提条件

- **.NET 6.0**（または最近の .NET バージョン）をマシンにインストールしておくこと。  
- **有効な Aspose.PDF for .NET ライセンス**（または無料評価キー）。  
- Visual Studio 2022、Rider、またはお好みのエディタ。  
- 参照できるフォルダーに配置した既存の PDF ファイル（`input.pdf`）。

> **プロのコツ:** テストだけの場合は、無料評価版で十分です—小さな透かしが追加されますが、その他はフル製品と同様に動作します。

## ステップ 1: プロジェクトの設定と名前空間のインポート

まず、新しいコンソールプロジェクトを作成（または既存プロジェクトに追加）し、必要な名前空間をインポートします。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;   // Required for shape classes
```

なぜ重要かというと、`Aspose.Pdf` はコアのドキュメントモデルを提供し、`Aspose.Pdf.Drawing` には後で使用する `Rectangle` 形状クラスが含まれています。後者がなければ、コンパイラは `Rectangle` が未定義であるとエラーを出します。

## ステップ 2: C# で PDF ドキュメントを読み込む

ここで実際に **C# で PDF ドキュメントを読み込む** ことになります。既存のファイルを変更する際に最初に行う操作です。

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";
Document pdfDoc = new Document(inputPath);
Console.WriteLine($"Loaded PDF with {pdfDoc.Pages.Count} page(s).");
```

*説明*:  
- `Document` はファイル全体を表す Aspose のオブジェクトです。  
- コンストラクタにフルパスを渡すことでファイルがメモリに読み込まれます。  
- `Console.WriteLine` 行はオプションですが、デバッグに便利です—ページ数が 0 なら早い段階で問題があることが分かります。

## ステップ 3: 矩形形状の定義

ここが **PDF に形状を追加する方法** の核心です。ページの左下隅を (0,0) とする座標系で位置とサイズを指定する `Rectangle` オブジェクトを作成します。

```csharp
// Step 3: Define a rectangle (left, bottom, right, top)
Rectangle rect = new Rectangle(0, 0, 200, 100)
{
    // Optional styling – you can tweak these as needed
    FillColor = Color.Transparent,          // No fill, just the border
    Border = new Border(BorderStyle.Solid, 2, Color.Red)
};
```

`FillColor` を透明に設定する理由: 多くのケースでは輪郭だけが欲しい（ハイライトボックスを想像してください）。`Border` プロパティで太さと色を制御でき、赤色は標準的な白紙ページ上で矩形を目立たせます。

## ステップ 4: 形状がページ境界内に収まっているか確認する

`**矩形を追加する**` 前に、形状がページ端をはみ出さないか確認する習慣をつけましょう。Aspose にはこの目的のために `ValidateShapeBounds` が用意されています。

```csharp
// Step 4: Validate that the rectangle fits on the first page
bool fits = pdfDoc.Pages[1].ValidateShapeBounds(rect);
if (!fits)
{
    Console.WriteLine("Rectangle exceeds page dimensions – adjusting...");
    // Simple fallback: shrink to fit the page width
    rect.Right = pdfDoc.Pages[1].PageInfo.Width - 10;
    rect.Top  = pdfDoc.Pages[1].PageInfo.Height - 10;
}
```

*理由*: ページ外に描画しようとすると描画の乱れや例外が発生することがあります。このチェックにより、サイズに関係なく PDF でチュートリアルが安定します。

## ステップ 5: 対象ページに矩形を追加する

いよいよ **PDF に形状を追加する** 時です。`AddRectangle` メソッドは形状をページのアノテーションコレクションに追加し、PDF ビューアは他の描画と同様に表示します。

```csharp
// Step 5: Add the rectangle to the first page
pdfDoc.Pages[1].AddRectangle(rect);
Console.WriteLine("Rectangle added to page 1.");
```

別のページを対象にしたい場合は、インデックス `1` を目的のページ番号に置き換えるだけです（Aspose は 1 ベースのインデックスを使用します）。

## ステップ 6: 変更した PDF を保存する

最後のステップは変更をディスクに書き戻すことです。元のファイルを上書きすることも、新しいファイルを作成することもできます—ここでは `output.pdf` を生成します。

```csharp
// Step 6: Save the updated PDF
string outputPath = @"YOUR_DIRECTORY\output.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved as {outputPath}");
```

*期待される結果*: `output.pdf` を Adobe Reader などのビューアで開くと、1 ページ目の左下隅に鮮明な赤い矩形が表示されます。

![PDF に追加された矩形を示す図](https://example.com/rectangle-diagram.png "PDF に形状を追加する例")

*Alt text*: "PDF に形状を追加する – PDF ファイルの 1 ページ目に描かれた矩形"

## ステップ 7: 完全動作例（コピー＆ペースト可能）

以下はすぐにコンパイルして実行できる完全なプログラムです。`YOUR_DIRECTORY` は実際のフォルダー パスに置き換えてください。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;   // For color definitions

namespace PdfShapeDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the PDF document in C#
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document pdfDoc = new Document(inputPath);
            Console.WriteLine($"Loaded PDF with {pdfDoc.Pages.Count} page(s).");

            // Define the rectangle shape
            Rectangle rect = new Rectangle(0, 0, 200, 100)
            {
                FillColor = Color.Transparent,
                Border = new Border(BorderStyle.Solid, 2, Color.Red)
            };

            // Validate bounds on the first page
            if (!pdfDoc.Pages[1].ValidateShapeBounds(rect))
            {
                Console.WriteLine("Rectangle exceeds page dimensions – adjusting...");
                rect.Right = pdfDoc.Pages[1].PageInfo.Width - 10;
                rect.Top  = pdfDoc.Pages[1].PageInfo.Height - 10;
            }

            // Add the rectangle (how to add shape to pdf)
            pdfDoc.Pages[1].AddRectangle(rect);
            Console.WriteLine("Rectangle added to page 1.");

            // Save the modified PDF
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved as {outputPath}");
        }
    }
}
```

プログラムを実行し、`output.pdf` を開くと、配置した通りに赤い矩形が表示されます。別の形状（楕円、線、ポリゴン）が必要な場合は、`Rectangle` を `Ellipse`、`Line`、または `Polygon` に置き換えるだけで、同じ手順が使えます。これが実質的に Aspose を使った **PDF に形状を描く方法** です。

## よくある質問とエッジケース

### 複数ページに描画したい場合は？

`pdfDoc.Pages` をループし、各ページで `AddRectangle`（または他の形状）を呼び出すだけです。ページサイズが異なる場合は座標を調整してください。

```csharp
foreach (Page page in pdfDoc.Pages)
{
    page.AddRectangle(rect);
}
```

### 矩形を色で塗りつぶすことはできますか？

もちろんです。`FillColor` を `Transparent` から好きな `Color`（例: `Color.Yellow`）に変更すれば、形状は塗りつぶされたブロックとして表示されます。

### パスワード保護された PDF でも動作しますか？

パスワードを指定すれば、Aspose.PDF は暗号化されたファイルを開くことができます。

```csharp
Document pdfDoc = new Document(inputPath, new LoadOptions { Password = "mySecret" });
```

### 角丸矩形を追加するには？

`Rectangle` の代わりに `RoundedRectangle` クラスを使用します。残りの手順は同じです。

## まとめ

Aspose.PDF を使用した C# での **PDF に形状を追加する方法** を解説しました。手順は次の通りです:

1. **C# で PDF ドキュメントを読み込む** – `Document` オブジェクトを作成。  
2. **矩形（または他の形状）を定義**。  
3. **境界を検証** してはみ出しを防止。  
4. **対象ページに矩形を追加**。  
5. **保存** してファイルを更新。

これが **aspose pdf add rectangle** の全工程で、円や線、カスタムポリゴンに応用できるテンプレートが手に入りました。

## 次にやること

- **他の描画プリミティブを探る**: `Ellipse`、`Line`、`Polygon`。  
- **形状の横にテキストアノテーションを追加** して、インタラクティブ性を高める。  
- **PDF フォームフィールドと組み合わせる** ことで、記入可能な契約書を作成。  
- **Aspose の PDF 変換機能をチェック** して、注釈付き PDF をプレビュー用サムネイル画像に変換。

自由に試してみてください—透かしを描いたり、表のセルをハイライトしたり、署名フィールドを枠で囲んだりできます。API は柔軟で、基本はすでに習得しました。

コーディングを楽しんで、PDF が常に意図した通りの見た目になることを願っています！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法を応用した密接に関連するトピックを扱っています。各リソースには完全な動作コード例とステップバイステップの解説が含まれ、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを探るのに役立ちます。

- [Aspose.PDF で PDF ドキュメントを作成 – ページ追加、形状追加、保存](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [Aspose.PDF for .NET を使用して PDF にページ番号を追加・カスタマイズする方法 | ドキュメント操作ガイド](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF for .NET を使用して PDF にハイパーリンクを追加する方法：包括的ガイド](/pdf/english/net/bookmarks-navigation/add-hyperlinks-pdf-aspose-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}