---
category: general
date: 2026-08-04
description: Agregar rectángulo a PDF usando C#. Aprende cómo dibujar una forma en
  PDF con C# y Aspose.Pdf en un ejemplo claro y completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to pdf
- how to draw shape in pdf c#
language: es
lastmod: 2026-08-04
og_description: Añade un rectángulo a PDF usando C#. Este tutorial muestra cómo dibujar
  formas en PDF con C# de forma rápida y fiable.
og_image_alt: Screenshot of a PDF page with a blue rectangle drawn by C# code
og_title: Agregar un rectángulo a PDF con C# – guía completa de programación
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  headline: Add rectangle to PDF with C# – step‑by‑step guide
  type: TechArticle
- description: Add rectangle to PDF using C#. Learn how to draw shape in PDF C# with
    Aspose.Pdf in a clear, complete example.
  name: Add rectangle to PDF with C# – step‑by‑step guide
  steps:
  - name: '**Create a new console project**'
    text: '**Create a new console project**'
  - name: '**Add the Aspose.Pdf package**'
    text: '**Add the Aspose.Pdf package**'
  - name: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
    text: '**Place `input.pdf`** in the project directory (or any folder you reference
      later).'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Agregar rectángulo a PDF con C# – guía paso a paso
url: /es/net/images-graphics/add-rectangle-to-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Agregar rectángulo a PDF con C# – guía paso a paso

Si necesitas **agregar rectángulo a PDF** desde una aplicación C#, esta guía te muestra exactamente cómo hacerlo. Verás un ejemplo completo y ejecutable que dibuja una forma en PDF C# usando la biblioteca Aspose.Pdf, y comprenderás por qué cada línea de código es importante.

Dibujar formas en PDFs es un requisito común para generadores de informes, plantillas de facturas y personalización de documentos. Al final de este tutorial podrás insertar cualquier anotación rectangular, cambiar su tamaño, color o posición, y guardar el documento modificado sin perder el contenido existente.

**Lo que aprenderás**

* Cómo cargar un PDF existente con Aspose.Pdf.  
* Cómo definir los límites del rectángulo y crear una forma rectangular.  
* Cómo agregar el rectángulo a la colección de párrafos de una página.  
* Cómo guardar el PDF actualizado y verificar el resultado.  
* Variaciones para múltiples páginas, transparencia y estilos de línea personalizados.

**Requisitos previos**

* .NET 6.0 o posterior (el código también funciona con .NET Framework 4.7+).  
* Visual Studio 2022 o cualquier IDE de C#.  
* Una referencia NuGet a `Aspose.Pdf` (versión de prueba gratuita o con licencia).  
* Un archivo PDF de entrada llamado `input.pdf` ubicado en una carpeta que controles.

---

## Cómo dibujar forma en PDF C# – configurar el proyecto

1. **Crear un nuevo proyecto de consola**  

   ```bash
   dotnet new console -n PdfRectangleDemo
   cd PdfRectangleDemo
   ```

2. **Agregar el paquete Aspose.Pdf**  

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. **Colocar `input.pdf`** en el directorio del proyecto (o en cualquier carpeta que referencies más adelante).

El proyecto ya está listo para compilar código que **agregará rectángulo a PDF**.

---

## Paso 1: Cargar el documento PDF

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // Load the existing PDF file.
        Document pdfDoc = new Document("input.pdf");
```

*La clase `Document` analiza el archivo y expone una colección `Pages`. La carga es la primera operación requerida antes de que pueda ocurrir cualquier dibujo.*

---

## Paso 2: Elegir la página de destino

```csharp
        // Get the first page (pages are 1‑based).
        Page firstPage = pdfDoc.Pages[1];
```

*Si necesitas agregar el rectángulo a una página diferente, reemplaza el índice por el número de página deseado. La biblioteca lanza una excepción cuando el índice está fuera de rango, así que asegúrate de que el PDF contenga suficientes páginas.*

---

## Paso 3: Definir los límites del rectángulo

```csharp
        // Define the rectangle's position and size (points).
        // (left, bottom, right, top) – origin is bottom‑left.
        Rectangle bounds = new Rectangle(50, 700, 300, 800);
```

*El sistema de coordenadas usa puntos (1 pt = 1/72 pulgada). El ejemplo crea un rectángulo de 250 pt de ancho por 100 pt de alto cerca de la parte superior de la página. Ajusta los números para que encajen en tu diseño.*

---

## Paso 4: Crear la forma rectangular

```csharp
        // Create a rectangle shape with the defined bounds.
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            // Optional styling – a semi‑transparent blue fill.
            FillColor = Color.FromRgb(0, 120, 215),
            FillOpacity = 0.4,

            // Optional border – 2 pt thick, dark gray.
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };
```

*La clase `Rectangle` hereda de `GraphicalObject`. Establecer `FillColor` y `Border` es opcional, pero demuestra cómo controlar la apariencia cuando **cómo dibujar forma en PDF C#** más allá de un contorno simple.*

---

## Paso 5: Agregar el rectángulo a la página

```csharp
        // Add the rectangle shape to the page's paragraph collection.
        firstPage.Paragraphs.Add(rectangleShape);
```

*Los párrafos son el contenedor para cualquier objeto dibujable. Al insertar la forma en `Paragraphs`, Aspose.Pdf la renderiza cuando se guarda el documento.*

---

## Paso 6: Guardar el PDF modificado

```csharp
        // Save the updated PDF to a new file.
        pdfDoc.Save("output.pdf");

        // Inform the user.
        Console.WriteLine("Rectangle added and saved to output.pdf");
    }
}
```

*Guardar crea un archivo nuevo para que el `input.pdf` original permanezca sin cambios. Puedes sobrescribir el archivo de origen pasando la misma ruta, pero mantener una copia de seguridad es una buena práctica.*

---

## Código fuente completo (ejecutable)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color struct

class Program
{
    static void Main()
    {
        // Step 1: Load the PDF document
        Document pdfDoc = new Document("input.pdf");

        // Step 2: Get the first page (pages are 1‑based)
        Page firstPage = pdfDoc.Pages[1];

        // Step 3: Define rectangle bounds (left, bottom, right, top)
        Rectangle bounds = new Rectangle(50, 700, 300, 800);

        // Step 4: Create a rectangle shape with optional styling
        Rectangle rectangleShape = new Rectangle(bounds)
        {
            FillColor = Color.FromArgb(102, 0, 120, 215), // 40 % opacity blue
            FillOpacity = 0.4,
            Border = new Border
            {
                Width = 2,
                Color = Color.FromRgb(50, 50, 50)
            }
        };

        // Step 5: Add the rectangle shape to the page
        firstPage.Paragraphs.Add(rectangleShape);

        // Step 6: Save the modified PDF
        pdfDoc.Save("output.pdf");

        Console.WriteLine("Rectangle added to PDF successfully.");
    }
}
```

**Salida esperada** – Abre `output.pdf` en cualquier visor de PDF. Deberías ver un rectángulo relleno de azul cerca de la esquina superior derecha de la primera página, contorneado con un borde gris oscuro.

---

## Cómo dibujar forma en PDF C# en múltiples páginas

Si necesitas **agregar rectángulo a PDF** en cada página, recorre la colección `Pages`:

```csharp
foreach (Page page in pdfDoc.Pages)
{
    Rectangle rect = new Rectangle(50, 700, 300, 800);
    Rectangle shape = new Rectangle(rect)
    {
        FillColor = Color.FromArgb(80, 255, 0, 0), // semi‑transparent red
        Border = new Border { Width = 1, Color = Color.Black }
    };
    page.Paragraphs.Add(shape);
}
```

*Este patrón reutiliza los mismos límites en cada página. Ajusta las coordenadas por página si necesitas posiciones diferentes.*

---

## Problemas comunes y consejos de buenas prácticas

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| El rectángulo aparece fuera de la página | Las coordenadas se miden desde la esquina inferior izquierda; usar un sistema de coordenadas orientado a la parte superior puede generar confusión. | Recuerda que el eje Y crece hacia arriba. Usa valores que quepan dentro del tamaño de la página (`page.PageInfo.Width`, `page.PageInfo.Height`). |
| La forma es invisible | Opacidad de relleno establecida en `0` o ancho del borde en `0`. | Asegúrate de que `FillOpacity` sea mayor que `0` y que `Border.Width` sea al menos `0.5`. |
| Guardar lanza `AccessDeniedException` | El archivo de salida está abierto en otro programa. | Cierra cualquier visor antes de ejecutar el código, o guarda en una ruta diferente. |
| El rectángulo se superpone al contenido existente | No se estableció control de capas. | Usa la propiedad `ZIndex` (valores más altos se renderizan encima) si necesitas controlar la superposición. |

---

## Extender el rectángulo – degradados, rotación y transparencia

Aspose.Pdf soporta gráficos avanzados. Para crear un rectángulo rotado con un degradado lineal:

```csharp
Rectangle gradientRect = new Rectangle(bounds)
{
    // Gradient fill from left (blue) to right (green)
    FillColor = Color.Blue,
    FillColor2 = Color.Green,
    FillMode = FillMode.LinearGradient,
    // Rotate 45 degrees around the rectangle's center
    Rotation = 45
};
firstPage.Paragraphs.Add(gradientRect);
```

*El mismo patrón de código demuestra **cómo dibujar forma en PDF C#** con efectos visuales más ricos.*

---

## Verificar el resultado programáticamente

Puedes confirmar que el rectángulo se añadió verificando el recuento de párrafos de la página:

```csharp
int shapeCount = firstPage.Paragraphs.Count;
Console.WriteLine($"Page 1 now contains {shapeCount} paragraph objects.");
```

Si el recuento aumentó en uno después de la inserción, la operación fue exitosa.

---

## Conclusión

Ahora sabes cómo **agregar rectángulo a PDF** usando C#. El tutorial cubrió cargar un documento, definir límites, crear una forma rectangular, insertarla en una página y guardar el resultado. También viste cómo manejar múltiples páginas, evitar errores comunes y aplicar estilos avanzados.

A continuación, explora temas relacionados como **cómo dibujar forma en PDF C#** para círculos, polígonos o rutas libres, y aprende a combinar formas con texto e imágenes para crear informes PDF totalmente funcionales.

¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds Guide](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)
- [How to Add an Image Stamp to a PDF Using Aspose.PDF for .NET: A Comprehensive Guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [How to Add a Rotating Image Watermark to PDFs Using Aspose.PDF for .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}