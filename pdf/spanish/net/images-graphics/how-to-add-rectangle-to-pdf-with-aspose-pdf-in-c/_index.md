---
category: general
date: 2026-10-10
description: Aprende cómo agregar un rectángulo a un PDF, dibujar una forma en un
  PDF y guardar el PDF modificado usando Aspose.PDF. Incluye una guía paso a paso
  para acceder a una página PDF específica.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to PDF
- draw shape on PDF
- save modified PDF
- add shape to PDF
- access specific PDF page
language: es
lastmod: 2026-10-10
og_description: Añadir un rectángulo a un PDF usando Aspose.PDF en C#. Este tutorial
  muestra cómo dibujar una forma en un PDF, acceder a una página específica del PDF
  y guardar el PDF modificado.
og_image_alt: Screenshot of a PDF page with a blue rectangle overlay created by Aspose.PDF
og_title: Agregar rectángulo a PDF con Aspose.PDF – guía completa de C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  headline: How to add rectangle to PDF with Aspose.PDF in C#
  type: TechArticle
- description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  name: How to add rectangle to PDF with Aspose.PDF in C#
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: What if the PDF has only one page?
    text: Attempting to access `pdfDocument.Pages[1]` throws an `ArgumentOutOfRangeException`.
      Guard against this by checking `pdfDocument.Pages.Count` before indexing.
  - name: How to add multiple rectangles on different pages?
    text: Repeat Steps 2‑4 for each target page, adjusting the rectangle’s coordinates
      as needed. You can place the logic inside a loop that iterates over `pdfDocument.Pages`.
  - name: Can I use other shapes such as circles or polygons?
    text: Yes. Aspose.PDF provides `Ellipse`, `Polygon`, and `Polyline` classes that
      follow the same pattern as `Rectangle`. Replace the `new Aspose.Pdf.Drawing.Rectangle`
      call with the desired shape class.
  - name: Does the library support PDFs with rotated pages?
    text: Aspose.PDF automatically respects page rotation when rendering shapes. The
      rectangle’s coordinates are interpreted in the page’s native coordinate system,
      so no extra transformation is required.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Cómo añadir un rectángulo a un PDF con Aspose.PDF en C#
url: /es/net/images-graphics/how-to-add-rectangle-to-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo agregar un rectángulo a PDF con Aspose.PDF en C#

Si necesitas **agregar un rectángulo a PDF** de forma programática, esta guía te muestra exactamente cómo hacerlo. Aprenderás a **dibujar una forma en PDF**, a seleccionar una página concreta y a **guardar el PDF modificado** sin errores.

Trabajar con documentos PDF es un requisito frecuente para informes, facturación o anotación de documentos. Al finalizar este tutorial podrás **agregar una forma a PDF** con confianza, manejar errores de fuera de límites y integrar la solución en cualquier proyecto .NET.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* SDK de .NET 6.0 o posterior instalado  
* Visual Studio 2022 (o cualquier IDE de C#)  
* Una licencia de Aspose.PDF para .NET o una clave de evaluación gratuita – la API funciona de la misma manera en ambos modos  
* Un archivo PDF llamado `input.pdf` ubicado en una carpeta a la que puedas referenciar desde tu código  

Estos elementos son las únicas dependencias externas del ejemplo.

## Paso 1: Instalar el paquete NuGet Aspose.PDF

La biblioteca Aspose.PDF proporciona las clases `Document`, `Rectangle` y otras clases de dibujo que necesitas.

```bash
dotnet add package Aspose.PDF
```

Ejecutar este comando agrega la última versión estable de Aspose.PDF a tu proyecto, poniendo a disposición las clases PDF para la compilación.

## Paso 2: Cargar el documento PDF

La primera operación es cargar el archivo fuente. Esto crea una representación en memoria que puedes modificar.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;

class PdfRectangleExample
{
    static void Main()
    {
        // Load the PDF document from disk
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

*Por qué es importante*: Cargar el documento te da acceso a su colección de páginas, lo cual es necesario para **acceder a una página PDF específica** más adelante.

## Paso 3: Acceder a la segunda página (índice base 0)

Las páginas PDF están indexadas desde `0`. Para colocar un rectángulo en la segunda página, recupera la página en el índice `1`.

```csharp
        // Access the second page (pages are zero‑based)
        var page = pdfDocument.Pages[1];
```

Si el documento tiene menos de dos páginas, se lanzará una `ArgumentOutOfRangeException`, lo que te alerta sobre la necesidad de una cláusula de protección en código de producción.

## Paso 4: Crear la forma rectángulo

Define la posición y el tamaño del rectángulo usando la estructura `Rectangle`, y luego envuélvelo en un objeto de dibujo de Aspose.

```csharp
        // Define rectangle bounds: (x, y, width, height)
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            // Optional visual styling
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };
```

*Por qué es importante*: Las propiedades `BorderInfo` y `FillColor` te permiten **dibujar una forma en PDF** con un contorno visible y un relleno opcional, haciendo que el rectángulo destaque para los lectores.

## Paso 5: Añadir el rectángulo a la colección de párrafos de la página

Aspose.PDF trata los objetos de dibujo como elementos de párrafo. Añadir el rectángulo a la colección `Paragraphs` de la página lo renderiza en la misma.

```csharp
        // Add the rectangle shape to the page
        page.Paragraphs.Add(rectangleShape);
```

En este punto el documento PDF en memoria contiene la nueva forma, pero el archivo en disco permanece sin cambios hasta que lo guardes.

## Paso 6: Guardar el PDF modificado y manejar errores de fuera de límites

Llamar a `Save` escribe el documento actualizado en un nuevo archivo. Si el rectángulo supera las dimensiones de la página, Aspose lanza una `PdfException`. Capturar esta excepción te permite informar del problema de forma limpia.

```csharp
        try
        {
            // Save the altered PDF to a new file
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            // Handle shape that does not fit on the page
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

*Por qué es importante*: El bloque `try/catch` asegura que tu aplicación **guarde el PDF modificado** de forma segura, y el mensaje de error te ayuda a ajustar las coordenadas del rectángulo si es necesario.

## Ejemplo completo funcional

Uniendo todos los pasos, aquí tienes el programa completo listo para ejecutar:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;
using System.Drawing; // Required for Color

class PdfRectangleExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // Step 2: Access the second page (zero‑based)
        var page = pdfDocument.Pages[1];

        // Step 3: Create a rectangle shape positioned at (100,100) with width 300 and height 200
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };

        // Step 4: Add the rectangle shape to the page's paragraph collection
        page.Paragraphs.Add(rectangleShape);

        // Step 5: Save the modified PDF, handling out‑of‑bounds cases
        try
        {
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

### Salida esperada

Al ejecutar el programa se imprime:

```
PDF saved successfully with rectangle added.
```

y se crea `output.pdf` que muestra el contenido original más un rectángulo azul en las coordenadas especificadas de la segunda página.

Si el rectángulo fuera más grande que la página, verías:

```
Shape out of bounds: The shape exceeds page margins.
```

## Preguntas frecuentes y casos límite

### ¿Qué pasa si el PDF tiene solo una página?

Intentar acceder a `pdfDocument.Pages[1]` lanza una `ArgumentOutOfRangeException`. Evita esto verificando `pdfDocument.Pages.Count` antes de indexar.

```csharp
if (pdfDocument.Pages.Count < 2)
{
    Console.WriteLine("Document does not contain a second page.");
    return;
}
```

### ¿Cómo agregar varios rectángulos en diferentes páginas?

Repite los Pasos 2‑4 para cada página objetivo, ajustando las coordenadas del rectángulo según sea necesario. Puedes colocar la lógica dentro de un bucle que itere sobre `pdfDocument.Pages`.

### ¿Puedo usar otras formas como círculos o polígonos?

Sí. Aspose.PDF proporciona las clases `Ellipse`, `Polygon` y `Polyline` que siguen el mismo patrón que `Rectangle`. Sustituye la llamada `new Aspose.Pdf.Drawing.Rectangle` por la clase de forma deseada.

### ¿La biblioteca soporta PDFs con páginas rotadas?

Aspose.PDF respeta automáticamente la rotación de la página al renderizar formas. Las coordenadas del rectángulo se interpretan en el sistema de coordenadas nativo de la página, por lo que no se requiere una transformación adicional.

## Consideraciones de rendimiento

* **Uso de memoria** – Cargar un PDF grande (cientos de megabytes) consume memoria proporcional. Si solo necesitas modificar una página, considera usar `PdfFileInfo` para extraer esa página, modificarla y luego volver a combinarla.  
* **Procesamiento por lotes** – Al agregar formas a muchos documentos, reutiliza una única instancia de `License` para evitar la sobrecarga de validar la licencia repetidamente.

## Próximos pasos

Ahora que puedes **agregar un rectángulo a PDF**, explora estos temas relacionados:

* **draw shape on PDF** – aprende a superponer texto, imágenes y marcas de agua  
* **add shape to PDF** – combina múltiples formas en una sola capa de anotación  
* **save modified PDF** – usa streams (`MemoryStream`) para devolver PDFs directamente desde APIs web  
* **access specific PDF page** – implementa extracción de rangos de páginas para informes personalizados  

Experimenta con diferentes colores, estilos de línea y niveles de transparencia para que coincidan con las directrices de tu marca.

---

*¡Feliz codificación! Si este tutorial te ayudó a **agregar un rectángulo a PDF**, considera compartirlo con tus compañeros o contribuir con mejoras a la comunidad.*

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide](/pdf/english/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [How to Add a Line Object in PDF Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}