---
category: general
date: 2026-03-06
description: C#でPDFドキュメントを作成し、ベーツ番号を簡単に追加します。空白ページのPDFを追加する方法、ページにスタンプを配置する方法、ベーツ番号付けの実装方法を学びましょう。
draft: false
keywords:
- create pdf document
- add bates number
- add blank page pdf
- how to add bates numbering
- place stamp on page
language: ja
og_description: C#でPDF文書を作成し、ベーツ番号を追加します。このガイドでは、空白ページのPDFを追加し、ページにスタンプを配置し、ベーツ番号付けを適用する方法を示します。
og_title: Bates番号付けでPDFドキュメントを作成 – C#チュートリアル
tags:
- Aspose.Pdf
- C#
- PDF automation
title: C#でベーツ番号付きPDFドキュメントを作成する – 完全ガイド
url: /ja/net/programming-with-stamps-and-watermarks/create-pdf-document-with-bates-numbering-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# でベーツ番号付き PDF ドキュメントを作成する

PDF ドキュメントを **C# で作成** したいとき、ベーツ番号をどうやって追加すればいいのか悩んだことはありませんか？ あなた一人だけではありません。法律事務所や裁判所、さらには企業のコンプライアンスチームでも、毎日この課題に直面しています。朗報です！ Aspose.Pdf の数行のコードで、真っ新な PDF を生成し、空白ページを追加し、スムーズにベーツ番号をスタンプできるようになります。

このチュートリアルでは、プロジェクトのセットアップから空白ページ PDF の追加、**ベーツ番号の付け方**、そして **ページへのスタンプ配置** と保存までの全工程を順を追って解説します。最後まで読めば、任意の .NET アプリに貼り付け可能な完成形のコードスニペットが手に入ります。曖昧な説明は一切なく、実行可能なサンプルがすべて揃っています。

## 必要なもの

- **.NET 6+**（または .NET Framework 4.6+ – Aspose.Pdf はどちらでも動作します）
- **Aspose.Pdf for .NET** NuGet パッケージ（`Install-Package Aspose.Pdf`）
- 使いやすい IDE（Visual Studio、Rider、または C# 拡張機能付き VS Code）

以上です。余計な DLL や外部サービスは不要です。さっそく始めましょう。

## Step 1: Create PDF Document – Initial Setup

まずは新しい `Document` オブジェクトを作ります。これは、すべてのコンテンツが配置される空のキャンバスと考えてください。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Initialize a new PDF document
Document pdfDocument = new Document();
```

> **ポイント:** `Document` クラスは Aspose のすべての操作のエントリーポイントです。インスタンス化することで、`Pages` コレクションやメタデータ、セキュリティ設定など、プロフェッショナルな PDF を構築するための基礎にアクセスできます。

## Step 2: Add Blank Page PDF

ページのない PDF は、ページのない本と同じで実用的ではありません。空白ページを追加すれば、ベーツ番号をスタンプする土台ができます。

```csharp
// Add a single blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **プロのコツ:** 複数ページが必要な場合は、ループ内で `pdfDocument.Pages.Add()` を呼び出すだけです。各呼び出しは独立してカスタマイズ可能な新しい `Page` オブジェクトを返します。

## Step 3: How to Add Bates Numbering – Create the TextStamp

ここが本題です：**ベーツ番号**。Aspose.Pdf では、特別なアーティファクトフラグを付けた `TextStamp` として実装されます。

```csharp
// Create a text stamp that will serve as a Bates number
TextStamp batesStamp = new TextStamp("Bates-001")
{
    // Mark the stamp as a Bates‑numbering artifact (helps PDF viewers treat it specially)
    Artifact = ArtifactType.BatesNumbering,
    // Align the stamp to the bottom‑right corner of the page
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Add a small margin so the number isn’t glued to the edge
    Margin = new Margin { Bottom = 10, Right = 10 }
};
```

> **`Artifact` を設定する理由:** 一部の PDF リーダーはベーツ番号を検索可能なメタデータとして扱います。スタンプを `BatesNumbering` アーティファクトとしてフラグ付けすれば、下流ツールが自動的に認識できるようになります。

## Step 4: Place Stamp on Page

スタンプが用意できたら、**ページにスタンプを配置** します。ここで実際に PDF に番号が表示されます。

```csharp
// Add the Bates number stamp to the previously created page
page.AddStamp(batesStamp);
```

> **エッジケース:** 各ページで番号をインクリメントしたい場合は、`pdfDocument.Pages` をループし、`AddStamp` を呼ぶ前に `batesStamp.Value` を更新します。この例ではシンプルに固定の “Bates‑001” を使用しています。

## Step 5: Save and Verify the Result

最後に PDF をディスクに保存します。書き込み権限のあるフォルダーを選択してください。権限が不足していると `UnauthorizedAccessException` が発生します。

```csharp
// Save the stamped PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/BatesStamped.pdf");
```

`BatesStamped.pdf` を任意のビューアで開くと、空白ページの右下に小さな “Bates‑001” がきれいに表示されているはずです。

> **期待される出力:**  
> ![PDF with Bates number stamp](image-placeholder.png "PDF with Bates number stamp")  
> *Alt text: PDF with Bates number stamp on the bottom‑right corner.*

番号が表示されない場合は、余白の値やページサイズ（デフォルトの A4 で問題ありません）を再確認してください。また、`Artifact` フラグが後処理ツールで除去されていないかもチェックしましょう。

## Full Working Example

以下は、コピー＆ペーストだけで動作する完全版プログラムです。`using` ディレクティブとコメントをすべて含んでいるので、すぐに実行できます。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize a new PDF document
        Document pdfDocument = new Document();

        // 2️⃣ Add a blank page – this is where we’ll put the Bates number
        Page page = pdfDocument.Pages.Add();

        // 3️⃣ Create a TextStamp for the Bates number
        TextStamp batesStamp = new TextStamp("Bates-001")
        {
            Artifact = ArtifactType.BatesNumbering,          // Marks it as a Bates‑numbering artifact
            HorizontalAlignment = HorizontalAlignment.Right, // Align right
            VerticalAlignment = VerticalAlignment.Bottom,    // Align bottom
            Margin = new Margin { Bottom = 10, Right = 10 }  // Small margin from edges
        };

        // 4️⃣ Place the stamp on the page
        page.AddStamp(batesStamp);

        // 5️⃣ Save the PDF to disk
        string outputPath = @"C:\Temp\BatesStamped.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"PDF created successfully: {outputPath}");
    }
}
```

プログラムを実行し、PDF を開けば、ベーツ番号が指定した位置に正しく配置されているのが確認できます。 🎉

## Common Variations & Gotchas

| シナリオ | 変更点 | 理由 |
|----------|----------------|-----|
| **複数ページで番号をインクリメント** | `pdfDocument.Pages` をループし、`AddStamp` 前に `batesStamp.Value = $"Bates-{i:D3}"` を設定 | 各ページに固有の識別子を付与でき、法的バンドルで一般的に使用されます |
| **別の配置（左上）** | `HorizontalAlignment = HorizontalAlignment.Left` と `VerticalAlignment = VerticalAlignment.Top` に変更 | 組織によってはヘッダーに番号を入れる方が好まれる場合があります |
| **カスタムフォントや色** | `batesStamp.TextState.Font = FontRepository.FindFont("Arial"); batesStamp.TextState.FontSize = 12; batesStamp.TextState.ForegroundColor = Color.Red;` を設定 | 可読性向上やブランドガイドラインへの適合に役立ちます |
| **既存 PDF を背景として追加** | `Document src = new Document("source.pdf"); pdfDocument.Pages.Add(src.Pages[1]);` を使用 | 事前に生成されたフォーム上にスタンプを重ねる必要がある場合に便利です |

## Wrapping Up

ここまでで、**PDF ドキュメントの作成**、**空白ページ PDF の追加**、そして **ベーツ番号の付与** を Aspose.Pdf for .NET で実装し、**ページへのスタンプ配置** と保存までを実演しました。コードは意図的にコンパクトにしてあるので、数十ファイルのバッチ処理や Web サービスへの統合といった大規模ワークフローにも容易に拡張できます。

次のステップとしては以下を検討してください：

- 大量のケースファイル向けにインクリメントロジックを自動化する
- PDF 生成を ASP.NET Core API に組み込む
- `pdfDocument.Encrypt(...)` でパスワード保護などのセキュリティを追加する

ぜひ実験し、試行錯誤しながらコメントで質問を共有してください。コーディングを楽しみながら、常に完璧にスタンプされた PDF を手に入れましょう！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}