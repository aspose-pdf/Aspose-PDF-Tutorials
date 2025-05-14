---
"description": "Aspose.PDF for .NET を使用して PDF ドキュメントのすべてのページからテキストを検索して取得する方法を学習します。"
"linktitle": "検索してテキストをすべて取得"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "検索してテキストをすべて取得"
"url": "/ja/net/programming-with-text/search-and-get-text-all/"
"weight": 420
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 検索してテキストをすべて取得

## 導入

PDFから特定のテキストを抽出したいと思ったことはありませんか？でも、難しいと感じたことはありませんか？PDFはまるで鍵のかかったコンテナのように、必要な情報を取得するのが難しいと感じることがあります。しかし、朗報です。Aspose.PDF for .NETを使えば、あらゆるPDFから簡単にテキストを検索・取得できます。この強力なライブラリは、.NETアプリケーションでPDFを操作するために必要なものをすべて提供しており、テキスト抽出を非常に簡単に行えます。このチュートリアルでは、Aspose.PDF for .NETを使用してPDFファイルからテキストを検索・抽出するプロセスを詳しく説明します。テキスト分析ツールを構築する場合でも、PDFレポートからのデータ抽出を自動化する場合でも、このチュートリアルはまさにうってつけです。

## 前提条件

コードに進む前に、すべてがセットアップされていることを確認しましょう。

1. Aspose.PDF for .NET: Aspose.PDF for .NETをダウンロードしてインストールする必要があります。ダウンロードページから入手できます。 [ここ](https://releases。aspose.com/pdf/net/).
2. .NET 環境: 開発マシンに .NET Framework または .NET Core が設定されていることを確認します。
3. 基本的な C## の知識: C# と .NET プロジェクトの操作に関するある程度の知識が推奨されます。
4. PDF文書: テキスト抽出の対象となるサンプルPDFファイル。この例では、 `SearchAndGetTextFromAll。pdf`.

## パッケージのインポート

コードを記述する前に、Aspose.PDF を操作するために必要な名前空間をプロジェクトにインポートする必要があります。

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

これらの名前空間は、PDF のドキュメント オブジェクト モデルへのアクセスを提供し、ファイル内のテキストを操作できるようにします。

簡単に実行できるように、プロセスを簡単な手順に分解してみましょう。

## ステップ1: ドキュメントディレクトリを設定する

まず最初に、PDFファイルが保存されているディレクトリへのパスを指定する必要があります。これにより、アプリケーションはテキストを抽出するファイルを見つけやすくなります。

```csharp
// ドキュメント ディレクトリへのパス。
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

- その `dataDir` 変数は、 `SearchAndGetTextFromAll.pdf` ファイルが保存されます。
- 交換する `"YOUR DOCUMENT DIRECTORY"` マシン上の実際のパスを入力します。

## ステップ2: PDFドキュメントを開く

次に、Aspose.PDFの `Document` 物体。

```csharp
// ドキュメントを開く
Document pdfDocument = new Document(dataDir + "SearchAndGetTextFromAll.pdf");
```

- 新しいインスタンスを作成します `Document` PDF の完全なファイル パスを渡してクラスを作成します。
- これにより、PDF がメモリに読み込まれ、処理の準備が整います。

## ステップ3: テキストアブソーバーを作成する

その `TextFragmentAbsorber` オブジェクトはPDF内の特定のテキストを検索するために使用されます。この場合、「text」という単語を検索します。

```csharp
// 入力された検索フレーズのすべてのインスタンスを検索するための TextAbsorber オブジェクトを作成します。
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("text");
```

- その `TextFragmentAbsorber` 文字列で初期化される `"text"`これは、PDF 文書内で「テキスト」という単語の出現を検索することを意味します。

## ステップ4：すべてのページでアブソーバーを受け入れる

ここで、PDF ドキュメントにアブソーバーを受け入れ、すべてのページでテキストを検索するように指示します。

```csharp
// すべてのページの吸収剤を受け入れる
pdfDocument.Pages.Accept(textFragmentAbsorber);
```

- その `Accept` メソッドはドキュメントのページに適用されます。これにより、指定されたテキストがすべてのページで検索されます。

## ステップ5: テキストフラグメントの抽出

アブソーバーが文書をスキャンしたら、抽出されたテキストの断片を取得できます。

```csharp
// 抽出したテキストフラグメントを取得する
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- その `TextFragments` の財産 `TextFragmentAbsorber` 検索語に一致するすべてのテキストフラグメントのコレクションを返します。

## ステップ6: テキストフラグメントをループする

テキストフラグメントのコレクションができたので、それらをループして詳細を抽出します。

```csharp
// フラグメントをループする
foreach (TextFragment textFragment in textFragmentCollection)
{
    Console.WriteLine("Text : {0} ", textFragment.Text);
    Console.WriteLine("Position : {0} ", textFragment.Position);
    Console.WriteLine("XIndent : {0} ", textFragment.Position.XIndent);
    Console.WriteLine("YIndent : {0} ", textFragment.Position.YIndent);
    Console.WriteLine("Font - Name : {0}", textFragment.TextState.Font.FontName);
    Console.WriteLine("Font - IsAccessible : {0} ", textFragment.TextState.Font.IsAccessible);
    Console.WriteLine("Font - IsEmbedded : {0} ", textFragment.TextState.Font.IsEmbedded);
    Console.WriteLine("Font - IsSubset : {0} ", textFragment.TextState.Font.IsSubset);
    Console.WriteLine("Font Size : {0} ", textFragment.TextState.FontSize);
    Console.WriteLine("Foreground Color : {0} ", textFragment.TextState.ForegroundColor);
}
```

- その `foreach` ループはそれぞれを繰り返す `TextFragment` コレクション内。
- 実際のテキスト、ページ上の位置、フォントの詳細、フォント サイズなど、各フラグメントのさまざまなプロパティを印刷します。
- その `XIndent` そして `YIndent` プロパティは、PDF 内のテキスト フラグメントの正確な座標を示します。

## 結論

これで完了です！わずか数行のコードで、Aspose.PDF for .NET を使用して PDF からテキストを検索し、抽出することができました。Aspose.PDF は柔軟性が高く、PDF を様々な方法で操作できるため、.NET 環境で堅牢な PDF ソリューションを必要とする開発者にとって最適な選択肢です。このサンプルを簡単に拡張して、他の単語を検索したり、より詳細な情報を抽出したり、ニーズに合わせて PDF コンテンツを操作したりすることも可能です。このガイドが、PDF を操作するための明確で分かりやすいアプローチを提供できたことを願っています。ぜひ、ご自身の PDF で試してみてください。

## よくある質問

### 一度に複数の単語を検索できますか?  
はい、変更できます `TextFragmentAbsorber` 検索文字列を適宜調整して複数のフレーズを検索します。

### テキストが複数行にまたがる場合はどうなりますか?  
Aspose.PDF は、複数行にまたがるテキストでも認識・抽出します。これらの断片は個別に処理できます。

### 抽出したテキストをファイルに保存するにはどうすればよいですか?  
抽出したテキストは、次のような標準のC#ファイルI/O操作を使用してファイルに書き込むことができます。 `StreamWriter`。

### Aspose.PDF はスキャンされた PDF からのテキスト抽出をサポートしていますか?  
Aspose.PDFはOCRをサポートしていません。スキャンしたPDFの場合は、テキストを認識するためにOCRツールが必要になります。

### 暗号化された PDF をどのように処理すればよいですか?  
PDF がパスワードで保護されている場合は、ドキュメントを読み込むときにパスワードを入力することで、Aspose.PDF を使用してロックを解除できます。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}