---
category: general
date: 2026-03-27
description: 空白のPDFページを作成し、画像からPDFを作成する方法、PDFに画像を追加する方法、PDF内の画像をトリミングする方法、PDF内の画像のサイズを変更する方法を、C#で
  Aspose.Pdf を使用して学びます。
draft: false
keywords:
- create blank pdf page
- create pdf from image
- add image to pdf
- crop image in pdf
- resize image in pdf
language: ja
og_description: Aspose.Pdf を使用して空白の PDF ページを作成し、画像を即座に追加、トリミング、リサイズします。開発者向けのステップバイステップ
  C# チュートリアル。
og_title: 空白のPDFページを作成 – C#で画像を追加、トリミング、リサイズ
tags:
- Aspose.Pdf
- C#
- PDF generation
title: 空白PDFページの作成 – 画像の追加、トリミング、リサイズの完全ガイド
url: /ja/net/programming-with-images/create-blank-pdf-page-full-guide-to-adding-cropping-resizing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 空白の PDF ページの作成 – 完全 C# チュートリアル

空白の PDF ページを **create blank PDF page** して、そこに画像を貼り付けたいと思ったことはありませんか？最初の手順が分からないと感じるのはあなただけではありません。実際のアプリケーション—例えば請求書、製品カタログ、または簡易レポートジェネレータ—では、PDF のキャンバスを新規に作成し、画像を配置し、必要に応じてトリミングし、最終的にサイズ調整する必要があります。

このガイドでは、Aspose.Pdf ライブラリを使用して、**create PDF from image**、**add image to PDF**、**crop image in PDF**、**resize image in PDF** の全工程を解説します。最後まで読むと、トリミングとリサイズが施されたプロフェッショナルな PDF を生成する、すぐに実行できるコードスニペットが手に入ります。

---

## 必要なもの

- **.NET 6+**（または .NET Framework 4.6+）。API はバージョン間で同じように動作しますが、最新のランタイムの方がパフォーマンスが向上します。
- **Aspose.Pdf for .NET** – NuGet（`Install-Package Aspose.Pdf`）から取得するか、公式サイトから無料トライアルをダウンロードできます。
- ディスク上の任意の場所に配置した画像ファイル（JPEG、PNG など）。ここでは `input.jpg` と呼びます。
- コードエディタ – Visual Studio、VS Code、または Rider など、使い慣れたものを使用してください。

> プロのコツ: CI/CD パイプラインを使用している場合は、Aspose.Pdf NuGet パッケージをプロジェクトファイルに追加しておくと、ビルドが依存関係を忘れることがありません。

---

## ステップ 1: 空白の PDF ページを作成

最初に行うのは、新しい PDF ドキュメントを作成し、そこに **blank PDF page** を追加することです。ドキュメントをノートブック、ページを最初の用紙と考えてください。

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Devices;

class Program
{
    static void Main()
    {
        // Step 1: Initialize a fresh PDF document (blank canvas)
        using var pdfDocument = new Document();

        // Step 2: Add a blank page – this is where the image will live
        Page pdfPage = pdfDocument.Pages.Add();

        // (More steps follow...)
```

なぜ最初にページを追加する必要があるのでしょうか？Aspose API は、後でグラフィックを配置する際にページオブジェクトが存在することを前提としています。この手順を省略すると、描画先がないため `NullReferenceException` がスローされます。

---

## ステップ 2: 画像から PDF を作成（オプションのクイックスタート）

画像だけを含む PDF（余分なテキストやページがない）を作成したいだけの場合、Aspose はショートカットを提供しています。メインの流れには必須ではありませんが、知っておくと便利です。

```csharp
// Quick way: convert an image directly to a one‑page PDF
// Comment out if you prefer the manual approach below
pdfDocument.Pages.Add(ImageStreamToPdfPage("YOUR_DIRECTORY/input.jpg"));
```
```csharp
static Page ImageStreamToPdfPage(string imagePath)
{
    var stream = File.OpenRead(imagePath);
    var page = new Page(pdfDocument);
    // The image fills the whole page by default
    page.AddImage(stream, new Rectangle(0, 0, pdfDocument.PageInfo.Width, pdfDocument.PageInfo.Height));
    return page;
}
```

このスニペットは **create pdf from image** ショートカットを示していますが、正確に **crop** と **resize** を行えるように、手動の方法で続けます。

---

## ステップ 3: ソース画像ストリームを読み込む

ここでは画像ファイルをストリームとして開きます。ストリームを使用すると、特に大きな画像の場合でもメモリ使用量を抑えることができます。

```csharp
        // Step 3: Open the source image file as a read‑only stream
        using var imageStream = File.OpenRead("YOUR_DIRECTORY/input.jpg");
```

ファイルが見つからない場合は `FileNotFoundException` がスローされますので、パスを再確認してください。本番コードでは try‑catch で囲み、分かりやすいメッセージをログに出すことを検討してください。

---

## ステップ 4: ソースおよびデスティネーション矩形を定義（Crop & Resize）

Aspose では 2 つの矩形を指定できます：

1. **Source rectangle** – 元画像のうち保持したい部分。
2. **Destination rectangle** – PDF ページ上でその部分が描画される領域で、最終的なサイズを決定します。

```csharp
        // Step 4: Set up the area of the image to keep (crop) and its size on the PDF page (resize)
        // Source rectangle – top‑left corner (0,0), width 600px, height 800px
        var sourceRectangle = new Rectangle(0, 0, 600, 800);

        // Destination rectangle – where the cropped piece lands on the page
        // Here we shrink it to half the original dimensions (300x400)
        var destinationRectangle = new Rectangle(0, 0, 300, 400);
```

全画像をそのまま使用しない理由は何ですか？実際のシナリオでは、白い余白をトリミングしたりロゴにフォーカスしたりする必要があることが多いためです。数値はご自身の画像サイズに合わせて調整してください。

---

## ステップ 5: 画像を PDF に追加し、Crop と Resize を適用

矩形が準備できたら `AddImage` を呼び出します。この一度の呼び出しで、ソース画像の指定部分を抽出し、指定サイズでページに描画するという重い処理を行います。

```csharp
        // Step 5: Place the cropped & resized image onto the blank page
        pdfPage.AddImage(imageStream, sourceRectangle, destinationRectangle);
```

内部では Aspose が XObject を作成し、トリミングとスケーリングを一括で行うため、別途画像処理ライブラリを使用する必要はありません。

---

## ステップ 6: 結果の PDF を保存

最後に、ドキュメントをディスクに保存します。ファイル `CroppedImage.pdf` には、作成した **blank PDF page** が含まれ、そこにきれいにトリミング・リサイズされた画像が配置されます。

```csharp
        // Step 6: Write the PDF to the output file
        pdfDocument.Save("YOUR_DIRECTORY/CroppedImage.pdf");
    }
}
```

`CroppedImage.pdf` を任意のビューアで開くと、画像が左上隅に配置された 1 ページが表示され、サイズは正確に 300 × 400 ポイント（72 dpi で約 4 × 5 インチ）です。

> **期待される出力:** 1 ページの PDF で、画像はソースから矩形 (0,0,600,800) にトリミングされ、ページ上では半分のサイズ（300 × 400）で表示されます。

---

## よくある質問とエッジケース

### ソース矩形より画像が小さい場合は？

Aspose は画像を自動的に伸張してソース矩形に合わせますが、これによりぼやけることがあります。これを防ぐには、実際の画像サイズに基づいてソース矩形を計算してください：

```csharp
using var img = Image.FromStream(imageStream);
var actualWidth = img.Width;
var actualHeight = img.Height;
var sourceRect = new Rectangle(0, 0, actualWidth, actualHeight);
```

### 画像をページ上の別の位置に配置するには？

`destinationRectangle` の X と Y の値を変更するだけです。例えば、画像を中央に配置するには：

```csharp
float pageWidth = pdfPage.PageInfo.Width;
float pageHeight = pdfPage.PageInfo.Height;
float destX = (pageWidth - destinationRectangle.Width) / 2;
float destY = (pageHeight - destinationRectangle.Height) / 2;
var centeredRect = new Rectangle(destX, destY, destinationRectangle.Width, destinationRectangle.Height);
pdfPage.AddImage(imageStream, sourceRectangle, centeredRect);
```

### 複数の画像を追加したい場合は？

異なる source/destination 矩形で **Step 5** を繰り返します。各呼び出しは同じページに新しい XObject を追加します。または、`pdfDocument.Pages.Add()` で追加ページを作成できます。

### 高解像度の出力が必要な場合は？

Aspose はポイント単位で動作します（1 pt = 1/72 インチ）。300 dpi が必要な場合は、目的のサイズに 4.2（300/72）を掛けてからデスティネーション矩形を設定してください。

---

## 本番向け PDF のプロティップス

- **Dispose properly:** サンプルの `using` 文によりファイルハンドルが確実に閉じられ、Windows でのファイルロックを防止します。
- **Compression:** 保存前に `pdfDocument.Compress();` を呼び出すと、ファイルサイズが縮小します。
- **Security:** PDF を保護したい場合は、`pdfDocument.Encrypt` にユーザーパスワードを設定します。
- **Performance:** バッチ処理では、単一の `Document` インスタンスを再利用し、ループでページを追加するとオーバーヘッドが削減されます。

---

## 完全動作サンプル（コピー＆ペースト可能）

```csharp
using System;
using System.Drawing;          // Needed for Image class (System.Drawing.Common NuGet)
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Devices;

class CreatePdfWithCroppedImage
{
    static void Main()
    {
        // Initialize a new PDF document (blank canvas)
        using var pdfDocument = new Document();

        // Add a blank page – the surface for our image
        Page pdfPage = pdfDocument.Pages.Add();

        // Load the image file
        using var imageStream = File.OpenRead("YOUR_DIRECTORY/input.jpg");

        // Optional: Adjust source rectangle to actual image size
        using var img = Image.FromStream(imageStream);
        var sourceRectangle = new Rectangle(0, 0, img.Width, img.Height);
        imageStream.Position = 0; // Reset stream after reading size

        // Destination rectangle – half the size, placed at (0,0)
        var destinationRectangle = new Rectangle(0, 0, img.Width / 2, img.Height / 2);

        // Place the cropped (full‑image here) and resized picture onto the page
        pdfPage.AddImage(imageStream, sourceRectangle, destinationRectangle);

        // Save the PDF
        pdfDocument.Save("YOUR_DIRECTORY/CroppedImage.pdf");

        Console.WriteLine("PDF created successfully!");
    }
}
```

> **注意:** `YOUR_DIRECTORY` を実際のフォルダパスに置き換えてください。上記コードは、画像の実際のサイズを読み取って動的に **create pdf from image** を行う方法も示しています。

---

## 結論

ここまでで、Aspose.Pdf for .NET を使用して **create blank PDF page**、**add image to PDF**、**crop image in PDF**、**resize image in PDF** を行うために必要なすべてをカバーしました。このスニペットは単体で完結し、すぐに動作し、外部の画像ライブラリや煩雑なグラフィックコンテキストを使用せずに PDF 操作ができる点で、Aspose が堅実な選択肢である理由を示しています。

次のステップとして、テキスト注釈の追加、テーブル生成、複数 PDF の結合などに挑戦できるでしょう。これらの作業もすべて同じパターンに従います：**blank PDF page** を作成し、ステップごとにコンテンツを重ねていきます。

何か別のやり方に興味がありますか？コメントで教えてください。会話を続けましょう。コーディングを楽しんで！

![Create blank PDF page with cropped image using C#](https://example.com/placeholder-image.png "Create blank PDF page with cropped image using C#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}