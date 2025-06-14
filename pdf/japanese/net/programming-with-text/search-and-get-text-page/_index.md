---
"description": "Aspose.PDF for .NET を使用して PDF ファイル内の特定のページからテキストを検索して取得する方法を学習します。"
"linktitle": "PDFファイル内のテキストページを検索して取得する"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "PDFファイル内のテキストページを検索して取得する"
"url": "/ja/net/programming-with-text/search-and-get-text-page/"
"weight": 430
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDFファイル内のテキストページを検索して取得する

## 導入

PDFドキュメント内の特定のテキストを検索し、抽出して後で活用したいと思ったことはありませんか？ ドキュメントを処理するアプリを開発していて、正確なデータ抽出が必要な場合や、PDFを効率的に解析したい場合など、様々なケースに対応しています。どんな場合でも、このチュートリアルは最適です！ このチュートリアルでは、Aspose.PDF for .NETを使用してPDFファイル内のページからテキストを検索して取得する方法を詳しく説明します。初心者の方でも、経験豊富な開発者の方でも、このガイドは分かりやすく、魅力的な方法で各ステップを解説します。準備はできましたか？さあ、始めましょう！

## 前提条件

コーディングを始める前に、必要なものがすべて揃っていることを確認しましょう。

1. Aspose.PDF for .NETライブラリ: ダウンロードはこちらから [ここ](https://releases.aspose.com/pdf/net/) または、同じリンクから無料トライアル版を入手してください。ご購入については、 [Asposeストア](https://purchase。aspose.com/buy).
2. .NET Framework: Visual Studio などの動作する .NET 開発環境が必要です。
3. PDFファイル：テキストを検索して抽出できるサンプルPDFファイルが必要です。このチュートリアルでは、ファイル名を「 `SearchAndGetTextPage。pdf`.

## パッケージのインポート

まず最初に、Aspose.PDF for .NET を使用するために必要な名前空間をインポートする必要があります。これらがコードの先頭に含まれていることを確認してください。

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System
```

前提条件は説明しましたので、コードをステップごとに解説していきましょう。各ステップは分かりやすく説明されているので、簡単に理解できます。

## ステップ1: ドキュメントディレクトリへのパスを設定する

PDFファイルを操作する前に、PDF文書が保存されている場所へのパスを定義する必要があります。これにより、プログラムがファイルにアクセスできるようになります。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

- dataDir: PDFファイルが保存されているフォルダへのパスです。 `"YOUR DOCUMENT DIRECTORY"` PDF が配置されている実際のパスを入力します。

## ステップ2: PDFドキュメントを読み込む

次のステップは、PDF文書をメモリに読み込み、操作できるようにすることです。手順は以下のとおりです。

```csharp
Document pdfDocument = new Document(dataDir + "SearchAndGetTextPage.pdf");
```

- Document: これは PDF ファイルを読み込む Aspose.PDF クラスです。
- pdfDocument: PDF ファイルが読み込まれた後に保存される変数。

## ステップ3: テキスト吸収オブジェクトを作成する

その `TextFragmentAbsorber` クラスを使用すると、PDF内の特定のテキストを検索できます。このクラスのインスタンスを作成し、指定した検索フレーズに一致するすべてのインスタンスを検索してみましょう。

```csharp
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("Figure");
```

- TextFragmentAbsorber: このクラスは、PDF からテキストを検索して抽出する役割を担います。
- 「図」: PDF 内で検索する任意のテキストに置き換えます。

## ステップ4：PDF全体にテキストアブソーバーを適用する

テキスト吸収機能を設定したら、プログラムに PDF のすべてのページを検索するように指示する必要があります。

```csharp
pdfDocument.Pages.Accept(textFragmentAbsorber);
```

- Accept(): このメソッドは、テキスト アブソーバーを PDF に適用し、すべてのページで指定したテキストをスキャンします。

## ステップ5: 抽出したテキストを取得して反復処理する

PDFのスキャンが完了したので、結果を取得して表示します。抽出したテキストの断片をループ処理します。

```csharp
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- TextFragmentCollection: このコレクションには、テキスト アブソーバーによって検出されたテキスト フラグメントのすべてのインスタンスが保持されます。

## ステップ6: 各フラグメントをループしてデータを抽出する

ループ処理を始めます `textFragmentCollection` 各テキストセグメントの位置、フォントの詳細、色など、さまざまなプロパティを抽出します。

```csharp
foreach (TextFragment textFragment in textFragmentCollection)
{
	foreach (TextSegment textSegment in textFragment.Segments)
	{
		Console.WriteLine("Text : {0} ", textSegment.Text);
		Console.WriteLine("Position : {0} ", textSegment.Position);
		Console.WriteLine("XIndent : {0} ", textSegment.Position.XIndent);
		Console.WriteLine("YIndent : {0} ", textSegment.Position.YIndent);
		Console.WriteLine("Font - Name : {0}", textSegment.TextState.Font.FontName);
		Console.WriteLine("Font - IsAccessible : {0} ", textSegment.TextState.Font.IsAccessible);
		Console.WriteLine("Font - IsEmbedded : {0} ", textSegment.TextState.Font.IsEmbedded);
		Console.WriteLine("Font - IsSubset : {0} ", textSegment.TextState.Font.IsSubset);
		Console.WriteLine("Font Size : {0} ", textSegment.TextState.FontSize);
		Console.WriteLine("Foreground Color : {0} ", textSegment.TextState.ForegroundColor);
	}
}
```

- TextFragment: 各フラグメントには、見つかったテキストの一部が含まれます。
- TextSegment: 各フラグメントには、テキストの異なる部分を表す複数のセグメントを含めることができます。
- TextState: テキストのフォント、サイズ、色に関する詳細情報を提供します。

このループでは、実際のテキスト、その位置 (X 座標と Y 座標)、フォント、フォントが PDF に埋め込まれているかどうか、テキストの前景色などの詳細を出力します。

## 結論

これで完了です！Aspose.PDF for .NET を使って、PDF ファイルからテキストを検索し、抽出することができました。このライブラリの柔軟性は驚くほどです。大規模なドキュメント内の特定のテキストを検索したり、抽出したり、プロパティを分析したりする必要がある場合でも、Aspose.PDF を使えば簡単にできます。さらに、ここで紹介したコードを使えば、ニーズに合わせてカスタマイズすることも可能です。 

## よくある質問

### 一度に複数のフレーズを検索できますか?  
はい、複数のフレーズを検索するためにコードを変更することができます。 `TextFragmentAbsorber` オブジェクト。

### 特定のページからテキストを抽出するにはどうすればよいですか?  
特定のページをターゲットにするには、 `TextFragmentAbsorber` 文書全体ではなく、1ページのみに適用します。例: `pdfDocument。Pages[1].Accept(textFragmentAbsorber);`.

### Aspose.PDF for .NET は無料ですか?  
Aspose.PDFは商用製品ですが、 [無料トライアル](https://releases。aspose.com/).

### Aspose.PDF を使用して PDF から画像を抽出できますか?  
はい、Aspose.PDFではテキストに加えて画像も抽出できます。 [ドキュメント](https://reference.aspose.com/pdf/net/) 詳細についてはこちらをご覧ください。

### さらにヘルプやサポートが必要な場合はどうすればいいですか?  
いつでもサポートを受けることができます [Aspose サポートフォーラム](https://forum。aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}