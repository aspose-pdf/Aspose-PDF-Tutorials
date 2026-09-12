---
category: general
date: 2026-09-12
description: Aprende cómo agregar transparencia a un PDF, dibujar un rectángulo en
  un PDF y guardar el PDF con transparencia usando Aspose.PDF en C# – guía paso a
  paso.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- draw rectangle on pdf
- save pdf with transparency
language: es
lastmod: 2026-09-12
og_description: Añade transparencia a PDF, dibuja un rectángulo en PDF y guarda el
  PDF con transparencia usando Aspose.PDF en C#. Sigue este tutorial completo.
og_image_alt: Screenshot of a PDF page showing a semi‑transparent rectangle drawn
  with Aspose.PDF
og_title: Añade transparencia a PDF y dibuja un rectángulo en PDF – guía completa
  de C#
schemas:
- author: Aspose
  dateModified: '2026-09-12'
  description: Learn how to add transparency to PDF, draw a rectangle on PDF, and
    save PDF with transparency using Aspose.PDF in C# – step‑by‑step guide.
  headline: How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Cómo agregar transparencia a un PDF y dibujar un rectángulo en un PDF con Aspose.PDF
url: /es/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo agregar transparencia a PDF y dibujar un rectángulo en PDF con Aspose.PDF

Si necesita **agregar transparencia a PDF** archivos, esta guía le muestra exactamente cómo hacerlo en C#. También aprenderá cómo **dibujar un rectángulo en PDF** y finalmente **guardar PDF con transparencia** para que el resultado pueda reutilizarse en informes, facturas o cualquier flujo de trabajo de automatización de documentos.

En este tutorial usted:

* Cargará un documento PDF existente.
* Creará un estado gráfico personalizado que define la opacidad del trazo y del relleno.
* Aplicará ese estado gráfico al lienzo y dibujará un rectángulo.
* Guardará el archivo modificado preservando la configuración de transparencia.

No se requieren herramientas externas más allá de la biblioteca Aspose.PDF for .NET, y cada línea de código se explica para que entienda *por qué* cada paso es importante.

## Requisitos previos

* .NET 6.0 o posterior (el código también funciona con .NET Framework 4.7+).
* Una copia con licencia o de evaluación de **Aspose.PDF for .NET**. Instálela vía NuGet:

```bash
dotnet add package Aspose.Pdf
```

* Un PDF de entrada (`input.pdf`) colocado en una carpeta que pueda referenciar desde su proyecto.

## Paso 1: Cargar el documento PDF

La primera operación es abrir el archivo fuente. Usar la sentencia `using` garantiza que el documento se libere correctamente, lo que evita problemas de bloqueo de archivo más adelante cuando intente guardar.

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";
using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

*Por qué esto es importante*: Cargar el documento le brinda acceso a la colección de páginas, a los diccionarios de recursos y a los objetos de lienzo necesarios para dibujar.

## Paso 2: Acceder al diccionario de recursos de la primera página

Cada página PDF tiene un **diccionario de recursos** que almacena objetos como fuentes, imágenes y estados gráficos. Para introducir una nueva configuración de transparencia necesitamos editar la entrada `ExtGState`.

```csharp
// Step 2: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

*Por qué esto es importante*: El `DictionaryEditor` nos permite leer y modificar objetos PDF de bajo nivel sin romper la estructura del documento.

## Paso 3: Crear un estado gráfico personalizado con valores de transparencia

Un estado gráfico (`ExtGState`) controla cómo se renderizan las operaciones de dibujo. Definimos dos parámetros de opacidad:

* **CA** – opacidad del trazo (el contorno de las formas).
* **ca** – opacidad del relleno (el interior de las formas).

También establecemos el modo de fusión (`BM`) a “Normal”, que es la operación de composición más común.

```csharp
// Step 3: Create a custom graphics state (ExtGState) with transparency settings
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
var customGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "CA", new Aspose.Pdf.Cos.CosPdfNumber(1)),          // stroke opacity = 100 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),        // fill opacity = 50 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))      // normal blend mode
};

foreach (var p in parameters)
    customGs.Add(p);

// Register the new graphics state under the name "GS0"
extGStateDict.Add("GS0", customGs);
```

*Por qué esto es importante*: Al agregar `GS0` al diccionario `ExtGState` creamos una referencia reutilizable que el lienzo puede activar antes de dibujar. La opacidad de relleno de `0.5` hace que el rectángulo sea semitransparente, logrando el objetivo de **agregar transparencia a PDF**.

## Paso 4: Aplicar el estado gráfico y dibujar un rectángulo

Ahora indicamos al lienzo de la página que use el estado gráfico que acabamos de crear y luego dibujamos un rectángulo. Las coordenadas siguen el sistema de coordenadas PDF (origen en la esquina inferior izquierda).

```csharp
// Step 4: Apply the custom graphics state and draw a rectangle
var canvas = firstPage.Canvas;

// Activate the transparency graphics state
canvas.SetGraphicsState("GS0");

// Draw a rectangle from (100, 500) to (200, 600)
canvas.Rectangle(100, 500, 200, 600);

// Render the rectangle outline using the current graphics state
canvas.Stroke();
```

*Por qué esto es importante*: `SetGraphicsState("GS0")` cambia el contexto de dibujo a la configuración de transparencia definida anteriormente. El método `Rectangle` define la forma, y `Stroke` renderiza el contorno con la opacidad especificada. Si también desea un rectángulo relleno, reemplace `Stroke()` por `FillAndStroke()`.

## Paso 5: Guardar el PDF modificado preservando la transparencia

Finalmente, escriba el documento de nuevo en disco. El archivo de salida contiene el nuevo estado gráfico, el rectángulo dibujado y la información de transparencia.

```csharp
// Step 5: Save the modified PDF
string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
pdfDocument.Save(outputPath);
```

*Por qué esto es importante*: Guardar el documento finaliza todos los cambios. El archivo resultante puede abrirse en cualquier visor de PDF, y el rectángulo aparecerá con un 50 % de opacidad de relleno.

### Resultado esperado

Al abrir `output_with_extgstate.pdf` debería ver un rectángulo cuyo borde es completamente opaco y cuyo interior es semitransparente, permitiendo que el contenido subyacente de la página se muestre a través de él.

## Casos límite y consejos prácticos

| Situación | Ajuste recomendado |
|-----------|--------------------|
| **Múltiples páginas** | Recorra `pdfDocument.Pages` y repita los pasos 2‑4 para cada página objetivo. |
| **Valores de opacidad diferentes** | Cambie los valores `CosPdfNumber` de `CA` (trazo) y `ca` (relleno) a cualquier número entre `0` (totalmente transparente) y `1` (totalmente opaco). |
| **Modos de fusión personalizados** | Reemplace `"Normal"` por `"Multiply"`, `"Screen"` o cualquier modo de fusión estándar de PDF compatible con su visor. |
| **Rectángulo relleno** | Llame a `canvas.FillAndStroke()` en lugar de `canvas.Stroke()` para aplicar tanto el relleno como el contorno. |
| **Reutilizar el mismo estado gráfico** | Puede llamar a `canvas.SetGraphicsState("GS0")` antes de dibujar cualquier número de formas en la misma página. |

**Consejo profesional:** Siempre inspeccione el diccionario de recursos después de agregar un nuevo `ExtGState`. Si el diccionario no existe, créelo primero:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
    resourcesEditor.Add("ExtGState", new Aspose.Pdf.Cos.CosPdfDictionary(pdfDocument));
```

## Ejemplo completo y ejecutable

A continuación se muestra un programa autocontenido que puede copiar en una aplicación de consola y ejecutar de inmediato (reemplaze `YOUR_DIRECTORY` con una ruta real).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF document
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Access the first page’s resources
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        if (!resourcesEditor.ContainsKey("ExtGState"))
            resourcesEditor.Add("ExtGState", new CosPdfDictionary(pdfDocument));

        // 3️⃣ Create a custom graphics state with transparency
        var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        var customGs = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };

        foreach (var p in parameters)
            customGs.Add(p);

        extGStateDict.Add("GS0", customGs);

        // 4️⃣ Apply the graphics state and draw a rectangle
        var canvas = firstPage.Canvas;
        canvas.SetGraphicsState("GS0");
        canvas.Rectangle(100, 500, 200, 600);
        canvas.Stroke(); // use FillAndStroke() for a filled shape

        // 5️⃣ Save the PDF with transparency
        string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine("PDF saved with a transparent rectangle at: " + outputPath);
    }
}
```

Ejecutar el programa produce `output_with_extgstate.pdf`, que demuestra **agregar transparencia a PDF**, **dibujar rectángulo en PDF** y **guardar PDF con transparencia** todo en un solo flujo.

## Conclusión

Ahora sabe cómo **agregar transparencia a PDF** archivos, **dibujar rectángulo en PDF** y **guardar PDF con transparencia** usando Aspose.PDF for .NET. El proceso gira en torno a crear un `ExtGState` personalizado, aplicarlo al lienzo y persistir los cambios. Con estos bloques de construcción puede extender la técnica a otras formas, múltiples páginas o valores de opacidad dinámicos.

**Próximos pasos**

* Explore otros primitivas de dibujo como `canvas.Ellipse`, `canvas.Path` o `canvas.TextFragment` reutilizando el mismo estado gráfico.
* Combine la transparencia con superposiciones de imágenes para crear marcas de agua (`canvas.Image` + `ExtGState` personalizado).
* Revise la documentación de Aspose.PDF sobre **parámetros del estado gráfico** para efectos de composición avanzados.

¡Feliz codificación y disfrute de la flexibilidad visual que la transparencia aporta a sus flujos de trabajo con PDF!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarle a dominar características adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Cómo crear PDF en C# – Agregar página, dibujar rectángulo y guardar](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [Cómo agregar un objeto línea en PDF usando Aspose.PDF for .NET: Guía paso a paso](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Agregar sellos de imagen a PDFs usando Aspose.PDF for .NET: Guía paso a paso](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}