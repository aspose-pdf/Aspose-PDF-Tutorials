---
title: Encrypt PDF to Allow Only Form Filling Using Aspose.Pdf for .NET
weight: 101
limit:
description: Learn how to encrypt a PDF with AES‑256, set passwords, and limit permissions to form‑filling only using Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, encrypt PDF, PDF form filling permissions, AES-256 PDF encryption, viewer password PDF, owner password PDF]
url: /net/security-permissions/encrypt-pdf-form-filling/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Learn how to encrypt a PDF with AES‑256, set passwords, and limit permissions
    to form‑filling only using Aspose.Pdf for .NET.
  headline: Encrypt PDF to Allow Only Form Filling Using Aspose.Pdf for .NET
  type: TechArticle
- description: Learn how to encrypt a PDF with AES‑256, set passwords, and limit permissions
    to form‑filling only using Aspose.Pdf for .NET.
  name: Encrypt PDF to Allow Only Form Filling Using Aspose.Pdf for .NET
  steps:
  - name: Define the source and destination file paths and the viewer and owner passwords.
    text: Define the source and destination file paths and the viewer and owner passwords.
  - name: Check that the source PDF exists and abort with an error message if it does
      not.
    text: Check that the source PDF exists and abort with an error message if it does
      not.
  - name: Start a try block to handle any errors that may occur during processing.
    text: Start a try block to handle any errors that may occur during processing.
  - name: Open the existing PDF file by creating a Document object named pdfDoc.
    text: Open the existing PDF file by creating a Document object named pdfDoc.
  - name: Set permissions to allow only form filling, encrypt the document with viewer
      and owner passwords using AES‑256, and save the protected PDF.
    text: Set permissions to allow only form filling, encrypt the document with viewer
      and owner passwords using AES‑256, and save the protected PDF.
  - name: Write a confirmation message to the console and close the try block.
    text: Write a confirmation message to the console and close the try block.
  - name: Catch any exceptions and output the error message to the console.
    text: Catch any exceptions and output the error message to the console.
  type: HowTo
- questions:
  - answer: When opened with the viewer (user) password, the document can be viewed
      and form fields can be filled, but all other actions such as editing text, adding
      annotations, or extracting content are blocked.
    question: What can a user do with the PDF after it is encrypted with `Permissions.FillForm`?
  - answer: Combine permissions using the bitwise OR operator, e.g., `Permissions
      allowed = Permissions.FillForm | Permissions.Printing;` and pass the combined
      value to `pdfDoc.Encrypt`.
    question: How can I allow additional rights, like printing, while still restricting
      everything else?
  - answer: Yes. The first argument is the user (viewer) password that grants the
      limited rights, and the second argument is the owner (admin) password that provides
      full control over the document.
    question: Does the order of the passwords in `pdfDoc.Encrypt(viewerPass, adminPass,
      …)` matter?
  - answer: Aspose.Pdf will throw an exception when trying to open an already encrypted
      file; you must first open it with its existing password, remove or modify the
      protection, and then apply the new encryption settings.
    question: What happens if the source PDF is already password‑protected?
  type: FAQPage
images:
- /net/security-permissions/encrypt-pdf-form-filling/og-image.png
og_title: Encrypt PDF and Allow Only Form Filling
og_description: Secure your PDF with AES‑256 and let users fill forms but nothing else.
og_image_alt: Screenshot showing Aspose.Pdf for .NET code that encrypts a PDF and restricts it to form‑filling only
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Encrypt PDF to Allow Only Form Filling Using Aspose.Pdf
In this tutorial you’ll learn how to open an existing PDF with Aspose.Pdf for .NET, apply AES‑256 encryption, set viewer and owner passwords, and restrict the document’s permissions so that recipients can only fill out form fields. This approach is useful when you need to protect the content while still permitting users to complete interactive forms. The code walks through each step and saves the secured PDF ready for distribution.

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

**Q: What can a user do with the PDF after it is encrypted with `Permissions.FillForm`?**  
A: When opened with the viewer (user) password, the document can be viewed and form fields can be filled, but all other actions such as editing text, adding annotations, or extracting content are blocked.

**Q: How can I allow additional rights, like printing, while still restricting everything else?**  
A: Combine permissions using the bitwise OR operator, e.g., `Permissions allowed = Permissions.FillForm | Permissions.Printing;` and pass the combined value to `pdfDoc.Encrypt`.

**Q: Does the order of the passwords in `pdfDoc.Encrypt(viewerPass, adminPass, …)` matter?**  
A: Yes. The first argument is the user (viewer) password that grants the limited rights, and the second argument is the owner (admin) password that provides full control over the document.

**Q: What happens if the source PDF is already password‑protected?**  
A: Aspose.Pdf will throw an exception when trying to open an already encrypted file; you must first open it with its existing password, remove or modify the protection, and then apply the new encryption settings.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}