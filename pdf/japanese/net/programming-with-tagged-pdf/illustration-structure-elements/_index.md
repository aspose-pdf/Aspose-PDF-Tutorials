---
"description": "ステップバイステップのチュートリアルに従って、Aspose.PDF for .NET でイラスト要素を含む構造化 PDF を作成します。"
"linktitle": "イラスト構造要素"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "イラスト構造要素"
"url": "/ja/net/programming-with-tagged-pdf/illustration-structure-elements/"
"weight": 100
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# イラスト構造要素

## 導入

.NETアプリケーションで、美しく構造化されたPDFを作成する準備はできていますか？コンテンツのタグ付けが必要なプロジェクトに取り組んでいる場合でも、PDFを次のレベルに引き上げたい場合でも、Aspose.PDF for .NETには、イラストの構造要素を扱うために必要なすべてのツールが備わっています。このチュートリアルでは、最も複雑な部分も明確に理解できるように、プロセスをステップバイステップで説明します。

## 前提条件

詳細に入る前に、スムーズに進めるために必要なものがすべて揃っていることを確認しましょう。

1. Aspose.PDF for .NET – Aspose.PDFライブラリがインストールされている必要があります。まだインストールされていない場合は、 [ここからダウンロード](https://releases.aspose.com/pdf/net/)まずは試してみたい方は、 [無料トライアル](https://releases。aspose.com/).
2. Visual Studio – C# でコーディングするため、Visual Studio または互換性のある IDE がインストールされていることを確認してください。
3. .NET Framework – Aspose.PDF for .NET と互換性のあるバージョンがあることを確認してください。
4. 一時ライセンス – Aspose.PDFは試用モードではいくつかの制限がありますので、 [一時ライセンス](https://purchase.aspose.com/temporary-license/) すべての機能のロックを解除します。

以上です！必要な名前空間をインポートしてコーディングを進めましょう。

## 名前空間のインポート

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

これが基礎です。これらの名前空間をインポートしないと、Aspose.PDF の機能を利用したり、タグ付き PDF コンテンツを処理したりすることはできません。それでは、手順を詳しく見ていきましょう。

## ステップ1: ドキュメントディレクトリの設定

PDFの作成を始める前に、ファイルを保存するドキュメントディレクトリへのパスを指定する必要があります。これは、画像やその他のアセットが保存されているシステム上のフォルダです。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

このステップはシンプルですが、非常に重要です。プログラムに、作業するファイルの場所と保存場所を指示することになります。PDFファイルのホームベースを作るようなものです。 `"YOUR DOCUMENT DIRECTORY"` マシン上の実際のパスを入力します。

## ステップ2: 新しいPDFドキュメントを作成する

さて、いよいよPDFドキュメントを作成します。このステップでは、空のPDFドキュメントを作成し、後続のステップで修正や拡張を行っていきます。
 ドキュメントを作成する

```csharp
Document document = new Document();
```

この行が魔法の働きをします。完全に空白の新しいPDFファイルを作成し、コンテンツを追加するのを待ちます。まるで新しいキャンバスを開くようなものだと考えてください。

## ステップ3: タグ付きPDFコンテンツへのアクセス

イラストの構造要素を扱うには、ドキュメントのタグ付きコンテンツを活用する必要があります。これにより、特定のタグを定義し、PDFの構造化とアクセシビリティを向上させることができます。

```csharp
ITaggedContent taggedContent = document.TaggedContent;
```

ここで魔法が起こるのです！ `TaggedContent` オブジェクトは、PDF内の要素がどのように解釈されるかを定義します。アクセシビリティや構造を扱う場合、このステップは非常に重要です。

## ステップ4: ドキュメントのタイトルと言語を設定する

構造化されたPDFを作成するため、タイトルと言語を定義することが不可欠です。これはアクセシビリティを向上させるだけでなく、ドキュメントをよりプロフェッショナルで検索しやすいものにします。

```csharp
taggedContent.SetTitle("Tagged Pdf Document");
taggedContent.SetLanguage("en-US");
```

タイトルと言語を指定することで、PDFに個性を与えることができます。タイトルはドキュメントのプロパティに表示され、言語を設定することでスクリーンリーダーやその他のアクセシビリティツールとの互換性が確保されます。

## ステップ5：イラスト（図）要素の作成

いよいよイラストを追加する、楽しいパートです！今回は、画像、代替テキストの説明、タイトルを含む図要素を作成します。

```csharp
IllustrationElement figure1 = taggedContent.CreateFigureElement();
taggedContent.RootElement.AppendChild(figure1);
```

このコードは新しい図要素を作成し、それをドキュメントのルート要素に追加します。これは、ドキュメントに画像プレースホルダーを追加するようなものです。

## ステップ6: 代替テキスト、タイトル、画像の追加

PDFのアクセシビリティを確保するため、イラストに代替テキストとタイトルを追加してください。画像も添付いたします。

```csharp
figure1.AlternativeText = "Figure One";
figure1.Title = "Image 1";
figure1.SetTag("Fig1");
figure1.SetImage(dataDir + "image.jpg");
```

これが最後の仕上げです。画像に説明的な代替テキスト（スクリーンリーダーで役立ちます）とタイトルを付け、実際の画像ファイルを設定します。 `SetTag` メソッドは図にタグを付け、後で参照しやすくします。

重要な注意: 画像のパスが `SetImage` マシン上の有効なイメージ ファイルを指します。

## ステップ7: タグ付きPDF文書を保存する

すべてのコンテンツを追加し、構造化したら、PDFを保存します。このステップですべてが確定し、実際のファイルが生成されます。

```csharp
document.Save(dataDir + "IllustrationStructureElements.pdf");
```

簡単ですよね？このコマンドは、これまでの作業をすべて取り込み、先ほど指定したディレクトリに新しいPDFファイルを作成します。フォルダを確認すれば、イラスト要素を含む構造化されたPDFが完成です！

## 結論

おめでとうございます！Aspose.PDF for .NET を使って、イラスト構造要素を含むタグ付きPDFを作成する方法を習得しました。このアプローチにより、PDFは見た目が美しいだけでなく、構造化され、アクセシビリティも確保されます。コンテンツにタグを付け、代替テキストを追加することで、支援技術を使用する人を含め、誰もがドキュメントを楽しめるようになります。

## よくある質問

### タグ付き PDF コンテンツとは何ですか?
タグ付き PDF は、見出し、段落、図などのさまざまな要素を識別するためのタグまたはラベルが含まれた PDF であり、ドキュメントのアクセシビリティが向上します。

### 代替テキストを設定するとどのような効果がありますか?
代替テキストは画像の説明を提供し、スクリーン リーダーで読み取ることができるため、視覚障害のあるユーザーのアクセシビリティが向上します。

### タグ付き PDF に複数の画像を追加できますか?
はい！複数作成できます `FigureElement` オブジェクトを作成し、単一の画像の場合と同じように、各オブジェクトをドキュメントに追加します。

### Aspose.PDF for .NET を使用するにはライセンスが必要ですか?
はい、Aspose.PDFは有料のライブラリですが、 [一時ライセンス](https://purchase.aspose.com/temporary-license/) または、 [無料トライアル](https://releases。aspose.com/).

### PDF を作成した後に図の要素を変更することは可能ですか?
PDF を保存したら、直接変更することはできませんが、Aspose.PDF を使用してドキュメントを再度開き、変更を加えて再度保存することができます。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}