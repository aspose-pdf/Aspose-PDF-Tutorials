---
category: general
date: 2026-02-09
description: Aspose PDF を使用して C# で PDF を PNG に保存し、次に PDF を HTML にエクスポートし、透かしスタンプ PDF
  を追加し、ASP.NET の PDF 変換のために PDFX‑1a を変換する方法を学びます。
draft: false
keywords:
- save pdf as png
- export pdf to html
- add watermark stamp pdf
- how to convert pdfx-1a
- asp.net pdf conversion
language: ja
og_description: Aspose PDFを使用してC#でPDFをPNGとして保存し、次にPDFをHTMLにエクスポートし、透かしスタンプPDFを追加し、ASP.NETのPDF変換のためにPDFX‑1aを変換する方法を発見してください。
og_title: PDFをPNGとして保存し、Aspose PDFでPDF/X‑1aに変換
tags:
- aspnet
- pdf
- csharp
title: Aspose PDFでPDFをPNGとして保存し、PDF/X‑1aに変換
url: /ja/net/conversion-export/save-pdf-as-png-and-convert-to-pdf-x-1a-with-aspose-pdf/
---

spits out an HTML version that respects font encoding. No vague references, just concrete code and the “why” behind every line."

Translate.

Next heading: "## Prerequisites"

List items.

Translate each bullet.

Then "## Step 1: Load the Source PDF Document" etc.

Translate each heading and description.

Make sure to keep code block placeholders unchanged.

Also translate "Why this matters:" etc.

Proceed.

Let's craft final output.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose PDF を使用して PDF を PNG として保存し、PDF/X‑1a に変換する

PDF を **PNG として保存** する方法で、髪の毛が抜けそうになる経験はありませんか？ あなただけではありません—開発者は常に、元の PDF をそのまま残しつつページをラスタライズする手軽な方法を求めています。このガイドではその手順を詳しく解説し、さらに **PDF を HTML にエクスポート**、**ウォーターマークスタンプ PDF** の追加、そして堅牢な **ASP.NET PDF 変換** パイプラインのために **PDFX‑1a に変換** する方法も紹介します。

このチュートリアルから得られるものは、PDF を読み込み、PDF/X‑1a 準拠のファイルに変換し、最初のページを PNG としてレンダリングし、動的テキストスタンプを追加し、最後にフォントエンコーディングを考慮した HTML バージョンを出力する、コピー＆ペーストだけで動く C# プログラムです。曖昧な説明はなく、具体的なコードと各行の「なぜ」を示します。

## 前提条件

- .NET 6.0 以降（コードは .NET Framework 4.7+ でも動作します）
- Aspose.Pdf for .NET NuGet パッケージ（`Install-Package Aspose.Pdf`）
- ICC プロファイルファイル（`profile.icc`）※PDF/X‑1a 準拠が必要な場合
- 変換したい元の PDF（`input.pdf`）

以上だけです—余計なライブラリや隠れた手順はありません。これらが揃っていればすぐに始められます。

## Step 1: Load the Source PDF Document

何かを行う前に、まず PDF をメモリに読み込む必要があります。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Devices;

// Load the PDF you’ll be working with
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

**この重要性:** `Document` はコアオブジェクトで、ページ、フォント、メタデータへのアクセスを提供します。一度だけロードすれば、パイプライン全体が高速になります。

## Step 2: Convert to PDF/X‑1a (How to Convert PDFX‑1a)

PDF/X‑1a は印刷用ファイルのデファクトスタンダードです。変換することで全フォントが埋め込まれ、色が明確に定義されます。

```csharp
// Set up conversion options for PDF/X‑1a
PdfFormatConversionOptions conversionOptions = new PdfFormatConversionOptions(
    PdfFormat.PDF_X_1A,               // Target format
    ConvertErrorAction.Delete)       // What to do on errors
{
    IccProfileFileName = "YOUR_DIRECTORY/profile.icc", // External ICC profile
    OutputIntent = new OutputIntent("FOGRA39")        // Output intent for printing
};

// Perform the conversion
pdfDocument.Convert(conversionOptions);
```

**プロのコツ:** ICC プロファイルを省略すると、Aspose はデフォルトのプロファイルを埋め込みますが、印刷業者が要求する正確なプロファイルを使用すれば色ずれを防げます。

## Step 3: Save the PDF/X‑1a‑Compliant File

ドキュメントが PDF/X‑1a 仕様を満たしたら、ファイルとして書き出します。

```csharp
pdfDocument.Save("YOUR_DIRECTORY/pdfx1a.pdf");
```

ファイルサイズが増えることに気付くでしょう—追加リソースが埋め込まれるため、信頼性の高い印刷出力に必要な挙動です。

## Step 4: Render the First Page to PNG (Save PDF as PNG)

ここがメインキーワードの出番です: **PDF を PNG として保存** し、サムネイルやウェブ表示に利用します。

```csharp
// Configure PNG device with font analysis (helps with text extraction later)
PngDevice pngDevice = new PngDevice
{
    RenderingOptions = new RenderingOptions { AnalyzeFonts = true }
};

// Render only the first page
pngDevice.Process(pdfDocument.Pages[1], "YOUR_DIRECTORY/page1.png");
```

![PDF を PNG として保存した例](https://example.com/images/save-pdf-as-png.png "PDF ページを PNG に保存した例")

`AnalyzeFonts` フラグは、Aspose に PNG メタデータにフォント情報を埋め込ませます。後で元テキストにマッピングしたい場合に便利です。

## Step 5: Add a Watermark Stamp PDF

**ウォーターマークスタンプ PDF** の追加は Aspose の `TextStamp` で簡単です。スタンプは矩形に合わせて自動サイズ調整します。

```csharp
// Create a text stamp that auto‑adjusts its font size
TextStamp textStamp = new TextStamp("Important notice")
{
    AutoAdjustFontSizeToFitStampRectangle = true,
    AutoAdjustFontSizePrecision = 0.01f,
    Width = 400,               // Width of the stamp rectangle
    Height = 200,              // Height of the stamp rectangle
    WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords
};

// Place the stamp on the first page
pdfDocument.Pages[1].AddStamp(textStamp);
```

**自動調整が必要な理由:** ページごとに密度が異なるため、API に最適なフォントサイズ計算を任せるとテキストが矩形からはみ出すことがなくなります。

## Step 6: Save the Stamped PDF

スタンプを付与したら、変更を永続化します。

```csharp
pdfDocument.Save("YOUR_DIRECTORY/stamped.pdf");
```

任意のビューアで `stamped.pdf` を開くと、 “Important notice” ボックスがきれいに中央に配置されているのが確認できます—手動で調整する必要はありません。

## Step 7: Export PDF to HTML (Export PDF to HTML)

最後に、フォントエンコーディングに CMap を優先して **PDF を HTML にエクスポート** します。これにより生成された HTML は可能な限り Unicode を使用し、テキスト検索が可能になります。

```csharp
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    FontEncodingStrategy = HtmlSaveOptions.FontEncodingRules.DecreaseToUnicodePriorityLevel
};

// Save the HTML representation
pdfDocument.Save("YOUR_DIRECTORY/cmap.html", htmlOptions);
```

生成された `cmap.html` には、複雑なグラフィック用の `<canvas>` 要素とテキスト用の適切な `<span>` タグが含まれ、SEO フレンドリーなウェブページとして利用できます。

## 完全動作サンプル

以下はコンソールアプリに貼り付けるだけの完全プログラムです。プレースホルダーのパスを置き換えるだけで動作します。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Devices;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Convert to PDF/X‑1a (how to convert pdfx‑1a)
        PdfFormatConversionOptions conversionOptions = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_1A,
            ConvertErrorAction.Delete)
        {
            IccProfileFileName = "YOUR_DIRECTORY/profile.icc",
            OutputIntent = new OutputIntent("FOGRA39")
        };
        pdfDocument.Convert(conversionOptions);

        // 3️⃣ Save the PDF/X‑1a file
        pdfDocument.Save("YOUR_DIRECTORY/pdfx1a.pdf");

        // 4️⃣ Render first page as PNG (save pdf as png)
        PngDevice pngDevice = new PngDevice
        {
            RenderingOptions = new RenderingOptions { AnalyzeFonts = true }
        };
        pngDevice.Process(pdfDocument.Pages[1], "YOUR_DIRECTORY/page1.png");

        // 5️⃣ Add a dynamic watermark stamp (add watermark stamp pdf)
        TextStamp textStamp = new TextStamp("Important notice")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            AutoAdjustFontSizePrecision = 0.01f,
            Width = 400,
            Height = 200,
            WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords
        };
        pdfDocument.Pages[1].AddStamp(textStamp);

        // 6️⃣ Save the stamped PDF
        pdfDocument.Save("YOUR_DIRECTORY/stamped.pdf");

        // 7️⃣ Export to HTML (export pdf to html)
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            FontEncodingStrategy = HtmlSaveOptions.FontEncodingRules.DecreaseToUnicodePriorityLevel
        };
        pdfDocument.Save("YOUR_DIRECTORY/cmap.html", htmlOptions);

        Console.WriteLine("All operations completed successfully.");
    }
}
```

**期待される出力**

- `pdfx1a.pdf` – 印刷対応の PDF/X‑1a ファイル
- `page1.png` – 最初のページのラスタ画像（サムネイルに最適）
- `stamped.pdf` – スケーラブルな “Important notice” ウォーターマークが付いた元 PDF
- `cmap.html` – Unicode フォントを使用したウェブフレンドリーな HTML バージョン

## よくある質問とエッジケース

- **ソース PDF が暗号化されている場合は？**  
  パスワード付きでロードします: `new Document("input.pdf", new LoadOptions { Password = "secret" })`。

- **すべての変換で ICC プロファイルが必要ですか？**  
  必須ではありません—Aspose は汎用プロファイルにフォールバックしますが、厳密な PDF/X‑1a 準拠が必要な場合は印刷所が指定するプロファイルを使用すべきです。

- **複数ページを PNG にレンダリングできますか？**  
  もちろん可能です。`pdfDocument.Pages` をループし、`pngDevice.Process(page, $"page{page.Number}.png")` を呼び出します。

- **HTML 出力はモバイルフレンドリーですか？**  
  生成された HTML はレスポンシブな `<canvas>` 要素を使用しています。純粋に CSS ベースのテキストが必要な場合は `htmlOptions.SplitIntoPages = false` に設定し、`htmlOptions.PartsEmbeddingMode` を調整してください。

## ASP.NET PDF 変換のヒント

このコードを ASP.NET Core コントローラに組み込む際は、次の点に注意してください。

1. **結果をストリームで返す**—ディスクに書き込む代わりに `MemoryStream` を使用し、`FileResult` を返します。  
2. **`Document` とデバイスオブジェクトは `using` で確実に破棄**  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}