---
"description": "このチュートリアルでは、Aspose.PDF for .NET を使用してPDFのページサイズを取得し、操作を行う方法を説明します。詳細な手順が示されており、プロセス全体をガイドします。"
"linktitle": "PDFのページサイズを取得する"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "PDFのページサイズを取得する"
"url": "/ja/net/programming-with-pdf-pages/get-dimensions/"
"weight": 60
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDFのページサイズを取得する

## 導入

PDFドキュメントのページサイズを調整したいと思ったことはありませんか？ページのサイズを変更したり、ニーズに合わせて回転させたりしたいと思ったことはありませんか？もしそうなら、このチュートリアルはまさにうってつけです！このチュートリアルでは、Aspose.PDF for .NETを使ってPDFのページサイズを取得および変更する方法を解説します。初心者の方でも、経験豊富な開発者の方でも、このガイドはシンプルで分かりやすいでしょう。

Aspose.PDF for .NETは、PDFファイルの作成、操作、変換をスムーズに行える強力なライブラリです。まるでPDF用のスイスアーミーナイフを持っているかのようです。あらゆる細部を微調整し、ニーズにぴったり合うように調整できます。それでは早速、この素晴らしいツールを使ってPDFのページサイズを取得・更新する方法を学びましょう！

## 前提条件

始める前に、このチュートリアルをスムーズに進めるために、いくつかの準備が必要です。

1. Aspose.PDF for .NET: 次のようなことが可能です [最新バージョンはこちらからダウンロードしてください](https://releases.aspose.com/pdf/net/)免許証をお持ちでなくてもご心配なく！ [無料トライアル](https://releases.aspose.com/)、または [一時ライセンス](https://purchase。aspose.com/temporary-license/).
2. Visual Studio: コードの記述と実行に使用する開発環境。
3. C# の基本知識: 物事はシンプルに進めますが、C# に多少精通しているとプロセスがスムーズになります。
4. 使用する PDF ファイル: サンプル PDF ファイルを取得するか、新しい PDF ファイルを作成してテストします。

## パッケージのインポート

Aspose.PDF for .NET を使用するには、いくつかの重要な名前空間をインポートする必要があります。これにより、PDF ドキュメントを操作するための準備が整います。手順は以下のとおりです。

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

これらのインポートにより、特にページの管理やページのサイズの取得など、PDF ファイルの操作に必要なコア クラスにアクセスできるようになります。

すべての準備が整ったので、プロセスをわかりやすい手順に分解してみましょう。

## ステップ1: ファイルパスを定義してドキュメントを読み込む

最初のステップは、PDFドキュメントへのパスを指定し、Aspose.PDFを使用して読み込むことです。これにより、PDFファイル内のページを操作できるようになります。

```csharp
// ドキュメント ディレクトリへのパス。
string dataDir = "YOUR DOCUMENT DIRECTORY";

// ドキュメントを開く
Document pdfDocument = new Document(dataDir + "UpdateDimensions.pdf");
```

このステップでは、基本的に作業したいPDFファイルを開きます。書籍の特定のページを開いたことがある方なら、これはかなり似ていますが、PDF文書を開いてそのページにアクセスすることになります。

## ステップ2: ページが存在しない場合は空白ページを追加する

ドキュメントにページがない場合はどうすればいいでしょうか？ご安心ください！ドキュメントに空白ページを追加して作業を進めることができます。ページが存在するかどうかを確認し、必要に応じて新しいページを追加する方法は次のとおりです。

```csharp
// PDF文書に空白ページを追加します
Page page = pdfDocument.Pages.Count > 0 ? pdfDocument.Pages[1] : pdfDocument.Pages.Add();
```

このコード行は、ドキュメント内に既にページが存在するかどうかを確認します。存在する場合は、最初のページを選択します（`Pages[1]`それ以外の場合は、空白のページが作成され、PDF に追加されます。

空のノートを開いて、何も書かれていない場合は最初のページに書き込むようなものだと考えてください。簡単ですよね?

## ステップ3: ページの高さと幅の情報を取得する

作業するページができたので、ページのサイズを取得してみましょう。 `GetPageRect()` 高さと幅を取得する方法。

```csharp
// ページの高さと幅の情報を取得する
Console.WriteLine(page.GetPageRect(true).Width.ToString() + ":" + page.GetPageRect(true).Height.ToString());
```

ここ、 `GetPageRect(true)` ページの高さと幅を含む長方形を返します。定規で紙を測るようなものです。出力はコンソールに表示され、現在のページ寸法がわかります。

## ステップ4：ページを90度回転する

ページを回転させたいですか？問題ありません！簡単なプロパティで、ページを90度回転させることができます。

```csharp
// ページを90度回転する
page.Rotate = Rotation.on90;
```

この手順でページを時計回りに90度回転させます。机の上の印刷されたシートを回転させると、横向きになります。

## ステップ5: 回転後のページサイズを再確認する

ページを回転させた後は、寸法を再度確認することをお勧めします。なぜなら、回転によって高さと幅の解釈が変化する可能性があるからです。

```csharp
// ページの高さと幅の情報を取得する
Console.WriteLine(page.GetPageRect(true).Width.ToString() + ":" + page.GetPageRect(true).Height.ToString());
```

これで、ページのサイズが新しい向きに基づいて更新されます。スマートフォンで写真を回転させるのと同じように、幅が高さに、そしてその逆も突然起こります。


## 結論

おめでとうございます！Aspose.PDF for .NET を使用して PDF ページのサイズを取得および変更する方法を学習しました。これで、PDF を読み込み、ページのサイズを確認し、必要に応じてページを回転させることができるはずです。

PDFの操作は複雑である必要はありません。Aspose.PDFを使えば、直感的な操作で数ステップで簡単に操作できます。次回PDFのページサイズを操作する必要がある場合は、必要な操作を正確に把握できるはずです。

## よくある質問

### ページを 90 度以外の角度で回転できますか?
はい、Aspose.PDFでは、ページを0度、90度、180度、または270度回転させることができます。 `Rotation` 財産。

### PDF にページがない場合はどうなりますか?
PDFにページがない場合は、 `Pages.Add()` このチュートリアルで示されている方法を使用します。

### 複数のページを一度に操作できますか?
はい、複数のページをループして、サイズ変更や回転などの変換をすべてのページに適用できます。

### ページのサイズは PDF 内のコンテンツに影響しますか?
ページのサイズはキャンバスのサイズのみを変更し、コンテンツは変更しません。ただし、サイズを変更すると、ページ上でのコンテンツの表示が変わる場合があります。

### Aspose.PDF for .NET の詳細情報はどこで入手できますか?
訪問することができます [ドキュメントはこちら](https://reference.aspose.com/pdf/net/) より詳細な情報と高度な使用例については、こちらをご覧ください。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}