---
title: Comparación PDF lado a lado excluyendo anotaciones con Aspose.Pdf for .NET
weight: 101
limit:
description: Guía paso a paso para comparar PDFs y excluir áreas de anotaciones usando Aspose.Pdf for .NET.
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Guía paso a paso para comparar PDFs y excluir áreas de anotaciones
    usando Aspose.Pdf for .NET.
  headline: Comparación PDF lado a lado excluyendo anotaciones con Aspose.Pdf for
    .NET
  type: TechArticle
- description: Guía paso a paso para comparar PDFs y excluir áreas de anotaciones
    usando Aspose.Pdf for .NET.
  name: Comparación PDF lado a lado excluyendo anotaciones con Aspose.Pdf for .NET
  steps:
  - name: Define las rutas de archivo para el PDF principal, el PDF secundario y el
      PDF de diferencias de salida.
    text: Define las rutas de archivo para el PDF principal, el PDF secundario y el
      PDF de diferencias de salida.
  - name: Verifica que ambos archivos PDF de entrada existan y aborta con un mensaje
      de error si falta alguno.
    text: Verifica que ambos archivos PDF de entrada existan y aborta con un mensaje
      de error si falta alguno.
  - name: Abre los dos archivos PDF como objetos Document (pdfA y pdfB) dentro de
      un bloque using para que se eliminen automáticamente.
    text: Abre los dos archivos PDF como objetos Document (pdfA y pdfB) dentro de
      un bloque using para que se eliminen automáticamente.
  - name: Recopila los rectángulos delimitadores de cada anotación en pdfA y guárdalos
      en ignoredRectsA.
    text: Recopila los rectángulos delimitadores de cada anotación en pdfA y guárdalos
      en ignoredRectsA.
  - name: Recopila los rectángulos delimitadores de cada anotación en pdfB y guárdalos
      en ignoredRectsB.
    text: Recopila los rectángulos delimitadores de cada anotación en pdfB y guárdalos
      en ignoredRectsB.
  - name: Crea un objeto SideBySideComparisonOptions y asigna los rectángulos de anotación
      recopilados previamente a ExcludeAreas1 y ExcludeAreas2 para que esas regiones
      se ignoren durante la comparación.
    text: Crea un objeto SideBySideComparisonOptions y asigna los rectángulos de anotación
      recopilados previamente a ExcludeAreas1 y ExcludeAreas2 para que esas regiones
      se ignoren durante la comparación.
  - name: Ejecuta la comparación PDF lado a lado usando los dos objetos Document y
      las opciones configuradas, escribiendo el resultado en outputPdf.
    text: Ejecuta la comparación PDF lado a lado usando los dos objetos Document y
      las opciones configuradas, escribiendo el resultado en outputPdf.
  - name: Elimina los objetos Document y sale del bloque using.
    text: Elimina los objetos Document y sale del bloque using.
  - name: Imprime un mensaje de confirmación indicando que la comparación ha finalizado
      y dónde se guardó el PDF de diferencias.
    text: Imprime un mensaje de confirmación indicando que la comparación ha finalizado
      y dónde se guardó el PDF de diferencias.
  type: HowTo
- questions:
  - answer: Sí. El código simplemente no agrega rectángulos a la lista `ignoredRects`
      correspondiente, por lo que `ExcludeAreas1`/`ExcludeAreas2` reciben una matriz
      vacía y el comparador procesa toda la página.
    question: ¿Qué ocurre si una página PDF no tiene anotaciones – seguirá funcionando
      la comparación?
  - answer: Establece `ExcludeAreas1` (o `ExcludeAreas2`) con los rectángulos recopilados
      y deja la otra propiedad como una matriz vacía; el comparador ignorará las regiones
      solo en el documento especificado.
    question: ¿Puedo excluir solo las anotaciones de un documento mientras mantengo
      las anotaciones del otro en la diferencia?
  - answer: Los rectángulos superpuestos se fusionan internamente por el comparador,
      por lo que los límites de anotación superpuestos se excluyen de forma segura
      sin contar doble.
    question: ¿Los rectángulos de anotación superpuestos causan algún problema con
      `ExcludeAreas`?
  - answer: Sí, establece `compareOpts.ExcludeTables = true;` – esta bandera funciona
      junto a `ExcludeAreas1`/`ExcludeAreas2` para también excluir regiones de tablas.
    question: ¿Existe una forma de excluir tablas además de anotaciones usando el
      mismo objeto de opciones?
  - answer: El código verifica `if (a != null && a.Rect != null)` antes de agregar
      a la lista, por lo que los rectángulos nulos simplemente se omiten y no se lanza
      ninguna excepción.
    question: ¿Qué pasa si la propiedad `Rect` de una anotación es nula – lanzará
      el código una excepción?
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: Comparar PDFs sin anotaciones
og_description: Ejecuta una diferencia PDF lado a lado que omite todas las marcas de anotación.
og_image_alt: Guía que muestra una comparación PDF lado a lado que excluye regiones de anotación usando Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Comparación PDF lado a lado excluyendo anotaciones con Aspose.Pdf
Este tutorial muestra cómo comparar dos archivos PDF usando Aspose.Pdf for .NET mientras se ignora cualquier contenido de anotación. Extrae los cuadros delimitadores de todas las anotaciones de cada documento, los introduce en SideBySideComparisonOptions y luego ejecuta una comparación lado a lado. El resultado es un PDF de diferencias que resalta solo los cambios que no son anotaciones.

---

{{< tutorial-widget sourcePath="pdf/net/forms-annotations/exclude-annotations" >}}


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

**Q: ¿Qué ocurre si una página PDF no tiene anotaciones – seguirá funcionando la comparación?**  
A: Sí. El código simplemente no agrega rectángulos a la lista `ignoredRects` correspondiente, por lo que `ExcludeAreas1`/`ExcludeAreas2` reciben una matriz vacía y el comparador procesa toda la página.

**Q: ¿Puedo excluir solo las anotaciones de un documento mientras mantengo las anotaciones del otro en la diferencia?**  
A: Establece `ExcludeAreas1` (o `ExcludeAreas2`) con los rectángulos recopilados y deja la otra propiedad como una matriz vacía; el comparador ignorará las regiones solo en el documento especificado.

**Q: ¿Los rectángulos de anotación superpuestos causan algún problema con `ExcludeAreas`?**  
A: Los rectángulos superpuestos se fusionan internamente por el comparador, por lo que los límites de anotación superpuestos se excluyen de forma segura sin contar doble.

**Q: ¿Existe una forma de excluir tablas además de anotaciones usando el mismo objeto de opciones?**  
A: Sí, establece `compareOpts.ExcludeTables = true;` – esta bandera funciona junto a `ExcludeAreas1`/`ExcludeAreas2` para también excluir regiones de tablas.

**Q: ¿Qué pasa si la propiedad `Rect` de una anotación es nula – lanzará el código una excepción?**  
A: El código verifica `if (a != null && a.Rect != null)` antes de agregar a la lista, por lo que los rectángulos nulos simplemente se omiten y no se lanza ninguna excepción.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}