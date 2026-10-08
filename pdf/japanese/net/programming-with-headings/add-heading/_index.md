---
title: Aspose.PDF for .NET を使用して PDF に見出し、言語、タイトルを追加する
weight: 110
limit:
description: Aspose.PDF for .NET を使用して PDF を作成し、言語とタイトルを設定し、レベル 1 の見出しを追加します。
keywords: [Aspose.PDF for .NET, add heading pdf .net, set pdf language, pdf document title, ITaggedContent example, StructureElement pdf]
url: /net/programming-with-headings/add-heading/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Aspose.PDF for .NET を使用して PDF を作成し、言語とタイトルを設定し、レベル 1 の見出しを追加します。
  headline: Aspose.PDF for .NET を使用して PDF に見出し、言語、タイトルを追加する
  type: TechArticle
- description: Aspose.PDF for .NET を使用して PDF を作成し、言語とタイトルを設定し、レベル 1 の見出しを追加します。
  name: Aspose.PDF for .NET を使用して PDF に見出し、言語、タイトルを追加する
  steps:
  - name: 生成された PDF の出力ファイル名を定義します。
    text: 生成された PDF の出力ファイル名を定義します。
  - name: '`using` ブロック内で新しい空の PDF ドキュメントインスタンス（`pdfDoc`）を作成します。'
    text: '`using` ブロック内で新しい空の PDF ドキュメントインスタンス（`pdfDoc`）を作成します。'
  - name: タグ付けされた PDF 構造を操作するために `ITaggedContent` インターフェイスを取得します。
    text: タグ付けされた PDF 構造を操作するために `ITaggedContent` インターフェイスを取得します。
  - name: ドキュメントのデフォルト言語を英語（米国）に設定し、タイトルメタデータを割り当てます。
    text: ドキュメントのデフォルト言語を英語（米国）に設定し、タイトルメタデータを割り当てます。
  - name: 論理構造ツリーのルート要素を取得します。
    text: 論理構造ツリーのルート要素を取得します。
  - name: レベル 1 のヘッダー要素を作成し、表示テキストを設定し、言語を指定します。
    text: レベル 1 のヘッダー要素を作成し、表示テキストを設定し、言語を指定します。
  - name: ヘッダー要素をルートに追加し、見出しが PDF に表示されるようにします。
    text: ヘッダー要素をルートに追加し、見出しが PDF に表示されるようにします。
  - name: PDF を指定されたファイルに保存し、ドキュメントのスコープを閉じます。
    text: PDF を指定されたファイルに保存し、ドキュメントのスコープを閉じます。
  - name: コンソールに確認メッセージを出力します。
    text: コンソールに確認メッセージを出力します。
  type: HowTo
- questions:
  - answer: '`SetLanguage` はドキュメント全体の論理構造のデフォルト言語を定義します。個別に言語が設定されていない要素は「en-US」を継承します。'
    question: '`tagContent.SetLanguage(\"en-US\")` を PDF に呼び出すとどのような効果がありますか？'
  - answer: '`header.Language` の設定は任意です。例に示すように別の値を割り当てない限り、見出しはドキュメントのデフォルト言語を継承します。'
    question: ドキュメントで既に `SetLanguage` を呼び出している場合、`header.Language` を設定する必要がありますか？
  - answer: '`tagContent.CreateHeaderElement(2)` を使用してレベル 2 の見出しを作成します。数値引数は PDF の構造ツリーに反映される見出しレベルを指定します。'
    question: レベル 1 の見出しではなく、レベル 2 の見出しを作成するにはどうすればよいですか？
  - answer: '`SetTitle` は指定された文字列を PDF のドキュメントメタデータのタイトルフィールドに書き込みます。この情報は PDF リーダーで表示でき、検索やインデックス作成に使用されます。'
    question: '`tagContent.SetTitle(\"PDF Example with Header\")` は何を行いますか？'
  - answer: 見出し要素が論理構造ツリーに追加されないため、PDF の出力に表示されず、アクセシビリティツールでも見出しとして認識されません。
    question: '`rootElement.AppendChild(header)` を省略するとどうなりますか？'
  type: FAQPage
images:
- /net/programming-with-headings/add-heading/og-image.png
og_title: PDF に見出しを挿入し、言語を設定する
og_description: .NET の数行のコードで PDF を作成し、言語とタイトルを設定し、レベル 1 の見出しを追加する方法を学びます。
og_image_alt: Aspose.PDF for .NET を使用して PDF に見出し、言語、タイトルを追加する方法を示すガイド
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.PDF for .NET を使用して PDF に見出し、言語、タイトルを追加する
このチュートリアルでは、Aspose.PDF for .NET を使用して新しい PDF ドキュメントを作成し、デフォルト言語とドキュメントタイトルを割り当て、レベル 1 の見出しを挿入する手順を説明します。Document、ITaggedContent、StructureElement、HeaderElement クラスを使用して、アクセシビリティツールに適した適切にタグ付けされた PDF を生成する方法がわかります。

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-headings/add-heading" >}}


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

**Q: `tagContent.SetLanguage(\"en-US\")` を PDF に呼び出すとどのような効果がありますか？**  
A: `SetLanguage` はドキュメント全体の論理構造のデフォルト言語を定義します。個別に言語が設定されていない要素は「en-US」を継承します。

**Q: ドキュメントで既に `SetLanguage` を呼び出している場合、`header.Language` を設定する必要がありますか？**  
A: `header.Language` の設定は任意です。例に示すように別の値を割り当てない限り、見出しはドキュメントのデフォルト言語を継承します。

**Q: レベル 1 の見出しではなく、レベル 2 の見出しを作成するにはどうすればよいですか？**  
A: `tagContent.CreateHeaderElement(2)` を使用してレベル 2 の見出しを作成します。数値引数は PDF の構造ツリーに反映される見出しレベルを指定します。

**Q: `tagContent.SetTitle(\"PDF Example with Header\")` は何を行いますか？**  
A: `SetTitle` は指定された文字列を PDF のドキュメントメタデータのタイトルフィールドに書き込みます。この情報は PDF リーダーで表示でき、検索やインデックス作成に使用されます。

**Q: `rootElement.AppendChild(header)` を省略するとどうなりますか？**  
A: 見出し要素が論理構造ツリーに追加されないため、PDF の出力に表示されず、アクセシビリティツールでも見出しとして認識されません。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}