---
"description": "Aspose.PDF for .NET を使用して PDF ファイルにテキスト スタンプを追加する方法をステップ バイ ステップ ガイドで学習し、ドキュメントのプレゼンテーションを向上させましょう。"
"linktitle": "PDFファイルにテキストスタンプを追加する"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "PDFファイルにテキストスタンプを追加する"
"url": "/ja/net/programming-with-stamps-and-watermarks/add-text-stamp/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDFファイルにテキストスタンプを追加する

## 導入

今日のデジタル時代において、PDFは文書の共有や配信に広く利用されています。開発者、コンテンツクリエイター、あるいは単にPDFファイルをより魅力的にしたいと考えている人にとって、PDFをプログラムで操作する方法を知っていると、状況は大きく変わります。ぜひ活用したい便利な機能の一つが、PDFファイルにテキストスタンプを追加する機能です。テキストスタンプを追加することで、文書にプロフェッショナルな印象を与えたり、「サンプル」「機密」といった重要な情報や透かしなどを追加したりできます。

## 前提条件

コードに進む前に、すべてが正しく設定されていることを確認するための前提条件がいくつかあります。必要なものは次のとおりです。

1. Aspose.PDF for .NET: プロジェクトにAspose.PDFライブラリがインストールされていることを確認してください。まだインストールされていない場合は、以下のリンクからダウンロードできます。 [Aspose ウェブサイト](https://releases。aspose.com/pdf/net/).
2. Visual Studio または互換 IDE: .NET コードを記述して実行するには開発環境が必要です。開発者の間で最もよく選ばれているのは Visual Studio です。
3. C# の基礎知識: C# とオブジェクト指向プログラミングの原則を理解していると、例をよりよく理解できるようになります。
4. サンプルPDFファイル：作業に必要なPDFファイルをご用意ください。基本的なPDFファイルを作成することも、既存のPDFファイルを使用して機能をテストすることもできます。

これらの前提条件を整理したら、コーディングに進むことができます。

## パッケージのインポート

それでは、必要なパッケージをインポートしましょう。このステップは、Asposeライブラリのクラスとメソッドをプロジェクトで利用できるようにするため、非常に重要です。

### Aspose.PDFアセンブリをインポートする

まず、Aspose.PDF 名前空間をインポートする必要があります。C# ファイルの先頭に、次の using ディレクティブを追加します。

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

これにより、PDF ドキュメントの作成と操作に不可欠なクラスにアクセスできるようになります。

それでは、チュートリアルの本題に入りましょう。プロセスを明確かつ簡潔なステップに分解します。各ステップでは、PDFファイルにテキストスタンプを追加するためのコードについて順を追って説明します。

## ステップ1: ドキュメントディレクトリを設定する

まず、PDFドキュメントが保存されているディレクトリを設定する必要があります。つまり、コード内で編集対象のPDFファイルがどこにあるかを認識する必要があります。

```csharp
// ドキュメント ディレクトリへのパス。
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

説明: 置き換え `"YOUR DOCUMENT DIRECTORY"` PDFファイルの実際のパス（`AddTextStamp.pdf`）が保存されます。このパスは、後で変更されたPDFを開いて保存するときに使用されます。

## ステップ2: PDFドキュメントを開く

次に、PDF文書を `Document` Aspose.PDF 名前空間からのクラス。

```csharp
// ドキュメントを開く
Document pdfDocument = new Document(dataDir + "AddTextStamp.pdf");
```

説明: ここでは、 `Document` クラスにPDFファイルへのパスを渡します。これによりPDFが読み込まれ、操作できるようになります。

## ステップ3: テキストスタンプを作成する

ここで、後で PDF ドキュメントに適用するテキスト スタンプを作成します。

```csharp
// テキストスタンプを作成する
TextStamp textStamp = new TextStamp("Sample Stamp");
```

説明: `TextStamp` 表示したいテキストを含むオブジェクトが作成されます。この場合、スタンプのテキストとして「Sample Stamp」を使用します。

## ステップ4: スタンプのプロパティを設定する

スタンプをカスタマイズするには、背景色、位置、回転など、さまざまなプロパティを設定できます。それでは、設定してみましょう。

```csharp
// スタンプを背景にするかどうかを設定する
textStamp.Background = true;

// 原点を設定
textStamp.XIndent = 100;
textStamp.YIndent = 100;

// スタンプを回転させる
textStamp.Rotate = Rotation.on90;
```

説明：
- 背景: これを設定すると `true` つまり、スタンプは PDF コンテンツの背後に表示されます。
- XIndent と YIndent: これらのプロパティは、ページ上のスタンプの位置を決定します。この例では、スタンプはページの左端と上端から100単位の位置に配置されます。
- 回転：スタンプを90度回転させます。デザイン要件に応じて、様々な回転オプションを選択できます。

## ステップ5: テキストプロパティをカスタマイズする

次に、スタンプ内のテキストの外観をカスタマイズして創造性を発揮してみましょう。

```csharp
// テキストプロパティを設定する
textStamp.TextState.Font = FontRepository.FindFont("Arial");
textStamp.TextState.FontSize = 14.0F;
textStamp.TextState.FontStyle = FontStyles.Bold | FontStyles.Italic;
textStamp.TextState.ForegroundColor = Aspose.Pdf.Color.FromRgb(Color.Aqua);
```

説明：
- フォント: Arial フォントを使用し、太字と斜体にしています。
- フォントサイズ: 14 ポイントに設定されています。
- ForegroundColor: RGBを使用して、テキストの色をアクアに設定します。ブランディングやデザインのニーズに合わせて自由に色を変更できます。

## ステップ6: PDFページにスタンプを追加する

ここで、PDF ドキュメントの特定のページにスタンプを追加します。

```csharp
// 特定のページにスタンプを追加する
pdfDocument.Pages[1].AddStamp(textStamp);
```

説明: この例では、スタンプはPDFの最初のページに追加されます（ページは1からインデックスされます）。ドキュメントに応じてページ番号を調整してください。

## ステップ7: 変更したPDFを保存する

最後に、新しく追加したテキストスタンプを含むドキュメントを保存しましょう。

```csharp
dataDir = dataDir + "AddTextStamp_out.pdf";

// 出力ドキュメントを保存する
pdfDocument.Save(dataDir);
Console.WriteLine("\nText stamp added successfully.\nFile saved at " + dataDir);
```

説明: 出力ファイルの新しいパスを定義し、変更したドキュメントを保存します。保存後、パスがコンソールに表示され、操作が成功したことが確認できます。

## 結論

おめでとうございます！Aspose.PDF for .NET を使用して、PDF ファイルにテキストスタンプを追加することができました。この方法を使えば、ドキュメントに効率的に注釈を付けることができ、プロフェッショナルな印象と使いやすさの両方を高めることができます。透かし、署名、簡単なメモなどを追加する場合でも、Aspose ライブラリは PDF を簡単に操作できる強力なツールを提供します。

## よくある質問

### PDF のテキスト スタンプとは何ですか?
テキスト スタンプは、PDF ドキュメントに配置できるテキストを含むグラフィカル オーバーレイであり、注釈や透かしとしてよく使用されます。

### スタンプを画像でカスタマイズできますか？
はい、Aspose.PDF は画像スタンプの追加もサポートしており、より柔軟なデザインを実現します。

### Aspose.PDF ではどのようなプログラミング言語を使用できますか?
Aspose.PDF は主に .NET に重点を置いていますが、Java や Python などの他の言語用のバージョンも用意されています。

### Aspose.PDF の一時ライセンスを取得するにはどうすればよいですか?
一時ライセンスを申請するには、 [購入リンク](https://purchase.aspose.com/temporary-license/) 彼らのウェブサイトで。

### Aspose.PDF のサポートはどこで受けられますか?
Aspose.PDFのサポートは、 [サポートフォーラム](https://forum。aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}