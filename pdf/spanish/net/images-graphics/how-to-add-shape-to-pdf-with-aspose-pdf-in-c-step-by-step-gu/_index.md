---
category: general
date: 2026-06-18
description: Cómo agregar una forma a un PDF usando Aspose.PDF en C# – cargar un PDF,
  dibujar un rectángulo y guardarlo.
draft: false
keywords:
- how to add shape to pdf
- load pdf document in c#
- how to draw shapes in pdf
- aspose pdf add rectangle
language: es
og_description: Cómo agregar una forma a un PDF con Aspose.PDF en C#. Aprende a cargar
  un documento PDF, dibujar un rectángulo y guardar el archivo actualizado.
og_title: Cómo agregar una forma a un PDF con Aspose.PDF en C#
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: How to add shape to PDF using Aspose.PDF in C# – load a PDF, draw a
    rectangle, and save it.
  headline: How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide
  type: TechArticle
- description: How to add shape to PDF using Aspose.PDF in C# – load a PDF, draw a
    rectangle, and save it.
  name: How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide
  steps:
  - name: What if I need to draw on multiple pages?
    text: Simply loop over `pdfDoc.Pages` and call `AddRectangle` (or any other shape)
      for each page. Remember to adjust coordinates if pages have different sizes.
  - name: Can I fill the rectangle with a color?
    text: Absolutely. Change `FillColor` from `Transparent` to any `Color` you like,
      e.g., `Color.Yellow`. The shape will appear as a solid block.
  - name: Does this work with password‑protected PDFs?
    text: 'Aspose.PDF can open encrypted files if you supply the password:'
  - name: How to add a rectangle with rounded corners?
    text: Use the `RoundedRectangle` class instead of `Rectangle`. The rest of the
      steps stay identical.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Cómo agregar una forma a PDF con Aspose.PDF en C# – Guía paso a paso
url: /es/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo agregar una forma a un PDF con Aspose.PDF en C# – Tutorial completo

¿Alguna vez te has preguntado **cómo agregar una forma a un PDF** sin lidiar con flujos de bytes de bajo nivel? En muchas aplicaciones reales necesitas resaltar una región, subrayar una cláusula o simplemente dibujar un cuadro delimitador para un campo de firma. La buena noticia es que Aspose.PDF lo hace muy fácil. En esta guía cargaremos un documento PDF en C#, dibujaremos un rectángulo y guardaremos el resultado—nada más, nada menos.

Recorreremos cada línea de código, explicaremos *por qué* cada pieza es importante y hasta te mostraremos una forma rápida de verificar que la forma realmente quedó donde esperas. Al final estarás cómodo con **cómo dibujar formas en archivos PDF**, y tendrás un fragmento reutilizable que puedes insertar en cualquier proyecto .NET.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

- **.NET 6.0** (o cualquier versión reciente de .NET) instalado en tu máquina.  
- Una **licencia válida de Aspose.PDF para .NET** (o una clave de evaluación gratuita).  
- Visual Studio 2022, Rider o cualquier editor que prefieras.  
- Un archivo PDF existente (`input.pdf`) colocado en una carpeta a la que puedas hacer referencia.

> **Consejo profesional:** Si solo estás probando, la versión de evaluación gratuita es perfectamente adecuada—añade una pequeña marca de agua pero, por lo demás, se comporta como el producto completo.

## Paso 1: Configurar el proyecto e importar los espacios de nombres

Primero, crea un nuevo proyecto de consola (o añádelo a uno existente) y trae los espacios de nombres necesarios al alcance.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;   // Required for shape classes
```

Por qué es importante: `Aspose.Pdf` te brinda el modelo de documento central, mientras que `Aspose.Pdf.Drawing` contiene la clase de forma `Rectangle` que usaremos más adelante. Sin este último, el compilador se quejará de que `Rectangle` no está definido.

## Paso 2: Cargar el documento PDF en C#

Ahora realmente **cargamos el documento PDF en C#**. Esta es la primera operación que siempre realizas cuando pretendes modificar un archivo existente.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";
Document pdfDoc = new Document(inputPath);
Console.WriteLine($"Loaded PDF with {pdfDoc.Pages.Count} page(s).");
```

*Explicación*:  
- `Document` es la representación de Aspose del archivo completo.  
- Pasar la ruta completa al constructor lee el archivo en memoria.  
- La línea `Console.WriteLine` es opcional pero útil para depuración—si el recuento de páginas es cero sabes que algo falló temprano.

## Paso 3: Definir la forma rectángulo

Aquí es donde llegamos al corazón de **cómo agregar una forma a un PDF**. Creamos un objeto `Rectangle` que especifica su posición y tamaño usando el sistema de coordenadas donde (0,0) es la esquina inferior‑izquierda de la página.

```csharp
// Step 3: Define a rectangle (left, bottom, right, top)
Rectangle rect = new Rectangle(0, 0, 200, 100)
{
    // Optional styling – you can tweak these as needed
    FillColor = Color.Transparent,          // No fill, just the border
    Border = new Border(BorderStyle.Solid, 2, Color.Red)
};
```

Por qué establecemos `FillColor` como transparente: la mayoría de los casos de uso solo quieren un contorno (piensa en una caja de resaltado). La propiedad `Border` te permite controlar el grosor y el color; el rojo hace que el rectángulo destaque en una página típica blanca.

## Paso 4: Verificar que la forma cabe dentro de los límites de la página

Antes de **agregar el rectángulo**, es una buena práctica asegurarse de que la forma no se desborde de los bordes de la página. Aspose proporciona `ValidateShapeBounds` para exactamente este propósito.

```csharp
// Step 4: Validate that the rectangle fits on the first page
bool fits = pdfDoc.Pages[1].ValidateShapeBounds(rect);
if (!fits)
{
    Console.WriteLine("Rectangle exceeds page dimensions – adjusting...");
    // Simple fallback: shrink to fit the page width
    rect.Right = pdfDoc.Pages[1].PageInfo.Width - 10;
    rect.Top  = pdfDoc.Pages[1].PageInfo.Height - 10;
}
```

*Por qué*: Intentar dibujar fuera de la página puede causar fallos de renderizado o incluso lanzar una excepción. Esta comprobación hace que el tutorial sea robusto para PDFs de cualquier tamaño.

## Paso 5: Añadir el rectángulo a la página deseada

Ahora finalmente **agregamos la forma al PDF**. El método `AddRectangle` adjunta la forma a la colección de anotaciones de la página, lo que significa que los visores PDF la renderizarán como cualquier otro dibujo.

```csharp
// Step 5: Add the rectangle to the first page
pdfDoc.Pages[1].AddRectangle(rect);
Console.WriteLine("Rectangle added to page 1.");
```

Si necesitas dirigirte a una página diferente, simplemente reemplaza el índice `1` por el número de página apropiado (Aspose usa indexación basada en 1).

## Paso 6: Guardar el PDF modificado

El último paso es escribir los cambios de vuelta al disco. Puedes sobrescribir el archivo original o crear uno nuevo—aquí generaremos `output.pdf`.

```csharp
// Step 6: Save the updated PDF
string outputPath = @"YOUR_DIRECTORY\output.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved as {outputPath}");
```

*Qué esperar*: Abre `output.pdf` en Adobe Reader o cualquier visor y deberías ver un rectángulo rojo nítido anclado a la esquina inferior‑izquierda de la primera página.

![Diagrama que muestra el rectángulo añadido al PDF](https://example.com/rectangle-diagram.png "ejemplo de cómo agregar forma a pdf")

*Texto alternativo*: "cómo agregar forma a pdf – rectángulo dibujado en la primera página de un archivo PDF"

## Paso 7: Ejemplo completo (listo para copiar y pegar)

A continuación tienes el programa completo que puedes compilar y ejecutar de inmediato. Recuerda reemplazar `YOUR_DIRECTORY` con la ruta real de la carpeta en tu máquina.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;   // For color definitions

namespace PdfShapeDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the PDF document in C#
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document pdfDoc = new Document(inputPath);
            Console.WriteLine($"Loaded PDF with {pdfDoc.Pages.Count} page(s).");

            // Define the rectangle shape
            Rectangle rect = new Rectangle(0, 0, 200, 100)
            {
                FillColor = Color.Transparent,
                Border = new Border(BorderStyle.Solid, 2, Color.Red)
            };

            // Validate bounds on the first page
            if (!pdfDoc.Pages[1].ValidateShapeBounds(rect))
            {
                Console.WriteLine("Rectangle exceeds page dimensions – adjusting...");
                rect.Right = pdfDoc.Pages[1].PageInfo.Width - 10;
                rect.Top  = pdfDoc.Pages[1].PageInfo.Height - 10;
            }

            // Add the rectangle (how to add shape to pdf)
            pdfDoc.Pages[1].AddRectangle(rect);
            Console.WriteLine("Rectangle added to page 1.");

            // Save the modified PDF
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved as {outputPath}");
        }
    }
}
```

Ejecuta el programa, abre `output.pdf` y verás el rectángulo rojo exactamente donde lo colocamos. Si necesitas una forma diferente—elipse, línea o polígono—simplemente cambia `Rectangle` por `Ellipse`, `Line` o `Polygon` manteniendo el mismo flujo de trabajo. Eso es esencialmente **cómo dibujar formas en PDF** usando Aspose.

## Preguntas frecuentes y casos especiales

### ¿Qué pasa si necesito dibujar en varias páginas?
Simplemente recorre `pdfDoc.Pages` y llama a `AddRectangle` (o cualquier otra forma) para cada página. Recuerda ajustar las coordenadas si las páginas tienen tamaños diferentes.

```csharp
foreach (Page page in pdfDoc.Pages)
{
    page.AddRectangle(rect);
}
```

### ¿Puedo rellenar el rectángulo con un color?
Absolutamente. Cambia `FillColor` de `Transparent` a cualquier `Color` que desees, por ejemplo, `Color.Yellow`. La forma aparecerá como un bloque sólido.

### ¿Esto funciona con PDFs protegidos con contraseña?
Aspose.PDF puede abrir archivos cifrados si proporcionas la contraseña:

```csharp
Document pdfDoc = new Document(inputPath, new LoadOptions { Password = "mySecret" });
```

### ¿Cómo agregar un rectángulo con esquinas redondeadas?
Utiliza la clase `RoundedRectangle` en lugar de `Rectangle`. El resto de los pasos permanece idéntico.

## Recapitulación

Hemos cubierto **cómo agregar una forma a un PDF** usando Aspose.PDF en C#. El proceso se reduce a:

1. **Cargar el documento PDF en C#** – crear un objeto `Document`.  
2. **Definir un rectángulo** (o cualquier otra forma).  
3. **Validar los límites** para evitar desbordes.  
4. **Agregar el rectángulo** a la página objetivo.  
5. **Guardar** el archivo modificado.

Ese es todo el flujo de trabajo para **aspose pdf add rectangle**, y ahora tienes una plantilla que puedes adaptar para círculos, líneas o polígonos personalizados.

## ¿Qué sigue?

- **Explora otros primitivas de dibujo**: `Ellipse`, `Line`, `Polygon`.  
- **Añade anotaciones de texto** junto a tus formas para una interactividad más rica.  
- **Combínalo con campos de formulario PDF** si estás construyendo un contrato rellenable.  
- **Revisa las funciones de conversión de PDF de Aspose** para convertir tus PDFs anotados en imágenes para miniaturas de vista previa.

Siéntete libre de experimentar—tal vez dibujar una marca de agua, resaltar una celda de tabla o delinear un campo de firma. La API es flexible, y ahora conoces los fundamentos.

¡Feliz codificación, y que tus PDFs siempre se vean exactamente como lo deseas!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add Hyperlinks in PDFs Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/bookmarks-navigation/add-hyperlinks-pdf-aspose-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}