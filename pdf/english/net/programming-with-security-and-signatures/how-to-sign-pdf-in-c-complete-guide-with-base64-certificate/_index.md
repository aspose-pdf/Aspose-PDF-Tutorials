---
category: general
date: 2025-12-25
description: How to sign PDF using a Base64‑encoded certificate in C#. Learn to sign
  PDF with certificate, apply digital signature PDF, and master digital signature
  PDF C#.
draft: false
keywords:
- how to sign pdf
- sign pdf with certificate
- digital signature pdf c#
- apply digital signature pdf
language: en
og_description: How to sign PDF using a Base64‑encoded certificate in C#. This tutorial
  shows you how to sign PDF with certificate, apply digital signature PDF, and handle
  edge cases.
og_title: How to Sign PDF in C# – Step‑by‑Step Guide
tags:
- PDF
- C#
- Aspose.PDF
title: How to Sign PDF in C# – Complete Guide with Base64 Certificate
url: /net/programming-with-security-and-signatures/how-to-sign-pdf-in-c-complete-guide-with-base64-certificate/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Sign PDF in C# – Complete Guide with Base64 Certificate

Ever wondered **how to sign PDF** files from a .NET application without a physical certificate file on disk? Maybe you received a certificate as a Base64 string from a secure vault and need to embed it into a PDF. In this tutorial we’ll walk through a full, runnable example that shows you **how to sign PDF** using a Base64‑encoded certificate, explains why each step matters, and covers common pitfalls you might hit along the way.

By the end of this guide you’ll be able to:

* Sign PDF with certificate stored in memory.
* Apply digital signature PDF to a specific page and rectangle.
* Understand the interplay between Aspose.Pdf, X509 certificates, and RSA signing.
* Extend the solution for other hash algorithms or multi‑page signatures.

> **Prerequisites** – You’ll need the Aspose.PDF for .NET library (version 23.9 or later), .NET 6+ (or .NET Framework 4.7.2), and a Base64‑encoded PFX certificate. No external services are required.

---

## What You’ll Need

| Item | Reason |
|------|--------|
| **Aspose.Pdf** NuGet package | Provides `PdfFileSignature` and `ExternalSignature` classes. |
| **X509Certificate2** from `System.Security.Cryptography.X509Certificates` | Loads the PFX from a Base64 string. |
| **RSACryptoServiceProvider** | Performs the actual RSA hash signing. |
| **System.Drawing** (or `System.Drawing.Common` for .NET Core) | Supplies the `Rectangle` struct for signature placement. |
| **A PDF file** (`input.pdf`) | The document we’ll be signing. |
| **Base64‑encoded PFX** (`base64Certificate`) | The private key we’ll use for signing. |

If any of these sound unfamiliar, don’t worry – we’ll explain each piece as we go.

---

## Step 1: Load the Base64 Certificate into an X509Certificate2

The first thing you have to do is turn the Base64 string into a usable `X509Certificate2` object. This is the foundation for any **sign pdf with certificate** operation.

```csharp
using System;
using System.Security.Cryptography;
using System.Security.Cryptography.X509Certificates;

// ...

// Replace these placeholders with your actual values
string base64Certificate = "MIIG...";   // Your Base64‑encoded PFX
string certificatePassword = "yourPassword";

// Convert Base64 to a byte array
byte[] certBytes = Convert.FromBase64String(base64Certificate);

// Load the certificate (Exportable flag is required for later RSA extraction)
X509Certificate2 cert = new X509Certificate2(
    certBytes,
    certificatePassword,
    X509KeyStorageFlags.Exportable);
```

**Why Exportable?** The `Exportable` flag lets us extract the private key into an `RSACryptoServiceProvider`. Without it, the RSA instance would be inaccessible, and the later `CustomSignHash` delegate would throw.

---

## Step 2: Create a Custom Hash‑Signing Delegate

Aspose.Pdf’s `ExternalSignature` class lets you plug in any signing logic you like. Here we’ll feed it a lambda that receives the raw hash bytes and returns a signed blob. This is the heart of **digital signature pdf c#**.

```csharp
using Aspose.Pdf.Forms;
using System.Drawing;

// ...

var externalSignature = new ExternalSignature(base64Certificate, false);

// CustomSignHash receives the pre‑computed hash and the algorithm name (e.g., "SHA1")
externalSignature.CustomSignHash = (hash, algorithm) =>
{
    // Use the previously loaded X509Certificate2
    using (RSA rsa = cert.GetRSAPrivateKey())
    {
        // Map the algorithm name to its OID; SHA1 is used for compatibility with many PDF readers
        string oid = CryptoConfig.MapNameToOID(algorithm ?? "SHA1");
        // Sign the hash using PKCS#1 v1.5 padding (the default for PDF signatures)
        return rsa.SignHash(hash, HashAlgorithmName.SHA1, RSASignaturePadding.Pkcs1);
    }
};
```

**Note on Algorithms:** While SHA‑256 is more secure, many older PDF viewers only understand SHA‑1 signatures. You can swap `"SHA1"` for `"SHA256"` if your target audience uses modern readers.

---

## Step 3: Bind the PDF Document to the Signature Engine

Now we tell Aspose which PDF we want to sign. The `PdfFileSignature` class works directly with file streams, making it ideal for batch processing.

```csharp
using Aspose.Pdf.Facades;

// ...

string dataFolder = @"C:\MyPdfFolder\";   // Adjust to your environment
string inputPdfPath = System.IO.Path.Combine(dataFolder, "input.pdf");

// Initialise the signature handler
using (var pdfSigner = new PdfFileSignature())
{
    // Load the PDF we’re about to sign
    pdfSigner.BindPdf(inputPdfPath);
```

---

## Step 4: Apply the Signature to a Specific Page and Rectangle

You can place the visual signature anywhere you like. Here we’ll put it on page 1, near the bottom‑right corner.

```csharp
    // Define where the signature appearance will be rendered
    var signatureRect = new Rectangle(200, 200, 200, 100);

    // Sign the document
    pdfSigner.Sign(
        pageNumber: 1,
        signatureName: "Second Approval",
        location: "second_user@example.com",
        reason: "Australia",
        contactInfo: false,
        rectangle: signatureRect,
        signature: externalSignature);
```

**Why a Rectangle?** PDF signatures are anchored to a rectangular region. The coordinates are in points (1 inch = 72 points). Adjust `X`, `Y`, `Width`, and `Height` to match your layout.

---

## Step 5: Save the Signed PDF

Finally, write the signed output back to disk. The same `PdfFileSignature` instance can be reused for additional signatures if you need to sign multiple pages.

```csharp
    string outputPdfPath = System.IO.Path.Combine(dataFolder, "SignWithBase64Certificate_out.pdf");
    pdfSigner.Save(outputPdfPath);
}

// Inform the user
Console.WriteLine($"✅ PDF signed successfully! Output saved to: {outputPdfPath}");
```

---

## Full Working Example

Putting it all together, here’s the complete, copy‑and‑paste‑ready program:

```csharp
using System;
using System.Drawing;
using System.Security.Cryptography;
using System.Security.Cryptography.X509Certificates;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load Base64‑encoded certificate
        // -------------------------------------------------
        string base64Certificate = "MIIG...";               // <-- your Base64 string
        string certPassword = "yourPassword";
        byte[] certBytes = Convert.FromBase64String(base64Certificate);
        X509Certificate2 cert = new X509Certificate2(
            certBytes,
            certPassword,
            X509KeyStorageFlags.Exportable);

        // -------------------------------------------------
        // 2️⃣ Prepare ExternalSignature with custom hash signer
        // -------------------------------------------------
        var externalSignature = new ExternalSignature(base64Certificate, false);
        externalSignature.CustomSignHash = (hash, algorithm) =>
        {
            using (RSA rsa = cert.GetRSAPrivateKey())
            {
                // Default to SHA1 for broad compatibility
                string oid = CryptoConfig.MapNameToOID(algorithm ?? "SHA1");
                return rsa.SignHash(hash, HashAlgorithmName.SHA1, RSASignaturePadding.Pkcs1);
            }
        };

        // -------------------------------------------------
        // 3️⃣ Bind PDF and apply signature
        // -------------------------------------------------
        string dataFolder = @"C:\MyPdfFolder\";
        string inputPdf = System.IO.Path.Combine(dataFolder, "input.pdf");
        string outputPdf = System.IO.Path.Combine(dataFolder, "SignWithBase64Certificate_out.pdf");

        using (var pdfSigner = new PdfFileSignature())
        {
            pdfSigner.BindPdf(inputPdf);

            var rect = new Rectangle(200, 200, 200, 100); // X, Y, Width, Height

            pdfSigner.Sign(
                pageNumber: 1,
                signatureName: "Second Approval",
                location: "second_user@example.com",
                reason: "Australia",
                contactInfo: false,
                rectangle: rect,
                signature: externalSignature);

            pdfSigner.Save(outputPdf);
        }

        Console.WriteLine($"✅ PDF signed! Check: {outputPdf}");
    }
}
```

**Expected Result:** Open `SignWithBase64Certificate_out.pdf` in Adobe Acrobat Reader. You’ll see a signature field on page 1 with the name “Second Approval.” The signature status should read *Signed and all signatures are valid* (provided the certificate chain is trusted).

---

## Common Questions & Edge Cases

### 1️⃣ What if the PDF already contains a signature field?

Aspose.Pdf will add a *new* invisible signature on top of any existing fields. If you need to reuse an existing visible field, call the overload that accepts the field name instead of a rectangle.

### 2️⃣ Can I sign with a certificate stored in Azure Key Vault?

Absolutely. Pull the secret as a Base64 string, then follow **Step 1**. The rest of the flow stays unchanged because the signing logic lives in your own delegate.

### 3️⃣ How do I switch to SHA‑256?

Just change the `algorithm` argument inside `CustomSignHash`:

```csharp
return rsa.SignHash(hash, HashAlgorithmName.SHA256, RSASignaturePadding.Pkcs1);
```

Remember to update the `reason` or `location` strings if your policy requires it.

### 4️⃣ What if the certificate is password‑less?

Pass an empty string (`""`) to the `X509Certificate2` constructor. The `Exportable` flag is still required.

### 5️⃣ Multi‑page signing?

Wrap the `pdfSigner.Sign` call in a loop, adjusting `pageNumber` and `rectangle` for each page. Aspose.Pdf handles multiple signatures without issue.

---

## Pro Tips & Gotchas

* **Pro tip:** Always verify the signed PDF with a third‑party tool (Acrobat, PDF‑XChange) before shipping it to clients. This catches chain‑validation problems early.
* **Watch out for:** Using `RSACryptoServiceProvider` on .NET Core can throw a `PlatformNotSupportedException` on Linux. Prefer `RSA.Create()` (as shown) for cross‑platform compatibility.
* **Performance note:** Loading the certificate once and reusing the `RSA` instance is faster than creating a new one per signature.
* **Security reminder:** Never hard‑code the certificate password in source control. Use environment variables or a secret manager.

---

## Conclusion

We’ve taken you from the question **how to sign PDF** in C# to a fully functional, production‑ready example that **sign pdf with certificate**, **apply digital signature pdf**, and handle the nuances of **digital signature pdf c#**. The key takeaways are:

* Load the Base64 certificate into an `X509Certificate2` with exportable private key.
* Plug a custom hash‑signing delegate into Aspose

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}