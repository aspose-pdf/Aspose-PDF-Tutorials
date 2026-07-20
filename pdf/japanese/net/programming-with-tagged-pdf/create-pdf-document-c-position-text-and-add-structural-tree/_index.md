---
category: general
date: 2026-07-20
description: 'Aspose.Pdf を使用して C# で PDF ドキュメントを作成: PDF にテキストを配置し、アクセシビリティのために構造ツリーを追加します。ステップバイステップのガイドに従ってください。'
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document c#
- position text in pdf
- add structural tree
- Aspose.Pdf tagging
- PDF/A‑2b generation
language: ja
lastmod: 2026-07-20
og_description: C#ですぐにPDFドキュメントを作成。PDF内のテキスト配置方法と、Aspose.Pdfを使用して構造ツリーを追加し、PDF/A‑2bに準拠させる方法を学びましょう。
og_image_alt: Screenshot showing positioned text inside a PDF generated with Aspose.Pdf
  in C#
og_title: C#でPDFドキュメントを作成 – テキスト配置とタグ構造の完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: 'Create PDF document C# with Aspose.Pdf: position text in PDF and add
    structural tree for accessibility. Follow this step‑by‑step guide.'
  headline: Create PDF Document C# – Position Text and Add Structural Tree
  type: TechArticle
- description: 'Create PDF document C# with Aspose.Pdf: position text in PDF and add
    structural tree for accessibility. Follow this step‑by‑step guide.'
  name: Create PDF Document C# – Position Text and Add Structural Tree
  steps:
  - name: Can I use other units (mm, cm) for positioning?
    text: Aspose.Pdf works natively with points. If you prefer millimeters, convert
      using `1 mm ≈ 2.83465 pt`. For example, `Position(25.4, 254)` places the paragraph
      1 cm from the left and 9 cm from the bottom.
  - name: What if I need to add multiple tags (headings, tables)?
    text: Simply create additional `StructureElement` objects with tags like `"H1"`
      for headings or `"Table"` for tables, and add the corresponding content as kids.
      Nesting works the same way—children inherit the parent’s logical order.
  - name: Does this approach work for PDF/A‑1b or PDF/A‑3b?
    text: Yes. Replace `SaveFormat.PdfA2b` with `SaveFormat.PdfA1b` or `SaveFormat.PdfA3b`.
      Keep in mind that each PDF/A version has its own set of required metadata; Aspose.Pdf
      will prompt you if something is missing.
  type: HowTo
tags:
- C#
- PDF
- Aspose.Pdf
title: C#でPDF文書を作成 – テキストの配置と構造ツリーの追加
url: /ja/net/programming-with-tagged-pdf/create-pdf-document-c-position-text-and-add-structural-tree/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDFドキュメント作成 C# – テキストの位置指定と構造ツリーの追加

テキストを正確に配置でき、かつアクセシビリティのために適切な構造ツリーを埋め込んだ **PDFドキュメントをC#で作成** したいことはありませんか？請求書、レポート、電子書籍を作成する開発者は常にこのニーズに直面しています。このチュートリアルでは、強力な Aspose.Pdf ライブラリを使用した、すぐに実行できる完全なサンプルを順を追って解説します。

**position text in PDF** の方法、**add structural tree** 手順でのセマンティックタグの付与、そして最終的に PDF/A‑2b 準拠のドキュメントとして保存する方法をカバーします。最後まで読むと、任意の .NET プロジェクトに組み込める再利用可能なスニペットが手に入ります。

---

## 必要なもの

- **.NET 6.0** 以上（コードは .NET Framework 4.6+ でも動作します）  
- **Aspose.Pdf for .NET** NuGet パッケージ (`Install-Package Aspose.Pdf`)  
- 基本的な C# 開発環境（Visual Studio、Rider、または VS Code）  

追加のサードパーティーツールは不要です。ライブラリがページレイアウトから PDF/A 準拠まで全てを処理します。

---

## 手順 1: PDF ドキュメントの初期化 (Create PDF Document C#)

最初に新しい `Document` オブジェクトを作成します。これは何も描かれていないキャンバスのようなもので、ページやテキスト、構造メタデータを受け取る準備ができています。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Struct;

// Create a new PDF document – this is the core of our create pdf document c# workflow
Document pdfDoc = new Document();

// Add a blank page to the document; the page will host our positioned text
Page pdfPage = pdfDoc.Pages.Add();
```

> **Why this matters:** `Document` クラスは Aspose.Pdf のすべての操作のエントリーポイントです。早めにページを追加しておくことで、後から視覚コンテンツと構造ツリーの両方を結び付ける基盤ができます。

---

## 手順 2: Paragraph を定義して位置指定 (Position Text in PDF)

ここで `Paragraph` オブジェクトを作成し、Aspose にページ上の正確な表示位置を指示します。PDF の座標はポイント単位（1 インチ = 72 pt）で測定されるため、`Position(72, 720)` は左端から 1 インチ、下端から 10 インチの位置に段落を配置します。

```csharp
// Define a paragraph positioned 1 inch from the left and 10 inches from the bottom
Paragraph positionedParagraph = new Paragraph
{
    // Position(x, y) – X is horizontal, Y is vertical from the bottom-left corner
    Position = new Position(72, 720) // 72 pt = 1 inch, 720 pt = 10 inch
};

// Add the actual text we want to display
positionedParagraph.Segments.Add(
    new TextFragment("Tagged paragraph at a specific location.")
);
```

> **Pro tip:** 複数行を配置する場合は、各段落の `Y` 座標を調整するか、より細かい制御が必要なときは `TextBuilder` を使用してください。

---

## 手順 3: 構造要素の作成 (Add Structural Tree)

アクセシビリティ対応 PDF は、コンテンツの論理順序を示す *構造ツリー* に依存します。ここではタグ `"P"`（段落）を持つ `StructureElement` を作成し、先ほど位置指定した段落を子要素として添付します。

```csharp
// Create a structural element (tag) for the paragraph – this is the add structural tree step
StructureElement structElement = new StructureElement("P");

// Attach the paragraph as a child of the structural element
structElement.AddKid(positionedParagraph);
```

> **Why we add a structural tree:** スクリーンリーダーやその他の支援技術はこれらのタグを利用して文書をナビゲートします。タグが無ければ、見た目は完璧でもアクセシビリティが確保されません。

---

## 手順 4: 構造要素をページに紐付け

各ページは独自の構造要素コレクションを保持しています。`structElement` を `pdfPage.StructElements` に追加することで、論理階層を視覚レイアウトに統合します。

```csharp
// Attach the structural element to the page's structure tree
pdfPage.StructElements.Add(structElement);
```

> **Common pitfall:** このステップを忘れると、タグはメモリ上に存在しますがページに結び付けられず、支援技術からは見えなくなります。

---

## 手順 5: PDF/A‑2b として保存 (Ensuring Long‑Term Preservation)

PDF/A‑2b は長期保存向けに設計された PDF のサブセットです。Aspose.Pdf はワンコールでこの形式を生成できます。`"YOUR_DIRECTORY"` を実際のパスに置き換えてください。

```csharp
// Save the document as a PDF/A‑2b file – ideal for long‑term storage and compliance
pdfDoc.Save("YOUR_DIRECTORY/TaggedWithPosition.pdf", SaveFormat.PdfA2b);
```

> **Result:** テキストが指定した位置に正確に配置され、文書にはアクセシビリティツール向けの適切な構造ツリーが含まれた PDF が生成されます。

---

## 完全動作サンプル

以下はコンソールアプリにそのまま貼り付けて使用できる完全なプログラムです。Aspose.Pdf の NuGet 参照を追加すれば、ビルドして実行できます。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Struct;

namespace PdfPositioningDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Initialize the document
            Document pdfDoc = new Document();
            Page pdfPage = pdfDoc.Pages.Add();

            // Step 2: Define and position the paragraph
            Paragraph positionedParagraph = new Paragraph
            {
                Position = new Position(72, 720) // 1 inch left, 10 inches up
            };
            positionedParagraph.Segments.Add(
                new TextFragment("Tagged paragraph at a specific location.")
            );

            // Step 3: Create the structural element (tag)
            StructureElement structElement = new StructureElement("P");
            structElement.AddKid(positionedParagraph);

            // Step 4: Attach the structural element to the page
            pdfPage.StructElements.Add(structElement);

            // Step 5: Save as PDF/A‑2b
            string outputPath = @"C:\Temp\TaggedWithPosition.pdf";
            pdfDoc.Save(outputPath, SaveFormat.PdfA2b);

            Console.WriteLine($"PDF created successfully at: {outputPath}");
        }
    }
}
```

**Expected output:** 実行後に `TaggedWithPosition.pdf` を開きます。1 ページ目の右下付近に「Tagged paragraph at a specific location.」という文が表示されます。Adobe Acrobat の「Tags」パネルなどで PDF のタグを確認すると、該当段落に `<P>` 要素がリンクされていることが分かります。

---

![Aspose.Pdfで生成されたPDFの位置指定テキストのスクリーンショット](/images/pdf-positioned.png){: .align-center }

*画像の代替テキスト:* **create pdf document c#** – Aspose.Pdfで生成されたPDF内の位置指定テキストを示すスクリーンショット。

---

## よくある質問とエッジケース

### 他の単位（mm、cm）で位置指定できますか？

Aspose.Pdf はポイント単位で動作します。ミリメートルを使用したい場合は `1 mm ≈ 2.83465 pt` で換算してください。例として `Position(25.4, 254)` は左端から 1 cm、下端から 9 cm の位置に段落を配置します。

### 複数のタグ（見出し、テーブル）を追加したい場合は？

`"H1"`（見出し）や `"Table"`（テーブル）といったタグを持つ `StructureElement` を追加し、対応するコンテンツを子要素として設定します。入れ子構造も同様に機能し、子要素は親の論理順序を継承します。

### PDF/A‑1b や PDF/A‑3b でも同様に動作しますか？

はい。`SaveFormat.PdfA2b` を `SaveFormat.PdfA1b` または `SaveFormat.PdfA3b` に置き換えるだけです。ただし、各 PDF/A バージョンには必須メタデータが異なるため、欠落がある場合は Aspose.Pdf が警告を出します。

---

## まとめ

**create pdf document c#** のシナリオを通じて以下を実施しました。

1. Aspose.Pdf を使用して新規 PDF をインスタンス化。  
2. 正確な座標で **position text in PDF**。  
3. アクセシビリティ向けに **add structural tree** 要素を付与。  
4. 標準準拠の PDF/A‑2b ファイルとして保存。  

すべての手順は独立しており、複数ページや異なるタグタイプへの拡張も容易です。

---

## 次にやることは？

- **Styling text** – `TextState` を使ってフォント、色、サイズを変更。  
- **Embedding images** – `ImageFragment` を使用し、段落と並べて配置。  
- **Generating tables** – `Table` オブジェクトを作成し、`"Table"` タグでマークしてリッチなセマンティクスを提供。  
- **Automation pipelines** – このコードをバックグラウンドサービスに組み込み、毎晩請求書を自動生成。

ぜひ試してみて、どのバリエーションが最も役立つか教えてください。Happy coding!

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を応用した関連トピックを扱っています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、API の追加機能を習得したり、プロジェクトで代替実装を検討したりするのに役立ちます。

- [Create Tagged PDFs with Aspose.PDF for .NET: A Complete Guide to Enhancing Accessibility and Document Structure](/pdf/english/net/advanced-features/create-tagged-pdfs-aspose-pdf-net/)
- [Create PDF Document with Aspose.PDF – Step‑by‑Step Guide](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Create & Rotate Text in PDFs Using Aspose.PDF .NET: A Comprehensive Guide for Developers](/pdf/english/net/text-operations/create-rotate-text-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}