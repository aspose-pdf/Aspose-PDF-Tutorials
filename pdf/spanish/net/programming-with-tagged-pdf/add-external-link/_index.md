---
title: Agregar enlace externo etiquetado con tooltip al PDF usando Aspose.Pdf para .NET
weight: 440
limit:
description: Aprenda cómo agregar un hipervínculo externo etiquetado con texto visible y tooltip a un PDF usando Aspose.Pdf para .NET.
keywords: [Aspose.Pdf for .NET, add external link pdf, tagged pdf hyperlink, pdf tooltip title, pdf logical structure, c# pdf hyperlink]
url: /net/programming-with-tagged-pdf/add-external-link/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Aprenda cómo agregar un hipervínculo externo etiquetado con texto visible
    y tooltip a un PDF usando Aspose.Pdf para .NET.
  headline: Agregar enlace externo etiquetado con tooltip al PDF usando Aspose.Pdf
    para .NET
  type: TechArticle
- description: Aprenda cómo agregar un hipervínculo externo etiquetado con texto visible
    y tooltip a un PDF usando Aspose.Pdf para .NET.
  name: Agregar enlace externo etiquetado con tooltip al PDF usando Aspose.Pdf para
    .NET
  steps:
  - name: Defina las rutas del PDF de origen y del archivo de resultado.
    text: Defina las rutas del PDF de origen y del archivo de resultado.
  - name: Verifique que el PDF de origen exista y abortar si no se encuentra.
    text: Verifique que el PDF de origen exista y abortar si no se encuentra.
  - name: Abra el documento PDF dentro de un bloque using para garantizar su correcta
      liberación.
    text: Abra el documento PDF dentro de un bloque using para garantizar su correcta
      liberación.
  - name: Obtenga el administrador de contenido etiquetado para el documento abierto.
    text: Obtenga el administrador de contenido etiquetado para el documento abierto.
  - name: Establezca el idioma del documento a English (US) y dé al PDF un título
      derivado del nombre del archivo.
    text: Establezca el idioma del documento a English (US) y dé al PDF un título
      derivado del nombre del archivo.
  - name: Recupere el elemento raíz del árbol de estructura lógica al que se agregarán
      los nuevos elementos.
    text: Recupere el elemento raíz del árbol de estructura lógica al que se agregarán
      los nuevos elementos.
  - name: Cree un elemento de enlace, establezca su texto visible, la URL de destino
      y el título del tooltip, y luego insértelo en la estructura del documento.
    text: Cree un elemento de enlace, establezca su texto visible, la URL de destino
      y el título del tooltip, y luego insértelo en la estructura del documento.
  - name: Guarde el PDF actualizado en el archivo de resultado especificado.
    text: Guarde el PDF actualizado en el archivo de resultado especificado.
  - name: Muestre un mensaje de confirmación que indique dónde se guardó el PDF modificado.
    text: Muestre un mensaje de confirmación que indique dónde se guardó el PDF modificado.
  type: HowTo
- questions:
  - answer: '`pdfDoc.TaggedContent` devuelve el contenido etiquetado existente si
      el documento ya está etiquetado; no crea un árbol duplicado.'
    question: ¿Qué ocurre si el PDF de origen ya está etiquetado – al llamar a `pdfDoc.TaggedContent`
      se creará un nuevo árbol de etiquetas o se reutilizará el existente?
  - answer: Sí – localice el `StructureElement` deseado (p. ej., un `Div` o `Paragraph`
      en una página) mediante el árbol de estructura lógica y llame a `AppendChild(externalLink)`
      sobre ese elemento.
    question: ¿Puedo colocar el hipervínculo en una página específica en lugar de
      añadirlo al elemento raíz?
  - answer: El tooltip se muestra solo si `externalLink.Title` se establece antes
      de `pdfDoc.Save`; establecerlo después de guardar no tiene efecto en el PDF
      ya escrito.
    question: ¿Es necesaria la propiedad `Title` de `LinkElement` para que aparezca
      el tooltip, y puede establecerse después de llamar a `Save`?
  - answer: Asigne un `FileSpecification` (p. ej., `new FileSpecification(\"file:///C:/Docs/manual.pdf\")`)
      a `externalLink.Hyperlink` en lugar de usar `WebHyperlink`.
    question: ¿Cómo crear un enlace a un archivo local en lugar de una URL web?
  type: FAQPage
images:
- /net/programming-with-tagged-pdf/add-external-link/og-image.png
og_title: Insertar un enlace externo etiquetado con tooltip en un PDF
og_description: Incruste un hipervínculo accesible con texto visible y tooltip en su PDF usando Aspose.Pdf para .NET.
og_image_alt: Guía que muestra cómo agregar un hipervínculo externo etiquetado con tooltip a un PDF usando Aspose.Pdf para .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Agregar enlace externo etiquetado con tooltip al PDF usando Aspose.Pdf para .NET
Este tutorial muestra cómo abrir un PDF existente con Aspose.Pdf para .NET, crear un hipervínculo externo etiquetado que incluya texto visible y un título de tooltip, insertar el enlace en la estructura lógica del documento y guardar el archivo actualizado. Al seguir los pasos, producirá un PDF accesible donde el enlace forma parte de la jerarquía de etiquetas y brinda contexto adicional a los lectores.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-tagged-pdf/add-external-link" >}}


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

**Q: ¿Qué ocurre si el PDF de origen ya está etiquetado – al llamar a `pdfDoc.TaggedContent` se creará un nuevo árbol de etiquetas o se reutilizará el existente?**  
A: `pdfDoc.TaggedContent` devuelve el contenido etiquetado existente si el documento ya está etiquetado; no crea un árbol duplicado.

**Q: ¿Puedo colocar el hipervínculo en una página específica en lugar de añadirlo al elemento raíz?**  
A: Sí – localice el `StructureElement` deseado (p. ej., un `Div` o `Paragraph` en una página) mediante el árbol de estructura lógica y llame a `AppendChild(externalLink)` sobre ese elemento.

**Q: ¿Es necesaria la propiedad `Title` de `LinkElement` para que aparezca el tooltip, y puede establecerse después de llamar a `Save`?**  
A: El tooltip se muestra solo si `externalLink.Title` se establece antes de `pdfDoc.Save`; establecerlo después de guardar no tiene efecto en el PDF ya escrito.

**Q: ¿Cómo crear un enlace a un archivo local en lugar de una URL web?**  
A: Asigne un `FileSpecification` (p. ej., `new FileSpecification(\"file:///C:/Docs/manual.pdf\")`) a `externalLink.Hyperlink` en lugar de usar `WebHyperlink`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}