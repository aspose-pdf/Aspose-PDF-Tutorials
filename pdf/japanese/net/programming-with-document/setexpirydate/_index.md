---
"description": "Aspose.PDF for .NET を使用してPDFファイルに有効期限を設定する方法を学びましょう。このステップバイステップガイドでドキュメントのセキュリティを強化しましょう。"
"linktitle": "PDFファイルに有効期限を設定する"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "PDFファイルに有効期限を設定する"
"url": "/ja/net/programming-with-document/setexpirydate/"
"weight": 300
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDFファイルに有効期限を設定する

## 導入

今日のデジタル時代において、ドキュメントの管理とセキュリティ保護はこれまで以上に重要になっています。特定の日付を過ぎると自動的にアクセスできなくなるPDFファイルを送信するとしたらどうでしょう。まるで魔法のようですね。Aspose.PDF for .NETを使えば、PDFファイルに簡単に有効期限を設定できます。この機能は、特定の期間後にアクセスを制限する必要がある機密文書に特に役立ちます。このチュートリアルでは、PDFファイルに有効期限を設定するプロセスをステップバイステップで解説します。さあ、コーディングの準備を始めましょう！

## 前提条件

始める前に、いくつか準備しておくべきことがあります。

1. 開発環境：.NET開発環境がセットアップされていることを確認してください。Visual Studio、または.NETをサポートするその他のIDEが利用可能です。
2. Aspose.PDF for .NET: Aspose.PDFライブラリがインストールされている必要があります。まだインストールされていない場合は、こちらからダウンロードできます。 [ここ](https://releases。aspose.com/pdf/net/).
3. C#の基礎知識：このチュートリアルは、C#プログラミングの基礎知識があることを前提としています。C#を初めて使う方もご安心ください！シンプルで分かりやすい内容にしています。

## パッケージのインポート

Aspose.PDF を使い始めるには、C# プロジェクトに必要な名前空間をインポートする必要があります。手順は以下のとおりです。

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
```

これらの名前空間により、Aspose.PDF で PDF ドキュメントを操作するために必要なコア機能にアクセスできるようになります。

## ステップ1: ドキュメントディレクトリを設定する

まず最初に、ドキュメントディレクトリへのパスを指定する必要があります。出力PDFはここに保存されます。 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

交換する `"YOUR DOCUMENT DIRECTORY"` PDFファイルを保存する実際のパスを指定します。プログラムに「ここがファイルの保存場所だよ！」と指示するようなものです。

## ステップ2: Documentオブジェクトのインスタンス化

次に、 `Document` クラス。これがPDFを作成するキャンバスになります。

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
```

考えてみてください `Document` オブジェクトを白紙のように扱います。お好きなようにコンテンツを追加できます。

## ステップ3: PDFにページを追加する

ドキュメントの準備ができたら、次はページを追加しましょう。ここにコンテンツを配置します。

```csharp
doc.Pages.Add();
```

PDFに新しいページが作成されました。まるでノートに新しいページを追加して、考えを書き留めるのと同じです。

## ステップ4: ページにテキストを追加する

テキストを追加して、このページをもう少し面白くしてみましょう。シンプルな「Hello World」メッセージを追加します。

```csharp
doc.Pages[1].Paragraphs.Add(new TextFragment("Hello World..."));
```

このコード行は、PDFの最初のページにテキストフラグメントを追加します。ページの先頭にタイトルを書くようなものです。

## ステップ5: 有効期限のJavaScriptを作成する

いよいよ楽しいパートです！PDFの有効期限をチェックするJavaScriptアクションを作成します。現在の日付が有効期限を過ぎている場合は、ユーザーに警告メッセージが表示されます。

```csharp
JavascriptAction javaScript = new JavascriptAction(
"var year=2017;"
+ "var month=5;"
+ "today = new Date(); today = new Date(today.getFullYear(), today.getMonth());"
+ "expiry = new Date(year, month);"
+ "if (today.getTime() > expiry.getTime())"
+ "app.alert('The file is expired. You need a new one.');");
```

何が起こっているかは以下のとおりです:
- 有効期限の年と月を定義します。
- 今日の日付を取得します。
- 今日の日付と有効期限を比較します。
- 今日の日付が有効期限を過ぎている場合は、メッセージがポップアップ表示されます。

## ステップ6: JavaScriptをPDFオープンアクションとして設定する

次に、PDFドキュメントの開くアクションとしてJavaScriptアクションを設定する必要があります。これは、PDFが開かれるとすぐにJavaScriptが実行されることを意味します。

```csharp
doc.OpenAction = javaScript;
```

この行は、誰かがPDFを開いたときにJavaScriptを実行するように指示します。カレンダーを開いた瞬間にリマインダーが鳴る設定のようなものです。

## ステップ7: PDFドキュメントを保存する

最後に、有効期限機能を使用して PDF ドキュメントを保存します。 

```csharp
dataDir = dataDir + "SetExpiryDate_out.pdf";
doc.Save(dataDir);
```

この行は、PDFファイルを「SetExpiryDate_out.pdf」という名前で指定のディレクトリに保存します。まるで完成したアート作品を額縁に飾っているような気分です！

## 結論

これで完了です！Aspose.PDF for .NET を使って、有効期限付きの PDF ファイルを作成できました。この機能はセキュリティを強化するだけでなく、機密情報を安全に管理することにも役立ちます。契約書、レポート、その他の重要な文書を送信する場合、有効期限を設定することで状況は大きく変わります。

## よくある質問

### Aspose.PDF for .NET とは何ですか?
Aspose.PDF for .NET は、開発者が .NET アプリケーションで PDF ドキュメントを作成、操作、変換できるようにする強力なライブラリです。

### Aspose.PDF は無料で使用できますか?
はい、Aspose.PDFの無料試用版をご利用いただけます。ダウンロードしてご利用ください。 [ここ](https://releases。aspose.com/).

### Aspose.PDF を購入するにはどうすればよいですか?
Aspose.PDFを購入するには、 [購入ページ](https://purchase。aspose.com/buy).

### サポートが必要な場合はどうすればいいですか?
ご質問やサポートが必要な場合は、 [Aspose サポートフォーラム](https://forum。aspose.com/c/pdf/10).

### Aspose.PDF の一時ライセンスを取得できますか?
はい、一時ライセンスを申請できます [ここ](https://purchase。aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}