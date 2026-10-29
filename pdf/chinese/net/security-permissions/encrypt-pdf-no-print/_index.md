---
title: 使用 Aspose.PDF for .NET 对 PDF 进行加密并禁用打印权限
weight: 101
limit:
description: 了解如何使用 Aspose.PDF for .NET 通过 AES‑256 加密 PDF 并禁用打印。
keywords: [Aspose.PDF for .NET, pdf encryption aes-256, disable pdf printing, pdf password protection, no print permission pdf]
url: /net/security-permissions/encrypt-pdf-no-print/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: 了解如何使用 Aspose.PDF for .NET 通过 AES‑256 加密 PDF 并禁用打印。
  headline: 使用 Aspose.PDF for .NET 对 PDF 进行加密并禁用打印权限
  type: TechArticle
- description: 了解如何使用 Aspose.PDF for .NET 通过 AES‑256 加密 PDF 并禁用打印。
  name: 使用 Aspose.PDF for .NET 对 PDF 进行加密并禁用打印权限
  steps:
  - name: 定义源 PDF 路径、输出受保护文件名，以及查看者密码和所有者密码。
    text: 定义源 PDF 路径、输出受保护文件名，以及查看者密码和所有者密码。
  - name: 检查源文件是否存在，如果缺失则以错误信息中止。
    text: 检查源文件是否存在，如果缺失则以错误信息中止。
  - name: 打开原始 PDF，设置无权限，使用指定的密码通过 AES‑256 加密，并保存受保护的文件。
    text: 打开原始 PDF，设置无权限，使用指定的密码通过 AES‑256 加密，并保存受保护的文件。
  - name: 使用查看者密码重新打开加密的 PDF，并将其 IsEncrypted 标志写入控制台以确认已受保护。
    text: 使用查看者密码重新打开加密的 PDF，并将其 IsEncrypted 标志写入控制台以确认已受保护。
  - name: 打印最终信息，指示加密已完成并显示输出文件名。
    text: 打印最终信息，指示加密已完成并显示输出文件名。
  type: HowTo
- questions:
  - answer: '`Permissions` 是标志枚举；赋值为 `0` 表示未设置任何权限位，因此 Aspose.Pdf 不会授予 PrintDocument
      权限，查看器无法打印 PDF。'
    question: 为什么将 `Permissions rights = 0;` 设置为 0 会禁用打印？
  - answer: 可以，在 `pdfDoc.Encrypt` 调用中将 `CryptoAlgorithm.AESx256` 替换为 `CryptoAlgorithm.AESx128`（或其他受支持的枚举值）；其余代码保持不变。
    question: 我可以使用不同的加密算法，例如 AES‑128，且代码保持不变吗？
  - answer: Aspose.Pdf 会接受相同的密码，但所有者密码将不再提供额外权限；PDF 仍会被加密，且您指定的权限（无）仍然生效。
    question: 如果查看者密码和主（所有者）密码相同会怎样？
  - answer: 使用查看者密码打开受保护的文件（`new Document(securedFile, viewerPwd)`），并尝试在 PDF 查看器中打印；由于未设置
      `PrintDocument` 权限，查看器会拒绝打印指令。
    question: 如何确认加密后打印真的被阻止？
  - answer: 代码会检查 `File.Exists(sourceFile)`，在返回前向 `Console.Error` 写入错误信息，从而防止 `Document`
      构造函数抛出 `FileNotFoundException`。
    question: 如果 `original.pdf` 不存在会抛出什么错误，应该如何处理？
  type: FAQPage
images:
- /net/security-permissions/encrypt-pdf-no-print/og-image.png
og_title: 加密 PDF 并阻止打印
og_description: 使用 AES‑256 加密保护您的 PDF，并确保其无法打印——一步步指南。
og_image_alt: 截图显示 Aspose.PDF for .NET 代码，用于加密 PDF 并禁用打印。
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.PDF for .NET 对 PDF 进行加密并禁用打印权限
本教程展示如何使用 Aspose.PDF for .NET 打开现有 PDF，应用 AES‑256 加密且不授予任何权限——从而实际禁用打印——保存受保护的文档，并通过使用查看者密码打开来确认保护。按照逐步代码操作，以确保 PDF 在加密后无法打印。

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

**Q: 为什么将 `Permissions rights = 0;` 设置为 0 会禁用打印？**  
A: `Permissions` 是标志枚举；赋值为 `0` 表示未设置任何权限位，因此 Aspose.Pdf 不会授予 PrintDocument 权限，查看器无法打印 PDF。

**Q: 我可以使用不同的加密算法，例如 AES‑128，且代码保持不变吗？**  
A: 可以，在 `pdfDoc.Encrypt` 调用中将 `CryptoAlgorithm.AESx256` 替换为 `CryptoAlgorithm.AESx128`（或其他受支持的枚举值）；其余代码保持不变。

**Q: 如果查看者密码和主（所有者）密码相同会怎样？**  
A: Aspose.Pdf 会接受相同的密码，但所有者密码将不再提供额外权限；PDF 仍会被加密，且您指定的权限（无）仍然生效。

**Q: 如何确认加密后打印真的被阻止？**  
A: 使用查看者密码打开受保护的文件（`new Document(securedFile, viewerPwd)`），并尝试在 PDF 查看器中打印；由于未设置 `PrintDocument` 权限，查看器会拒绝打印指令。

**Q: 如果 `original.pdf` 不存在会抛出什么错误，应该如何处理？**  
A: 代码会检查 `File.Exists(sourceFile)`，在返回前向 `Console.Error` 写入错误信息，从而防止 `Document` 构造函数抛出 `FileNotFoundException`。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}