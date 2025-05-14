---
"description": "Aspose.PDF for .NET を使用して PDF 内のテーブル行にスタイルを設定する方法をステップバイステップ ガイドで学習し、ドキュメントの書式設定を簡単に強化します。"
"linktitle": "スタイルテーブル行"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "スタイルテーブル行"
"url": "/ja/net/programming-with-tagged-pdf/style-table-row/"
"weight": 180
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# スタイルテーブル行

## 導入

構造化され、美しくフォーマットされたPDFドキュメントを作成するなら、Aspose.PDF for .NETが頼りになるソリューションです。レポートや請求書の自動化、動的な表の作成など、様々なスタイルで表をフォーマットすることが、洗練されたドキュメントの鍵となります。このチュートリアルでは、Aspose.PDF for .NETを使った表の行のスタイル設定について詳しく解説します。コーヒーを飲みながらの楽しい会話のように、ステップバイステップで丁寧に解説していきますので、ご安心ください。

## 前提条件

細かい話に入る前に、準備が整っているか確認しましょう。必要なものは以下のとおりです。

1. Aspose.PDF for .NET ライブラリ  
   まだお持ちでない場合は、こちらから入手してください。 [ここ](https://releases.aspose.com/pdf/net/)また、 [無料トライアル](https://releases.aspose.com/) 始めましょう。
2. 開発環境  
   Visual Studio またはお好みの C# IDE をセットアップします。.NET もインストールする必要がありますが、おそらく既にご存知だと思います。
3. C#と.NETの基礎知識  
   C#をしっかり理解していれば、このチュートリアルは簡単に理解できるでしょう。でもご安心ください。各ステップを詳しく説明します！

## パッケージのインポート

Aspose.PDF を使い始める前に、必要な名前空間をインポートする必要があります。C# プロジェクトに以下のコードを追加してください。

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

これらは、テーブルを作成してスタイル設定するために不可欠であり、もちろん、コンプライアンスのためにタグ付けされたコンテンツを操作するためにも不可欠です。

それでは、タスクを段階的に分解して、プロのようにテーブル行のスタイルを設定できるようにしましょう。

## ステップ1：新しいPDFドキュメントを作成する

まず最初に、新しいPDFドキュメントを作成しましょう。このドキュメントには、スタイル設定されたすべての表の行が含まれます。

```csharp
// ドキュメント ディレクトリへのパス。
string dataDir = "YOUR DOCUMENT DIRECTORY";

// ドキュメントを作成
Document document = new Document();
```

ここでは、単に新しい `Document` PDFファイルを表すオブジェクトです。出力ファイルを保存するディレクトリパスを必ず設定してください。

## ステップ2: タグ付けされたコンテンツを操作する

アクセシビリティを考慮したPDF構造化のために、タグ付きコンテンツを活用します。これにより、表などの構造化された要素を作成し、PDF/UAなどのアクセシビリティ標準に準拠させることができます。

```csharp
ITaggedContent taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example table row style");
taggedContent.SetLanguage("en-US");
```

ここでは、PDFのタグ付きコンテンツのタイトルと言語を設定しています。PDFに名前を付けて、どの言語で表示するかを指定するようなものです。

## ステップ3: テーブル構造を定義する

次に、これから作成する表の構造を定義しましょう。すべての表には、ヘッダー、本文、フッターが必要です。整理されたブログ記事とよく似ていますね。

```csharp
// ルート構造要素を取得する
StructureElement rootElement = taggedContent.RootElement;

// テーブル構造要素を作成する
TableElement tableElement = taggedContent.CreateTableElement();
rootElement.AppendChild(tableElement);
TableTHeadElement tableTHeadElement = tableElement.CreateTHead();
TableTBodyElement tableTBodyElement = tableElement.CreateTBody();
TableTFootElement tableTFootElement = tableElement.CreateTFoot();
```

ここで行っているのは、ヘッダー付きのテーブルを作成することです（`THead`）、 体 （`TBody`）、フッター（`TFoot`）。これらの要素が行を保持します。

## ステップ4: 表のヘッダー行を追加する

ヘッダーのない表は、タイトルのない本のようなものです。まずはデータの文脈を示すヘッダー行を作成しましょう。

```csharp
TableTRElement headTrElement = tableTHeadElement.CreateTR();
headTrElement.AlternativeText = "Head Row";
for (int colIndex = 0; colIndex < 3; colIndex++)
{
    TableTHElement thElement = headTrElement.CreateTH();
    thElement.SetText(String.Format("Head {0}", colIndex));
}
```

ここでは、ループして3つのヘッダーセルを追加します（`TableTHElement`）にそれぞれ説明文を添えてみました。簡単ですよね？

## ステップ5: スタイル設定されたボディ行を追加する

いよいよ楽しい作業、行のスタイル設定です！カスタムスタイルで7行を作成しましょう。背景色、境界線、パディング、テキストの配置を設定します。

```csharp
for (int rowIndex = 0; rowIndex < 7; rowIndex++)
{
    TableTRElement trElement = tableTBodyElement.CreateTR();
    trElement.AlternativeText = String.Format("Row {0}", rowIndex);
    trElement.BackgroundColor = Color.LightGoldenrodYellow;
    trElement.Border = new BorderInfo(BorderSide.All, 0.75F, Color.DarkGray);
    trElement.DefaultCellBorder = new BorderInfo(BorderSide.All, 0.50F, Color.Blue);
    trElement.MinRowHeight = 100.0;
    trElement.FixedRowHeight = 120.0;
    trElement.IsInNewPage = (rowIndex % 3 == 1);
    trElement.IsRowBroken = true;

    for (int colIndex = 0; colIndex < 3; colIndex++)
    {
        TableTDElement tdElement = trElement.CreateTD();
        tdElement.SetText(String.Format("Cell [{0}, {1}]", rowIndex, colIndex));
    }
}
```

- 背景色: プロフェッショナルでありながら温かみのある雰囲気を出すために、明るいゴールデンロッドの黄色を使用しました。
- 境界線: 各行には濃い灰色の外側の境界線と青いセル境界線が付けられ、シャープな外観になります。
- 高さとパディング: 行の高さが設定され、すっきりとした外観になるようにパディングが追加されます。
- ページ区切り: 表を読みやすくするために、1 行おきに新しいページが始まります。

## ステップ6: フッター行を追加する

ヘッダーと同様に、フッターは表の固定要素です。フッターを作成しましょう。

```csharp
TableTRElement footTrElement = tableTFootElement.CreateTR();
footTrElement.AlternativeText = "Foot Row";
for (int colIndex = 0; colIndex < 3; colIndex++)
{
    TableTDElement tdElement = footTrElement.CreateTD();
    tdElement.SetText(String.Format("Foot {0}", colIndex));
}
```

3つのフッターセルをループして、少しテキストを追加するだけです。フッターの代替テキストは「Foot Row」に設定し、アクセシビリティを高めています。

## ステップ7: PDFドキュメントを保存する

テーブルのセッティングが完了したら、傑作を保存する時間です。

```csharp
document.Save(dataDir + "StyleTableRow.pdf");
```

このように、スタイルを設定した美しいテーブル行がすべて含まれた PDF が保存されます。

## ステップ8: PDF/UA準拠の検証

当社の PDF がアクセシビリティ標準に準拠していることを確認するために、PDF/UA 準拠を検証します。

```csharp
document = new Document(dataDir + "StyleTableRow.pdf");
bool isPdfUaCompliance = document.Validate(dataDir + "StyleTableRow.xml", PdfFormat.PDF_UA_1);
Console.WriteLine(String.Format("PDF/UA compliance: {0}", isPdfUaCompliance));
```

これにより、PDFがPDF/UA標準に準拠し、誰もがアクセスできるようになります。アクセシビリティこそが重要です！

## 結論

これで完了です！わずか数行のコードで、Aspose.PDF for .NET を使ってPDFに完全にスタイル設定された表を作成できました。ヘッダーからフッターまで、各行にスタイルを設定し、アクセシビリティ要素を追加し、ドキュメントのコンプライアンス検証も行いました。企業レポートやプレゼンテーションを作成する場合でも、単にPDFで楽しむ場合でも、このガイドが役立ちます。さあ、プロのように表にスタイルを設定してみましょう！

## よくある質問

### 表のフォントスタイルも変更できますか?  
はい！フォントスタイルは、 `TextState` 各セルにオブジェクトがあり、完全なカスタマイズが可能です。

### テーブルに列を追加するにはどうすればよいですか?  
調整するだけです `colCount` 変数を追加し、ループ内にヘッダー、本文、フッターのセルを追加します。

### 行の高さを設定しないとどうなりますか?  
行の高さを設定しない場合、テーブルはコンテンツに基づいて自動的に調整されます。

### これを動的な行数に使用できますか?  
もちろんです！データベースやその他のソースからデータを取得し、行数と列数を動的に調整できます。

### Aspose.PDF for .NET は無料で使用できますか?  
Aspose.PDF for .NETはライセンス製品ですが、 [無料トライアル](https://releases.aspose.com/) または [一時ライセンス](https://purchase。aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}