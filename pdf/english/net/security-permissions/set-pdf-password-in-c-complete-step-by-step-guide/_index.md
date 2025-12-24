---
category: general
date: 2025-12-23
description: Set PDF password quickly with C#. Learn to encrypt PDF with password,
  decrypt PDF with password, and even encrypt multiple PDFs using pdf encryption c#
  techniques.
draft: false
keywords:
- set pdf password
- encrypt pdf with password
- decrypt pdf with password
- encrypt multiple pdfs
- pdf encryption c#
language: en
og_description: Set PDF password instantly. This guide shows how to encrypt PDF with
  password, decrypt PDF with password, and batch‑encrypt multiple PDFs using pdf encryption
  c#.
og_title: Set PDF Password in C# – Full Programming Tutorial
tags:
- C#
- PDF
- Security
title: Set PDF Password in C# – Complete Step‑by‑Step Guide
url: /net/security-permissions/set-pdf-password-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Set PDF Password in C# – Complete Step‑by‑Step Guide

Ever wondered how to **set PDF password** from a C# application without pulling your hair out? You're not the only one. Whether you're protecting invoices, confidential reports, or simply keeping a personal diary safe, adding a password to a PDF is a must‑have skill for any .NET developer.

In this tutorial we’ll walk through the entire process: from encrypting a single PDF with password, to decrypting it later, and even handling a batch of files. We'll also sprinkle in a few “what if” scenarios so you know how to adapt the code when things get a little more complex. By the end you’ll have a solid, production‑ready snippet that you can drop into any C# project.

## Prerequisites

- **.NET 6+** (the code compiles on .NET Framework 4.7 as well, but .NET 6 is the sweet spot)
- A PDF processing library that exposes `Security`, `EncryptionOptions`, `DecryptionOptions`, and `FileDataSource`. In the examples we use a hypothetical library called **PdfSecureLib**; replace the namespaces with the ones from your actual vendor (i.e., iText7, PdfSharp, or Aspose.PDF).
- Basic familiarity with C# console applications.
- Two sample PDFs: `input.pdf` (the file you want to protect) and a folder where you’ll write the output.

> **Pro tip:** Keep your passwords in a secure vault (Azure Key Vault, AWS Secrets Manager, etc.) instead of hard‑coding them.

---

## 📸 Visual Overview  

![Diagram showing the flow of setting a PDF password using C#](https://example.com/set-pdf-password-diagram.png "set pdf password diagram")

*Image alt text: set pdf password diagram illustrating encryption and decryption steps.*

---

## How to Set PDF Password Using C#

The core of **setting a PDF password** lives in three simple steps: create a `Security` object, configure the encryption options, and run the process. Let’s break it down.

### Step 1: Add the Required Namespaces

```csharp
using PdfSecureLib;          // Replace with your actual library namespace
using System.IO;
```

> **Why?** Importing the right namespaces makes the `Security`, `EncryptionOptions`, and `FileDataSource` classes visible to the compiler.

### Step 2: Prepare the Encryption Options

```csharp
// Owner password grants full rights; user password limits what the recipient can do.
var encryptionOptions = new EncryptionOptions(
    ownerPassword: "123456789",          // Full‑access password
    userPassword: "123",                 // Password required to open the PDF
    privileges: DocumentPrivilege.ForbidAll); // Disallow printing, copying, etc.

// Tell the library which file to encrypt and where to write the result.
encryptionOptions.AddInput(new FileDataSource(@"C:\PDFs\input.pdf"));
encryptionOptions.AddOutput(new FileDataSource(@"C:\PDFs\encrypted.pdf"));
```

> **What’s happening?** We’re creating an `EncryptionOptions` instance that tells the library to *set PDF password* (`ownerPassword` and `userPassword`) and to block every privilege (`ForbidAll`). This is the most restrictive scenario—feel free to loosen it later.

### Step 3: Run the Encryption Process

```csharp
var encryptor = new Security();
encryptor.Process(encryptionOptions);
Console.WriteLine("✅ PDF encrypted successfully!");
```

> **Result:** `encrypted.pdf` now requires the user password “123” to open, and even if someone guesses it they still can’t print or copy content because we forbade all privileges.

---

## Decrypt PDF with Password – Getting Back the Original

Once a PDF is locked, you’ll often need to **decrypt PDF with password** for downstream processing (e.g., OCR, merging). The reversal is just as easy.

### Step 4: Set Up Decryption Options

```csharp
var decryptionOptions = new DecryptionOptions(ownerPassword: "123456789");

// Input is the encrypted file, output is the decrypted copy.
decryptionOptions.AddInput(new FileDataSource(@"C:\PDFs\encrypted.pdf"));
decryptionOptions.AddOutput(new FileDataSource(@"C:\PDFs\decrypted.pdf"));
```

### Step 5: Execute Decryption

```csharp
var decryptor = new Security();
decryptor.Process(decryptionOptions);
Console.WriteLine("🔓 PDF decrypted successfully!");
```

> **Tip:** If you only know the **user password**, pass it to the `DecryptionOptions` constructor instead of the owner password. Most libraries accept either.

---

## Encrypt Multiple PDFs – Scaling Up

In real projects you rarely work with a single file. Let’s extend the previous logic to **encrypt multiple PDFs** in one go. The key is to loop over a collection of file paths and reuse the same `EncryptionOptions` template.

```csharp
string[] pdfFiles = Directory.GetFiles(@"C:\PDFs\ToEncrypt", "*.pdf");
string outputFolder = @"C:\PDFs\EncryptedBatch";

foreach (var pdfPath in pdfFiles)
{
    var fileName = Path.GetFileNameWithoutExtension(pdfPath);
    var outputPath = Path.Combine(outputFolder, $"{fileName}_protected.pdf");

    var batchOptions = new EncryptionOptions(
        ownerPassword: "batchOwner!2025",
        userPassword: "batchUser#2025",
        privileges: DocumentPrivilege.ForbidAll);

    batchOptions.AddInput(new FileDataSource(pdfPath));
    batchOptions.AddOutput(new FileDataSource(outputPath));

    // Reuse the same Security instance for efficiency.
    encryptor.Process(batchOptions);
    Console.WriteLine($"🔐 Encrypted: {fileName}");
}
```

> **Why batch?** Looping reduces boilerplate and lets you apply the same **pdf encryption c#** policy across dozens of documents. Adjust the passwords per‑batch if you need per‑file uniqueness.

---

## Full Working Example

Below is a self‑contained console app that ties everything together. Paste it into a new **C#** project, restore the `PdfSecureLib` NuGet package (or your chosen library), and hit **F5**.

```csharp
// Program.cs
using PdfSecureLib;
using System;
using System.IO;

namespace PdfPasswordDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // ---------- SINGLE FILE ENCRYPTION ----------
            var encryptor = new Security();
            var encryptOpts = new EncryptionOptions(
                ownerPassword: "123456789",
                userPassword: "123",
                privileges: DocumentPrivilege.ForbidAll);

            encryptOpts.AddInput(new FileDataSource(@"C:\PDFs\input.pdf"));
            encryptOpts.AddOutput(new FileDataSource(@"C:\PDFs\encrypted.pdf"));
            encryptor.Process(encryptOpts);
            Console.WriteLine("✅ Single PDF encrypted.");

            // ---------- SINGLE FILE DECRYPTION ----------
            var decryptor = new Security();
            var decryptOpts = new DecryptionOptions(ownerPassword: "123456789");
            decryptOpts.AddInput(new FileDataSource(@"C:\PDFs\encrypted.pdf"));
            decryptOpts.AddOutput(new FileDataSource(@"C:\PDFs\decrypted.pdf"));
            decryptor.Process(decryptOpts);
            Console.WriteLine("🔓 Single PDF decrypted.");

            // ---------- BATCH ENCRYPTION ----------
            string[] files = Directory.GetFiles(@"C:\PDFs\BatchInput", "*.pdf");
            string outDir = @"C:\PDFs\BatchEncrypted";
            Directory.CreateDirectory(outDir);

            foreach (var file in files)
            {
                var name = Path.GetFileNameWithoutExtension(file);
                var outPath = Path.Combine(outDir, $"{name}_protected.pdf");

                var batchOpts = new EncryptionOptions(
                    ownerPassword: "batchOwner!2025",
                    userPassword: "batchUser#2025",
                    privileges: DocumentPrivilege.ForbidAll);

                batchOpts.AddInput(new FileDataSource(file));
                batchOpts.AddOutput(new FileDataSource(outPath));
                encryptor.Process(batchOpts);
                Console.WriteLine($"🔐 Batch encrypted: {name}");
            }

            Console.WriteLine("🎉 All operations completed.");
        }
    }
}
```

**Expected output in the console:**

```
✅ Single PDF encrypted.
🔓 Single PDF decrypted.
🔐 Batch encrypted: Report_Jan
🔐 Batch encrypted: Invoice_2024
🔐 Batch encrypted: Contract_ABC
🎉 All operations completed.
```

After running, you’ll find three sets of files:

1. `encrypted.pdf` – password‑protected.
2. `decrypted.pdf` – original content restored.
3. A folder of `*_protected.pdf` files – each one **encrypted multiple PDFs** in one sweep.

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| *What if I need to allow printing but still require a password?* | Change `DocumentPrivilege.ForbidAll` to `DocumentPrivilege.AllowPrinting`. Most libraries expose a flags enum so you can combine `AllowPrinting | AllowCopying` etc. |
| *Can I use a different password per file in the batch?* | Absolutely. Generate a random password inside the `foreach` loop and store it (e.g., in a CSV) for later reference. |
| *Is it safe to store passwords in plain text?* | No. Use `SecureString` or a secret manager. The example keeps them simple for clarity. |
| *What about large PDFs (>100 MB)?* | The `Security` class usually streams data, so memory usage stays low. Just ensure the underlying library supports streaming. |
| *How do I verify that the password was actually applied?* | Attempt to open the file with a PDF viewer without entering a password – it should refuse. Programmatically, call `PdfReader.IsEncrypted` after creation. |

---

## Best Practices for PDF Encryption in C#

1. **Never hard‑code secrets** – pull them from environment variables or a vault.
2. **Prefer owner passwords** for administrative tasks; user passwords are what end‑users see.
3. **Log actions, not passwords** – your logs should say “File X encrypted” but never echo the secret.
4. **Test with both correct and incorrect passwords** to ensure the library throws the expected exceptions.
5. **Keep libraries up‑to‑date** – security patches often fix vulnerabilities in PDF handling.

---

## Conclusion

We’ve covered everything you need to **set PDF password** in C#: encrypting a single document, decrypting it later, and scaling the process to **encrypt multiple PDFs**. The code snippets are ready‑to‑run, and the explanations answer the *how* and the *why* behind each line. 

Now you can protect invoices, hide confidential reports, or build a secure document‑delivery service without breaking a sweat. Next steps? Try integrating the routine into an ASP.NET Core API, explore digital signatures, or experiment with selective permission sets (e.g., allow printing but forbid copying). The sky’s the limit.

Got more questions?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}