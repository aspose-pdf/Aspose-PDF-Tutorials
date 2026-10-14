---
title: Compare PDFs y genere un documento de diferencias resaltado usando Aspose.PDF for .NET
weight: 101
limit:
description: Aprenda a comparar dos PDFs y crear un PDF de diferencias resaltado con Aspose.PDF for .NET.
keywords: [pdf comparison, Aspose.PDF for .NET, compare pdf files, generate diff pdf, pdf diff highlighting, pdf document comparison]
url: /net/document-manipulation/compare-pdfs/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Aprenda a comparar dos PDFs y crear un PDF de diferencias resaltado
    con Aspose.PDF for .NET.
  headline: Compare PDFs y genere un documento de diferencias resaltado usando Aspose.PDF
    for .NET
  type: TechArticle
- description: Aprenda a comparar dos PDFs y crear un PDF de diferencias resaltado
    con Aspose.PDF for .NET.
  name: Compare PDFs y genere un documento de diferencias resaltado usando Aspose.PDF
    for .NET
  steps:
  - name: Declare las rutas de archivo para los PDFs original, modificado y de salida
      de diferencias.
    text: Declare las rutas de archivo para los PDFs original, modificado y de salida
      de diferencias.
  - name: Verifique que ambos PDFs de entrada existan y abortar con un mensaje de
      error si falta alguno.
    text: Verifique que ambos PDFs de entrada existan y abortar con un mensaje de
      error si falta alguno.
  - name: Cargue los PDFs original y modificado en objetos `Document` dentro de un
      bloque `using`.
    text: Cargue los PDFs original y modificado en objetos `Document` dentro de un
      bloque `using`.
  - name: Cree una instancia de `ComparisonOptions` con la configuración predeterminada
      para la comparación.
    text: Cree una instancia de `ComparisonOptions` con la configuración predeterminada
      para la comparación.
  - name: Ejecute la comparación, generando un PDF de diferencias en `outputPath`
      que resalta las diferencias entre los dos documentos.
    text: Ejecute la comparación, generando un PDF de diferencias en `outputPath`
      que resalta las diferencias entre los dos documentos.
  - name: Imprima un mensaje de confirmación indicando que el PDF de diferencias ha
      sido creado.
    text: Imprima un mensaje de confirmación indicando que el PDF de diferencias ha
      sido creado.
  - name: Cierre el bloque `using`, liberando los objetos `Document` de origen y destino.
    text: Cierre el bloque `using`, liberando los objetos `Document` de origen y destino.
  type: HowTo
- questions:
  - answer: El código verifica `File.Exists` tanto para `originalDocument.pdf` como
      para `modifiedDocument.pdf`; si falta alguno escribe un error en `Console.Error`
      y sale sin crear un PDF de diferencias.
    question: ¿Qué ocurre si uno de los archivos PDF de entrada no existe?
  - answer: No, la versión actual de Aspose.Pdf.Comparison no incluye una bandera
      `TextComparisonOptions` para comparación sin distinción de mayúsculas, por lo
      que los cambios de mayúsculas aparecerán como diferencias en el PDF de diferencias
      generado.
    question: ¿Puedo hacer que la comparación ignore las diferencias de mayúsculas
      y minúsculas en el texto?
  - answer: '`TextPdfComparer.CompareFlatDocuments(sourceDoc, targetDoc, compareOpts,
      outputPath)` ejecuta la comparación usando los `ComparisonOptions` proporcionados
      y escribe las diferencias resaltadas en `diffOutput.pdf`.'
    question: ¿Qué método realiza realmente la comparación de PDF y crea el archivo
      de diferencias?
  - answer: Las sentencias `using` llaman automáticamente a `Dispose` tanto en `sourceDoc`
      como en `targetDoc` cuando el bloque termina, por lo que no se requiere código
      adicional de disposición.
    question: ¿Necesito disponer manualmente de los objetos `Document`?
  type: FAQPage
images:
- /net/document-manipulation/compare-pdfs/og-image.png
og_title: Genere un PDF de diferencias comparando dos PDFs
og_description: Cree un PDF de diferencias resaltado para ver los cambios entre dos documentos usando Aspose.PDF for .NET.
og_image_alt: Guía que muestra cómo comparar dos PDFs y producir un PDF de diferencias que resalta los cambios usando Aspose.PDF for .NET.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Compare PDFs y genere un documento de diferencias resaltado usando Aspose.PDF
Este tutorial demuestra cómo usar Aspose.Pdf.Comparison para comparar dos archivos PDF y producir un PDF de diferencias que resalta claramente las diferencias. Aprenderá cómo cargar los documentos original y modificado, ejecutar la comparación y guardar el archivo de diferencias resultante. El código paso a paso muestra el proceso exacto para generar un informe visual de comparación.

---

{{< tutorial-widget sourcePath="pdf/net/document-manipulation/compare-pdfs" >}}


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

**Q: ¿Qué ocurre si uno de los archivos PDF de entrada no existe?**  
A: El código verifica `File.Exists` tanto para `originalDocument.pdf` como para `modifiedDocument.pdf`; si falta alguno escribe un error en `Console.Error` y sale sin crear un PDF de diferencias.

**Q: ¿Puedo hacer que la comparación ignore las diferencias de mayúsculas y minúsculas en el texto?**  
A: No, la versión actual de Aspose.Pdf.Comparison no incluye una bandera `TextComparisonOptions` para comparación sin distinción de mayúsculas, por lo que los cambios de mayúsculas aparecerán como diferencias en el PDF de diferencias generado.

**Q: ¿Qué método realiza realmente la comparación de PDF y crea el archivo de diferencias?**  
A: `TextPdfComparer.CompareFlatDocuments(sourceDoc, targetDoc, compareOpts, outputPath)` ejecuta la comparación usando los `ComparisonOptions` proporcionados y escribe las diferencias resaltadas en `diffOutput.pdf`.

**Q: ¿Necesito disponer manualmente de los objetos `Document`?**  
A: Las sentencias `using` llaman automáticamente a `Dispose` tanto en `sourceDoc` como en `targetDoc` cuando el bloque termina, por lo que no se requiere código adicional de disposición.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}