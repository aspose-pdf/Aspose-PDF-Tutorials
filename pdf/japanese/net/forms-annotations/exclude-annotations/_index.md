---
title: Aspose.Pdf for .NET を使用した注釈除外のサイドバイサイド PDF 比較
weight: 101
limit:
description: Aspose.Pdf for .NET を使用して PDF を比較し、注釈領域を除外する手順ごとのガイドです。
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Aspose.Pdf for .NET を使用して PDF を比較し、注釈領域を除外する手順ごとのガイドです。
  headline: Aspose.Pdf for .NET を使用した注釈除外のサイドバイサイド PDF 比較
  type: TechArticle
- description: Aspose.Pdf for .NET を使用して PDF を比較し、注釈領域を除外する手順ごとのガイドです。
  name: Aspose.Pdf for .NET を使用した注釈除外のサイドバイサイド PDF 比較
  steps:
  - name: プライマリ PDF、セカンダリ PDF、および出力差分 PDF のファイルパスを定義します。
    text: プライマリ PDF、セカンダリ PDF、および出力差分 PDF のファイルパスを定義します。
  - name: 両方の入力 PDF ファイルが存在することを確認し、どちらかが欠落している場合はエラーメッセージで中止します。
    text: 両方の入力 PDF ファイルが存在することを確認し、どちらかが欠落している場合はエラーメッセージで中止します。
  - name: using ブロック内で 2 つの PDF ファイルを Document オブジェクト（pdfA と pdfB）として開き、ブロック終了時に自動的に破棄されるようにします。
    text: using ブロック内で 2 つの PDF ファイルを Document オブジェクト（pdfA と pdfB）として開き、ブロック終了時に自動的に破棄されるようにします。
  - name: pdfA のすべての注釈のバウンディング矩形を収集し、ignoredRectsA に格納します。
    text: pdfA のすべての注釈のバウンディング矩形を収集し、ignoredRectsA に格納します。
  - name: pdfB のすべての注釈のバウンディング矩形を収集し、ignoredRectsB に格納します。
    text: pdfB のすべての注釈のバウンディング矩形を収集し、ignoredRectsB に格納します。
  - name: SideBySideComparisonOptions オブジェクトを作成し、事前に収集した注釈矩形を ExcludeAreas1 と ExcludeAreas2
      に割り当て、比較時にそれらの領域が無視されるようにします。
    text: SideBySideComparisonOptions オブジェクトを作成し、事前に収集した注釈矩形を ExcludeAreas1 と ExcludeAreas2
      に割り当て、比較時にそれらの領域が無視されるようにします。
  - name: 2 つの Document オブジェクトと設定したオプションを使用してサイドバイサイド PDF 比較を実行し、結果を outputPdf に書き込みます。
    text: 2 つの Document オブジェクトと設定したオプションを使用してサイドバイサイド PDF 比較を実行し、結果を outputPdf に書き込みます。
  - name: Document オブジェクトを破棄し、using ブロックを抜けます。
    text: Document オブジェクトを破棄し、using ブロックを抜けます。
  - name: 比較が完了したことと、diff PDF が保存された場所を示す確認メッセージを出力します。
    text: 比較が完了したことと、diff PDF が保存された場所を示す確認メッセージを出力します。
  type: HowTo
- questions:
  - answer: はい。コードは対応する `ignoredRects` リストに矩形を追加しないだけなので、`ExcludeAreas1`/`ExcludeAreas2`
      には空の配列が渡され、比較器はページ全体を処理します。
    question: PDF ページに注釈がまったくない場合はどうなりますか—比較はまだ機能しますか？
  - answer: '`ExcludeAreas1`（または `ExcludeAreas2`）に収集した矩形を設定し、もう一方のプロパティは空の配列のままにします。比較器は指定したドキュメントの領域のみを無視します。'
    question: 1 つのドキュメントの注釈だけを除外し、もう一方の注釈は diff に残すことはできますか？
  - answer: 重複する矩形は比較器内部でマージされるため、重複した注釈領域は二重カウントされずに安全に除外されます。
    question: '`ExcludeAreas` で重複する注釈矩形が問題を引き起こすことはありますか？'
  - answer: はい、`compareOpts.ExcludeTables = true;` を設定します。このフラグは `ExcludeAreas1`/`ExcludeAreas2`
      と併用してテーブル領域も除外します。
    question: 同じオプションオブジェクトを使用して、注釈に加えてテーブルも除外する方法はありますか？
  - answer: コードはリストに追加する前に `if (a != null && a.Rect != null)` をチェックしているので、null の矩形は単にスキップされ、例外はスローされません。
    question: 注釈の `Rect` プロパティが null の場合、コードは例外をスローしますか？
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: 注釈なしで PDF を比較する
og_description: すべての注釈マークをスキップするサイドバイサイド PDF 差分を実行します。
og_image_alt: Aspose.Pdf for .NET を使用して注釈領域を除外したサイドバイサイド PDF 比較を示すガイド
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf for .NET を使用した注釈除外のサイドバイサイド PDF 比較
このチュートリアルでは、Aspose.Pdf for .NET を使用して任意の注釈コンテンツを無視しながら 2 つの PDF ファイルを比較する方法を示します。各ドキュメントからすべての注釈のバウンディングボックスを抽出し、それらの領域を SideBySideComparisonOptions に渡してサイドバイサイド比較を実行します。結果は、注釈以外の変更のみをハイライトした diff PDF です。

---

{{< tutorial-widget sourcePath="pdf/net/forms-annotations/exclude-annotations" >}}


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

**Q: PDF ページに注釈がまったくない場合はどうなりますか—比較はまだ機能しますか？**  
A: はい。コードは対応する `ignoredRects` リストに矩形を追加しないだけなので、`ExcludeAreas1`/`ExcludeAreas2` には空の配列が渡され、比較器はページ全体を処理します。

**Q: 1 つのドキュメントの注釈だけを除外し、もう一方の注釈は diff に残すことはできますか？**  
A: `ExcludeAreas1`（または `ExcludeAreas2`）に収集した矩形を設定し、もう一方のプロパティは空の配列のままにします。比較器は指定したドキュメントの領域のみを無視します。

**Q: `ExcludeAreas` で重複する注釈矩形が問題を引き起こすことはありますか？**  
A: 重複する矩形は比較器内部でマージされるため、重複した注釈領域は二重カウントされずに安全に除外されます。

**Q: 同じオプションオブジェクトを使用して、注釈に加えてテーブルも除外する方法はありますか？**  
A: はい、`compareOpts.ExcludeTables = true;` を設定します。このフラグは `ExcludeAreas1`/`ExcludeAreas2` と併用してテーブル領域も除外します。

**Q: 注釈の `Rect` プロパティが null の場合、コードは例外をスローしますか？**  
A: コードはリストに追加する前に `if (a != null && a.Rect != null)` をチェックしているので、null の矩形は単にスキップされ、例外はスローされません。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}