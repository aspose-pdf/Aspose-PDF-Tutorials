---
"description": "Aspose.PDF for .NET を使って、PDF ファイルから画像を簡単に抽出する方法を学びましょう。このステップバイステップガイドに従って、PDF 処理スキルを向上させましょう。"
"linktitle": "PDFファイル内の画像を検索して取得する"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "PDFファイル内の画像を検索して取得する"
"url": "/ja/net/programming-with-images/search-and-get-images/"
"weight": 260
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDFファイル内の画像を検索して取得する

## 導入

Aspose.PDF for .NET を使ってPDFファイルから画像を簡単に抽出する方法をお探しですか？まさにうってつけです！この記事では、PDFドキュメントに埋め込まれた画像を効果的に検索・取得する方法を詳しく説明します。経験豊富な開発者の方でも、PDF操作の世界に足を踏み入れたばかりの方でも、このガイドは手順全体をステップバイステップで解説します。

## 前提条件

コードの細部に入る前に、リストにチェックを入れる必要のある前提条件がいくつかあります。 

### .NET フレームワーク

お使いのマシンに.NET Frameworkがインストールされていることを確認してください。Aspose.PDF for .NETはさまざまなバージョンと互換性がありますが、最新の機能と改善点をすべてご利用いただくには、最新の安定リリースをご利用いただくことをお勧めします。

### Aspose.PDF ライブラリ

Aspose.PDFライブラリへのアクセスが必要です。まだアクセスしていない場合は、こちらのリンクからダウンロードできます。 [Aspose.PDF for .NET をダウンロード](https://releases.aspose.com/pdf/net/)さらに、 [1ヶ月無料トライアル](https://releases.aspose.com/) 無料でプロジェクトを開始できます。

### 開発環境

コードをシームレスに記述して実行するには、Visual Studio などの適切な開発環境や、好みの IDE をセットアップする必要があります。

## パッケージのインポート

Aspose.PDF for .NET を使用するには、まずプロジェクトに適切な名前空間をインポートする必要があります。必要な手順は以下のとおりです。

```csharp
using System.IO;
using Aspose.Pdf;
using System;
```

これらのパッケージはそれぞれ、PDF文書を操作する際に特定の目的を果たします。 `Aspose.Pdf` 名前空間は操作の基礎であり、他の 2 つは PDF 内の画像とテキストの処理に役立ちます。

## ステップ1: ドキュメントパスを設定する

まず最初に、PDFファイルのパスを定義する必要があります。以下のコードで設定します。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

「YOUR DOCUMENT DIRECTORY」をPDFファイルを含むディレクトリへの実際のパスに置き換えます。例: `C:\Documents\`。

## ステップ2: PDFドキュメントを開く

次に、PDF文書をアプリケーションに読み込みます。これは、新しい `Document` 指定したファイル パスを持つインスタンスを作成します。

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document(dataDir + "SearchAndGetImages.pdf");
```

## ステップ3: ImagePlacementAbsorberを作成する

PDF内の画像を検索するには、 `ImagePlacementAbsorber` オブジェクト。このクラスは、抽出プロセス中にPDFから画像を吸収するのに役立ちます。

```csharp
ImagePlacementAbsorber abs = new ImagePlacementAbsorber();
```

## ステップ4：すべてのページでアブソーバーを受け入れる

このステップは、 `Document` すべてのページに画像吸収体を適用します。これにより、文書内のどこに配置した画像も確実に認識されます。

```csharp
doc.Pages.Accept(abs);
```

## ステップ5: 画像の配置をループする

画像を理解したら、次はそれらを詳しく見ていきましょう。PDFから抽出した各画像の配置をループで確認します。

```csharp
foreach (ImagePlacement imagePlacement in abs.ImagePlacements)
{
    // 画像のプロパティを取得するためのさらなる手順
}
```

## ステップ6: 画像のプロパティを抽出する

ループ内では、各画像に関する貴重なプロパティの取得を開始できます。 `imagePlacement` オブジェクトでは、寸法と解像度にアクセスできます。

```csharp
XImage image = imagePlacement.Image; // 画像を取得する

Console.Out.WriteLine("image width:" + imagePlacement.Rectangle.Width);
Console.Out.WriteLine("image height:" + imagePlacement.Rectangle.Height);
Console.Out.WriteLine("image LLX:" + imagePlacement.Rectangle.LLX);
Console.Out.WriteLine("image LLY:" + imagePlacement.Rectangle.LLY);
Console.Out.WriteLine("image horizontal resolution:" + imagePlacement.Resolution.X);
Console.Out.WriteLine("image vertical resolution:" + imagePlacement.Resolution.Y);
```

## 結論

これで完了です！これらの手順に従うことで、Aspose.PDF for .NET を使用してPDFファイルから画像を効率的に検索・取得できるようになります。わずか数行のコードで、貴重な画像とそのプロパティを抽出でき、アプリケーションの可能性を大きく広げることができます。

## よくある質問

### Aspose.PDF ライブラリは無料で使用できますか?  
Aspose.PDF for .NET は有料ライブラリですが、1 か月間の無料試用版をダウンロードできます。

### パスワードで保護された PDF ファイルから画像を抽出できますか?  
はい、ただし、ドキュメントを開くときにパスワードを入力する必要があります。

### PDF から抽出できる画像の種類は何ですか?  
形式（JPEG、PNGなど）に関係なく、埋め込まれたすべての画像を抽出できます。

### 抽出できる画像の数に制限はありますか?  
厳密な制限はなく、PDF ファイル自体によって異なります。

### 抽出した画像をディスクに保存できますか?  
はい、画像をディスクに保存するには、 `XImage` コード内のオブジェクト。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}