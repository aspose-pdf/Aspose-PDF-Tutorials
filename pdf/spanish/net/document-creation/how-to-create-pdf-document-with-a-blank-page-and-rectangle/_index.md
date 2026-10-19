---
category: general
date: 2026-09-05
description: Crear un documento PDF en C# añadiendo una página en blanco, dibujando
  un rectángulo y guardando el archivo PDF. Sigue un ejemplo paso a paso de Aspose.PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add blank page pdf
- draw rectangle pdf
- save pdf file
- how to add rectangle
language: es
lastmod: 2026-09-05
og_description: Crear documento PDF en C# añadiendo una página en blanco, dibujando
  un rectángulo y guardando el archivo PDF. Sigue este ejemplo completo con Aspose.PDF.
og_image_alt: Screenshot showing a PDF document with a drawn rectangle on a blank
  page
og_title: Crear documento PDF con página en blanco y rectángulo – Guía de C#
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  headline: How to create PDF document with a blank page and rectangle
  type: TechArticle
- description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  name: How to create PDF document with a blank page and rectangle
  steps:
  - name: 'Edge case: custom page size'
    text: 'If your layout requires a 6 × 9 inch page, replace the default call with:'
  - name: 'Pro tip: styling the rectangle'
    text: 'You can change the stroke color and line width:'
  - name: 'Edge case: overwriting existing files'
    text: 'Aspose.PDF overwrites an existing file by default. To protect previous
      outputs, check for file existence first:'
  - name: Expected output
    text: Running the program creates a single‑page PDF. When you open `output.pdf`
      you will see a blank white page with a red rectangle positioned 100 points from
      the left and bottom edges, measuring 200 × 200 points.
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
- PDF generation
title: Cómo crear un documento PDF con una página en blanco y un rectángulo
url: /es/net/document-creation/how-to-create-pdf-document-with-a-blank-page-and-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear un documento PDF con una página en blanco y un rectángulo

Si necesitas **crear documento PDF** programáticamente, esta guía muestra una solución completa en C#. Aprenderás cómo agregar una página en blanco, dibujar un rectángulo en esa página y, finalmente, guardar el archivo PDF. El ejemplo utiliza la biblioteca Aspose.PDF, que funciona con .NET 6+ y .NET Framework 4.5+.

Agregar una página en blanco y dibujar formas es un requisito común para facturas, certificados o informes personalizados. Al final de este tutorial tendrás un proyecto ejecutable que produce un PDF que contiene un solo rectángulo ubicado en (100, 100) con un tamaño de 200 × 200 puntos.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* Visual Studio 2022 (o cualquier IDE de C#)
* .NET 6 SDK o .NET Framework 4.5+
* Paquete NuGet Aspose.PDF for .NET  
  ```bash
  dotnet add package Aspose.PDF
  ```
* Permiso de escritura en el directorio de salida

No se requiere configuración adicional; el código funciona listo para usar.

## Crear documento PDF – visión general

El proceso completo consta de cuatro pasos lógicos:

1. **Instanciar** un objeto `Document` – representa el archivo PDF.
2. **Agregar una página en blanco** – la página proporciona un lienzo para dibujar.
3. **Dibujar un rectángulo** – un objeto `Path` define la forma.
4. **Guardar el archivo PDF** – persiste el documento en el disco.

Cada paso está aislado en su propia sección para que puedas reutilizar o reemplazar partes según sea necesario.

![Diagram of a PDF with a rectangle on a blank page](https://example.com/placeholder-image.png){.img-fluid alt="Diagrama de un PDF con un rectángulo en una página en blanco"}

## Agregar página en blanco pdf

Un PDF debe contener al menos una página antes de que se puedan colocar gráficos. El método `Pages.Add()` crea una página vacía con dimensiones predeterminadas (A4). Si necesitas un tamaño diferente, pasa un argumento `PageSize`.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();

// Step 2: Add a blank page to the document
Page pdfPage = pdfDocument.Pages.Add();   // adds an A4 page by default
```

*Por qué este paso es importante* – El objeto página contiene colecciones para texto, imágenes y gráficos vectoriales. Sin una página, cualquier intento de agregar un rectángulo generará una excepción.

### Caso límite: tamaño de página personalizado

Si tu diseño requiere una página de 6 × 9 pulgadas, reemplaza la llamada predeterminada con:

```csharp
var pageSize = new Size(432, 648); // 72 points per inch
Page pdfPage = pdfDocument.Pages.Add(pageSize);
```

## Dibujar rectángulo pdf

Dibujar un rectángulo consiste en crear una geometría `Rectangle` y envolverla en un `Path`. La llamada `ValidateBounds()` asegura que la forma encaje dentro de los márgenes de la página, evitando recortes.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

// Step 4: Add the rectangle to the page contents
Path rectanglePath = new Path(shapeRect).ValidateBounds();
pdfPage.Contents.Add(rectanglePath);
```

*Por qué este paso es importante* – El objeto `Path` es la primitiva vectorial de bajo nivel utilizada por Aspose.PDF. Al validar los límites evitas errores en tiempo de ejecución cuando el rectángulo supera los límites de la página.

### Consejo profesional: estilo del rectángulo

Puedes cambiar el color del trazo y el ancho de línea:

```csharp
rectanglePath.GraphInfo = new GraphInfo
{
    StrokeColor = Color.Red,
    LineWidth = 2
};
```

Esto produce un contorno rojo con un grosor de 2 puntos.

## Guardar archivo pdf

Persistir el documento finaliza el archivo en el disco. El método `Save` acepta una ruta de archivo o un stream. Proporcionar una ruta absoluta hace que la ubicación sea explícita, lo cual es útil para scripts de automatización.

```csharp
// Step 5: Save the PDF to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

*Por qué este paso es importante* – Guardar es el único punto donde la representación en memoria se convierte en un archivo físico. Si necesitas devolver el PDF desde una API web, reemplaza la ruta del archivo con un `MemoryStream`.

### Caso límite: sobrescribir archivos existentes

Aspose.PDF sobrescribe un archivo existente por defecto. Para proteger salidas anteriores, verifica la existencia del archivo primero:

```csharp
if (File.Exists(outputPath))
{
    File.Delete(outputPath);
}
pdfDocument.Save(outputPath);
```

## Cómo agregar un rectángulo – mejores prácticas

* **Mantén las coordenadas dentro de los márgenes de la página** – usa `ValidateBounds()` o calcula los márgenes manualmente.
* **Reutiliza objetos `GraphInfo`** al dibujar múltiples formas; esto reduce la asignación de memoria.
* **Descarta el objeto `Document`** (como se muestra con `using var`) para liberar los recursos nativos rápidamente.
* **Prueba con diferentes configuraciones de DPI** si más adelante incrustas imágenes raster; las formas vectoriales como los rectángulos permanecen nítidas a cualquier resolución.

## Ejemplo completo funcional

A continuación se muestra el programa completo que puedes copiar en una aplicación de consola. Compila sin modificaciones y produce `output.pdf` en la carpeta del proyecto.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using var pdfDocument = new Document();

        // Add a blank page to the document
        Page pdfPage = pdfDocument.Pages.Add();

        // Define a rectangle shape (x, y, width, height)
        Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

        // Create a path for the rectangle and validate its bounds
        Path rectanglePath = new Path(shapeRect).ValidateBounds();

        // Optional: style the rectangle (red outline, 2‑pt width)
        rectanglePath.GraphInfo = new GraphInfo
        {
            StrokeColor = Color.Red,
            LineWidth = 2
        };

        // Add the rectangle to the page contents
        pdfPage.Contents.Add(rectanglePath);

        // Determine output path
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");

        // Ensure no leftover file blocks the save operation
        if (File.Exists(outputPath))
        {
            File.Delete(outputPath);
        }

        // Save the PDF to a file
        pdfDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

### Resultado esperado

Ejecutar el programa crea un PDF de una sola página. Cuando abras `output.pdf` verás una página blanca en blanco con un rectángulo rojo ubicado a 100 puntos del borde izquierdo y del inferior, con un tamaño de 200 × 200 puntos.

## Conclusión

Ahora sabes cómo **crear documento PDF**, **agregar página en blanco pdf**, **dibujar rectángulo pdf** y **guardar archivo pdf** usando Aspose.PDF en C#. El ejemplo cubre las llamadas esenciales a la API, explica por qué cada llamada es necesaria y brinda consejos para variaciones comunes como tamaños de página personalizados o estilo del rectángulo.

A continuación, explora temas relacionados como **agregar texto**, **incrustar imágenes** o **crear informes multipágina**. El mismo patrón—instanciar un `Document`, manipular páginas, agregar contenido vectorial o raster, luego `Save`—se aplica a todos esos escenarios. Siéntete libre de experimentar con diferentes formas, colores y diseños de página para adaptarlos a las necesidades de tu proyecto.

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Crear documento PDF C# – Agregar página, dibujar rectángulo y guardar](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)
- [Crear documento PDF con Aspose.PDF – Guía paso a paso](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Crear documento PDF con Aspose – Agregar página, cuadro de texto y formulario](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}