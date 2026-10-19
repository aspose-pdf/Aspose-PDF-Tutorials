---
title: Comparar PDFs mientras se ignoran áreas específicas usando Aspose.Pdf para .NET
weight: 201
limit:
description: Aprenda a comparar PDFs lado a lado e ignorar regiones seleccionadas usando Aspose.Pdf para .NET.
keywords: [Aspose.Pdf for .NET, pdf comparison, exclude areas pdf, ignore regions pdf diff, side-by-side pdf comparison, pdf diff highlighting]
url: /net/document-manipulation/exclude-areas/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Aprenda a comparar PDFs lado a lado e ignorar regiones seleccionadas
    usando Aspose.Pdf para .NET.
  headline: Comparar PDFs mientras se ignoran áreas específicas usando Aspose.Pdf
    para .NET
  type: TechArticle
- description: Aprenda a comparar PDFs lado a lado e ignorar regiones seleccionadas
    usando Aspose.Pdf para .NET.
  name: Comparar PDFs mientras se ignoran áreas específicas usando Aspose.Pdf para
    .NET
  steps:
  - name: Defina las rutas de archivo para los dos PDFs de origen y el PDF de diferencias
      de salida.
    text: Defina las rutas de archivo para los dos PDFs de origen y el PDF de diferencias
      de salida.
  - name: Verifique que ambos archivos PDF de origen existan y abortar con un mensaje
      de error si falta alguno.
    text: Verifique que ambos archivos PDF de origen existan y abortar con un mensaje
      de error si falta alguno.
  - name: Cree una matriz que contenga el área rectangular que se debe ignorar en
      el primer PDF.
    text: Cree una matriz que contenga el área rectangular que se debe ignorar en
      el primer PDF.
  - name: Cree una matriz que contenga el área rectangular que se debe ignorar en
      el segundo PDF.
    text: Cree una matriz que contenga el área rectangular que se debe ignorar en
      el segundo PDF.
  - name: Configure la comparación lado a lado, asignando las matrices de áreas a
      ignorar a las propiedades correspondientes.
    text: Configure la comparación lado a lado, asignando las matrices de áreas a
      ignorar a las propiedades correspondientes.
  - name: Cargue ambos PDFs y ejecute la comparación lado a lado, generando el archivo
      de diferencias en la ruta especificada.
    text: Cargue ambos PDFs y ejecute la comparación lado a lado, generando el archivo
      de diferencias en la ruta especificada.
  - name: Imprima un mensaje de confirmación que indique que la comparación ha finalizado
      y dónde se guardó el PDF de diferencias.
    text: Imprima un mensaje de confirmación que indique que la comparación ha finalizado
      y dónde se guardó el PDF de diferencias.
  type: HowTo
- questions:
  - answer: Las coordenadas están en puntos (1/72 de pulgada) con el origen en la
      esquina inferior izquierda de la página, por lo que los dos primeros números
      son X/Y inferior izquierdo y los dos últimos son X/Y superior derecho.
    question: ¿Qué sistema de coordenadas usan los valores de `Rectangle` al definir
      zonas a ignorar?
  - answer: 'Sí: proporcione varios objetos `Aspose.Pdf.Rectangle` en la matriz `ExcludeAreas1`
      (o `ExcludeAreas2`); cada rectángulo se excluirá de forma independiente durante
      la comparación.'
    question: ¿Puedo ignorar más de una área rectangular en el mismo documento?
  - answer: No. `ExcludeAreas1` se aplica al primer PDF y `ExcludeAreas2` al segundo,
      por lo que puede especificar coordenadas diferentes para cada documento.
    question: ¿Los rectángulos a ignorar deben ser idénticos en ambos PDFs?
  - answer: Aspose.Pdf ignora silenciosamente los rectángulos que quedan completamente
      fuera de la página; no tienen efecto en el resultado de la comparación.
    question: ¿Qué ocurre si un rectángulo se define fuera de los límites de la página?
  - answer: Las matrices `ExcludeAreas` se aplican por página, por lo que debe agregar
      el mismo `Rectangle` a la colección de cada página (p. ej., iterar sobre `pdf.Pages`
      y asignar la matriz) antes de llamar a `SideBySidePdfComparer.Compare`.
    question: ¿Cómo puedo excluir la misma región en cada página de un PDF?
  type: FAQPage
images:
- /net/document-manipulation/exclude-areas/og-image.png
og_title: Ignorar regiones al comparar PDFs
og_description: Vea cómo omitir áreas seleccionadas en una comparación PDF lado a lado y obtener un PDF de diferencias limpio.
og_image_alt: Guía que muestra la comparación PDF lado a lado con regiones rectangulares excluidas usando Aspose.Pdf para .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Comparar PDFs mientras se ignoran áreas específicas usando Aspose.Pdf para .NET
Este tutorial demuestra cómo comparar dos documentos PDF lado a lado con Aspose.Pdf para .NET mientras se excluyen regiones rectangulares designadas del análisis. Al definir áreas de exclusión en cada archivo, el PDF de diferencias generado resalta solo los cambios que importan, facilitando la concentración en las diferencias relevantes.

---

{{< tutorial-widget sourcePath="pdf/net/document-manipulation/exclude-areas" >}}


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

**Q: ¿Qué sistema de coordenadas usan los valores de `Rectangle` al definir zonas a ignorar?**  
A: Las coordenadas están en puntos (1/72 de pulgada) con el origen en la esquina inferior izquierda de la página, por lo que los dos primeros números son X/Y inferior izquierdo y los dos últimos son X/Y superior derecho.

**Q: ¿Puedo ignorar más de una área rectangular en el mismo documento?**  
A: Sí: proporcione varios objetos `Aspose.Pdf.Rectangle` en la matriz `ExcludeAreas1` (o `ExcludeAreas2`); cada rectángulo se excluirá de forma independiente durante la comparación.

**Q: ¿Los rectángulos a ignorar deben ser idénticos en ambos PDFs?**  
A: No. `ExcludeAreas1` se aplica al primer PDF y `ExcludeAreas2` al segundo, por lo que puede especificar coordenadas diferentes para cada documento.

**Q: ¿Qué ocurre si un rectángulo se define fuera de los límites de la página?**  
A: Aspose.Pdf ignora silenciosamente los rectángulos que quedan completamente fuera de la página; no tienen efecto en el resultado de la comparación.

**Q: ¿Cómo puedo excluir la misma región en cada página de un PDF?**  
A: Las matrices `ExcludeAreas` se aplican por página, por lo que debe agregar el mismo `Rectangle` a la colección de cada página (p. ej., iterar sobre `pdf.Pages` y asignar la matriz) antes de llamar a `SideBySidePdfComparer.Compare`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}