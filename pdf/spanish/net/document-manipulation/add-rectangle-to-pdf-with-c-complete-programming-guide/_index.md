---
category: general
date: 2026-06-05
description: Agregar un rectángulo a un PDF usando Aspose.Pdf en C#. Aprende cómo
  cargar un PDF existente, editar la página del PDF e insertar una forma en el PDF
  en minutos.
draft: false
keywords:
- add rectangle to pdf
- draw rectangle on pdf
- load existing pdf
- edit pdf page
- insert shape into pdf
language: es
og_description: Añade un rectángulo a PDF rápidamente. Este tutorial muestra cómo
  cargar un PDF existente, editar la página del PDF y dibujar un rectángulo en el
  PDF usando Aspose.Pdf.
og_title: Agregar rectángulo a PDF con C# – Guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Add rectangle to PDF using Aspose.Pdf in C#. Learn how to load existing
    PDF, edit PDF page, and insert shape into PDF in minutes.
  headline: Add Rectangle to PDF with C# – Complete Programming Guide
  type: TechArticle
- description: Add rectangle to PDF using Aspose.Pdf in C#. Learn how to load existing
    PDF, edit PDF page, and insert shape into PDF in minutes.
  name: Add Rectangle to PDF with C# – Complete Programming Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.6+). - Aspose.Pdf
      for .NET NuGet package (`Install-Package Aspose.Pdf`). - Basic familiarity with
      C# syntax (no deep PDF knowledge required).'
  - name: Why loading matters
    text: Before you can draw anything, the PDF must be in memory. The `Document`
      constructor reads the file, parses its internal structure, and gives you an
      object model to work with. If the file is locked or corrupted, Aspose will throw
      a descriptive exception—so you know exactly what went wrong.
  - name: Code
    text: '```csharp Document doc = new Document("YOUR_DIRECTORY/input.pdf"); ```'
  - name: Why page selection is crucial
    text: PDFs are page‑oriented; each page has its own coordinate system. Aspose
      uses a **1‑based** index, which trips up developers coming from 0‑based collections.
      Selecting the wrong page either throws an `ArgumentOutOfRangeException` or modifies
      an unintended page.
  - name: Code
    text: '```csharp Page page = doc.Pages[1]; // First page ```'
  - name: Understanding the rectangle coordinates
    text: A rectangle in Aspose.Pdf is defined by its lower‑left (`xLL`, `yLL`) and
      upper‑right (`xUR`, `yUR`) corners. The coordinate system starts at the **bottom‑left**
      of the page, with X increasing to the right and Y increasing upward. This is
      opposite of many UI frameworks, so keep an eye on the axes.
  - name: Code to add the shape
    text: '```csharp Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500,
      700); page.AddRectangle(rect); ```'
  - name: Why saving is the final step
    text: All manipulations stay in memory until you persist them. `Document.Save`
      writes the new content to disk (or stream). Overwriting the original file is
      possible, but keeping a backup (`output.pdf`) is safer.
  - name: Code
    text: '```csharp doc.Save("YOUR_DIRECTORY/output.pdf"); ```'
  type: HowTo
- questions:
  - answer: Yes—loop through `doc.Pages` and repeat the `AddRectangle` call for each
      `Page` object.
    question: Can I add the rectangle to every page automatically?
  - answer: Aspose provides `AddCircle`, `AddPolygon`, and `AddPolyline` methods.
      The same rectangle logic applies for bounding boxes.
    question: What if I need to draw a circle or a polygon?
  - answer: 'Compute the center coordinates:'
    question: Is there a way to position the rectangle relative to the page center?
  - answer: Aspose loads pages lazily, but if you’re processing thousands of pages,
      consider using `PdfExtractor` to work on subsets or stream the file to reduce
      memory footprint.
    question: Performance concerns for large PDFs?
  type: FAQPage
tags:
- pdf
- csharp
- aspose
- shape-manipulation
title: Agregar rectángulo a PDF con C# – Guía completa de programación
url: /es/net/document-manipulation/add-rectangle-to-pdf-with-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Agregar rectángulo a PDF con C# – Guía completa de programación

¿Alguna vez necesitaste **add rectangle to pdf** pero no estabas seguro de qué llamada API usar? No estás solo—muchos desarrolladores se topan con ese obstáculo cuando intentan editar un PDF programáticamente por primera vez. ¿La buena noticia? Con unas pocas líneas de C# y la poderosa biblioteca Aspose.Pdf, puedes dibujar un rectángulo en cualquier página de un documento existente en un instante.

En esta guía recorreremos la carga de un PDF existente, la selección de la página correcta, la definición de un rectángulo que encaje y, finalmente, la inserción de la forma en el PDF. Al final tendrás un fragmento reutilizable que podrás insertar en cualquier proyecto .NET. Ah, y también abordaremos matices de **draw rectangle on pdf** que quizás no hayas considerado.

## Lo que obtendrás

- Una solución clara, paso a paso, que funciona out‑of‑the‑box.
- Comprensión de cómo cargar archivos **load existing pdf** de forma segura.
- Consejos para **edit pdf page** sin dañar el documento.
- Estrategias para **insert shape into pdf** más allá de los simples rectángulos.
- Código C# listo para ejecutar que puedes copiar y pegar inmediatamente.

### Requisitos previos

- .NET 6.0 o posterior (el código también funciona en .NET Framework 4.6+).
- Paquete NuGet Aspose.Pdf para .NET (`Install-Package Aspose.Pdf`).
- Familiaridad básica con la sintaxis de C# (no se requiere conocimiento profundo de PDF).

Si los tienes, vamos a sumergirnos.

![Ejemplo de añadir rectángulo a PDF](add-rectangle-to-pdf.png "Captura de pantalla que muestra un rectángulo añadido a una página PDF – add rectangle to pdf")

## Añadir rectángulo a PDF – Visión general paso a paso

A continuación se muestra el ejemplo completo y ejecutable que sigue el orden exacto que discutiremos:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the existing PDF file
        Document doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Select the first page (pages are 1‑based)
        Page page = doc.Pages[1];

        // 3️⃣ Define a rectangle that fits inside the page bounds
        //    (xLL, yLL, xUR, yUR) – lower‑left & upper‑right corners
        Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500, 700);

        // 4️⃣ Add the rectangle to the page – this draws the shape
        page.AddRectangle(rect);

        // 5️⃣ Save the modified PDF to a new file
        doc.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

Ahora desglosaremos cada línea para que entiendas **por qué** hacemos lo que hacemos, no solo **qué**.

## Cargar documento PDF existente

### Por qué es importante cargar

Antes de poder dibujar cualquier cosa, el PDF debe estar en memoria. El constructor `Document` lee el archivo, analiza su estructura interna y te proporciona un modelo de objetos con el que trabajar. Si el archivo está bloqueado o corrupto, Aspose lanzará una excepción descriptiva—para que sepas exactamente qué salió mal.

### Código

```csharp
Document doc = new Document("YOUR_DIRECTORY/input.pdf");
```

- Reemplaza `YOUR_DIRECTORY` con la ruta absoluta o relativa a tu archivo fuente.
- La ruta puede ser una URL si habilitas la carga remota de Aspose (escenario avanzado).
- **Consejo:** Envuelve esto en un bloque `try/catch` para manejar `FileNotFoundException` o `PdfException` de forma elegante.

```csharp
try
{
    Document doc = new Document("input.pdf");
}
catch (Exception ex)
{
    Console.WriteLine($"Failed to load PDF: {ex.Message}");
    return;
}
```

## Seleccionar y preparar la página

### Por qué la selección de página es crucial

Los PDFs están orientados por páginas; cada página tiene su propio sistema de coordenadas. Aspose utiliza un índice **basado en 1**, lo que confunde a los desarrolladores acostumbrados a colecciones basadas en 0. Seleccionar la página incorrecta lanza una `ArgumentOutOfRangeException` o modifica una página no deseada.

### Código

```csharp
Page page = doc.Pages[1]; // First page
```

Si necesitas trabajar en la página 3, simplemente cambia el índice a `3`. Para escenarios dinámicos, puedes iterar:

```csharp
foreach (Page pg in doc.Pages)
{
    // Apply rectangle to every page
}
```

## Definir y dibujar rectángulo en PDF

### Comprender las coordenadas del rectángulo

Un rectángulo en Aspose.Pdf se define por sus esquinas inferior‑izquierda (`xLL`, `yLL`) y superior‑derecha (`xUR`, `yUR`). El sistema de coordenadas comienza en la **esquina inferior‑izquierda** de la página, con X aumentando hacia la derecha y Y aumentando hacia arriba. Esto es opuesto al de muchos frameworks UI, así que vigila los ejes.

- `0,0` es la esquina inferior‑izquierda de la página.
- Ancho = `xUR - xLL`; Altura = `yUR - yLL`.

Si accidentalmente defines un rectángulo más grande que la página, `AddRectangle` lanzará una excepción. Para evitarlo, puedes consultar el tamaño de la página:

```csharp
double pageWidth  = page.PageInfo.Width;
double pageHeight = page.PageInfo.Height;
```

Luego limita tu rectángulo:

```csharp
double rectWidth  = Math.Min(500, pageWidth);
double rectHeight = Math.Min(700, pageHeight);
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, rectWidth, rectHeight);
```

### Código para añadir la forma

```csharp
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500, 700);
page.AddRectangle(rect);
```

- `AddRectangle` dibuja automáticamente un borde negro delgado.
- ¿Quieres un rectángulo relleno? Usa `page.AddAnnotation(new SquareAnnotation(page, rect) { FillColor = Color.Yellow });`.
- ¿Necesitas un grosor de línea diferente? Establece `rect.LineWidth = 2;` antes de añadir.

#### Caso límite: múltiples rectángulos

Si llamas a `AddRectangle` repetidamente, cada llamada añade otra forma. Para evitar superposiciones, desplaza los rectángulos posteriores:

```csharp
for (int i = 0; i < 3; i++)
{
    var offset = i * 20;
    var r = new Aspose.Pdf.Rectangle(offset, offset, 500 + offset, 700 + offset);
    page.AddRectangle(r);
}
```

## Guardar el PDF modificado

### Por qué guardar es el paso final

Todas las manipulaciones permanecen en memoria hasta que las persistes. `Document.Save` escribe el nuevo contenido en disco (o en un stream). Sobrescribir el archivo original es posible, pero mantener una copia de seguridad (`output.pdf`) es más seguro.

### Código

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

- También puedes guardar en un `MemoryStream` si necesitas enviar el PDF por HTTP:

```csharp
using var ms = new MemoryStream();
doc.Save(ms);
byte[] pdfBytes = ms.ToArray();
// return File(pdfBytes, "application/pdf");
```

## Ejemplo completo funcional (listo para copiar y pegar)

Juntando todo, aquí tienes el programa final que puedes ejecutar ahora mismo:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

class AddRectangleDemo
{
    static void Main()
    {
        const string inputPath  = "input.pdf";
        const string outputPath = "output.pdf";

        // Load the existing PDF
        Document doc;
        try
        {
            doc = new Document(inputPath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error loading PDF: {ex.Message}");
            return;
        }

        // Ensure the document has at least one page
        if (doc.Pages.Count == 0)
        {
            Console.WriteLine("PDF contains no pages.");
            return;
        }

        // Select the first page (1‑based index)
        Page page = doc.Pages[1];

        // Get page dimensions to avoid overflow
        double pageW = page.PageInfo.Width;
        double pageH = page.PageInfo.Height;

        // Define rectangle size (clamp to page bounds)
        double rectW = Math.Min(500, pageW);
        double rectH = Math.Min(700, pageH);
        Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, rectW, rectH);

        // Optional: set line width and color
        rect.LineWidth = 2;
        rect.Color = Color.Blue;

        // Add rectangle to the page
        page.AddRectangle(rect);

        // Save the result
        doc.Save(outputPath);
        Console.WriteLine($"Rectangle added and saved to {outputPath}");
    }
}
```

**Salida esperada:** Abre `output.pdf` y verás un rectángulo con borde azul anclado en la esquina inferior‑izquierda de la primera página, con un tamaño de hasta 500 × 700 puntos (o más pequeño si la página es diminuta).

## Preguntas frecuentes y consejos profesionales

- **¿Puedo añadir el rectángulo a cada página automáticamente?**  
  Sí—itera a través de `doc.Pages` y repite la llamada `AddRectangle` para cada objeto `Page`.

- **¿Qué pasa si necesito dibujar un círculo o un polígono?**  
  Aspose ofrece los métodos `AddCircle`, `AddPolygon` y `AddPolyline`. La misma lógica del rectángulo se aplica para las cajas delimitadoras.

- **¿Existe una forma de posicionar el rectángulo relativo al centro de la página?**  
  Calcula las coordenadas centrales:  
  ```csharp
  double centerX = pageW / 2;
  double centerY = pageH / 2;
  double halfW = rectW / 2;
  double halfH = rectH / 2;
  var centeredRect = new Aspose.Pdf.Rectangle(centerX - halfW, centerY - halfH,
                                              centerX + halfW, centerY + halfH);
  page.AddRectangle(centeredRect);
  ```

- **¿Preocupaciones de rendimiento para PDFs grandes?**  
  Aspose carga las páginas de forma perezosa, pero si procesas miles de páginas, considera usar `PdfExtractor` para trabajar con subconjuntos o transmitir el archivo para reducir el consumo de memoria.

## Conclusión

Ahora sabes **cómo añadir rectángulo

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Crear documento PDF con Aspose.PDF – Añadir página, forma y guardar](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [Cómo añadir sellos de página en PDFs usando Aspose.PDF para .NET: Guía completa](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Añadir imágenes y números de página a PDFs usando Aspose.PDF para .NET: Guía completa](/pdf/english/net/document-manipulation/enhance-pdfs-images-page-numbers-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}