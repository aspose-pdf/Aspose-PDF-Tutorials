---
"description": "Aspose.PDF for .NET を使用してPDFファイルに日付と時刻のスタンプを追加する方法を、ステップバイステップで解説します。ドキュメントの信頼性を高めるのに最適です。"
"linktitle": "PDFファイルに日付タイムスタンプを追加する"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "PDFファイルに日付タイムスタンプを追加する"
"url": "/ja/net/programming-with-stamps-and-watermarks/add-date-time-stamp/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDFファイルに日付タイムスタンプを追加する

## 導入

ドキュメント、特にPDFを管理する上で、日付とタイムスタンプを追加することは大きな効果を発揮します。法務文書、プロジェクトレポート、請求書など、どのような文書を作成する場合でも、タイムスタンプは信頼性を高めるだけでなく、ドキュメントがいつ作成または変更されたかを明確に記録します。このガイドでは、.NET向けAspose.PDFライブラリを使用してPDFファイルに日付とタイムスタンプを追加する手順を詳しく説明します。 

この記事は分かりやすく、理解しやすいように作成されているので、プログラミングやAspose.PDFライブラリの初心者でも、自信を持ってこの機能を実装できます。さあ、始めましょう！

## 前提条件

始める前に、いくつかの前提条件を満たす必要があります。

1. Visual Studio: お使いのマシンにVisual Studioがインストールされていることを確認してください。ここでコードを記述し、実行します。
2. Aspose.PDF for .NET: Aspose.PDFライブラリをダウンロードしてインストールする必要があります。最新バージョンは以下から入手できます。 [ここ](https://releases。aspose.com/pdf/net/).
3. C# の基礎知識: C# プログラミングの知識があれば、例をより深く理解することができますが、初心者でも心配する必要はありません。すべてをステップごとに説明します。
4. PDFファイル: サンプルのPDFファイルを用意してください。この例では、 `AddTextStamp。pdf`.

これらの前提条件が満たされたら、PDF ファイルに日付と時刻のスタンプを追加する準備が整います。

## パッケージのインポート

まず、C#プロジェクトに必要な名前空間をインポートする必要があります。手順は以下のとおりです。

### 新しいプロジェクトを作成する

1. Visual Studio を開く: Visual Studio アプリケーションを起動します。
2. 新しいプロジェクトの作成: スタート画面から「新しいプロジェクトの作成」を選択します。
3. コンソール アプリの選択: プロジェクト テンプレートのリストから「コンソール アプリ (.NET Framework)」を選択します。
4. プロジェクトに名前を付ける: プロジェクトに名前を付けます。例: `PDFDateTimeStamp`。

### Aspose.PDF 参照を追加する

1. [参照] を右クリック: ソリューション エクスプローラーで、プロジェクトの [参照] フォルダーを右クリックします。
2. 「参照の追加」を選択します。コンテキスト メニューから「参照の追加」を選択します。
3. Aspose.PDF を参照: Aspose.PDF をダウンロードした場所に移動し、選択します。「OK」をクリックしてプロジェクトに追加します。

### 必要な名前空間をインポートする

あなたの `Program.cs` ファイルでは、次の名前空間をインポートする必要があります。

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
using Aspose.Pdf.Annotations;
```

すべての設定が完了したので、PDF ファイルに日付と時刻のスタンプを追加するプロセスを、明確で管理しやすい手順に分解してみましょう。

## ステップ1: ドキュメントディレクトリを設定する

まず、PDFファイルが保存されているディレクトリを指定する必要があります。コードはこのディレクトリ内でPDFファイルを検索するため、これは非常に重要です。

```csharp
// ドキュメント ディレクトリへのパス。
string dataDir = "YOUR DOCUMENT DIRECTORY"; // 実際のパスに置き換えてください
```

必ず交換してください `YOUR DOCUMENT DIRECTORY` PDF ファイルへの実際のパスを入力します。

## ステップ2: PDFドキュメントを開く

次に、タイムスタンプを追加する PDF ドキュメントを開きます。 

```csharp
// ドキュメントを開く
Document pdfDocument = new Document(dataDir + "AddTextStamp.pdf");
```

このコード行は、 `Document` クラスを作成し、PDFファイルを `pdfDocument` 物体。

## ステップ3: 日付タイムスタンプを作成する

次は日付とタイムスタンプを生成します。特定の形式で表示できるようにフォーマットします。 

```csharp
string annotationText = DateTime.Now.ToString("MM/dd/yy hh:mm:ss tt ");
```

ここ、 `DateTime.Now` 現在の日付と時刻を取得し、 `ToString` 希望する形式にフォーマットします。

## ステップ4: テキストスタンプを作成する

日付と時刻の文字列が準備できたら、PDF に追加するテキスト スタンプを作成できます。

```csharp
// テキストスタンプを作成する
TextStamp textStamp = new TextStamp(annotationText);
```

この行は、 `TextStamp` フォーマットされた日付と時刻の文字列を使用します。

## ステップ5: スタンプのプロパティを設定する

スタンプの外観と位置をカスタマイズできます。プロパティの設定方法は次のとおりです。

```csharp
// スタンプのプロパティを設定する
textStamp.BottomMargin = 10;
textStamp.RightMargin = 20;
textStamp.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Right;
textStamp.VerticalAlignment = VerticalAlignment.Bottom;
```

この手順では、余白を設定し、スタンプを PDF ページの右下隅に揃えます。

## ステップ6: PDFにスタンプを追加する

次に、PDF ドキュメントにテキスト スタンプを追加します。 

```csharp
// 切手コレクションにスタンプを追加する
pdfDocument.Pages[1].AddStamp(textStamp);
```

この行は、PDFの最初のページにスタンプを追加します。別のページにスタンプを配置したい場合は、ページ番号を変更できます。

## ステップ7: フリーテキスト注釈を作成する（オプション）

スタンプに注釈を追加したい場合は、 `FreeTextAnnotation` 次のように：

```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 6, System.Drawing.Color.Black);
FreeTextAnnotation textAnnotation = new FreeTextAnnotation(pdfDocument.Pages[1], new Aspose.Pdf.Rectangle(0, 0, 0, 0), default_appearance);
textAnnotation.Name = "Stamp";
textAnnotation.Accept(new AnnotationSelector(textAnnotation));
textAnnotation.Contents = textStamp.Value;
```

このオプションの手順では、スタンプに関する追加のコンテキストや情報を提供できるフリーテキスト注釈を作成します。

## ステップ8: 注釈の境界線を設定する

注釈の境界線をカスタマイズしたい場合は、次のようにします。

```csharp
Border border = new Border(textAnnotation);
border.Width = 0;
border.Dash = new Dash(1, 1);
textAnnotation.Border = border;
textAnnotation.Rect = new Aspose.Pdf.Rectangle(0, 0, 0, 0);
pdfDocument.Pages[1].Annotations.Add(textAnnotation);
```

このコード スニペットは、境界線の幅を 0 に設定して境界線を非表示にし、注釈を PDF に追加します。

## ステップ9: PDFドキュメントを保存する

最後に、変更した PDF ドキュメントを保存する必要があります。 

```csharp
dataDir = dataDir + "AddDateTimeStamp_out.pdf"; // 出力ファイル名を指定する
pdfDocument.Save(dataDir);
Console.WriteLine("\nDate time stamp added successfully.\nFile saved at " + dataDir);
```

この行は、タイムスタンプが追加されたPDFを新しいファイルに保存します。出力内容は、指定したディレクトリで確認できます。

## 結論

おめでとうございます！Aspose.PDF for .NET を使用して、PDF ファイルに日付と時刻のスタンプを追加することができました。このシンプルながらも効果的な機能は、ドキュメントをよりプロフェッショナルなものにし、作成日時や変更日時を明確に記録するのに役立ちます。 

## よくある質問

### タイムスタンプの日付形式をカスタマイズできますか?
はい、変更できます `ToString` 日付形式を好みに合わせて変更する方法。

### Aspose.PDF は無料で使用できますか?
Aspose.PDFは無料トライアルを提供していますが、フル機能を使用するにはライセンスを購入する必要があります。一時ライセンスを取得できます。 [ここ](https://purchase。aspose.com/temporary-license/).

### PDF に複数のタイムスタンプを追加できますか?
もちろんです！複数の `TextStamp` インスタンスを作成し、PDF 内の別のページまたは位置に追加します。

### Visual Studio を持っていない場合はどうなりますか?
任意の C# IDE またはテキスト エディターを使用できますが、プロジェクトの実行とデバッグには Visual Studio をお勧めします。

### Aspose.PDF の使用例をもっと知りたい場合は、どこに行けばよいですか?
さらに多くの例とチュートリアルについては、 [Aspose.PDF ドキュメント](https://reference。aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}