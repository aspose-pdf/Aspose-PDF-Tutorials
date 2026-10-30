---
title: Cifrar PDF con permiso de No‑Impresión usando Aspose.PDF para .NET
weight: 101
limit:
description: Aprenda a cifrar un PDF con AES‑256 y desactivar la impresión usando Aspose.PDF para .NET.
keywords: [Aspose.PDF for .NET, pdf encryption aes-256, disable pdf printing, pdf password protection, no print permission pdf]
url: /net/security-permissions/encrypt-pdf-no-print/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Aprenda a cifrar un PDF con AES‑256 y desactivar la impresión usando
    Aspose.PDF para .NET.
  headline: Cifrar PDF con permiso de No‑Impresión usando Aspose.PDF para .NET
  type: TechArticle
- description: Aprenda a cifrar un PDF con AES‑256 y desactivar la impresión usando
    Aspose.PDF para .NET.
  name: Cifrar PDF con permiso de No‑Impresión usando Aspose.PDF para .NET
  steps:
  - name: Defina la ruta del PDF de origen, el nombre del archivo protegido de salida
      y las contraseñas de visualización y de propietario.
    text: Defina la ruta del PDF de origen, el nombre del archivo protegido de salida
      y las contraseñas de visualización y de propietario.
  - name: Verifique que el archivo de origen exista y abortar con un mensaje de error
      si falta.
    text: Verifique que el archivo de origen exista y abortar con un mensaje de error
      si falta.
  - name: Abra el PDF original, establezca sin permisos, encripte el con AES‑256 usando
      las contraseñas especificadas y guarde el archivo protegido.
    text: Abra el PDF original, establezca sin permisos, encripte el con AES‑256 usando
      las contraseñas especificadas y guarde el archivo protegido.
  - name: Vuelva a abrir el PDF cifrado con la contraseña de visualización y escriba
      su bandera IsEncrypted en la consola para confirmar la protección.
    text: Vuelva a abrir el PDF cifrado con la contraseña de visualización y escriba
      su bandera IsEncrypted en la consola para confirmar la protección.
  - name: Imprima un mensaje final indicando que el cifrado está completo y el nombre
      del archivo de salida.
    text: Imprima un mensaje final indicando que el cifrado está completo y el nombre
      del archivo de salida.
  type: HowTo
- questions:
  - answer: '`Permissions` es un enum de banderas; asignar `0` significa que no se
      establecen bits de permiso, por lo que Aspose.Pdf no otorga el derecho PrintDocument
      y el visor no puede imprimir el PDF.'
    question: ¿Por qué establecer `Permissions rights = 0;` desactiva la impresión?
  - answer: Sí, reemplace `CryptoAlgorithm.AESx256` por `CryptoAlgorithm.AESx128`
      (u otro valor de enum compatible) en la llamada `pdfDoc.Encrypt`; el resto del
      código permanece sin cambios.
    question: ¿Puedo usar un algoritmo de cifrado diferente, como AES‑128, con el
      mismo código?
  - answer: Aspose.Pdf aceptará contraseñas idénticas, pero la contraseña de propietario
      ya no proporcionará privilegios adicionales; el PDF seguirá cifrado y se aplicarán
      los permisos que especificó (ninguno).
    question: ¿Qué ocurre si la contraseña de visualización y la contraseña maestra
      (de propietario) son iguales?
  - answer: Abra el archivo protegido con la contraseña de visualización (`new Document(securedFile,
      viewerPwd)`) e intente imprimir desde un visor de PDF; como no se estableció
      permiso `PrintDocument`, el visor rechazará el comando de impresión.
    question: ¿Cómo puedo confirmar que la impresión está realmente bloqueada después
      del cifrado?
  - answer: El código verifica `File.Exists(sourceFile)` y escribe un error en `Console.Error`
      antes de retornar, evitando que el constructor `Document` lance una `FileNotFoundException`.
    question: ¿Qué error se lanza si `original.pdf` no existe y cómo debo manejarlo?
  type: FAQPage
images:
- /net/security-permissions/encrypt-pdf-no-print/og-image.png
og_title: Cifrar PDF y bloquear la impresión
og_description: Asegure su PDF con cifrado AES‑256 y asegúrese de que no pueda imprimirse—guía paso a paso.
og_image_alt: Captura de pantalla que muestra código de Aspose.PDF para .NET que cifra un PDF y desactiva la impresión.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cifrar PDF con permiso de No‑Impresión usando Aspose.PDF para .NET
Este tutorial muestra cómo abrir un PDF existente con Aspose.PDF para .NET, aplicar cifrado AES‑256 sin conceder permisos—deshabilitando efectivamente la impresión—guardar el documento protegido y confirmar la protección abriéndolo con la contraseña de visualización. Siga el código paso a paso para asegurarse de que su PDF no pueda imprimirse después del cifrado.

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

**Q: ¿Por qué establecer `Permissions rights = 0;` desactiva la impresión?**  
A: `Permissions` es un enum de banderas; asignar `0` significa que no se establecen bits de permiso, por lo que Aspose.Pdf no otorga el derecho PrintDocument y el visor no puede imprimir el PDF.

**Q: ¿Puedo usar un algoritmo de cifrado diferente, como AES‑128, con el mismo código?**  
A: Sí, reemplace `CryptoAlgorithm.AESx256` por `CryptoAlgorithm.AESx128` (u otro valor de enum compatible) en la llamada `pdfDoc.Encrypt`; el resto del código permanece sin cambios.

**Q: ¿Qué ocurre si la contraseña de visualización y la contraseña maestra (de propietario) son iguales?**  
A: Aspose.Pdf aceptará contraseñas idénticas, pero la contraseña de propietario ya no proporcionará privilegios adicionales; el PDF seguirá cifrado y se aplicarán los permisos que especificó (ninguno).

**Q: ¿Cómo puedo confirmar que la impresión está realmente bloqueada después del cifrado?**  
A: Abra el archivo protegido con la contraseña de visualización (`new Document(securedFile, viewerPwd)`) e intente imprimir desde un visor de PDF; como no se estableció permiso `PrintDocument`, el visor rechazará el comando de impresión.

**Q: ¿Qué error se lanza si `original.pdf` no existe y cómo debo manejarlo?**  
A: El código verifica `File.Exists(sourceFile)` y escribe un error en `Console.Error` antes de retornar, evitando que el constructor `Document` lance una `FileNotFoundException`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}