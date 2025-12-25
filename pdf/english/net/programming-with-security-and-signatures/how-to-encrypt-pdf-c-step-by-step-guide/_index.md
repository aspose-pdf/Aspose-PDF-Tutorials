---
category: general
date: 2025-12-25
description: How to encrypt PDF using C# in minutes. Learn to set owner password PDF,
  remove PDF encryption and decrypt PDF owner password with clear code examples.
draft: false
keywords:
- how to encrypt pdf
- remove pdf encryption
- how to decrypt pdf
- decrypt pdf owner password
- set owner password pdf
language: en
og_description: How to encrypt PDF quickly with C#. This guide shows how to set owner
  password PDF, remove PDF encryption and decrypt PDF owner password in a single tutorial.
og_title: How to Encrypt PDF – C# Step‑by‑Step Guide
tags:
- PDF
- C#
- Security
title: How to Encrypt PDF – C# Step‑by‑Step Guide
url: /net/programming-with-security-and-signatures/how-to-encrypt-pdf-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Encrypt PDF – C# Step‑by‑Step Guide

Ever wondered **how to encrypt PDF** files directly from your C# application? You're not the only one—developers constantly need to protect confidential reports, invoices, or contracts without dragging a third‑party UI tool.  

The good news is that you can do it programmatically in just a few lines, and you’ll also learn **remove PDF encryption**, **how to decrypt PDF**, and even **set owner password PDF** for tighter control. In this tutorial we’ll walk through a complete, ready‑to‑run example, explain why each line matters, and cover a few common pitfalls along the way.

> **Quick recap:** By the end of this guide you’ll have a C# console app that can encrypt a PDF with an owner password, decrypt it using that same password, and optionally strip the protection entirely.

## Prerequisites — What You Need Before You Start

- .NET 6.0 or later (the code also works on .NET Framework 4.8, but the newer SDK gives a nicer experience).  
- A PDF library that exposes `Security`, `EncryptionOptions`, `DecryptionOptions`, and `FileDataSource`. In our examples we use the fictional **PdfSecurityLib** – replace it with the actual library you’re using (e.g., iText7, PdfSharpCore, etc.).  
- A sample PDF named `sample.pdf` placed in a folder you control (we’ll refer to it as `YOUR_DIRECTORY`).  
- Basic familiarity with C# console applications.

If any of those sound unfamiliar, pause a moment and install the .NET SDK or grab the NuGet package for your chosen PDF library. Once you’re set, let’s dive in.

![how to encrypt pdf example](https://example.com/images/encrypt-pdf.png "how to encrypt pdf example")

## How to Encrypt PDF with an Owner Password

### Step 1 — Create the encryption engine

The `Security` class is the entry point for all cryptographic operations. Think of it as the “security guard” that decides who can open the document.

```csharp
using PdfSecurityLib;          // Replace with your actual namespace
using System;

namespace PdfEncryptionDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the security engine
            var encryptor = new Security();
```

### Step 2 — Configure encryption options

Here we define the **owner password** (`123456789`) and a **user password** (`123`). The owner password lets you change permissions later, while the user password is what a typical viewer would need to open the file. We also forbid all editing privileges to illustrate a strict policy.

```csharp
            // 2️⃣ Set up encryption details
            var encryptionOptions = new EncryptionOptions(
                ownerPassword: "123456789",
                userPassword:  "123",
                permissions:   DocumentPrivilege.ForbidAll);

            // Tell the engine where to read from and where to write to
            encryptionOptions.AddInput(new FileDataSource(@"YOUR_DIRECTORY\sample.pdf"));
            encryptionOptions.AddOutput(new FileDataSource(@"YOUR_DIRECTORY\encrypted.pdf"));
```

### Step 3 — Apply the encryption

Calling `Process` actually writes the encrypted file to disk. If everything goes well, you’ll see `encrypted.pdf` appear in your folder.

```csharp
            // 3️⃣ Perform the encryption
            encryptor.Process(encryptionOptions);
            Console.WriteLine("✅ PDF encrypted successfully.");
```

## Remove PDF Encryption – Decrypting the File

Now that we have a locked PDF, let’s see **how to decrypt PDF** using the owner password we set earlier. This part also demonstrates **remove PDF encryption** entirely, leaving you with a plain copy.

### Step 4 — Create the decryption engine

Just like encryption, decryption uses the same `Security` class. No need to instantiate a new type.

```csharp
            // 4️⃣ Initialize the decryption engine
            var decryptor = new Security();
```

### Step 5 — Configure decryption options

We only need the owner password here; the library will ignore the user password because we have full rights.

```csharp
            // 5️⃣ Define decryption parameters (owner password only)
            var decryptionOptions = new DecryptionOptions(ownerPassword: "123456789");
            decryptionOptions.AddInput(new FileDataSource(@"YOUR_DIRECTORY\encrypted.pdf"));
            decryptionOptions.AddOutput(new FileDataSource(@"YOUR_DIRECTORY\decrypted.pdf"));
```

### Step 6 — Remove the protection

Calling `Process` writes a clean, unprotected PDF to `decrypted.pdf`. If you compare it byte‑by‑byte with the original `sample.pdf`, they should be identical (aside from metadata timestamps).

```csharp
            // 6️⃣ Strip the encryption
            decryptor.Process(decryptionOptions);
            Console.WriteLine("✅ PDF decrypted (encryption removed) successfully.");
        }
    }
}
```

### Full Code Snapshot

Putting it all together, the complete program looks like this:

```csharp
using PdfSecurityLib;
using System;

namespace PdfEncryptionDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // ---------- Encrypt ----------
            var encryptor = new Security();

            var encryptionOptions = new EncryptionOptions(
                ownerPassword: "123456789",
                userPassword:  "123",
                permissions:   DocumentPrivilege.ForbidAll);

            encryptionOptions.AddInput(new FileDataSource(@"YOUR_DIRECTORY\sample.pdf"));
            encryptionOptions.AddOutput(new FileDataSource(@"YOUR_DIRECTORY\encrypted.pdf"));

            encryptor.Process(encryptionOptions);
            Console.WriteLine("✅ PDF encrypted successfully.");

            // ---------- Decrypt ----------
            var decryptor = new Security();

            var decryptionOptions = new DecryptionOptions(ownerPassword: "123456789");
            decryptionOptions.AddInput(new FileDataSource(@"YOUR_DIRECTORY\encrypted.pdf"));
            decryptionOptions.AddOutput(new FileDataSource(@"YOUR_DIRECTORY\decrypted.pdf"));

            decryptor.Process(decryptionOptions);
            Console.WriteLine("✅ PDF decrypted (encryption removed) successfully.");
        }
    }
}
```

Run the program (`dotnet run` from the project folder) and you’ll end up with two new files: `encrypted.pdf` (protected) and `decrypted.pdf` (plain). Open `encrypted.pdf` in any PDF viewer; you’ll be prompted for the user password (`123`). Supply the owner password (`123456789`) and you’ll see the document with full rights.

## Set Owner Password PDF – Best Practices

While the example uses simple numeric passwords, production code should follow these guidelines:

| Guideline | Why It Matters |
|-----------|----------------|
| **Use at least 12 characters** | Longer passwords resist brute‑force attacks. |
| **Mix character sets** (upper, lower, digits, symbols) | Increases entropy, making the password harder to guess. |
| **Store passwords securely** (e.g., Azure Key Vault, AWS Secrets Manager) | Hard‑coding secrets is a security anti‑pattern. |
| **Validate password strength before encryption** | Prevents accidental weak protection. |
| **Prefer owner‑only encryption** when you need to change permissions later | The owner password can modify rights without re‑encrypting the whole file. |

Implementing these checks is straightforward. Here’s a tiny helper you can drop into the above program:

```csharp
static bool IsStrongPassword(string pwd)
{
    return pwd.Length >= 12 &&
           System.Text.RegularExpressions.Regex.IsMatch(pwd, @"[A-Z]") &&
           System.Text.RegularExpressions.Regex.IsMatch(pwd, @"[a-z]") &&
           System.Text.RegularExpressions.Regex.IsMatch(pwd, @"\d") &&
           System.Text.RegularExpressions.Regex.IsMatch(pwd, @"[\W_]");
}
```

Call `IsStrongPassword` before you construct `EncryptionOptions`. If it returns `false`, throw an exception or prompt the user to choose a stronger phrase.

## How to Decrypt PDF Owner Password – Edge Cases

1. **Wrong Owner Password** – The library will raise a `SecurityException`. Catch it and inform the caller rather than crashing.

    ```csharp
    try { decryptor.Process(decryptionOptions); }
    catch (SecurityException ex)
    {
        Console.WriteLine($"❌ Decryption failed: {ex.Message}");
    }
    ```

2. **No Owner Password (User‑only protection)** – Some PDFs are encrypted with only a user password. In that case you must provide the *user* password to `DecryptionOptions`. The API usually has an overload that accepts both.

3. **Multiple Encryption Layers** – Rare, but if a PDF has been encrypted twice, you’ll need to run the decryption step repeatedly, each time with the correct password.

## Common Pitfalls & Pro Tips

- **Pitfall:** Forgetting to close file streams before re‑using the same path.  
  **Pro tip:** The `FileDataSource` class handles stream disposal internally, but if you open files manually, wrap them in `using`.

- **Pitfall:** Using the same password for owner and user.  
  **Pro tip:** Keep them distinct; the owner password should be secret, while the user password can be shared with intended recipients.

- **Pitfall:** Over‑restricting permissions and then being unable to edit later.  
  **Pro tip:** Start with `DocumentPrivilege.AllowAll` during development, then tighten the rights once you’re confident the workflow works.

- **Pitfall:** Hard‑coding paths like `"YOUR_DIRECTORY\sample.pdf"` on Linux.  
  **Pro tip:** Use `Path.Combine(Environment.CurrentDirectory, "sample.pdf")` for cross‑platform compatibility.

## Verify Your Results

After the program finishes, perform these quick checks:

1. Open `encrypted.pdf` → it should request a password.  
2. Enter the **user password** (`123`) → the file opens read‑only.  
3. Open `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}