---
"description": "この包括的なチュートリアルでは、Aspose.PDF for .NET を使用して PDF ドキュメントに目次を追加しながらページ番号をカスタマイズする方法を学びます。"
"linktitle": "目次を追加しながらページ番号をカスタマイズする"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "目次を追加しながらページ番号をカスタマイズする"
"url": "/ja/net/programming-with-document/customizepagenumbeswhileaddingtoc/"
"weight": 100
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 目次を追加しながらページ番号をカスタマイズする

## 導入

ドキュメント管理の世界では、PDFが圧倒的な地位を占めています。様々なプラットフォーム間でドキュメントを共有・保存するための頼りになるフォーマットです。しかし、PDFドキュメントに目次（TOC）などの機能を追加したい場合はどうすればよいでしょうか？そこで活躍するのがAspose.PDF for .NETです！この強力なライブラリを使えば、開発者はPDFファイルを簡単に操作でき、コンテンツの追加、変更、カスタマイズを簡単に行うことができます。このチュートリアルでは、Aspose.PDF for .NETを使用してPDFドキュメントに目次を追加しながらページ番号をカスタマイズする方法を詳しく説明します。さあ、コーディングの準備を始めましょう！

## 前提条件

コードに進む前に、準備しておく必要のあるものがいくつかあります。

1. Visual Studio: お使いのマシンにVisual Studioがインストールされていることを確認してください。これが開発環境となります。
2. Aspose.PDF for .NET: Aspose.PDFライブラリをダウンロードしてインストールする必要があります。 [ここ](https://releases。aspose.com/pdf/net/).
3. C# の基礎知識: C# プログラミングに精通していると、コード スニペットをよりよく理解できるようになります。
4. サンプルPDFファイル：サンプルPDFファイルをご用意ください。簡単なPDFファイルを作成することも、既存のPDFファイルをダウンロードすることもできます。

## パッケージのインポート

まず、必要なパッケージをインポートする必要があります。Visual Studioプロジェクトを開き、Aspose.PDFライブラリへの参照を追加してください。これはNuGetパッケージマネージャーを使用して行うことができます。

1. ソリューション エクスプローラーでプロジェクトを右クリックします。
2. 「NuGet パッケージの管理」を選択します。
3. 「Aspose.PDF」を検索してインストールします。

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

ライブラリをインストールしたら、コーディングを開始できます。

## ステップ1: ドキュメントディレクトリを設定する

まず最初に、ドキュメントディレクトリを設定する必要があります。ここに入力PDFファイルと出力PDFファイルを保存します。 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string inFile = dataDir + "42824.pdf";
string outFile = dataDir + "42824_out.pdf";
```

このスニペットでは、 `YOUR DOCUMENT DIRECTORY` PDFファイルが保存されている実際のパスを入力してください。これにより、既存のPDFファイルを読み込み、修正版を保存できるようになります。

## ステップ2: 既存のPDFファイルを読み込む

ドキュメント ディレクトリが設定されたので、既存の PDF ファイルを読み込みましょう。 

```csharp
Document doc = new Document(inFile);
```

ここで、新しい `Document` 入力ファイルパスを渡すことでオブジェクトを作成できます。これにより、プログラムからPDFコンテンツを操作できるようになります。

## ステップ3: 目次用の新しいページを挿入する

次に、目次を配置する新しいページを PDF に作成する必要があります。

```csharp
Aspose.Pdf.Page tocPage = doc.Pages.Insert(1);
```

この行は文書の先頭に新しいページを挿入します。このページに目次が表示されます。

## ステップ4: TOC情報を作成する

それでは、TOC 情報を表すオブジェクトを作成しましょう。

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocInfo.PageNumbersPrefix = "P";
tocPage.TocInfo = tocInfo;
```

このステップでは、 `TocInfo` オブジェクトを作成し、タイトルを「目次」に設定します。フォントサイズとスタイルもカスタマイズします。 `PageNumbersPrefix` 「P」に設定されており、目次のページ番号の前に付けられます。

## ステップ5: 目次に見出しを追加する

いよいよ楽しい部分です！ドキュメントのページをループして、目次に見出しを追加します。

```csharp
for (int i = 1; i < doc.Pages.Count; i++)
{
    Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
    TextSegment segment2 = new TextSegment();
    heading2.TocPage = tocPage;
    heading2.Segments.Add(segment2);
    heading2.DestinationPage = doc.Pages[i + 1];
    heading2.Top = doc.Pages[i + 1].Rect.Height;
    segment2.Text = "Page " + i.ToString();
    tocPage.Paragraphs.Add(heading2);
}
```

このループでは、新しい `Heading` 各ページのオブジェクトを作成します。各見出しのリンク先ページと表示テキスト（「ページX」（Xはページ番号））を指定します。最後に、見出しを目次ページに追加します。

## ステップ6: 更新したドキュメントを保存する

必要な見出しをすべて追加したら、更新したドキュメントを保存します。

```csharp
doc.Save(outFile);
```

この行は、目次が含まれた変更済みのPDFを保存します。これで出力ファイルを開いて、カスタマイズした目次を確認できます。

## 結論

これで完了です！Aspose.PDF for .NET を使って、PDF ドキュメントに目次を追加しながらページ番号をカスタマイズできました。この強力なライブラリを使えば、PDF ファイルの操作が簡単になり、わずか数行のコードでドキュメントの質を大幅に向上させることができます。レポート、電子書籍、その他の種類の PDF を作成する場合でも、目次があれば読者のナビゲーションが大幅に改善されます。さあ、何を待っているのですか？Aspose.PDF を使い始めて、今すぐ素晴らしい PDF を作成してみましょう！

## よくある質問

### Aspose.PDF for .NET とは何ですか?
Aspose.PDF for .NET は、開発者がプログラムによって PDF ドキュメントを作成、操作、変換できるようにするライブラリです。

### Aspose.PDF は無料で使用できますか?
はい、Asposeはライブラリの機能を試すために無料の試用版を提供しています。ダウンロードできます。 [ここ](https://releases。aspose.com/).

### Aspose.PDF のサポートを受けるにはどうすればよいですか?
Asposeフォーラムにアクセスしてサポートを受けることができます [ここ](https://forum。aspose.com/c/pdf/10).

### 一時ライセンスはありますか?
はい、Aspose.PDFの一時ライセンスをリクエストできます。 [ここ](https://purchase。aspose.com/temporary-license/).

### Aspose.PDF for .NET はどこで購入できますか?
Aspose.PDF for .NETを購入できます [ここ](https://purchase。aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}