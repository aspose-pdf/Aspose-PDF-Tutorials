---
category: general
date: 2026-06-21
description: Bates番号付けPDFを追加し、Bates番号の付け方、PDFをPDF/X‑4に変換、PDFをPDF/A‑4に変換、そしてC#でPDFにデジタル署名する方法を単一のウォークスルーで学びます。
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbers
- digitally sign pdf c#
- convert pdf to pdf/x-4
- convert pdf to pdfa-4
language: ja
og_description: PDFにベーツ番号を追加、ベーツ番号の追加方法を見る、PDFをPDF/X‑4に変換、PDFをPDF/A‑4に変換、そしてAspose.Pdfを使用してC#でPDFにデジタル署名を行う。
og_title: Bates番号付PDFの追加 – ステップバイステップ C# チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add bates numbering pdf and learn how to add bates numbers, convert
    pdf to pdf/x-4, convert pdf to pdfa-4, and digitally sign pdf c# in a single walkthrough.
  headline: Add Bates Numbering PDF – Complete C# Guide with Signing & Conversion
  type: TechArticle
- questions:
  - answer: Yes. Use `BatesNumberingOptions` properties such as `Location` and `FontSize`
      to fine‑tune placement.
    question: Can I change the position of the Bates numbers?
  - answer: Switch `PdfFormat.PDF_X_4` to `PdfFormat.PDFA_4` in the conversion options.
      That satisfies the **convert pdf to pdfa-4** requirement.
    question: What if I need PDF/A‑4 instead of PDF/X‑4?
  - answer: Absolutely. Replace `DigestHashAlgorithm.Sha384` with `DigestHashAlgorithm.Sha256`
      (or any supported algorithm).
    question: My certificate uses a different hash algorithm—can I use SHA‑256?
  - answer: 'Not strictly. In this flow we save after conversion and after Bates numbering
      to give you intermediate files. You could defer saving until the end if you
      prefer a single write operation. ## Wrap‑Up We’ve just demonstrated a practical,
      end‑to‑end solution that **add bates numbering pdf**, explains **'
    question: Do I need to call `document.Save` after each step?
  type: FAQPage
tags:
- Aspose.Pdf
- C#
- PDF processing
- Bates numbering
title: PDFにベーツ番号を付与 – 署名と変換を含む完全なC#ガイド
url: /ja/net/programming-with-security-and-signatures/add-bates-numbering-pdf-complete-c-guide-with-signing-conver/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates番号付PDFの追加 – 完全なC#ガイド（署名と変換）

Ever wondered **add bates numbering pdf** without pulling your hair out? You're not the only one. Legal teams, auditors, and anyone who needs traceable documents constantly ask *how to add bates numbers* to a PDF, and then they also need the file to meet PDF/X‑4 or PDF/A‑4 standards and be digitally signed.  

In this tutorial we’ll walk through exactly that—using Aspose.Pdf for .NET we’ll **add bates numbering pdf**, show **how to add bates numbers**, **convert pdf to pdf/x-4**, **convert pdf to pdfa-4**, and finally **digitally sign pdf c#**. By the end you’ll have a ready‑to‑run program that produces three polished PDFs: a PDF/X‑4 version, a Bates‑numbered version, and a digitally signed version.

![Bates番号付PDFの例](image-placeholder.png "Bates番号付PDFの実行画面のスクリーンショット")

## 必要なもの

- **.NET 6+**（または .NET Framework 4.6+）。Aspose.Pdf は両方をサポートしています。
- 有効な **Aspose.Pdf for .NET ライセンス**（評価版でも動作しますが、透かしが表示されます）。
- **PKCS#7 証明書ファイル**（`.pfx`）と署名用パスワード。
- 変換したい **サンプル PDF**（管理できるフォルダーに配置してください）。
- Visual Studio、Rider、またはお好みの C# IDE。

That’s it—no extra NuGet packages beyond `Aspose.Pdf`. If you haven’t added the library yet, run:

```bash
dotnet add package Aspose.Pdf
```

Now let’s dive into the code.

## ステップ 1: ソース PDF ドキュメントの読み込み

First, we need to bring the original file into memory. This is the foundation for every later operation.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

// Load the source PDF – adjust the path to your environment
var document = new Document("YOUR_DIRECTORY/sample.pdf");
```

> **Why this matters:** Loading the PDF creates a `Document` object that represents the entire file, giving us access to conversion, form fields, and security APIs.

## ステップ 2: PDF を PDF/X‑4 に変換（PDF/A‑4 準拠）

If your workflow demands archival quality, PDF/X‑4 (a subset of PDF/A‑4) is the way to go. Here’s how to **convert pdf to pdf/x-4** with Aspose.

```csharp
// Set conversion options – PDF/X‑4 is the target format
var conversionOptions = new PdfFormatConversionOptions(PdfFormat.PDF_X_4, ConvertErrorAction.Delete);

// Perform the conversion
document.Convert(conversionOptions);
```

> **Tip:** The `ConvertErrorAction.Delete` flag strips out any content that would break compliance, ensuring a clean PDF/X‑4 output.

## ステップ 3: PDF/X‑4 バージョンの保存

Now that the document complies with PDF/X‑4, we persist it to disk.

```csharp
document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");
```

You now have a **convert pdf to pdfa-4**‑compatible file (PDF/X‑4 is a member of the PDF/A‑4 family). Feel free to open it in Acrobat to verify the compliance badge.

## ステップ 4: Bates 番号付与 – “Add Bates Numbering PDF” の核心

Bates numbering is a sequential identifier placed on each page. This is the exact answer to *how to add bates numbers* programmatically.

```csharp
// Configure Bates numbering options
var batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",   // Optional prefix
    Start = 5000        // Starting number
};

// Apply Bates numbering to the document
document.AddBatesNumbering(batesOptions);
```

> **Why this works:** `AddBatesNumbering` walks through every page and stamps the number in the default location (bottom‑right). You can later tweak the position via `BatesNumberingOptions` if needed.

## ステップ 5: Bates 番号付 PDF の保存

After we’ve **add bates numbering pdf**, we need a separate file that preserves the numbers.

```csharp
document.Save("YOUR_DIRECTORY/sample_bates.pdf");
```

Open the file; you should see “CASE‑5000”, “CASE‑5001”, and so on at the bottom of each page.

## ステップ 6: PDF にデジタル署名 – “Digitally Sign PDF C#” の実装

A digital signature guarantees authenticity and integrity. Below we’ll **digitally sign pdf c#** using a SHA‑384 hash.

```csharp
// Prepare the signature handler
var signature = new PdfFileSignature(document);

// Load the PKCS#7 certificate (adjust password)
var pkcs7 = new PKCS7Detached(
    "YOUR_DIRECTORY/mycert.pfx", // Path to .pfx
    "pwd",                       // Certificate password
    DigestHashAlgorithm.Sha384   // Strong hashing algorithm
);

// Sign page 1, place signature rectangle at (100,100)-(200,150)
signature.Sign(
    pageNumber: 1,
    signatureAppearance: true,
    rectangle: new Rectangle(100, 100, 200, 150),
    pkcs7: pkcs7
);
```

> **Pro tip:** The `Rectangle` defines where the visible signature appears. If you don’t need a visual cue, set `signatureAppearance` to `false`.

## ステップ 7: デジタル署名済み PDF の保存

Finally, write the signed document to disk.

```csharp
signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
```

You now have a **digitally sign pdf c#** file that can be validated in any PDF reader supporting digital signatures.

## 完全なソースコード – ワンストップソリューション

Below is the complete, ready‑to‑run program that ties everything together. Copy‑paste, adjust the paths, and hit **F5**.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source PDF document
        // -------------------------------------------------
        var document = new Document("YOUR_DIRECTORY/sample.pdf");

        // -------------------------------------------------
        // Step 2: Convert the document to PDF/X‑4 format
        // (PDF/A‑4 compliance)
        // -------------------------------------------------
        var conversionOptions = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_4,
            ConvertErrorAction.Delete);
        document.Convert(conversionOptions);

        // -------------------------------------------------
        // Step 3: Save the PDF/X‑4 version
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");

        // -------------------------------------------------
        // Step 4: Add Bates numbering – how to add bates numbers
        // -------------------------------------------------
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 5000
        };
        document.AddBatesNumbering(batesOptions);

        // -------------------------------------------------
        // Step 5: Save the Bates‑numbered PDF
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_bates.pdf");

        // -------------------------------------------------
        // Step 6: Sign the document using SHA‑384 hashing
        // -------------------------------------------------
        var signature = new PdfFileSignature(document);
        var pkcs7 = new PKCS7Detached(
            "YOUR_DIRECTORY/mycert.pfx",
            "pwd",
            DigestHashAlgorithm.Sha384);
        signature.Sign(
            pageNumber: 1,
            signatureAppearance: true,
            rectangle: new Rectangle(100, 100, 200, 150),
            pkcs7: pkcs7);

        // -------------------------------------------------
        // Step 7: Save the digitally signed PDF
        // -------------------------------------------------
        signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
    }
}
```

### 期待される出力

| ファイル | 用途 | 主な機能 |
|------|---------|-------------|
| `sample_pdfx4.pdf` | PDF/X‑4 バージョン | PDF/A‑4 準拠 |
| `sample_bates.pdf` | Bates 番号付 PDF | **add bates numbering pdf** が適用 |
| `sample_signed.pdf` | デジタル署名済み PDF | SHA‑384 で **digitally sign pdf c#** |

Open any of the three files in Adobe Acrobat Reader; you’ll see the Bates numbers on the second file and a signature field on the third.

## よくある質問 (FAQ)

**Q: Bates 番号の位置を変更できますか？**  
A: はい。`BatesNumberingOptions` の `Location` や `FontSize` などのプロパティを使用して配置を微調整できます。

**Q: PDF/X‑4 の代わりに PDF/A‑4 が必要な場合は？**  
A: 変換オプションで `PdfFormat.PDF_X_4` を `PdfFormat.PDFA_4` に切り替えてください。これで **convert pdf to pdfa-4** の要件を満たします。

**Q: 証明書が別のハッシュアルゴリズムを使用しています—SHA‑256 を使えますか？**  
A: もちろんです。`DigestHashAlgorithm.Sha384` を `DigestHashAlgorithm.Sha256`（またはサポートされている任意のアルゴリズム）に置き換えてください。

**Q: 各ステップの後に `document.Save` を呼び出す必要がありますか？**  
A: 必要ではありません。このフローでは変換後と Bates 番号付与後に中間ファイルを作成するために保存しています。単一の書き込み操作にしたい場合は、最後まで保存を遅らせても構いません。

## まとめ

We’ve just demonstrated a practical, end‑to‑end solution that **add bates numbering pdf**, explains **how to add bates numbers**, shows **convert pdf to pdf/x-4**, covers

## 次に学ぶべきことは？

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Aspose Pdf Net 添付ファイル追加と PDF/A 変換](/pdf/german/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net 添付ファイル追加と PDF/A 変換](/pdf/french/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net 添付ファイル追加と PDF/A 変換](/pdf/japanese/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}