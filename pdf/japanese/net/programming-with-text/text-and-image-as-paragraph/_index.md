---
"description": "Aspose.PDF for .NET を使用して、テキストと画像を含むPDFを作成します。テキストとインライン画像を追加する方法をステップバイステップで学びます。"
"linktitle": "PDFファイル内の段落としてのテキストと画像"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "PDFファイル内の段落としてのテキストと画像"
"url": "/ja/net/programming-with-text/text-and-image-as-paragraph/"
"weight": 530
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDFファイル内の段落としてのテキストと画像

## 導入

今日のデジタル世界において、PDFは私たちのほとんどが日常的に目にする普遍的なドキュメント形式です。レポート、電子書籍、請求書など、PDFを使えば様々なプラットフォーム間で情報を簡単に共有できます。しかし、PDFをプログラムでカスタマイズしたい場合はどうすればよいでしょうか？そこでAspose.PDF for .NETが役立ちます。このチュートリアルでは、Aspose.PDF for .NETを使って、PDFファイルにテキストや画像をインライン段落として挿入する方法を説明します。

## 前提条件

コードに進む前に、スムーズに理解するために必要なものがすべて揃っていることを確認しましょう。

- Aspose.PDF for .NETライブラリ：Aspose.PDF for .NETをインストールする必要があります。ダウンロードできます。 [ここ](https://releases。aspose.com/pdf/net/).
- Visual Studio: .NET をサポートするバージョンであれば、どれでも問題なく動作します。
- C# の基本的な理解: C# に多少精通していると役立ちますが、心配しないでください。すべての手順を説明します。
- PDF ドキュメントの準備: カスタム画像を追加する場合は、準備しておいてください。

ライブラリの無料トライアルもご利用いただけます [ここ](https://releases.aspose.com/)、または大規模なプロジェクトに取り組んでいる場合は、購入を検討してください [ここ](https://purchase.aspose.com/buy)さらに詳しい情報が必要な場合は、ドキュメントをご覧ください。 [ここ](https://reference。aspose.com/pdf/net/).

## パッケージのインポート

Aspose.PDF for .NET を使い始めるには、必要な名前空間をインポートする必要があります。これらの名前空間により、C# コードで Aspose.PDF の機能を操作できるようになります。

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System;
```

簡単ですよね？それでは、楽しい部分、つまり独自の PDF ファイルの作成に進みましょう。

## ステップバイステップガイド：テキストとインライン画像を含むPDFを作成する

これを分かりやすく、実行しやすいステップに分解してみましょう。パズルを組み立てているところを想像してみてください。それぞれのステップは、正しいピースを見つけてはめ込むようなものです。

## ステップ1: PDFドキュメントを初期化する

最初のステップは、Aspose.PDF を使用して新しい PDF ドキュメントを初期化することです。このドキュメントは、テキストや画像を追加するための基盤となります。

```csharp
// ドキュメント ディレクトリへのパス。
string dataDir = "YOUR DOCUMENT DIRECTORY";
// ドキュメントインスタンスをインスタンス化する
Document doc = new Document();
```

ここで何が起こっているのでしょうか？単に新しい文書を作成しているだけです。 `Document` クラスを作成し、PDFを保存するディレクトリを定義します。まるで傑作のための新しいキャンバスを開くようなものです！

## ステップ2：PDFにページを追加する

ページがないと文書はあまり役に立ちませんよね？文書に空白ページを追加してみましょう。

```csharp
// Documentインスタンスのページコレクションにページを追加する
Page page = doc.Pages.Add();
```

このコードスニペットは、ドキュメントのページコレクションに新しいページを追加します。ノートブックの空白ページを開くようなイメージです。

## ステップ3: 段落としてテキストを追加する

次に、テキスト段落を追加します。ここにメッセージや見出しを挿入します。

```csharp
// TextFragmentを作成する
TextFragment text = new TextFragment("Hello World.. ");
// Pageオブジェクトの段落コレクションにテキストフラグメントを追加する
page.Paragraphs.Add(text);
```

ここでは、 `TextFragment` 「Hello World..」というテキストを保持するオブジェクトを作成し、それを段落としてページに追加します。PDF文書の最初の文を書くようなものです。

## ステップ4: インライン段落として画像を追加する

テキストが完成したら、インライン段落として画像を追加して、より洗練されたデザインに仕上げましょう。インライン段落とは、Word文書で画像が表示されるのと同じように、画像がテキストの直後に表示されることを意味します。

```csharp
// 画像インスタンスを作成する
Aspose.Pdf.Image image = new Aspose.Pdf.Image();
// 画像をインライン段落として設定し、直後に表示されるようにする 
// 前の段落オブジェクト（TextFragment）
image.IsInLineParagraph = true;
// 画像ファイルのパスを指定する 
image.File = dataDir + "aspose-logo.jpg";
```

このスニペットでは、 `Image` オブジェクトを作成し、テキストとインラインで配置するように指示し、画像ファイルへのパスを指定します。これは、ドキュメント内の文の直後に画像を貼り付けるのと同じです。「aspose-logo.jpg」を任意の画像に置き換えることができます。

## ステップ5: 画像サイズを設定する（オプション）

画像のサイズを変更したいですか？問題ありません。Aspose.PDF では、ドキュメントに追加する前に画像の高さと幅を調整するオプションが用意されています。

```csharp
// 画像の高さを設定する（オプション）
image.FixHeight = 30;
// 画像の幅を設定する（オプション）
image.FixWidth = 100;
```

この部分はオプションですが、PDF内で画像がどの程度の大きさで表示されるかを制御するのに役立ちます。写真を印刷する前にサイズを変更するようなものです。

## ステップ6: 段落コレクションに画像を追加する

画像の準備ができました。次に、それをインライン段落としてドキュメントに挿入してみましょう。

```csharp
// ページオブジェクトの段落コレクションに画像を追加する
page.Paragraphs.Add(image);
```

この行は、段落コレクション内のテキストの直後に画像を追加します。テキストエディタで「画像を挿入」ボタンを押すのと同じです。

## ステップ7: 別のインラインテキスト段落を追加する

画像の直後にさらにテキストを追加したい場合はどうすればよいでしょうか。別のインラインテキストフラグメントを挿入してそれを実現してみましょう。

```csharp
// TextFragment オブジェクトを異なる内容で再初期化する
text = new TextFragment(" Hello Again..");
// TextFragment をインライン段落として設定する
text.IsInLineParagraph = true;
// 新しく作成した TextFragment をページの段落コレクションに追加します。
page.Paragraphs.Add(text);
```

再利用しています `TextFragment` ここに新しいテキスト（「Hello Again..」）を追加し、画像の直後にインラインで挿入します。これにより、PDFに流れるような統一感のある見た目が生まれます。

## ステップ8: PDFドキュメントを保存する

もうすぐ完了です！次に、指定したディレクトリにドキュメントを保存しましょう。

```csharp
dataDir = dataDir + "TextAndImageAsParagraph_out.pdf";
doc.Save(dataDir);
Console.WriteLine("\nText and image added successfully as inline paragraphs.\nFile saved at " + dataDir);
```

この最後のステップで、ファイルは「TextAndImageAsParagraph_out.pdf」という名前でディレクトリに保存されます。おめでとうございます。テキストとインライン画像の両方を含むPDFが作成されました。

## 結論

Aspose.PDF for .NET を使えば、テキストと画像をインライン段落として配置した PDF を簡単に作成できます。以下の手順に従うだけで、簡単に作成できます。わずか数行のコードで、PDF ファイルに動的なコンテンツを追加し、見た目も魅力的でプロフェッショナルな仕上がりにできます。ビジネスレポートでも電子書籍でも、PDF のレイアウトを自由にコントロールできれば、大きな違いが生まれます。

## よくある質問

### 複数の画像をインライン段落として追加できますか?  
はい、別々の画像を作成することで複数の画像を追加できます。 `Image` オブジェクトを段落コレクションに追加します。

### PDF 内のテキストと画像の位置を制御できますか?  
はい、余白などのプロパティを使用して、テキストと画像の正確な配置を制御できます。

### Aspose.PDF for .NET は無料ですか?  
いいえ、ライセンス製品ですが、 [無料トライアル](https://releases.aspose.com/) またはライセンスを購入する [ここ](https://purchase。aspose.com/buy).

### テキストにハイパーリンクを追加できますか?  
はい、Aspose.PDFではテキスト内にハイパーリンクを追加できます。 [ドキュメント](https://reference.aspose.com/pdf/net/) 詳細についてはこちらをご覧ください。

### テキストのフォントやスタイルをカスタマイズできますか?  
もちろんです！テキストフラグメントのフォント、色、その他のスタイルプロパティを簡単にカスタマイズできます。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}