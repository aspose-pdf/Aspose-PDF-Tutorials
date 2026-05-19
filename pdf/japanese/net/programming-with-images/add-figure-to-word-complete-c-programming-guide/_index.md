---
category: general
date: 2026-04-12
description: C#でWordに図をすばやく追加する方法。Wordでの図の配置方法、docxへの図の挿入、そして高度なレイアウトのためのカスタムXMLの追加を学びましょう。
draft: false
keywords:
- add figure to word
- position figure in word
- insert figure into docx
- how to add custom xml
- how to position shape word
language: ja
og_description: C#でWordに図をすばやく追加。Wordでの図の配置方法、docxへの図の挿入、そして高度なレイアウトのためのカスタムXMLの追加方法を学びましょう。
og_title: Wordに図を追加 – 完全なC#プログラミングガイド
tags:
- C#
- Word Automation
- Document Generation
title: Wordに図を追加 – 完全C#プログラミングガイド
url: /ja/net/programming-with-images/add-figure-to-word-complete-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Word に図を追加 – 完全 C# プログラミングガイド

**Word に図を追加**したいけど、どこから始めればいいか分からないことはありませんか？ 多くのオフィス自動化プロジェクトで足りないのは、カスタム XML パート内に配置されたきれいな画像や図です。このガイドでは、**Word で図を配置**する方法、*.docx* ファイルに図を挿入する手順、そしてカスタム XML を調整して図をネイティブな Word オブジェクトのように扱う方法を詳しく解説します。

実際の例として GemBox.Document ライブラリ（小さなファイルは無料、 大規模は商用）を使用します。最終的に、座標 X = 50、Y = 200 の位置にタグ付けされたコンテナ内に図を配置する、自己完結型の実行可能プログラムが完成します。「ドキュメントを参照」などの曖昧な手順はありません—明確なコードとその動作理由、すぐに自分のプロジェクトにコピーできるヒントを提供します。

## 前提条件

- .NET 6.0 以降（コードは .NET Core 3.1 でもコンパイル可能）
- **GemBox.Document** NuGet パッケージ（`Install-Package GemBox.Document`）
- 事前にカスタム XML タグが配置された Word ファイル（`input.docx`）
- 基本的な C# の知識（各行が何をしているかが分かります）

> **プロのコツ:** 事前にタグ付けされたドキュメントがない場合は、Word で *コンテンツ コントロール* → *XML マッピング ウィンドウ* → カスタム XML パートをマッピングして作成できます。ライブラリはそのコントロールを `TaggedContent` として扱います。

## 手順 1 – ソース ドキュメントを読み込む

最初に既存の *.docx* ファイルを開きます。`Document` が GemBox のすべての操作のエントリーポイントです。

```csharp
using GemBox.Document;
using System.Drawing;

// Set the license key (free version uses a limited license key)
ComponentInfo.SetLicense("FREE-LIMITED-KEY");

// Step 1: Load the source document
Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
```

*なぜ必要か？* ファイルを読み込むことで、内部パーツやカスタム XML コンテナにアクセスできるようになります。これがなければ、図を配置する `TaggedContent` ノードを特定できません。

## 手順 2 – タグ付けされたコンテンツ（カスタム XML コンテナ）にアクセス

カスタム XML は Word の *コンテンツ コントロール* 内に格納されます。GemBox ではこれを `TaggedContent` として公開しています。

```csharp
// Step 2: Access the document's tagged content (the container for custom XML)
TaggedContent taggedContent = doc.TaggedContent;
```

ドキュメントに複数のタグ付けセクションがある場合、`TaggedContent` は **最初の** セクションを返します。特定のタグ名で取得したい場合は、`doc.TaggedContents` を列挙して選択できます。

## 手順 3 – 図要素を作成

`FigureElement` は画像、チャート、または Word が *シェイプ* として扱うすべての視覚オブジェクトを表します。タグ付けされたコンテナ内に作成します。

```csharp
// Step 3: Create a new figure element that will be placed inside the tagged content
FigureElement figure = taggedContent.CreateFigureElement();
```

*なぜここで図を作成するのか？* カスタム XML ノードに結び付けることで、Word はその図が論理的セクションに属すると認識し、後の編集やコンテンツ コントロールベースのワークフローで重要になります。

## 手順 4 – 図を正確に配置

Word はポイント（1 pt ≈ 1/72 in）で位置を指定します。`PointF` 構造体を使うと X/Y 座標を簡単に設定できます。

```csharp
// Step 4: Position the figure at the desired coordinates (X = 50, Y = 200)
figure.Position = new PointF(50, 200);
```

> **シェイプの位置指定方法:** `Position` プロパティは `PointF` を受け取り、最初の値が水平オフセット（左）、2 番目が垂直オフセット（上）をページ余白基準で表します。数値を調整して配置を微調整してください。

## 手順 5 – 図をタグ付けコンテンツ ツリーに挿入

ここで図をカスタム XML ツリーのルート要素に結び付けます。これによりシェイプが Word 文書に物理的に追加されます。

```csharp
// Step 5: Insert the figure into the root element of the tagged content tree
taggedContent.RootElement.AppendChild(figure);
```

この時点で図は文書内に存在しますが、まだ画像ソースが設定されていません。ディスク上のシンプルな PNG を追加しましょう。

```csharp
// Optional: Load an image and assign it to the figure
using (var imageStream = System.IO.File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
{
    figure.Image = new Image(imageStream);
}
```

## 手順 6 – 変更後の文書を保存

最後に変更を新しい *.docx* ファイルに書き出します。

```csharp
// Step 6: Save the updated document
doc.Save(@"YOUR_DIRECTORY\output.docx");
```

`output.docx` を Word で開くと、カスタム XML ブロック内の (50, 200) の位置に画像が正確に配置されているはずです。

### 完全動作サンプル

```csharp
using GemBox.Document;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // License (free version)
        ComponentInfo.SetLicense("FREE-LIMITED-KEY");

        // Load the source DOCX
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // Access the first tagged content container
        TaggedContent taggedContent = doc.TaggedContent;

        // Create a new figure element
        FigureElement figure = taggedContent.CreateFigureElement();

        // Position the figure (X = 50 pt, Y = 200 pt)
        figure.Position = new PointF(50, 200);

        // Load an image file and assign it
        using (FileStream fs = File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
        {
            figure.Image = new Image(fs);
        }

        // Append the figure to the custom XML root
        taggedContent.RootElement.AppendChild(figure);

        // Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

**期待される結果:** `output.docx` を開くと、指定した位置に PNG が配置され、カスタム XML パート内にネストされていることが確認できます。文書の XML（`.docx` → 解凍 → `word/document.xml`）を確認すると、正しい `<w:pict>` 要素と `<v:shape>` の座標が見られます。

## よくある質問とエッジケース

### ドキュメントに複数のタグ付けセクションがある場合は？

`doc.TaggedContents` を列挙し、タグ名で選択します。

```csharp
TaggedContent myTag = doc.TaggedContents.First(tc => tc.TagName == "MyCustomTag");
```

### 図にキャプションを追加するには？

```csharp
figure.Caption = new CaptionElement("Figure 1 – Sample Diagram");
```

### Word 2010 以降でも動作しますか？

はい。GemBox.Document は Open XML 標準を対象としており、Word 2007 以降（2010、2013、2016、2019、Microsoft 365 を含む）で互換性があります。

### シェイプを回転させるには？

```csharp
figure.Rotation = 45; // degrees
```

### ラスター画像ではなくベクターグラフィックを使用するには？

```csharp
figure.Image = new Image(@"YOUR_DIRECTORY\vector.svg");
```

## プロのコツと落とし穴

- **ファイルパス:** `Path.Combine` を使用してハードコーディングされた区切り文字を回避し、特に非 Windows 環境での互換性を確保してください。
- **ライセンス制限:** 無料版 GemBox のライセンスは文書サイズを 20 KB に制限します。大きなファイルは商用キーを購入してください。
- **パフォーマンス:** バッチ処理では単一の `Document` インスタンスを再利用するとメモリ使用量が大幅に削減されます。
- **シェイプのはみ出し:** 図のサイズがページ余白を超えると Word がクリップします。`figure.Width` と `figure.Height` を調整してください。

## 結論

これで **Word に図を追加**する方法、**Word で図を正確に配置**する方法、そしてカスタム XML を操作してシェイプをネイティブ要素のように扱う方法が分かりました。完全な実行可能サンプルは、ドキュメントの読み込み、`FigureElement` の作成、座標設定、画像の添付、そして更新された *.docx* の保存までのすべての手順を示しています。

次は **docx に図を挿入** する練習として、複数の図をループで追加したり、動的にチャートを生成したりしてみてください。また、**カスタム XML を追加** してリッチなコンテンツ コントロールを作成したり、**テーブルやヘッダー内でシェイプを配置**する方法を学んだりすると、さらに応用範囲が広がります。ここで学んだ基礎があれば、Word 文書の自動化をプロ並みに実現できます。

コーディングを楽しんで、何か問題があれば遠慮なくコメントを残してください！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}