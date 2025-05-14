---
"description": "Aspose.PDF for .NET を使用すると、PDF から開いているアクションを簡単に削除できます。効果的な PDF 管理のためのステップバイステップのガイドを含む簡単なチュートリアルです。"
"linktitle": "開いているアクションを削除"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "開いているアクションを削除"
"url": "/ja/net/programming-with-links-and-actions/remove-open-action/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 開いているアクションを削除

## 導入

このチュートリアルでは、Aspose.PDF for .NET を使用して PDF ドキュメントから開くアクションを削除するために必要な簡単な手順を解説します。その簡単さにきっと驚かれることでしょう。チュートリアルを終える頃には、PDF のプロになったような気分になれるはずです。それでは、前提条件を見ていきましょう。

## 前提条件

始める前に、いくつか準備しておく必要があります。

1. C# の基本的な理解: C# プログラミング言語に精通していると、コード スニペットを簡単に操作できるようになります。
2. Visual Studio: Visual Studioがインストールされていることを確認してください。これは.NET開発で最も一般的なIDEです。
3. Aspose.PDF for .NET: このライブラリが必要です。ダウンロードできます。 [ここ](https://releases。aspose.com/pdf/net/). 
4. .NET Framework: プロジェクトが .NET Framework を使用するように設定されていることを確認します (バージョン 4.0 以降を推奨)。
5. オープンアクションを含むPDFファイル：これが今回使用するドキュメントです。作成することも、練習用にサンプルをダウンロードすることもできます。

基礎が整えば、すぐに作業を開始できます。それでは、コーディングを開始するために必要なパッケージをインポートしましょう。

## パッケージのインポート

コーディングを始めるには、プロジェクトにいくつかの必須パッケージを追加する必要があります。これにより、PDFファイルに対して実行する操作の基礎が整います。必要な手順は以下のとおりです。

### プロジェクトを開く

操作を実行する .NET プロジェクトを Visual Studio で開きます。

### Aspose.PDF ライブラリを追加する

Aspose.PDFライブラリをプロジェクトに追加する必要があります。NuGetパッケージマネージャーを使えば簡単に追加できます。Aspose.PDFを検索し、最新の安定バージョンをインストールするだけです。

### 必要な名前空間を含める

C#ファイルの先頭で、Aspose.PDF名前空間をインポートする必要があります。これにより、コードにAsposeが提供するPDF機能を使用することを認識させます。追加する内容は以下のとおりです。

```csharp
using System.IO;
using Aspose.Pdf;
using System;
```

これですべての設定が完了し、準備が整いました。次は、PDF ドキュメントから開いているアクションを削除する具体的な手順について説明します。

## ステップ1: ドキュメントディレクトリを定義する

まず最初に、PDFファイルの保存場所を指定する必要があります。これはワークスペースの設定と考えていただければと思います。手順は以下のとおりです。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

必ず交換してください `"YOUR DOCUMENT DIRECTORY"` PDFが保存されている実際のパスに置き換えます。例:

```csharp
string dataDir = "C:\\Documents\\";
```

これにより、次のいくつかのステップの準備が整います。 

## ステップ2: PDFドキュメントを開く

次に、PDFドキュメントをアプリケーションに読み込みましょう。ここから魔法が始まります！以下のコードを使用してください。

```csharp
Document document = new Document(dataDir + "RemoveOpenAction.pdf");
```

このステップでは、アプリケーションに新しい `Document` オブジェクトは「RemoveOpenAction.pdf」という名前のPDFファイルを表します。このファイルが指定したディレクトリに存在することを確認してください。

## ステップ3: 開くアクションを削除する

いよいよ、ドキュメントから開くアクションを削除する番です。これはたった1行のコードで実行できます。やり方は以下のとおりです。

```csharp
document.OpenAction = null;
```

この行は、基本的にドキュメントに、開いているアクションセットがなくなったことを伝えます。つまり、PDFを保存する直前に、PDFを最初からやり直すようなものです。

## ステップ4: 更新したドキュメントを保存する

開くアクションを削除したら、変更を保存します。更新したドキュメントをディレクトリに保存する方法は次のとおりです。

```csharp
dataDir = dataDir + "RemoveOpenAction_out.pdf";
document.Save(dataDir);
```

このコードは、変更されたドキュメントを「RemoveOpenAction_out.pdf」という名前で同じディレクトリに保存します。つまり、不要なアクションが削除された新しいバージョンのPDFが作成されたことになります。

## ステップ5: 成功を確認する

操作が成功したことを全員に知らせるために、コンソールに確認メッセージを表示したい場合があります。次の行を追加するだけで、処理が完了です。

```csharp
Console.WriteLine("\nOpen action removed successfully.\nFile saved at " + dataDir);
```

この手順は厳密には必須ではありませんが、操作を実行した後に閉じておくと便利です。これで完了です！PDFドキュメントから開くアクションを削除できました。

## 結論

さあ、完成です！わずか数行のC#コードとAspose.PDF for .NETのパワーを活用すれば、PDFファイルを開くためのアクションを省き、作業効率を大幅に向上させることができます。ドキュメント管理は見た目ほど複雑ではありません。Asposeのようなツールを使いこなせば、PDFファイルを自在に操り、PDFファイルをより効率的に活用できるようになります。

## よくある質問

### PDF ファイル内のオープンアクションとは何ですか?
オープンアクションは、サウンドの再生や Web ページへの移動など、PDF を開いたときに実行されるコマンドです。

### Aspose.PDF for .NET には料金がかかりますか?
Asposeは無料トライアルを提供しています。ダウンロードできます。 [ここ](https://releases。aspose.com/).

### PDF から複数の開いているアクションを削除できますか?
はい、設定できます `OpenAction` 財産に `null` 開いているアクションをすべて削除します。

### オープンアクションの削除が機能したかどうかをテストするにはどうすればよいですか?
保存したPDFファイルを開き、事前に設定したアクションが実行されるか確認してください。実行されなければ成功です。

### 問題が発生した場合、どこでサポートを受けられますか?
PDF関連の問題のサポートについては、Asposeフォーラムをご覧ください。 [ここ](https://forum。aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}