---
"description": "Aspose.PDF for .NET の GetDocumentWindow 機能を使用して、PDF ドキュメントのウィンドウ プロパティに関する情報を取得する方法を学習します。"
"linktitle": "ドキュメントウィンドウを取得"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "ドキュメントウィンドウを取得"
"url": "/ja/net/programming-with-document/getdocumentwindow/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ドキュメントウィンドウを取得

# 導入

PDFファイルを扱っていて、開いた時の表示をより細かく制御したいと思いませんか？メニューバーを非表示にしたり、ウィンドウを最初のページに合わせてサイズ変更したりと、Aspose.PDF for .NETには、ビューアでPDFファイルを開いた時の動作をカスタマイズするために必要なツールがすべて揃っています。このチュートリアルでは、Aspose.PDF for .NETでドキュメントウィンドウの設定を取得および操作する方法を詳しく説明します。


# 前提条件

チュートリアルに進む前に、次の前提条件が満たされていることを確認してください。

- 開発環境に Aspose.PDF for .NET がインストールされています。
  - [Aspose.PDF for .NET をダウンロード](https://releases.aspose.com/pdf/net/)
- Aspose.PDFの有効なライセンス、または [無料トライアル](https://releases.aspose.com/) または [一時ライセンス](https://purchase。aspose.com/temporary-license/).
- .NET と C# の基本的な理解。
- Visual Studio または他の適切な IDE。

# パッケージのインポート

コードを書き始める前に、必要なパッケージをインポートする必要があります。プロジェクトを開き、C#ファイルの先頭に次の名前空間を追加してください。

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

これにより、Aspose.PDF for .NET を使用して PDF ドキュメントを操作するために必要なすべてのクラスとメソッドにアクセスできるようになります。

それでは、さまざまなドキュメントウィンドウ設定を取得するプロセスを詳しく見ていきましょう。この例では、サンプルPDFファイルを使用します。 `GetDocumentWindow。pdf`.

## ステップ1: ドキュメントディレクトリのパスを設定する

まず最初に、PDFファイルへのパスを定義する必要があります。実行中にエラーが発生しないように、正しいファイルパスを設定することが重要です。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

ここで、 `"YOUR DOCUMENT DIRECTORY"` PDFファイルが実際に保存されているディレクトリに置き換えます。これは、PDF文書を読み込む作業ディレクトリです。

## ステップ2: PDFドキュメントを開く

ファイルパスが設定されたら、次はAspose.PDFを使ってPDFドキュメントを開きます。これによりドキュメントがメモリに読み込まれ、プロパティを取得できるようになります。

```csharp
Document pdfDocument = new Document(dataDir + "GetDocumentWindow.pdf");
```

この簡単なコード行で、PDFファイルを `pdfDocument` オブジェクトが作成され、そのすべてのプロパティにアクセスできるようになります。

## ステップ3: ウィンドウの中央揃えステータスを取得する

次に、ドキュメントウィンドウを開いたときに中央に配置するかどうかを確認します。デフォルト値は `false`。

```csharp
Console.WriteLine("CenterWindow : {0}", pdfDocument.CenterWindow);
```

出力が `true`の場合、ドキュメントウィンドウは画面の中央に表示されます。それ以外の場合は、デフォルトの位置に表示されます。

## ステップ4: テキストの方向を確認する

PDFの見た目においてもう一つ重要な要素は、テキストの方向です。テキストが左から右（L2R）に読み込まれるか、右から左（R2L）に読み込まれるかを決定します。この情報は、以下のコードで取得できます。

```csharp
Console.WriteLine("Direction : {0}", pdfDocument.Direction);
```

出力は次のようになります `L2R` 左から右へのテキストの場合 `R2L` 右から左に書くテキスト用です。この設定は、アラビア語やヘブライ語などの言語の文書に特に役立ちます。

## ステップ5: ウィンドウにドキュメントのタイトルを表示する

次のプロパティでは、ウィンドウのタイトルバーにドキュメントのタイトルを表示するかファイル名を表示するかを指定します。デフォルトでは、 `false`つまり、ファイル名が表示されます。

```csharp
Console.WriteLine("DisplayDocTitle : {0}", pdfDocument.DisplayDocTitle);
```

ファイル名の代わりにドキュメントのタイトルを表示する場合は、この設定を有効にする必要があります。

## ステップ6：最初のページに合わせてウィンドウのサイズを変更する

PDFを開いたときに、最初のページに合わせてドキュメントウィンドウのサイズを自動的に変更したい場合があります。この機能が有効になっているかどうかを確認する方法は次のとおりです。

```csharp
Console.WriteLine("FitWindow : {0}", pdfDocument.FitWindow);
```

デフォルトでは、 `false`つまり、最初のページのサイズに関係なく、ウィンドウのサイズはそのまま残ります。

## ステップ7: メニューバーを非表示にする

より集中して読みたい場合は、ビューアアプリケーションのメニューバーを非表示にすることをお勧めします。この設定は、次の行で取得できます。

```csharp
Console.WriteLine("HideMenuBar : {0}", pdfDocument.HideMenubar);
```

これは戻ってくる `true` メニューバーが非表示の場合、 `false` さもないと。

## ステップ8: ツールバーを非表示にする

同様に、PDFビューアのツールバーを非表示にして、ユーザーインターフェースをすっきりさせたい場合もあります。この設定は次のように取得できます。

```csharp
Console.WriteLine("HideToolBar : {0}", pdfDocument.HideToolBar);
```

この設定を有効にすると、PDF を開いたときにツールバーが非表示になります。

## ステップ9: スクロールバーとUI要素を非表示にする

スクロール バーなどの追加の UI 要素なしでページ コンテンツのみを表示する場合は、この設定でその動作を制御します。

```csharp
Console.WriteLine("HideWindowUI : {0}", pdfDocument.HideWindowUI);
```

に設定すると `true`、PDF ビューアではスクロール バーやその他のユーザー インターフェイス要素が非表示になり、ドキュメント コンテンツのみが表示されます。

## ステップ10: 非全画面ページモードを設定する

フルスクリーンモードを終了するときにドキュメントの表示方法を制御できます。 `NonFullScreenPageMode` プロパティ。この設定は、ユーザーが非フルスクリーンモードでドキュメントを操作する方法を定義するのに役立ちます。

```csharp
Console.WriteLine("NonFullScreenPageMode : {0}", pdfDocument.NonFullScreenPageMode);
```

出力は、サムネイル、アウトライン、添付ファイルパネルなどのさまざまなモードに設定できます。

## ステップ11: ページレイアウトを定義する

この設定では、ドキュメントのページのレイアウトを制御できます。例えば、単一ページ表示や連続列表示を選択できます。

```csharp
Console.WriteLine("PageLayout : {0}", pdfDocument.PageLayout);
```

これにより、ユーザーはドキュメントのコンテンツを柔軟に読み取ったり表示したりできるようになります。

## ステップ12: ページモードを指定する

最後に、 `PageMode` プロパティは、ドキュメントを開いたときにどのように表示するかを定義します。サムネイルの表示、全画面モードへの切り替え、添付ファイルパネルの表示などのオプションがあります。

```csharp
Console.WriteLine("PageMode : {0}", pdfDocument.PageMode);
```

ニーズに応じて、PDF の目的に合った任意のモードに設定できます。

## 結論

ご覧のとおり、Aspose.PDF for .NET は、様々な PDF ビューアで PDF ドキュメントの表示方法を調整するための包括的なツールを提供します。ツールバーを非表示にしたり、ウィンドウを中央に配置したり、テキストの方向を制御したりと、Aspose.PDF はユーザーの閲覧エクスペリエンスを向上させる柔軟性を提供します。

# よくある質問

### PDF の初期ズーム レベルをカスタマイズできますか?
はい、Aspose.PDF では、ドキュメントを開いたときにズーム レベルを設定できます。

### PDF のウィンドウ サイズをロックするにはどうすればよいですか?
設定できるのは `FitWindow` ウィンドウのサイズ変更を防止するプロパティ。

### Aspose.PDF はさまざまな読み取りモードをサポートしていますか?
はい、全画面、サムネイル、添付ファイルなどのさまざまなモードをサポートしています。

### PDF ビューアでスクロール バーを非表示にすることは可能ですか?
はい、スクロールバーを非表示にするには、 `HideWindowUI` 財産に `true`。

### ドキュメントウィンドウを開いたときに中央に配置できますか?
はい、設定することでこれを制御できます `CenterWindow` 財産。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}