---
title: Aspose.Pdf for .NET を使用して、ツールチップ付きのタグ付け外部リンクを PDF に追加する
weight: 440
limit:
description: Aspose.Pdf for .NET を使用して、表示テキストとツールチップを持つタグ付け外部ハイパーリンクを PDF に追加する方法を学びます。
keywords: [Aspose.Pdf for .NET, add external link pdf, tagged pdf hyperlink, pdf tooltip title, pdf logical structure, c# pdf hyperlink]
url: /net/programming-with-tagged-pdf/add-external-link/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Aspose.Pdf for .NET を使用して、表示テキストとツールチップを持つタグ付け外部ハイパーリンクを PDF に追加する方法を学びます。
  headline: Aspose.Pdf for .NET を使用して、ツールチップ付きのタグ付け外部リンクを PDF に追加する
  type: TechArticle
- description: Aspose.Pdf for .NET を使用して、表示テキストとツールチップを持つタグ付け外部ハイパーリンクを PDF に追加する方法を学びます。
  name: Aspose.Pdf for .NET を使用して、ツールチップ付きのタグ付け外部リンクを PDF に追加する
  steps:
  - name: ソース PDF と結果ファイルのパスを定義します。
    text: ソース PDF と結果ファイルのパスを定義します。
  - name: ソース PDF が存在するか確認し、見つからない場合は中止します。
    text: ソース PDF が存在するか確認し、見つからない場合は中止します。
  - name: 適切なリソース解放を保証するため、using ブロック内で PDF ドキュメントを開きます。
    text: 適切なリソース解放を保証するため、using ブロック内で PDF ドキュメントを開きます。
  - name: 開いたドキュメントのタグ付けコンテンツマネージャを取得します。
    text: 開いたドキュメントのタグ付けコンテンツマネージャを取得します。
  - name: ドキュメントの言語を English (US) に設定し、ファイル名から派生したタイトルを PDF に付けます。
    text: ドキュメントの言語を English (US) に設定し、ファイル名から派生したタイトルを PDF に付けます。
  - name: 新しい要素を追加する論理構造ツリーのルート要素を取得します。
    text: 新しい要素を追加する論理構造ツリーのルート要素を取得します。
  - name: リンク要素を作成し、表示テキスト、ターゲット URL、ツールチップタイトルを設定してから、ドキュメントの構造に挿入します。
    text: リンク要素を作成し、表示テキスト、ターゲット URL、ツールチップタイトルを設定してから、ドキュメントの構造に挿入します。
  - name: 更新された PDF を指定された結果ファイルに保存します。
    text: 更新された PDF を指定された結果ファイルに保存します。
  - name: 変更された PDF が保存された場所を示す確認メッセージを出力します。
    text: 変更された PDF が保存された場所を示す確認メッセージを出力します。
  type: HowTo
- questions:
  - answer: '`pdfDoc.TaggedContent` は、ドキュメントがすでにタグ付けされている場合は既存のタグ付けコンテンツを返します。重複したツリーは作成されません。'
    question: ソース PDF がすでにタグ付けされている場合、`pdfDoc.TaggedContent` を呼び出すと新しいタグツリーが作成されますか、それとも既存のものが再利用されますか？
  - answer: 'はい。論理構造ツリーを介して目的の `StructureElement`（例: ページ上の `Div` や `Paragraph`）を見つけ、その要素に対して
      `AppendChild(externalLink)` を呼び出します。'
    question: ハイパーリンクをルート要素に追加するのではなく、特定のページに配置できますか？
  - answer: ツールチップは `externalLink.Title` が `pdfDoc.Save` 前に設定された場合にのみ表示されます。保存後に設定しても、既に書き込まれた
      PDF には影響しません。
    question: '`LinkElement` の `Title` プロパティはツールチップを表示するために必須ですか？また、`Save` 呼び出し後に設定できますか？'
  - answer: '`WebHyperlink` の代わりに、`externalLink.Hyperlink` に `FileSpecification`（例:
      `new FileSpecification(\"file:///C:/Docs/manual.pdf\")`）を割り当てます。'
    question: Web URL の代わりにローカルファイルへのリンクを作成するにはどうすればよいですか？
  type: FAQPage
images:
- /net/programming-with-tagged-pdf/add-external-link/og-image.png
og_title: PDF にツールチップ付きのタグ付け外部リンクを挿入する
og_description: Aspose.Pdf for .NET を使用して、表示テキストとツールチップを持つアクセシブルなハイパーリンクを PDF に埋め込みます。
og_image_alt: Aspose.Pdf for .NET を使用して、ツールチップ付きのタグ付け外部ハイパーリンクを PDF に追加する方法を示すガイド
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf for .NET を使用して、ツールチップ付きのタグ付け外部リンクを PDF に追加する
このチュートリアルでは、Aspose.Pdf for .NET を使用して既存の PDF を開き、表示テキストとツールチップタイトルを含むタグ付けされた外部ハイパーリンクを作成し、そのリンクをドキュメントの論理構造に挿入し、更新されたファイルを保存する方法を示します。手順に従うことで、リンクがタグ階層の一部となり、読者に追加のコンテキストを提供するアクセシブルな PDF を作成できます。

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-tagged-pdf/add-external-link" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: ソース PDF がすでにタグ付けされている場合、`pdfDoc.TaggedContent` を呼び出すと新しいタグツリーが作成されますか、それとも既存のものが再利用されますか？**  
A: `pdfDoc.TaggedContent` は、ドキュメントがすでにタグ付けされている場合は既存のタグ付けコンテンツを返します。重複したツリーは作成されません。

**Q: ハイパーリンクをルート要素に追加するのではなく、特定のページに配置できますか？**  
A: はい。論理構造ツリーを介して目的の `StructureElement`（例: ページ上の `Div` や `Paragraph`）を見つけ、その要素に対して `AppendChild(externalLink)` を呼び出します。

**Q: `LinkElement` の `Title` プロパティはツールチップを表示するために必須ですか？また、`Save` 呼び出し後に設定できますか？**  
A: ツールチップは `externalLink.Title` が `pdfDoc.Save` 前に設定された場合にのみ表示されます。保存後に設定しても、既に書き込まれた PDF には影響しません。

**Q: Web URL の代わりにローカルファイルへのリンクを作成するにはどうすればよいですか？**  
A: `WebHyperlink` の代わりに、`externalLink.Hyperlink` に `FileSpecification`（例: `new FileSpecification(\"file:///C:/Docs/manual.pdf\")`）を割り当てます。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}