---
title: Personalizar el fondo, bordes y relleno de celdas de tabla en PDFs con Aspose.Pdf for .NET
weight: 101
limit:
description: Aprende cómo crear un PDF con una tabla de dos columnas y aplicar colores de fondo personalizados, bordes y relleno a cada celda usando Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, style table cells pdf, pdf table cell background, pdf table cell border, pdf cell padding, Aspose PDF table styling]
url: /net/tables-lists/style-table-cells/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Aprende cómo crear un PDF con una tabla de dos columnas y aplicar colores
    de fondo personalizados, bordes y relleno a cada celda usando Aspose.Pdf for .NET.
  headline: Personalizar el fondo, bordes y relleno de celdas de tabla en PDFs con
    Aspose.Pdf for .NET
  type: TechArticle
- description: Aprende cómo crear un PDF con una tabla de dos columnas y aplicar colores
    de fondo personalizados, bordes y relleno a cada celda usando Aspose.Pdf for .NET.
  name: Personalizar el fondo, bordes y relleno de celdas de tabla en PDFs con Aspose.Pdf
    for .NET
  steps:
  - name: Crear un nuevo documento PDF vacío dentro de un bloque using.
    text: Crear un nuevo documento PDF vacío dentro de un bloque using.
  - name: Añadir una página en blanco al documento PDF.
    text: Añadir una página en blanco al documento PDF.
  - name: Instanciar un objeto Table con dos columnas de 200 puntos, un borde exterior
      negro delgado y un relleno de celda predeterminado de 5 puntos.
    text: Instanciar un objeto Table con dos columnas de 200 puntos, un borde exterior
      negro delgado y un relleno de celda predeterminado de 5 puntos.
  - name: Añadir la primera fila a la tabla.
    text: Añadir la primera fila a la tabla.
  - name: Crear la primera celda, insertar el texto "First cell", establecer un fondo
      amarillo claro, un borde rojo de 2 puntos y un margen de 4 puntos.
    text: Crear la primera celda, insertar el texto "First cell", establecer un fondo
      amarillo claro, un borde rojo de 2 puntos y un margen de 4 puntos.
  - name: Crear la segunda celda, añadir el texto "Second cell", darle un fondo verde
      claro, un borde azul de 2 puntos y un margen de 4 puntos.
    text: Crear la segunda celda, añadir el texto "Second cell", darle un fondo verde
      claro, un borde azul de 2 puntos y un margen de 4 puntos.
  - name: Añadir la segunda fila a la tabla.
    text: Añadir la segunda fila a la tabla.
  - name: Crear la tercera celda, insertar "Third cell", establecer un fondo cian
      claro, un borde gris oscuro de 2 puntos y un margen de 4 puntos.
    text: Crear la tercera celda, insertar "Third cell", establecer un fondo cian
      claro, un borde gris oscuro de 2 puntos y un margen de 4 puntos.
  - name: Crear la cuarta celda, añadir "Fourth cell", darle un fondo rosa claro,
      un borde púrpura de 2 puntos y un margen de 4 puntos.
    text: Crear la cuarta celda, añadir "Fourth cell", darle un fondo rosa claro,
      un borde púrpura de 2 puntos y un margen de 4 puntos.
  - name: Añadir la tabla completamente estilizada a la página para que sea visible
      en el PDF.
    text: Añadir la tabla completamente estilizada a la página para que sea visible
      en el PDF.
  - name: Guardar el documento PDF en un archivo y cerrar el bloque using.
    text: Guardar el documento PDF en un archivo y cerrar el bloque using.
  - name: Imprimir un mensaje de confirmación en la consola.
    text: Imprimir un mensaje de confirmación en la consola.
  type: HowTo
- questions:
  - answer: '`DefaultCellPadding` proporciona un relleno base para cada celda, pero
      si asignas un `Margin` (p. ej., `cellA1.Margin = new MarginInfo(...)`) los valores
      del margen sobrescriben el relleno predeterminado para esa celda específica.'
    question: ¿El `DefaultCellPadding` establecido en el `Table` afecta a las celdas
      que también tienen un `Margin` definido?
  - answer: Sin `Table.Border`, se omite el rectángulo exterior que rodea toda la
      tabla; solo serán visibles los bordes individuales de las celdas que establezcas
      (p. ej., `cellA2.Border`).
    question: ¿Cómo quedará el PDF si elimino la propiedad `Border` del objeto `Table`?
  - answer: Sí, crea un `BorderInfo` con un `BorderSide` específico (p. ej., `new
      BorderInfo(BorderSide.Left, 3, Aspose.Pdf.Color.Black)`) y asígnalo a la propiedad
      `Border` de la celda.
    question: ¿Puedo dar a una celda un ancho de borde diferente en cada lado?
  - answer: Instancia una nueva `Row` con `Row newRow = dataTable.Rows.Add();` y luego
      agrega celdas a `newRow.Cells` como en las filas anteriores.
    question: ¿Cómo añado una tercera fila a la tabla después del código mostrado?
  type: FAQPage
images:
- /net/tables-lists/style-table-cells/og-image.png
og_title: Estilizar celdas de tabla PDF – Fondo, borde, relleno
og_description: Formatea rápidamente celdas de tabla en un PDF con colores, bordes y espaciado personalizados usando Aspose.Pdf for .NET.
og_image_alt: Guía que muestra cómo dar estilo al color de fondo, borde y relleno de celdas de tabla en un PDF usando Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Personalizar el fondo, bordes y relleno de celdas de tabla en PDFs con Aspose.Pdf
En este tutorial verás cómo generar un documento PDF, añadir una tabla de dos columnas y controlar con precisión la apariencia de cada celda. Al establecer colores de fondo, definir bordes y ajustar el relleno, puedes hacer que los datos de la tabla destaquen y tengan un aspecto pulido. El ejemplo usa las clases Aspose.Pdf Document y Table para demostrar cada opción de estilo.

---

{{< tutorial-widget sourcePath="pdf/net/tables-lists/style-table-cells" >}}


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

**Q: ¿El `DefaultCellPadding` establecido en el `Table` afecta a las celdas que también tienen un `Margin` definido?**  
A: `DefaultCellPadding` proporciona un relleno base para cada celda, pero si asignas un `Margin` (p. ej., `cellA1.Margin = new MarginInfo(...)`) los valores del margen sobrescriben el relleno predeterminado para esa celda específica.

**Q: ¿Cómo quedará el PDF si elimino la propiedad `Border` del objeto `Table`?**  
A: Sin `Table.Border`, se omite el rectángulo exterior que rodea toda la tabla; solo serán visibles los bordes individuales de las celdas que establezcas (p. ej., `cellA2.Border`).

**Q: ¿Puedo dar a una celda un ancho de borde diferente en cada lado?**  
A: Sí, crea un `BorderInfo` con un `BorderSide` específico (p. ej., `new BorderInfo(BorderSide.Left, 3, Aspose.Pdf.Color.Black)`) y asígnalo a la propiedad `Border` de la celda.

**Q: ¿Cómo añado una tercera fila a la tabla después del código mostrado?**  
A: Instancia una nueva `Row` con `Row newRow = dataTable.Rows.Add();` y luego agrega celdas a `newRow.Cells` como en las filas anteriores.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}