---
category: general
date: 2026-06-08
description: C#でAspose.PDFを使用してPDF内の画像をトリミングする。数行のコードで画像付きPDFの作成、画像付きPDFの保存、PDFへの画像追加方法を学びましょう。
draft: false
keywords:
- crop image in pdf
- create pdf with image
- save pdf with image
- how to add image to pdf
- how to crop image pdf
language: ja
og_description: C#でAspose.PDFを使用してPDF内の画像をトリミングする。このチュートリアルでは、画像付きPDFの作成方法、画像付きPDFの保存方法、そして画像をPDFに素早く追加する方法を示します。
og_title: Aspose.PDFでPDFの画像をトリミングする – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  headline: Crop Image in PDF with Aspose.PDF – Complete Guide
  type: TechArticle
- description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  name: Crop Image in PDF with Aspose.PDF – Complete Guide
  steps:
  - name: '**Image stream** – the raw bytes of your picture.'
    text: '**Image stream** – the raw bytes of your picture.'
  - name: '**Placement rectangle** – where on the page the image lives.'
    text: '**Placement rectangle** – where on the page the image lives.'
  - name: '**Crop rectangle** – the portion of the image you actually want to render.'
    text: '**Crop rectangle** – the portion of the image you actually want to render.'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
- Image processing
title: Aspose.PDFでPDFの画像をトリミングする – 完全ガイド
url: /ja/net/programming-with-images/crop-image-in-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.PDF を使用した PDF の画像トリミング – 完全ガイド

グラフィックエディタを起動せずに **PDF の画像をトリミング** したいと思ったことはありませんか？ あなただけではありません。レポートや請求書、電子書籍などで、画像の一部—たとえばロゴの隅やチャートの一部—だけが必要で、PDF 内に直接配置したいことがあります。  

このガイドではまさにそれを実現します。**画像で PDF を作成**し、**PDF に画像を追加**し、そして Aspose.PDF ライブラリ for C# を使用して **PDF の画像をトリミング** します。最後には **画像付き PDF を保存** する方法も学べるので、ファイルを誰にでも配布できます。

---

## 必要なもの

- .NET 6.0 以降（コードは .NET Framework 4.6+ でも動作します）  
- ライセンス版または試用版の **Aspose.PDF for .NET**（NuGet `Install-Package Aspose.PDF` でインストール）  
- ディスク上の画像ファイル（JPEG/PNG）—ここでは `image.jpg` と呼びます  
- お好きな IDE（Visual Studio、Rider、VS Code）

それだけです。余計なサービスや外部ツールは不要です。

---

## 手順 1: プロジェクトのセットアップとインポート

まず、コンソールアプリを作成し、使用する名前空間をインポートします。`using` 文でコードをすっきりさせ、後の手順を読みやすくします。

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;   // for text fragments if you want captions later
```

> **プロのコツ:** Visual Studio を使用している場合は、プロジェクトを右クリック → *Manage NuGet Packages* → 「Aspose.PDF」を検索してインストールしてください。ライブラリは画像の配置とトリミングを内部で処理するため、サードパーティの画像ライブラリは不要です。

---

## 手順 2: 画像で PDF を作成

ここで実際に **画像で PDF を作成** します。以下のスニペットは新しい `Document` を作成し、空白ページを追加し、画像ストリームを準備します。

```csharp
// Initialize a new PDF document
Document pdf = new Document();

// Add a blank page – think of it as a clean canvas
Page page = pdf.Pages.Add();

// Open the source image file
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // We'll place the whole image first; cropping comes next
    // Define where the image should sit on the page (in points; 1 point = 1/72 inch)
    Rectangle placement = new Rectangle(0, 0, 600, 800); // width=600pt, height=800pt

    // Add the image without cropping yet – just to see the full picture
    page.AddImage(imgStream, placement);
}
```

このコードを実行すると、指定したサイズに伸ばされた画像全体が表示された PDF が生成されます。トリミングを始める前の簡単な動作確認に最適です。

---

## 手順 3: PDF に画像を追加する方法（トリミングの準備）

正確な領域がすでに分かっている場合は、フルサイズのステップを省略して **PDF に画像を追加する方法** に直接進めます。`AddImage` メソッドは 3 つのパラメータを受け取ります。

1. **画像ストリーム** – 画像の生バイト列です。  
2. **配置矩形** – ページ上で画像が配置される領域です。  
3. **トリミング矩形** – 実際に描画したい画像の領域です。

以下は、配置 **と** トリミングを 1 回の呼び出しで行うコンパクト版です。

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Full‑size placement rectangle (you can adjust X/Y if you need margins)
    Rectangle placement = new Rectangle(0, 0, 600, 800);

    // Crop area: upper‑left quarter of the original image
    Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

    // This single line both adds the image and crops it
    page.AddImage(imgStream, placement, crop);
}
```

> **なぜこれが機能するか:** Aspose.PDF は内部でトリミング矩形を画像のピクセル寸法にマッピングし、`placement` 領域内にそのスライスだけを描画します。余計なビットマップ処理が不要なので、PDF のサイズを小さく保てます。

---

## 手順 4: PDF の画像トリミング – 高度なオプション

時には四分の一トリミングだけでは足りません。カスタム矩形が必要だったり、画像のアスペクト比を保持したいことがあります。以下はより柔軟なアプローチです。

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Placement on the page (centered, 300pt wide, keep original height)
    Rectangle placement = new Rectangle(150, 400, 450, 1200);

    // Suppose you want a 200 × 150 pixel region starting at (50, 30) in the source image
    // First, convert pixel coordinates to points (assuming 72 DPI)
    float dpi = 72f;
    float left   = 50  / dpi * 72; // = 50 points
    float bottom = 30  / dpi * 72; // = 30 points
    float width  = 200 / dpi * 72; // = 200 points
    float height = 150 / dpi * 72; // = 150 points

    Rectangle crop = new Rectangle(left, bottom, left + width, bottom + height);

    page.AddImage(imgStream, placement, crop);
}
```

**エッジケースの取り扱い:**  
- **Null ストリーム** – 漏れを防ぐために、示したように `FileStream` を必ず `using` ブロックでラップしてください。  
- **大きな画像** – ソース画像が非常に大きい場合は、`placement` 矩形を縮小することを検討してください。Aspose が自動的にダウンサンプリングします。  
- **透過 PNG** – ライブラリはアルファチャンネルを尊重するため、トリミング領域の透過性が保持されます。

---

## 手順 5: 画像付き PDF を保存（検証）

最後に **画像付き PDF を保存** します。`Save` メソッドでドキュメントをディスクに書き出します。API を構築している場合は、Web クライアントにストリームとして返すことも可能です。

```csharp
// Save the final PDF to the output folder
pdf.Save("YOUR_DIRECTORY/output.pdf");

// Optional: Open the file automatically (only works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/output.pdf",
    UseShellExecute = true
});
```

`output.pdf` を開くと、`image.jpg` のトリミングされた部分だけが、定義した位置に正確に配置されているはずです。画像が伸びて見える場合は、`placement` 矩形の幅・高さをトリミング矩形のアスペクト比に合わせて調整してください。

---

## よくある質問と落とし穴

| 質問 | 回答 |
|----------|--------|
| **同じページに複数の画像をトリミングできますか？** | もちろんです。各画像に対して個別の配置矩形とトリミング矩形を指定して `page.AddImage` を呼び出してください。 |
| **画像が別の形式（例: BMP）の場合はどうすれば？** | Aspose.PDF は JPEG、PNG、BMP、GIF、TIFF を標準でサポートしています。ファイル拡張子を変更するだけです。 |
| **本番環境で使用するにはライセンスが必要ですか？** | 試用版は最大5ページまで使用可能です。本番環境では透かしを除去するためにライセンスを購入してください。 |
| **トリミングした画像を回転させるには？** | 画像を追加した後、`Image` オブジェクトを取得し、その `Rotate` プロパティを設定します（例: `Rotate = RotationAngle.Rotate90`）。 |
| **絶対ポイントではなくパーセンテージでトリミングする方法はありますか？** | はい。`image.Width * 0.25` などで矩形サイズを計算し、Step 4 の例のようにポイントに変換してください。 |

---

## 完全動作サンプル（コピー＆ペースト可能）

```csharp
using System;
using System.IO;
using Aspose.Pdf;

namespace CropImageInPdfDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new PDF document and add a blank page
            Document pdf = new Document();
            Page page = pdf.Pages.Add();

            // 2️⃣ Open the image that will be placed on the page
            using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
            {
                // 3️⃣ Define where the image will sit on the page (points)
                Rectangle placement = new Rectangle(0, 0, 600, 800);

                // 4️⃣ Define the crop area – upper‑left quarter of the image
                Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

                // 5️⃣ Add the image using both placement and crop rectangles
                page.AddImage(imgStream, placement, crop);
            }

            // (Optional) Save the PDF to verify the result
            pdf.Save("YOUR_DIRECTORY/output.pdf");

            Console.WriteLine("PDF created and image cropped successfully!");
        }
    }
}
```

プログラムを実行し、`output.pdf` を開くと、`image.jpg` の左上四分の一だけがページ左上に描画されているのが確認できます。`crop` 矩形の値を変更して、さまざまなスライスを試してみてください。

---

## 結論

Aspose.PDF for C# を使用した **PDF の画像トリミング** の全プロセスを解説しました。新規ドキュメントの作成から **画像で PDF を作成**、**PDF に画像を追加**、カスタム **画像トリミング矩形** の適用、そして最終的に **画像付き PDF を保存** するまでを順を追って実演しました。これで請求書、マーケティングブローシャ、レポートなど、任意の PDF に正確にトリミングされた画像を埋め込めます。次は `TextFragment` でキャプションを追加したり、トリミング画像の周囲にシェイプを描画して強調したりするとさらに効果的です。  

他に知りたいシナリオがあればコメントで教えてください。ハッピーコーディング！

## 次に学ぶべきことは？

- [Aspose.PDF for .NET を使用して PDF の画像サイズを設定する方法](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [Aspose.PDF for .NET を使用して PDF に画像スタンプを追加する方法：包括的ガイド](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [Aspose.PDF for .NET を使用して PDF から画像情報を抽出する方法](/pdf/english/net/images-graphics/extract-image-info-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}