---
category: general
date: 2026-08-14
description: GroupDocs を使用して C# でベーツ番号付けオプションを設定する方法。Word を PDF に変換する際に、カスタムプレフィックスと開始番号を追加するステップバイステップのチュートリアルをご覧ください。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set bates numbering options
- Bates numbering C#
- GroupDocs API
- document conversion C#
- AddBatesNumbering method
- C# PDF generation
language: ja
lastmod: 2026-08-14
og_description: C#でベーツ番号付けオプションを迅速に設定する方法。このガイドでは、Word を PDF に変換する際にカスタムプレフィックスと開始番号を追加する方法を示します。
og_image_alt: Screenshot of C# code applying Bates numbering to a PDF
og_title: C#でベーツ番号付けオプションを設定する方法 – ステップバイステップチュートリアル
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  headline: How to set bates numbering options in C# – complete guide
  type: TechArticle
- description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  name: How to set bates numbering options in C# – complete guide
  steps:
  - name: '`Document` – loads the source file.'
    text: '`Document` – loads the source file.'
  - name: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
    text: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
  - name: '`AddBatesNumbering` – the method that injects the numbering into each page.'
    text: '`AddBatesNumbering` – the method that injects the numbering into each page.'
  type: HowTo
tags:
- Bates numbering
- C#
- .NET
- GroupDocs
- PDF conversion
title: C#でベーツ番号付けオプションを設定する方法 – 完全ガイド
url: /ja/net/programming-with-stamps-and-watermarks/how-to-set-bates-numbering-options-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# でベーツ番号付与オプションを設定する方法 – 完全ガイド

C# で **ベーツ番号付与オプションの設定方法** が必要な方のために、本ガイドでは正確な手順を解説します。開始番号の設定、プレフィックスの追加、Word 文書を PDF に変換しながら番号付与を適用する方法を学べます。

文書処理では、法的またはアーカイブ目的で各ページに固有の識別子を付与する必要があることが多いです。このチュートリアルを終える頃には、訴訟支援ツールや自動レポートジェネレータなど、任意の .NET プロジェクトに組み込める再利用可能なスニペットが手に入ります。外部ツールは不要で、GroupDocs.Conversion ライブラリと数行の C# だけで完了します。

## 必要なもの

開始する前に、以下を用意してください。

* .NET 6.0 SDK 以降がインストール済み  
* Visual Studio 2022（または .NET をサポートする任意の IDE）  
* 有効な GroupDocs.Conversion ライセンス（無料トライアルでテスト可能）  
* 番号付与したいサンプル Word 文書（`input.docx`）

これらの前提条件があれば、追加設定なしでコードを実行できます。

## ベーツ番号付与オプションの設定概要

**ベーツ番号付与オプションの設定方法** の核心は次の 3 つのオブジェクトです。

1. `Document` – ソースファイルを読み込みます。  
2. `BatesNumberingOptions` – 開始番号、プレフィックス、その他の書式設定を保持します。  
3. `AddBatesNumbering` – 各ページに番号付与を挿入するメソッド。

各要素が何のためにあるかを理解すれば、カスタムフォントや多言語番号付与といった複雑なシナリオにも対応できるようになります。

## 手順 1: GroupDocs.Conversion NuGet パッケージをインストール

ソリューションフォルダーでターミナルを開き、次を実行してください。

```bash
dotnet add package GroupDocs.Conversion
```

**GroupDocs API** は、後述のチュートリアルで使用する `Document` クラスと `AddBatesNumbering` 拡張メソッドを提供します。

## 手順 2: ソース文書を読み込む

```csharp
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;

// Step 2: Load the source Word document
Document document = new Document(@"C:\Docs\input.docx");
```

*なぜこの手順が必要か？*  
ファイルを読み込むことで、変換エンジンが操作できるメモリ上の表現が生成されます。`Document` インスタンスがなければ、ベーツ番号付与やその他の変換は実行できません。

## 手順 3: ベーツ番号付与オプションを作成

```csharp
// Step 3: Configure Bates numbering
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // The first page will be numbered 1000
    StartNumber = 1000,
    // Each page will be prefixed with "CASE-"
    Prefix = "CASE-",
    // Optional: set the number format (e.g., 4 digits)
    NumberFormat = "#0000",
    // Optional: choose where the number appears (header/footer)
    Position = BatesNumberingPosition.FooterRight
};
```

*なぜこの手順が必要か？*  
`BatesNumberingOptions` は **ベーツ番号付与オプションの設定** に必要なすべての設定をカプセル化します。`StartNumber` と `Prefix` を調整することで、ケース管理システムに合わせた出力が可能になります。`Position` プロパティは視覚的な配置を制御し、コンプライアンス要件で頻繁に求められます。

## 手順 4: 文書にベーツ番号付与を適用

```csharp
// Step 4: Apply the numbering to every page
document.AddBatesNumbering(batesOptions);
```

`AddBatesNumbering` メソッドはロード済みの `Document` の各ページを走査し、設定された文字列を挿入します。メモリ上の表現に対して動作するため、保存前に透かし入れなどの追加処理をチェーンできるのが利点です。

## 手順 5: 結果を PDF に変換して保存

```csharp
// Step 5: Define PDF conversion options (optional)
PdfConvertOptions pdfOptions = new PdfConvertOptions
{
    // Preserve original layout
    EmbedStandardFonts = true
};

// Save the numbered document as PDF
document.Save(@"C:\Docs\output.pdf", pdfOptions);
```

*なぜこの手順が必要か？*  
PDF は法的文書の一般的な最終形式です。`PdfConvertOptions` オブジェクトで出力を細かく調整できますが、基本的な番号付与だけなら必須ではありません。`Save` 呼び出しで、番号付与済みの PDF がディスクに書き出されます。

## 完全な実行可能サンプル

すべてをまとめた自己完結型コンソールアプリケーションは以下の通りです。コンパイルして実行できます。

```csharp
using System;
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;
using GroupDocs.Conversion.Options.Convert.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the source Word document
            Document document = new Document(@"C:\Docs\input.docx");

            // Configure Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1000,
                Prefix = "CASE-",
                NumberFormat = "#0000",
                Position = BatesNumberingPosition.FooterRight
            };

            // Apply numbering to each page
            document.AddBatesNumbering(batesOptions);

            // Optional: set PDF conversion preferences
            PdfConvertOptions pdfOptions = new PdfConvertOptions
            {
                EmbedStandardFonts = true
            };

            // Save the numbered PDF
            document.Save(@"C:\Docs\output.pdf", pdfOptions);

            Console.WriteLine("Bates numbering applied successfully. Output saved to output.pdf");
        }
    }
}
```

**期待される出力**

プログラムを実行すると `output.pdf` が生成され、各ページの右フッターに `CASE-1000`、`CASE-1001` などのラベルが表示されます。任意の PDF ビューアで開き、番号が正しく表示されていることを確認してください。

## よくある落とし穴とベストプラクティス

| 問題 | 発生理由 | 回避策 |
|------|----------|--------|
| **相対パスが `FileNotFoundException` を引き起こす** | コンソールアプリの作業ディレクトリは Visual Studio のものと異なる場合があります。 | 絶対パスを使用するか、`Path.Combine(AppContext.BaseDirectory, "input.docx")` を利用してください。 |
| **番号が既存のフッターと重なる** | ソース文書にすでにフッター領域にコンテンツがあると、新しい番号が隠れることがあります。 | 別の `Position`（例: `HeaderLeft`）を選択するか、テンプレート自体を調整してください。 |
| **大容量文書が遅い** | ベーツ番号付与は各ページを走査するため、ファイルサイズが大きくなるとメモリ使用量が増加します。 | 500 ページを超える場合は `Document.Split` でチャンク処理を行ってください。 |
| **ライセンス期限切れ** | 無料トライアルは 30 日で期限切れとなり、`AddBatesNumbering` 実行時に例外が発生します。 | 文書読み込み前に有効なライセンスキーを設定します: `License license = new License(); license.SetLicense("license.lic");` |

**プロのコツ:** ケースごとに異なる番号形式（例: `2023-CASE-001`）が必要な場合は、`BatesNumberingOptions` を作成する前にプレフィックスを動的に組み立ててください。

## ソリューションの拡張

同じ **Bates numbering C#** アプローチは、`.txt`、`.html`、画像など他のソース形式でも利用できます。`Document` オブジェクト作成時に拡張子を変更すれば、変換エンジンが自動的に処理します。

また、**document conversion C#** と OCR を組み合わせてスキャン済み PDF に対応することも可能です。

```csharp
// Example: add OCR before numbering (requires GroupDocs.Viewer)
using GroupDocs.Viewer;
using GroupDocs.Viewer.Options;

Document scannedPdf = new Document(@"C:\Docs\scanned.pdf");
var viewer = new Viewer(scannedPdf);
var viewOptions = new HtmlViewOptions();
viewer.View(viewOptions); // OCR step
// Then apply Bates numbering as shown earlier
```

## 結論

これで C# における **ベーツ番号付与オプションの設定方法** を最初から最後まで習得できました。`BatesNumberingOptions` オブジェクトを作成し、`AddBatesNumbering` で適用、PDF として保存することで、法的に準拠した一意の識別文書を自動生成できます。

ここからは **C# PDF 生成**、**document conversion C#**、あるいはウォーターマーキングやデジタル署名といった高度な **GroupDocs API** 機能を探求してみましょう。さまざまなプレフィックス、配置、番号形式を試して、ワークフローに最適な設定を見つけてください。

Happy coding!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを基にした関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能をマスターしたり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [Add Bates Numbering PDF in C# – Complete Guide](/pdf/english/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add a Text Stamp Footer in PDFs Using Aspose.PDF for .NET&#58; A Step‑By‑Step Guide](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}