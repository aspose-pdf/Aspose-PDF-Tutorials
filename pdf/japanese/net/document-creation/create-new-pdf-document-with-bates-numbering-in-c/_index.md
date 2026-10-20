---
category: general
date: 2026-08-04
description: C#で新しいPDFドキュメントを作成し、Aspose.Pdfを使用してBates番号付けPDFを迅速に追加する – 空白ページPDFとカスタムページ番号の追加方法を学ぶ。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new pdf document
- add bates numbering pdf
- how to add bates
- add blank page pdf
- add custom page numbers
language: ja
lastmod: 2026-08-04
og_description: C#で新しいPDFドキュメントを作成し、法務ケース管理のためにベーツ番号付与を自動的に追加 – 完全なコード例を含む。
og_image_alt: Screenshot of a C# program creating a PDF document with Bates numbers
  applied
og_title: C#でベーツ番号付きの新しいPDF文書を作成する
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create new PDF document in C# and add Bates numbering pdf quickly using
    Aspose.Pdf – learn to add blank page pdf and custom page numbers.
  headline: Create new PDF document with Bates numbering in C#
  type: TechArticle
tags:
- C#
- PDF
- Aspose.Pdf
- Bates numbering
title: C#でベーツ番号付きの新しいPDF文書を作成する
url: /ja/net/document-creation/create-new-pdf-document-with-bates-numbering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でベーツ番号付きの新しいPDFドキュメントを作成する

C#で**新しいPDFドキュメントを作成**する必要がある場合、このガイドではAspose.Pdfを使用して**ベーツ番号をPDFに追加**する方法を示します。**空白ページのPDFを追加**し、**カスタムページ番号を追加**する設定方法を学び、最終ファイルを保存します。

このチュートリアルでは、ライブラリのインストールから法的ケースファイル標準に準拠したPDFの生成まで、すべての手順をカバーします。最後まで実行すれば、PDFを生成し、空白ページを挿入し、ベーツ番号を適用し、番号形式をカスタマイズできる単一の実行可能プログラムが完成します。

## 前提条件

* .NET 6.0 SDK またはそれ以降がインストールされている  
* Visual Studio 2022（または任意の C# IDE）  
* 有効な Aspose.Pdf for .NET ライセンスまたは無料評価キー  

追加の NuGet パッケージは必要ありません。チュートリアルが自動的にすべてインストールします。

## 手順 1: NuGet を使用して Aspose.Pdf をインストールする

プロジェクトフォルダーでターミナルを開き、次のコマンドを実行します。

```bash
dotnet add package Aspose.Pdf
```

このコマンドは Aspose.Pdf の最新安定版をプロジェクトに追加し、`Document`、`BatesNumbering` などの PDF 操作クラスを利用できるようにします。

## 手順 2: 新しいPDFドキュメントを作成 – 初期設定

PDF ファイルの作成は、後続のすべての操作の基盤となります。`Document` クラスは PDF 全体のコンテナを表します。

```csharp
using Aspose.Pdf;

// Step 2: Create a new PDF document
using var doc = new Document();
```

*Why this matters*: `Document` のインスタンス化は、ページ、フォント、グラフィックに必要な内部構造を割り当てます。`using var` を使用すると、保存後にファイルが適切に破棄されます。

## 手順 3: 空白ページのPDFを追加する

コンテンツを配置する前に、PDF には少なくとも 1 ページが必要です。空白ページを追加すると、ベーツ番号用のクリーンなキャンバスが得られます。

```csharp
// Step 3: Add a blank page to the document
Page page = doc.Pages.Add();
```

`Pages.Add()` メソッドは、ドキュメントのページコレクションの末尾に新しい空白ページを追加します。後で **カスタムページ番号を追加** する必要がある場合は、この呼び出しを繰り返してページを増やすことができます。

## 手順 4: ベーツ番号付与の設定 – ベーツを追加する方法

ベーツ番号は、法的文書で一般的に使用される連番識別子です。`BatesNumbering` クラスを通じて設定します。

```csharp
// Step 4: Set up Bates numbering options
var bates = new BatesNumbering
{
    StartNumber = 1000,      // Starting number for the sequence
    Prefix = "CaseA-",       // Text to prepend to each number
    Increment = 1,           // Increment between consecutive numbers
    // Optional: Set the location, font size, etc.
};
```

*Why this matters*: `StartNumber` は最初の番号を定義し、`Prefix` は読みやすいラベルを付加し、`Increment` は増分サイズを制御します。`HorizontalAlignment`、`VerticalAlignment`、`FontSize`、`Margins` を調整して、各ページ上の番号の外観を制御できます。

## 手順 5: ページにベーツ番号付与PDFを適用する

番号オプションの準備ができたら、ページ（またはドキュメント全体）に適用します。

```csharp
// Step 5: Apply the Bates numbering to the page
bates.Apply(page);
```

`Apply` を呼び出すと、デフォルトでページのフッターにフォーマットされた番号が挿入されます。別の位置に番号を配置したい場合は、`Apply` を呼ぶ前に `bates.Position` を設定してください。

## 手順 6: ベーツ番号が適用されたPDFを保存する

最後に、メモリ上のドキュメントをディスクに書き出します。

```csharp
// Step 6: Save the PDF with Bates numbers applied
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumbered.pdf");

doc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

保存されたファイルには、ページ下部に **CaseA-1000** と表示されたベーツ番号が付いた単一ページが含まれます。任意のビューアで PDF を開き、番号が正しく付与されていることを確認してください。

## 期待される出力

`BatesNumbered.pdf` を開くと、次のように表示されます。

* 1 枚の空白ページ（追加でページを追加した場合はそれ以上）  
* ページ下部に **CaseA-1000** のテキストが配置されている（デフォルト位置）  

同じ `BatesNumbering` インスタンスを再利用してページを追加すると、番号は自動的に増加します（CaseA-1001、CaseA-1002、…）。

## プロのコツ: ベーツ番号に加えてカスタムページ番号を追加する

ベーツ番号と従来のページ番号の両方が必要な場合があります。ベーツ番号を適用した後に `TextFragment` を追加することで、両方を組み合わせられます。

```csharp
// Add a traditional page number in the header
var pageNumber = new TextFragment($"Page {page.Number}")
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Top,
    FontSize = 12,
    Font = FontRepository.FindFont("Arial")
};
page.Paragraphs.Add(pageNumber);
```

このスニペットは、ベーツラベルを保持しながら **カスタムページ番号を追加** する方法を示しています。

## エッジケース: �数ページへのベーツ番号付与

ドキュメントに複数ページがある場合、同じ `BatesNumbering` インスタンスをループで各ページに適用できます。

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    bates.Apply(doc.Pages[i]);
}
```

このループにより、定義した `StartNumber` と `Increment` に基づいて、すべてのページに連番が付与されます。

## よくある落とし穴と回避方法

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| Numbers appear off‑center | デフォルトの配置がレイアウトに合わないことがある | `bates.HorizontalAlignment` と `bates.VerticalAlignment` を明示的に設定する |
| Numbers overlap existing content | マージンが定義されていない | `bates.Margin` を調整するか、`bates.Position` を使用して番号の位置を移動する |
| License exception at runtime | 評価版は出力に制限がある | ドキュメント作成前に有効な Aspose.Pdf ライセンスを適用する (`License license = new License(); license.SetLicense("Aspose.Pdf.lic");`) |

## 完全な動作例

以下はコピーして貼り付け、実行できる自己完結型プログラムです。

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1. Create a new PDF document
        using var doc = new Document();

        // 2. Add a blank page pdf
        Page page = doc.Pages.Add();

        // 3. Configure Bates numbering – how to add bates
        var bates = new BatesNumbering
        {
            StartNumber = 1000,
            Prefix = "CaseA-",
            Increment = 1,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(20, 20, 20, 20),
            FontSize =


## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックをカバーしています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Aspose.PDF for .NET を使用した PDF のページ番号の追加とカスタマイズ方法 | ドキュメント操作ガイド](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF .NET: FloatingBox を使用して PDF にページ番号を追加する](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Aspose.PDF で PDF ドキュメントを作成 – ページ、シェイプの追加と保存](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}