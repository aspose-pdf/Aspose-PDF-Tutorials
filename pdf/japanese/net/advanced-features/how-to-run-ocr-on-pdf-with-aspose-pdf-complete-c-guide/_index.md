---
category: general
date: 2026-03-22
description: C#でAspose.Pdfを使用してPDFファイルにOCRを実行する方法。スキャンしたPDFを変換し、PDFを検索可能にし、PDFドキュメントを簡単に読み込む方法を学びましょう。
draft: false
keywords:
- how to run OCR
- run OCR on pdf
- convert scanned pdf
- make pdf searchable
- load pdf document
language: ja
og_description: Aspose.Pdf を使用して PDF ファイルで OCR を実行する方法。このチュートリアルでは、スキャンされた PDF を変換し、PDF
  を検索可能にし、C# で PDF ドキュメントをロードする方法を示します。
og_title: PDFでOCRを実行する方法 – 完全C#ガイド
tags:
- OCR
- Aspose.Pdf
- C#
- PDF processing
title: Aspose.PdfでPDFにOCRを実行する方法 – 完全C#ガイド
url: /ja/net/advanced-features/how-to-run-ocr-on-pdf-with-aspose-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDFでOCRを実行する方法 – 完全なC#ガイド

PDFファイルでOCRを実行することは、スキャンした書類を扱う際の一般的なハードルです。スキャンした請求書を検索しようとして壁にぶつかったことはありませんか？あなたは一人ではありません。このチュートリアルでは、Aspose.Pdf を使用して **PDFでOCRを実行** する正確な手順を順を追って説明します。ぼやけたスキャンを完全に検索可能なドキュメントに変換します。最後まで読むと、**スキャンしたPDFを変換**、**PDFを検索可能にする**、そしてもちろん **PDFドキュメントをロード** する方法も習得できます。

プロジェクトの設定から出力の検証まで、すべてをカバーします。手を抜くことなく、「ドキュメント参照」的なショートカットもありません—今日 Visual Studio に貼り付けて実行できる完全なサンプルです。.NET 6 または .NET Framework 4.8 で動作するか気になる方へ、答えはイエスです。Aspose.Pdf は両方をサポートしており、以下のコードは自動的に適応します。

## 前提条件

- **Aspose.Pdf for .NET**（2026年3月時点の最新バージョン）。NuGet から取得できます：`Install-Package Aspose.Pdf`。
- 処理したい **scanned PDF**（参照できるフォルダーに配置してください。例：`YOUR_DIRECTORY/input.pdf`）。
- .NET 6 SDK 以降（構文は `using var` を使用し、C# 8 以降でサポートされています）。
- お好みの IDE—Visual Studio、Rider、または VS Code いずれでも問題なく動作します。

以上です。追加の OCR エンジンや外部サービスは不要です。Aspose の組み込み `OcrPlugin` が重い処理を担います。

## OCR の実行方法 – コアステップ

以下は完全な単体プログラムです。`Program.cs` として保存し実行してください。コンソールは静かに終了し、入力ファイルの隣に検索可能な PDF が生成されます。

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Plugins;

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document you want to OCR
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Step 2: Create a PluginManager – this is the hub for all PDF plugins
        var pluginManager = new PluginManager();

        // Step 3: Register the built‑in OCR plugin (the one that actually reads the image)
        pluginManager.RegisterPlugin(new OcrPlugin());

        // Step 4: Prepare execution options – here we set English as the language.
        // You can add more languages by comma‑separating them, e.g., "eng,spa".
        var ocrOptions = new PluginExecutionOptions
        {
            Parameters = { ["Language"] = "eng" }
        };

        // Step 5: Execute the OCR plugin on the loaded document.
        // This mutates pdfDocument in‑place, turning each scanned page into searchable text.
        pluginManager.Execute(pdfDocument, ocrOptions);

        // Step 6: Save the OCR‑processed PDF to a new file.
        pdfDocument.Save("YOUR_DIRECTORY/ocr-output.pdf");

        Console.WriteLine("OCR complete! Output saved to ocr-output.pdf");
    }
}
```

### コードの動作をステップごとに説明

1. **Load PDF Document** – `Document` コンストラクタはファイルをメモリに読み込みます。これにより “load pdf document” の要件を満たし、操作可能なオブジェクトが得られます。
2. **Plugin Manager** – Aspose は OCR などのオプション機能をマネージャーで分離しています。適切なハンマーを選ぶツールボックスと考えてください。
3. **Register OCR Plugin** – `RegisterPlugin(new OcrPlugin())` を呼び出すことで、Aspose に光学文字認識を実行する意図を伝えます。
4. **Execution Options** – `PluginExecutionOptions` でプロセスを細かく調整できます。`Language` を `"eng"` に設定すると、エンジンは英字文字を対象にします。スペイン語は `"spa"`、ドイツ語は `"deu"` を追加することも可能です。
5. **Run the OCR** – `pluginManager.Execute` は各ページを走査し、ラスタ画像を抽出、OCR エンジンを実行し、不可視のテキストレイヤーを重ねます。これが **run OCR on pdf** の核心です。
6. **Save the Result** – 最終的な PDF には隠しテキストレイヤーが含まれ、**make PDF searchable** になります。Adobe Reader で開き、検索ツールを使えば入力した任意の単語が見つかります。

## ステップ 1: PDF ドキュメントのロード

`using var` を使用し、単なる `new Document()` を使わない理由が気になるかもしれません。`using` 文は処理が完了した時点でファイルハンドルを解放することを保証し、後で Windows 上で同じファイルを上書きしようとする際に重要です。

```csharp
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

パスが間違っていると、Aspose は `FileNotFoundException` をスローします。フォルダーの権限を再確認してください—特に Linux では大文字小文字が区別されるため注意が必要です。

## ステップ 2: OCR プラグインの登録と設定

OCR プラグインはデフォルトではロードされません。これはコアライブラリを軽量に保つためです。登録はワンライナーですが、ワークフローで必要なら複数のプラグイン（例：透かし除去）をチェーンすることもできます。

```csharp
var pluginManager = new PluginManager();
pluginManager.RegisterPlugin(new OcrPlugin());
```

> **Pro tip:** バッチで数百枚の PDF を処理する予定がある場合、`PluginManager` を一度だけインスタンス化して再利用してください。ファイルごとに作成すると不要なオーバーヘッドが発生します。

## ステップ 3: OCR プロセスの実行（スキャンした PDF の変換）

いよいよ本格的な処理です。`Execute` メソッドは各ページを走査し、OCR を実行し、テキストを PDF に書き戻します。効率的で、Aspose は画像データをストリーミングするため、200 ページのスキャンでもメモリ不足になることはありません。

```csharp
var ocrOptions = new PluginExecutionOptions
{
    Parameters = { ["Language"] = "eng" }
};

pluginManager.Execute(pdfDocument, ocrOptions);
```

**Why set the language?** OCR の精度は言語モデルに大きく依存します。`"eng"` を指定すると、エンジンは英字文字形状を優先し、誤検出を減らします。

## ステップ 4: 検索可能な PDF の保存と検証

保存はシンプルですが、検証で多くの開発者がつまずきます。実行後、任意の PDF ビューアで出力を開き、**Ctrl + F** ショートカットを試してください。元は画像だった単語が見つかれば、**make PDF searchable** に成功したことになります。

```csharp
pdfDocument.Save("YOUR_DIRECTORY/ocr-output.pdf");
```

![OCR 後の検索可能な PDF – PDFでOCRを実行する方法](/images/ocr-searchable.png "OCR 実行後の検索可能な PDF（PDFでOCRを実行する方法）")

*上のスクリーンショットは、用語を検索した際に隠しテキストレイヤーがハイライトされる様子を示しています。*

## よくある落とし穴とプロのコツ

| 問題 | 発生理由 | 対策 |
|-------|----------------|-----|
| **空白の出力** | Language パラメータが欠如しているか、サポートされていないコードに設定されています。 | `["Language"] = "eng"`（または他の ISO‑639‑2 コード）を設定してください。 |
| **処理が遅い** | ダウンサンプリングなしの大きな画像です。 | `Parameters` に `["Resolution"] = "300"` を追加し、OCR を低 DPI で実行させます。 |
| **フォントが欠如** | OCR はテキストを生成しますが、ビューアがフォントをレンダリングできません。 | `pdfDocument.FontEmbeddingMode = FontEmbeddingMode.Always` を設定してフォントを埋め込みます。 |
| **メモリリーク** | `Document` オブジェクトを破棄していないためです。 | 示したように `using var` を使用するか、手動で `pdfDocument.Dispose()` を呼び出してください。 |

### エッジケース

- **Multi‑language PDFs:** 混在コンテンツを処理するには、`"eng,spa,fra"` のようにカンマ区切りのリストを渡します。
- **Password‑protected files:** `new Document("file.pdf", new LoadOptions { Password = "secret" })` でロードします。
- **Selective OCR:** 特定のページだけ OCR が必要な場合、`PageRange` オブジェクトを作成し、`Parameters["Pages"] = "1-3,5"` として渡します。

## まとめ: 達成したこと

- **How to run OCR on PDF** – Aspose.Pdf の組み込みプラグインを使用。
- **Convert scanned PDF** – 外部サービスなしで検索可能なバージョンに変換。
- **Make PDF searchable** – エンドユーザーがテキストを即座に検索できるように。
- **Load PDF document** – 安全にロードし、リソースを速やかに解放。

これらはすべて、30 行未満のクリーンな C# コードで実現できます。

## 次に試すこと

- 多言語契約書を OCR するために、さまざまな言語で実験してみてください。
- OCR と **text extraction**（`pdfDocument.Pages[i].ExtractText()`）を組み合わせて、データ入力を自動化。
- OCR 前に機密情報を削除するために **Redaction plugin** を使用し、コンプライアンスを確保。
- コードを API エンドポイントの背後にあるマイクロサービスとしてデプロイし、非開発者がスキャンをアップロードして即座に検索可能な PDF を受け取れるように。

このコードをクラウドにスケールさせる方法や Azure Functions との統合について質問がありますか？コメントを残してください。一緒にシナリオを検討しましょう。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}