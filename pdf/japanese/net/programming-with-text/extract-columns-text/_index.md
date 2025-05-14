---
"description": "Aspose.PDF for .NET を使用してPDFファイルからテキスト列を抽出する方法を学びましょう。このガイドでは、コード例と解説を用いて各ステップを詳しく説明します。"
"linktitle": "PDFファイル内の列テキストの抽出"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "PDFファイル内の列テキストの抽出"
"url": "/ja/net/programming-with-text/extract-columns-text/"
"weight": 150
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDFファイル内の列テキストの抽出

## 導入

PDFファイルで作業していて、特定の列形式でテキストを抽出したいとお考えですか？請求書、レポート、その他の構造化ドキュメントを処理する場合でも、PDFからテキストを正確に抽出するのは容易ではありません。Aspose.PDF for .NETを使えば、このプロセスを簡素化できます。このチュートリアルでは、PDFファイルから列形式のテキストを簡単に抽出する方法を詳しく説明します。 

## 前提条件

コードに進む前に、必要な基本的な事項について説明しましょう。

- Aspose.PDF for .NET: 最新バージョンのAspose.PDF for .NETがインストールされていることを確認してください。最新バージョンでない場合は、 [ここからダウンロード](https://releases。aspose.com/pdf/net/).
- 開発環境: コードを操作するには、Visual Studio または別の .NET 開発環境が必要です。
- PDF ドキュメント: サンプルの PDF ドキュメントを用意してください。できればテキストの列があるドキュメントが望ましいです。このドキュメントからテキストを抽出するからです。

Aspose.PDF for .NETをまだインストールしていない場合は、 [無料トライアル](https://releases.aspose.com/) または [ライセンスを購入する](https://purchase.aspose.com/buy) フル機能をご利用いただけます。 [一時ライセンス](https://purchase.aspose.com/temporary-license) 必要であれば。

## 名前空間のインポート

プロジェクトで Aspose.PDF for .NET を使用するには、次の名前空間をインポートする必要があります。

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

## ステップバイステップガイド: PDFからテキストの列を抽出する

それでは、コードの各部分を分解して、その仕組みをより深く理解しましょう。プロセスの各セグメントをステップごとに説明しながら、実際に見ていきましょう。

## ステップ1: PDFドキュメントを読み込む

まず最初にPDFファイルを読み込みます。 `Document` オブジェクトです。これが Aspose.PDF がドキュメントとやり取りする方法です。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document pdfDocument = new Document(dataDir + "ExtractTextPage.pdf");
```

このステップでは、PDF文書を保存するディレクトリを定義します。 `"YOUR DOCUMENT DIRECTORY"` ローカルPDFファイルへのパスを入力します。 `Document` オブジェクトは PDF をメモリに読み込み、さらに処理するためにアクセスできるようにします。

## ステップ2: テキストフラグメント吸収装置を設定する

次に、 `TextFragmentAbsorber` PDFファイルからすべてのテキストを吸収またはキャプチャします。このアブソーバークラスは、PDF内の特定の領域からテキストの断片を抽出するように設計されており、テキスト列の抽出に最適です。

```csharp
TextFragmentAbsorber tfa = new TextFragmentAbsorber();
pdfDocument.Pages.Accept(tfa);
TextFragmentCollection tfc = tfa.TextFragments;
```

ここでは、 `TextFragmentAbsorber` これをPDFの全ページに適用するには、 `Accept()`。その `TextFragmentCollection` 抽出されたテキストを保存し、このコレクションから必要に応じてテキストを操作または抽出できます。

## ステップ3: 抽出したテキストのフォントサイズを調整する

テキスト断片をキャプチャしたら、特に元のテキストが大きすぎる場合は、フォントサイズを縮小したい場合があります。この例では、フォントサイズを70%縮小しています。

```csharp
foreach (TextFragment tf in tfc)
{
    // フォントサイズを70%縮小
    tf.TextState.FontSize = tf.TextState.FontSize * 0.7f;
}
```

このコードは各 `TextFragment` コレクション内のテキストを抽出し、フォントサイズを70%縮小します。フォントサイズを調整すると、特に異なる目的に合わせて書式設定する場合に、抽出したテキストの管理が容易になります。

## ステップ4: ドキュメントをメモリストリームに保存する

テキストを変更した後、PDFを `MemoryStream`これにより、ドキュメントをディスクに書き戻すことなく、さらに処理するためにメモリ内に保持することができます。

```csharp
Stream st = new MemoryStream();
pdfDocument.Save(st);
pdfDocument = new Document(st);
```

ここでは、PDFをメモリストリームに保存し、ドキュメントを再読み込みします。この方法は、大きなファイルを扱っていて、不要なディスク操作を避けたい場合に便利です。

## ステップ5: Text Absorberを使用してすべてのテキストを抽出する

PDFの準備ができたので、次はテキストを抽出します。 `TextAbsorber` ドキュメントからすべてのテキストを取得します。

```csharp
TextAbsorber textAbsorber = new TextAbsorber();
pdfDocument.Pages.Accept(textAbsorber);
String extractedText = textAbsorber.Text;
```

このステップでは、 `TextAbsorber` PDFからすべてのテキストを吸収し、抽出されたテキストは `extractedText` 文字列。ここで魔法が起こります。テキスト列がプレーンテキスト形式になります。

## ステップ6: 抽出したテキストをファイルに保存する

最後に、抽出したテキストを `.txt` 簡単にアクセスして、さらに使用するためのファイルです。

```csharp
dataDir = dataDir + "ExtractColumnsText_out.txt";
System.IO.File.WriteAllText(dataDir, extractedText);
Console.WriteLine("\nColumns text extracted successfully from Pages of PDF Document.\nFile saved at " + dataDir);
```

このコードは抽出したテキストを新しい `.txt` ファイルをコピーし、指定したディレクトリに保存します。処理が成功したことを確認するメッセージがコンソールに表示されます。

## 結論

これで完了です！Aspose.PDF for .NET を使って PDF ファイルからテキスト列を抽出するのは、想像以上に簡単です。わずか数行のコードで、PDF を読み込み、特定のテキストを抽出し、書式を調整し、結果をテキストファイルに保存できます。

この手法は、表、レポート、列で構成されたコンテンツなどの構造化ドキュメントの処理に非常に役立ちます。データ抽出の自動化や大量のドキュメント処理など、Aspose.PDF はこれらを効率的に実行するためのツールを提供します。

## よくある質問

### PDF の特定のページからテキストを抽出できますか?  
はい！変更できます `TextFragmentAbsorber` 特定のページをターゲットにするには `pdfDocument.Pages[pageIndex].Accept(tfa);` 方法。

### 複数列の PDF で 1 つの列からのみテキストを抽出することは可能ですか?  
はい、ただしテキストフラグメントの座標を次のように操作する必要があります。 `TextFragment.Rectangle` ドキュメントの特定の領域をターゲットにします。

### テキスト抽出の精度を向上させるにはどうすればよいですか?  
精度を高めるには、PDFの構造が明確に定義されていることを確認し、複雑なレイアウトの文書は避けてください。また、 `TextFragmentAbsorber` フォント スタイル、サイズ、または領域に基づいてテキストを抽出します。

### Aspose.PDF はスキャンされたドキュメントからのテキスト抽出をサポートしていますか?  
はい、ただしOCR（光学文字認識）技術を使用する必要があります。Asposeにはそのためのツールも用意されています。

### 何千ページもの大きな PDF ファイルを処理するにはどうすればよいでしょうか?  
大きな PDF の場合、メモリ使用量の増加を避けるために、一度に数ページからテキストを抽出してドキュメントをチャンク単位で処理します。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}