---
category: general
date: 2026-06-05
description: C#でAspose.Pdfを使用してPDFに矩形を追加します。既存のPDFを読み込み、PDFページを編集し、数分でPDFに図形を挿入する方法を学びましょう。
draft: false
keywords:
- add rectangle to pdf
- draw rectangle on pdf
- load existing pdf
- edit pdf page
- insert shape into pdf
language: ja
og_description: PDFに矩形をすばやく追加します。このチュートリアルでは、既存のPDFを読み込み、PDFページを編集し、Aspose.Pdfを使用してPDFに矩形を描画する方法を示します。
og_title: C#でPDFに矩形を追加する – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Add rectangle to PDF using Aspose.Pdf in C#. Learn how to load existing
    PDF, edit PDF page, and insert shape into PDF in minutes.
  headline: Add Rectangle to PDF with C# – Complete Programming Guide
  type: TechArticle
- description: Add rectangle to PDF using Aspose.Pdf in C#. Learn how to load existing
    PDF, edit PDF page, and insert shape into PDF in minutes.
  name: Add Rectangle to PDF with C# – Complete Programming Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.6+). - Aspose.Pdf
      for .NET NuGet package (`Install-Package Aspose.Pdf`). - Basic familiarity with
      C# syntax (no deep PDF knowledge required).'
  - name: Why loading matters
    text: Before you can draw anything, the PDF must be in memory. The `Document`
      constructor reads the file, parses its internal structure, and gives you an
      object model to work with. If the file is locked or corrupted, Aspose will throw
      a descriptive exception—so you know exactly what went wrong.
  - name: Code
    text: '```csharp Document doc = new Document("YOUR_DIRECTORY/input.pdf"); ```'
  - name: Why page selection is crucial
    text: PDFs are page‑oriented; each page has its own coordinate system. Aspose
      uses a **1‑based** index, which trips up developers coming from 0‑based collections.
      Selecting the wrong page either throws an `ArgumentOutOfRangeException` or modifies
      an unintended page.
  - name: Code
    text: '```csharp Page page = doc.Pages[1]; // First page ```'
  - name: Understanding the rectangle coordinates
    text: A rectangle in Aspose.Pdf is defined by its lower‑left (`xLL`, `yLL`) and
      upper‑right (`xUR`, `yUR`) corners. The coordinate system starts at the **bottom‑left**
      of the page, with X increasing to the right and Y increasing upward. This is
      opposite of many UI frameworks, so keep an eye on the axes.
  - name: Code to add the shape
    text: '```csharp Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500,
      700); page.AddRectangle(rect); ```'
  - name: Why saving is the final step
    text: All manipulations stay in memory until you persist them. `Document.Save`
      writes the new content to disk (or stream). Overwriting the original file is
      possible, but keeping a backup (`output.pdf`) is safer.
  - name: Code
    text: '```csharp doc.Save("YOUR_DIRECTORY/output.pdf"); ```'
  type: HowTo
- questions:
  - answer: Yes—loop through `doc.Pages` and repeat the `AddRectangle` call for each
      `Page` object.
    question: Can I add the rectangle to every page automatically?
  - answer: Aspose provides `AddCircle`, `AddPolygon`, and `AddPolyline` methods.
      The same rectangle logic applies for bounding boxes.
    question: What if I need to draw a circle or a polygon?
  - answer: 'Compute the center coordinates:'
    question: Is there a way to position the rectangle relative to the page center?
  - answer: Aspose loads pages lazily, but if you’re processing thousands of pages,
      consider using `PdfExtractor` to work on subsets or stream the file to reduce
      memory footprint.
    question: Performance concerns for large PDFs?
  type: FAQPage
tags:
- pdf
- csharp
- aspose
- shape-manipulation
title: C#でPDFに矩形を追加する – 完全プログラミングガイド
url: /ja/net/document-manipulation/add-rectangle-to-pdf-with-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で PDF に矩形を追加する – 完全プログラミングガイド

Ever needed to **PDF に矩形を追加** but weren’t sure which API call to use? You’re not alone—many developers hit that wall when they first try to edit a PDF programmatically. The good news? With a few lines of C# and the powerful Aspose.Pdf library, you can draw a rectangle on any page of an existing document in a flash.

In this guide we’ll walk through loading an existing PDF, selecting the right page, defining a rectangle that fits, and finally inserting the shape into the PDF. By the end you’ll have a reusable snippet that you can drop into any .NET project. Oh, and we’ll also touch on **PDF 上に矩形を描画** nuances you might not have considered.

## 得られるもの

- すぐに使える、明確なステップバイステップのソリューション。
- **load existing pdf** ファイルを安全に扱う方法の理解。
- **edit pdf page** でドキュメントを破損しないためのヒント。
- 矩形だけでなく **insert shape into pdf** の戦略。
- すぐにコピー＆ペーストできる実行可能な C# コード。

### 前提条件

- .NET 6.0 以降（コードは .NET Framework 4.6+ でも動作します）。
- Aspose.Pdf for .NET NuGet パッケージ（`Install-Package Aspose.Pdf`）。
- C# 構文の基本的な知識（PDF の深い知識は不要）。

これらが揃っているなら、さっそく始めましょう。

![PDF に矩形を追加した例](add-rectangle-to-pdf.png "PDF ページに矩形が追加されたスクリーンショット – add rectangle to pdf")

## PDF に矩形を追加する – ステップバイステップ概要

以下は、説明する正確な順序に従った完全な実行可能サンプルです。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the existing PDF file
        Document doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Select the first page (pages are 1‑based)
        Page page = doc.Pages[1];

        // 3️⃣ Define a rectangle that fits inside the page bounds
        //    (xLL, yLL, xUR, yUR) – lower‑left & upper‑right corners
        Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500, 700);

        // 4️⃣ Add the rectangle to the page – this draws the shape
        page.AddRectangle(rect);

        // 5️⃣ Save the modified PDF to a new file
        doc.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

それでは各行を分解して、**なぜ**それを行うのか、**何を**行うのかだけでなく理解しましょう。

## 既存の PDF ドキュメントを読み込む

### なぜ読み込みが重要か

何かを描画する前に、PDF はメモリ上に存在する必要があります。`Document` コンストラクタはファイルを読み込み、内部構造を解析し、操作できるオブジェクトモデルを提供します。ファイルがロックされているか破損している場合、Aspose は詳細な例外をスローし、何が問題か正確に把握できます。

### コード

```csharp
Document doc = new Document("YOUR_DIRECTORY/input.pdf");
```

- `YOUR_DIRECTORY` をソースファイルへの絶対パスまたは相対パスに置き換えます。
- Aspose のリモートロードを有効にすれば、パスは URL にすることも可能です（高度なシナリオ）。
- **Tip:** これを `try/catch` ブロックでラップし、`FileNotFoundException` または `PdfException` を適切に処理します。

```csharp
try
{
    Document doc = new Document("input.pdf");
}
catch (Exception ex)
{
    Console.WriteLine($"Failed to load PDF: {ex.Message}");
    return;
}
```

## ページを選択し準備する

### なぜページ選択が重要か

PDF はページ指向で、各ページは独自の座標系を持ちます。Aspose は **1 基数** のインデックスを使用するため、0 基数のコレクションに慣れた開発者は戸惑うことがあります。誤ったページを選択すると `ArgumentOutOfRangeException` がスローされるか、意図しないページが変更されます。

### コード

```csharp
Page page = doc.Pages[1]; // First page
```

ページ 3 で作業する必要がある場合は、インデックスを `3` に変更するだけです。動的なシナリオでは、ループを使用できます。

```csharp
foreach (Page pg in doc.Pages)
{
    // Apply rectangle to every page
}
```

## PDF 上に矩形を定義し描画する

### 矩形座標の理解

Aspose.Pdf の矩形は、左下 (`xLL`, `yLL`) と右上 (`xUR`, `yUR`) のコーナーで定義されます。座標系はページの **左下** を原点とし、X は右方向に、Y は上方向に増加します。これは多くの UI フレームワークとは逆なので、軸に注意してください。

- `0,0` はページの左下隅です。
- 幅 = `xUR - xLL`; 高さ = `yUR - yLL`.

矩形をページより大きく設定すると、`AddRectangle` が例外をスローします。これを防ぐには、ページサイズを取得できます。

```csharp
double pageWidth  = page.PageInfo.Width;
double pageHeight = page.PageInfo.Height;
```

次に矩形をクランプします。

```csharp
double rectWidth  = Math.Min(500, pageWidth);
double rectHeight = Math.Min(700, pageHeight);
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, rectWidth, rectHeight);
```

### 形状を追加するコード

```csharp
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500, 700);
page.AddRectangle(rect);
```

- `AddRectangle` は自動的に細い黒い枠線を描画します。
- 塗りつぶし矩形が必要ですか？ `page.AddAnnotation(new SquareAnnotation(page, rect) { FillColor = Color.Yellow });` を使用します。
- 異なる線の太さが必要ですか？ 追加する前に `rect.LineWidth = 2;` を設定します。

#### エッジケース: 複数の矩形

`AddRectangle` を繰り返し呼び出すと、呼び出しごとに別の形状が追加されます。重なりを防ぐために、後続の矩形をオフセットします。

```csharp
for (int i = 0; i < 3; i++)
{
    var offset = i * 20;
    var r = new Aspose.Pdf.Rectangle(offset, offset, 500 + offset, 700 + offset);
    page.AddRectangle(r);
}
```

## 変更された PDF を保存する

### なぜ保存が最終ステップなのか

すべての操作は永続化するまでメモリ上に留まります。`Document.Save` は新しい内容をディスク（またはストリーム）に書き込みます。元のファイルを上書きすることも可能ですが、バックアップ（`output.pdf`）を残す方が安全です。

### コード

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

- PDF を HTTP 経由で送信する必要がある場合は、`MemoryStream` に保存することもできます。

```csharp
using var ms = new MemoryStream();
doc.Save(ms);
byte[] pdfBytes = ms.ToArray();
// return File(pdfBytes, "application/pdf");
```

## 完全動作例（コピー＆ペースト可能）

すべてをまとめると、以下がすぐに実行できる最終プログラムです。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

class AddRectangleDemo
{
    static void Main()
    {
        const string inputPath  = "input.pdf";
        const string outputPath = "output.pdf";

        // Load the existing PDF
        Document doc;
        try
        {
            doc = new Document(inputPath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error loading PDF: {ex.Message}");
            return;
        }

        // Ensure the document has at least one page
        if (doc.Pages.Count == 0)
        {
            Console.WriteLine("PDF contains no pages.");
            return;
        }

        // Select the first page (1‑based index)
        Page page = doc.Pages[1];

        // Get page dimensions to avoid overflow
        double pageW = page.PageInfo.Width;
        double pageH = page.PageInfo.Height;

        // Define rectangle size (clamp to page bounds)
        double rectW = Math.Min(500, pageW);
        double rectH = Math.Min(700, pageH);
        Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, rectW, rectH);

        // Optional: set line width and color
        rect.LineWidth = 2;
        rect.Color = Color.Blue;

        // Add rectangle to the page
        page.AddRectangle(rect);

        // Save the result
        doc.Save(outputPath);
        Console.WriteLine($"Rectangle added and saved to {outputPath}");
    }
}
```

**期待される出力:** `output.pdf` を開くと、最初のページの左下隅に青い枠線の矩形が表示されます。サイズは最大で 500 × 700 ポイント（ページが小さい場合はそれ以下）です。

## よくある質問とプロのコツ

- **矩形をすべてのページに自動的に追加できますか？**  
  はい—`doc.Pages` をループし、各 `Page` オブジェクトに対して `AddRectangle` 呼び出しを繰り返します。

- **円や多角形を描画したい場合はどうすればいいですか？**  
  Aspose は `AddCircle`、`AddPolygon`、`AddPolyline` メソッドを提供しています。バウンディングボックスに対する矩形ロジックと同様に使用できます。

- **矩形をページの中心に相対的に配置する方法はありますか？**  
  中心座標を計算します:  
  ```csharp
  double centerX = pageW / 2;
  double centerY = pageH / 2;
  double halfW = rectW / 2;
  double halfH = rectH / 2;
  var centeredRect = new Aspose.Pdf.Rectangle(centerX - halfW, centerY - halfH,
                                              centerX + halfW, centerY + halfH);
  page.AddRectangle(centeredRect);
  ```

- **大きな PDF のパフォーマンスはどうですか？**  
  Aspose はページを遅延ロードしますが、数千ページを処理する場合は `PdfExtractor` を使用してサブセットで作業するか、ファイルをストリームしてメモリ使用量を削減することを検討してください。

## 結論

これで **矩形を追加する方法** がわかりました

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Aspose.PDF で PDF ドキュメントを作成 – ページ、形状の追加と保存](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [Aspose.PDF for .NET を使用して PDF にページスタンプを追加する方法：完全ガイド](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Aspose.PDF for .NET を使用して PDF に画像とページ番号を追加する：完全ガイド](/pdf/english/net/document-manipulation/enhance-pdfs-images-page-numbers-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}