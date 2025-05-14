---
"description": "Aspose.PDF for .NET を使用してHTMLをPDFに変換する方法をステップバイステップで解説します。ドキュメント生成を効率化したい開発者に最適です。"
"linktitle": "HTMLからPDFへの変換中に資格情報を提供する"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "HTMLからPDFへの変換中に資格情報を提供する"
"url": "/ja/net/document-conversion/provide-credentials-during-html-to-pdf/"
"weight": 240
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# HTMLからPDFへの変換中に資格情報を提供する

## 導入

ソフトウェア開発の世界では、HTMLからPDFへの変換はよくある要件です。レポート、請求書、その他のドキュメントを作成する場合でも、このタスクを処理する信頼できるライブラリがあれば、時間と労力を大幅に節約できます。そこで登場するのがAspose.PDF for .NETです。開発者がPDFドキュメントを簡単に作成、操作、変換できる強力なライブラリです。このチュートリアルでは、Aspose.PDFを使用して、安全なアクセスのための認証情報を提供しながら、HTMLからPDFに変換するプロセスを詳しく説明します。さあ、コーディングの準備を始めましょう！

## 前提条件

始める前に、いくつか準備しておくべきことがあります。

1. Visual Studio: お使いのマシンにVisual Studioがインストールされていることを確認してください。これが開発環境となります。
2. Aspose.PDF for .NET: ライブラリは以下からダウンロードできます。 [Webサイト](https://releases.aspose.com/pdf/net/)まずは試してみたいという方は、 [無料トライアル](https://releases。aspose.com/).
3. C# の基礎知識: C# プログラミングに精通していると、例をよりよく理解できるようになります。
4. インターネット アクセス: URL から HTML コンテンツを取得するため、インターネット接続が有効であることを確認してください。

## パッケージのインポート

Aspose.PDF を使い始めるには、必要なパッケージをプロジェクトにインポートする必要があります。手順は以下のとおりです。

1. Visual Studio プロジェクトを開きます。
2. ソリューション エクスプローラーでプロジェクトを右クリックし、「NuGet パッケージの管理」を選択します。
3. 「Aspose.PDF」を検索し、最新バージョンをインストールしてください。

```csharp
using System.IO;
using Aspose.Pdf;
using System;
using System.Net;
```
すべての設定が完了したので、資格情報を使用して HTML を PDF に変換するプロセスを管理しやすい手順に分解してみましょう。

## ステップ1: ドキュメントディレクトリを設定する

HTMLをPDFに変換する前に、出力PDFの保存場所を指定する必要があります。これは、ドキュメントディレクトリへのパスを定義することで行います。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

交換する `"YOUR DOCUMENT DIRECTORY"` PDFファイルを保存する実際のパスを指定します。デスクトップ上のフォルダでも、システム上の他の場所でも構いません。

## ステップ2: Webリクエストを作成する

次に、特定のURLからHTMLコンテンツを取得するためのリクエストを作成する必要があります。ここで `WebRequest` クラス。

```csharp
WebRequest request = WebRequest.Create("http://My.signchart.com/Report/PrintBook.asp?ProjectGuid=6FB9DBB0-");
```

ここでは、変換したいHTMLを含むURLへのリクエストを作成しています。URLは、実際に使用するURLに置き換えてください。

## ステップ3: 資格情報を設定する（必要な場合）

サーバーがコンテンツにアクセスするために認証情報を必要とする場合は、それを設定する必要があります。これは、 `CredentialCache。DefaultCredentials`.

```csharp
request.Credentials = CredentialCache.DefaultCredentials;
```

この行は、リクエストが現在のユーザーのデフォルトの認証情報を使用することを保証します。特定の認証情報を提供する必要がある場合は、新しい認証情報を作成できます。 `NetworkCredential` 物体。

## ステップ4: レスポンスを得る

リクエストの設定が完了したら、サーバーからの応答を取得します。

```csharp
HttpWebResponse response = (HttpWebResponse)request.GetResponse();
```

この行はリクエストを送信し、サーバーからの応答を待ちます。すべてがうまくいけば、必要なHTMLコンテンツが受信されます。

## ステップ5: レスポンスストリームを読み取る

レスポンスを受け取ったら、サーバーから返されたコンテンツを読み取る必要があります。これは、 `StreamReader`。

```csharp
Stream dataStream = response.GetResponseStream();
StreamReader reader = new StreamReader(dataStream);
string responseFromServer = reader.ReadToEnd();
reader.Close();
dataStream.Close();
response.Close();
```

ここでは、レスポンスストリームの内容全体を文字列変数に読み込みます。 `responseFromServer`リソースを解放するために、リーダーとストリームを閉じることを忘れないでください。

## ステップ6: HTMLをPDFに変換する

いよいよ面白い部分です！Aspose.PDF を使用して HTML コンテンツを PDF ドキュメントに変換します。

```csharp
MemoryStream stream = new MemoryStream(System.Text.Encoding.UTF8.GetBytes(responseFromServer));
HtmlLoadOptions options = new HtmlLoadOptions("http://My.signchart.com/");
options.ExternalResourcesCredentials = CredentialCache.DefaultCredentials;

Document pdfDocument = new Document(stream, options);
```

このステップでは、 `MemoryStream` HTMLコンテンツから設定 `HtmlLoadOptions`これにより、HTML が参照する可能性のある外部リソース (画像やスタイルシートなど) のベース URL を指定できます。

## ステップ7: PDFドキュメントを保存する

最後に、生成された PDF ドキュメントを指定されたディレクトリに保存する必要があります。

```csharp
pdfDocument.Save(dataDir + "ProvideCredentialsDuringHTMLToPDF_out.pdf");
```

この行はPDFファイルを次の名前で保存します `ProvideCredentialsDuringHTMLToPDF_out.pdf` 先ほど指定したディレクトリにあります。

## 結論

これで完了です！Aspose.PDF for .NET を使って、安全なアクセスのための認証情報を提供しながら、HTML を PDF に変換できました。この強力なライブラリを使えば、PDF ドキュメントを簡単に操作でき、わずか数行のコードで HTML コンテンツからプロフェッショナルな PDF を生成できます。 

## よくある質問

### Aspose.PDF for .NET とは何ですか?
Aspose.PDF for .NET は、開発者が .NET アプリケーションで PDF ドキュメントを作成、操作、変換できるようにするライブラリです。

### Aspose.PDF をインストールするにはどうすればよいですか?
Aspose.PDFはVisual StudioのNuGetパッケージマネージャーからインストールするか、 [Webサイト](https://releases。aspose.com/pdf/net/).

### Aspose.PDF は無料で使用できますか?
はい、Aspose では、購入前にライブラリを評価できる無料試用版を提供しています。

### Aspose.PDF で作成できるドキュメントの種類は何ですか?
Aspose.PDF を使用すると、レポート、請求書、フォームなど、さまざまなドキュメントを作成できます。

### Aspose.PDF のサポートはどこで受けられますか?
サポートを見つけたり質問したりできます [Aspose サポートフォーラム](https://forum。aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}