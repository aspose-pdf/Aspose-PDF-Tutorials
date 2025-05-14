---
"description": "Aspose.PDF for .NET を使用して、PDF ドキュメントからデジタル署名と証明書情報を抽出する方法を学びましょう。C# 開発者向けの完全なステップバイステップガイドです。"
"linktitle": "署名情報の抽出"
"second_title": "Aspose.PDF for .NET API リファレンス"
"title": "署名情報の抽出"
"url": "/ja/net/programming-with-security-and-signatures/extract-signature-info/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 署名情報の抽出

## 導入

今日のデジタル世界では、ドキュメントのセキュリティと整合性を確保することが極めて重要です。PDFを保護するための一般的な方法の一つは、デジタル署名の追加です。しかし、署名の詳細を取得して検証することは、特に複数の証明書を扱う場合は困難になることがあります。このガイドでは、Aspose.PDF for .NETを使用してPDFドキュメントから署名情報を抽出するプロセスを詳しく説明し、この作業を容易にします。署名フィールドへのアクセス方法、証明書情報の抽出方法、そしてファイルへの保存方法を学習します。

## 前提条件

始める前に、すべて準備が整っていることを確認しましょう。

- Aspose.PDF for .NETライブラリ:まだお持ちでない場合は、以下からダウンロードできます。 [Aspose.PDF for .NET のダウンロード ページ](https://releases。aspose.com/pdf/net/). 
- .NET 開発環境: Visual Studio などの IDE が必要です。
- 基本的な C# の知識: C# の知識は、このチュートリアルのコード スニペットを理解するのに役立ちます。
- デジタル署名付きの PDF ドキュメント: テストのために、少なくとも 1 つのデジタル署名が含まれる PDF ファイルがあることを確認してください。

## 必要な名前空間のインポート

コードに進む前に、必要な名前空間をインポートすることが重要です。これらの名前空間により、Aspose.PDF の機能にアクセスし、PDF ドキュメントを操作できるようになります。

```csharp
using System.IO;
using Aspose.Pdf.Forms;
using Aspose.Pdf;
using System;
```

基本的な設定が完了したら、PDF から署名情報を抽出する実際のプロセスに進みましょう。

## ステップ1: ドキュメントディレクトリの設定

PDF文書で作業する前に、使用するファイルの場所を指定する必要があります。 `"YOUR DOCUMENT DIRECTORY"` PDF が保存されているディレクトリの実際のパスを入力します。

```csharp
// ドキュメント ディレクトリへのパス。
string dataDir = "YOUR DOCUMENT DIRECTORY";
string input = dataDir + "ExtractSignatureInfo.pdf";
```

ここでは、PDFファイルを含むディレクトリとファイル名を指定します。ファイルがそのディレクトリに存在することを確認してください。

## ステップ2: PDFドキュメントの読み込み

ディレクトリの設定が完了したら、次のステップは、 `Document` Aspose.PDF からのクラス。

```csharp
using (Document pdfDocument = new Document(input))
{
    // ここでPDFを処理します。
}
```

このコード行は、 `Document` PDFファイルを表すオブジェクト。 `using` ステートメントは、ドキュメントが処理された後にリソースがクリーンアップされることを保証します。

## ステップ3: フォームフィールドへのアクセス

このステップでは、PDF文書内のすべてのフォームフィールドをループ処理します。署名は通常フォームフィールドとして保存されるため、このステップは署名フィールドを識別するのに役立ちます。

```csharp
foreach (Field field in pdfDocument.Form)
{
    // ここで署名フィールドを識別します。
}
```

反復処理によって `Form` の財産 `Document` オブジェクトを使用すると、各フォーム フィールドを調べて、署名フィールドであるかどうかを確認できます。

## ステップ4: 署名フィールドの識別

フォームフィールドにアクセスしたら、次のステップは署名フィールドを識別することです。これは、各フィールドを `SignatureField` 物体。

```csharp
SignatureField sf = field as SignatureField;
if (sf != null)
{
    // 署名情報を抽出します。
}
```

ここでは、 `as` 各フォームフィールドを `SignatureField`キャストが成功した場合、フィールドが署名であることがわかります。

## ステップ5: 証明書の抽出

署名フィールドを特定したら、次は署名から証明書を抽出します。証明書には、署名者と署名の有効性に関する重要な情報が含まれています。

```csharp
Stream cerStream = sf.ExtractCertificate();
```

その `ExtractCertificate` メソッドは `Stream` 証明書データを含むオブジェクト。このストリームは、証明書を保存して、さらに分析したり保管したりするために使用できます。

## ステップ6: 証明書をファイルに保存する

証明書を抽出したら、最後のステップはそれをファイルに保存することです。今回は、証明書を `.cer` ファイル。

```csharp
if (cerStream != null)
{
    using (cerStream)
    {
        byte[] bytes = new byte[cerStream.Length];
        using (FileStream fs = new FileStream(dataDir + @"input.cer", FileMode.CreateNew))
        {
            cerStream.Read(bytes, 0, bytes.Length);
            fs.Write(bytes, 0, bytes.Length);
        }
    }
}
```

このコード ブロックでは、次の操作を行います。

1. 証明書ストリームが null でないかどうかを確認します。
2. 証明書データをバイト配列に読み取ります。
3. バイト配列を `.cer` ドキュメントディレクトリ内のファイル。

## 結論

Aspose.PDF for .NET を使って PDF ドキュメントからデジタル署名と関連する証明書情報を抽出するのは、シンプルな手順に分解すれば非常に簡単です。ドキュメントの監査、署名の検証、あるいは証明書の保管など、どんな作業でも、このチュートリアルを読めば効率的に作業を進めるための知識が得られます。今日のデジタル社会において、ドキュメントのセキュリティ確保と検証は極めて重要であり、Aspose.PDF for .NET のようなツールを使えば、はるかに簡単に処理できます。

## よくある質問

### Aspose.PDF for .NET を使用して PDF から複数の署名を抽出できますか?
はい、コードはドキュメント内のすべてのフォーム フィールドをループし、複数の署名が存在する場合にそれを抽出できます。

### PDF に署名が見つからない場合はどうなりますか?
署名フィールドが存在しない場合は、コードはエラーをスローせずに署名フィールドをスキップします。

### この方法を使用して署名の有効性を検証できますか?
証明書を抽出することはできますが、署名の有効性を検証するには、証明書の信頼チェーンを確認するなどの追加の手順が必要です。

### Aspose.PDF for .NET を使用して他のフォーム フィールド データを抽出することは可能ですか?
はい、Aspose.PDF を使用すると、署名フィールドだけでなく、PDF 内のさまざまな種類のフォーム フィールドにアクセスして操作できます。

### 抽出した証明書の詳細を表示するにはどうすればいいですか?
証明書が `.cer` ファイルは、任意の証明書ビューアを使用して開くことも、システム証明書ストアにインポートしてさらに検査することもできます。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}