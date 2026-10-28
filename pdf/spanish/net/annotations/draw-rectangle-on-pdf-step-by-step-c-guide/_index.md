---
category: general
date: 2026-08-14
description: Dibuja un rectángulo en PDF rápidamente usando C#. Aprende a definir
  las dimensiones del rectángulo y a añadir formas a una página PDF en solo unas pocas
  líneas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- draw rectangle on pdf
- how to define rectangle dimensions
language: es
lastmod: 2026-08-14
og_description: dibujar rectángulo en pdf con C# en segundos. Esta guía muestra cómo
  definir las dimensiones del rectángulo, agregar una forma y verificar los límites
  de la página para obtener gráficos PDF confiables.
og_image_alt: Screenshot of a PDF page showing a black rectangle drawn with C# code
og_title: dibujar rectángulo en pdf – tutorial completo de C#
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: draw rectangle on pdf quickly using C#. Learn how to define rectangle
    dimensions and add shapes to a PDF page in just a few lines.
  headline: draw rectangle on pdf – step‑by‑step C# guide
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
- RectangleShape
- Graphics
title: Dibujar un rectángulo en PDF – guía paso a paso en C#
url: /es/net/annotations/draw-rectangle-on-pdf-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# dibujar rectángulo en pdf – tutorial completo de C#

Si necesitas **dibujar rectángulo en pdf** usando C#, esta guía te muestra una solución concisa y lista para producción. Verás exactamente **cómo definir dimensiones del rectángulo**, verificar que la forma encaje y añadirla a una página con una única llamada de método.

El tutorial cubre todo, desde crear un documento PDF hasta renderizar el rectángulo, para que puedas copiar‑pegar el código en tu propio proyecto y ver los resultados al instante. No se requiere documentación externa, solo los pasos a continuación.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* .NET 6.0 o posterior (el código también funciona con .NET Framework 4.7+)
* El paquete NuGet **Aspose.PDF for .NET** (`Install-Package Aspose.PDF`)
* Un conocimiento básico de la sintaxis de C#
* Un IDE como Visual Studio o VS Code

> **Consejo profesional:** Usa la licencia de evaluación gratuita de Aspose.PDF para experimentos rápidos; añade una pequeña marca de agua pero te permite probar todas las funciones.

## Cómo dibujar rectángulo en PDF con C#

El núcleo de la tarea es crear un `RectangleShape`, establecer su tamaño y trazo, y adjuntarlo a una `Page`. El siguiente encabezado H2 contiene la palabra clave principal, cumpliendo con los requisitos SEO.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        Document pdfDoc = new Document();

        // 2️⃣ Add a blank page (default size: A4)
        Page page = pdfDoc.Pages.Add();

        // 3️⃣ Define the rectangle bounds (x, y, width, height)
        //    This demonstrates how to define rectangle dimensions.
        Rectangle rectBounds = new Rectangle(0, 0, 500, 700);

        // 4️⃣ Create the rectangle shape and set its stroke color
        RectangleShape rectangleShape = new RectangleShape(rectBounds)
        {
            StrokeColor = Color.Black   // black outline
        };

        // 5️⃣ Verify that the shape fits within the page boundaries
        page.CheckShapeBoundary(rectangleShape);

        // 6️⃣ Add the shape to the page
        page.Add(rectangleShape);

        // 7️⃣ Save the PDF to disk
        string outPath = "RectangleDemo.pdf";
        pdfDoc.Save(outPath);
        Console.WriteLine($"PDF saved to {outPath}");
    }
}
```

### Explicación de cada paso

| Paso | Por qué es importante |
|------|-----------------------|
| **1️⃣ Crear un nuevo documento PDF** | Inicializa el contenedor que alojará páginas y gráficos. |
| **2️⃣ Añadir una página en blanco** | Necesitas un objeto `Page` porque las formas se adjuntan a una página, no directamente al documento. |
| **3️⃣ Definir los límites del rectángulo** | Aquí es donde **cómo definir dimensiones del rectángulo**. El constructor `Rectangle` recibe `x`, `y`, `width` y `height` en puntos (1 pt = 1/72 in). |
| **4️⃣ Crear la forma del rectángulo** | `RectangleShape` es la clase de Aspose que renderiza un rectángulo. Establecer `StrokeColor` define el contorno; también podrías establecer `FillColor` para un relleno sólido. |
| **5️⃣ Verificar los límites de la página** | `CheckShapeBoundary` lanza una excepción si el rectángulo supera el tamaño de la página, evitando PDFs malformados. |
| **6️⃣ Añadir la forma a la página** | La forma pasa a ser parte del flujo de contenido de la página. |
| **7️⃣ Guardar el PDF** | Persiste el documento en un archivo que puedes abrir con cualquier visor de PDF. |

El `RectangleDemo.pdf` resultante contiene un rectángulo negro ubicado en la esquina superior izquierda de la página, con exactamente 500 pt de ancho y 700 pt de alto.

![dibujar rectángulo en pdf ejemplo](https://example.com/rectangle-demo.png "dibujar rectángulo en pdf ejemplo")

*Texto alternativo de la imagen: dibujar rectángulo en pdf ejemplo que muestra un rectángulo negro en la esquina superior izquierda de una página PDF.*

## Cómo definir dimensiones del rectángulo para diferentes tamaños de página

El fragmento anterior usa valores fijos (`500 x 700`). En aplicaciones reales a menudo necesitas que el rectángulo se adapte al ancho y alto de la página.

```csharp
// Get page dimensions (in points)
float pageWidth = page.PageInfo.Width;
float pageHeight = page.PageInfo.Height;

// Define a rectangle that occupies 80% of the page width and 50% of the height
float rectWidth  = pageWidth * 0.8f;
float rectHeight = pageHeight * 0.5f;

// Center the rectangle on the page
float rectX = (pageWidth - rectWidth) / 2;
float rectY = (pageHeight - rectHeight) / 2;

Rectangle dynamicRect = new Rectangle(rectX, rectY, rectWidth, rectHeight);
RectangleShape dynamicShape = new RectangleShape(dynamicRect)
{
    StrokeColor = Color.DarkBlue,
    FillColor   = Color.LightGray   // optional fill
};

page.CheckShapeBoundary(dynamicShape);
page.Add(dynamicShape);
```

**Puntos clave:**

* Usa `page.PageInfo.Width` y `Height` para leer el tamaño real de la página.
* Multiplicar por un factor (p. ej., `0.8f`) te permite expresar dimensiones como porcentaje de la página.
* Centrar se logra restando el tamaño del rectángulo al tamaño de la página y dividiendo el resto entre dos.

## Problemas comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| El rectángulo se extiende más allá de la página | Dimensiones codificadas que son mayores que el tamaño de la página. | Llama a `page.CheckShapeBoundary` **antes** de añadir la forma; ajusta las dimensiones si se lanza una excepción. |
| El trazo no es visible | `StrokeColor` dejado en su valor predeterminado (`Color.Empty`). | Establece explícitamente `StrokeColor` (p. ej., `Color.Black`). |
| El rectángulo aparece fuera de la pantalla | Las coordenadas comienzan en la esquina inferior izquierda en el espacio PDF; usar coordenadas estilo pantalla (superior izquierda) provoca un volteo. | Recuerda que el origen `(0,0)` está en la esquina inferior izquierda. Ajusta `y` en consecuencia o usa `pageHeight - desiredY`. |
| Grosor de línea inesperado | El ancho de línea predeterminado puede ser demasiado fino para impresión. | Configura `rectangleShape.LineWidth = 2;` para aumentar el grosor. |

## Extender el ejemplo

Una vez que puedas **dibujar rectángulo en pdf**, puedes añadir fácilmente otras formas:

* **EllipseShape** – para círculos u óvalos.
* **PolygonShape** – para polígonos personalizados.
* **TextFragment** – para etiquetar tus rectángulos.

Todas las formas comparten el mismo flujo de trabajo: definir límites, configurar apariencia, verificar límites y luego añadir a la página.

## Programa completo y ejecutable

A continuación tienes el programa completo que combina el rectángulo básico y el ejemplo de dimensionado dinámico. Cópialo en un nuevo proyecto de consola, restaura el paquete NuGet `Aspose.PDF` y ejecútalo.

```csharp
using System;
using System.Drawing;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class RectangleDemo
{
    static void Main()
    {
        // Create document and page
        Document doc = new Document();
        Page page = doc.Pages.Add();

        // ==== Fixed‑size rectangle (basic example) ====
        Rectangle fixedRect = new Rectangle(0, 0, 500, 700);
        RectangleShape fixedShape = new RectangleShape(fixedRect)
        {
            StrokeColor = Color.Black,
            LineWidth   = 1
        };
        page.CheckShapeBoundary(fixedShape);
        page.Add(fixedShape);

        // ==== Dynamic rectangle that adapts to page size ====
        float pageW = page.PageInfo.Width;
        float pageH = page.PageInfo.Height;

        float dynWidth  = pageW * 0.6f;
        float dynHeight = pageH * 0.3f;
        float dynX      = (pageW - dynWidth) / 2;
        float dynY      = (pageH - dynHeight) / 2;

        Rectangle dynamicRect = new Rectangle(dynX, dynY, dynWidth, dynHeight);
        RectangleShape dynamicShape = new RectangleShape(dynamicRect)
        {
            StrokeColor = Color.DarkBlue,
            FillColor   = Color.LightYellow,
            LineWidth   = 2
        };
        page.CheckShapeBoundary(dynamicShape);
        page.Add(dynamicShape);

        // Save PDF
        string outFile = "CombinedRectangles.pdf";
        doc.Save(outFile);
        Console.WriteLine($"PDF created: {outFile}");
    }
}
```

**Salida esperada:**  
Abre `CombinedRectangles.pdf`. Verás un rectángulo negro anclado en la esquina inferior izquierda y un rectángulo azul oscuro centrado con relleno amarillo claro. Ambos rectángulos respetan los márgenes de la página.

## Conclusión

Ahora sabes cómo **dibujar rectángulo en pdf** con C# y, con precisión, **cómo definir dimensiones del rectángulo** tanto para diseños fijos como responsivos. El enfoque utiliza `RectangleShape` de Aspose.PDF, verificación de límites y aritmética sencilla para adaptarse a cualquier tamaño de página.

A continuación, podrías explorar:

* Añadir **colores de relleno** y **estilos de línea** (discontinuo, punteado) – palabra clave secundaria: cómo definir dimensiones del rectángulo con estilo.
* Combinar múltiples formas en una sola `Page` para crear gráficos o formularios.
* Exportar el PDF a un stream para APIs web en lugar de guardarlo en disco.

Experimenta con diferentes tamaños, colores y posiciones para dominar los gráficos PDF en tus aplicaciones .NET. ¡Feliz codificación!


## ¿Qué deberías aprender a continuación?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye código completo y ejemplos funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo personalizar PDFs con Aspose.PDF para .NET: establecer márgenes de página y dibujar líneas](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [Cómo añadir sellos de página en PDFs usando Aspose.PDF para .NET: guía completa](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Cómo añadir sellos de número de página en PDFs usando Aspose.PDF para .NET | Marcas de agua y fondos](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}