---
title: 使用 Aspose.Pdf for .NET 对 PDF 进行仅表单填写的 AES‑256 加密
weight: 201
limit:
description: 了解如何使用 Aspose.Pdf for .NET 对 PDF 进行 AES‑256 加密，限制为仅表单填写，并设置查看者/所有者密码。
keywords: [Aspose.Pdf for .NET, PDF encryption .NET, restrict PDF permissions, form filling permission PDF, AES-256 PDF encryption, set PDF passwords .NET]
url: /net/security-permissions/encrypt-form-filling/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: 了解如何使用 Aspose.Pdf for .NET 对 PDF 进行 AES‑256 加密，限制为仅表单填写，并设置查看者/所有者密码。
  headline: 使用 Aspose.Pdf for .NET 对 PDF 进行仅表单填写的 AES‑256 加密
  type: TechArticle
- description: 了解如何使用 Aspose.Pdf for .NET 对 PDF 进行 AES‑256 加密，限制为仅表单填写，并设置查看者/所有者密码。
  name: 使用 Aspose.Pdf for .NET 对 PDF 进行仅表单填写的 AES‑256 加密
  steps:
  - name: 声明源 PDF 路径、输出路径以及查看者密码和所有者密码。
    text: 声明源 PDF 路径、输出路径以及查看者密码和所有者密码。
  - name: 检查源文件是否存在；如果不存在，写入错误信息并退出。
    text: 检查源文件是否存在；如果不存在，写入错误信息并退出。
  - name: 进入 try 块，并使用 `using` 语句打开 PDF 文档，创建 `pdfDoc` 变量。
    text: 进入 try 块，并使用 `using` 语句打开 PDF 文档，创建 `pdfDoc` 变量。
  - name: 创建一个仅允许填写表单的 `Permissions` 对象。
    text: 创建一个仅允许填写表单的 `Permissions` 对象。
  - name: 使用查看者密码和主密码对 `pdfDoc` 进行加密，应用权限集合并使用 AES‑256。
    text: 使用查看者密码和主密码对 `pdfDoc` 进行加密，应用权限集合并使用 AES‑256。
  - name: 将加密后的 PDF 保存到指定的输出文件，并关闭 `using` 块。
    text: 将加密后的 PDF 保存到指定的输出文件，并关闭 `using` 块。
  - name: 向控制台写入确认信息并关闭 try 块。
    text: 向控制台写入确认信息并关闭 try 块。
  - name: 捕获任何异常，将其消息输出到错误流，并关闭 catch 块。
    text: 捕获任何异常，将其消息输出到错误流，并关闭 catch 块。
  type: HowTo
- questions:
  - answer: '`Permissions.FillForm` 允许用户填写交互式表单字段，但禁用所有其他操作，如打印、内容提取或修改文档结构。'
    question: '`Permissions.FillForm` 标志在加密的 PDF 中实际允许和阻止哪些操作？'
  - answer: 可以，在 `pdfDoc.Encrypt` 方法中将 `CryptoAlgorithm.AESx256` 替换为 `CryptoAlgorithm.AESx128`（或其他受支持的枚举值），即可更改加密强度。
    question: 我可以在同一个 `Encrypt` 调用中使用不同的加密算法，例如 AES‑128 吗？
  - answer: 查看者密码（`readPass`）用于打开 PDF 并强制执行指定的权限，而所有者密码（`fullPass`）授予完全不受限制的访问权，可用于更改权限或移除加密。
    question: 查看者密码（`viewerPwd`）和所有者密码（`masterPwd`）有什么区别？
  - answer: 传入 `Permissions.None`（或省略该参数）会生成一个没有特殊限制的 PDF，意味着查看者密码仍然保护文件，但用户可以执行所有标准操作，如打印和复制。
    question: 如果我省略 `permissionSet` 参数或传入 `Permissions.None`，加密后 PDF 会有什么权限？
  type: FAQPage
images:
- /net/security-permissions/encrypt-form-filling/og-image.png
og_title: 使用 AES‑256 对 PDF 进行仅表单填写的加密
og_description: 使用 Aspose.Pdf for .NET 的 AES‑256 加密和密码，确保 PDF 只能被用户填写表单。
og_image_alt: 截图显示使用 Aspose.Pdf for .NET 加密 PDF 并将其限制为仅表单填写的步骤
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Pdf for .NET 对 PDF 进行仅表单填写的 AES‑256 加密
本教程展示如何保护已有的 PDF，使用户只能填写表单。它演示了使用 Aspose.Pdf for .NET 打开文档、将权限限制为表单填写、应用 AES‑256 加密、设置查看者密码和所有者密码，最后保存安全文件的过程。

---

{{< tutorial-widget sourcePath="pdf/net/security-permissions/encrypt-form-filling" >}}


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

**Q: `Permissions.FillForm` 标志在加密的 PDF 中实际允许和阻止哪些操作？**  
A: `Permissions.FillForm` 允许用户填写交互式表单字段，但禁用所有其他操作，如打印、内容提取或修改文档结构。

**Q: 我可以在同一个 `Encrypt` 调用中使用不同的加密算法，例如 AES‑128 吗？**  
A: 可以，在 `pdfDoc.Encrypt` 方法中将 `CryptoAlgorithm.AESx256` 替换为 `CryptoAlgorithm.AESx128`（或其他受支持的枚举值），即可更改加密强度。

**Q: 查看者密码（`viewerPwd`）和所有者密码（`masterPwd`）有什么区别？**  
A: 查看者密码（`readPass`）用于打开 PDF 并强制执行指定的权限，而所有者密码（`fullPass`）授予完全不受限制的访问权，可用于更改权限或移除加密。

**Q: 如果我省略 `permissionSet` 参数或传入 `Permissions.None`，加密后 PDF 会有什么权限？**  
A: 传入 `Permissions.None`（或省略该参数）会生成一个没有特殊限制的 PDF，意味着查看者密码仍然保护文件，但用户可以执行所有标准操作，如打印和复制。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}