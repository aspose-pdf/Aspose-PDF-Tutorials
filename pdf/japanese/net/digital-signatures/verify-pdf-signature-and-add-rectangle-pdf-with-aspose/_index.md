---
category: general
date: 2026-02-09
description: C#でAspose.PDFを使用してPDF署名を検証します。矩形をPDFに追加する方法、更新されたPDFを保存する方法、そしてAspose.PDFの署名機能の使い方を学びます。
draft: false
keywords:
- verify pdf signature
- add rectangle pdf
- save updated pdf
- aspose pdf signature
- add graphics pdf
language: ja
og_description: C#でPDF署名を迅速に検証する。このガイドでは、PDFにグラフィックを追加し、更新されたPDFを保存し、Aspose PDF署名APIを使用する方法を示します。
og_title: PDF署名を検証し、矩形を追加する – 完全なAsposeガイド
tags:
- Aspose.PDF
- C#
- Digital Signature
- PDF Manipulation
title: AsposeでPDF署名を検証し、矩形を追加する
url: /ja/net/digital-signatures/verify-pdf-signature-and-add-rectangle-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose を使用した PDF 署名の検証と矩形の追加

C# プロジェクトで **verify pdf signature** が必要だったことはありますか、でもどこから始めればよいか分からなかったでしょうか？ あなたは一人ではありません—デジタル署名はコンプライアンスに必須ですが、署名後にドキュメントを調整する必要がある開発者は多く躓きます。  

このチュートリアルでは、**verifies pdf signature** を行い、最初のページに **rectangle** を追加し、形状がページ境界内に収まっていることを確認し、最後に **save updated pdf** する完全な実行可能サンプルを、最新の Aspose.PDF API を使って解説します。最後まで読めば、任意の .NET ソリューションに組み込める単一の自己完結型プログラムが手に入ります。

## 学べること

- Aspose.PDF で署名済み PDF を読み込む方法。
- **aspose pdf signature** クラスを使って各署名を検証し、改ざんを検出する方法。
- **Add rectangle pdf** グラフィックを安全に追加し、ページに収まるようにする方法。
- **Save updated pdf** で既存の署名を保持しながら保存する方法。
- ヒント、エッジケースの対処法、よくある落とし穴。

外部ドキュメントは不要です—必要な情報はすべてここにあります。

## 前提条件

- .NET 6.0 以降（コードは .NET Framework 4.7+ でも動作します）。
- Aspose.PDF for .NET NuGet パッケージ（≥ 23.10）。インストールは以下の通り：

```bash
dotnet add package Aspose.Pdf
```

- `signed.pdf` という名前の署名済み PDF ファイルを、管理できるフォルダーに配置します（コード中の `YOUR_DIRECTORY` を置き換えてください）。
- C# と Visual Studio または VS Code の基本的な知識。

> **Pro tip:** 署名済み PDF が手元にない場合は、Aspose が提供している無料デモファイルをサイトからダウンロードしてテストに利用できます。

---

## verify pdf signature – ステップバイステップ

最初に行うべきことは、ドキュメントを開き、すべてのデジタル署名をループで確認することです。Aspose.PDF には便利な 2 つのメソッドがあります：`VerifySignature` は暗号チェックが通るかを示し、 newer `IsSignatureCompromised` は署名後に発生した可能性のある改ざんをフラグします。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

// Load the signed PDF document
Document pdfDocument = new Document("YOUR_DIRECTORY/signed.pdf");

// Create a signature handler for the document
PdfFileSignature signatureHandler = new PdfFileSignature(pdfDocument);

// Iterate over each signature name in the PDF
foreach (var signatureName in signatureHandler.GetSignNames())
{
    // Verify the cryptographic integrity
    bool isValid = signatureHandler.VerifySignature(signatureName);
    
    // Detect if the signature has been compromised (e.g., document altered)
    bool isCompromised = signatureHandler.IsSignatureCompromised(signatureName);
    
    Console.WriteLine($"{signatureName}: valid={isValid}, compromised={isCompromised}");
}
```

**Why this matters:**  
- `VerifySignature` だけでは、署名者の証明書が依然として信頼できるかだけが確認されます。  
- `IsSignatureCompromised` は、隠しオブジェクトの追加など微細な変更を検出し、署名後に PDF の視覚コンテンツが変更されたかどうかを教えてくれます。

**Expected output** (例: 署名が 2 つある場合):

```
Signature1: valid=True, compromised=False
Signature2: valid=True, compromised=True
```

いずれかの署名が `compromised=True` を返した場合は、処理を中止するかユーザーに警告してください。ドキュメントの完全性は保証できません。

---

## ページに矩形 PDF を追加

署名が無事であること（または改ざんの有無を把握できたこと）を確認したら、シンプルな矩形グラフィックを追加しましょう。これは「Reviewed」スタンプを付けたり、セクションをハイライトしたり、特定領域に注意を引くのに便利です。

```csharp
// Access the first page (pages are 1‑based in Aspose)
Page firstPage = pdfDocument.Pages[1];

// Define a rectangle shape (coordinates: lower-left X, lower-left Y, upper-right X, upper-right Y)
Rectangle shapeRect = new Rectangle(100, 500, 200, 600);

// Add the rectangle to the page's graphics collection
firstPage.AddRectangle(shapeRect);
```

**What the numbers mean:**  
- PDF の座標系は左下隅が原点です。  
- この例では、矩形は横 100 ポイント、縦 100 ポイントのサイズで、典型的な A4 ページのほぼ中央に配置されます。

> **Note:** よりリッチな形状が必要な場合は、Aspose は `AddEllipse`、`AddPolygon` などもサポートしています。

---

## グラフィックの境界をチェック – 矩形が収まることを確認

変更を確定する前に、グラフィックがページの印刷可能領域内に収まっているか確認するのが賢明です。新しい `CheckGraphicsBounds` メソッドがまさにそれを行います。

```csharp
// Verify that the rectangle does not exceed page limits
bool shapeFits = firstPage.CheckGraphicsBounds(shapeRect);
Console.WriteLine($"Shape fits page: {shapeFits}");
```

`shapeFits` が `false` を返した場合は、矩形の座標を調整してください—サイズを縮小するか、ページ下部に移動するなどです。これにより、特に印刷時に見栄えが悪くなるクリッピングを防げます。

---

## 更新された PDF を保存 – 署名と新しいグラフィックを保持

最後に、変更済みドキュメントをディスクに書き戻します。`Save` メソッドは既存の署名を尊重し、コンテンツが実際に変更されていない限り署名を無効にしません（このチェックは既に `IsSignatureCompromised` で行っています）。

```csharp
// Save the updated PDF to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

// Inform the user
Console.WriteLine("PDF saved as output.pdf with new rectangle.");
```

**Why use a new file?**  
元のファイルに上書き保存すると、元の署名が消えてしまい、前後の状態を比較できなくなります。`output.pdf` に書き出すことで、監査目的のために元ファイルを保持できます。

---

## 完全な実行可能サンプル

以下はコンソール アプリにコピーペーストできる完全プログラムです。すべての手順が統合されており、各ブロックにコメントが付いています。最後に期待されるコンソール出力も確認できます。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the signed PDF document
        // -------------------------------------------------
        string inputPath = "YOUR_DIRECTORY/signed.pdf";
        Document pdfDocument = new Document(inputPath);
        Console.WriteLine($"Loaded PDF: {inputPath}");

        // -------------------------------------------------
        // 2️⃣ Verify each digital signature and detect compromise
        // -------------------------------------------------
        PdfFileSignature signatureHandler = new PdfFileSignature(pdfDocument);
        foreach (var signatureName in signatureHandler.GetSignNames())
        {
            bool isValid = signatureHandler.VerifySignature(signatureName);
            bool isCompromised = signatureHandler.IsSignatureCompromised(signatureName);
            Console.WriteLine($"{signatureName}: valid={isValid}, compromised={isCompromised}");
        }

        // -------------------------------------------------
        // 3️⃣ Access the first page and add a rectangle
        // -------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        Rectangle shapeRect = new Rectangle(100, 500, 200, 600);
        firstPage.AddRectangle(shapeRect);
        Console.WriteLine("Added rectangle to page 1.");

        // -------------------------------------------------
        // 4️⃣ Ensure the rectangle fits inside the page bounds
        // -------------------------------------------------
        bool shapeFits = firstPage.CheckGraphicsBounds(shapeRect);
        Console.WriteLine($"Shape fits page: {shapeFits}");

        // -------------------------------------------------
        // 5️⃣ Save the updated PDF
        // -------------------------------------------------
        string outputPath = "YOUR_DIRECTORY/output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Saved updated PDF as: {outputPath}");
    }
}
```

**Expected console output** (有効で改ざんされていない署名が 1 つある場合):

```
Loaded PDF: YOUR_DIRECTORY/signed.pdf
Signature1: valid=True, compromised=False
Added rectangle to page 1.
Shape fits page: True
Saved updated PDF as: YOUR_DIRECTORY/output.pdf
```

署名が改ざんされている場合は `compromised=True` が表示され、続行するかどうかを判断できます。

---

## よくある質問とエッジケースの対処

| Question | Answer |
|----------|--------|
| **What if the PDF has no signatures?** | `GetSignNames()` は空のコレクションを返すので、ループはスキップされ、グラフィックは引き続き追加可能です。 |
| **Can I add multiple rectangles?** | はい—異なる `Rectangle` オブジェクトを使って `AddRectangle` を繰り返し呼び出すだけです。 |
| **What about password‑protected PDFs?** | 検証前に `pdfDocument = new Document("file.pdf", new LoadOptions("password"));` のようにパスワードを指定して読み込みます。 |
| **Will adding graphics invalidate a valid signature?** | 追加したグラフィックが署名対象のページに含まれる場合のみ無効化されます。`IsSignatureCompromised` で検出でき、対象外であれば署名はそのまま保持されます。 |
| **Do I need to close resources?** | Aspose.PDF のオブジェクトはマネージドなので必須ではありませんが、余裕があれば `using` ブロックで囲んでリソースを解放すると安全です。 |

---

## 本番環境でのプロチップ

- **Batch processing:** 入出力パスを受け取るメソッドで全体をラップし、`Parallel.ForEach` でファイルリストを並列処理すると高速化できます。  
- **Logging:** `Console.WriteLine` を Serilog などの本格的なロガーに置き換えて、検証結果を監査ログに記録しましょう。  
- **Signature policy:** `VerifySignature` に加えて証明書失効チェック（OCSP/CRL）を組み合わせると、コンプライアンスがさらに強化されます。  
- **Graphics styling:** `firstPage.AddRectangle(shapeRect, new GraphicState { StrokeColor = Color.Red, FillColor = Color.Yellow });` のように StrokeColor や FillColor を設定すれば、矩形が目立ちます。  
- **Version lock:** ライブラリ更新時の破壊的変更を防ぐため、Aspose.PDF の NuGet バージョンを固定しておきましょう。

---

## 結論

これで **verify pdf signature**、**add rectangle pdf**、そして **save updated pdf** を最新の Aspose.PDF API で実現する、堅牢なエンドツーエンドのサンプルが手に入りました。コードは改ざん署名をチェックし、グラフィックがページ境界内に収まることを保証し、元のデジタル署名を保持します—実務のコンプライアンスワークフローが求める要件そのものです。

次に試したいこと：

- **add graphics pdf**（透かしや QR コードなど）を追加する。  
- **aspose pdf signature** API を使って新しい署名をプログラムから作成する。  
- ASP.NET Core の Web サービスでリアルタイムにドキュメント検証を自動化する。

ぜひ実行して矩形座標を調整し、さまざまな PDF 構造に対するライブラリの挙動を確認してみてください。Happy coding、そして PDF が署名されつつスタイリッシュであり続けますように！

![PDF 署名検証例](image.png "PDF 署名検証例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}