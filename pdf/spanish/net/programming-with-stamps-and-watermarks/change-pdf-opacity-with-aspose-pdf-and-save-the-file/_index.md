---
category: general
date: 2026-11-12
description: Aprende a cambiar la opacidad de un PDF usando Aspose.Pdf, agregar transparencia,
  establecer el modo de fusión y guardar el PDF modificado en C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF opacity
- how to add transparency
- save modified PDF
- how to set blend mode
- set fill opacity
language: es
lastmod: 2026-11-12
og_description: Cambia la opacidad de PDF con Aspose.Pdf, aprende cómo añadir transparencia,
  establecer el modo de fusión y guardar archivos PDF modificados en C#.
og_image_alt: Screenshot of a PDF page with altered opacity using Aspose.Pdf
og_title: Cambiar la opacidad del PDF con Aspose.Pdf – agregar transparencia y guardar
schemas:
- author: Aspose
  dateModified: '2026-11-12'
  description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  headline: Change PDF opacity with Aspose.Pdf and save the file
  type: TechArticle
- description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  name: Change PDF opacity with Aspose.Pdf and save the file
  steps:
  - name: Load the PDF document
    text: Start by creating a `Document` instance that points to your source file.
      The constructor reads the entire PDF into memory, allowing you to manipulate
      its internal objects.
  - name: Access the first page’s resources
    text: Each PDF page stores a *resource dictionary* that holds objects such as
      fonts, images, and graphics states. You need to edit this dictionary to inject
      a new `ExtGState` entry.
  - name: Ensure an ExtGState dictionary exists
    text: The `ExtGState` dictionary holds custom graphics states. If it does not
      exist, the code creates one automatically.
  - name: Define a new graphics state (ExtGState)
    text: A graphics state defines how drawing operations behave. The following dictionary
      sets stroke opacity (`CA`), fill opacity (`ca`), and blend mode (`BM`).
  - name: Register the graphics state in the resource dictionary
    text: Give the new state a name (e.g., `GS0`) and add it to the `ExtGState` dictionary.
      This name will be referenced later in the page content stream.
  - name: Apply the graphics state to page content
    text: To actually see the opacity effect, insert the `/GS0 gs` operator before
      the drawing commands you want to affect. The example below draws a semi‑transparent
      rectangle.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The `Save` method overwrites
      the target file or creates a new one if it does not exist.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Cambiar la opacidad del PDF con Aspose.Pdf y guardar el archivo
url: /es/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-and-save-the-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cambiar la opacidad del PDF con Aspose.Pdf y guardar el archivo

Si necesita **cambiar la opacidad del PDF** en un documento, Aspose.Pdf proporciona una API sencilla para ajustar tanto la transparencia del trazo como del relleno. Este tutorial muestra exactamente **cómo añadir transparencia**, **cómo establecer el modo de fusión**, y **guardar archivos PDF modificados** con solo unas pocas líneas de código C#.

Recorrerá cada paso—desde cargar un PDF existente hasta definir un nuevo estado gráfico y persistir los cambios. Al final de esta guía podrá:

* Reducir la visibilidad de gráficos vectoriales o imágenes.
* Aplicar un modo de fusión personalizado como *Normal* o *Multiply*.
* Exportar el archivo actualizado sin perder ningún otro contenido.

El único requisito previo es un entorno de desarrollo .NET funcional y una referencia a la biblioteca Aspose.Pdf (versión 23.9 o posterior). No se requieren herramientas externas.

## Requisitos previos

| Requisito | Por qué es importante |
|-------------|----------------|
| .NET 6.0 SDK or later | Garantiza la compatibilidad con las últimas APIs de Aspose.Pdf. |
| Aspose.Pdf for .NET NuGet package | Proporciona las clases `Document`, `CosPdfDictionary` y relacionadas usadas en el código. |
| A PDF file to edit (e.g., `input.pdf`) | Sirve como fuente para los cambios de opacidad. |

Instale el paquete NuGet con:

```bash
dotnet add package Aspose.Pdf
```

## Cambiar la opacidad del PDF con Aspose.Pdf

### Paso 1: Cargar el documento PDF

Comience creando una instancia de `Document` que apunte a su archivo de origen. El constructor lee todo el PDF en memoria, lo que le permite manipular sus objetos internos.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;

// Load the existing PDF
var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");
```

> **¿Por qué este paso?** Cargar el archivo crea un modelo de objetos manipulable. Todos los cambios posteriores operan sobre esta representación en memoria, asegurando que el archivo original permanezca intacto hasta que lo guarde explícitamente.

### Paso 2: Acceder a los recursos de la primera página

Cada página PDF almacena un *diccionario de recursos* que contiene objetos como fuentes, imágenes y estados gráficos. Necesita editar este diccionario para inyectar una nueva entrada `ExtGState`.

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor simplifies access to the page's resource dictionary
var resourcesEditor = new DictionaryEditor(page.Resources);
```

> **Consejo:** Si su PDF contiene varias páginas que necesitan la misma opacidad, repita este paso para cada página o comparta un único `ExtGState` entre páginas.

### Paso 3: Asegurar que exista un diccionario ExtGState

El diccionario `ExtGState` contiene estados gráficos personalizados. Si no existe, el código crea uno automáticamente.

```csharp
// Get or create the ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                     ?? new CosPdfDictionary(pdfDoc);
resourcesEditor["ExtGState"] = extGStateDict;
```

> **¿Por qué este paso?** Sin un contenedor `ExtGState`, cualquier intento de referenciar un nuevo estado gráfico fallaría, lo que resultaría en un PDF que ignora sus configuraciones de opacidad.

### Paso 4: Definir un nuevo estado gráfico (ExtGState)

Un estado gráfico define cómo se comportan las operaciones de dibujo. El siguiente diccionario establece la opacidad del trazo (`CA`), la opacidad del relleno (`ca`) y el modo de fusión (`BM`).

```csharp
// Create an empty dictionary for the new graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Set desired parameters
var parameters = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (1 = opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (0.5 = 50% transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var param in parameters)
    newGraphicsState.Add(param);
```

> **Cómo establecer la opacidad del relleno:** La entrada `ca` controla la opacidad de las formas rellenas (texto, rutas). Ajuste el valor numérico entre `0` (totalmente transparente) y `1` (totalmente opaco) según los requisitos de su diseño.

> **Cómo establecer el modo de fusión:** La entrada `BM` selecciona el algoritmo de composición. Los valores comunes incluyen `Normal`, `Multiply`, `Screen` y `Overlay`. Elija el que coincida con su intención visual.

### Paso 5: Registrar el estado gráfico en el diccionario de recursos

Asigne al nuevo estado un nombre (p. ej., `GS0`) y agréguelo al diccionario `ExtGState`. Este nombre será referenciado más adelante en el flujo de contenido de la página.

```csharp
// Add the graphics state with a symbolic name
extGStateDict.Add("GS0", newGraphicsState);
```

> **Consejo profesional:** Use una convención de nombres como `GS0`, `GS1`, … al crear múltiples estados. Previene colisiones de nombres y facilita la depuración.

### Paso 6: Aplicar el estado gráfico al contenido de la página

Para ver realmente el efecto de opacidad, inserte el operador `/GS0 gs` antes de los comandos de dibujo que desea afectar. El ejemplo a continuación dibuja un rectángulo semitransparente.

```csharp
// Build a content stream that uses the new graphics state
var content = new MemoryStream();
var writer = new StreamWriter(content);

// Activate the graphics state
writer.WriteLine("q");                 // Save graphics state
writer.WriteLine("/GS0 gs");           // Apply custom ExtGState
writer.WriteLine("0.2 0.5 0.8 rg");    // Set fill color (RGB)
writer.WriteLine("100 500 200 100 re"); // Rectangle (x y width height)
writer.WriteLine("f");                 // Fill rectangle
writer.WriteLine("Q");                 // Restore graphics state
writer.Flush();

content.Position = 0;
page.Contents.Add(new ContentStream(content));
```

> **¿Por qué los operadores `q` y `Q`?** Empujan y sacan de la pila de estados gráficos, asegurando que el cambio de opacidad solo afecte al rectángulo y no al resto de la página.

### Paso 7: Guardar el PDF modificado

Finalmente, escriba el documento actualizado en disco. El método `Save` sobrescribe el archivo de destino o crea uno nuevo si no existe.

```csharp
// Persist the changes
pdfDoc.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **Cómo guardar el PDF modificado:** La llamada `Save` escribe todas las modificaciones en memoria, incluido el nuevo `ExtGState`, en la ruta especificada. También puede transmitir el resultado a un `MemoryStream` para respuestas web.

## Ejemplo completo en funcionamiento

A continuación se muestra un programa único y autocontenido que incorpora cada paso descrito arriba. Cópielo en una aplicación de consola y ejecútelo para verificar el cambio de opacidad.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Operators;

class ChangePdfOpacityDemo
{
    static void Main()
    {
        // 1. Load the PDF
        var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");

        // 2. Get first page and its resources
        var page = pdfDoc.Pages[1];
        var resourcesEditor = new DictionaryEditor(page.Resources);

        // 3. Ensure ExtGState dictionary exists
        var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                             ?? new CosPdfDictionary(pdfDoc);
        resourcesEditor["Ext


## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarle a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Cómo guardar PDF modificado con Aspose.Pdf y añadir transparencia](/pdf/english/net/document-manipulation/how-to-save-modified-pdf-with-aspose-pdf-and-add-transparenc/)
- [Cómo añadir transparencia a PDF usando Aspose.PDF en C#](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [Cómo añadir estado gráfico PDF y controlar la transparencia con Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}