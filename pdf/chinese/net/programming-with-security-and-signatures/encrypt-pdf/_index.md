---
title: 使用 Aspose.PDF for .NET 通过用户和所有者密码加密 PDF
weight: 220
limit:
description: 学习如何加载 PDF，限制权限，使用 AES‑256 通过用户和所有者密码进行加密，并使用 Aspose.PDF for .NET 保存受保护的文档。
keywords: [pdf encryption, Aspose.PDF for .NET, aes-256 pdf protection, user password pdf, owner password pdf, restrict pdf permissions]
url: /net/programming-with-security-and-signatures/encrypt-pdf/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: 学习如何加载 PDF，限制权限，使用 AES‑256 通过用户和所有者密码进行加密，并使用 Aspose.PDF for .NET 保存受保护的文档。
  headline: 使用 Aspose.PDF for .NET 通过用户和所有者密码加密 PDF
  type: TechArticle
- description: 学习如何加载 PDF，限制权限，使用 AES‑256 通过用户和所有者密码进行加密，并使用 Aspose.PDF for .NET 保存受保护的文档。
  name: 使用 Aspose.PDF for .NET 通过用户和所有者密码加密 PDF
  steps:
  - name: 声明源文件和目标文件的路径，以及用户（client）和所有者（admin）密码。
    text: 声明源文件和目标文件的路径，以及用户（client）和所有者（admin）密码。
  - name: 检查源 PDF 是否存在，如果不存在则以错误信息中止。
    text: 检查源 PDF 是否存在，如果不存在则以错误信息中止。
  - name: 打开 PDF，仅允许内容修改和提取，使用 AES‑256 和两个密码进行加密，保存受保护的文件，并显示成功信息。
    text: 打开 PDF，仅允许内容修改和提取，使用 AES‑256 和两个密码进行加密，保存受保护的文件，并显示成功信息。
  - name: 捕获所有出现的错误，并将异常信息写入错误控制台。
    text: 捕获所有出现的错误，并将异常信息写入错误控制台。
  type: HowTo
- questions:
  - answer: '`Permissions.ModifyContent` 允许用户编辑 PDF 的文本和对象，而 `Permissions.ExtractContent`
      允许复制文本或图像。两者结合可实现内容编辑和提取，但仍会阻止打印，因为未包含 `Permissions.Print`。'
    question: 当我将 `Permissions.ModifyContent` 与 `Permissions.ExtractContent` 组合使用时，会授予哪些权限？
  - answer: 可以，在 `Encrypt` 调用中将 `CryptoAlgorithm.AESx256` 替换为其他枚举值，例如 `CryptoAlgorithm.AESx128`；其余代码保持不变。
    question: 我可以使用其他加密算法，例如 AES‑128，而不是 `CryptoAlgorithm.AESx256` 吗？
  - answer: 用户密码（`clientPwd`）用于打开 PDF 并强制执行指定的权限，而所有者密码（`adminPwd`）则拥有完整访问权限，持有者可以更改权限或移除加密。
    question: 用户（client）密码与所有者（admin）密码在实际使用中有什么区别？
  - answer: PDF 仍会被加密，但用户和所有者权限的区别消失；任何知道该唯一密码的人都能获得完整访问权限，实际上使权限设置失效。
    question: 如果我为 client 和 admin 密码设置相同的字符串会怎样？
  type: FAQPage
images:
- /net/programming-with-security-and-signatures/encrypt-pdf/og-image.png
og_title: 使用用户和所有者密码（AES‑256）加密 PDF
og_description: 只需几分钟，即可通过添加用户和所有者密码并使用 AES‑256 加密来保护您的 PDF。
og_image_alt: 指南展示如何在 Aspose.PDF for .NET 中使用 AES‑256 通过用户和所有者密码加密 PDF
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.PDF for .NET 通过用户和所有者密码加密 PDF
本教程引导您使用 Aspose.PDF 加载已有 PDF，应用权限限制，并通过使用 AES‑256 算法的用户（client）密码和所有者（admin）密码进行加密来保护文档，最后保存受保护的文件。

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-security-and-signatures/encrypt-pdf" >}}


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

**Q: 当我将 `Permissions.ModifyContent` 与 `Permissions.ExtractContent` 组合使用时，会授予哪些权限？**  
A: `Permissions.ModifyContent` 允许用户编辑 PDF 的文本和对象，而 `Permissions.ExtractContent` 允许复制文本或图像。两者结合可实现内容编辑和提取，但仍会阻止打印，因为未包含 `Permissions.Print`。

**Q: 我可以使用其他加密算法，例如 AES‑128，而不是 `CryptoAlgorithm.AESx256` 吗？**  
A: 可以，在 `Encrypt` 调用中将 `CryptoAlgorithm.AESx256` 替换为其他枚举值，例如 `CryptoAlgorithm.AESx128`；其余代码保持不变。

**Q: 用户（client）密码与所有者（admin）密码在实际使用中有什么区别？**  
A: 用户密码（`clientPwd`）用于打开 PDF 并强制执行指定的权限，而所有者密码（`adminPwd`）则拥有完整访问权限，持有者可以更改权限或移除加密。

**Q: 如果我为 client 和 admin 密码设置相同的字符串会怎样？**  
A: PDF 仍会被加密，但用户和所有者权限的区别消失；任何知道该唯一密码的人都能获得完整访问权限，实际上使权限设置失效。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}