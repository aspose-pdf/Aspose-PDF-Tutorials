---
title: Rotar cada página de PDF 180° usando Aspose.Pdf para .NET
weight: 260
limit:
description: Guía paso a paso para rotar todas las páginas de un PDF 180 grados con Aspose.Pdf para .NET.
keywords: [rotate pdf pages .net, Aspose.Pdf for .NET, rotate all pages 180 degrees, pdf page rotation, c# pdf manipulation]
url: /net/programming-with-pdf-pages/rotate-pages/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Guía paso a paso para rotar todas las páginas de un PDF 180 grados
    con Aspose.Pdf para .NET.
  headline: Rotar cada página de PDF 180° usando Aspose.Pdf para .NET
  type: TechArticle
- description: Guía paso a paso para rotar todas las páginas de un PDF 180 grados
    con Aspose.Pdf para .NET.
  name: Rotar cada página de PDF 180° usando Aspose.Pdf para .NET
  steps:
  - name: Declare las rutas de archivo de origen y destino para el PDF.
    text: Declare las rutas de archivo de origen y destino para el PDF.
  - name: Verifique que el archivo de origen exista y abortar con un mensaje de error
      si no es así.
    text: Verifique que el archivo de origen exista y abortar con un mensaje de error
      si no es así.
  - name: Cree un objeto Document para el PDF de origen dentro de un bloque using
      para gestionar los recursos.
    text: Cree un objeto Document para el PDF de origen dentro de un bloque using
      para gestionar los recursos.
  - name: Itere a través de cada Page en pdfDoc.Pages y establezca su propiedad Rotate
      a Rotation.on180, volteando cada página al revés.
    text: Itere a través de cada Page en pdfDoc.Pages y establezca su propiedad Rotate
      a Rotation.on180, volteando cada página al revés.
  - name: Guarde el Document modificado en el archivo de destino, preservando las
      rotaciones.
    text: Guarde el Document modificado en el archivo de destino, preservando las
      rotaciones.
  - name: Escriba un mensaje de confirmación en la consola indicando que la operación
      se completó.
    text: Escriba un mensaje de confirmación en la consola indicando que la operación
      se completó.
  type: HowTo
- questions:
  - answer: El código verifica `File.Exists(sourceFile)` y escribe un error en `Console.Error`
      antes de devolver, por lo que no se lanza ninguna excepción y el programa finaliza
      de forma ordenada.
    question: ¿Qué ocurre si el archivo PDF de origen no existe?
  - answer: Sí, reemplace `Rotation.on180` por otro valor de enumeración como `Rotation.on90`
      (horario) o `Rotation.on270` (antihorario) para aplicar una rotación diferente.
    question: ¿Puedo rotar las páginas en un ángulo diferente, por ejemplo, 90° en
      sentido horario?
  - answer: La colección `Pages` de Aspose.Pdf está basada en 1, pero el iterador
      `foreach` abstrae eso, iterando sobre cada objeto `Page` sin importar el índice
      subyacente.
    question: ¿La colección de páginas está basada en cero? ¿Cómo funciona el bucle
      `foreach`?
  - answer: Llamar a `pdfDoc.Save(destinationFile)` sobrescribirá cualquier archivo
      existente con ese nombre, así que use un nombre de archivo diferente o haga
      una copia de seguridad del original si necesita conservarlo.
    question: ¿Se sobrescribirá el PDF original si utilizo el mismo nombre de archivo
      para `destinationFile`?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/rotate-pages/og-image.png
og_title: Rotar cada página de PDF 180°
og_description: Aprenda cómo voltear todas las páginas de un PDF al revés con solo unas pocas líneas de código C#.
og_image_alt: Guía que muestra cómo rotar cada página de un PDF 180 grados usando Aspose.Pdf para .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Rotar cada página de PDF 180° usando Aspose.Pdf para .NET
Este tutorial muestra cómo rotar cada página de un documento PDF existente 180 grados con la clase Document de Aspose.Pdf. Al aplicar una rotación de página completa, puede corregir rápidamente escaneos al revés o reorientar documentos sin recrearlos. El ejemplo está escrito en C# y funciona en la plataforma .NET.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/rotate-pages" >}}


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

**Q: ¿Qué ocurre si el archivo PDF de origen no existe?**  
A: El código verifica `File.Exists(sourceFile)` y escribe un error en `Console.Error` antes de devolver, por lo que no se lanza ninguna excepción y el programa finaliza de forma ordenada.

**Q: ¿Puedo rotar las páginas en un ángulo diferente, por ejemplo, 90° en sentido horario?**  
A: Sí, reemplace `Rotation.on180` por otro valor de enumeración como `Rotation.on90` (horario) o `Rotation.on270` (antihorario) para aplicar una rotación diferente.

**Q: ¿La colección de páginas está basada en cero? ¿Cómo funciona el bucle `foreach`?**  
A: La colección `Pages` de Aspose.Pdf está basada en 1, pero el iterador `foreach` abstrae eso, iterando sobre cada objeto `Page` sin importar el índice subyacente.

**Q: ¿Se sobrescribirá el PDF original si utilizo el mismo nombre de archivo para `destinationFile`?**  
A: Llamar a `pdfDoc.Save(destinationFile)` sobrescribirá cualquier archivo existente con ese nombre, así que use un nombre de archivo diferente o haga una copia de seguridad del original si necesita conservarlo.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}