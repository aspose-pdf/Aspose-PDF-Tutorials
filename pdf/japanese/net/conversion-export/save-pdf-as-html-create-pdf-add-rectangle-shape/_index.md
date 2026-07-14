---
category: general
date: 2026-07-14
description: Aspose.Pdf を使用して PDF を HTML に保存 – PDF ドキュメントの作成方法、矩形シェイプの追加方法、画像なしのクリーンな
  HTML へのエクスポート方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save pdf as html
- how to create pdf document
- add rectangle shape pdf
language: ja
lastmod: 2026-07-14
og_description: Aspose.PdfでPDFをHTMLに保存。PDFドキュメントの作成方法、矩形形状の描画、画像なしで数分でHTMLを生成する方法をご紹介します。
og_image_alt: Screenshot of a PDF saved as HTML showing a rectangle shape
og_title: PDFをHTMLとして保存 – PDFの作成と長方形シェイプの追加クイックガイド
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Save PDF as HTML using Aspose.Pdf – learn how to create PDF document,
    add rectangle shape PDF, and export to clean HTML without images.
  headline: Save PDF as HTML – Create PDF, add rectangle shape
  type: TechArticle
tags:
- pdf
- aspnet
- csharp
- html-export
title: PDFをHTMLとして保存 – PDFを作成し、長方形シェイプを追加
url: /ja/net/conversion-export/save-pdf-as-html-create-pdf-add-rectangle-shape/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF を HTML として保存 – PDF を作成し、矩形シェイプを追加

PDF を **HTML として保存** しながら、元の PDF にグラフィックを描画できる方法を考えたことはありませんか？ あなただけではありません。多くの社内ツールでは、カスタムシェイプを含む PDF のクリーンな HTML プレビューが必要ですが、従来のコンバータは重いラスタ画像を埋め込むか、ベクターデータを完全に除去してしまいます。

このチュートリアルでは、**Aspose.Pdf** を使ってプログラムで **PDF ドキュメントを作成**し、**矩形シェイプ PDF** を描画し、ベーツ番号付けを設定し、最後に **画像を除外した HTML として PDF を保存** する方法を順を追って説明します。最後まで実行すれば、任意のブラウザで開ける HTML ファイルを生成する C# コンソールアプリが完成します—追加の画像ファイルは不要です。

> **プロのコツ:** Aspose.Pdf は .NET 6+、.NET Framework 4.6+、さらには .NET Core でも動作するので、レガシーな Windows サービスにも、最新のマイクロサービスにも同様に組み込めます。

---

## 前提条件

- **Visual Studio 2022**（Community 以上）または任意の C# 対応 IDE。  
- **Aspose.Pdf for .NET** NuGet パッケージ（バージョン 23.11 以降）。Package Manager Console でインストールします:

```powershell
Install-Package Aspose.Pdf
```

- C# の基本構文に慣れていること；PDF の経験は不要です。

---

## Aspose.Pdf で PDF を HTML として保存

以下はそのままコピー＆ペーストできる完全版コードです。元のスニペットと同じ手順に従いながら、コメント、エラーハンドリング、メインフローを読みやすくするための小さなヘルパーメソッドを追加しています。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

namespace PdfToHtmlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a fresh PDF document.
            Document pdfDoc = new Document();
            Page pdfPage = pdfDoc.Pages.Add();

            // 2️⃣ Draw a rectangle shape on the page.
            //    This demonstrates the "add rectangle shape pdf" requirement.
            var rectangle = new Rectangle(100, 500, 300, 700)
            {
                // Optional visual tweaks
                FillColor = Color.GetYellow(),
                Border = new Border
                {
                    Width = 2,
                    Color = Color.GetRed()
                }
            };
            pdfPage.Paragraphs.Add(rectangle);
            pdfPage.ValidateGraphicsState(); // Ensures the shape fits within page bounds

            // 3️⃣ Configure Bates numbering – useful for legal documents.
            var bates = new BatesNumbering { StartNumber = 1, Prefix = "DOC-" };
            pdfDoc.BatesNumbering = bates;

            // 4️⃣ Add a tagged element with an explicit position.
            //    Tagging is important for accessibility (PDF/UA).
            var taggedElement = new TagStructure();
            taggedElement.PositionSettings = new TagPositionSettings { X = 150, Y = 600 };
            pdfPage.TagStructure.Add(taggedElement);

            // 5️⃣ Enable detection of compromised signatures.
            pdfDoc.SecurityOptions.DetectCompromisedSignatures = true;
            bool hasCompromisedSignature = pdfDoc.SecurityOptions.HasCompromisedSignature;
            Console.WriteLine($"Compromised signature? {hasCompromisedSignature}");

            // 6️⃣ Finally, save the PDF as HTML *without* embedding raster images.
            var htmlOptions = new HtmlSaveOptions
            {
                SkipImages = true,               // Removes <img> tags for raster data
                FixedLayout = true,              // Preserves the original page layout
                ExportEmbeddedFonts = false      // Keeps the HTML lightweight
            };

            string outputPath = @"output.html";
            pdfDoc.Save(outputPath, htmlOptions);
            Console.WriteLine($"✅ PDF successfully saved as HTML at: {outputPath}");
        }
    }
}
```

### コードの内容をステップごとに解説

| ステップ | 重要な理由 |
|------|----------------|
| **PDF ドキュメントを作成** | 基礎です—`Document` オブジェクトがなければ何も追加できません。 |
| **矩形シェイプ PDF を追加** | ベクタ描画の例です；矩形は最もシンプルな形状ですが、同じ API で円や多角形も描画できます。 |
| **ベーツ番号付けを設定** | 訴訟やバッチ処理シナリオでページを一意に識別するために頻繁に必要です。 |
| **タグ構造を設定** | アクセシビリティが向上します；スクリーンリーダーはタグを使って読み順を把握します。 |
| **改ざんされた署名を検出** | セキュリティ対応アプリはデジタル署名が改ざんされたかどうかを知る必要があります。 |
| **PDF を HTML として保存** | 最終目標—画像ファイルが肥大化しない、PDF のレイアウトを反映したクリーンな HTML を生成します。 |

> **`SkipImages = true` の理由は？**  
> ベクタグラフィック（今回の矩形など）を含む PDF を変換する場合、ラスタの代替は通常不要です。`SkipImages` を設定すると、`<img>` 要素が除去され、ベース64 のブロブ参照がなくなるため、HTML ファイルは数キロバイトに抑えられます。

---

## Aspose.Pdf で PDF ドキュメントを作成する方法

Aspose に不慣れな方は、ライブラリは PDF を Word 文書のように扱います：**ページ** を追加し、そこに **段落**、**シェイプ**、**注釈** を配置します。`Document` クラスがエントリーポイントで、各 `Page` は `Paragraphs` コレクションを持ちます。`TextFragmentAbsorber`、`Image`、`Rectangle` などを継承したオブジェクトはすべてこのコレクションに挿入可能です。

以下は空白の PDF だけを作成する最小限のスニペットです—ゼロから始めたいときに便利です:

```csharp
Document emptyPdf = new Document();
Page firstPage = emptyPdf.Pages.Add();   // Adds a default‑size A4 page
emptyPdf.Save("empty.pdf");
```

追加のページはシンプルな `for` ループでチェーンできますし、`PageInfo` を使ってページレベルの設定（余白、サイズ）を適用できます。この柔軟性が Aspose.Pdf をサーバーサイド PDF 生成の定番にしています。

---

## 矩形シェイプ PDF を追加 – グラフィック描画

`Rectangle` クラスは `Aspose.Pdf.Annotations` にあり、4 つの座標 **左下 X**、**左下 Y**、**右上 X**、**右上 Y** を受け取ります。PDF の座標系は次のように考えてください

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを基にした、密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、API の追加機能を習得したり、独自プロジェクトで代替実装を検討したりするのに役立ちます。

- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [Convert PDF to HTML in .NET Using Aspose.PDF Without Saving Images](/pdf/english/net/conversion-export/convert-pdf-html-net-asposepdf-no-images/)
- [PDF to HTML Conversion Using Aspose.PDF .NET&#58; Save Images as External PNGs](/pdf/english/net/conversion-export/pdf-to-html-conversion-external-png-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}