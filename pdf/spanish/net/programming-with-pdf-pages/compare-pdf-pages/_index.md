---
title: Compare páginas PDF página por página con Aspose.Pdf for .NET
weight: 360
limit:
description: Aprenda a comparar dos PDFs página por página y crear un informe de diferencias usando Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, pdf page comparison, textpdfcomparer, pdf diff report, compare pdf documents, page by page pdf diff]
url: /net/programming-with-pdf-pages/compare-pdf-pages/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Aprenda a comparar dos PDFs página por página y crear un informe de
    diferencias usando Aspose.Pdf for .NET.
  headline: Compare páginas PDF página por página con Aspose.Pdf for .NET
  type: TechArticle
- description: Aprenda a comparar dos PDFs página por página y crear un informe de
    diferencias usando Aspose.Pdf for .NET.
  name: Compare páginas PDF página por página con Aspose.Pdf for .NET
  steps:
  - name: Declare las rutas de archivo para el PDF original, el PDF revisado y el
      informe de diferencias de salida.
    text: Declare las rutas de archivo para el PDF original, el PDF revisado y el
      informe de diferencias de salida.
  - name: Verifique que ambos PDFs de origen existan y abortar con un mensaje de error
      si falta alguno.
    text: Verifique que ambos PDFs de origen existan y abortar con un mensaje de error
      si falta alguno.
  - name: Abra ambos PDFs, cree opciones de comparación predeterminadas, ejecute una
      diferencia página por página con `TextPdfComparer.CompareDocumentsPageByPage`
      y muestre un mensaje de éxito.
    text: Abra ambos PDFs, cree opciones de comparación predeterminadas, ejecute una
      diferencia página por página con `TextPdfComparer.CompareDocumentsPageByPage`
      y muestre un mensaje de éxito.
  - name: Capture cualquier excepción lanzada durante la comparación y escriba un
      mensaje de error en la consola.
    text: Capture cualquier excepción lanzada durante la comparación y escriba un
      mensaje de error en la consola.
  type: HowTo
- questions:
  - answer: TextPdfComparer.CompareDocumentsPageByPage compara las páginas de forma
      pareada hasta el documento más corto; cualquier página restante en el PDF más
      largo se trata como secciones añadidas o eliminadas y se incluyen en el informe
      de diferencias.
    question: ¿Qué ocurre si los dos PDFs tienen un número diferente de páginas?
  - answer: Cree una instancia de ComparisonOptions y establezca sus propiedades de
      estilo visual (p. ej., HighlightColor, InsertedTextColor, DeletedTextColor)
      antes de pasarla a CompareDocumentsPageByPage.
    question: ¿Cómo puedo cambiar los colores de resaltado u otros aspectos visuales
      del informe de diferencias?
  - answer: El ejemplo verifica la existencia del archivo en relación al directorio
      de trabajo actual; asegúrese de que las rutas sean absolutas o de que la carpeta
      de trabajo del ejecutable contenga los PDFs, de lo contrario la verificación
      fallará.
    question: Obtengo un error “Archivo no encontrado” aunque los archivos PDF existen
      – ¿qué está mal?
  - answer: Sí, pero debe cargar cada Document con un objeto LoadOptions que incluya
      la contraseña (p. ej., `new Document(path, new LoadOptions { Password = "pwd"
      })`) antes de llamar al comparador.
    question: ¿Puedo comparar PDFs protegidos con contraseña con este código?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/compare-pdf-pages/og-image.png
og_title: Genere un informe de diferencias PDF página por página
og_description: Vea exactamente qué cambió entre dos PDFs con una rápida diferencia página por página.
og_image_alt: Guía que muestra cómo comparar páginas PDF lado a lado y producir un informe de diferencias usando Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Compare páginas PDF página por página con Aspose.Pdf
Este tutorial muestra cómo usar el TextPdfComparer de Aspose.Pdf para realizar una comparación página por página de dos documentos PDF. Aprenderá a detectar diferencias en cada página y a generar un PDF de informe de diferencias que resalta esos cambios. El ejemplo recorre la carga de los PDFs de origen, la ejecución de la comparación y el guardado del informe resultante.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/compare-pdf-pages" >}}


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

**Q: ¿Qué ocurre si los dos PDFs tienen un número diferente de páginas?**  
A: TextPdfComparer.CompareDocumentsPageByPage compara las páginas de forma pareada hasta el documento más corto; cualquier página restante en el PDF más largo se trata como secciones añadidas o eliminadas y se incluyen en el informe de diferencias.

**Q: ¿Cómo puedo cambiar los colores de resaltado u otros aspectos visuales del informe de diferencias?**  
A: Cree una instancia de ComparisonOptions y establezca sus propiedades de estilo visual (p. ej., HighlightColor, InsertedTextColor, DeletedTextColor) antes de pasarla a CompareDocumentsPageByPage.

**Q: Obtengo un error “Archivo no encontrado” aunque los archivos PDF existen – ¿qué está mal?**  
A: El ejemplo verifica la existencia del archivo en relación al directorio de trabajo actual; asegúrese de que las rutas sean absolutas o de que la carpeta de trabajo del ejecutable contenga los PDFs, de lo contrario la verificación fallará.

**Q: ¿Puedo comparar PDFs protegidos con contraseña con este código?**  
A: Sí, pero debe cargar cada Document con un objeto LoadOptions que incluya la contraseña (p. ej., `new Document(path, new LoadOptions { Password = "pwd" })`) antes de llamar al comparador.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}