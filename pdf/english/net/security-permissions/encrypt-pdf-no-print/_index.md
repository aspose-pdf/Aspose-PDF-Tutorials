---
title: Encrypt PDF with No‑Print Permission Using Aspose.PDF for .NET
weight: 101
limit:
description: Learn how to encrypt a PDF with AES‑256 and disable printing using Aspose.PDF for .NET.
keywords: [Aspose.PDF for .NET, pdf encryption aes-256, disable pdf printing, pdf password protection, no print permission pdf]
url: /net/security-permissions/encrypt-pdf-no-print/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Learn how to encrypt a PDF with AES‑256 and disable printing using
    Aspose.PDF for .NET.
  headline: Encrypt PDF with No‑Print Permission Using Aspose.PDF for .NET
  type: TechArticle
- description: Learn how to encrypt a PDF with AES‑256 and disable printing using
    Aspose.PDF for .NET.
  name: Encrypt PDF with No‑Print Permission Using Aspose.PDF for .NET
  steps:
  - name: Define the source PDF path, the output protected file name, and the viewer
      and owner passwords.
    text: Define the source PDF path, the output protected file name, and the viewer
      and owner passwords.
  - name: Check that the source file exists and abort with an error message if it
      is missing.
    text: Check that the source file exists and abort with an error message if it
      is missing.
  - name: Open the original PDF, set no permissions, encrypt it with AES‑256 using
      the specified passwords, and save the protected file.
    text: Open the original PDF, set no permissions, encrypt it with AES‑256 using
      the specified passwords, and save the protected file.
  - name: Re‑open the encrypted PDF with the viewer password and write its IsEncrypted
      flag to the console to confirm protection.
    text: Re‑open the encrypted PDF with the viewer password and write its IsEncrypted
      flag to the console to confirm protection.
  - name: Print a final message indicating that encryption is complete and the output
      file name.
    text: Print a final message indicating that encryption is complete and the output
      file name.
  type: HowTo
- questions:
  - answer: '`Permissions` is a flag enum; assigning `0` means no permission bits
      are set, so Aspose.Pdf does not grant the PrintDocument right and the viewer
      cannot print the PDF.'
    question: Why does setting `Permissions rights = 0;` disable printing?
  - answer: Yes, replace `CryptoAlgorithm.AESx256` with `CryptoAlgorithm.AESx128`
      (or another supported enum value) in the `pdfDoc.Encrypt` call; the rest of
      the code stays unchanged.
    question: Can I use a different encryption algorithm, like AES‑128, with the same
      code?
  - answer: Aspose.Pdf will accept identical passwords, but the owner password will
      no longer provide extra privileges; the PDF will still be encrypted, and the
      permissions you specified (none) will apply.
    question: What happens if the viewer password and the master (owner) password
      are the same?
  - answer: Open the protected file with the viewer password (`new Document(securedFile,
      viewerPwd)`) and try to print from a PDF viewer; because no `PrintDocument`
      permission was set, the viewer will refuse the print command.
    question: How can I confirm that printing is really blocked after encryption?
  - answer: The code checks `File.Exists(sourceFile)` and writes an error to `Console.Error`
      before returning, preventing a `FileNotFoundException` from being thrown by
      the `Document` constructor.
    question: What error is thrown if `original.pdf` does not exist, and how should
      I handle it?
  type: FAQPage
images:
- /net/security-permissions/encrypt-pdf-no-print/og-image.png
og_title: Encrypt PDF and Block Printing
og_description: Secure your PDF with AES‑256 encryption and make sure it can’t be printed—step‑by‑step guide.
og_image_alt: Screenshot showing Aspose.PDF for .NET code that encrypts a PDF and disables printing.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Encrypt PDF with No‑Print Permission Using Aspose.PDF
This tutorial shows how to open an existing PDF with Aspose.PDF for .NET, apply AES‑256 encryption while granting no permissions—effectively disabling printing—save the secured document, and confirm the protection by opening it with the viewer password. Follow the step‑by‑step code to ensure your PDF cannot be printed after encryption.

---

{{< tutorial-widget sourcePath="pdf/net/security-permissions/encrypt-pdf-no-print" >}}


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

**Q: Why does setting `Permissions rights = 0;` disable printing?**  
A: `Permissions` is a flag enum; assigning `0` means no permission bits are set, so Aspose.Pdf does not grant the PrintDocument right and the viewer cannot print the PDF.

**Q: Can I use a different encryption algorithm, like AES‑128, with the same code?**  
A: Yes, replace `CryptoAlgorithm.AESx256` with `CryptoAlgorithm.AESx128` (or another supported enum value) in the `pdfDoc.Encrypt` call; the rest of the code stays unchanged.

**Q: What happens if the viewer password and the master (owner) password are the same?**  
A: Aspose.Pdf will accept identical passwords, but the owner password will no longer provide extra privileges; the PDF will still be encrypted, and the permissions you specified (none) will apply.

**Q: How can I confirm that printing is really blocked after encryption?**  
A: Open the protected file with the viewer password (`new Document(securedFile, viewerPwd)`) and try to print from a PDF viewer; because no `PrintDocument` permission was set, the viewer will refuse the print command.

**Q: What error is thrown if `original.pdf` does not exist, and how should I handle it?**  
A: The code checks `File.Exists(sourceFile)` and writes an error to `Console.Error` before returning, preventing a `FileNotFoundException` from being thrown by the `Document` constructor.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}