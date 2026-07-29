---
category: general
date: 2026-06-21
description: 添加 Bates 编号 PDF，并学习如何添加 Bates 编号、将 PDF 转换为 PDF/X‑4、将 PDF 转换为 PDF/A‑4，以及在
  C# 中对 PDF 进行数字签名，一站式教程。
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbers
- digitally sign pdf c#
- convert pdf to pdf/x-4
- convert pdf to pdfa-4
language: zh
og_description: 为 PDF 添加贝茨编号，了解如何添加贝茨编号，将 PDF 转换为 PDF/X-4，将 PDF 转换为 PDF/A-4，并使用 Aspose.Pdf
  在 C# 中对 PDF 进行数字签名。
og_title: 为 PDF 添加贝茨编号 – 步骤详解 C# 教程
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add bates numbering pdf and learn how to add bates numbers, convert
    pdf to pdf/x-4, convert pdf to pdfa-4, and digitally sign pdf c# in a single walkthrough.
  headline: Add Bates Numbering PDF – Complete C# Guide with Signing & Conversion
  type: TechArticle
- questions:
  - answer: Yes. Use `BatesNumberingOptions` properties such as `Location` and `FontSize`
      to fine‑tune placement.
    question: Can I change the position of the Bates numbers?
  - answer: Switch `PdfFormat.PDF_X_4` to `PdfFormat.PDFA_4` in the conversion options.
      That satisfies the **convert pdf to pdfa-4** requirement.
    question: What if I need PDF/A‑4 instead of PDF/X‑4?
  - answer: Absolutely. Replace `DigestHashAlgorithm.Sha384` with `DigestHashAlgorithm.Sha256`
      (or any supported algorithm).
    question: My certificate uses a different hash algorithm—can I use SHA‑256?
  - answer: 'Not strictly. In this flow we save after conversion and after Bates numbering
      to give you intermediate files. You could defer saving until the end if you
      prefer a single write operation. ## Wrap‑Up We’ve just demonstrated a practical,
      end‑to‑end solution that **add bates numbering pdf**, explains **'
    question: Do I need to call `document.Save` after each step?
  type: FAQPage
tags:
- Aspose.Pdf
- C#
- PDF processing
- Bates numbering
title: 为 PDF 添加贝茨编号 – 完整的 C# 指南（含签名与转换）
url: /zh/net/programming-with-security-and-signatures/add-bates-numbering-pdf-complete-c-guide-with-signing-conver/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 添加 Bates 编号 PDF – 完整 C# 指南，包含签名与转换

是否曾经想过 **add bates numbering pdf** 却又不想抓狂？你并不是唯一的。法律团队、审计员以及所有需要可追溯文档的人经常会问 *如何向 PDF 添加 Bates 编号*，并且他们还需要文件符合 PDF/X‑4 或 PDF/A‑4 标准并进行数字签名。  

在本教程中，我们将完整演示——使用 Aspose.Pdf for .NET **add bates numbering pdf**，展示 **how to add bates numbers**，**convert pdf to pdf/x-4**，**convert pdf to pdfa-4**，以及最后 **digitally sign pdf c#**。完成后，你将拥有一个可直接运行的程序，生成三个精致的 PDF：PDF/X‑4 版本、带 Bates 编号的版本以及数字签名版本。

![添加 Bates 编号 PDF 示例](image-placeholder.png "Screenshot showing add bates numbering pdf in action")

## 你需要的环境

- **.NET 6+**（或 .NET Framework 4.6+）。Aspose.Pdf 两者皆支持。
- **有效的 Aspose.Pdf for .NET 许可证**（也可以使用评估版，但会出现水印）。
- 用于签名的 **PKCS#7 证书文件**（`.pfx`）及其密码。
- 你想要转换的 **示例 PDF**（放在自己可控的文件夹中）。
- Visual Studio、Rider 或任意你喜欢的 C# IDE。

就这些——除 `Aspose.Pdf` 外无需额外的 NuGet 包。如果还未添加库，请运行：

```bash
dotnet add package Aspose.Pdf
```

下面我们进入代码实现。

## 第一步：加载源 PDF 文档

首先，需要将原始文件加载到内存中。这是后续所有操作的基础。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

// Load the source PDF – adjust the path to your environment
var document = new Document("YOUR_DIRECTORY/sample.pdf");
```

> **为什么重要：** 加载 PDF 会创建一个表示整个文件的 `Document` 对象，让我们能够访问转换、表单字段以及安全相关的 API。

## 第二步：将 PDF 转换为 PDF/X‑4（符合 PDF/A‑4 标准）

如果你的工作流要求归档质量，PDF/X‑4（PDF/A‑4 的子集）是最佳选择。下面演示如何使用 Aspose **convert pdf to pdf/x-4**。

```csharp
// Set conversion options – PDF/X‑4 is the target format
var conversionOptions = new PdfFormatConversionOptions(PdfFormat.PDF_X_4, ConvertErrorAction.Delete);

// Perform the conversion
document.Convert(conversionOptions);
```

> **小技巧：** `ConvertErrorAction.Delete` 标志会删除所有可能导致不合规的内容，确保输出的 PDF/X‑4 干净合规。

## 第三步：保存 PDF/X‑4 版本

文档已符合 PDF/X‑4 标准后，将其写入磁盘。

```csharp
document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");
```

现在你拥有一个 **convert pdf to pdfa-4** 兼容的文件（PDF/X‑4 属于 PDF/A‑4 系列）。可在 Acrobat 中打开以验证合规徽章。

## 第四步：添加 Bates 编号 – “Add Bates Numbering PDF”的核心

Bates 编号是放置在每页上的顺序标识符。这正是 *how to add bates numbers* 的程序化答案。

```csharp
// Configure Bates numbering options
var batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",   // Optional prefix
    Start = 5000        // Starting number
};

// Apply Bates numbering to the document
document.AddBatesNumbering(batesOptions);
```

> **工作原理：** `AddBatesNumbering` 会遍历每一页并在默认位置（右下角）盖章。若需要，可通过 `BatesNumberingOptions` 调整位置。

## 第五步：保存带 Bates 编号的 PDF

在 **add bates numbering pdf** 完成后，需要生成一个保留编号的独立文件。

```csharp
document.Save("YOUR_DIRECTORY/sample_bates.pdf");
```

打开文件，你应当能在每页底部看到 “CASE‑5000”、 “CASE‑5001” 等编号。

## 第六步：数字签名 PDF – “Digitally Sign PDF C#” 实战

数字签名保证了真实性和完整性。下面我们将使用 SHA‑384 哈希 **digitally sign pdf c#**。

```csharp
// Prepare the signature handler
var signature = new PdfFileSignature(document);

// Load the PKCS#7 certificate (adjust password)
var pkcs7 = new PKCS7Detached(
    "YOUR_DIRECTORY/mycert.pfx", // Path to .pfx
    "pwd",                       // Certificate password
    DigestHashAlgorithm.Sha384   // Strong hashing algorithm
);

// Sign page 1, place signature rectangle at (100,100)-(200,150)
signature.Sign(
    pageNumber: 1,
    signatureAppearance: true,
    rectangle: new Rectangle(100, 100, 200, 150),
    pkcs7: pkcs7
);
```

> **专业提示：** `Rectangle` 定义了可见签名出现的位置。如果不需要可视化提示，可将 `signatureAppearance` 设置为 `false`。

## 第七步：保存数字签名后的 PDF

最后，将签名后的文档写入磁盘。

```csharp
signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
```

现在你拥有一个 **digitally sign pdf c#** 文件，可在任何支持数字签名的 PDF 阅读器中验证。

## 完整源码 – 一站式解决方案

下面是完整的、可直接运行的程序。复制粘贴，调整路径后按 **F5** 即可。

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source PDF document
        // -------------------------------------------------
        var document = new Document("YOUR_DIRECTORY/sample.pdf");

        // -------------------------------------------------
        // Step 2: Convert the document to PDF/X‑4 format
        // (PDF/A‑4 compliance)
        // -------------------------------------------------
        var conversionOptions = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_4,
            ConvertErrorAction.Delete);
        document.Convert(conversionOptions);

        // -------------------------------------------------
        // Step 3: Save the PDF/X‑4 version
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");

        // -------------------------------------------------
        // Step 4: Add Bates numbering – how to add bates numbers
        // -------------------------------------------------
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 5000
        };
        document.AddBatesNumbering(batesOptions);

        // -------------------------------------------------
        // Step 5: Save the Bates‑numbered PDF
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_bates.pdf");

        // -------------------------------------------------
        // Step 6: Sign the document using SHA‑384 hashing
        // -------------------------------------------------
        var signature = new PdfFileSignature(document);
        var pkcs7 = new PKCS7Detached(
            "YOUR_DIRECTORY/mycert.pfx",
            "pwd",
            DigestHashAlgorithm.Sha384);
        signature.Sign(
            pageNumber: 1,
            signatureAppearance: true,
            rectangle: new Rectangle(100, 100, 200, 150),
            pkcs7: pkcs7);

        // -------------------------------------------------
        // Step 7: Save the digitally signed PDF
        // -------------------------------------------------
        signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
    }
}
```

### 预期输出

| 文件 | 用途 | 关键特性 |
|------|---------|-------------|
| `sample_pdfx4.pdf` | PDF/X‑4 版本 | 符合 PDF/A‑4 合规性 |
| `sample_bates.pdf` | 带 Bates 编号的 PDF | 已应用 **add bates numbering pdf** |
| `sample_signed.pdf` | 数字签名 PDF | 已使用 SHA‑384 的 **digitally sign pdf c#** |

在 Adobe Acrobat Reader 中打开任意一个文件；第二个文件会显示 Bates 编号，第三个文件会出现签名字段。

## 常见问题 (FAQ)

**Q: 能否更改 Bates 编号的位置？**  
A: 可以。使用 `BatesNumberingOptions` 的 `Location`、`FontSize` 等属性即可微调。

**Q: 如果需要 PDF/A‑4 而不是 PDF/X‑4，怎么办？**  
A: 将转换选项中的 `PdfFormat.PDF_X_4` 替换为 `PdfFormat.PDFA_4`。这样即可满足 **convert pdf to pdfa-4** 的需求。

**Q: 我的证书使用不同的哈希算法——可以改用 SHA‑256 吗？**  
A: 完全可以。将 `DigestHashAlgorithm.Sha384` 替换为 `DigestHashAlgorithm.Sha256`（或其他受支持的算法）。

**Q: 每一步都必须调用 `document.Save` 吗？**  
A: 并非必须。在本流程中我们在转换后和添加 Bates 编号后各保存一次，以便得到中间文件。如果你更倾向于一次性写入，也可以等到最后再保存。

## 小结

我们已经演示了一个实用的端到端方案，**add bates numbering pdf**，解释了 **how to add bates numbers**，展示了 **convert pdf to pdf/x-4**，并涵盖了

## 接下来你可以学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并在项目中探索替代实现方式。每篇资源均提供完整可运行的代码示例和逐步解释。

- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/german/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/french/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/japanese/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}