---
"description": "Aspose.PDF for .NET の Bradley アルゴリズムを使用して PDF を TIFF に変換する方法を学びます。スムーズな変換を実現するためのステップバイステップガイド、前提条件、FAQ をご案内します。"
"linktitle": "ブラッドリーアルゴリズム"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "ブラッドリーアルゴリズム"
"url": "/ja/net/programming-with-images/bradley-algorithm/"
"weight": 30
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ブラッドリーアルゴリズム

## 導入

PDFファイルの操作では、単に読んだり編集したりするだけでなく、画像に変換する必要がある場合もあります。PDFをTIFF画像に変換する強力な方法の一つは、Aspose.PDF for .NETライブラリのBradleyアルゴリズムを使用することです。この方法は、ドキュメントのアーカイブ化やその他の特殊なユースケースに最適な、高品質のバイナリ画像を生成します。

このチュートリアルでは、Bradley二値化アルゴリズムを用いてPDFページをTIFF画像に変換するプロセスを、詳細かつ分かりやすく解説します。Aspose.PDF for .NETは、このタスクを簡素化し、ドキュメントワークフローの自動化と効率化を実現します。

## 前提条件

コードに進む前に、必要なすべてのものが揃っていることを確認しましょう。

- Aspose.PDF for .NET: ライブラリが必要です。こちらからダウンロードしてください。 [ここ](https://releases。aspose.com/pdf/net/).
- Visual Studio (または任意の C# IDE)。
- C# の基礎知識。
- 有効な免許証または [一時ライセンス](https://purchase.aspose.com/temporary-license/) Aspose から。

## パッケージのインポート

まず最初に、プロジェクトに必要な名前空間をインポートしてください。これらのライブラリは、PDFドキュメントの操作、TIFF形式への変換、そしてBradley二値化アルゴリズムの適用に必要なツールを提供します。

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

スムーズに理解していただけるよう、プロセスを簡単なステップに分解して解説します。このガイドを読み終える頃には、Bradleyアルゴリズムを使ってPDFページをバイナリTIFF画像に変換できるようになります。

## ステップ1: ドキュメントディレクトリを設定する

最初のステップは、PDFドキュメントが保存されているディレクトリへのパスを指定することです。また、生成されるTIFF画像の出力パスも定義します。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // PDFファイルへのパス
```

ここには、元のPDFファイルと変換後のTIFFファイルの両方が保存されます。コードがエラーなくファイルを読み書きできるように、ディレクトリが適切に設定されていることを確認してください。

## ステップ2: PDFドキュメントを開く

パスが設定されたら、変換したいPDFドキュメントを開きます。Aspose.PDF for .NETを使えば、ドキュメントを簡単に読み込み、さらに処理を進めることができます。

```csharp
Document pdfDocument = new Document(dataDir + "PageToTIFF.pdf");
```

ここ、 `PageToTIFF.pdf` はサンプルファイルです。任意のPDFファイルに置き換えることができます。ドキュメントオブジェクトは、その後の操作のためにPDFを保持します。

## ステップ3: 画像の出力パスを定義する

次に、標準 TIFF とバイナリ化されたバージョンの両方を含む、生成された TIFF ファイルの出力パスを指定します。

```csharp
string outputImageFile = dataDir + "resultant_out.tif";
string outputBinImageFile = dataDir + "37116-bin_out.tif";
```

これらのパスを分離することで、標準の TIFF 変換用のファイルと、Bradley アルゴリズムを適用した後の 2 値化画像用のファイルが 1 つずつ作成されます。

## ステップ4: 解決オブジェクトを作成する

PDFをTIFFに変換する際、解像度は画質を決定づける重要な要素となります。ここでは、高画質出力を実現するために、解像度を300DPIに設定します。

```csharp
Resolution resolution = new Resolution(300);
```

DPI が高いほど、特に印刷またはアーカイブされるドキュメントを扱う場合に、画像の鮮明度が向上します。

## ステップ5: TIFF設定を構成する

次に、TIFF画像の設定を行います。ここでは、LZW圧縮を使用し、色深度を1bpp（1ピクセルあたり1ビット）に設定して、2値画像を作成します。

```csharp
TiffSettings tiffSettings = new TiffSettings();
tiffSettings.Compression = CompressionType.LZW;
tiffSettings.Depth = Aspose.Pdf.Devices.ColorDepth.Format1bpp;
```

深度を1bppに設定することで、画像をバイナリ出力用に準備します。LZW圧縮は、画質を損なうことなくファイルサイズを効率的に削減できるため、選択されています。

## ステップ6: TIFFデバイスを作成する

次に、変換を処理するTIFFデバイスを作成する必要があります。このデバイスは、先ほど定義した解像度とTIFF設定を使用します。

```csharp
TiffDevice tiffDevice = new TiffDevice(resolution, tiffSettings);
```

TIFFデバイスはこの操作の中核です。PDF文書を読み込み、事前定義された設定に基づいて各ページをTIFF画像に変換します。

## ステップ7: PDFページをTIFFに変換する

PDFを処理して最初のページをTIFF画像に変換します。 `Process` このメソッドを使用すると、特定のページまたはドキュメント全体を変換できます。この例では、最初のページを変換します。

```csharp
tiffDevice.Process(pdfDocument, outputImageFile);
```

メソッドが完了すると、前に定義した場所に TIFF 画像が保存されます。

## ステップ8: Bradley二値化アルゴリズムを適用する

いよいよ魔法の登場です。ブラッドリーアルゴリズムです！このアルゴリズムは、グレースケールのTIFF画像をバイナリ画像に変換し、ドキュメント認識システム向けに最適化します。

```csharp
using (FileStream inStream = new FileStream(outputImageFile, FileMode.Open))
{
    using (FileStream outStream = new FileStream(outputBinImageFile, FileMode.Create))
    {
        tiffDevice.BinarizeBradley(inStream, outStream, 0.1);
    }
}
```

BinarizeBradleyメソッドは、2つのファイルストリーム（入力と出力）としきい値（ここでは、 `0.1`）は二値化レベルを決定します。実行後、完璧に二値化された画像がすぐに使用できるようになります。

## ステップ9: 変換が成功したことを確認する

最後に、プロセスが成功したことをユーザーに知らせることをお勧めします。これは、シンプルなコンソール出力で行うことができます。

```csharp
System.Console.WriteLine("Conversion using Bradley algorithm performed successfully!");
```

これが印刷されると、PDF ページがバイナリ TIFF 画像に正常に変換されたことがわかります。

## 結論

これで完了です！Aspose.PDF for .NET を使用して、PDF ページを TIFF 画像に変換し、Bradley 二値化アルゴリズムを適用する方法を学習しました。このプロセスは、ドキュメントのアーカイブ、光学式文字認識 (OCR)、その他の専門的なアプリケーションに不可欠です。高画質と効率的な圧縮により、ドキュメント画像は鮮明でありながら扱いやすいサイズに保たれます。

## よくある質問

### ブラッドリーアルゴリズムとは何ですか?
ブラッドリー アルゴリズムは、周囲の環境に基づいて各ピクセルの適応しきい値を決定することにより、グレースケール画像をバイナリ (白黒) 画像に変換するバイナリ化手法です。

### この方法を使用して複数の PDF ページを TIFF に変換できますか?
はい、変更できます `Process` ドキュメント内のページをループしてすべてのページを変換するメソッド。

### PDF を TIFF に変換する場合の最適な解像度は何ですか?
高画質画像の場合、通常は300DPIが推奨されます。ただし、必要に応じてこの値を調整できます。

### 色深度における 1bpp とはどういう意味ですか?
1bpp (ピクセルあたり 1 ビット) は、画像が白黒になり、各ピクセルが完全に黒か完全に白になることを意味します。

### Bradley アルゴリズムは OCR に適していますか?
はい、ブラッドリー アルゴリズムは、スキャンされたドキュメント内のテキストのコントラストを強調するため、OCR の前処理でよく使用されます。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}