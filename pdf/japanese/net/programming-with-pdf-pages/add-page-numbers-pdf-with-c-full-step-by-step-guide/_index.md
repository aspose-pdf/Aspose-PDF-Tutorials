---
category: general
date: 2026-01-02
description: C#で Aspose.Pdf を使用して PDF にページ番号を素早く追加します。ベーツ番号付け、フッターテキスト、カスタム透かしの追加、そして単一スクリプトで
  PDF ページをループ処理する方法を学びましょう。
draft: false
keywords:
- add page numbers pdf
- add bates numbering
- add footer text
- add custom watermark
- loop through pdf pages
language: ja
og_description: Aspose.PdfでPDFにページ番号を即座に追加します。このガイドでは、ベーツ番号の追加、フッターテキスト、カスタム透かし、PDFページのループ処理についても解説しています。
og_title: C#でPDFにページ番号を追加 – 完全プログラミングチュートリアル
tags:
- C#
- Aspose.Pdf
- PDF manipulation
title: C#でPDFにページ番号を追加する – 完全ステップバイステップガイド
url: /ja/net/programming-with-pdf-pages/add-page-numbers-pdf-with-c-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add page numbers pdf with C# – Complete Programming Tutorial

PDF ファイルに **ページ番号を追加** したいけど、どこから始めればいいか分からないことはありませんか？ あなたは一人ではありません。開発者は常に、PDF の各ページに番号、フッター、あるいはベーツ方式の識別子をスタンプする方法を尋ねています。

このチュートリアルでは、**PDF ページをループ** し、ページ番号フッターをスタンプし、（必要なら）カスタム透かしを追加する、すぐに実行できる C# のサンプルを紹介します。また、スタンプをベーツ番号に切り替える方法も示します。これは、法的またはフォレンジック文書向けに「ベーツ番号を追加」するということです。最後まで読めば、これらすべてのタスクを手間なく処理できる再利用可能なメソッドが手に入ります。

## Add page numbers pdf – Overview

コードに入る前に、Aspose.Pdf の世界で「add page numbers pdf」が実際に何を意味するのかを整理しましょう。ライブラリでは、ページ上に配置するテキストはすべて **TextStamp** として扱われます。ページプレースホルダー（`{page}`）を含むスタンプを作成し、各ページに適用すれば、連番が自動的に付与されます。同じスタンプに追加テキストを入れれば、**フッター テキストの追加**（例: 「Confidential」やケース固有の識別子）も可能です。

> **なぜ PDF のコンテンツストリームを直接編集せずにスタンプを使うのか？**  
> スタンプはページの余白、回転、既存のグラフィックを考慮した高レベルオブジェクトです。プロパティを数か所変更してスクリプトを再実行するだけで済むので、保守性も格段に向上します。

## Loop through PDF pages to apply stamps

最初の実践ステップは、ソース PDF を開き、ページを順に走査することです。これはほとんどの Aspose サンプルで使用される、**loop through pdf pages** パターンです。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Paths – change these to match your environment
string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // The loop – every Page object lives in pdfDocument.Pages
    foreach (Page page in pdfDocument.Pages)
    {
        // We'll attach a stamp later (see next section)
    }

    // Save the modified document
    pdfDocument.Save(outputPdfPath);
}
```

> **プロのコツ:** PDF が数百ページと大きい場合は、バッチ処理でメモリ使用量を抑えることを検討してください。Aspose.Pdf はページを遅延ストリーミングするため、ループ自体はすでにかなり効率的です。

## Add bates numbering and footer text

各ページを走査できるようになったので、ページ番号と任意のフッターテキストの両方を保持する **再利用可能な TextStamp** を作成しましょう。`{page}` プレースホルダーは現在のページインデックスに自動置換されます。

```csharp
// Create a stamp that will be reused for every page
var batesStamp = new TextStamp("Bates-{page} – Confidential")
{
    // Position the stamp 20 points from the left and bottom edges
    XIndent = 20,
    YIndent = 20,
    // Align left‑bottom so it behaves like a traditional footer
    HorizontalAlignment = HorizontalAlignment.Left,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Font styling – Times New Roman, 10pt, bold, gray
    Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Gray }
};

// Attach the stamp to every page
foreach (Page page in pdfDocument.Pages)
    page.AddStamp(batesStamp);
```

### Why this works

* **`Bates-{page}`** – Aspose が `{page}` を実際のページ番号に置き換えることで、クラシックなベーツ番号が自動的に生成されます。  
* **`Confidential`** – これが **add footer text** 部分です。任意の文字列に置き換えられ、データベースから取得することも可能です。  
* **Styling** – `TextState` を使うと、色、透明度、回転などを PDF の内部コンテンツストリームに触れずに調整できます。

単に数字だけが欲しい場合は、`Bates-` プレフィックスと余分なテキストを削除してください。

```csharp
var simpleStamp = new TextStamp("{page}")
{
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    Font = new Font(FontFamily.Helvetica, 12, FontStyle.Regular),
    TextState = { ForegroundColor = Color.Black }
};
```

## Add a custom watermark (optional)

フッターだけでなく、半透明のロゴや「DRAFT」などの全ページに重ねるオーバーレイが必要になることもあります。そこで **add custom watermark** が活躍します。同じ `TextStamp` クラスを再利用し、配置と透明度を変更するだけです。

```csharp
var watermark = new TextStamp("DRAFT")
{
    // Center it both horizontally and vertically
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Center,
    // Make it big and light
    Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Red, FontSize = 72, FontStyle = FontStyle.Bold, 
                  Transparency = 0.5f }   // 50% transparent
};

// Apply the watermark on top of the page‑number stamp
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(watermark);   // watermark on top
    page.AddStamp(batesStamp);  // then the footer
}
```

> **注意:** 順序は重要です。透かしを先に追加すれば、ページ番号が半透明テキストの上に表示され、読みやすさが保たれます。

## Save the PDF and verify results

スタンプ処理が終わったら、変更をディスクに書き戻すだけです。先ほど配置した `Save` 呼び出しが主な処理を行いますが、ここで簡単な検証コードを追加し、処理したページ数を出力してみましょう。

```csharp
pdfDocument.Save(outputPdfPath);

// Quick verification
using (var resultDoc = new Document(outputPdfPath))
{
    Console.WriteLine($"✅ Successfully added page numbers to {resultDoc.Pages.Count} pages.");
}
```

プログラムを実行すると、すべてのページの末尾に **「Bates‑3 – Confidential」**（シンプルスタンプを使用した場合は「3」）が表示され、透かしを有効にしていればページ中央に薄く「DRAFT」が重なります。

### Expected output

| Page | Footer (example) |
|------|------------------|
| 1    | Bates‑1 – Confidential |
| 2    | Bates‑2 – Confidential |
| …    | … |
| N    | Bates‑N – Confidential |

ビューアでファイルを開くと、番号は左下から 20 pts の位置に配置され、一般的な法務文書の慣例に合わせた配置になります。

## Full working example (copy‑paste ready)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // ---------- Create the page‑number/footer stamp ----------
    var batesStamp = new TextStamp("Bates-{page} – Confidential")
    {
        XIndent = 20,
        YIndent = 20,
        HorizontalAlignment = HorizontalAlignment.Left,
        VerticalAlignment   = VerticalAlignment.Bottom,
        Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Gray }
    };

    // ---------- Optional watermark ----------
    var watermark = new TextStamp("DRAFT")
    {
        HorizontalAlignment = HorizontalAlignment.Center,
        VerticalAlignment   = VerticalAlignment.Center,
        Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Red, Transparency = 0.5f }
    };

    // ---------- Apply stamps to every page ----------
    foreach (Page page in pdfDocument.Pages)
    {
        page.AddStamp(watermark);   // comment out if you don't need a watermark
        page.AddStamp(batesStamp);
    }

    // ---------- Save and verify ----------
    pdfDocument.Save(outputPdfPath);
    Console.WriteLine($"✅ Added page numbers and watermark to {pdfDocument.Pages.Count} pages.");
}
```

このコードを `AddPageNumbers.cs` として保存し、Aspose.Pdf NuGet パッケージを復元（`Install-Package Aspose.Pdf`）して実行してください。**add page numbers pdf** ファイルが生成され、同時に **add bates numbering**、**add footer text**、**add custom watermark**、そして古典的な **loop through pdf pages** パターンがすべてデモンストレーションされます。

![add page numbers pdf example](https://example.com/images/add-page-numbers-pdf.png "Screenshot showing numbered PDF pages with footer and watermark")

## Conclusion

Aspose.Pdf と C# を使って **add page numbers pdf** ファイルを作成するために必要なすべてを網羅しました。ページごとのループ、ベーツ番号のスタンプ、カスタムフッターテキストの追加、さらには半透明透かしのレイヤリングまで、コードはどの既存プロジェクトにもすぐに組み込めるほどコンパクトです。

次のステップとしては、フッターテキストをデータベースから取得したり、セクションごとにフォントを変えたり、ベーツ番号一覧の別 PDF を生成したりと、より高度なシナリオに挑戦してみてください。ここで示したコア概念を応用すれば、要件が拡大しても柔軟に対応できます。

ぜひ試してみて、スタイリングを調整し、コメントで結果を教えてください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}