---
"description": "Aspose.PDF for .NET のテキスト デバイスを使用して PDF ドキュメントからテキストを抽出する方法を学習します。"
"linktitle": "テキストデバイスを使用してテキストを抽出する"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "テキストデバイスを使用してテキストを抽出する"
"url": "/ja/net/programming-with-text/extract-text-using-text-device/"
"weight": 210
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# テキストデバイスを使用してテキストを抽出する

## 導入

PDFからテキストを抽出するのは、特に様々な形式、埋め込みフォント、複雑なレイアウトを持つドキュメントを扱う場合は、難しい場合があります。しかし、Aspose.PDF for .NETを使えば、このプロセスは簡単になります！PDFのページをプレーンテキストに変換して詳細な分析を行いたい場合でも、特定のセクションだけを抽出したい場合でも、Aspose.PDFが対応します。このチュートリアルでは、Aspose.PDFのTextDeviceクラスを使用してPDFからテキストを抽出する方法を、ステップバイステップで解説します。また、分かりやすい説明も提供しているので、同じ方法をご自身のプロジェクトに簡単に適用できます。

## 前提条件

コードの説明に入る前に、必要な準備がすべて整っていることを確認してください。必要なものは以下のとおりです。

1. Aspose.PDF for .NET: 最新バージョンを以下からダウンロードしてください。 [Aspose.PDF for .NET のダウンロード ページ](https://releases。aspose.com/pdf/net/).
2. 開発環境: Visual Studio またはその他の C# 開発環境。
3. .NET Framework: プロジェクトが .NET Framework 4.x 以上を対象としていることを確認します。
4. 入力PDFファイル: テキスト抽出に使用するPDFファイル。これをマシン上のディレクトリ（以下、 `YOUR DOCUMENT DIRECTORY`）。

## パッケージのインポート

コードの先頭で、Aspose.PDF を操作するために必要な名前空間をインポートする必要があります。

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Devices;
using System;
using System.Text;
```

## ステップ1：PDF文書を読み込む

テキストを抽出する前に、PDF文書をメモリに読み込む必要があります。このステップでは、Aspose.PDFの `Document` クラス。これにより、ファイル内のすべてのページとコンテンツにアクセスできるようになります。

```csharp
// PDFドキュメントへのパスを定義する
string dataDir = "YOUR DOCUMENT DIRECTORY";

// PDF文書を読み込む
Document pdfDocument = new Document(dataDir + "input.pdf");
```

ここでは、 `Document pdfDocument = new Document(dataDir + "input.pdf");` PDFを読み込むには、 `dataDir` 変数はPDFファイルのディレクトリパスを保持します。これによりドキュメント全体にアクセスでき、ページをループしてコンテンツを抽出できるようになります。

## ステップ2: テキスト保存用の文字列ビルダーを設定する

ドキュメントが読み込まれたら、抽出したテキストを保存する方法が必要です。そのためには、 `StringBuilder` これにより、効率的な文字列連結が可能になります。

```csharp
// 抽出したテキストを保持するStringBuilder
StringBuilder builder = new StringBuilder();
```

初期化する `StringBuilder` インスタンスは各ページから抽出されたテキストを収集します。これは、ループ内での通常の文字列連結に比べて、大きな文字列を処理するより効率的な方法です。

## ステップ3: PDFページをループする

次に、PDF文書の各ページをループしてテキストを抽出します。各ページを個別に処理するには、 `TextDevice` PDF コンテンツをテキスト形式に変換する役割を担うクラスです。

```csharp
// PDF内のすべてのページをループする
foreach (Page pdfPage in pdfDocument.Pages)
{
    // 各ページを処理してテキストを抽出します
}
```

このループはPDFのすべてのページを巡回します（`pdfDocument.Pages`）。各ページからテキストを抽出し、 `StringBuilder`。

## ステップ4：各ページからテキストを抽出する

さて、各ページのテキスト抽出プロセスを設定します。ここでは、 `TextDevice` オブジェクトを作成し、それを使用してPDFページを処理します。 `TextDevice` 設定した抽出オプションに基づいて、生のテキストまたはフォーマットされたテキストを抽出します。

```csharp
using (MemoryStream textStream = new MemoryStream())
{
    // テキスト抽出用のテキストデバイスを作成する
    TextDevice textDevice = new TextDevice();
    
    // テキスト抽出オプションを「Pure」モードに設定する
    TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);
    textDevice.ExtractionOptions = textExtOptions;

    // 現在のページからテキストを抽出し、メモリストリームに保存します
    textDevice.Process(pdfPage, textStream);

    // メモリストリームをテキストに変換する
    string extractedText = Encoding.Unicode.GetString(textStream.ToArray());

    // 抽出したテキストをStringBuilderに追加します
    builder.Append(extractedText);
}
```

- `TextDevice textDevice = new TextDevice();`：その `TextDevice` クラスは PDF からテキストを抽出するために使用されます。
- `TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);`: このオプションは、フォントや位置などの書式設定を保持せずに生のテキストを抽出します。 `TextFormattingMode.Raw` 書式設定をさらに細かく制御する必要がある場合。
- `textDevice.Process(pdfPage, textStream);`: PDFの各ページを処理し、抽出したテキストを `MemoryStream`。
- 最後に、テキストを `MemoryStream` 文字列にそれを追加して `StringBuilder`。

## ステップ5: 抽出したテキストをファイルに保存する

すべてのページを処理した後、テキストは `StringBuilder`最後のステップは、抽出したテキストをファイルに保存することです。

```csharp
// テキストファイルの出力パスを定義する
dataDir = dataDir + "input_Text_Extracted_out.txt";

// 抽出したテキストをファイルに保存する
File.WriteAllText(dataDir, builder.ToString());

Console.WriteLine("\nText extracted successfully from PDF document.\nFile saved at " + dataDir);
```

- `File.WriteAllText(dataDir, builder.ToString());`これは、 `StringBuilder` テキストファイルに変換します。
- 出力ファイルのパスはファイル名（`"input_Text_Extracted_out.txt"`）に `dataDir` パス。

## 結論

Aspose.PDF for .NET を使用した PDF からのテキスト抽出は、シンプルかつ効率的なプロセスです。このガイドで説明する手順に従うだけで、PDF ドキュメントを簡単に開き、ページをループ処理し、テキストをテキストファイルに抽出できます。これは、大量の PDF データの処理、テキスト分析、またはドキュメントを変換してさらなる操作を行う際に特に役立ちます。

Aspose.PDF は、テキスト抽出だけでなく、注釈の処理、画像の操作、さらには PDF を HTML や Word などの他の形式に変換することまで可能です。このライブラリの柔軟性と強力さは、.NET アプリケーションにおける PDF 管理に非常に役立つツールです。

## よくある質問

### Aspose.PDF は画像ベースの PDF からテキストを抽出できますか?
いいえ、Aspose.PDF はコンテンツベースの PDF からテキストを抽出するように設計されています。画像ベースの PDF の場合は、OCR 技術が必要です。

### Aspose.PDF はテキストを抽出するときに書式を保持しますか?
デフォルトでは、テキストは書式設定なしで抽出されますが、一部の書式設定を保持する場合は抽出オプションを調整できます。

### 特定のページ範囲からテキストを抽出できますか?
はい、すべてのページではなく特定の範囲のページをループするようにコードを変更することができます。

### Aspose.PDF のテキスト抽出モードは何ですか?
Aspose.PDF には、Raw と Pure の 2 つのモードがあります。Raw モードでは元のレイアウトが保持され、Pure モードでは書式設定なしでテキストのみが抽出されます。

### Aspose.PDF for .NET は .NET Core と互換性がありますか?
はい、Aspose.PDF for .NET は .NET Core および .NET Framework と完全に互換性があります。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}