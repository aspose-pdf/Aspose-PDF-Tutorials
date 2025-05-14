---
"description": "このステップバイステップのチュートリアルでは、Aspose.PDF for .NET を使用して PDF に水平および垂直に整列したラジオ ボタンを作成する方法を学習します。"
"linktitle": "水平方向と垂直方向のラジオボタン"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "水平方向と垂直方向のラジオボタン"
"url": "/ja/net/programming-with-forms/horizontally-and-vertically-radio-buttons/"
"weight": 180
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 水平方向と垂直方向のラジオボタン

## 導入

インタラクティブなPDFフォームを作成すると、特に情報収集においてユーザーエクスペリエンスを大幅に向上させることができます。最も一般的なフォーム要素の一つはラジオボタンで、ユーザーは選択肢の中から1つを選択できます。このチュートリアルでは、Aspose.PDF for .NETを使用して、水平方向と垂直方向に並んだラジオボタンを作成する方法を説明します。経験豊富な開発者の方にも、初心者の方にも、このガイドはプロセスをステップバイステップで解説し、各要素を明確に理解できるようにします。

## 前提条件

コードに進む前に、いくつかの前提条件を満たす必要があります。

1. Aspose.PDF for .NET: Aspose.PDFライブラリがインストールされていることを確認してください。ダウンロードは以下から行えます。 [サイト](https://releases。aspose.com/pdf/net/).
2. Visual Studio: コードを記述およびテストできる開発環境。
3. C# の基礎知識: C# プログラミングに精通していると、コード スニペットをよりよく理解できるようになります。

## パッケージのインポート

まず、C#プロジェクトに必要なパッケージをインポートする必要があります。手順は以下のとおりです。

### 新しいプロジェクトを作成する

Visual Studioを開き、新しいC#プロジェクトを作成します。簡単にするために、コンソールアプリケーションを選択してください。

### Aspose.PDF 参照を追加する

1. ソリューション エクスプローラーでプロジェクトを右クリックします。
2. 「NuGet パッケージの管理」を選択します。
3. 「Aspose.PDF」を検索し、最新バージョンをインストールしてください。

```csharp
using System;
using System.IO;
using Aspose.Pdf.Facades;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
```

すべての設定が完了したので、コードを分解して、水平および垂直に揃ったラジオ ボタンを作成しましょう。

## ステップ1: ドキュメントディレクトリを設定する

この手順では、PDF ドキュメントを保存するディレクトリへのパスを定義します。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

交換する `"YOUR DOCUMENT DIRECTORY"` PDFファイルを保存する実際のパスを指定します。これは、プログラムに入力ファイルの検索場所と出力ファイルの保存場所を指示するため、非常に重要です。

## ステップ2: 既存のPDF文書を読み込む

次に、作業対象となるPDF文書を読み込む必要があります。これは、 `FormEditor` クラス。

```csharp
FormEditor formEditor = new FormEditor();
formEditor.BindPdf(dataDir + "input.pdf");
```

ここでは、 `FormEditor` 既存のPDFファイルにバインドします。 `input.pdf`指定したディレクトリにこのファイルが存在することを確認してください。

## ステップ3: ラジオボタンのプロパティを構成する

それでは、ラジオボタンのプロパティをいくつか設定しましょう。ボタン間の間隔、向き、サイズなどです。

```csharp
formEditor.RadioGap = 4; // ラジオボタンのオプション間の距離
formEditor.RadioHoriz = true; // 水平方向の配置の場合はtrueに設定
formEditor.RadioButtonItemSize = 20; // ラジオボタンのサイズ
formEditor.Facade.BorderWidth = 1; // 境界線の幅
formEditor.Facade.BorderColor = System.Drawing.Color.Black; // 境界線の色
```

これらのプロパティは、PDFでラジオボタンがどのように表示されるかを定義するのに役立ちます。 `RadioGap` プロパティはボタン間のスペースを制御し、 `RadioHoriz` レイアウトを決定します。

## ステップ4: 水平ラジオボタンを追加する

ここで、PDF に水平ラジオ ボタンを追加してみましょう。

```csharp
formEditor.Items = new string[] { "First", "Second", "Third" };
formEditor.AddField(FieldType.Radio, "NewField1", 1, 40, 600, 120, 620);
```

このコードでは、ラジオボタンの項目を定義し、PDFに追加します。 `AddField` このメソッドは、フィールド タイプ、フィールド名、配置の座標など、いくつかのパラメータを取ります。

## ステップ5: 垂直ラジオボタンを追加する

次に、縦向きのラジオボタンを追加します。そのためには、向きを縦向きに戻す必要があります。

```csharp
formEditor.RadioHoriz = false; // 垂直方向の配置の場合は false に設定
formEditor.Items = new string[] { "First", "Second", "Third" };
formEditor.AddField(FieldType.Radio, "NewField2", 1, 40, 500, 60, 550);
```

前と同じように項目を定義して PDF に追加しますが、今回は垂直に揃えます。

## ステップ6: PDFドキュメントを保存する

最後に、変更した PDF ドキュメントを保存する必要があります。

```csharp
dataDir = dataDir + "HorizontallyAndVerticallyRadioButtons_out.pdf";
formEditor.Save(dataDir);
Console.WriteLine("\nHorizontally and vertically laid out radio buttons successfully.\nFile saved at " + dataDir);
```

このコードは、新しく追加されたラジオボタンを含むPDFを保存します。出力ファイルは指定されたディレクトリに保存されていることを確認してください。

## 結論

Aspose.PDF for .NET を使えば、PDF フォームにラジオボタンを簡単に作成できます。このチュートリアルで説明する手順に従えば、PDF フォームに水平方向と垂直方向の両方のラジオボタンを簡単に追加できます。これにより、ドキュメントのインタラクティブ性が向上するだけでなく、ユーザーエクスペリエンス全体も向上します。ぜひお試しください。

## よくある質問

### Aspose.PDF for .NET とは何ですか?
Aspose.PDF for .NET は、開発者がプログラムによって PDF ドキュメントを作成、操作、変換できるようにする強力なライブラリです。

### Aspose.PDF は無料で使用できますか?
はい、Asposeはライブラリを評価するための無料トライアル版を提供しています。ダウンロードしてご利用ください。 [ここ](https://releases。aspose.com/).

### Aspose.PDF のサポートを受けるにはどうすればよいですか?
サポートを受けるには、 [Asposeフォーラム](https://forum。aspose.com/c/pdf/10).

### Aspose.PDF で他のフォーム要素を作成することは可能ですか?
もちろんです! Aspose.PDF は、テキスト フィールド、チェックボックス、ドロップダウンなど、さまざまなフォーム要素をサポートしています。

### Aspose.PDF for .NET はどこで購入できますか?
Aspose.PDF for .NETは以下から購入できます。 [購入ページ](https://purchase。aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}