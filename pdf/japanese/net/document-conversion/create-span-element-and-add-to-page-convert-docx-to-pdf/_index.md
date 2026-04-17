---
category: general
date: 2026-03-27
description: C#でspan要素を作成し、DOCXをPDFに変換してPDFとして保存する際にページへspanを追加する方法を学びます。開発者向けのステップバイステップガイド。
draft: false
keywords:
- create span element
- how to add span
- convert docx to pdf
- add element to page
- save as pdf
language: ja
og_description: C#でspan要素を作成し、DOCXをPDFに変換しながらページにspanを追加する方法を学び、PDFとして保存します。完全なコード例が含まれています。
og_title: span要素を作成してページに追加 – DOCXをPDFに変換
tags:
- C#
- DocumentProcessing
- PDFConversion
title: span要素を作成してページに追加 – DOCXをPDFに変換
url: /ja/net/document-conversion/create-span-element-and-add-to-page-convert-docx-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# span 要素を作成してページに追加 – DOCX を PDF に変換

DOCX ファイル内で **span 要素** を作成することは、正確なレイアウト制御が必要なときによくある作業です。このチュートリアルでは、ページに **span を追加する方法**、**DOCX を PDF に変換する方法**、そして **PDF として保存する方法** を、いくつかのシンプルな手順でご紹介します。  

Word 文書を見て「正確な座標に小さなテキストボックスを置きたい」と思ったことがあるなら、ここがピッタリです。ソースファイルの読み込みから、完成した PDF の出力まで、全体のワークフローを順を追って解説します。

## 達成できること

このガイドの最後までに、以下ができるようになります：

* ドキュメント ライブラリの `Document` クラスを使用して `.docx` ファイルをロードします。  
* `TaggedContent` API を使用して **span 要素を作成** します。  
* 選択したページ上でその span を正確な X/Y 座標に配置します。  
* ページが最初でなくても、**要素をページに追加** できるようにします。  
* 単一の `Save` 呼び出しで **DOCX を PDF に変換** し、**PDF として保存** します。

外部ツールは不要、謎の設定も不要—そのままプロジェクトにコピー＆ペーストできるシンプルな C# コードだけです。

## 前提条件

* .NET 6 以上（またはライブラリがサポートする任意の最新 .NET ランタイム）。  
* `Document`、`TaggedContent`、`Position` などを提供するドキュメント処理 SDK。  
* C# の構文に関する基本的な理解—`Console.WriteLine` が書ければ問題ありません。

> **プロのコツ:** SDK のバージョンは常に最新に保ちましょう。最新リリース（2026年3月時点で v3.2）にはページレベル操作のパフォーマンス向上が含まれています。

---

![Diagram illustrating how to create span element and place it on a PDF page](https://example.com/images/create-span-element.png "Create span element placement diagram")

## span 要素の作成 – 位置指定とページへの追加

以下は、ソース DOCX の読み込みから最終 PDF の書き出しまでをすべて実行する完全な実行可能コードです。コンソール アプリに貼り付けて、パスを調整し、実行してみてください。

```csharp
using DocumentProcessing;   // Replace with the actual namespace of your SDK
using DocumentProcessing.Models;

class Program
{
    static void Main()
    {
        // Step 1: Load the DOCX you want to modify
        // -------------------------------------------------
        // The constructor takes a file path; make sure the file exists.
        Document doc = new Document(@"C:\Docs\input.docx");

        // Step 2: Create a new span element using the TaggedContent API
        // -------------------------------------------------
        // A span is a lightweight container for inline content.
        var span = doc.TaggedContent.CreateSpanElement();
        // Optional: add some text inside the span
        span.Text = "Hello, world!";

        // Step 3: Position the span at the desired coordinates (X = 50, Y = 750)
        // -------------------------------------------------
        // Position uses points (1/72 inch). Adjust as needed.
        span.Position = new Position(50, 750);

        // Step 4: Add the span to the target page (page index 1 = second page)
        // -------------------------------------------------
        // Pages are zero‑based; index 1 means the second page in the document.
        doc.Pages[1].Add(span);

        // Step 5: Convert the modified DOCX to PDF and save the result
        // -------------------------------------------------
        // The Save method automatically detects the output format from the extension.
        doc.Save(@"C:\Docs\output.pdf");

        // Confirmation output
        Console.WriteLine("Span added, document converted, and PDF saved successfully.");
    }
}
```

### 手順ごとの説明

#### 手順 1 – DOCX ドキュメントのロード  
`Document` オブジェクトを `input.docx` に対してインスタンス化します。このオブジェクトはメモリ上の Word ファイル全体を表し、ページ、コンテンツ、メタデータへアクセスできるようになります。  

#### 手順 2 – span 要素の作成  
`TaggedContent.CreateSpanElement()` 呼び出しは、軽量なインライン コンテナを返します。テキスト、画像、その他のインライン要素を保持できる、目に見えない小さな箱と考えてください。`span.Text` にテキストを設定するのは任意ですが、デバッグ時に便利です。  

#### 手順 3 – span の位置指定  
`new Position(50, 750)` は、span の左上隅を左余白から 50 pt、ページ上端から 750 pt の位置に設定します。これらの値は絶対座標なので、任意の場所に配置でき、正確なレイアウトが可能です。  

#### 手順 4 – 対象ページへの span の追加  
`doc.Pages[1].Add(span)` は、2 ページ目に span を挿入します。API はゼロベースインデックスを使用するため、ページ 0 が最初のページです。最初のページに追加したい場合は `doc.Pages[0]` を使用してください。  

#### 手順 5 – DOCX を PDF に変換して PDF として保存  
`doc.Save("output.pdf")` を呼び出すと、変更されたドキュメントをディスクに書き出すと同時に、拡張子が `.pdf` であることにより内容が PDF に変換されます。別途変換ステップは不要で、これが **PDF として保存** する最も簡単な方法です。

---

## 別のページに span を追加する方法（上級）

ページインデックスが事前に分からないこともあります。その場合は、人間にとって分かりやすいページ番号で検索したり、特定のキーワードでページを探したりできます。

```csharp
// Find the page that contains the word "Summary"
int targetIndex = doc.Pages
    .Select((p, i) => new { Page = p, Index = i })
    .FirstOrDefault(x => x.Page.Text.Contains("Summary"))?.Index ?? 0;

// Fallback to first page if not found
targetIndex = Math.Max(targetIndex, 0);

// Add the span to the discovered page
doc.Pages[targetIndex].Add(span);
```

**なぜ重要か:** ページ数が変動するレポートでは、`Pages[1]` をハードコーディングするとレイアウトが崩れます。このスニペットは、**span を動的に追加** するための堅牢なパターンを示しています。

---

## よくある落とし穴と回避策

| 問題 | 起こること | 対策 |
|-------|--------------|-----|
| **Span not visible** | 座標がページ外になっている、または span の幅/高さが 0 です。 | `Position` の値を再確認し、PDF ビューアの定規機能を使って確認してください。 |
| **Wrong page index** | 0 ページ目に追加したつもりが、実際は 2 ページ目に表示される。 | API はゼロベースなので、人間が読むページ番号に 1 を足すことを忘れないでください。 |
| **Saving overwrites source** | `doc.Save("input.docx")` が元のファイルを上書きしてしまう。 | 変換時は必ず新しいパス（例: `output.pdf`）に保存してください。 |
| **Missing SDK reference** | `Document` クラスでコンパイルエラーが出る。 | NuGet パッケージをインストールします: `dotnet add package DocumentProcessing.SDK`。 |

---

## 結果の検証

プログラムを実行したら、任意の PDF ビューアで `output.pdf` を開きます。2 ページ目の (50, 750) に「Hello, world!」というテキストが正確に表示されているはずです。別の位置に表示された場合は、`Position` の値を調整して再実行してください。  

自動テストが必要な場合は、PDF パーサー（例: iTextSharp）を使ってテキスト座標をプログラムでアサートできます。

```csharp
// Example using iTextSharp to verify position (pseudo‑code)
var pdfReader = new PdfReader(@"C:\Docs\output.pdf");
var page = pdfReader.GetPageContent(2);
Debug.Assert(page.Contains("Hello, world!"));
```

---

## 次のステップ

* **span のスタイル設定** – `span.Font`、`span.Color` などのスタイリングプロパティを調べます。  
* **画像の追加** – グラフィックには span の代わりに `CreateImageElement()` を使用します。  
* **バッチ処理** – DOCX ファイルが入ったフォルダーをループ処理します。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}