---
"description": "Aspose.PDF for .NET を使って PDF のページの向きを変更する手順をステップバイステップで説明します。手順は簡単で、プロジェクトに簡単に実装できます。"
"linktitle": "方向転換"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "方向転換"
"url": "/ja/net/programming-with-pdf-pages/change-orientation/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 方向転換

## 導入

PDFファイルのページの向きがどうしても…ずれてしまって困ったことはありませんか？スキャンや作成が不完全なドキュメントを扱っていて、ページを回転させないと意味が通じない、なんて経験はありませんか？Aspose.PDF for .NETを使えば、ページの向きの変更を含め、あらゆる方法でPDFファイルを操作できる、簡単かつパワフルなツールが手に入ります。縦向きから横向きへ、あるいはその逆へ切り替えたい場合でも、このガイドでは手順をステップバイステップで解説します。

では、PDF ページを簡単に回転させる準備ができたら、始めましょう。

## 前提条件

PDF のページの向きを変更する詳細に入る前に、必要な準備について簡単に説明しておきましょう。

- Aspose.PDF for .NET: Aspose.PDFライブラリが.NET用にインストールされていることを確認してください。まだインストールされていない場合は、 [ここからダウンロード](https://releases。aspose.com/pdf/net/).
- .NET 開発環境: .NET での作業には、Visual Studio、JetBrains Rider、または任意の IDE を使用できます。
- C# の基本知識: このガイドはわかりやすいものですが、C# の基本を理解しておくと、さらに理解しやすくなります。
- PDFファイル: 以下の例では、複数ページのPDFファイルがあることを前提としています。お手元にPDFファイルがない場合は、サンプルPDFを作成またはダウンロードしてご利用ください。

また、まだ始めたばかりの場合は、Aspose.PDFを試してみるといいでしょう。 [無料の一時ライセンス](https://purchase.aspose.com/temporary-license/) 決める前に [フルバージョンを購入する](https://purchase。aspose.com/buy).

## 名前空間のインポート

PDFのページの向きを操作する前に、C#プロジェクトに必要な名前空間をインポートする必要があります。以下のことを確認してください。

```csharp
using System.IO;
using Aspose.Pdf;
```

これをインポートしたら、チュートリアルのメイン部分に進みましょう。

## ステップ1: PDFドキュメントを読み込む

まず最初に、変更したいPDFファイルを読み込みます。 `Document` PDF を開くには、Aspose.PDF 名前空間のクラスを使用します。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document(dataDir + "input.pdf");
```

この行は、指定したディレクトリからPDFを読み込みます。 `"YOUR DOCUMENT DIRECTORY"` ファイルの実際のパスを入力します。 `"input.pdf"` 方向を変更する PDF です。

## ステップ2: 各ページをループする

ドキュメントが読み込まれたので、PDFの各ページをループしてみましょう。 `foreach` ループしてすべてのページを巡回し、すべてのページに向きの変更を適用できるようにします。

```csharp
foreach (Page page in doc.Pages)
{
    // 各ページを操作する
}
```

このループはドキュメント内のすべてのページを反復処理します。

## ステップ3: ページのメディアボックスを取得する

PDFの各ページには `MediaBox` ページの境界を定義する要素です。現在の向きを判定し、変更するには、この要素にアクセスする必要があります。

```csharp
Aspose.Pdf.Rectangle r = page.MediaBox;
```

その `MediaBox` ページの幅、高さ、位置などの寸法がわかります。

## ステップ4：幅と高さを入れ替える

ページの向きを縦向きから横向きへ、または横向きから縦向きへ変更するには、幅と高さの値を入れ替えるだけです。この手順でページのサイズを調整できます。

```csharp
double newHeight = r.Width;
double newWidth = r.Height;
double newLLX = r.LLX;
double newLLY = r.LLY + (r.Height - newHeight);
```

このコードは高さと幅を入れ替え、左下隅の位置を変更します（`LLY`）を使用して、回転後にコンテンツがきれいに収まるようにします。

## ステップ5: MediaBoxとCropBoxを更新する

新しい高さと幅ができたので、ページに変更を適用してみましょう。 `MediaBox` そして `CropBox`。その `CropBox` 元のドキュメントに 1 セットしかない場合は、ページ全体が正しく表示されるようにするために不可欠です。

```csharp
page.MediaBox = new Aspose.Pdf.Rectangle(newLLX, newLLY, newLLX + newWidth, newLLY + newHeight);
page.CropBox = new Aspose.Pdf.Rectangle(newLLX, newLLY, newLLX + newWidth, newLLY + newHeight);
```

この手順では、計算した新しい寸法に基づいてページのサイズを変更します。

## ステップ6: ページを回転する

最後に、ページの回転角度を設定します。Aspose.PDF を使えば、これは非常に簡単に設定できます。ページを90度回転させて、縦向きから横向き、またはその逆に変更できます。

```csharp
page.Rotate = Rotation.on90;
```

このコードはページを 90 度回転し、希望の方向に反転します。

## ステップ7: 出力PDFを保存する

すべてのページに向きの変更を適用した後、変更されたドキュメントを新しいファイルに保存します。 

```csharp
dataDir = dataDir + "ChangeOrientation_out.pdf";
doc.Save(dataDir);
System.Console.WriteLine("\nPage orientation changed successfully.\nFile saved at " + dataDir);
```

新しいファイル名を必ず入力してください（この場合は `ChangeOrientation_out.pdf`）をクリックして出力を保存します。これにより、元のファイルが上書きされることはありません。

### 結論

これで完了です！Aspose.PDF for .NET を使って PDF ファイルのページの向きを変更するのは、ドキュメントを読み込み、ページをループ処理し、MediaBox を調整して、更新したファイルを保存するだけです。スキャン品質の悪いドキュメントを扱う場合でも、書式設定に合わせてページを回転させる必要がある場合でも、このステップバイステップガイドが役立ちます。

## よくある質問

### PDF 内のすべてのページではなく、特定のページを回転できますか?  
はい、すべてのページをループするのではなく、インデックスを使用して特定のページをターゲットにするようにループを変更できます。

### 何ですか `MediaBox`？  
その `MediaBox` PDFファイルのページのサイズと形状を定義します。ページのコンテンツが配置される場所です。

### Aspose.PDF for .NET は他のファイル形式でも動作しますか?  
はい、Aspose.PDF は HTML、XML、XPS など、さまざまなファイル形式を処理できます。

### Aspose.PDF for .NET の無料版はありますか?  
はい、始めることができます [無料トライアル](https://releases.aspose.com/) またはリクエスト [一時ライセンス](https://purchase。aspose.com/temporary-license/).

### 一度保存した変更を元に戻すことはできますか?  
ドキュメントを保存すると、変更は永続的に保存されます。必ずコピーで作業するか、元のファイルのバックアップを保存してください。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}