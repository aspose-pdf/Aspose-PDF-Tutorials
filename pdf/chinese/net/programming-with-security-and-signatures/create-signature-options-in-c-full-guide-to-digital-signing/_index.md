---
category: general
date: 2026-08-14
description: 在 C# 中创建签名选项以应用数字签名。了解如何配置签名、实现自定义哈希函数以及以编程方式签署文档。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create signature options
- custom hash function
- apply digital signature
- how to sign document
- how to configure signature
language: zh
lastmod: 2026-08-14
og_description: 在 C# 中创建签名选项并应用数字签名。本教程将指导您配置签名、添加自定义哈希函数以及对文档进行签名。
og_image_alt: Code editor view showing C# creation of signature options and document
  signing
og_title: 在 C# 中创建签名选项 – 步骤式数字签名指南
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: Create signature options in C# to apply digital signature. Learn how
    to configure signature, implement a custom hash function, and sign documents programmatically.
  headline: Create signature options in C# – full guide to digital signing
  type: TechArticle
- description: Create signature options in C# to apply digital signature. Learn how
    to configure signature, implement a custom hash function, and sign documents programmatically.
  name: Create signature options in C# – full guide to digital signing
  steps:
  - name: '**Hash calculation** – now delegated to your custom hash function.'
    text: '**Hash calculation** – now delegated to your custom hash function.'
  - name: '**Signature generation** – using the private key supplied to the library’s
      configuration.'
    text: '**Signature generation** – using the private key supplied to the library’s
      configuration.'
  - name: '**Embedding** – the generated signature is attached to the output file.'
    text: '**Embedding** – the generated signature is attached to the output file.'
  type: HowTo
tags:
- digital signature
- C#
- security
title: 在 C# 中创建签名选项 – 数字签名完整指南
url: /zh/net/programming-with-security-and-signatures/create-signature-options-in-c-full-guide-to-digital-signing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中创建签名选项 – 数字签名完整指南

在 C# 中创建签名选项以配置数字签名工作流。本教程展示如何应用数字签名、实现自定义哈希函数以及使用 `SignatureOptions` 类对文档进行签名。如果您曾需要在 .NET 应用程序中对 PDF、XML 或任何二进制负载进行签名，下面的步骤将为您提供一个可直接运行的解决方案。

您将学习如何：

* 使用自定义哈希算法配置 `SignatureOptions`，
* 正确调用签名方法，
* 验证签名是否已应用，
* 避免在配置签名时常见的陷阱。

唯一的前置条件是最近的 .NET SDK（≥ .NET 6）以及提供 `SignatureOptions` 的签名库（例如 **GroupDocs.Signature**、**Aspose.Signature** 或类似的 API）。无需任何外部工具。

---

## Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6 SDK 或更高版本 | 提供示例中使用的现代语言特性。 |
| 一个签名库的 NuGet 包（例如 `GroupDocs.Signature`） | 提供 `SignatureOptions` 类型和 `Sign` 扩展方法。 |
| 私钥或证书的访问权限 | 生成可验证的数字签名所必需。 |

使用标准 CLI 安装库：

```bash
dotnet add package GroupDocs.Signature
```

---

## Step 1: Create signature options

## 步骤 1：创建签名选项

第一步是实例化 `SignatureOptions` 并设置控制签名过程的属性。该对象告诉库 *要签署什么* 以及 *如何签署*。

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Options;

// Create a new SignatureOptions instance
var signatureOptions = new SignatureOptions
{
    // The signing algorithm (e.g., RSA‑SHA256) is defined by the library.
    // You can also set visual appearance, page number, etc., here.
    // For this tutorial we focus on the custom hash function.
};
```

**Why this matters:** `SignatureOptions` 充当您的代码与签名引擎之间的契约。提前配置它可以避免在签署多个文档时重复编写样板代码。

---

## Step 2: Implement a custom hash function

## 步骤 2：实现自定义哈希函数

*自定义哈希函数* 让您完全控制签名算法所签署的摘要。当默认哈希（SHA‑256）不符合合规要求，或需要对文档的子集进行哈希时，这非常有用。

```csharp
using System.Security.Cryptography;
using System.Text;

// Define a delegate that matches the library’s expected signature
Func<byte[], byte[]> MyHash = data =>
{
    // Example: compute SHA‑512 and then truncate to 256 bits
    using var sha512 = SHA512.Create();
    var fullHash = sha512.ComputeHash(data);

    // Truncate to the first 32 bytes (256 bits)
    var truncated = new byte[32];
    Buffer.BlockCopy(fullHash, 0, truncated, 0, truncated.Length);
    return truncated;
};

// Attach the custom hash to the options
signatureOptions.CustomSignHash = hash => MyHash(hash);
```

**Why this matters:** 通过为 `CustomSignHash` 赋值，您用 `MyHash` 替代库内部的哈希步骤。签名引擎现在会签署您函数返回的字节，从而确保符合任何自定义策略。

---

## Step 3: Load the document and apply digital signature

## 步骤 3：加载文档并应用数字签名

准备好选项后，您可以打开目标文件并调用签名方法。`Sign` 方法由库提供，并使用已配置的 `SignatureOptions`。

```csharp
using System.IO;

// Path to the file you want to sign
string inputPath = @"C:\Docs\contract.pdf";
string outputPath = @"C:\Docs\contract.signed.pdf";

// Load the document into the Signature object
using var signature = new Signature(inputPath);

// Sign the document using the previously created options
bool result = signature.Sign(outputPath, signatureOptions);

if (!result)
{
    throw new InvalidOperationException("The document could not be signed.");
}
```

**Why this matters:** 调用 `Sign` 在内部执行三项操作：

1. **Hash calculation** – 现在委托给您的自定义哈希函数。  
2. **Signature generation** – 使用库配置中提供的私钥。  
3. **Embedding** – 将生成的签名附加到输出文件。

如果任何步骤失败，方法会返回 `false`，以便您优雅地处理错误。

---

## Step 4: Verify that the document is signed

## 步骤 4：验证文档是否已签名

快速验证可以确认签名已正确应用。大多数库都提供 `Verify` 方法来检查已签文件的完整性。

```csharp
using var verifier = new Signature(outputPath);
var verificationResult = verifier.Verify();

Console.WriteLine(verificationResult
    ? "Signature verified successfully."
    : "Signature verification failed.");
```

**Why this matters:** 验证可确保签名文档在签署后未被篡改，并且自定义哈希产生了兼容的摘要。

---

## How to configure signature for different file types

## 如何为不同文件类型配置签名

相同的 `SignatureOptions` 对象可重复用于 PDF、Word 文档、图像或普通二进制文件。唯一需要更改的是具体的选项类（例如 `PdfSignatureOptions`、`WordSignatureOptions`）。下面是针对 JPEG 图像的快速示例：

```csharp
using GroupDocs.Signature.Options;

var imageOptions = new ImageSignatureOptions
{
    // Position the signature on the image
    Left = 100,
    Top = 50,
    Width = 150,
    Height = 50,
    CustomSignHash = hash => MyHash(hash)   // reuse the same custom hash
};

using var imgSignature = new Signature(@"C:\Images\photo.jpg");
imgSignature.Sign(@"C:\Images\photo.signed.jpg", imageOptions);
```

**Why this matters:** 了解如何为每种格式 *configure signature* 能让您在多个文档类型之间复用同一代码库，而无需重新编写哈希逻辑。

---

## Common pitfalls and best practices

## 常见陷阱与最佳实践

| Pitfall | Recommended fix |
|---------|-----------------|
| 在创建 `SignatureOptions` 后忘记设置 `CustomSignHash` | 在构造选项对象后立即分配该委托。 |
| 使用签名证书不支持的哈希算法 | 确认证书的密钥用法与哈希长度匹配（例如 RSA‑2048 与 SHA‑512）。 |
| 忽视释放 `Signature` 对象的必要性 | 将 `Signature` 实例放入 `using` 块中以释放文件句柄。 |
| 将已签名文件覆盖原始源文件 | 始终写入新文件路径（`outputPath`），以保留原始文档。 |

---

## Full working example

## 完整工作示例

下面是一个自包含的程序，演示了所有步骤的组合。将其复制到新的控制台项目中运行；控制台会报告成功或失败。

```csharp
using System;
using System.IO;
using System.Security.Cryptography;
using GroupDocs.Signature;
using GroupDocs.Signature.Options;

class Program
{
    // Custom hash implementation (SHA‑512 truncated to 256 bits)
    private static byte[] MyHash(byte[] data)
    {
        using var sha512 = SHA512.Create();
        var full = sha512.ComputeHash(data);
        var truncated = new byte[32];
        Buffer.BlockCopy(full, 0, truncated, 0, truncated.Length);
        return truncated;
    }

    static void Main()
    {
        // Paths
        string input = @"C:\Docs\contract.pdf";
        string output = @"C:\Docs\contract.signed.pdf";

        // Step 1: create signature options
        var signatureOptions = new SignatureOptions
        {
            CustomSignHash = hash => MyHash(hash)
        };

        // Step 2: sign the document
        using var signer = new Signature(input);
        bool signed = signer.Sign(output, signatureOptions);
        if (!signed)
        {
            Console.WriteLine("Signing failed.");
            return;
        }

        // Step 3: verify the signature
        using var verifier = new Signature(output);
        bool verified = verifier.Verify();
        Console.WriteLine(verified
            ? "Signature verified successfully."
            : "Signature verification failed.");
    }
}
```

**Expected output**

**预期输出**

```
Signature verified successfully.
```

如果控制台打印出 “Signing failed.” 或 “Signature verification failed.”，请再次检查证书配置，并确保自定义哈希返回的字节数组大小符合预期。

---

## Conclusion

## 结论

现在您已经了解如何在 C# 中 **create signature options**，附加 **custom hash function**，并对任何受支持的文档 **apply digital signature**。本教程覆盖了完整的生命周期：配置选项、签署文件以及验证结果。通过复用同一 `SignatureOptions` 实例，您还可以 **how to configure signature** 用于图像、Word 文件或原始二进制文件。

---

## What’s next?

## 接下来怎么做？

* 探索更多 `SignatureOptions` 属性，如可视化印章、时间戳服务器和证书链——这些与 **apply digital signature** 关键字相呼应。  
* 通过在 `MyHash` 中替换实现，尝试其他哈希算法（例如 Blake2b）。  
* 将签名流程集成到 Web API 中，以实现即时文档签名——这是 **how to sign document** 在面向服务的架构中的自然扩展。

欢迎根据自己的安全策略调整代码，并在评论中分享您的经验。祝签名愉快！

## What Should You Learn Next?

## 接下来应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您在自己的项目中进一步掌握 API 功能并探索替代实现方式。每个资源都包含完整的可运行代码示例和逐步解释。

- [如何使用 Aspose.PDF for .NET 更改 PDF 签名语言](/pdf/english/net/digital-signatures/change-pdf-signature-language-aspose-net/)
- [Aspose Pdf .NET 数字签名教程（德语）](/pdf/german/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)
- [Aspose Pdf .NET 数字签名教程（法语）](/pdf/french/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}