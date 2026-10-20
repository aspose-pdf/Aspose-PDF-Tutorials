---
category: general
date: 2026-08-08
description: C#でAspose.Pdfを使用してPDFにベーツ番号付けを追加する。このチュートリアルでは、空白ページのPDFを追加し、プログラムでPDFを生成する方法も示しています。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering pdf
- add blank page pdf
- generate pdf programmatically
- create pdf aspose
language: ja
lastmod: 2026-08-08
og_description: Aspose.Pdf を使用して C# でベーツ番号付き PDF を追加します。空白ページ PDF の追加方法、プログラムでの PDF
  生成、数分で最終ドキュメントを保存する方法を学びましょう。
og_image_alt: Screenshot of C# code adding Bates numbering and a blank page to a PDF
  using Aspose.Pdf
og_title: AsposeでPDFにベーツ番号付与 – 完全C#ガイド
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  headline: Add bates numbering pdf with Aspose – step‑by‑step guide
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  name: Add bates numbering pdf with Aspose – step‑by‑step guide
  steps:
  - name: What if I need a different font or position?
    text: 'The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`,
      `HorizontalAlignment`, and `VerticalAlignment`. For example:'
  - name: How do I exclude a specific page from numbering?
    text: Create a separate `BatesNumberingArtifact` for the pages you want to number
      and add it only to those pages. Pages without an attached artifact will remain
      unnumbered.
  - name: Does this work with existing PDFs?
    text: 'Yes. Instead of `new Document()`, load an existing file:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF generation
- Bates numbering
title: AsposeでPDFにベーツ番号を追加 – ステップバイステップガイド
url: /ja/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose で bates numbering pdf を追加 – ステップバイステップガイド

Aspose.Pdf を使用した bates numbering pdf の追加は、基本的な手順を理解すれば簡単です。blank page pdf の追加や pdf をプログラムで生成する必要がある場合も、このガイドですべてカバーしています。

このチュートリアルで行うこと:

* 最初から新しい PDF ドキュメントを作成する。  
* Bates 番号を配置する blank page pdf を追加する。  
* カスタムプレフィックスで Bates numbering artifact を設定する。  
* PDF を保存し、生成されたファイルに番号が表示されるようにする。  

最後まで実行すると、**CASE‑1000**、**CASE‑1001**、… のような Bates 番号が付いた PDF を生成する完全な C# コンソール アプリケーションが完成します。これは法務や e‑discovery ワークフローで一般的に求められる要件です。

## 前提条件

* .NET 6.0 SDK 以降（コードは .NET Framework 4.8 でも動作します）。  
* Visual Studio 2022 または任意の C# 対応 IDE。  
* 有効な Aspose.Pdf for .NET ライセンス（または無料評価キー）。  
* C# の基本的な構文に慣れていること。

> **プロのコツ:** ライセンスなしでコードを実行すると、Aspose は出力 PDF に小さな透かしを追加します。

## Step 1: Set up the project and import Aspose.Pdf

新しいコンソール プロジェクトを作成し、Aspose.Pdf NuGet パッケージを追加します:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

サンプルで必要な `using` ディレクティブは次のとおりです:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
```

これらの名前空間により、後で使用する `Document`、`Page`、`BatesNumberingArtifact` クラスにアクセスできます。

## Step 2: Add a blank page pdf

Bates 番号はページに付与する必要があるため、まず番号付けアーティファクトを受け取る blank page を作成します。

```csharp
// Step 2: Add a blank page pdf
Document pdfDocument = new Document();          // creates an empty PDF
Page pdfPage = pdfDocument.Pages.Add();         // adds the first (blank) page
```

`Document` クラスは PDF 全体を表し、`Pages.Add()` はドキュメントのページコレクションの末尾に新しい空白ページを挿入します。ドキュメントが空の状態から開始するため、この呼び出しで最初のページも作成されます。

## Step 3: Configure the Bates numbering artifact

次に、Bates 番号の表示形式を定義します。`BatesNumberingArtifact` を使用すると、開始番号、プレフィックス、サフィックス、書式設定オプションを設定できます。

```csharp
// Step 3: Define Bates numbering settings
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
{
    StartNumber = 1000,          // first number in the sequence
    Prefix = "CASE-",            // custom prefix before each number
    // Optional: you can also set Suffix, FontSize, FontColor, etc.
};
```

**重要なポイント:**  
`StartNumber` を **1000** に設定すると、一般的な法務ケースファイルの慣例に合わせられます。`Prefix` により、各番号が **CASE‑1000**、**CASE‑1001**、… のように表示され、検索やソートが容易になります。

## Step 4: Attach the artifact to the page

アーティファクトはページの `Artifacts` コレクションに追加する必要があり、保存時に Aspose が各ページに描画します。

```csharp
// Step 4: Attach the Bates numbering artifact to the PDF page
pdfPage.Artifacts.Add(batesArtifact);
```

ドキュメントを保存すると、Aspose は自動的にすべてのページにアーティファクトを繰り返し配置し、次のページごとに番号をインクリメントします。

## Step 5: (Optional) Add additional pages

さらにページが必要な場合は、`pdfDocument.Pages.Add()` を繰り返すだけです。前ステップで添付した Bates numbering artifact は新しいページにも自動的に表示されます。

```csharp
// Example: add two more pages
pdfDocument.Pages.Add();
pdfDocument.Pages.Add();
```

## Step 6: Save the PDF – generate pdf programmatically

最後に、ドキュメントをディスクに永続化します。ここで初めて Bates 番号がページに描画されます。

```csharp
// Step 6: Save the PDF – generate pdf programmatically
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumberedDocument.pdf");

// Ensure the directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);

pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to: {outputPath}");
```

**期待される結果:**  
*BatesNumberedDocument.pdf* を開くと、3 ページの PDF が表示されます。各ページの右下に Bates 番号が表示されます:

* ページ 1 → **CASE‑1000**  
* ページ 2 → **CASE‑1001**  
* ページ 3 → **CASE‑1002**

アーティファクトがページコレクションに添付されているため、番号は自動的にインクリメントされます。

## Full, runnable example

すべてをまとめた完全なコンソール プログラムは以下の通りです。コピーして貼り付け、実行できます:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new PDF document
            Document pdfDocument = new Document();

            // Add a blank page pdf
            Page pdfPage = pdfDocument.Pages.Add();

            // Define Bates numbering settings (add bates numbering pdf)
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
            {
                StartNumber = 1000,
                Prefix = "CASE-"
            };

            // Attach the artifact to the page
            pdfPage.Artifacts.Add(batesArtifact);

            // (Optional) add more pages to see incremented numbers
            pdfDocument.Pages.Add(); // page 2
            pdfDocument.Pages.Add(); // page 3

            // Save the PDF – generate pdf programmatically
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "BatesNumberedDocument.pdf");

            Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);
            pdfDocument.Save(outputPath);

            Console.WriteLine($"PDF saved to: {outputPath}");
        }
    }
}
```

`dotnet run` でプログラムを実行します。実行後、デスクトップ上に作成されたファイルを確認し、Bates 番号が正しく付与されていることを確認してください。

![bates numbering pdf の例を追加](/images/bates-numbering.png "Add bates numbering pdf example")

## Common questions and edge cases

### 異なるフォントや位置が必要な場合は？

`BatesNumberingArtifact` には `FontSize`、`FontColor`、`HorizontalAlignment`、`VerticalAlignment` などのプロパティが用意されています。例:

```csharp
batesArtifact.FontSize = 12;
batesArtifact.FontColor = Color.Blue;
batesArtifact.HorizontalAlignment = HorizontalAlignment.Left;
batesArtifact.VerticalAlignment = VerticalAlignment.Top;
```

### 特定のページだけ番号付けを除外したい場合は？

番号付けしたいページ用に別の `BatesNumberingArtifact` を作成し、対象ページにのみ追加します。アーティファクトが添付されていないページは番号が付与されません。

### 既存の PDF でも同様に機能しますか？

はい。`new Document()` の代わりに既存ファイルを読み込みます:

```csharp
Document pdfDocument = new Document("input.pdf");
```

その後、目的のページにアーティファクトを添付して保存します。

## Conclusion

これで **add bates numbering pdf** を Aspose.Pdf で実装する方法、**add blank page pdf** の手順、そして **generate pdf programmatically** の方法を、クリーンで再利用可能な C# ソリューションとして習得しました。このアプローチはページ数やカスタムプレフィックス、スタイリングオプションに関係なく機能し、最終ドキュメントを完全にコントロールできます。

次に検討できるステップ:

* Use **create pdf as

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示したテクニックを基にした関連トピックを扱っています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add an Empty Page at the End of a PDF Using Aspose.PDF for .NET | Step-by-Step Guide](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)
- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}