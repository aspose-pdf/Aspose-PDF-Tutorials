---
category: general
date: 2026-10-07
description: C# を使用して PDF にベーツ番号を追加する方法を学びましょう。このステップバイステップガイドでは、PDF のページ番号付けやその他の番号付けテクニックもカバーしています。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- pdf page numbering
- number pdf pages
- how to add bates
- bates numbering pdf
language: ja
lastmod: 2026-10-07
og_description: PDFにベーツ番号付けをすばやく追加します。このチュートリアルに従って、PDFページ番号付けをマスターし、PDFページに番号を付け、文書追跡を自動化しましょう。
og_image_alt: Screenshot of a PDF with Bates numbers added using Aspose.Pdf
og_title: C#でPDFにベーツ番号付けを追加 – 完全なAsposeガイド
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  headline: How to add bates numbering to a PDF with Aspose.Pdf
  type: TechArticle
- description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  name: How to add bates numbering to a PDF with Aspose.Pdf
  steps:
  - name: 1. Can I change the location of the numbers?
    text: Yes. Set `batesOptions.Position = new Position(10, 10, 10, 10);` where the
      four values represent margins from the top, bottom, left, and right edges. Aspose
      also provides predefined enums such as `BatesNumberingPosition.BottomCenter`.
  - name: 2. What if my PDF already contains page numbers?
    text: Adding Bates numbers will **stack** on top of existing numbers. To avoid
      visual clutter, either hide the original numbers (if they are part of a text
      layer) or adjust the `batesOptions` font size and position.
  - name: 3. Does this work with encrypted PDFs?
    text: 'Aspose can open password‑protected PDFs if you supply the password:'
  - name: 4. How do I **number pdf pages** with a simple sequential counter (no prefix/suffix)?
    text: 'Just set `Prefix = string.Empty` and `Suffix = string.Empty`:'
  - name: 5. Can I use this approach in ASP.NET Core to serve PDFs on‑the‑fly?
    text: 'Absolutely. Load the document, apply the numbering, then write the stream
      to the HTTP response:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Aspose.Pdf を使用して PDF にベーツ番号付けを追加する方法
url: /ja/net/programming-with-pdf-pages/how-to-add-bates-numbering-to-a-pdf-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf を使用して PDF に bates numbering を追加する方法

PDF に **bates numbering** を追加する必要がある場合、このガイドでは C# での具体的な手順を示します。法的バンドルの作成、ケースファイルの管理、または単に信頼性の高い **pdf page numbering** が必要な場合でも、以下の手順で完全な実行可能なソリューションを提供します。

このチュートリアルでは次のことを学びます:

* 既存の PDF ファイルを読み込む。
* プレフィックス、開始番号、桁埋め、セパレーター、サフィックスなどの Bates numbering オプションを設定する。
* 各ページに番号付けを適用する。
* 更新されたドキュメントを保存する。

外部ツールは Aspose.Pdf for .NET ライブラリ以外必要ありません。また、コードは .NET 6+ および .NET Framework 4.7.2+ でも動作します。

---

## 前提条件

| 要件 | 重要な理由 |
|-------------|----------------|
| **Aspose.Pdf for .NET** (NuGet パッケージ `Aspose.Pdf`) | `Document` と `BatesNumberingOptions` クラスをコードで使用できるように提供します。 |
| **.NET SDK** (6.0 以上推奨) | C# コンソール アプリケーションをコンパイルおよび実行できるようにします。 |
| **番号付けしたいソース PDF** | チュートリアルでは例として `source.pdf` を使用しています。パスはご自身のファイルに置き換えてください。 |
| **出力フォルダーへの書き込み権限** | `Save` 呼び出しで新しいファイルを書き込む必要があります。 |

以下の CLI コマンドでライブラリをインストールできます:

```bash
dotnet add package Aspose.Pdf
```

---

## ステップ 1: 新しいコンソール プロジェクトを作成する

ターミナルを開き、次のコマンドを実行します:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
```

これにより、**bates numbering** を追加するために必要なコードを記述できる最小限の C# プロジェクトが作成されます。

---

## ステップ 2: 必要な `using` ディレクティブを追加する

`Program.cs` を開き、ファイルの先頭に以下の名前空間を追加します:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

* `Aspose.Pdf` は PDF の読み込みと保存に使用する `Document` クラスへのアクセスを提供します。  
* `Aspose.Pdf.Text` には番号の表示方法を定義するオブジェクト `BatesNumberingOptions` が含まれています。

---

## ステップ 3: ソース PDF を読み込む

最初の実行行は、番号付けしたい PDF を読み込みます。`"YOUR_DIRECTORY/source.pdf"` を実際のファイルパスに置き換えてください。

```csharp
// Load the source PDF
Document pdf = new Document("YOUR_DIRECTORY/source.pdf");
```

ファイルが見つからない場合、Aspose は `FileNotFoundException` をスローします。これを防ぐために、事前にパスを検証するとよいでしょう:

```csharp
if (!System.IO.File.Exists("YOUR_DIRECTORY/source.pdf"))
{
    Console.WriteLine("Source PDF not found.");
    return;
}
```

---

## ステップ 4: Bates numbering オプションを定義する

`BatesNumberingOptions` を使用すると、番号付けのすべての視覚要素を制御できます。以下の例は、法的ケースファイル向けの典型的な構成を示しています:

```csharp
// Define Bates numbering options
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",          // Text before the numeric part
    StartNumber = 1000,       // First number to use
    Digits = 6,               // Pad with leading zeros (e.g., 001000)
    Separator = "-",          // Character between prefix, number, and suffix
    Suffix = "-2025"          // Text after the numeric part
};
```

**各プロパティの重要性**

| プロパティ | 目的 |
|----------|---------|
| `Prefix` | プロジェクト、クライアント、ケースで文書をグループ化するのに役立ちます。 |
| `StartNumber` | 初期カウンタを設定します。既に番号付けされたファイルがある場合に便利です。 |
| `Digits` | 幅を統一し、ソートを容易にします。 |
| `Separator` | プレフィックスとサフィックスを組み合わせる際の可読性を向上させます。 |
| `Suffix` | 年、バージョン、その他の後置識別子を追加できます。 |

`batesOptions.Position` と `batesOptions.Font` を使用して配置（上、下、左、右）やフォントスタイルも制御できます。ほとんどのシナリオではデフォルト（右下、12pt Times New Roman）で問題ありません。

---

## ステップ 5: 各ページに番号付けを適用する

`pdf.BatesNumbering.Add` を呼び出すと、ページの表示順に番号が挿入されます。

```csharp
// Apply Bates numbering to every page
pdf.BatesNumbering.Add(batesOptions);
```

特定のページ（例: 表紙ページを除外）だけに **number pdf pages** したい場合は、代わりに `PageCollection` を渡すことができます。

```csharp
// Example: skip the first page
pdf.BatesNumbering.Add(batesOptions, pdf.Pages.Skip(1));
```

---

## ステップ 6: 更新された PDF を保存する

最後に、変更されたドキュメントをディスクに書き込みます。ファイル名は通常、PDF に Bates 番号が含まれていることを示します。

```csharp
// Save the PDF with Bates numbers applied
pdf.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering added successfully.");
```

出力フォルダーが存在しない場合、Aspose が自動的に作成します。ただし、`UnauthorizedAccessException` を防ぐために書き込み権限があることを確認してください。

---

## 完全な実行可能サンプル

すべての要素を組み合わせた、コピーして貼り付けて実行できる完全なプログラムは以下の通りです：

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source PDF
        // -------------------------------------------------
        const string inputPath = "YOUR_DIRECTORY/source.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        Document pdf = new Document(inputPath);

        // -------------------------------------------------
        // 2️⃣ Configure Bates numbering
        // -------------------------------------------------
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            Digits = 6,
            Separator = "-",
            Suffix = "-2025"
        };

        // -------------------------------------------------
        // 3️⃣ Apply the numbering to every page
        // -------------------------------------------------
        pdf.BatesNumbering.Add(batesOptions);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";
        pdf.Save(outputPath);
        Console.WriteLine($"Bates numbering added. Saved to {outputPath}");
    }
}
```

**期待される出力**（コンソール）:

```
Bates numbering added. Saved to YOUR_DIRECTORY/bates_numbered.pdf
```

`bates_numbered.pdf` を開くと、各ページに `CASE-001000-2025`、`CASE-001001-2025` などのラベルがデフォルトの右下隅に表示されます。

---

## よくある質問 (FAQ)

### 1. 番号の位置を変更できますか？

はい。`batesOptions.Position = new Position(10, 10, 10, 10);` と設定します。4 つの値は上、下、左、右のマージンを表します。Aspose には `BatesNumberingPosition.BottomCenter` などの事前定義された列挙体も用意されています。

### 2. PDF にすでにページ番号が含まれている場合は？

Bates 番号を追加すると、既存の番号の上に **重ねて** 表示されます。視覚的な乱れを防ぐには、元の番号を非表示にする（テキスト層の一部である場合）か、`batesOptions` のフォントサイズと位置を調整してください。

### 3. 暗号化された PDF でも動作しますか？

パスワードを指定すれば、Aspose はパスワード保護された PDF を開くことができます。

```csharp
Document pdf = new Document("source.pdf", new LoadOptions { Password = "mySecret" });
```

その後、同様に Bates 番号が適用されます。

### 4. プレフィックス/サフィックスなしでシンプルな連番で **number pdf pages** するには？

`Prefix = string.Empty` と `Suffix = string.Empty` を設定すればよいです。

```csharp
BatesNumberingOptions simple = new BatesNumberingOptions
{
    StartNumber = 1,
    Digits = 4   // 0001, 0002, …
};
pdf.BatesNumbering.Add(simple);
```

### 5. ASP.NET Core でリアルタイムに PDF を配信する際にこの方法を使用できますか？

もちろん可能です。ドキュメントを読み込み、番号付けを適用し、ストリームを HTTP 応答に書き出します。

```csharp
using (var ms = new MemoryStream())
{
    pdf.Save(ms);
    ms.Position = 0;
    return File(ms, "application/pdf", "bates_numbered.pdf");
}
```

---

## エッジケースとベストプラクティスのヒント

| 状況 | 推奨アプローチ |
|-----------|----------------------|
| **大量の PDF（数百ページ）** | `pdf.BatesNumbering.Add` を **ページレベルの変換をすべて実行した後** に呼び出し、同じページを複数回再処理しないようにします。 |
| **カスタムフォント** | `batesOptions.Font = FontRepository.FindFont("Arial")` を設定し、スキャン文書の可読性向上のために `batesOptions.FontSize` を調整します。 |
| **パフォーマンスが重要なバッチジョブ** | ループで多数のファイルを処理する際は単一の `Document` インスタンスを再利用し、各イテレーション後に破棄してメモリを解放します。 |
| **国際文字** | Unicode 対応フォント（例: `Times New Roman Unicode`）を使用して、プレフィックスやサフィックスが正しく表示されるようにします。 |
| **バージョン互換性** | コードは Aspose.Pdf 23.10 以降で動作します。古いバージョンを対象とする場合は、プロパティ名の変更がないか API リファレンスを確認してください。 |

---

## 結論

これで Aspose.Pdf for .NET を使用して PDF に **bates numbering** を追加する方法が分かりました。このチュートリアルでは PDF の読み込み、`BatesNumberingOptions` の設定、各ページへの番号付け、結果の保存を扱いました。これらの要素を組み合わせれば、汎用的な **pdf page numbering** やカスタム形式の **number pdf pages** の実装、さらに大規模な自動化パイプラインへの統合も可能です。

**次のステップ**

* **bates numbering pdf** API をさらに調査し、フォント、色、配置をカスタマイズしてください。  
* **digital signatures** と組み合わせて、改ざん防止の法的バンドルを作成します。  
* 番号付け前に複数のケースファイルを結合する必要がある場合は、Aspose の **PDF merging** 機能を検討してください。

組織のファイリング基準に合わせて、さまざまなプレフィックス、サフィックス、桁数を試してみてください。コーディングを楽しんで！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Create PDF Document C# – Add Bates Numbering Guide](/pdf/english/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/)
- [How to Add Bates Numbering in PDF with C# – Complete Guide](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-c-complete-guide/)
- [Aspose PDF Tutorial – Insert a Blank Page and Update Bates Numbering](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}