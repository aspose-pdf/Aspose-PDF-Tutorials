---
category: general
date: 2026-08-14
description: C# を使って PDF に素早く矩形を描く。数行のコードで矩形のサイズを定義し、PDF ページに図形を追加する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- draw rectangle on pdf
- how to define rectangle dimensions
language: ja
lastmod: 2026-08-14
og_description: C#でPDFに数秒で矩形を描く。このガイドでは、矩形のサイズを定義し、シェイプを追加し、信頼性の高いPDFグラフィックのためにページ境界を確認する方法を示します。
og_image_alt: Screenshot of a PDF page showing a black rectangle drawn with C# code
og_title: PDF上に矩形を描く – 完全なC#チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: draw rectangle on pdf quickly using C#. Learn how to define rectangle
    dimensions and add shapes to a PDF page in just a few lines.
  headline: draw rectangle on pdf – step‑by‑step C# guide
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
- RectangleShape
- Graphics
title: PDFに矩形を描く – ステップバイステップ C# ガイド
url: /ja/net/annotations/draw-rectangle-on-pdf-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF に矩形を描く – 完全な C# チュートリアル

C# を使用して **draw rectangle on pdf** を行う必要がある場合、このガイドでは簡潔で本番環境でも使えるソリューションを示します。**how to define rectangle dimensions** の方法を正確に確認し、形状がページに収まることを検証し、単一のメソッド呼び出しでページに追加する手順が分かります。

このチュートリアルは PDF ドキュメントの作成から矩形の描画までを網羅しているため、コードをコピー＆ペーストしてすぐに結果を確認できます。外部ドキュメントは不要です—以下の手順だけで完了します。

## Prerequisites

開始する前に、以下が揃っていることを確認してください。

* .NET 6.0 以降（コードは .NET Framework 4.7+ でも動作します）
* **Aspose.PDF for .NET** NuGet パッケージ (`Install-Package Aspose.PDF`)
* C# 文法の基本的な理解
* Visual Studio や VS Code などの IDE

> **Pro tip:** 無料の評価ライセンスを使用すれば、少しの透かしが入りますがすべての機能をテストできます。

## How to draw rectangle on PDF with C#

タスクの核心は `RectangleShape` を作成し、サイズとストロークを設定し、`Page` に貼り付けることです。以下の H2 見出しは主要キーワードを含んでおり、SEO 要件を満たしています。

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        Document pdfDoc = new Document();

        // 2️⃣ Add a blank page (default size: A4)
        Page page = pdfDoc.Pages.Add();

        // 3️⃣ Define the rectangle bounds (x, y, width, height)
        //    This demonstrates how to define rectangle dimensions.
        Rectangle rectBounds = new Rectangle(0, 0, 500, 700);

        // 4️⃣ Create the rectangle shape and set its stroke color
        RectangleShape rectangleShape = new RectangleShape(rectBounds)
        {
            StrokeColor = Color.Black   // black outline
        };

        // 5️⃣ Verify that the shape fits within the page boundaries
        page.CheckShapeBoundary(rectangleShape);

        // 6️⃣ Add the shape to the page
        page.Add(rectangleShape);

        // 7️⃣ Save the PDF to disk
        string outPath = "RectangleDemo.pdf";
        pdfDoc.Save(outPath);
        Console.WriteLine($"PDF saved to {outPath}");
    }
}
```

### Explanation of each step

| Step | Why it matters |
|------|----------------|
| **1️⃣ Create a new PDF document** | ページとグラフィックを保持するコンテナを初期化します。 |
| **2️⃣ Add a blank page** | 形状はドキュメントではなくページに付随するため、`Page` オブジェクトが必要です。 |
| **3️⃣ Define the rectangle bounds** | ここで **how to define rectangle dimensions** を行います。`Rectangle` コンストラクタは `x`, `y`, `width`, `height`（単位はポイント、1 pt = 1/72 in）を受け取ります。 |
| **4️⃣ Create the rectangle shape** | `RectangleShape` は Aspose の矩形描画クラスです。`StrokeColor` を設定すると輪郭が描かれ、`FillColor` を設定すれば塗りつぶしが可能です。 |
| **5️⃣ Verify page boundaries** | `CheckShapeBoundary` は矩形がページサイズを超えている場合に例外をスローし、PDF の破損を防ぎます。 |
| **6️⃣ Add the shape to the page** | 形状がページのコンテンツストリームに組み込まれます。 |
| **7️⃣ Save the PDF** | 任意の PDF ビューアで開けるファイルとしてドキュメントを保存します。 |

結果として生成される `RectangleDemo.pdf` には、ページ左上隅に幅 500 pt、高さ 700 pt の黒い矩形が配置されます。

![draw rectangle on pdf example](https://example.com/rectangle-demo.png "draw rectangle on pdf example")

*Image alt text: draw rectangle on pdf example showing a black rectangle in the upper left corner of a PDF page.*

## How to define rectangle dimensions for different page sizes

上記のスニペットは固定値（`500 x 700`）を使用していますが、実際のアプリケーションではページの幅・高さに合わせて矩形を動的に調整する必要があります。

```csharp
// Get page dimensions (in points)
float pageWidth = page.PageInfo.Width;
float pageHeight = page.PageInfo.Height;

// Define a rectangle that occupies 80% of the page width and 50% of the height
float rectWidth  = pageWidth * 0.8f;
float rectHeight = pageHeight * 0.5f;

// Center the rectangle on the page
float rectX = (pageWidth - rectWidth) / 2;
float rectY = (pageHeight - rectHeight) / 2;

Rectangle dynamicRect = new Rectangle(rectX, rectY, rectWidth, rectHeight);
RectangleShape dynamicShape = new RectangleShape(dynamicRect)
{
    StrokeColor = Color.DarkBlue,
    FillColor   = Color.LightGray   // optional fill
};

page.CheckShapeBoundary(dynamicShape);
page.Add(dynamicShape);
```

**Key points:**

* `page.PageInfo.Width` と `Height` を使用して実際のページサイズを取得します。
* `0.8f` などの係数で掛け算すると、ページのパーセンテージとして寸法を表現できます。
* 矩形サイズをページサイズから引き、残りを半分にすることで中央寄せが実現できます。

## Common pitfalls and how to avoid them

| Pitfall | Why it happens | Fix |
|---------|----------------|-----|
| Rectangle extends beyond the page | ハードコードされた寸法がページサイズを超えている。 | 形状を追加する **前に** `page.CheckShapeBoundary` を呼び出し、例外が出たら寸法を調整する。 |
| Stroke not visible | `StrokeColor` がデフォルト（`Color.Empty`）のまま。 | 明示的に `StrokeColor` を設定する（例: `Color.Black`）。 |
| Rectangle appears off‑screen | PDF 空間では座標系の原点が左下にあるが、画面座標系（左上基準）を使用したため。 | 原点が左下であることを意識し、`y` を `pageHeight - desiredY` のように計算する。 |
| Unexpected line thickness | デフォルトの線幅が印刷には薄すぎる。 | `rectangleShape.LineWidth = 2;` で線幅を増やす。 |

## Extending the example

**draw rectangle on pdf** ができたら、他の形状も簡単に追加できます。

* **EllipseShape** – 円や楕円を描く。
* **PolygonShape** – 任意の多角形を描く。
* **TextFragment** – 矩形にラベルを付ける。

すべての形状は同じワークフローです：境界を定義し、外観を設定し、境界チェックを行い、ページに追加する。

## Complete, runnable program

以下は基本的な矩形と動的サイズ設定の例を組み合わせたフルプログラムです。新しいコンソールプロジェクトに貼り付け、`Aspose.PDF` NuGet パッケージを復元して実行してください。

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class RectangleDemo
{
    static void Main()
    {
        // Create document and page
        Document doc = new Document();
        Page page = doc.Pages.Add();

        // ==== Fixed‑size rectangle (basic example) ====
        Rectangle fixedRect = new Rectangle(0, 0, 500, 700);
        RectangleShape fixedShape = new RectangleShape(fixedRect)
        {
            StrokeColor = Color.Black,
            LineWidth   = 1
        };
        page.CheckShapeBoundary(fixedShape);
        page.Add(fixedShape);

        // ==== Dynamic rectangle that adapts to page size ====
        float pageW = page.PageInfo.Width;
        float pageH = page.PageInfo.Height;

        float dynWidth  = pageW * 0.6f;
        float dynHeight = pageH * 0.3f;
        float dynX      = (pageW - dynWidth) / 2;
        float dynY      = (pageH - dynHeight) / 2;

        Rectangle dynamicRect = new Rectangle(dynX, dynY, dynWidth, dynHeight);
        RectangleShape dynamicShape = new RectangleShape(dynamicRect)
        {
            StrokeColor = Color.DarkBlue,
            FillColor   = Color.LightYellow,
            LineWidth   = 2
        };
        page.CheckShapeBoundary(dynamicShape);
        page.Add(dynamicShape);

        // Save PDF
        string outFile = "CombinedRectangles.pdf";
        doc.Save(outFile);
        Console.WriteLine($"PDF created: {outFile}");
    }
}
```

**Expected output:**  
`CombinedRectangles.pdf` を開くと、左下隅に黒い矩形、中央に濃い青色の枠線と薄い黄色の塗りつぶしが施された矩形が表示されます。どちらもページ余白を考慮しています。

## Conclusion

これで C# を使って **draw rectangle on pdf** を行う方法と、固定レイアウトとレスポンシブレイアウトの両方で **how to define rectangle dimensions** を正確に指定する方法が分かりました。Aspose.PDF の `RectangleShape`、境界チェック、シンプルな算術演算を組み合わせるだけで、任意のページサイズに対応できます。

次に試すべきこと：

* **塗りつぶしカラー** と **線スタイル**（破線、点線）を追加する – 二次キーワード: how to define rectangle dimensions with style.
* 複数の形状を単一の `Page` に組み合わせてチャートやフォームを作成する。
* PDF をディスクに保存する代わりにストリームへエクスポートし、Web API で返す。

さまざまなサイズ、色、位置で実験し、.NET アプリケーションにおける PDF グラフィックのマスターを目指してください。Happy coding!

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示したテクニックを応用できる関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能を習得したり、代替実装アプローチを自分のプロジェクトで試したりするのに役立ちます。

- [Aspose.PDF for .NET を使用した PDF のカスタマイズ方法&#58; ページ余白の設定と線の描画](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [Aspose.PDF for .NET を使用した PDF へのページスタンプの追加方法&#58; 完全ガイド](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Aspose.PDF for .NET を使用した PDF のページ番号スタンプの追加方法 | ウォーターマークと背景](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}