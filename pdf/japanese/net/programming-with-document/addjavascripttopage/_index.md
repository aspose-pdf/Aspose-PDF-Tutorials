---
"description": "Aspose.PDF for .NET を使用して PDF ファイルに JavaScript を追加する方法を学びます。ドキュメントレベルおよびページレベルのスクリプト作成のためのコードチュートリアルを含むステップバイステップガイドです。"
"linktitle": "Java Script PDFファイルを追加する"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "PDFファイルにJava Scriptを追加する"
"url": "/ja/net/programming-with-document/addjavascripttopage/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDFファイルにJava Scriptを追加する

## 導入

ポップアップアラートや自動印刷機能といったインタラクティブな要素を使ってPDFをもっと魅力的にしたいと思ったことはありませんか？朗報です！実現可能です！Aspose.PDF for .NETを使えば、PDFドキュメントにJavaScriptをシームレスに追加できます。タスクの自動化やダイナミックなユーザーエクスペリエンスの構築など、PDFにJavaScriptを埋め込むことで、ファイルの機能性をさらに高めることができます。

## 前提条件

コーディング部分に進む前に、設定しておく必要のあるものがいくつかあります。

- Aspose.PDF for .NET: ライブラリをダウンロード [Aspose リリース](https://releases.aspose.com/pdf/net/) または [無料トライアル](https://releases。aspose.com/).
- 開発環境: Visual Studio などの .NET 互換 IDE。
- 基本的な C# の知識: このガイドでは、基本的な C# 構文に精通していることを前提としています。
- 一時ライセンス（オプション）： [一時ライセンス](https://purchase.aspose.com/temporary-license/) 開発中に制限を回避したい場合。

## パッケージのインポート

コードを書き始める前に、Aspose.PDFライブラリから必要な名前空間をインポートする必要があります。これらの名前空間を使用すると、PDFを操作したり、JavaScriptアクションを簡単に追加したりできるようになります。

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
```

適切な名前空間をインポートしたので、コーディングを開始する準備が整いました。

## ステップ1: 既存のPDFを読み込む

まず最初に、JavaScript を追加したい PDF ドキュメントを読み込む必要があります。このステップが、以降の変更の土台となります。例えば、PDF ドキュメントを開いたときに自動的に印刷するなど、動的な機能を追加したいとします。

PDF ファイルを読み込む方法は次のとおりです。

```csharp
// ドキュメント ディレクトリへのパス。
string dataDir = "YOUR DOCUMENT DIRECTORY";

// 既存のPDFファイルを読み込む
Document doc = new Document(dataDir + "input.pdf");
```

このコードスニペットでは、 `Document` 指定されたディレクトリから既存のPDFファイルを読み込むクラスです。 `"YOUR DOCUMENT DIRECTORY"` PDF ファイルへの実際のパスを入力します。

## ステップ2: ドキュメントレベルでJavaScriptを追加する

それでは、ドキュメントが開いたときに実行されるJavaScriptを追加しましょう。この例では、ユーザーがPDFを開いた瞬間に印刷ダイアログを開くスクリプトを作成します。

ドキュメントレベルのJavaScriptは、PDF全体に適用したいアクションに最適です。ドキュメント全体にグローバルルールを設定するようなものだと考えてください。

コードは次のとおりです:

```csharp
// ドキュメントレベルでのJavaScriptの追加
// 必要なJavaScriptステートメントでJavascriptActionをインスタンス化する
JavascriptAction javaScript = new JavascriptAction("this.print({bUI:true,bSilent:false,bShrinkToFit:true});");

// JavascriptActionオブジェクトをドキュメントのOpenActionに割り当てる
doc.OpenAction = javaScript;
```

このステップでは、 `JavascriptAction` ドキュメントを開いたときに印刷ダイアログを開くJavaScript関数を定義するオブジェクト。 `doc.OpenAction` 次に、この JavaScript アクションがプロパティに割り当てられます。

## ステップ3: ページレベルでJavaScriptを追加する

すべてのアクションがドキュメント全体に影響する必要はありません。特定のページを開いたり閉じたりするときに、特定のアクションを実行したい場合もあります。ここでは、特定のページ（例えばページ2）を開いたり閉じたりするときに実行されるJavaScriptアクションを設定します。

ページレベルのJavaScriptは、ターゲットを絞ったインタラクションに役立ちます。ユーザーがページに移動したときにメッセージを表示することから、フォームフィールドの自動入力などのカスタムアクションまで、あらゆる操作が可能です。

やり方は次のとおりです:

```csharp
// ページレベルでのJavaScriptの追加
doc.Pages[2].Actions.OnOpen = new JavascriptAction("app.alert('Page 2 opened')");
doc.Pages[2].Actions.OnClose = new JavascriptAction("app.alert('Page 2 closed')");
```

このコード スニペットでは、2 つの JavaScript アクションを追加します。
1. OnOpen アクション: ユーザーがページ 2 を開いたときに、「ページ 2 が開きました」というアラートを表示します。
2. OnClose アクション: ユーザーがページ 2 から移動したときに、「ページ 2 が閉じられました」というアラートを表示します。

これにより、PDFにインタラクティブなレイヤーが追加されます。ユーザーがページを開いたり離れたりする際にポップアップ通知が表示され、複数のページで一連の手順を案内する様子を想像してみてください。

## ステップ4: PDFドキュメントを保存する

これで、ドキュメント全体と特定のページの両方にJavaScriptが追加されました。最後のステップは、変更したPDFファイルを任意の場所に保存することです。この部分は簡単ですが非常に重要ですので、作業内容を保存することを忘れないでください。

コードは次のとおりです:

```csharp
// 出力ファイルのパスを指定する
dataDir = dataDir + "JavaScript-Added_out.pdf";

// 更新されたPDF文書を保存する
doc.Save(dataDir);

Console.WriteLine("\nJavaScript added successfully to the PDF.\nFile saved at " + dataDir);
```

このスニペットでは、JavaScriptを追加した更新されたドキュメントを、次の名前の新しいファイルに保存します。 `"JavaScript-Added_out.pdf"`これにより、元のファイルが上書きされることがなくなり、作業に使用できるバックアップが提供されます。

## 結論

Aspose.PDF for .NET を使用してPDFファイルにJavaScriptを追加すると、インタラクティブで動的なPDFを作成できます。印刷などのタスクの自動化やカスタムアラートの作成など、PDFにJavaScriptを埋め込むことで、ドキュメントの魅力と機能性をさらに高めることができます。

## よくある質問

### PDF 内の異なるページに複数の JavaScript アクションを追加できますか?
はい、個々のページまたはドキュメント全体に異なる JavaScript アクションを割り当てることができます。

### PDF に JavaScript を追加した後で削除することは可能ですか?
はい、既存のJavaScriptアクションを削除または変更するには、 `Actions` ドキュメントまたはページのプロパティ。

### PDF ではどのような JavaScript 関数を使用できますか?
印刷、アラート、フォーム操作など、Adobe Acrobat の JavaScript エンジンでサポートされている任意の JavaScript を使用できます。

### JavaScript はすべての PDF ビューアで動作しますか?
ほとんどのJavaScriptアクションは、Adobe AcrobatなどのインタラクティブPDFをサポートするPDFビューアで動作します。ただし、一部の基本的なPDFリーダーはJavaScriptをサポートしていない場合があります。

### PDF でのユーザー入力に基づいて JavaScript アクションをトリガーできますか?
はい、JavaScript をフォーム フィールドにバインドして、ユーザー入力に基づいてアクションをトリガーできます。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}