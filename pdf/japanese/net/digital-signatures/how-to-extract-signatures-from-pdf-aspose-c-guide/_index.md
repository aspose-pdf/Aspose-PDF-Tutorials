---
category: general
date: 2026-04-02
description: C# で Aspose.Pdf を使用して、署名の抽出、フィールドの追加、空白ページ PDF の追加、ウィジェットの追加、そして透明性を保持した
  PDF の作成方法を学びます。
draft: false
keywords:
- how to extract signatures
- how to add field
- add blank page pdf
- how to add widget
- preserve transparency pdf
language: ja
og_description: Aspose.Pdf を使用して PDF から署名を抽出し、フィールドや空白ページ、ウィジェットの追加、透明性の保持などの関連タスクを実行する方法。
og_title: PDFから署名を抽出する方法 – Aspose C# ガイド
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: PDFから署名を抽出する方法 – Aspose C# ガイド
url: /ja/net/digital-signatures/how-to-extract-signatures-from-pdf-aspose-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF から署名を抽出する方法 – Aspose C# ガイド

**PDF から署名を抽出する方法** は、契約書の自動処理や請求書承認、デジタル署名に依存するワークフローを自動化する際の一般的な要件です。  
このガイドでは、Aspose.Pdf for .NET を使用して **フィールドの追加方法**、**空白ページ PDF の追加方法**、**ウィジェットの追加方法**、そして **透明性を保持した PDF の作成方法** も併せて解説します。

毎晩何十件もの署名済み PDF が届くと想像してください。手作業でファイルを開いて署名を確認するのは悪夢です。数行の C# コードで署名者名をプログラム的に取得し、元のグラフィックをそのまま保ちつつ、既存の透明性やカラープロファイルを壊すことなく新しいフォームフィールドを追加できます。

> **得られるもの:** 透明性を保持した PDF/X‑4 への変換、埋め込まれたすべての署名名の抽出、空白ページの追加、同一ページ上の 2 箇所に表示されるテキストボックスフォームフィールドの作成を行う、完全に実行可能なサンプルです。

## 前提条件

- .NET 6.0 以降（コードは .NET Framework でも動作します）
- Aspose.Pdf for .NET **v25.2** 以上（`GetSignatureNames()` が必要です）
- Visual Studio プロジェクトまたは任意の C# IDE
- 以下のサンプル PDF を格納したフォルダー（自分で管理できる場所）  
  - `source.pdf` – 透明性を保ったまま変換したい任意の PDF  
  - `signed.pdf` – すでにデジタル署名が含まれている PDF  
  - （オプション）出力ファイル用の空フォルダー

> **プロのコツ:** まだライセンス版をお持ちでない場合は、Aspose のウェブサイトから無料の一時ライセンスを取得できます。無料モードはテストに使用できますが、透かしが追加されます。

## 手順 1 – PDF/X‑4 に変換して透明性を保持する

PDF をフラット化すると、透明性や埋め込みカラープロファイルが失われがちです。**PDF/X‑4** に変換すれば、これらのビジュアル要素をそのまま保持でき、印刷用ドキュメントに必須です。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

// 1️⃣ Convert source.pdf → PDF/X‑4 (preserves transparency & color profiles)
var conversionOptions = new PdfFormatConversionOptions(
    PdfFormat.PDF_X_4,          // Target format
    ConvertErrorAction.Delete  // Remove pages that cause conversion errors
);

using (var sourceDoc = new Document("YOUR_DIRECTORY/source.pdf"))
{
    sourceDoc.Convert(conversionOptions);
    sourceDoc.Save("YOUR_DIRECTORY/toPdfX4.pdf");
}
```

**重要なポイント:**  
PDF/X‑4 は、ライブ透明性を保持したままグラフィック交換を行うための ISO 標準です。`PdfFormatConversionOptions` を使用することで、透明オブジェクトがラスタライズされてファイルサイズが増大したり画質が低下したりする一般的な落とし穴を回避できます。

## 手順 2 – PDF から署名を抽出する方法

Aspose はバージョン 25.2 で `GetSignatureNames()` を導入し、署名抽出をワンライナーで実現しました。このメソッドは、各デジタル署名フィールドに割り当てられた論理名の配列を返します。

```csharp
using Aspose.Pdf;

// 2️⃣ Pull out every signature name from signed.pdf
using (var signedDoc = new Document("YOUR_DIRECTORY/signed.pdf"))
{
    // Returns strings like "Signature1", "EmployeeSignature", etc.
    string[] signatureNames = signedDoc.GetSignatureNames();   // new method in 25.2

    // Show the names in the console – you could store them in a DB instead
    Console.WriteLine("Found signatures: " + string.Join(", ", signatureNames));
}
```

**期待される出力:** `signed.pdf` に *ManagerSig* と *ClientSig* という 2 つの署名が含まれている場合、コンソールには次のように表示されます。

```
Found signatures: ManagerSig, ClientSig
```

**エッジケースの取り扱い:**  
- PDF に署名がまったくない場合、`GetSignatureNames()` は空配列を返し、例外はスローされません。  
- 署名フィールドが破損している PDF では、呼び出しを `try/catch` でラップし、エラーをログに記録して処理全体を中断しないようにできます。

## 手順 3 – 空白ページ PDF を追加し、複数ウィジェットを持つテキストボックスを作成する

新しいページの追加はシンプルですが、**フィールドの追加方法** と **ウィジェットの追加方法** を組み合わせるには少しコツが必要です。*ウィジェット* はフォームフィールドの視覚的表現であり、同一論理フィールドに複数のウィジェットを紐付けることで、同じデータを複数箇所に表示できます。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;

// 3️⃣ Build a fresh document, add a blank page, then a textbox with two widgets
using (var newDoc = new Document())
{
    // ---- Add a blank page -------------------------------------------------
    var page = newDoc.Pages.Add();   // This is the "add blank page pdf" step

    // ---- Define the primary widget (the actual appearance) ---------------
    var textBox = new TextBoxField(page, new Rectangle(100, 600, 300, 650))
    {
        PartialName = "Comments",               // logical name of the field
        Value = "Enter your comment here"       // default value
    };

    // ---- Add a second widget at a different location ----------------------
    var secondWidget = new WidgetAnnotation(page, new Rectangle(100, 500, 300, 550));
    textBox.Widgets.Add(secondWidget); // This is the "how to add widget" part

    // ---- Register the field with the document's form collection -----------
    newDoc.Form.Add(textBox, "Comments");

    // ---- Save the result --------------------------------------------------
    newDoc.Save("YOUR_DIRECTORY/TextBoxMultipleWidgets.pdf");
}
```

**複数ウィジェットを使う理由:**  
たとえば、契約書の表裏両面に同じコメントを表示したい場合、同一フィールドに 2 つのウィジェットを付与すれば、どちらか一方で変更した内容が自動的にもう一方にも反映されます。

**よくある落とし穴:**  
- `newDoc.Form` にフィールドを追加し忘れると、ウィジェットは PDF ビューアで見えなくなります。  
- 2 つのウィジェットに同一の矩形座標を指定すると重なって表示されます。`Rectangle` の値は必ず異なるように設定してください。

## 手順 4 – すべてを統合した実行可能サンプル

以下は、上記の手順を順番通りに実行する単一プログラムです。新しいコンソールプロジェクトにコピー＆ペーストし、パスを調整して実行してください。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;

namespace AsposePdfDemo
{
    class Program
    {
        static void Main()
        {
            // -----------------------------------------------------------------
            // 1️⃣ Preserve transparency by converting to PDF/X‑4
            // -----------------------------------------------------------------
            var conversionOptions = new PdfFormatConversionOptions(
                PdfFormat.PDF_X_4,
                ConvertErrorAction.Delete);

            using (var sourceDoc = new Document("YOUR_DIRECTORY/source.pdf"))
            {
                sourceDoc.Convert(conversionOptions);
                sourceDoc.Save("YOUR_DIRECTORY/toPdfX4.pdf");
                Console.WriteLine("✅ PDF/X‑4 conversion complete (transparency preserved).");
            }

            // -----------------------------------------------------------------
            // 2️⃣ Extract signature names
            // -----------------------------------------------------------------
            using (var signedDoc = new Document("YOUR_DIRECTORY/signed.pdf"))
            {
                string[] signatureNames = signedDoc.GetSignatureNames(); // new in 25.2
                if (signatureNames.Length == 0)
                    Console.WriteLine("⚠️ No signatures found.");
                else
                    Console.WriteLine("🔍 Found signatures: " + string.Join(", ", signatureNames));
            }

            // -----------------------------------------------------------------
            // 3️⃣ Add a blank page and a textbox with two widgets
            // -----------------------------------------------------------------
            using (var newDoc = new Document())
            {
                // Add a blank page – “add blank page pdf”
                var page = newDoc.Pages.Add();

                // Primary widget for the textbox
                var textBox = new TextBoxField(page, new Rectangle(100, 600, 300, 650))
                {
                    PartialName = "Comments",
                    Value = "Enter your comment here"
                };

                // Second widget – “how to add widget”
                textBox.Widgets.Add(new WidgetAnnotation(page, new Rectangle(100, 500, 300, 550)));

                // Register the field – “how to add field”
                newDoc.Form.Add(textBox, "Comments");

                // Save the final document
                newDoc.Save("YOUR_DIRECTORY/TextBoxMultipleWidgets.pdf");
                Console.WriteLine("✅ Blank page added and textbox with two widgets created.");
            }

            Console.WriteLine("\nAll tasks completed successfully!");
        }
    }
}
```

### 期待される出力

プログラムを実行すると、次のような出力が得られます。

```
✅ PDF/X‑4 conversion complete (transparency preserved).
🔍 Found signatures: ManagerSig, ClientSig
✅ Blank page added and textbox with two widgets created.

All tasks completed successfully!
```

`TextBoxMultipleWidgets.pdf` を Adobe Acrobat Reader で開くと、**Comments** とラベル付けされた同一のテキストボックスが 2 つ（上部とやや下部）表示されます。どちらかに入力すると、もう一方が即座に更新されます。

## よくある質問 (FAQ)

| 質問 | 回答 |
|----------|--------|
| **実際の署名バイト列を取得できますか？** | `GetSignatureNames()` は論理名のみを返します。証明書や署名値を取得するには `SignatureField` オブジェクト（`document.Form["fieldName"] as SignatureField`）を使用してください。 |
| **PDF/X‑4 変換は暗号化された PDF でも機能しますか？** | はい、`Document.Open(file, password)` でパスワードを指定すれば変換できます。 |
| **ウィジェットを 2 つ以上追加したい場合は？** | 追加したい分だけ `textBox.Widgets.Add()` を呼び出せば OK です。 |
| **空白ページは元の PDF と同じサイズになりますか？** | 新しいページはデフォルトサイズ（A4）になります。必要に応じてカスタムサイズの `Page` オブジェクトを渡してください。 |
| **コードは .NET Core と互換性がありますか？** | 完全に対応しています。Aspose.Pdf はクロスプラットフォームです。NuGet パッケージを .NET Core プロジェクトに参照すれば利用できます。 |

## 結論

本チュートリアルでは、**PDF から署名を抽出する方法** を中心に、**フィールドの追加方法**、**空白ページ PDF の追加方法**、**ウィジェットの追加方法**、そして **透明性を保持した PDF の作成方法** を Aspose.Pdf for C# を使って実装しました。これで、任意の文書処理パイプラインに組み込める、堅牢なエンドツーエンドソリューションが手に入りました。

次のチャレンジに挑戦してみませんか？ これらのテクニックに Aspose の OCR モジュールを組み合わせて、スキャン画像からテキストを読み取る処理を作成してみましょう。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}