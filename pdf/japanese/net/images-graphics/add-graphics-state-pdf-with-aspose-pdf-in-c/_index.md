---
category: general
date: 2026-10-07
description: Aspose.Pdf を使用して C# で PDF の透明度を変更するために、グラフィックスステートを追加します。このステップバイステップガイドに従って、カスタムグラフィックスステートを埋め込み、透明度を制御してください。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- modify pdf transparency
language: ja
lastmod: 2026-10-07
og_description: C#でAspose.Pdfを使用してグラフィックスステートPDFを追加します。カスタムグラフィックスステート辞書を作成してPDFの透明度を変更する方法を学びましょう。
og_image_alt: Screenshot showing the add graphics state pdf code editor in Visual
  Studio
og_title: Aspose.PdfでグラフィックスステートPDFを追加 – PDFの透明度を制御
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Add graphics state pdf using Aspose.Pdf in C# to modify PDF transparency.
    Follow this step‑by‑step guide to embed custom graphics states and control opacity.
  headline: Add graphics state pdf with Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: C#でAspose.Pdfを使ってPDFにグラフィックスステートを追加する
url: /ja/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf を使用した C# でのグラフィックスステート PDF の追加

ドキュメントに **add graphics state pdf** を追加する必要がある場合、本チュートリアルでは Aspose.Pdf for .NET を使った具体的な手順を示します。ガイドの最後まで読むと、 **modify PDF transparency** の方法も理解でき、任意の描画操作にカスタム不透明度を設定できるようになります。

PDF のグラフィックスステートを操作すると、線幅やブレンドモードなどのパラメータを制御でき、この記事で最も重要になるのはコンテンツの透明度です。以下の手順は C# に慣れた開発者向けで、公式 SDK ドキュメントを掘り下げることなくすぐに実行できるソリューションを提供します。

## 学べること

* `CA`、`ca`、`BM` エントリを持つ新しいグラフィックスステート辞書を作成し、値を設定する方法。  
* その辞書をページの `ExtGState` リソースに挿入し、PDF に認識させる手順。  
* `ca`（ストローク）と `CA`（塗り）の値が、以降の描画コマンドにおける **modify PDF transparency** にどのように影響するか。  
* 名前衝突やバージョン互換性といった一般的な落とし穴、そしてグラフィックスステートを後から拡張するためのプロのコツ。

**前提条件**

* .NET 6.0 以降（.NET Framework 4.7+ でも動作します）。  
* 有効な Aspose.Pdf for .NET ライセンス（無料評価版でもテストは可能）。  
* Visual Studio 2022 またはお好みの C# IDE。  

---

## 手順 1: Aspose.Pdf for .NET をインストール

プロジェクトに NuGet パッケージを追加します。

```bash
dotnet add package Aspose.Pdf
```

このパッケージには `Aspose.Pdf` 名前空間が含まれ、後述の `Document`、`DictionaryEditor`、`CosPdfDictionary` クラスが利用可能になります。

> **Pro tip:** バッチで多数の PDF を処理する場合は、`Program.cs` の早い段階で **License** を有効化して評価版の透かしを回避してください。

```csharp
// Apply your license (optional for evaluation)
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Aspose.Pdf.lic");
```

## 手順 2: 入出力パスを定義

SDK に既存の PDF（`input.pdf`）を指示し、変更後のファイルを保存する場所（`output.pdf`）を指定します。

```csharp
// Define input and output PDF file paths
string inputPath = @"C:\MyPdfs\input.pdf";
string outputPath = @"C:\MyPdfs\output.pdf";
```

> **Why this matters:** 絶対パスを使用することで、SDK が誤った作業ディレクトリを参照して `FileNotFoundException` が発生するのを防げます。

## 手順 3: PDF を開き、最初のページのリソースを取得

`ExtGState` 辞書は各ページのリソース辞書内にあります。ここではシンプルに最初のページを編集しますが、同様の手順で任意のページインデックスにも適用できます。

```csharp
using (var pdfDocument = new Aspose.Pdf.Document(inputPath))
{
    // Get the first page (pages are 1‑based)
    var firstPage = pdfDocument.Pages[1];

    // Access the page’s resource dictionary via DictionaryEditor
    var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);

    // Retrieve (or create) the ExtGState entry
    var extGStateDict = resourcesEditor["ExtGState"]
        .ToCosPdfDictionary(); // Throws if ExtGState does not exist
```

**Edge case:** ページに `ExtGState` エントリが存在しない場合は、以下のように作成します。

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
{
    var emptyDict = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", emptyDict);
    extGStateDict = emptyDict;
}
```

## 手順 4: 新しいグラフィックスステート辞書を構築

グラフィックスステートは、描画操作の振る舞いを記述するキー/バリューの集合です。透明度を設定するために必要なキーは次の 3 つです。

| Key | Meaning | Typical value |
|-----|---------|---------------|
| `CA` | 塗りの不透明度 (0 = 透明, 1 = 不透明) | `1`（完全に不透明） |
| `ca` | ストロークの不透明度（同スケール） | `0.5`（50 % 透明） |
| `BM` | ブレンドモード（例: `Normal`, `Multiply`） | `Normal` |

```csharp
    // Create an empty dictionary that will hold the graphics state
    var newGraphicsState = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Populate the dictionary with transparency and blend mode entries
    var graphicsStateEntries = new[]
    {
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "CA", new Aspose.Pdf.CosPdfNumber(1)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "ca", new Aspose.Pdf.CosPdfNumber(0.5)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "BM", new Aspose.Pdf.CosPdfName("Normal"))
    };

    foreach (var entry in graphicsStateEntries)
        newGraphicsState.Add(entry);
```

**Why these values?**  
`ca = 0.5` に設定すると、ストロークされたパス（線や枠線）が 50 % の不透明度で描画されます。一方 `CA = 1` は塗りつぶしを完全に不透明に保ちます。必要に応じて両方の数値を調整し、求める **modify PDF transparency** 効果を得てください。

## 手順 5: グラフィックスステートを ExtGState 辞書に挿入

新しいステートには一意の名前（例: `GS0`）を付ける必要があります。名前が既に存在すると、Aspose.Pdf は既存エントリを上書きし、他のコンテンツが壊れる可能性があります。

```csharp
    // Add the new graphics state under a custom name
    const string stateName = "GS0";

    // Ensure we don’t clash with an existing entry
    if (extGStateDict.ContainsKey(stateName))
        extGStateDict.Remove(stateName);

    extGStateDict.Add(stateName, newGraphicsState);
```

これでページのリソースは `GS0` を認識するようになりました。実際に使用するには、コンテンツストリーム内で `gs` 演算子（例: `GS0 gs`）を参照します。Aspose.Pdf では、生の PDF 演算子を注入してカスタムシェイプを描画することも可能です。

## 手順 6: 変更後の PDF を保存

```csharp
    // Persist the changes to a new file
    pdfDocument.Save(outputPath);
}
```

生成された `output.pdf` は元のビジュアルコンテンツを保持しつつ、以降に `GS0` を選択した描画コマンドは定義した透明度設定を遵守します。

### 期待される結果

`output.pdf` を Adobe Acrobat などのビューアで開き、`GS0` グラフィックスステートを使用して新しいストローク線を追加（例: `pdfDocument.Pages[1].Contents.Add(...)`）すると、線は半透明で表示され、塗りは不透明のままです。これにより **add graphics state pdf** と **modify PDF transparency** が正しく実装されたことが確認できます。

---

## 完全な実行可能サンプル

以下はコンソールアプリケーションに貼り付けてそのまま動作させられる完全プログラムです。ライセンスのロード、エラーハンドリング、各ステップの説明コメントが含まれています。

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣  Apply license (optional for evaluation)
        // -------------------------------------------------
        try
        {
            var license = new License();
            license.SetLicense("Aspose.Pdf.lic");
        }
        catch (Exception) { /* License not found – continue in evaluation mode */ }

        // -------------------------------------------------
        // 2️⃣  Define file locations
        // -------------------------------------------------
        string inputPath = @"C:\MyPdfs\input.pdf";
        string outputPath = @"C:\MyPdfs\output.pdf";

        // -------------------------------------------------
        // 3️⃣  Open document and prepare resources
        // -------------------------------------------------
        using (var pdfDocument = new Document(inputPath))
        {
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            if (!resourcesEditor.ContainsKey("ExtGState"))
            {
                var emptyExtGState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
                resourcesEditor.Add("ExtGState", emptyExtGState);
            }

            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // -------------------------------------------------
            // 4️⃣  Create custom graphics state (transparency)
            // -------------------------------------------------
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            newGraphicsState.Add("CA", new CosPdfNumber(1));   // Fill opacity
            newGraphicsState.Add("ca", new CosPdfNumber(0.5)); // Stroke opacity
            newGraphicsState.Add("BM", new CosPdf


## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを基にした関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全に動作するコード例が含まれており、API の追加機能を習得したり、独自プロジェクトで代替実装を検討したりする際に役立ちます。

- [Add Transparency to PDF with Aspose PDF in C# – Step‑by‑Step Guide](/pdf/english/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Add Transparency to PDF using Aspose – Complete C# Guide](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [How to Add an Image Stamp to a PDF Using Aspose.PDF for .NET: A Comprehensive Guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}