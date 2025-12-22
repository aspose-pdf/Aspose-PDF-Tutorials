---
category: general
date: 2025-12-22
description: How to encrypt PDF files with password protection using C#. Learn pdf
  password protection, encrypt pdf with password, and decrypt pdf with password in
  a single tutorial.
draft: false
keywords:
- how to encrypt pdf
- pdf password protection
- encrypt pdf with password
- decrypt pdf with password
- protect pdf with password
language: en
og_description: How to encrypt PDF files with password protection in C#. This guide
  shows you how to encrypt pdf with password and decrypt pdf with password, plus best
  practices.
og_title: How to Encrypt PDF – Step‑by‑Step Password Protection
tags:
- PDF
- C#
- Security
title: How to Encrypt PDF — Complete Guide with Password Protection and Decryption
url: /net/programming-with-security-and-signatures/how-to-encrypt-pdf-complete-guide-with-password-protection-a/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Encrypt PDF – Full‑Stack Password Protection Tutorial

Ever wondered **how to encrypt PDF** files so only the right people can open them? You're not the only one. Whether you're safeguarding financial statements, confidential contracts, or a simple personal note, adding password protection to a PDF is a tiny step that makes a huge security difference.

In this guide we'll walk through the entire process: from **pdf password protection** using C# to encrypt a document, to unlocking it again with the owner password. We'll also cover common pitfalls, variations like setting user‑only passwords, and a quick sanity check to make sure the protection actually works. By the end you’ll be able to **encrypt pdf with password**, **protect pdf with password**, and later **decrypt pdf with password**—all in a few lines of code.

## What You’ll Need

- .NET 6.0 or later (the code works with .NET Framework 4.7+ as well)  
- A PDF library that exposes `Security`, `EncryptionOptions`, `DecryptionOptions`, and `FileDataSource` classes (e.g., *PdfSharpCore* or a commercial SDK).  
- Two sample PDFs: one plain file (`sample.pdf`) and a folder where you have write permission.  

No extra NuGet packages beyond the PDF SDK itself. If you’re using a commercial library, replace the namespace imports accordingly.

## Step 1: Add the Required Namespaces

First, reference the SDK and any I/O helpers. This tiny block sets the stage for everything that follows.

```csharp
using System;
using YourPdfLibrary;          // Replace with the actual library namespace
using YourPdfLibrary.IO;       // For FileDataSource
using YourPdfLibrary.Security; // For Security, EncryptionOptions, DecryptionOptions
```

> **Pro tip:** If your IDE supports *global using* directives, dump these into a single file and you’ll never have to repeat them.

## Step 2: Create a Security Instance for Encryption

The `Security` class is the workhorse that applies cryptographic rules to a PDF. Think of it as the guard at the door.

```csharp
// Step 2: Initialize the encryptor
var encryptor = new Security();
```

Why a separate instance? The library keeps encryption and decryption state isolated, so you can reuse the same `Security` object for multiple documents without cross‑contamination.

## Step 3: Configure Encryption Options (Owner & User Passwords)

Now we tell the SDK *how* to protect the PDF. The owner password grants full rights (including changing permissions), while the user password only allows opening the file.

```csharp
// Step 3: Set up encryption parameters
var encryptionOptions = new EncryptionOptions(
    ownerPassword: "123456789",   // Full‑control password
    userPassword: "123",          // Password required just to open the file
    permissions: DocumentPrivilege.ForbidAll   // No printing, copying, etc.
);

// Attach input and output files
encryptionOptions.AddInput(new FileDataSource(@"YOUR_DIRECTORY\sample.pdf"));
encryptionOptions.AddOutput(new FileDataSource(@"YOUR_DIRECTORY\encrypted.pdf"));
```

> **Why forbid everything?** `DocumentPrivilege.ForbidAll` is a safe default for confidential docs. If you need to allow printing, replace it with `DocumentPrivilege.AllowPrinting`. This flexibility is why **pdf password protection** is more than a single password—it’s a policy.

## Step 4: Apply the Encryption Settings

With everything wired up, we finally run the encryption process.

```csharp
// Step 4: Encrypt the PDF
encryptor.Process(encryptionOptions);
Console.WriteLine("✅ PDF encrypted successfully: encrypted.pdf");
```

If the source file is missing or the output path is read‑only, the SDK will throw an exception—wrap it in a `try/catch` for production code.

## Step 5: Verify the Encryption (Optional but Recommended)

Before moving on, open `encrypted.pdf` in any PDF viewer. It should prompt for the *user password* (`123`). Trying to print or copy text will be blocked because we set `ForbidAll`. This quick sanity check confirms that our **protect pdf with password** step actually worked.

![Diagram showing how to encrypt PDF with password protection](https://example.com/images/encrypt-pdf-diagram.png "how to encrypt pdf illustration")

*Alt text:* how to encrypt pdf illustration

## Step 6: Create a Security Instance for Decryption

Decryption mirrors encryption but only needs the owner password (or the user password if the document allows it). Let’s set up the decryptor.

```csharp
// Step 6: Initialize the decryptor
var decryptor = new Security();
```

## Step 7: Configure Decryption Options

Here we supply the owner password we used earlier. If you only have the user password, pass that instead—just remember the permissions will stay limited.

```csharp
// Step 7: Set up decryption parameters
var decryptionOptions = new DecryptionOptions(ownerPassword: "123456789");

// Attach input and output files
decryptionOptions.AddInput(new FileDataSource(@"YOUR_DIRECTORY\encrypted.pdf"));
decryptionOptions.AddOutput(new FileDataSource(@"YOUR_DIRECTORY\decrypted.pdf"));
```

> **Edge case:** Some PDFs are encrypted with *AES‑256* only. Make sure your library version supports that algorithm; otherwise you’ll see an “Unsupported encryption” error.

## Step 8: Decrypt the PDF

Run the decryption process and watch the output file appear.

```csharp
// Step 8: Decrypt the PDF
decryptor.Process(decryptionOptions);
Console.WriteLine("🔓 PDF decrypted successfully: decrypted.pdf");
```

Open `decrypted.pdf`—you should see the original content, without any password prompt. If the file still asks for a password, double‑check that the owner password matches exactly (including case).

## Full Working Example

Putting it all together, here’s a self‑contained console app you can copy‑paste into Visual Studio. Adjust the `YOUR_DIRECTORY` placeholder to a real folder on your machine.

```csharp
using System;
using YourPdfLibrary;
using YourPdfLibrary.IO;
using YourPdfLibrary.Security;

class Program
{
    static void Main()
    {
        try
        {
            // ---------- Encryption ----------
            var encryptor = new Security();
            var encOpts = new EncryptionOptions(
                ownerPassword: "123456789",
                userPassword: "123",
                permissions: DocumentPrivilege.ForbidAll);

            encOpts.AddInput(new FileDataSource(@"YOUR_DIRECTORY\sample.pdf"));
            encOpts.AddOutput(new FileDataSource(@"YOUR_DIRECTORY\encrypted.pdf"));
            encryptor.Process(encOpts);
            Console.WriteLine("✅ Encrypted PDF created.");

            // ---------- Decryption ----------
            var decryptor = new Security();
            var decOpts = new DecryptionOptions(ownerPassword: "123456789");
            decOpts.AddInput(new FileDataSource(@"YOUR_DIRECTORY\encrypted.pdf"));
            decOpts.AddOutput(new FileDataSource(@"YOUR_DIRECTORY\decrypted.pdf"));
            decryptor.Process(decOpts);
            Console.WriteLine("🔓 Decrypted PDF restored.");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Error: {ex.Message}");
        }
    }
}
```

**Expected output in the console**

```
✅ Encrypted PDF created.
🔓 Decrypted PDF restored.
```

And two new files appear: `encrypted.pdf` (password‑protected) and `decrypted.pdf` (original content).

## Common Questions & Gotchas

| Question | Answer |
|----------|--------|
| *Can I set a different user password than the owner password?* | Absolutely. Pass two distinct strings to `EncryptionOptions`. The user password opens the file; the owner password lets you change permissions later. |
| *What if I need to allow printing but still forbid copying?* | Use `DocumentPrivilege.AllowPrinting` combined with `DocumentPrivilege.ForbidCopying`. Most SDKs expose a flags enum you can OR together. |
| *Is AES‑256 supported?* | Check the library’s changelog. If not, you might need to upgrade or switch to a newer SDK. |
| *Do I need to dispose of `Security` objects?* | They usually implement `IDisposable`. Wrap them in `using` statements in production code to free native resources promptly. |
| *How do I encrypt multiple PDFs in a batch?* | Loop over a collection of file paths, reusing the same `Security` instance or creating a new one per file—both approaches work. |

## Best Practices for PDF Password Protection

1. **Use strong, random passwords** – avoid simple strings like “123”. Consider a password manager‑generated GUID.  
2. **Store passwords securely** – never hard‑code them in source control; use environment variables or Azure Key Vault.  
3. **Log only success/failure, never the password** – this prevents accidental exposure in logs.  
4. **Validate encryption** – after encrypting, open the file programmatically to ensure it actually requires a password.  
5. **Document the policy** – keep a short README describing which PDFs are protected and why, so future maintainers understand the intent.

## Conclusion

We’ve covered **how to encrypt PDF** files with robust password protection, demonstrated how to **encrypt pdf with password**, showed you how to **protect pdf with password**, and finally walked through **decrypt pdf with password** using a straightforward C# workflow. By following the steps above you’ll have a reliable, repeatable pattern for securing any PDF in your .NET projects.

Ready for the next challenge? Try adding **digital signatures**, experiment with **different permission sets**, or integrate this logic into an ASP.NET Core API that encrypts user‑uploaded documents on the fly. The sky’s the limit, and now you have a solid foundation to build on.

Happy coding, and keep those PDFs safe!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}