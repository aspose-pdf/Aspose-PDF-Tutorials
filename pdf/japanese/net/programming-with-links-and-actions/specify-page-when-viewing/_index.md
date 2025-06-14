---
"description": "Aspose.PDF for .NET を使用して、PDF で表示するページを指定する方法を学びます。このシンプルなガイドで、ユーザーナビゲーションを強化しましょう。"
"linktitle": "閲覧時にページを指定"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "閲覧時にページを指定"
"url": "/ja/net/programming-with-links-and-actions/specify-page-when-viewing/"
"weight": 110
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 閲覧時にページを指定

## 導入

PDFアプリケーションを拡張し、ドキュメントを開いた際にユーザーを特定のページへ誘導したいとお考えですか？まさにうってつけのガイドです！このガイドでは、Aspose.PDF for .NETを使ってPDFを開いた際に表示するページを指定する方法について詳しく説明します。この機能は、特にドキュメントの重要なセクションに注目を集める必要がある場合、ユーザーエクスペリエンスを大幅に向上させることができます。

## 前提条件

コーディングを始める前に、必要なものがすべて揃っていることを確認しましょう。必要なものは以下のとおりです。

1. .NETの基礎知識：.NETフレームワークの知識は必須です。C#を使いこなせ、オブジェクト指向プログラミングの基礎知識があれば、問題ありません。

2. Aspose.PDF for .NET: プロジェクトにAspose.PDFライブラリがインストールされている必要があります。まだインストールしていない場合は、ダウンロードできます。 [ここ](https://releases。aspose.com/pdf/net/).

3. Visual Studio: このチュートリアルでは、IDEとしてVisual Studioを使用していることを前提としています。お使いのマシンにVisual Studioがインストールされていることを確認してください。

4. PDFファイル：作業に使用する既存のPDFファイルが必要です。お持ちでない場合は、サンプルドキュメントを作成するか、お好きなPDFファイルを使用してください。

これらの前提条件が整ったら、すぐにコーディングを開始できます。

## パッケージのインポート

準備が整ったので、必要なパッケージをプロジェクトにインポートしましょう。以下の手順に従ってください。

### Visual Studioを起動する

Visual Studio を開き、PDF ページ表示機能を実装する新しいプロジェクトを作成するか、既存のプロジェクトを読み込みます。

### Aspose.PDF を参照

Aspose.PDF ライブラリを使用するには、ライブラリへの参照を追加する必要があります。

1. ソリューション エクスプローラーでプロジェクトを右クリックします。
2. 「NuGet パッケージの管理」を選択します。
3. 検索する `Aspose.PDF` パッケージをインストールします。

### 名前空間のインポート

コード ファイルの先頭に次の using ディレクティブを追加します。

```csharp
using System;
using System.IO;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
```

これで、PDF ページ ナビゲーション ロジックの構築を開始する準備が整いました。

タスクを管理しやすいステップに分解してみましょう。PDFドキュメントを開き、表示時に表示する特定のページを指定し、更新されたドキュメントを保存するコードを作成します。 

## ステップ1: ドキュメントディレクトリを設定する

まず、ドキュメントへのパスを設定する必要があります。

```csharp
// ドキュメント ディレクトリへのパス。
string dataDir = "YOUR DOCUMENT DIRECTORY"; // ディレクトリに置き換えます
```

この行は、基本的にロードマップです。コードにPDFファイルの場所を指示します。 `YOUR DOCUMENT DIRECTORY` マシン上の実際のパスを入力します。

## ステップ2: PDFファイルを読み込む

次に、PDF ファイルをアプリケーションに読み込みます。

```csharp
// PDFファイルを読み込む
Document doc = new Document(dataDir + "SpecifyPageWhenViewing.pdf");
```

ここで起こっていることは、新しいインスタンスを作成しているということです `Document` PDFファイルへのパスを指定する際に、オブジェクトを使用します。テーブルの上に置いた本を開くようなイメージで考えてみてください。

## ステップ3：目的のページにアクセスする

次に、ドキュメントを開いたときに表示するページにアクセスします。

```csharp
// ドキュメントの2ページ目のインスタンスを取得する
Page page2 = doc.Pages[2]; // インデックスは1から始まることを覚えておいてください
```

ここでは、ドキュメントの2ページ目にアクセスしています。このコンテキストではページ番号は1から始まるので、2ページ目を参照する場合はインデックスに2を使用する必要があります。

## ステップ4: ズーム率を設定する

表示されるページのズーム レベルを調整できます。

```csharp
// 対象ページのズーム率を設定する変数を作成する
double zoom = 1; // 1は100%ズームを意味します
```

ズーム率を設定すると、ユーザーがページを開いた直後にページ全体が表示される割合を指定できます。値が1の場合、ページは100%のズーム率で表示されます。これは一般的に適切なデフォルトです。

## ステップ5: GoToActionインスタンスを作成する

ナビゲーション機能を使ってみましょう。

```csharp
// GoToActionインスタンスを作成する
GoToAction action = new GoToAction(doc.Pages[2]); 
```

このステップでは、 `GoToAction` これは基本的に、PDF 内の特定のポイント（この場合は 2 ページ目）に移動するアクションを表します。

## ステップ6: 目的地を定義する

次に、アクションがどこにつながるかを定義する必要があります。

```csharp
// 2ページ目へ
action.Destination = new XYZExplicitDestination(page2, 0, page2.Rect.Height, zoom);
```

この行は、GoToActionのGPS目的地を設定するようなものです。ページ上部（高さ）と指定されたズームレベルで、ページ2に移動するように指示しています。

## ステップ7: 開くアクションを設定する

ドキュメントを開いたときにこのアクションが実行されることを確認しましょう。

```csharp
// ドキュメントを開くアクションを設定する
doc.OpenAction = action;
```

これで、PDFを開いたときに、先ほど定義したナビゲーションアクションが実行されるようになります。まるで、ドキュメントの玄関にウェルカムマットを敷いたようなものです。

## ステップ8: 更新したドキュメントを保存する

最後に、変更を加えたドキュメントを保存します。

```csharp
// 更新されたドキュメントを保存する
doc.Save(dataDir + "goto2page_out.pdf");
```

このステップで作業は完了です。新しいPDFファイルが作成されます。 `goto2page_out.pdf` 指定したページが直接開きます。

これでコーディング部分は完了です。PDF を開いたときに特定のページを表示するように Aspose.PDF をプログラムできました。 

## 結論

このガイドでは、Aspose.PDF for .NET を使用して PDF ファイル内のページを指定する方法を、ステップバイステップで解説します。この機能は、ユーザーの操作性を向上させるだけでなく、ドキュメント内の重要なコンテンツへの操作性も向上させます。これらの機能を活用することで、PDF アプリケーションを差別化できる、よりユーザーフレンドリーなエクスペリエンスを実現できます。

## よくある質問

### Aspose.PDF for .NET とは何ですか?
Aspose.PDF for .NET は、開発者が .NET アプリケーション内で PDF ドキュメントを作成、変更、管理できるようにするライブラリです。

### 表示するページを複数指定できますか？
いいえ、ドキュメントを特定の1ページで開くように設定することしかできません。ただし、異なる開始ページごとに異なるドキュメントを作成することは可能です。

### ページを異なるズームレベルで表示したい場合はどうすればよいでしょうか?
ズームレベルは、 `zoom` ドキュメントを保存する前に変数を設定します。

### Aspose.PDF の使用例をもっと知りたい場合は、どこに行けばよいですか?
確認するには [ドキュメント](https://reference.aspose.com/pdf/net/) さらなる例と機能については、こちらをご覧ください。

### Aspose.PDF for .NET の無料試用版はありますか?
はい！Aspose.PDFの無料トライアルをダウンロードできます。 [ここ](https://releases。aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}