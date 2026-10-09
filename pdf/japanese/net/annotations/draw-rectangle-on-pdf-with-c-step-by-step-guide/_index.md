---
category: general
date: 2026-06-21
description: C#でPDFに矩形を描く。PDFドキュメントの読み込み方法、黒い矩形アノテーションの作成方法、そして変更したPDFを効率的に保存する方法を学びます。
draft: false
keywords:
- draw rectangle on pdf
- load pdf document
- add black rectangle
- create black rectangle
- save modified pdf
language: ja
og_description: PDFドキュメントを読み込み、黒い矩形アノテーションを作成し、変更後のPDFを保存して、C#でPDFに矩形を描画します。完全なコードが含まれています。
og_title: C#でPDFに矩形を描く – 完全プログラミングチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
    black rectangle annotation, and save modified PDF efficiently.
  headline: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
  type: TechArticle
- description: Draw rectangle on PDF using C#. Learn how to load PDF document, create
    black rectangle annotation, and save modified PDF efficiently.
  name: Draw Rectangle on PDF with C# – Step‑by‑Step Guide
  steps:
  - name: .NET 6.0 SDK (or any recent .NET version) installed
    text: .NET 6.0 SDK (or any recent .NET version) installed
  - name: 'A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package
      Aspose.PDF`)'
    text: 'A reference to **Aspose.PDF for .NET** (available via NuGet: `Install-Package
      Aspose.PDF`)'
  - name: An existing PDF file (`input.pdf`) placed in a folder you can read/write
    text: An existing PDF file (`input.pdf`) placed in a folder you can read/write
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
title: C#でPDFに矩形を描く – ステップバイステップガイド
url: /ja/net/annotations/draw-rectangle-on-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で PDF に矩形を描く – 完全プログラミングチュートリアル

.NET アプリから **PDF に矩形を描く** 必要があって、どこから始めればいいか分からないことはありませんか？ あなただけではありません。セクションをハイライトしたり、機密情報を隠したり、単に視覚的な目印を付けたりする場合でも、プログラムで *PDF に矩形を描く* 方法を学べば、手作業の編集にかかる時間を大幅に削減できます。

このガイドでは、**PDF ドキュメントを読み込み**、**黒い矩形を作成**し、**変更後の PDF を保存**する実用的な例を順を追って解説します。最後まで読めば、任意の C# プロジェクトに貼り付けられる再利用可能なスニペットが手に入り、謎はなく、コードと説明が明快になります。

## 本チュートリアルでカバーする内容

- Aspose.PDF for .NET ライブラリを使用した **PDF ドキュメントの読み込み** 方法  
- 矩形の座標を定義し、ページ境界内に収める方法  
- **黒い矩形を追加** するメソッドを使ってページに注釈を付ける手順  
- **変更後の PDF を保存** して新しいファイルに出力する方法  
- エッジケースの取り扱い（複数ページ、ページ外矩形、カスタムカラー）  

外部ツールや曖昧な参照は一切不要です。コピー＆ペーストできる完全な実行例だけをご提供します。

---

## 前提条件

作業を始める前に、以下を用意してください。

1. .NET 6.0 SDK（またはそれ以降の .NET バージョン）  
2. **Aspose.PDF for .NET** への参照（NuGet で入手可能: `Install-Package Aspose.PDF`）  
3. 読み書き可能なフォルダーに配置した既存の PDF ファイル（`input.pdf`）  

以上です。C# の基本構文に慣れていればすぐに始められます。

---

## 手順 1: PDF ドキュメントを読み込む

最初に必要なのは **PDF ドキュメントの読み込み** 呼び出しです。Aspose.PDF の `Document` クラスはファイルパスを受け取り、ファイル全体をメモリに読み込みます。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing;

// Load the source PDF
Document pdfDocument = new Document(@"C:\MyFiles\input.pdf");
```

*なぜ必要か*: PDF を読み込むことで、ページ、メタデータ、描画サーフェスにアクセスできるようになります。このステップがなければ、形状を配置することはできません。

---

## 手順 2: 対象ページを選択する

Aspose では PDF ページは 1 ベースです。したがって最初のページはインデックス 1 です。デモ用に最初のページを取得します。

```csharp
// Get the first page (pages are 1‑based)
Page targetPage = pdfDocument.Pages[1];
```

別のページで作業したい場合はインデックスを変更してください。インデックスが存在するか検証し、`ArgumentOutOfRangeException` を防ぎましょう。

---

## 手順 3: 矩形のジオメトリを定義する

矩形は左下 (X,Y) と右上 (X,Y) の座標で定義されます。`Rectangle` 構造体はこれらを `LLX`, `LLY`, `URX`, `URY` として保持します。

```csharp
// Define the rectangle (lower‑left X,Y and upper‑right X,Y)
Rectangle boundingRect = new Rectangle(100, 100, 300, 300);
```

数値は自由に調整できます。`100,100` は左端と下端から 100 ポイント離れた左下角を、`300,300` は右端と上端から 300 ポイント離れた右上角を意味します。

---

## 手順 4: 矩形がページ内に収まっているか確認する

ページ境界外に描画しようとすると、ライブラリのバージョンによっては無視されるか例外が発生します。簡単なチェックでコードの堅牢性を保ちましょう。

```csharp
// Ensure the rectangle fits within the page dimensions
if (targetPage.PageInfo.Width >= boundingRect.URX &&
    targetPage.PageInfo.Height >= boundingRect.URY)
{
    // Rectangle is safe to add
}
else
{
    throw new InvalidOperationException("Rectangle exceeds page dimensions.");
}
```

*プロのコツ*: ページサイズが様々な場合は、絶対座標ではなくページ幅・高さのパーセンテージで矩形を計算すると便利です。

---

## 手順 5: 黒い矩形の注釈を追加する

いよいよ **黒い矩形を追加** します。Aspose の `AddRectangle` はジオメトリと `Color` を受け取ります。ここでは `Color.Black` を使って **黒い矩形を作成** します。

```csharp
// Add a black rectangle annotation to the page
targetPage.AddRectangle(boundingRect, Color.Black);
```

この一行で、注釈オブジェクトの作成、枠線色の設定、ページの注釈コレクションへの挿入という重い処理が完了します。

別の塗りや枠線スタイルが必要な場合は、`Annotation` オブジェクトを受け取るオーバーロードを利用して、線幅、破線パターン、透明度などを調整できます。

---

## 手順 6: 変更後の PDF を保存する

最後に **変更後の PDF を保存** します。元ファイルを上書きすることも、新しいファイルに書き出すことも可能です。ここでは出力ファイルを作成します。

```csharp
// Save the updated PDF to a new location
pdfDocument.Save(@"C:\MyFiles\output.pdf");
```

これで一連の流れは完了です。プログラムを実行し、`output.pdf` を開くと、指定した位置に黒い矩形が描かれているはずです。

---

## 完全動作サンプル

以下は、すべての手順をまとめた自己完結型コンソールアプリケーションです。新しい `.csproj` に貼り付けて **Run** してください。

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load PDF document
            Document pdfDocument = new Document(@"C:\MyFiles\input.pdf");

            // 2️⃣ Get the first page (pages are 1‑based)
            Page firstPage = pdfDocument.Pages[1];

            // 3️⃣ Define the rectangle geometry
            Rectangle rect = new Rectangle(100, 100, 300, 300);

            // 4️⃣ Verify bounds
            if (firstPage.PageInfo.Width < rect.URX || firstPage.PageInfo.Height < rect.URY)
            {
                Console.WriteLine("Rectangle does not fit on the page.");
                return;
            }

            // 5️⃣ Add a black rectangle annotation
            firstPage.AddRectangle(rect, Color.Black);

            // 6️⃣ Save modified PDF
            pdfDocument.Save(@"C:\MyFiles\output.pdf");

            Console.WriteLine("Successfully drew rectangle on PDF and saved the file.");
        }
    }
}
```

**コンソール出力例**:

```
Successfully drew rectangle on PDF and saved the file.
```

`output.pdf` を開くと、指定した座標に黒い矩形が表示されます。

---

## よくあるバリエーションへの対応

| 状況 | 変更点 | 理由 |
|-----------|----------------|-----|
| **複数ページ** | `pdfDocument.Pages` をループし、各 `Page` オブジェクトに同じロジックを適用 | ドキュメント全体にバッチで注釈を付けられる |
| **異なる色** | `Color.Black` を `Color.Red` などの `System.Drawing.Color` に置き換える | ハイライト目的など、赤色などで目立たせたいときに有用 |
| **透明な塗り** | `new Annotation(rect) { Color = Color.Black, Opacity = 0.5 }` を使用 | 半透明オーバーレイを作成でき、完全な塗りつぶしより柔軟 |
| **動的矩形サイズ** | `URX` と `URY` を `PageInfo.Width * 0.5` などで計算 | ページサイズが異なる場合でも矩形が自動調整される |
| **エラーハンドリング** | 全体を `try…catch` で囲み、`Aspose.Pdf.IOException` をログに記録 | ソースファイルが存在しない、ロックされているなどのクラッシュを防止 |

これらの調整により、**黒い矩形の注釈** をさまざまなシナリオで再利用でき、コアロジックを書き直す必要がなくなります。

---

## プロのコツと落とし穴

- **Document の破棄**: Aspose.PDF は `IDisposable` を実装していますが、短命なコンソールアプリでは `using` パターンは必須ではありません。長時間稼働するサービスでは `using` ブロックで `Document` を囲み、ネイティブリソースを速やかに解放しましょう。  
- **座標系**: PDF の座標は左下が原点です。WinForms など左上原点に慣れている場合は Y 軸を反転させる必要があります（例: `pageHeight - y`）。  
- **パフォーマンス**: 非常に大きな PDF に注釈を付けるとメモリ使用量が増大します。ページを分割して処理したり、軽量編集向けの `PdfFileEditor` を検討してください。  
- **法的留意点**: ソース PDF の改変権限があるか確認しましょう。一部の文書は編集が制限されています。

---

## 結論

本稿では、C# を使って **PDF に矩形を描く** 方法を、**PDF ドキュメントの読み込み**、ジオメトリ定義、**黒い矩形の追加**、そして **変更後の PDF の保存** の順に実演しました。完全かつ実行可能なサンプルコードを提供したので、バッチ処理やカスタムスタイリングといった実務シナリオにもすぐに適用できます。

次のステップとして、テキストやハイライトなど他の注釈タイプを追加したり、注釈後に複数の PDF を結合したりすると良いでしょう。**PDF ドキュメントの読み込み** と **変更後の PDF の保存** は変わらないので、このパターンを自信を持って拡張できます。

試した工夫や質問があればコメントで共有してください。ハッピーコーディング！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した、密接に関連するテーマを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、API の追加機能習得や代替実装アプローチの探求に役立ちます。

- [Create Filled Rectangle Object in PDF using Java](/pdf/english/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)
- [Create Filled Rectangle Object In Pdf Using Java](/pdf/german/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)
- [Create Filled Rectangle Object In Pdf Using Java](/pdf/french/java/pdf-images/create-filled-rectangle-object-in-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}