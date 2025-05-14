---
"description": "このステップバイステップのチュートリアルでは、Aspose.PDF for .NET を使用してPDFに塗りつぶされた四角形を作成する方法を学びます。あらゆるレベルの開発者に最適です。"
"linktitle": "塗りつぶされた長方形を作成する"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "塗りつぶされた長方形を作成する"
"url": "/ja/net/programming-with-graphs/create-filled-rectangle/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 塗りつぶされた長方形を作成する

## 導入

見た目に美しいPDFをプログラムで作成したいと思ったことはありませんか？もしそうなら、まさにうってつけのチュートリアルです！このチュートリアルでは、PDFドキュメントを簡単に操作できる強力なライブラリ、Aspose.PDF for .NETの世界をご紹介します。今回は、PDFファイル内に塗りつぶされた四角形を作成する方法に焦点を当てます。経験豊富な開発者の方にも、初心者の方にも、このガイドは分かりやすく、各ステップを丁寧に解説します。さあ、コーディングの準備を始めましょう！

## 前提条件

コードに進む前に、準備しておく必要のあるものがいくつかあります。

1. Visual Studio: お使いのマシンにVisual Studioがインストールされていることを確認してください。Visual Studioは.NET開発に最適なIDEです。
2. Aspose.PDF for .NET: Aspose.PDFライブラリをダウンロードしてインストールする必要があります。 [ここ](https://releases。aspose.com/pdf/net/).
3. C# の基本知識: C# プログラミングに少し精通していると、コード スニペットをよりよく理解できるようになります。

## パッケージのインポート

まず、C#プロジェクトに必要なパッケージをインポートする必要があります。手順は以下のとおりです。

### 新しいプロジェクトを作成する

Visual Studioを開き、新しいC#プロジェクトを作成します。簡単にするために、コンソールアプリケーションを選択してください。

### Aspose.PDF 参照を追加する

1. ソリューション エクスプローラーでプロジェクトを右クリックします。
2. 「NuGet パッケージの管理」を選択します。
3. 「Aspose.PDF」を検索し、最新バージョンをインストールしてください。

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

すべての設定が完了したので、コードを見ていきましょう。

## ステップ1: ドキュメントディレクトリを設定する

まず最初に、PDFを保存するパスを指定する必要があります。これは、プログラムにファイルの作成場所を指示するため、非常に重要です。

```csharp
// ドキュメント ディレクトリへのパス。
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

交換する `"YOUR DOCUMENT DIRECTORY"` PDF を保存するマシン上の実際のパスを入力します。

## ステップ2: ドキュメントインスタンスを作成する

次に、 `Document` クラス。このクラスは、操作する PDF ドキュメントを表します。

```csharp
// ドキュメントインスタンスを作成する
Document doc = new Document();
```

この行は、操作できる新しい PDF ドキュメントを初期化します。

## ステップ3: ドキュメントにページを追加する

それでは、ドキュメントにページを追加しましょう。PDFには少なくとも1ページは必要ですよね？

```csharp
// PDFファイルのページコレクションにページを追加する
Page page = doc.Pages.Add();
```

このコードはドキュメントに新しいページを追加し、その上に図形を描画できるようにします。

## ステップ4: グラフインスタンスを作成する

図形を描くには、 `Graph` たとえば、グラフはさまざまな図形を描くことができるキャンバスだと考えてください。

```csharp
// グラフインスタンスを作成する
Aspose.Pdf.Drawing.Graph graph = new Aspose.Pdf.Drawing.Graph(100.0, 400.0);
```

ここでは、幅 100、高さ 400 のグラフを作成しています。

## ステップ5: ページにグラフを追加する

グラフが作成されたので、先ほど作成したページに追加しましょう。

```csharp
// ページインスタンスの段落コレクションにグラフオブジェクトを追加する
page.Paragraphs.Add(graph);
```

この行はグラフをページに添付し、描画できる状態にします。

## ステップ6: 長方形インスタンスを作成する

次に、色で塗りつぶす四角形を作成します。

```csharp
// 長方形インスタンスを作成する
Aspose.Pdf.Drawing.Rectangle rect = new Aspose.Pdf.Drawing.Rectangle(100, 100, 200, 120);
```

このコードでは、四角形の位置とサイズを定義します。パラメータは、x座標、y座標、幅、高さを表します。

## ステップ7: 塗りつぶしの色を指定する

それでは、長方形の色を選択しましょう。この例では赤で塗りつぶします。

```csharp
// グラフオブジェクトの塗りつぶし色を指定する
rect.GraphInfo.FillColor = Aspose.Pdf.Color.Red;
```

この行は、長方形の塗りつぶし色を赤に設定します。好きな色を選んでください。

## ステップ8: グラフに長方形を追加する

四角形の準備ができたら、それをグラフに追加します。

```csharp
// グラフオブジェクトの図形コレクションに長方形オブジェクトを追加します
graph.Shapes.Add(rect);
```

このコードはグラフに四角形を追加し、それを描画の一部にします。

## ステップ9: PDFドキュメントを保存する

最後に、ドキュメントを指定されたディレクトリに保存する必要があります。

```csharp
dataDir = dataDir + "CreateFilledRectangle_out.pdf";
// PDFファイルを保存する
doc.Save(dataDir);
```

このコードはPDFファイルを次の名前で保存します `CreateFilledRectangle_out.pdf` 先ほど指定したディレクトリにあります。

## ステップ10: 確認メッセージ

すべてがスムーズに進んだことを知らせるために、確認メッセージを印刷することができます。

```csharp
Console.WriteLine("\nFilled rectangle object created successfully.\nFile saved at " + dataDir);
```

この行は、塗りつぶされた四角形が正常に作成されたことを確認するメッセージをコンソールに出力します。

## 結論

これで完了です！Aspose.PDF for .NET を使って、PDF ドキュメントに塗りつぶされた四角形を作成できました。この強力なライブラリは、PDF 操作の可能性を広げ、プログラムで魅力的なドキュメントを作成できるようにします。レポート、請求書、その他あらゆる種類の PDF を作成する場合でも、Aspose.PDF がすべてをカバーします。

## よくある質問

### Aspose.PDF for .NET とは何ですか?
Aspose.PDF for .NET は、開発者がプログラムによって PDF ドキュメントを作成、操作、変換できるようにするライブラリです。

### Aspose.PDF は無料で使用できますか?
はい、Asposeはライブラリの機能を試すために無料の試用版を提供しています。ダウンロードできます。 [ここ](https://releases。aspose.com/).

### Aspose.PDF のサポートを受ける方法はありますか?
もちろんです！Asposeフォーラムでサポートを受けることができます。 [ここ](https://forum。aspose.com/c/pdf/10).

### Aspose.PDF を購入するにはどうすればよいですか?
Aspose.PDFは購入ページから購入できます。 [ここ](https://purchase。aspose.com/buy).

### Aspose.PDF ではどのような種類の図形を作成できますか?
Aspose.PDF ライブラリを使用すると、長方形、円、線など、さまざまな図形を作成できます。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}