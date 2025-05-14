---
"description": "Aspose.PDF for .NET でテーブル要素を作成し、スタイルを設定する方法を、ステップバイステップの手順、カスタム スタイル、PDF/UA 準拠を使用して学習します。"
"linktitle": "スタイルテーブル要素"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "スタイルテーブル要素"
"url": "/ja/net/programming-with-tagged-pdf/style-table-element/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# スタイルテーブル要素

## 導入

この記事では、Aspose.PDF for .NET を使って表要素を作成し、スタイルを設定する方法を詳しく説明します。表の構造化、カスタムスタイルの適用、そしてドキュメントの PDF/UA 準拠の検証方法も学習します。このチュートリアルを終える頃には、PDF ファイルにプロフェッショナルな外観の表を簡単に作成できるようになります。

## 前提条件

チュートリアルに進む前に、次のものを用意しておく必要があります。

1. Visual Studio または同様の IDE がマシンにインストールされています。
2. アプリケーションを実行するための .NET Framework または .NET Core SDK。
3. Aspose.PDF for .NETライブラリをダウンロードし、プロジェクトで参照してください。最新バージョンは以下から入手できます。 [ここ](https://releases。aspose.com/pdf/net/).
4. 有効なAsposeライセンスまたは [一時ライセンス](https://purchase.aspose.com/temporary-license/) ライブラリの全機能を利用できるようになります。

## パッケージのインポート

まず、必要な名前空間をプロジェクトにインポートします。

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

これらの名前空間は、コア PDF 操作、タグ付きコンテンツ、表、およびテキスト書式設定をカバーします。

それでは、Aspose.PDF で表を作成し、スタイルを設定するプロセスを詳しく説明しましょう。各セクションを詳しく説明するので、理解しやすいでしょう。

## ステップ1: 新しいPDFドキュメントを作成し、タグ付きコンテンツを設定する

この最初のステップでは、空白の PDF ドキュメントを作成し、タグ付けされたコンテンツを設定します。

```csharp
// ドキュメント ディレクトリへのパス。
string dataDir = "YOUR DOCUMENT DIRECTORY";

// 新しいPDF文書を作成する
Document document = new Document();

// タグ付きコンテンツの設定
ITaggedContent taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example table style");
taggedContent.SetLanguage("en-US");
```

まず新しいものを作ることから始めます `Document` オブジェクトはPDFを表します。 `TaggedContent` オブジェクトはドキュメントの構造を管理し、アクセシビリティ標準への準拠を保証するために使用されます。適切なタグ付けのために、ドキュメントのタイトルと言語を設定します。

## ステップ2: ルート要素を定義する

次に、PDF 内のすべてのコンテンツのコンテナーとして機能するルート構造要素を作成します。

```csharp
// ルート構造要素を取得する
StructureElement rootElement = taggedContent.RootElement;
```

その `RootElement` 表を含むすべての構造化要素のベースコンテナとして機能します。文書の構造階層を維持するのに役立ち、整理とアクセシビリティの両方にとって重要です。

## ステップ3: 表要素を作成してスタイルを設定する

ルート要素が設定されたので、 `TableElement` 背景色、境界線、配置などのスタイルを適用します。

```csharp
// テーブル構造要素を作成する
TableElement tableElement = taggedContent.CreateTableElement();
rootElement.AppendChild(tableElement);

// テーブルをスタイリングする
tableElement.BackgroundColor = Color.Beige;
tableElement.Border = new BorderInfo(BorderSide.All, 0.80F, Color.Gray);
tableElement.Alignment = HorizontalAlignment.Center;
tableElement.Broken = TableBroken.Vertical;
tableElement.ColumnAdjustment = ColumnAdjustment.AutoFitToWindow;
```

私たちは `TableElement`はテーブル構造を定義します。 `BackgroundColor`、 `Border`、 そして `Alignment` プロパティを使用すると、テーブルの外観をカスタマイズできます。 `Broken` このプロパティにより、表がページをまたいで分割される場合、垂直方向に分割されることが保証されます。

## ステップ4: 表のサイズとセルのスタイルを設定する

このステップでは、列の数、セルのパディング、その他の重要なテーブル プロパティを定義します。

```csharp
tableElement.ColumnWidths = "80 80 80 80 80";
tableElement.DefaultCellBorder = new BorderInfo(BorderSide.All, 0.50F, Color.DarkBlue);
tableElement.DefaultCellPadding = new MarginInfo(16.0, 2.0, 8.0, 2.0);
tableElement.DefaultCellTextState.ForegroundColor = Color.DarkCyan;
tableElement.DefaultCellTextState.FontSize = 8F;
```

表の各列が均等に間隔を空けるように列幅を指定します。 `DefaultCellBorder`、 `DefaultCellPadding`、 そして `DefaultCellTextState` 境界線、パディング、テキストの色、フォント サイズなど、セルの既定のスタイルを定義します。

## ステップ5: 繰り返し行とカスタムスタイルを追加する

繰り返し行や、ヘッダーやフッターなどの他の特定のテーブル要素のスタイルを定義することもできます。

```csharp
tableElement.RepeatingRowsCount = 3;
TextState rowStyle = new TextState();
rowStyle.BackgroundColor = Color.LightCoral;
tableElement.RepeatingRowsStyle = rowStyle;
```

その `RepeatingRowsCount` 表が複数ページにまたがる場合、最初の3行が繰り返されるようにします。 `RepeatingRowsStyle` これらの行にカスタム背景色を適用します。

## ステップ6: 表のヘッダー、本体、フッター要素を追加する

次に、表のヘッダー、本文、フッターのセクションを作成し、コンテンツを入力します。

```csharp
TableTHeadElement tableTHeadElement = tableElement.CreateTHead();
TableTBodyElement tableTBodyElement = tableElement.CreateTBody();
TableTFootElement tableTFootElement = tableElement.CreateTFoot();

// ヘッダー行を作成する
TableTRElement headTrElement = tableTHeadElement.CreateTR();
headTrElement.AlternativeText = "Head Row";
for (int colIndex = 0; colIndex < 5; colIndex++)
{
    TableTHElement thElement = headTrElement.CreateTH();
    thElement.SetText($"Head {colIndex}");
}

// テーブル本体にデータを入力する
for (int rowIndex = 0; rowIndex < 10; rowIndex++)
{
    TableTRElement trElement = tableTBodyElement.CreateTR();
    for (int colIndex = 0; colIndex < 5; colIndex++)
    {
        TableTDElement tdElement = trElement.CreateTD();
        tdElement.SetText($"Cell [{rowIndex}, {colIndex}]");
    }
}
```

表は、ヘッド、ボディ、フッターの3つの部分に分かれています。まず、ヘッダー行を作成します。 `TableTHElement` 列見出しを追加します。そして、表の本体に以下のデータを入力します。 `TableTDElement`各セルにその位置を含むラベルを入力します。

## ステップ7: ドキュメントを保存する

最後に、PDF ドキュメントを指定されたディレクトリに保存します。

```csharp
// タグ付きPDF文書を保存する
document.Save(dataDir + "StyleTableElement.pdf");
```

この手順では、スタイル設定されたテーブルを含む PDF ファイルを保存して、ドキュメント作成プロセスを完了します。

## ステップ8: PDF/UA準拠の検証

ドキュメントを保存した後、PDF/UA (ユニバーサル アクセシビリティ) 標準に準拠していることを確認することが重要です。

```csharp
// PDF/UA準拠を確認する
document = new Document(dataDir + "StyleTableElement.pdf");
bool isPdfUaCompliance = document.Validate(dataDir + "StyleTableElement.xml", PdfFormat.PDF_UA_1);
Console.WriteLine($"PDF/UA compliance: {isPdfUaCompliance}");
```

ここでドキュメントを再読み込みし、PDF/UA標準に準拠しているか検証します。コンプライアンスにより、PDFがアクセシビリティ要件を満たし、幅広いユーザーに適したものになることが保証されます。

## 結論

Aspose.PDF for .NET を使えば、PDF ドキュメントに表を作成し、スタイルを設定するのが簡単かつ直感的です。このチュートリアルで説明する手順に従うことで、カスタマイズされたスタイルで表を作成し、PDF がアクセシビリティ基準を満たすようにすることができます。レポートを作成する場合でも、構造化されたドキュメントを作成する場合でも、表はデータをわかりやすく提示するための強力なツールです。

## よくある質問

### 表のセル内に画像を追加できますか?
はい、表のセルに画像を挿入するには、 `Image` 要素。

### 列幅を動的に調整するにはどうすればよいですか?
設定できるのは `ColumnAdjustment` 財産に `AutoFitToWindow` コンテンツに応じて列幅を自動的に調整します。

### すべてのドキュメントで PDF/UA 準拠が必須ですか?
必須ではありませんが、高いアクセシビリティ基準を必要とするドキュメントには推奨されます。

### 特定の行に異なるスタイルを適用できますか?
はい、個々の行やセルを調整することでカスタマイズできます。 `TextState` または `BackgroundColor`。

### タグ付けされたコンテンツを使用する利点は何ですか?
タグ付きコンテンツはドキュメントのアクセシビリティを向上させ、PDF/UA などの標準への準拠を確保するのに役立ちます。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}