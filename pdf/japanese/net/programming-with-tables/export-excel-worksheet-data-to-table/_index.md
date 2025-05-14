---
"description": "Aspose.PDF for .NET を使用して、Excel ワークシートのデータを PDF テーブルにエクスポートする方法を学びます。コード例、前提条件、役立つヒントを含むステップバイステップのチュートリアルです。"
"linktitle": "Excel ワークシートのデータをテーブルにエクスポート"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "Excel ワークシートのデータをテーブルにエクスポート"
"url": "/ja/net/programming-with-tables/export-excel-worksheet-data-to-table/"
"weight": 70
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel ワークシートのデータをテーブルにエクスポート

## 導入

ExcelワークシートのデータをPDFファイルにエクスポートし、表形式で整理したいと思ったことはありませんか？Excelに大量のデータがあり、それをプロフェッショナルなPDFとして共有したいとしたらどうでしょう？複雑そうに思えるかもしれませんね。しかし、Aspose.PDF for .NETを使えば、この作業はあっという間に終わります。このチュートリアルでは、Aspose.PDF for .NETを使ってExcelワークシートのデータをPDFドキュメント内の表にエクスポートする手順を、ステップバイステップで丁寧に解説します。初めての方でも、最後まで使いこなせるようになるはずです。

## 前提条件

コーディングを始める前に、いくつかの準備をしておきましょう。

1. Aspose.PDF for .NETライブラリ – 最新バージョンがインストールされていることを確認してください。 [ここからダウンロード](https://releases。aspose.com/pdf/net/).
2. Aspose.Cells for .NET ライブラリ – Excelの操作に必要です。こちらからダウンロードしてください。 [ここ](https://releases。aspose.com/cells/net/).
3. .NET 開発環境 - Visual Studio のようなツールはコーディングに最適です。
4. Excel ファイル - エクスポートするデータを含む Excel ファイルを用意します。

Aspose.PDFとAspose.Cellsライブラリをお持ちでない場合は、 [無料トライアル](https://releases。aspose.com/).

## パッケージのインポート

まず、プロジェクトにAspose.PDFライブラリとAspose.Cellsライブラリの両方がインストールされていることを確認してください。Visual StudioのNuGetパッケージマネージャーを使用してインストールできます。

C# コードに必要なパッケージをインポートする方法は次のとおりです。

```csharp
using System.Data;
using System.IO;
using System.Linq;
```

前提条件が設定されたので、Excel シートから PDF ドキュメント内のテーブルにデータをエクスポートするプロセスを説明しましょう。

## ステップ1: Excelブックを読み込む

まず、Excelブックをプログラムに読み込む必要があります。このステップでは、Aspose.Cellsを使ってExcelファイルを開きます。

```csharp
// ドキュメント ディレクトリへのパス。
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Excelブックを読み込む
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(new FileStream(dataDir + "newBook1.xlsx", FileMode.Open));
```

説明: ここでは、Excelファイルが保存されているディレクトリパスを指定し、次の方法でワークブックを読み込みます。 `Aspose.Cells.Workbook`必ず調整してください `"YOUR DOCUMENT DIRECTORY"` ファイルの場所を指定します。

## ステップ2: 最初のワークシートにアクセスする

ワークブックを読み込んだ後、データが保存されている最初のワークシートにアクセスする必要があります。

```csharp
// Excelファイルの最初のワークシートにアクセスする
Aspose.Cells.Worksheet worksheet = workbook.Worksheets[0];
```

説明: この手順は簡単です。エクスポートするデータが含まれている最初のワークシートをワークブックから取得します。

## ステップ3: DataTableにデータをエクスポートする

ここで、Excel シートから DataTable オブジェクトにデータをエクスポートします。このオブジェクトは、データを PDF に転送するための仲介役として機能します。

```csharp
// 1番目のセルから7行2列の内容をDataTableにエクスポートする
DataTable dataTable = worksheet.Cells.ExportDataTable(0, 0, worksheet.Cells.MaxRow + 1, worksheet.Cells.MaxColumn + 1, true);
```

説明: `ExportDataTable` このメソッドは、ワークシートの最初のセルからすべての行と列にわたるデータを抽出します。このデータは、 `DataTable` 今後の使用のために。

## ステップ4：新しいPDFドキュメントを作成する

次に、Aspose.PDF を使用して新しい PDF ドキュメントを作成する必要があります。

```csharp
// ドキュメントインスタンスをインスタンス化する
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document();

// ドキュメントインスタンスにページを作成する
Aspose.Pdf.Page page = pdfDocument.Pages.Add();
```

説明: ここで、新しい `Aspose.Pdf.Document` そこにページを追加します。このページには、後でExcelデータから作成する表が含まれます。

## ステップ5: PDFで表オブジェクトを作成する

次に、PDF ドキュメント内に表を作成します。

```csharp
// テーブルオブジェクトを作成する
Aspose.Pdf.Table table = new Aspose.Pdf.Table();

// ページの段落コレクションに Table オブジェクトを追加します。
page.Paragraphs.Add(table);
```

説明: 私たちは `Aspose.Pdf.Table` オブジェクトを作成し、それをページの段落コレクションに追加します。これにより、テーブルがページに表示されるようになります。

## ステップ6: 列の幅と境界線を設定する

PDF内の表には列幅を定義する必要があります。また、表を読みやすくするために罫線を追加します。

```csharp
// 表の列幅を設定する
table.ColumnWidths = "40 100 100";

// デフォルトのセル境界線を設定する
table.DefaultCellBorder = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 0.1F);
```

説明: 3つの列の幅を設定し、すべてのセルにデフォルトの境界線を太さで設定します。 `0。1F`.

## ステップ7: DataTableからPDFテーブルにデータをインポートする

ここで、DataTable から PDF テーブルにデータをインポートします。

```csharp
// DataTableからTableオブジェクトにデータをインポートする
table.ImportDataTable(dataTable, true, 0, 0, dataTable.Rows.Count + 1, dataTable.Columns.Count);
```

説明: `ImportDataTable` このメソッドは、 `DataTable` PDFの表に追加します。これにより、Excelシートのデータが表に入力されます。

## ステップ8: ヘッダー行のスタイルを設定する

背景色、フォント、配置を変更して、表のヘッダー行のスタイルを設定しましょう。

```csharp
// テーブルから最初の行を取得する
Aspose.Pdf.Row headerRow = table.Rows[0];

// ヘッダー行のスタイルを設定する
foreach (Aspose.Pdf.Cell cell in headerRow.Cells)
{
    cell.BackgroundColor = Color.Blue;
    cell.DefaultCellTextState.Font = Aspose.Pdf.Text.FontRepository.FindFont("Helvetica-Oblique");
    cell.DefaultCellTextState.ForegroundColor = Color.Yellow;
    cell.DefaultCellTextState.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center;
}
```

説明: 最初の行 (ヘッダー) のすべてのセルをループし、背景色を青、テキスト色を黄色に設定し、テキストを中央に揃えます。

## ステップ9: 残りの行のスタイルを設定する

ヘッダーと残りの行を区別するために、残りの行に異なるスタイルを追加しましょう。

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++)
{
    foreach (Aspose.Pdf.Cell cell in table.Rows[i].Cells)
    {
        cell.BackgroundColor = Color.Gray;
        cell.DefaultCellTextState.ForegroundColor = Color.White;
    }
}
```

説明: ヘッダー以外のすべての行に対して、灰色の背景と白のテキスト色を設定します。

## ステップ10: PDFドキュメントを保存する

最後に、テーブルを含む PDF ドキュメントを保存します。

```csharp
// PDFを保存する
pdfDocument.Save(dataDir + "Exceldata_toPdf_table.pdf");
```

説明: PDFを指定されたディレクトリに保存します。これでExcelデータが美しくフォーマットされたPDFテーブルに保存されました。

## 結論

これで完了です！わずか数ステップで、Aspose.PDF for .NET を使って Excel ワークシートから PDF 内のテーブルにデータをエクスポートできました。プロセスを細かく分割し、途中でスタイルを設定することで、出力をカスタマイズし、データが整理されプロフェッショナルな印象を与えることができます。これで、次に誰かが Excel ファイルを渡して PDF レポートを要求した時、何をすればいいのかがすぐにわかるでしょう。

## よくある質問

### テーブルをさらにカスタマイズできますか?
もちろんです！色、フォント、配置を変更したり、特定のセルに境界線を追加したりすることもできます。

### Aspose.PDF for .NET は無料ですか?
無料トライアルを提供していますが、長期間使用するにはライセンスが必要です。 [ここから購入](https://purchase。aspose.com/buy).

### 特定の行と列のみをエクスポートできますか?
はい、パラメータを変更することができます `ExportDataTable` 特定の範囲をエクスポートする方法。

### これは大きな Excel ファイルでも機能しますか?
はい、Aspose.Cells は大きな Excel ファイルを効率的に処理できるように設計されています。

### PDF にページを追加するにはどうすればよいですか?
使用できます `pdfDocument.Pages.Add()` 必要な数だけページを追加できます。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}