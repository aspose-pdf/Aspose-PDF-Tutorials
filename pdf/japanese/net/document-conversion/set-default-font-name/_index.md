---
"description": "Aspose.PDF for .NET を使用してPDFを画像に変換する際のデフォルトのフォント名を設定する方法を説明します。このガイドでは、前提条件、手順、よくある質問について解説します。"
"linktitle": "デフォルトのフォント名を設定する"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "デフォルトのフォント名を設定する"
"url": "/ja/net/document-conversion/set-default-font-name/"
"weight": 270
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# デフォルトのフォント名を設定する

## 導入

PDFドキュメントを画像に変換しようとした際に、フォントがうまく表示されないことに気づいたことはありませんか？ テキストが歪んで表示されていたり、元のフォントがサポートされていない可能性があります。そんな時、デフォルトフォントを設定することで解決できます！ Aspose.PDF for .NET を使えば、PDFレンダリングのデフォルトフォントを簡単に設定でき、ドキュメントを鮮明でプロフェッショナルな仕上がりにすることができます。このチュートリアルでは、PDFを画像に変換する際のデフォルトフォント名の設定方法を詳しく説明します。このガイドを読み終える頃には、あらゆるPDFレンダリングの課題に対処できるスキルを身に付けているはずです。準備はいいですか？早速始めましょう！

## 前提条件

コードに進む前に、準備しておく必要があるものがいくつかあります。

- Aspose.PDF for .NET：この強力なライブラリを使ってPDF文書を操作します。ダウンロードは以下から行えます。 [Aspose ウェブサイト](https://releases。aspose.com/pdf/net/).
- Visual Studio: お使いのマシンにVisual Studioがインストールされていることを確認してください。これが開発環境となります。
- .NET Framework: .NET Framework がインストールされていることを確認してください。Aspose.PDF for .NET はさまざまなバージョンをサポートしているため、ニーズに合わせてドキュメントをご確認ください。
- PDFドキュメント：作業にはサンプルのPDFドキュメントが必要です。お持ちでない場合は、シンプルなPDFを作成するか、オンラインでサンプルをダウンロードしてください。

すべての設定が完了したら、コーディングを開始する準備が整います。

## パッケージのインポート

コードに進む前に、必要なパッケージをインポートすることが重要です。これにより、プロジェクトに必要なすべてのクラスとメソッドにアクセスできるようになります。

```csharp
using Aspose.Pdf.Devices;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
```

これらのインポートは、PDF 操作、画像レンダリング、およびファイル ストリーム操作を処理するために必要な名前空間を取り込むため、非常に重要です。

## ステップ1: プロジェクトとドキュメントパスを設定する

まず最初に、PDF文書が保存されているディレクトリパスを設定しましょう。これがPDFファイルを操作するための出発点となります。

```csharp
// ドキュメント ディレクトリへのパス。
string dataDir = "YOUR DOCUMENT DIRECTORY";
```
ここ、 `dataDir` PDF文書が保存されているディレクトリです。 `"YOUR DOCUMENT DIRECTORY"` ドキュメントへの実際のパスを指定します。コードがPDFファイルを取得する場所を知る必要があるため、これは必須です。

## ステップ2: PDFドキュメントを読み込む

ドキュメント パスが取得できたので、次の手順では PDF ドキュメントをメモリに読み込んで作業を開始します。

```csharp
using (Document pdfDocument = new Document(dataDir + "input.pdf"))
```
私たちは `Document` PDFファイルを読み込むには、Aspose.PDFライブラリのクラスを使用します。このクラスは、PDFドキュメントを操作するための様々なメソッドとプロパティを提供します。 `"input.pdf"` 実際のPDFファイル名に置き換えてください。このファイルはレンダリングの入力として使用されます。

## ステップ3: 出力用の画像ストリームを作成する

ドキュメントが読み込まれたら、レンダリングされた画像を保存するためのストリームを設定する必要があります。出力画像はここに保存されます。

```csharp
using (FileStream imageStream = new FileStream(dataDir + "SetDefaultFontName.png", FileMode.Create))
```
その `FileStream` クラスは、レンダリングされた画像を保存する新しいファイルを作成するために使用されます。この例では、画像を次のように保存しています。 `"SetDefaultFontName.png"`。その `FileMode.Create` 新しいファイルが作成されるか、既存のファイルが上書きされることを保証します。

## ステップ4: 画像の解像度を設定する

PDFを画像に変換する前に、解像度を設定することが重要です。解像度によって出力画像の品質と鮮明さが決まります。

```csharp
Resolution resolution = new Resolution(300);
```
その `Resolution` クラスは出力画像の解像度を設定します。ここでは、高画質画像の標準である300DPI（dots per inch）の解像度を選択しました。これにより、PDF内のテキストとグラフィックが細部を失うことなく鮮明に表示されます。

## ステップ5: PNGデバイスを構成する

次に、PDF を PNG 画像にレンダリングするデバイスを構成する必要があります。

```csharp
PngDevice pngDevice = new PngDevice(resolution);
```
その `PngDevice` クラスはPDF文書をPNG画像に変換する役割を担っています。 `resolution` これに反対することで、指定された DPI で画像が作成されるようになります。

## ステップ6: デフォルトのフォント名を設定する

ここが重要な部分です。デフォルトのフォント名を設定します。これは、PDFで元のフォントが利用できない場合に代替フォントとして使用されます。

```csharp
RenderingOptions ro = new RenderingOptions();
ro.DefaultFontName = "Arial";
pngDevice.RenderingOptions = ro;
```
インスタンスを作成します `RenderingOptions` そしてその `DefaultFontName` 財産に `"Arial"`つまり、PDFファイル内の元のフォントが見つからない場合、代わりにArialが使用されます。この手順は、レンダリングされた画像内のテキストの読みやすさと外観を維持するために非常に重要です。

## ステップ7: PDFページを画像に変換する

最後に、すべての設定が完了したら、PDF ドキュメントの最初のページを画像に変換し、先ほど作成したファイル ストリームを使用して保存できるようになります。

```csharp
pngDevice.Process(pdfDocument.Pages[1], imageStream);
```
その `Process` の方法 `PngDevice` クラスは、指定されたPDFページ（この場合は最初のページ）を画像に変換するために使用されます。出力は `imageStream`この手順では、PDF ページを指定された解像度とデフォルトのフォントで PNG 画像に変換します。

## ステップ8: ファイルストリームとPDFドキュメントを閉じる

画像をレンダリングした後は、リソースを解放するためにファイル ストリームと PDF ドキュメントを閉じることが重要です。

```csharp
imageStream.Close();
pdfDocument.Dispose();
```
閉会 `imageStream` ファイルが正しく保存され、データが失われないことを保証します。 `pdfDocument` メモリとリソースを解放し、潜在的なメモリ リークを防止します。

## 結論

これで完了です！わずか数行のコードで、Aspose.PDF for .NET を使用してPDFを画像にレンダリングする際に、デフォルトのフォント名を設定する方法を学習しました。このスキルは、特にサポートされていないフォントが含まれている可能性のあるPDFを扱う際に非常に役立ちます。デフォルトのフォントを設定することで、レンダリングされた画像の読みやすさとプロフェッショナルな外観を維持できます。

## よくある質問

### 指定されたデフォルトのフォントがシステムにインストールされていない場合はどうなりますか?
デフォルトのフォントが `RenderingOptions` システムにインストールされていない場合、Aspose.PDF はシステム定義のフォールバック フォントを使用します。

### Arial 以外のフォントをデフォルトのフォントとして使用できますか?
もちろんです！システムにインストールされている任意のフォントをデフォルトのフォントとして設定できます。

### PDF の複数ページを一度に画像に変換することは可能ですか?
はい、PDF のページをループし、同じプロセスを使用して各ページを個別にレンダリングできます。

### 高解像度を設定すると、PDF レンダリングのパフォーマンスに影響しますか?
はい、解像度を高くすると画像ファイルが大きくなり、レンダリング時間が長くなる可能性がありますが、より鮮明な画像が生成されます。

### PDF を PNG 以外の画像形式にレンダリングできますか?
はい、Aspose.PDF は JPEG、BMP、TIFF などのさまざまな画像形式へのレンダリングをサポートしています。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}