---
"date": "2025-04-10"
"description": "Aspose.PDF for .NET を使用して、TrueType (TTF) および Web Open Font Format (WOFF) フォントを維持しながら PDF を HTML に変換する方法を学びます。コード例を交えたステップバイステップのガイドです。"
"title": "Aspose.PDF for .NET で PDF を HTML に変換し、TTF および WOFF 形式でフォントを保持します"
"url": "/ja/net/conversion-export/convert-pdf-html-aspose-net-truetype-woff/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Aspose.PDF for .NET で PDF を HTML に変換: TTF および WOFF 形式でフォントを保持

## 導入
PDF文書をHTMLに変換する際、元のレイアウトやフォントの整合性を維持するのに苦労していませんか？フォントを保持しながらPDFを変換するのは難しい場合がありますが、そうする必要はありません。 **Aspose.PDF .NET 版**を使えば、TrueType（TTF）またはWeb Open Font Format（WOFF）フォントを維持しながら、PDFファイルをHTML形式に簡単に変換できます。このガイドでは、その手順をステップバイステップで解説します。

このチュートリアルでは、次の内容を取り上げます。
- PDFをHTMLに変換するときにフォントをTTFとして保存する方法
- フォントをWOFFとして保存するための変換の設定
- 変換中にすべての形式でフォントを保存する

この記事を読み終える頃には、Aspose.PDF for .NET を使ってフォント変換を効果的に管理する方法を包括的に理解できるようになります。では、始める前に必要な前提条件を見ていきましょう。

## 前提条件
Aspose.PDF を使用して PDF を HTML に変換する前に、次の要件を満たしていることを確認してください。

### 必要なライブラリと依存関係
- **Aspose.PDF .NET 版**このライブラリは、.NET アプリケーションで PDF ファイルを処理するために不可欠です。
- **.NET Framework または .NET Core/5+**: 開発環境がこれらのフレームワークをサポートしていることを確認してください。

### 環境設定要件
開発環境（Visual Studio など）が Aspose.PDF ライブラリに対応していることを確認してください。以下のものが必要です。
- .NET Framework または .NET Core/5+ で作成されたプロジェクト
- ライブラリをインストールするための NuGet パッケージ マネージャーへのアクセス

### 知識の前提条件
C# の基本的な理解と .NET でのファイル処理に関する知識があると役立ちます。

## Aspose.PDF for .NET のセットアップ
始めるには、Aspose.PDFライブラリをインストールする必要があります。これは、以下のパッケージマネージャーから実行できます。

**.NET CLI:**
```bash
dotnet add package Aspose.PDF
```

**パッケージ マネージャー コンソール:**
```powershell
Install-Package Aspose.PDF
```

**NuGet パッケージ マネージャー UI:**
「Aspose.PDF」を検索し、最新バージョンをインストールしてください。

### ライセンス取得
Aspose では、一時ライセンスを取得するか、フルライセンスをご購入いただけます。無料トライアルでは、すべての機能を制限なくお試しいただけますので、初期評価に最適です。ライセンスを使用して環境を設定する手順は以下のとおりです。
1. リクエスト [一時ライセンス](https://purchase。aspose.com/temporary-license/).
2. 操作を実行する前に、次のコード スニペットを使用してアプリケーションにライセンスを適用します。

```csharp
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Path to your License File");
```

## 実装ガイド
実装を、フォントを TTF、WOFF、およびすべての形式で保存するという 3 つの主要機能に分けて見てみましょう。

### フォントをTTFとして保存
**概要**
この機能を使用すると、PDF文書をHTMLに変換する際、フォントをTrueType形式（TTF）で保存できます。これにより、変換中にフォントの視覚的な整合性が維持されます。

#### ステップバイステップの実装
1. **ドキュメントとオプションを初期化します:**
   まずAspose.PDFを使ってPDF文書を読み込みましょう `Document` クラスとセットアップ `HtmlSaveOptions`。

   ```csharp
   string dataDir = "YOUR_DOCUMENT_DIRECTORY";
   string outFile = Path.GetFullPath(dataDir + "/36192_out.html");
   Document doc = new Document(dataDir + "/input.pdf");

   HtmlSaveOptions saveOptions = new HtmlSaveOptions();
   ```

2. **保存オプションを設定します。**
   レイアウトを維持し、フォント保存モードを指定するために必要なオプションを設定します。

   ```csharp
   saveOptions.FixedLayout = true; // 元のPDFレイアウトを維持する
   saveOptions.SplitIntoPages = false; // 複数のHTMLファイルに分割しないでください
   saveOptions.FontSavingMode = HtmlSaveOptions.FontSavingModes.AlwaysSaveAsTTF;
   ```

3. **出力ディレクトリの準備:**
   出力ディレクトリがリンクされたフォント ファイルを保存できる状態であることを確認します。

   ```csharp
   string linkedFilesFolder = Path.GetDirectoryName(outFile) + "/36192_files";
   if (Directory.Exists(linkedFilesFolder))
   {
       Directory.Delete(linkedFilesFolder, true); // 既存のファイルを消去する
   }
   ```

4. **ドキュメントを保存します:**
   最後に、指定したオプションでドキュメントを保存します。

   ```csharp
doc.Save(outFile、saveOptions);
```

### Save Fonts as WOFF
**Overview**
Configuring Aspose.PDF to save fonts in Web Open Font Format (WOFF) is beneficial for web optimization, reducing font file sizes while maintaining quality.

#### Step-by-Step Implementation
1. **Configure Save Options:**
   Initialize `HtmlSaveOptions` and set the font saving mode to WOFF.

   ```csharp
   HtmlSaveOptions woffSaveOptions = new HtmlSaveOptions();
   woffSaveOptions.FontSavingMode = HtmlSaveOptions.FontSavingModes.AlwaysSaveAsWOFF;
   ```

2. **保存オプションを適用:**
   TTF 方式と同様に、ドキュメントを保存するときにこれらのオプションを使用します。

### あらゆる形式でフォントを保存
**概要**
最大限の互換性と柔軟性を確保するには、変換中にフォントを利用可能なすべての形式で保存することをお勧めします。

#### ステップバイステップの実装
1. **ドキュメントとオプションを初期化します:**
   PDF文書を読み込み、設定する `HtmlSaveOptions`。

   ```csharp
   string dataDir = "YOUR_DOCUMENT_DIRECTORY";
   Document doc = new Document(dataDir + "/input.pdf");
   HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
   ```

2. **保存オプションを設定します。**
   すべてのフォント形式を保存し、レイアウトを維持するオプションを設定します。

   ```csharp
   htmlOptions.FixedLayout = true;
   htmlOptions.RasterImagesSavingMode = HtmlSaveOptions.RasterImagesSavingModes.AsExternalPngFilesReferencedViaSvg;
   htmlOptions.FontSavingMode = HtmlSaveOptions.FontSavingModes.SaveInAllFormats;
   ```

3. **ドキュメントを保存します:**
   これらの設定でドキュメントを保存します。

   ```csharp
doc.Save(dataDir + "/ThreeSetFonts_out.html", htmlOptions);
```

## Practical Applications
Converting PDFs to HTML with font preservation has numerous real-world applications:
1. **Web Publishing**: Ensure that documents retain their original styling when published online.
2. **Content Portability**: Easily move content between desktop and web environments without loss of formatting.
3. **Document Archiving**: Maintain document integrity during long-term storage or migration.

Integration possibilities include embedding these conversions into CMS systems, automated reporting tools, or digital libraries for seamless font management across platforms.

## Performance Considerations
When using Aspose.PDF for .NET, consider the following tips to optimize performance:
- **Memory Management**: Dispose of objects properly and utilize `using` statements where applicable.
- **Batch Processing**: Process documents in batches if dealing with large volumes to prevent memory overflow.
- **Resource Optimization**: Configure options like image compression and font subsetting to reduce file sizes.

## Conclusion
We've explored how to convert PDFs to HTML while preserving fonts using Aspose.PDF for .NET. Whether saving fonts as TTF, WOFF, or all formats, these techniques ensure your documents maintain their original design and readability in web environments. 

For further exploration, consider diving into Aspose's extensive documentation or experimenting with additional conversion features offered by the library.

## FAQ Section
1. **What are the benefits of converting PDFs to HTML using Aspose.PDF?**
   - Maintains document layout and font integrity.
   - Facilitates web publishing and content portability.
2. **Can I convert large PDF files efficiently with Aspose.PDF?**
   - Yes, by optimizing memory usage and processing in batches.
3. **How do I handle licensing for Aspose.PDF?**
   - Obtain a temporary or full license from the [Aspose website](https://purchase.aspose.com/buy).
4. **Is it possible to customize font settings during conversion?**
   - Yes, through various `HtmlSaveOptions`.
5. **What are some common issues when converting PDFs and how can I address them?**
   - Common issues include missing fonts or layout discrepancies. Adjusting save options and ensuring proper licensing can help mitigate these problems.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}