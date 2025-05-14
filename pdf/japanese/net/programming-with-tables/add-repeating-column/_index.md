---
"description": "Aspose.PDF for .NET を使用して、PDF ドキュメントに繰り返し列を追加する方法を学びましょう。例とコードを使ったステップバイステップのガイドです。開発者に最適です。"
"linktitle": "PDF文書に繰り返し列を追加する"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "PDF文書に繰り返し列を追加する"
"url": "/ja/net/programming-with-tables/add-repeating-column/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF文書に繰り返し列を追加する

## 導入

PDFドキュメントで繰り返し列を追加する必要がある場合は、ここが最適な場所です！Aspose.PDF for .NETを使えば、PDF内の表やコンテンツを簡単に管理できます。動的なレポート、請求書、その他の構造化ドキュメントを作成する場合でも、繰り返し列はデータ整理の画期的なツールとなります。PDFドキュメントに繰り返し列を追加する方法をステップバイステップで解説します。

## 前提条件

コードに進む前に、すべてがセットアップされていることを確認しましょう。

- Aspose.PDF for .NET: プロジェクトに Aspose.PDF for .NET ライブラリがインストールされている必要があります。
- [Aspose.PDF for .NET をダウンロード](https://releases.aspose.com/pdf/net/)
- [無料トライアル](https://releases.aspose.com/)
- 開発環境: Visual Studio などの .NET 互換 IDE がインストールされていることを確認します。
- C# の基本的な理解: すべてを詳しく説明しますが、C# の基本的な理解があれば、スムーズに理解できるようになります。
  
Aspose.PDF for .NETをまだお持ちでない場合は、 [一時ライセンス](https://purchase.aspose.com/temporary-license/) 機能の探索を始めましょう。

## パッケージのインポート

まず、Aspose.PDF for .NET から必要な名前空間をインポートする必要があります。手順は以下のとおりです。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

これらのパッケージは、PDF ドキュメントの操作やテーブルの操作に必要な基本的なクラスとメソッドを提供します。

それでは、PDFドキュメントに繰り返し列を追加するプロセスを複数のステップに分解してみましょう。一緒にやってみましょう！

## ステップ1: ドキュメントディレクトリへのパスを設定する

ファイルを作成または操作する前に、生成されたPDFを保存するパスを定義する必要があります。C#プロジェクトで、ファイルを保存するディレクトリパスを設定します。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "AddRepeatingColumn_out.pdf";
```

このパスは、出力PDFが保存されるディレクトリを指します。 `"YOUR DOCUMENT DIRECTORY"` マシン上の実際のパスを入力します。

## ステップ2: 新しいPDFドキュメントを作成する

まず、新しいインスタンスを作成します `Document` オブジェクト。これは、PDF 内のすべてのページとコンテンツのコンテナとして機能します。

```csharp
Document doc = new Document();
Aspose.Pdf.Page page = doc.Pages.Add();
```

ここでは、新しいPDF文書を作成し、そこに空白ページを追加しました。 `doc.Pages.Add()` メソッドはドキュメントに新しいページを挿入します。

## ステップ3: 外部テーブルのインスタンス化

次に、外側の表を作成します。この表はページ全体の幅に広がり、繰り返し列を含む表を含む他の表のコンテナとして機能します。

```csharp
Aspose.Pdf.Table outerTable = new Aspose.Pdf.Table();
outerTable.ColumnWidths = "100%";
outerTable.HorizontalAlignment = HorizontalAlignment.Left;
```

私たちは、 `ColumnWidths` プロパティを「100%」に設定すると、表はページ全体の幅に広がります。

## ステップ4: 内部テーブルを作成する

では、繰り返し列を持つ内部テーブルを作成しましょう。ここで重要なプロパティは次のとおりです。 `Broken`これにより、表を同じページに継続することができ、 `ColumnAdjustment`コンテンツに合わせて列幅を自動的に調整します。

```csharp
Aspose.Pdf.Table mytable = new Aspose.Pdf.Table();
mytable.Broken = TableBroken.VerticalInSamePage;
mytable.ColumnAdjustment = ColumnAdjustment.AutoFitToContent;
```

この内部テーブルは外部テーブル内にネストされます。

## ステップ5: ページに表を追加する

外側の表と内側の表の両方が準備できたので、ページに追加しましょう。この手順により、表がドキュメントの構造に組み込まれます。

```csharp
page.Paragraphs.Add(outerTable);
var bodyRow = outerTable.Rows.Add();
var bodyCell = bodyRow.Cells.Add();
bodyCell.Paragraphs.Add(mytable);
mytable.RepeatingColumnsCount = 5;
```

ここでは、 `outerTable` ページに、そして外側のテーブルの中に、 `mytable`さらに、 `RepeatingColumnsCount` 5 に設定し、データが追加されたときに繰り返す列の数を指定します。

## ステップ6: ヘッダー行を追加する

次に、表にヘッダーを追加します。ヘッダー行はデータのコンテキストを示し、列の構造を整えるのに役立ちます。 

```csharp
Aspose.Pdf.Row row = mytable.Rows.Add();
row.Cells.Add("header 1");
row.Cells.Add("header 2");
row.Cells.Add("header 3");
row.Cells.Add("header 4");
row.Cells.Add("header 5");
row.Cells.Add("header 6");
row.Cells.Add("header 7");
row.Cells.Add("header 11");
row.Cells.Add("header 12");
row.Cells.Add("header 13");
row.Cells.Add("header 14");
row.Cells.Add("header 15");
row.Cells.Add("header 16");
row.Cells.Add("header 17");
```

このコード スニペットは、最初の行 (ヘッダーとして使用します) を追加し、「ヘッダー 1」、「ヘッダー 2」などのテキストを含むセルを入力します。

## ステップ7: データ行を追加する

最後に、表にデータを追加します。このループは動的に行を作成し、セルにコンテンツを入力します。

```csharp
for (int RowCounter = 0; RowCounter <= 5; RowCounter++)
{
    Aspose.Pdf.Row row1 = mytable.Rows.Add();
    row1.Cells.Add("col " + RowCounter.ToString() + ", 1");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 2");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 3");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 4");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 5");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 6");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 7");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 11");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 12");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 13");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 14");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 15");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 16");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 17");
}
```

ループは 6 回繰り返され、行が追加され、各セルが対応する列データ (例: 「col 1, 1」、「col 2, 2」など) で埋められます。

## ステップ8: ドキュメントを保存する

すべての行と列を追加したら、最後の手順として、ドキュメントを指定されたファイル パスに保存します。

```csharp
doc.Save(outFile);
```

ドキュメントは繰り返し列とともに保存されました。

## 結論

これで完了です！これらの簡単な手順で、Aspose.PDF for .NET を使って繰り返し列を含む PDF ドキュメントを作成できます。ネストされたテーブルの柔軟性を活用することで、複雑なレイアウトを実現し、PDF をプロフェッショナルで整理された印象に仕上げることができます。次のプロジェクトでぜひこのツールを試して、Aspose.PDF の潜在能力を存分に発揮し、PDF 生成のニーズに対応してください。

## よくある質問

### Aspose.PDF for .NET とは何ですか?
Aspose.PDF for .NET は、開発者がプログラムによって PDF ドキュメントを作成、編集、管理できるようにする強力なライブラリです。

### 繰り返し列の数を動的に調整できますか?
はい、繰り返し列の数を変更するには、 `RepeatingColumnsCount` 財産。

### Aspose.PDF for .NET にライセンスを適用するにはどうすればよいですか?
ファイルまたはストリームからライセンスを適用するには、 [ドキュメント](https://reference。aspose.com/pdf/net/).

### 表のセルに画像を追加することは可能ですか?
はい、Aspose.PDF for .NET は、画像を含むさまざまな種類のコンテンツをテーブル セルに追加することをサポートしています。

### テーブルレイアウトをさらにカスタマイズできますか?
もちろんです! Aspose.PDF には、境界線、パディング、配置など、表のスタイルをカスタマイズするための幅広い機能が備わっています。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}