---
title: 使用 Aspose.Pdf for .NET 加密 PDF，仅允许填写表单
weight: 101
limit:
description: 了解如何使用 Aspose.Pdf for .NET 对 PDF 进行 AES‑256 加密、设置密码，并将权限限制为仅填写表单。
keywords: [Aspose.Pdf for .NET, encrypt PDF, PDF form filling permissions, AES-256 PDF encryption, viewer password PDF, owner password PDF]
url: /net/security-permissions/encrypt-pdf-form-filling/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: 了解如何使用 Aspose.Pdf for .NET 对 PDF 进行 AES‑256 加密、设置密码，并将权限限制为仅填写表单。
  headline: 使用 Aspose.Pdf for .NET 加密 PDF，仅允许填写表单
  type: TechArticle
- description: 了解如何使用 Aspose.Pdf for .NET 对 PDF 进行 AES‑256 加密、设置密码，并将权限限制为仅填写表单。
  name: 使用 Aspose.Pdf for .NET 加密 PDF，仅允许填写表单
  steps:
  - name: 定义源文件和目标文件的路径以及查看者密码和所有者密码。
    text: 定义源文件和目标文件的路径以及查看者密码和所有者密码。
  - name: 检查源 PDF 是否存在，如果不存在则以错误信息中止。
    text: 检查源 PDF 是否存在，如果不存在则以错误信息中止。
  - name: 启动 try 块以处理处理过程中可能出现的任何错误。
    text: 启动 try 块以处理处理过程中可能出现的任何错误。
  - name: 通过创建名为 pdfDoc 的 Document 对象来打开现有 PDF 文件。
    text: 通过创建名为 pdfDoc 的 Document 对象来打开现有 PDF 文件。
  - name: 设置仅允许填写表单的权限，使用 AES‑256 通过查看者密码和所有者密码加密文档，并保存受保护的 PDF。
    text: 设置仅允许填写表单的权限，使用 AES‑256 通过查看者密码和所有者密码加密文档，并保存受保护的 PDF。
  - name: 在控制台写入确认信息并关闭 try 块。
    text: 在控制台写入确认信息并关闭 try 块。
  - name: 捕获任何异常并将错误信息输出到控制台。
    text: 捕获任何异常并将错误信息输出到控制台。
  type: HowTo
- questions:
  - answer: 使用查看者（用户）密码打开时，文档可以被查看并且可以填写表单字段，但所有其他操作，如编辑文本、添加批注或提取内容，均被阻止。
    question: 使用 `Permissions.FillForm` 加密后，用户可以对 PDF 做些什么？
  - answer: 使用按位或运算符组合权限，例如 `Permissions allowed = Permissions.FillForm | Permissions.Printing;`，并将组合后的值传递给
      `pdfDoc.Encrypt`。
    question: 如何在仍然限制其他所有操作的同时，允许额外的权限，例如打印？
  - answer: 是的。第一个参数是授予有限权限的用户（查看者）密码，第二个参数是提供对文档完整控制的所有者（管理员）密码。
    question: '`pdfDoc.Encrypt(viewerPass, adminPass, …)` 中密码的顺序重要吗？'
  - answer: Aspose.Pdf 在尝试打开已加密的文件时会抛出异常；您必须先使用其现有密码打开文件，移除或修改保护，然后再应用新的加密设置。
    question: 如果源 PDF 已经设置了密码保护，会发生什么情况？
  type: FAQPage
images:
- /net/security-permissions/encrypt-pdf-form-filling/og-image.png
og_title: 加密 PDF 并仅允许填写表单
og_description: 使用 AES‑256 保护您的 PDF，让用户只能填写表单，不能进行其他操作。
og_image_alt: 截图显示 Aspose.Pdf for .NET 代码，该代码对 PDF 进行加密并仅限制为填写表单
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Pdf for .NET 加密 PDF，仅允许填写表单
在本教程中，您将学习如何使用 Aspose.Pdf for .NET 打开现有 PDF，应用 AES‑256 加密，设置查看者密码和所有者密码，并限制文档权限，使接收者只能填写表单字段。该方法在需要保护内容的同时仍允许用户完成交互式表单时非常有用。代码逐步演示每个步骤，并将已加密的 PDF 保存以供分发。

---

{{< tutorial-widget sourcePath="pdf/net/security-permissions/encrypt-pdf-form-filling" >}}


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

**Q: 使用 `Permissions.FillForm` 加密后，用户可以对 PDF 做些什么？**  
A: 使用查看者（用户）密码打开时，文档可以被查看并且可以填写表单字段，但所有其他操作，如编辑文本、添加批注或提取内容，均被阻止。

**Q: 如何在仍然限制其他所有操作的同时，允许额外的权限，例如打印？**  
A: 使用按位或运算符组合权限，例如 `Permissions allowed = Permissions.FillForm | Permissions.Printing;`，并将组合后的值传递给 `pdfDoc.Encrypt`。

**Q: `pdfDoc.Encrypt(viewerPass, adminPass, …)` 中密码的顺序重要吗？**  
A: 是的。第一个参数是授予有限权限的用户（查看者）密码，第二个参数是提供对文档完整控制的所有者（管理员）密码。

**Q: 如果源 PDF 已经设置了密码保护，会发生什么情况？**  
A: Aspose.Pdf 在尝试打开已加密的文件时会抛出异常；您必须先使用其现有密码打开文件，移除或修改保护，然后再应用新的加密设置。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}