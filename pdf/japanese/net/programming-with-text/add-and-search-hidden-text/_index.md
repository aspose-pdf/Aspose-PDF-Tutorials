---
"description": "Aspose.PDF for .NET を使用して、PDF ドキュメントに隠しテキストを追加および検索する方法を学びます。コード例を含むステップバイステップのガイドです。"
"linktitle": "PDFファイルに隠しテキストを追加して検索する"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "PDFファイルに隠しテキストを追加して検索する"
"url": "/ja/net/programming-with-text/add-and-search-hidden-text/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDFファイルに隠しテキストを追加して検索する

## 導入

このチュートリアルでは、Aspose.PDF for .NET を使用して PDF ファイルに隠しテキストを追加および検索する方法をステップバイステップで解説します。経験豊富な開発者の方でも、プログラミングスキルの向上を目指す初心者の方でも、この記事はアプリケーションに隠しテキスト機能を組み込むために必要な情報を提供します。

## 前提条件

コーディング部分に進む前に、満たしておく必要のある前提条件がいくつかあります。

### 要件チェックリスト
- Visual Studio: Visual Studioがインストールされていることを確認してください。このチュートリアルでは、.NET Frameworkを使用していることを前提としています。
- Aspose.PDF for .NET: Aspose.PDF for .NETライブラリが必要です。ダウンロードできます。 [ここ](https://releases。aspose.com/pdf/net/).
- C# の基礎知識: C# プログラミングに精通していると、コード スニペットをよりよく理解できるようになります。

## パッケージのインポート

コードを書き始める前に、必要なAspose.PDF名前空間をインポートする必要があります。手順は以下のとおりです。

### プロジェクトの設定
1. Visual Studio を開き、新しい C# プロジェクトを作成するか、既存のプロジェクトを使用します。
2. Aspose.PDFをインストールするには、NuGetパッケージを追加します。NuGetパッケージマネージャーに移動し、以下を検索してください。 `Aspose。PDF`. 
3. あるいは、以下のサイトから直接ライブラリをダウンロードすることもできます。 [ここ](https://releases.aspose.com/pdf/net/) プロジェクトに参照として追加します。

### 必要な名前空間をインポートする
C# ファイルの先頭で、次の名前空間をインポートします。

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

これらの名前空間には PDF ドキュメントを操作するために必要なクラスとメソッドが含まれているため、この手順は重要です。

## 隠しテキストを含むPDF文書の作成

準備が完了したら、可視テキストと不可視テキストの両方を含む PDF ドキュメントを作成する手順を確認しましょう。

### ステップ1: ドキュメントディレクトリを定義する
まず、PDFを保存するパスを設定します。ここから魔法が始まります！

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // これをあなたのディレクトリに変更してください
```

この行は生成されたPDFの保存場所を定義します。 `YOUR DOCUMENT DIRECTORY` 実際のパスを入力します。

### ステップ2: PDFドキュメントを作成する
次に、新しい PDF ドキュメントを作成し、ページを追加してみましょう。

```csharp
Aspose.Pdf.Document doc = new Aspose.Pdf.Document();
Page page = doc.Pages.Add();
```

ここでは、新しいドキュメントを初期化し、テキストフラグメントを配置するページを追加します。

### ステップ3: 表示テキストと非表示テキストを追加する
ここで、表示可能なテキストと非表示のテキストの両方を PDF に追加します。

```csharp
TextFragment frag1 = new TextFragment("This is common text.");
TextFragment frag2 = new TextFragment("This is invisible text.");
```

このスニペットでは、 `frag1` 表示されますが、 `frag2` 次は非表示に設定されます。

### ステップ4：テキストを非表示にする
テキストを作成するには `frag2` 目に見えない場合は、単に `TextState`。

```csharp
frag2.TextState.Invisible = true;
```

このプロパティを設定すると、 `frag2` PDF を表示するときにはレンダリングされません。

### ステップ5: ページにテキストフラグメントを追加する
最後に、これらのテキストフラグメントをページに追加し、PDF を保存します。

```csharp
page.Paragraphs.Add(frag1);
page.Paragraphs.Add(frag2);
doc.Save(dataDir + "39400_out.pdf");
doc.Dispose();
```

このコード部分では、テキストフラグメントをページに追加します。その後、ドキュメントを適切に保存して破棄します。

## PDF内の隠しテキストの検索

表示テキストと非表示テキストの両方を含む PDF を作成しましたが、非表示テキストを検索するにはどうすればよいでしょうか。詳しく見ていきましょう。

### ステップ1: PDFドキュメントを読み込む
PDF 内のテキストを検索するには、まず、作成したドキュメントを読み込む必要があります。

```csharp
doc = new Aspose.Pdf.Document(dataDir + "39400_out.pdf");
```

### ステップ2: テキストフラグメント吸収体を作成する
我々は `TextFragmentAbsorber` PDF 内のすべてのテキスト断片をキャプチャします。

```csharp
TextFragmentAbsorber absorber = new TextFragmentAbsorber();
absorber.Visit(doc.Pages[1]);
```

ここでは、最初のページからすべてのテキストフラグメントを吸収することを指定します。

### ステップ3: フラグメントを反復処理する
これで、収集されたテキストフラグメントを反復処理して、どれが表示され、どれが非表示になっているかを確認できます。

```csharp
foreach (TextFragment fragment in absorber.TextFragments)
{
    Console.WriteLine("Text '{0}' on pos {1} invisibility: {2}",
        fragment.Text, fragment.Position.ToString(), fragment.TextState.Invisible);
}
```

このループは各テキストフラグメントをチェックし、その内容、位置、可視性の状態を出力します。 `fragment.TextState.Invisible` true に設定すると、テキストが非表示になります。

### ステップ4：文書を廃棄する
最後に、作業が終わったら必ず文書を廃棄してください。

```csharp
doc.Dispose();
```

## 結論

このチュートリアルでは、Aspose.PDF for .NET を使用して PDF ファイルに隠しテキストを追加し、検索するプロセスを詳しく解説しました。表示テキストと隠しテキストの両方を含む PDF ドキュメントを作成する方法と、プログラムで隠しテキストを検索する方法を学習しました。この機能は、機密情報を保存する必要がある場合でも、ドキュメント内で独自のユーザーエクスペリエンスを提供する必要がある場合でも、さまざまなアプリケーションで非常に役立ちます。

ASPose.PDFに慣れてくると、可能性は無限に広がります。ぜひ実験を続け、PDFドキュメントの可能性の限界を広げてください！

## よくある質問

### Aspose.PDF は暗号化された PDF ファイルを処理できますか?  
はい、Aspose.PDF は PDF ドキュメントの暗号化と復号化をサポートしています。パスワードを設定すれば、PDF を簡単に保護できます。

### Aspose.PDF の試用版はありますか?  
もちろんです！無料トライアルはこちらからダウンロードできます。 [ここ](https://releases。aspose.com/).

### Aspose.PDF はどのようなプログラミング言語をサポートしていますか?  
Aspose.PDF は、C#、Java、Python など複数の言語をサポートしています。

### Aspose.PDF のドキュメントはどこにありますか?  
ドキュメントにアクセスできます [ここ](https://reference。aspose.com/pdf/net/).

### 問題が発生した場合、どうすればサポートを受けることができますか?  
サポートについては、Asposeフォーラムをご覧ください。 [ここ](https://forum。aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}