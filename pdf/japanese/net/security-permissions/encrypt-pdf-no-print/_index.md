---
title: Aspose.PDF for .NET を使用した印刷不可権限での PDF 暗号化
weight: 101
limit:
description: Aspose.PDF for .NET を使用して AES‑256 で PDF を暗号化し、印刷を無効にする方法を学びましょう。
keywords: [Aspose.PDF for .NET, pdf encryption aes-256, disable pdf printing, pdf password protection, no print permission pdf]
url: /net/security-permissions/encrypt-pdf-no-print/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Aspose.PDF for .NET を使用して AES‑256 で PDF を暗号化し、印刷を無効にする方法を学びましょう。
  headline: Aspose.PDF for .NET を使用した印刷不可権限での PDF 暗号化
  type: TechArticle
- description: Aspose.PDF for .NET を使用して AES‑256 で PDF を暗号化し、印刷を無効にする方法を学びましょう。
  name: Aspose.PDF for .NET を使用した印刷不可権限での PDF 暗号化
  steps:
  - name: ソース PDF のパス、出力する保護ファイル名、ビューアパスワードとオーナーパスワードを定義します。
    text: ソース PDF のパス、出力する保護ファイル名、ビューアパスワードとオーナーパスワードを定義します。
  - name: ソースファイルが存在するか確認し、存在しない場合はエラーメッセージを出して中止します。
    text: ソースファイルが存在するか確認し、存在しない場合はエラーメッセージを出して中止します。
  - name: 元の PDF を開き、権限を設定せず、指定したパスワードで AES‑256 暗号化し、保護されたファイルとして保存します。
    text: 元の PDF を開き、権限を設定せず、指定したパスワードで AES‑256 暗号化し、保護されたファイルとして保存します。
  - name: 暗号化された PDF をビューアパスワードで再度開き、IsEncrypted フラグをコンソールに出力して保護が確認できることを示します。
    text: 暗号化された PDF をビューアパスワードで再度開き、IsEncrypted フラグをコンソールに出力して保護が確認できることを示します。
  - name: 暗号化が完了し、出力ファイル名を示す最終メッセージを表示します。
    text: 暗号化が完了し、出力ファイル名を示す最終メッセージを表示します。
  type: HowTo
- questions:
  - answer: '`Permissions` はフラグ列挙型です。`0` を割り当てると権限ビットがすべて立たないため、Aspose.Pdf は PrintDocument
      権限を付与せず、ビューアは PDF を印刷できません。'
    question: なぜ `Permissions rights = 0;` と設定すると印刷が無効になるのでしょうか？
  - answer: はい、`pdfDoc.Encrypt` 呼び出しで `CryptoAlgorithm.AESx256` を `CryptoAlgorithm.AESx128`（または他のサポートされている列挙値）に置き換えるだけで、残りのコードは変更不要です。
    question: 同じコードで AES‑128 など別の暗号化アルゴリズムを使用できますか？
  - answer: Aspose.Pdf は同一のパスワードを受け付けますが、オーナーパスワードは追加の特権を提供しなくなります。PDF は依然として暗号化され、指定した権限（なし）が適用されます。
    question: ビューアパスワードとマスター（オーナー）パスワードが同じ場合、どうなりますか？
  - answer: 保護されたファイルをビューアパスワードで開き（`new Document(securedFile, viewerPwd)`）、PDF ビューアから印刷を試みます。`PrintDocument`
      権限が設定されていないため、ビューアは印刷コマンドを拒否します。
    question: 暗号化後に印刷が本当にブロックされているか、どう確認すればよいですか？
  - answer: コードは `File.Exists(sourceFile)` をチェックし、存在しなければ `Console.Error` にエラーを書き込んでからリターンするため、`Document`
      コンストラクタで `FileNotFoundException` がスローされるのを防ぎます。
    question: '`original.pdf` が存在しない場合、どのようなエラーがスローされ、どのように対処すべきですか？'
  type: FAQPage
images:
- /net/security-permissions/encrypt-pdf-no-print/og-image.png
og_title: PDF を暗号化して印刷をブロック
og_description: AES‑256 暗号化で PDF を保護し、印刷できないようにするステップバイステップガイドです。
og_image_alt: Aspose.PDF for .NET のコードで PDF を暗号化し、印刷を無効にする様子を示したスクリーンショット。
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.PDF for .NET を使用した印刷不可権限での PDF 暗号化
このチュートリアルでは、Aspose.PDF for .NET を使用して既存の PDF を開き、権限を付与しない AES‑256 暗号化（実質的に印刷を無効化）を適用し、保護されたドキュメントを保存し、ビューアパスワードで開いて保護を確認する方法を示します。暗号化後に PDF が印刷できないことを保証するためのステップバイステップコードに従ってください。

---

{{< tutorial-widget sourcePath="pdf/net/security-permissions/encrypt-pdf-no-print" >}}


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

**Q: なぜ `Permissions rights = 0;` と設定すると印刷が無効になるのでしょうか？**  
A: `Permissions` はフラグ列挙型です。`0` を割り当てると権限ビットがすべて立たないため、Aspose.Pdf は PrintDocument 権限を付与せず、ビューアは PDF を印刷できません。

**Q: 同じコードで AES‑128 など別の暗号化アルゴリズムを使用できますか？**  
A: はい、`pdfDoc.Encrypt` 呼び出しで `CryptoAlgorithm.AESx256` を `CryptoAlgorithm.AESx128`（または他のサポートされている列挙値）に置き換えるだけで、残りのコードは変更不要です。

**Q: ビューアパスワードとマスター（オーナー）パスワードが同じ場合、どうなりますか？**  
A: Aspose.Pdf は同一のパスワードを受け付けますが、オーナーパスワードは追加の特権を提供しなくなります。PDF は依然として暗号化され、指定した権限（なし）が適用されます。

**Q: 暗号化後に印刷が本当にブロックされているか、どう確認すればよいですか？**  
A: 保護されたファイルをビューアパスワードで開き（`new Document(securedFile, viewerPwd)`）、PDF ビューアから印刷を試みます。`PrintDocument` 権限が設定されていないため、ビューアは印刷コマンドを拒否します。

**Q: `original.pdf` が存在しない場合、どのようなエラーがスローされ、どのように対処すべきですか？**  
A: コードは `File.Exists(sourceFile)` をチェックし、存在しなければ `Console.Error` にエラーを書き込んでからリターンするため、`Document` コンストラクタで `FileNotFoundException` がスローされるのを防ぎます。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}