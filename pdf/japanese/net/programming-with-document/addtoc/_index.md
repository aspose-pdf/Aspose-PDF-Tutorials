---
"description": "Aspose.PDF for .NET を使用して PDF に目次を追加する方法を学びましょう。このステップバイステップガイドは、プロセスを簡素化し、ドキュメント内のナビゲーションを容易にします。"
"linktitle": "PDFファイルに目次を追加する"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "PDFファイルに目次を追加する"
"url": "/ja/net/programming-with-document/addtoc/"
"weight": 40
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDFファイルに目次を追加する

## 導入

長々としたPDFファイルをスクロールしながら、整理された目次があればいいのにと思ったことはありませんか？今日はそんなあなたに朗報です！このチュートリアルでは、Aspose.PDF for .NETを使ってPDFファイルに目次を追加する方法を学びます。複雑なレポート、電子書籍、ビジネス提案書など、どんな文書でも目次があれば、プロフェッショナルで読みやすい傑作に生まれ変わります。

## 前提条件

コードに進む前に、必要なものがすべて揃っていることを確認しましょう。

1. Aspose.PDF for .NET: Aspose.PDFライブラリをダウンロードしてインストールしてください。ダウンロードはこちらから。 [ここ](https://releases。aspose.com/pdf/net/).
   
2. 開発環境: マシンに Visual Studio などの .NET 開発環境が設定されていることを確認します。

3. ライセンス: ライセンスをお持ちでない場合は、無料トライアルを受けるか、一時ライセンスをリクエストできます。 [ここ](https://purchase。aspose.com/temporary-license/).

## パッケージのインポート

まず、コードファイルの先頭に必要な名前空間をインポートしてください。手順は以下のとおりです。

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

これらの名前空間を使用すると、PDF 固有の機能にアクセスし、ドキュメント内のテキスト要素を操作できます。

このタスクを簡単なステップに分けてみましょう。各ステップでは、PDFドキュメントに目次を作成して挿入するプロセスを順を追って説明します。

## ステップ1: PDFドキュメントを読み込む

最初に、目次を追加する既存の PDF ファイルを読み込む必要があります。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document(dataDir + "AddTOC.pdf");
```

このステップでは、ドキュメントディレクトリへのパスを指定し、 `Document` オブジェクト。必ず置き換えてください `"YOUR DOCUMENT DIRECTORY"` ファイルへの実際のパスを入力します。

## ステップ2: TOC用の新しいページを挿入する

次に、PDFドキュメントの先頭に新しいページを挿入します。このページに目次を配置します。

```csharp
Page tocPage = doc.Pages.Insert(1);
```

TOC ページを先頭に挿入することで、読者が PDF で最初に目にするページとして TOC ページが表示されるようになります。

## ステップ3: TOC情報オブジェクトを作成する

それでは、目次情報を表すオブジェクトを作成しましょう。また、目次を目立たせるためにタイトルも追加します。

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocPage.TocInfo = tocInfo;
```

ここでは、TOC のタイトルを「Table Of Contents」に設定し、フォント サイズを大きくし、強調するために太字にしました。

## ステップ4: TOC要素を定義する

このステップでは、目次に表示される要素（または見出し）を定義します。これらの要素は、読者がドキュメント内の特定のセクションに移動するのに役立ちます。

```csharp
string[] titles = new string[4];
titles[0] = "First page";
titles[1] = "Second page";
titles[2] = "Third page";
titles[3] = "Fourth page";
```

PDF 内のさまざまなページに対応する TOC 項目として機能する文字列の配列を作成しました。

## ステップ5: 目次の見出しを作成する

ここで重要な部分、つまり目次に見出しを追加し、それぞれのページにリンクする作業が始まります。

```csharp
for (int i = 0; i < 2; i++)
{
    Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
    TextSegment segment2 = new TextSegment();
    heading2.TocPage = tocPage;
    heading2.Segments.Add(segment2);

    heading2.DestinationPage = doc.Pages[i + 2];
    heading2.Top = doc.Pages[i + 2].Rect.Height;
    segment2.Text = titles[i];

    tocPage.Paragraphs.Add(heading2);
}
```

何が起こっているかは以下のとおりです:
- 見出し: 私たちは `Heading` オブジェクトを追加して `TextSegment` それに。
- リンク先ページ: 各見出しがリンクするページを設定します。
- 上部の位置: 見出しが指すページ上の位置を指定します。
- テキスト: 各見出しは、先ほど作成した配列からそれぞれのタイトルを取得します。

このループは、目次の最初の 2 つの要素の見出しを作成し、対応するページにリンクします。

## ステップ6: TOC付きのPDFを保存する

最後に、すべての TOC 要素を追加したら、更新された PDF を保存します。

```csharp
dataDir = dataDir + "TOC_out.pdf";
doc.Save(dataDir);
```

PDFに目次が追加された状態でファイルが保存されました。おめでとうございます！これで目次の追加が完了しました。

## ステップ7: 確認メッセージ

プロセスが完了したことをユーザーに知らせるために、コンソールに簡単なメッセージを表示します。

```csharp
Console.WriteLine("\nTOC added successfully to an existing PDF.\nFile saved at " + dataDir);
```

## 結論

これで完了です！Aspose.PDF for .NETを使えば、PDFに目次を追加するのは簡単、しかもカスタマイズも自在です。シンプルなナビゲーションリンクの作成から複雑な構造の作成まで、このツールが全てをカバーします。次回、長文のPDFを作成する際は、プロフェッショナルな仕上がりのために目次を追加しましょう！

## よくある質問

### Aspose.PDF で TOC の外観をカスタマイズできますか?  
はい、フォント スタイル、サイズ、配置など、目次の外観を完全にカスタマイズできます。

### TOC にサブ見出しを追加するにはどうすればよいですか?  
サブ見出しを追加するには、 `Heading` レベル（例： `Heading(2)`) をクリックして、階層的な目次を作成します。

### ドキュメントが変更された場合に目次を自動的に更新することは可能ですか?  
いいえ、目次は自動更新されません。ドキュメント構造が変更された場合は、目次を再作成する必要があります。

### TOC エントリを外部ドキュメントにリンクできますか?  
はい、ハイパーリンクを使用して TOC エントリを外部の PDF または URL にリンクできます。

### Aspose.PDF は複数レベルの TOC をサポートしていますか?  
はい、Aspose.PDF は、サブセクションを含む複雑なドキュメントの複数レベルの TOC をサポートしています。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}