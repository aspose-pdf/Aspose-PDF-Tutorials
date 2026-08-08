---
category: general
date: 2026-03-24
description: PDFドキュメントを作成し、タグ付きテキストの絶対位置設定方法を学びます。このチュートリアルでは、span要素の追加方法、タグ付きコンテンツの追加方法、そしてページ上でテキストを配置する方法を示します。
draft: false
keywords:
- create pdf document
- set absolute position
- add span element
- how to add tagged
- position text on page
language: ja
og_description: PDFドキュメントを作成し、絶対位置の設定、span要素の追加、タグ付きPDFコンテンツでページ上のテキスト配置方法をすぐに確認できます。
og_title: PDFドキュメントの作成 – タグ付けテキストの絶対位置指定
tags:
- Aspose.Pdf
- C#
- PDF Tagging
title: PDF文書を作成 – タグ付きテキストの絶対位置を設定
url: /ja/net/programming-with-tagged-pdf/create-pdf-document-set-absolute-position-for-tagged-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF ドキュメントの作成 – タグ付きテキストの絶対位置を設定

アクセシブルでタグ付きテキストが希望通りの位置に配置された **PDF ドキュメント** を作成したことはありますか？たとえば、ラベルを正確な座標に配置する必要があるフォーム形式の PDF を作成したり、証明書を生成して名前を背景画像と完全に合わせたい場合などです。

このガイドでは、**タグ付き** コンテンツの追加方法、**絶対位置の設定**、**span 要素の追加** を示す完全な実行可能サンプルを順に解説します。外部参照はなく、コピー＆ペーストできるコードと各行の「なぜ」についての説明だけです。

## 前提条件

- .NET 6 以上（または .NET Framework 4.6 以上）と C# コンパイラ  
- Aspose.Pdf for .NET（執筆時点での最新バージョン 23.12）を NuGet でインストール  
- C# 文法の基本的な知識  

これらが揃っていれば、さっそく始めましょう。

---

## PDF ドキュメントの作成 – 絶対位置の設定

最初に空の `Document` をインスタンス化します。このオブジェクトは PDF 全体を表し、タグ付きコンテンツツリーへのアクセスを提供します。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();
```

**これが重要な理由:**  
`Document` は PDF 構造のルートです。先に作成することで、ビジュアル要素（ページ、グラフィック）と論理構造（タグ）の両方のキャンバスが確保されます。`using` 文はファイルを適切に破棄し、Windows でのファイルハンドルリークを防止します。

---

## タグ付きコンテンツの有効化（タグの追加方法）

タグ付き要素を挿入する前に、ドキュメントを *タグ付き* とマークする必要があります。Aspose.Pdf は自動的に `TaggedContent` オブジェクトを作成しますが、フラグをオンにする必要があります。

```csharp
// Step 2: Mark the document as tagged (required for accessibility)
pdfDocument.TaggedContent = true;
```

**内部で何が起きているか:**  
`TaggedContent` を `true` に設定すると、PDF リーダーに論理構造ツリーが含まれていることを通知します。これはスクリーンリーダーにとって重要で、`SetPosition` メソッドが span 要素で正しく機能するためにも必要です。

---

## タグ付きコンテンツツリーのルート要素を取得

ルート要素はすべての構造タグ（`<Document>`、`<Section>`、`<Span>` など）の入口です。PDF の見えない “body” と考えてください。

```csharp
// Step 3: Retrieve the root element of the tag tree
var rootElement = pdfDocument.TaggedContent.RootElement;
```

**ルートが必要な理由:**  
以降のすべてのタグはツリーのどこかに接続しなければならず、そうしないとアクセシビリティ階層に現れません。

---

## Span 要素の追加 – インラインテキストの基本ブロック

*span* は HTML の `<span>` に相当する PDF 要素で、短いテキストを正確に配置したい場合に最適です。

```csharp
// Step 4: Create a span element that will hold the text
var spanElement = rootElement.CreateSpanElement();
```

**設計上の注意:**  
よりリッチな書式設定（太字、斜体、ハイパーリンク）が必要な場合は、span を `<Paragraph>` でラップするか、後で `TextFragment` オブジェクトを使用できます。絶対位置指定の場合、プレーンな span が最も軽量です。

---

## 絶対位置の設定 – X=100, Y=200

さあ、楽しい部分です：ページ上の正確な位置に span を配置します。座標系は左下隅 (0,0) を起点とし、ポイント単位（1 pt ≈ 1/72 インチ）を使用します。

```csharp
// Step 5: Position the span at an absolute location (X=100, Y=200)
spanElement.SetPosition(100, 200);
```

**なぜ絶対位置指定か:**  
ピクセル単位のレイアウトが必要な場合—たとえば証明書、請求書、フォームなど—相対的なフロー（左から右へのテキスト）だけでは不十分です。`SetPosition` は通常のテキストフローをバイパスし、指定した位置に要素を固定します。

---

## Span にテキストを追加

span の位置が決まったら、実際の文字列を注入します。

```csharp
// Step 6: Add the desired text to the span
spanElement.AddText("Positioned tagged text");
```

**ヒント:**  
Unicode 文字や右から左へのスクリプトが必要な場合でも、文字列をそのまま渡せば Aspose.Pdf が自動でエンコードします。

---

## Span をルート要素に追加

最後に、span をドキュメントの論理ツリーに接続し、最終的な PDF の一部にします。

```csharp
// Step 7: Append the span to the root so it becomes part of the PDF structure
rootElement.AppendChild(spanElement);
```

**このステップを忘れたらどうなるか:**  
span はメモリ上に存在しますが、ファイルにシリアライズされないため、テキストが表示されず、アクセシビリティツリーも不完全になります。

---

## 完全な実行可能サンプル

以下はコンソールアプリに貼り付けて使用できる完全なプログラムです。1 ページの PDF を作成し、(100, 200) にタグ付き span を追加し、`TaggedPositioned.pdf` として保存します。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Enable tagging for accessibility
        pdfDocument.TaggedContent = true;

        // 3️⃣ Add a blank page (required for visual placement)
        var page = pdfDocument.Pages.Add();

        // 4️⃣ Get the root element of the tagged‑content tree
        var rootElement = pdfDocument.TaggedContent.RootElement;

        // 5️⃣ Create a span element that will hold the text
        var spanElement = rootElement.CreateSpanElement();

        // 6️⃣ Position the span at an absolute location on the page (X=100, Y=200)
        spanElement.SetPosition(100, 200);

        // 7️⃣ Add the desired text to the span
        spanElement.AddText("Positioned tagged text");

        // 8️⃣ Append the span to the root so it becomes part of the PDF structure
        rootElement.AppendChild(spanElement);

        // 9️⃣ Save the document
        pdfDocument.Save("TaggedPositioned.pdf");

        Console.WriteLine("PDF created successfully – check TaggedPositioned.pdf");
    }
}
```

**期待される出力:**  
`TaggedPositioned.pdf` を任意のビューア（Adobe Acrobat、Foxit など）で開くと、左端から 100 pt、下端から 200 pt の位置に **“Positioned tagged text”** というフレーズが表示されます。*Tags* パネルを確認すれば、ドキュメントのルートの下に `<Span>` 要素が一覧表示され、コンテンツが正しくタグ付けされていることが分かります。

---

## よくある質問とエッジケース

### 最初のページ以外の特定のページにテキストを配置したい場合は？

`SetPosition` を呼び出す前に、目的のページを取得します（例：`var page = pdfDocument.Pages[3];`）。span は自動的に現在のページコンテキストに付加されます。

### 位置をインチやセンチメートルで指定できますか？

`SetPosition` はポイント単位を受け取ります。以下の式で変換してください：  
- **インチ → ポイント:** `points = inches * 72`  
- **センチメートル → ポイント:** `points = cm * 28.3465`

### span のフォントや色を変更するには？

span を作成した後、`TextState` を取得して変更できます：

```csharp
var textState = spanElement.TextState;
textState.Font = FontRepository.FindFont("Arial");
textState.FontSize = 12;
textState.ForegroundColor = Color.GetBlack();
```

### 既にタグが存在するドキュメントの場合は？

既存の要素（`rootElement` や特定の `<Section>` など）に新しい span を作成して追加できます。ただし、論理的な階層構造を保つことが重要です。スクリーンリーダーは整然としたツリーを期待します。

### PDF/A や PDF/UA への準拠でも動作しますか？

はい。タグ付き PDF は PDF/UA のコア要件です。PDF/A が必要な場合は、コンテンツ構築後に `pdfDocument.Convert(new PdfAConversionOptions(PdfAStandard.PdfA_1b));` を呼び出してください。

---

## プロのコツと落とし穴

- **プロのコツ:** コンテンツを配置する前に必ずページを追加してください。ページが無いと `SetPosition` はレンダリング先がなく、黙って失敗します。  
- **単位に注意:** UI デザインのピクセルと PDF のポイントを混在させるとテキストがずれます。変換を必ず確認してください。  
- **パフォーマンスのヒント:** 数千枚の PDF を生成する場合、単一の `Document` インスタンスを再利用し、実行間で `pdfDocument.Pages.Clear()` を呼び出して過剰なメモリ割り当てを防ぎます。  
- **アクセシビリティのリマインダー:** タグ付けは単なるオプションではなく、多くの規制（Section 508、EN 301 549）で必須です。`CreateSpanElement` を使用すれば、支援技術がテキストを検出できるようになります。

---

## 結論

ここまでで、**PDF ドキュメントをゼロから作成**し、**絶対位置を設定**し、**span 要素を追加**し、**タグ付きコンテンツの追加方法**を示しました。これにより、ページ上のテキストをピクセル単位で正確に配置できます。完全なサンプルはすぐに実行可能で、解説は *やり方* と *理由* の両方を網羅しています。開発者（や AI アシスタント）が信頼できるソリューションを求める際に必要な情報が揃っています。

次に検討できることは：

- 配置したテキストの背後に画像を追加し、透かし入り証明書を作成する。  
- `CreateParagraphElement` を使用して、絶対配置が必要な複数行ブロックを作成する。  
- 厳格なアクセシビリティ監査を満たすために PDF/UA へエクスポートする。  

座標やフォント、色は自由に調整してください。試行錯誤がタグ付き PDF 生成を習得する最速の方法です。問題があれば下にコメントを残してください。コーディングを楽しんで！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}