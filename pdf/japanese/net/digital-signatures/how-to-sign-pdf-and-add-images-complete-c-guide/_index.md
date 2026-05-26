---
category: general
date: 2026-03-29
description: C#でデジタル署名を使用してPDFに署名し、トリミングした画像を追加する方法。デジタル署名付きPDFの追加、PDF用画像のトリミング、そして画像をPDFに簡単に追加する方法を学びましょう。
draft: false
keywords:
- how to sign pdf
- add digital signature pdf
- crop image for pdf
- add image to pdf
- digital signature pdf page
language: ja
og_description: C#でAspose.Pdfを使用してデジタル署名でPDFに署名し、切り抜いた画像を埋め込む方法。このガイドで完全なソリューションをご確認ください。
og_title: PDFに署名し画像を追加する方法 – ステップバイステップ C# チュートリアル
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: PDFに署名して画像を追加する方法 – 完全C#ガイド
url: /ja/net/digital-signatures/how-to-sign-pdf-and-add-images-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDFに署名して画像を追加する方法 – 完全なC#ガイド

プログラムで **PDFに署名** しながらカスタム画像を挿入したことはありますか？承認ワークフローを構築していて、法的に有効な署名 *と* 同じページに署名者のサムネイル写真が必要になることがあります。要するに、 **digital signature pdf** を追加し、画像をトリミングして、 **add image to pdf** を手間なく実現したいということです。

このチュートリアルでは、ECDSA PKCS#7 証明書の読み込みから JPEG のトリミング、署名ページへのスタンプまで、すべての手順を解説します。最終的に、ページ 1 に署名し、写真を 400 × 400 px にトリミングして正確な位置に配置する、単一の実行可能 C# ファイルが手に入ります。外部スクリプト不要、魔法も不要、コードと解説だけです。

## Prerequisites

- .NET 6.0 以降（コードは .NET Framework 4.7+ でも動作します）
- **Aspose.Pdf for .NET** NuGet パッケージ（バージョン 23.9 以上）
- PKCS#7（`.pfx`）形式の ECDSA P‑256 証明書とそのパスワード
- 埋め込みたい JPEG 画像（例: `photo.jpg`）

> **Pro tip:** 証明書ファイルはソース管理から除外し、パスワードはシークレットマネージャで保護してください。

---

## Step 1: Set Up the Project and Imports

まずコンソールアプリを作成します（既存のサービスに統合しても構いません）。Aspose.Pdf の参照を追加します：

```bash
dotnet add package Aspose.Pdf
```

次に必要な名前空間をインクルードします：

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;
```

これらの `using` 文により、後で使用する `Document`、`Signature`、`Rectangle` クラスが利用可能になります。

## Step 2: Load the PDF and Prepare the Signature

既存の PDF（`source.pdf`）を開き、PKCS#7 の分離署名を使用する **digital signature pdf** オブジェクトを作成します。証明書は広く受け入れられている ECDSA P‑256 キーです。

```csharp
// Load the PDF you want to sign
var doc = new Document("YOUR_DIRECTORY/source.pdf");

// Initialize the signature appearance (optional but recommended)
var signature = new Signature(doc);
signature.Contact = "John Doe";
signature.Location = "New York, USA";
signature.Reason = "Document approval";

// Load the PKCS#7 certificate (ECDSA P‑256) for signing
var pkcsSignature = new PKCS7Detached(
    "YOUR_DIRECTORY/ecdsa.pfx",   // certificate file
    "YOUR_PASSWORD");             // certificate password
```

**Why this matters:** 分離型 PKCS#7 署名を使用すると、元の PDF コンテンツはそのままで暗号ハッシュが埋め込まれます。これは法的に有効な PDF の業界標準手法です。

## Step 3: Apply the Digital Signature to a Specific Page

次に、**page 1** に可視署名フィールドを配置します。矩形は署名ボックスの表示位置を定義します（座標はポイント単位、1 inch = 72 points）。

```csharp
// Apply the digital signature to page 1, covering a rectangular area
signature.Sign(
    pageNumber: 1,
    isVisible: true,
    signatureRect: new Rectangle(100, 100, 300, 300),
    pkcsSignature);
```

可視ボックスが不要な場合は `isVisible` を `false` に設定してください。`signatureRect` は文書レイアウトに合わせて調整可能です。

## Step 4: Open the Image Stream and Define Crop Areas

JPEG ファイルをストリームとして読み込み、左上 400 × 400 ピクセルを選択する **source rectangle** を指定します。これが **crop image for pdf** 操作です。

```csharp
// Open the image file that will be added to the PDF
using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

// Define the source rectangle that selects the portion to crop (0‑400 pixels)
var sourceRect = new Rectangle(0, 0, 400, 400);
```

> **Edge case:** 画像が 400 × 400 未満の場合、トリミングは自動的に画像の実際のサイズにクランプされ、例外は発生しません。

## Step 5: Define Where the Cropped Image Should Appear

次に、PDF ページ上の **destination rectangle** を設定します。この例では (50, 50) の位置に 200 × 200 points（≈2.78 インチ四方）のサイズで画像を配置します。

```csharp
// Define the destination rectangle where the cropped image will be placed on the page
var destinationRect = new Rectangle(50, 50, 200, 200);
```

自由に試してみてください：X/Y 座標を変更して画像の位置を移動したり、幅・高さを調整してスケーリングしたりできます。

## Step 6: Insert the Cropped Image onto the Signed Page

最後に、**page 1**（署名が付与された同じページ）に画像を追加します。使用する `AddImage` のオーバーロードは、ソース矩形とデスティネーション矩形を受け取り、1 回の呼び出しでトリミングと配置を同時に行います。

```csharp
// Insert the cropped image onto page 1 at the specified location
doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);
```

内部的には、Aspose.Pdf が 400 × 400 ピクセル領域を抽出し、200 × 200 points にリスケールして PDF コンテンツストリームに書き込みます。

## Step 7: Save the Signed and Image‑Enhanced PDF

すべての変更が完了したら、ドキュメントを永続化します。元ファイルを上書きするか、新しいファイルに書き出すかは自由です。

```csharp
// Save the final document
doc.Save("YOUR_DIRECTORY/output_signed.pdf");
Console.WriteLine("PDF signed and image added successfully!");
```

`output_signed.pdf` を Adobe Acrobat や任意の PDF ビューアで開くと、以下が確認できます：

- 指定した座標に表示される署名フィールド
- ページ 1 の (50, 50) に配置されたトリミング済み写真
- 証明書が信頼されていればデジタル署名が検証される

---

## Frequently Asked Questions (FAQ)

| Question | Answer |
|----------|--------|
| **Can I sign a different page?** | `signature.Sign` の `pageNumber` 引数を任意の有効なページインデックス（1 ベース）に変更してください。 |
| **What if I need multiple signatures?** | 各ページまたは各位置ごとに新しい `Signature` インスタンスを作成し、同じ証明書を使用する場合は同じ `pkcsSignature` を再利用できます。 |
| **Is the image cropping limited to rectangles?** | はい、Aspose.Pdf の `AddImage` は矩形領域のみ対応します。複雑な形状が必要な場合は、埋め込む前に System.Drawing などで画像を前処理してください。 |
| **How do I make the signature invisible?** | `isVisible` を `false` に設定し、`signatureRect` を省略します。署名は暗号的に有効なままです。 |
| **What formats can I embed besides JPEG?** | PNG、BMP、GIF、TIFF もサポートされています。ファイルパスを変更し、ストリームが正しいバイトを読み込むようにしてください。 |

---

## Full Working Example

以下に完全な単体プログラムを示します。`Program.cs` にコピペし、パスを調整して実行してください。

```csharp
// Program.cs
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        var doc = new Document("YOUR_DIRECTORY/source.pdf");

        // 2️⃣ Prepare the digital signature appearance
        var signature = new Signature(doc)
        {
            Contact = "John Doe",
            Location = "New York, USA",
            Reason = "Document approval"
        };

        // 3️⃣ Load the PKCS#7 ECDSA P‑256 certificate
        var pkcsSignature = new PKCS7Detached(
            "YOUR_DIRECTORY/ecdsa.pfx",
            "YOUR_PASSWORD");

        // 4️⃣ Apply a visible signature on page 1
        signature.Sign(
            pageNumber: 1,
            isVisible: true,
            signatureRect: new Rectangle(100, 100, 300, 300),
            pkcsSignature);

        // 5️⃣ Open the image to be added
        using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

        // 6️⃣ Define crop (source) and placement (destination) rectangles
        var sourceRect = new Rectangle(0, 0, 400, 400);      // crop 400×400 px from top‑left
        var destinationRect = new Rectangle(50, 50, 200, 200); // place at (50,50) with 200×200 pt size

        // 7️⃣ Insert the cropped image onto the same page
        doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);

        // 8️⃣ Save the final PDF
        doc.Save("YOUR_DIRECTORY/output_signed.pdf");
        Console.WriteLine("PDF signed and image added successfully!");
    }
}
```

**Expected result:** `output_signed.pdf` を開くと、署名フィールド（100 × 100 → 300 × 300 points）と、`photo.jpg` の左上から切り出した 200 × 200 point の画像が表示されます。署名は提供された ECDSA 証明書で検証可能です。

---

## Wrapping Up

**how to sign PDF**、**add digital signature pdf**、**crop image for pdf**、そして **add image to pdf** を Aspose.Pdf と C# で実装する方法を網羅しました。証明書の読み込みから最終ドキュメントの保存まで、すべてが 1 つの読みやすいソースファイルに収まります。

次のステップに挑戦したい方は、以下を検討してください：

- 異なるページに **multiple signatures** を追加する（“digital signature pdf page” の概念を利用）。
- 検証サービスへリンクする **QR codes** を埋め込む。
- ASP.NET Core API でオンザフライの PDF 生成を自動化する。

堅牢な PDF 自動化の鍵は、署名処理・画像処理・最終文書組み立ての明確な分離です。座標をいじったり、画像フォーマットを入れ替えたり、タイムスタンプを試したりして、ワークフローを自由に拡張してください。

質問やエッジケース、面白い活用例があればコメントで教えてください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}