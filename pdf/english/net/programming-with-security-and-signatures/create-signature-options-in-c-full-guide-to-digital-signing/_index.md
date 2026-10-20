---
category: general
date: 2026-08-14
description: Create signature options in C# to apply digital signature. Learn how
  to configure signature, implement a custom hash function, and sign documents programmatically.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create signature options
- custom hash function
- apply digital signature
- how to sign document
- how to configure signature
language: en
lastmod: 2026-08-14
og_description: Create signature options in C# and apply a digital signature. This
  tutorial walks you through configuring the signature, adding a custom hash function,
  and signing a document.
og_image_alt: Code editor view showing C# creation of signature options and document
  signing
og_title: Create signature options in C# – step‑by‑step digital signing guide
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
title: Create signature options in C# – full guide to digital signing
url: /net/programming-with-security-and-signatures/create-signature-options-in-c-full-guide-to-digital-signing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create signature options in C# – full guide to digital signing

Create signature options in C# to configure a digital‑signature workflow. This tutorial shows how to apply digital signature, implement a custom hash function, and sign a document using the `SignatureOptions` class. If you have ever needed to sign a PDF, XML, or any binary payload from a .NET application, the steps below give you a ready‑to‑run solution.

You will learn how to:

* configure `SignatureOptions` with a custom hash algorithm,
* call the signing method correctly,
* verify that the signature was applied,
* avoid common pitfalls when configuring the signature.

The only prerequisites are a recent .NET SDK (≥ .NET 6) and a signing library that exposes `SignatureOptions` (for example, **GroupDocs.Signature**, **Aspose.Signature**, or a similar API). No external tools are required.

---

## Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6 SDK or later | Provides the modern language features used in the examples. |
| A signing‑library NuGet package (e.g., `GroupDocs.Signature`) | Supplies the `SignatureOptions` type and the `Sign` extension method. |
| Access to a private key or certificate | Required to generate a verifiable digital signature. |

Install the library with the standard CLI:

```bash
dotnet add package GroupDocs.Signature
```

---

## Step 1: Create signature options

The first step is to instantiate `SignatureOptions` and set the properties that control the signing process. This object tells the library *what* to sign and *how* to sign it.

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

**Why this matters:** `SignatureOptions` acts as a contract between your code and the signing engine. By configuring it up front you avoid repeated boilerplate when signing multiple documents.

---

## Step 2: Implement a custom hash function

A *custom hash function* gives you full control over the digest that the signature algorithm signs. This is useful when the default hash (SHA‑256) does not meet compliance requirements or when you need to hash a subset of the document.

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

**Why this matters:** By assigning `CustomSignHash`, you replace the library’s internal hashing step with `MyHash`. The signing engine will now sign the bytes returned by your function, ensuring compliance with any custom policy.

---

## Step 3: Load the document and apply digital signature

With the options prepared, you can now open the target file and call the signing method. The method `Sign` is provided by the library and uses the configured `SignatureOptions`.

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

**Why this matters:** The call to `Sign` performs three actions internally:

1. **Hash calculation** – now delegated to your custom hash function.
2. **Signature generation** – using the private key supplied to the library’s configuration.
3. **Embedding** – the generated signature is attached to the output file.

If any step fails, the method returns `false`, allowing you to handle the error gracefully.

---

## Step 4: Verify that the document is signed

A quick verification confirms that the signature was correctly applied. Most libraries expose a `Verify` method that checks the integrity of the signed file.

```csharp
using var verifier = new Signature(outputPath);
var verificationResult = verifier.Verify();

Console.WriteLine(verificationResult
    ? "Signature verified successfully."
    : "Signature verification failed.");
```

**Why this matters:** Verification ensures that the signed document has not been tampered with after signing and that the custom hash produced a compatible digest.

---

## How to configure signature for different file types

The same `SignatureOptions` object can be reused for PDFs, Word documents, images, or plain binaries. The only change required is the specific options class (e.g., `PdfSignatureOptions`, `WordSignatureOptions`). Here’s a quick example for a JPEG image:

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

**Why this matters:** Understanding how to *configure signature* for each format lets you extend the same codebase across multiple document types without rewriting the hashing logic.

---

## Common pitfalls and best practices

| Pitfall | Recommended fix |
|---------|-----------------|
| Forgetting to set `CustomSignHash` after creating `SignatureOptions` | Assign the delegate immediately after constructing the options object. |
| Using a hash algorithm that the signing certificate does not support | Verify that the certificate’s key usage matches the hash length (e.g., RSA‑2048 with SHA‑512). |
| Overlooking the need to dispose `Signature` objects | Wrap the `Signature` instance in a `using` block to release file handles. |
| Saving the signed file over the original source | Always write to a new file path (`outputPath`) to preserve the original document. |

---

## Full working example

Below is a self‑contained program that puts all the pieces together. Copy it into a new console project and run it; the console will report success or failure.

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

```
Signature verified successfully.
```

If the console prints “Signing failed.” or “Signature verification failed.”, double‑check the certificate configuration and ensure the custom hash returns a byte array of the expected size.

---

## Conclusion

You now know how to **create signature options** in C#, attach a **custom hash function**, and **apply digital signature** to any supported document. The tutorial covered the full lifecycle: configuring the options, signing the file, and verifying the result. By reusing the same `SignatureOptions` instance you can also **how to configure signature** for images, Word files, or raw binaries.

---

## What’s next?

* Explore additional `SignatureOptions` properties such as visual stamps, timestamp servers, and certificate chains – these align with the **apply digital signature** keyword.
* Experiment with other hash algorithms (e.g., Blake2b) by swapping the implementation inside `MyHash`.
* Integrate the signing flow into a web API to enable on‑the‑fly document signing – a natural extension of **how to sign document** in a service‑oriented architecture.

Feel free to adapt the code for your own security policies, and share your experience in the comments. Happy signing!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Change PDF Signature Language with Aspose.PDF for .NET](/pdf/english/net/digital-signatures/change-pdf-signature-language-aspose-net/)
- [Digital Signature Aspose Pdf Net Tutorial](/pdf/german/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)
- [Digital Signature Aspose Pdf Net Tutorial](/pdf/french/net/digital-signatures/digital-signature-aspose-pdf-net-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}