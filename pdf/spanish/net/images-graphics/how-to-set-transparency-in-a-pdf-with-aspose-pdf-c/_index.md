---
category: general
date: 2026-10-13
description: Aprende cómo establecer la transparencia en un PDF con Aspose.Pdf para
  C#. También ve cómo guardar el PDF modificado y cambiar la alfa de relleno.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set transparency
- save modified pdf
- change fill alpha
- set fill opacity
- edit pdf resources
language: es
lastmod: 2026-10-13
og_description: Cómo establecer la transparencia en un PDF con Aspose.Pdf para C#.
  Sigue esta guía para editar recursos PDF, cambiar la alfa de relleno y guardar archivos
  PDF modificados.
og_image_alt: Screenshot of a PDF page showing transparent graphics applied with Aspose.Pdf
  in C#
og_title: Cómo establecer la transparencia en un PDF con Aspose.Pdf C# – guía paso
  a paso
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  headline: How to set transparency in a PDF with Aspose.Pdf C#
  type: TechArticle
- description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  name: How to set transparency in a PDF with Aspose.Pdf C#
  steps:
  - name: Load the PDF document
    text: '```csharp using Aspose.Pdf; using System.Collections.Generic;'
  - name: Edit PDF resources to add a graphics state
    text: '```csharp // Get the first page (pages are 1‑based) Page firstPage = pdfDocument.Pages[1];'
  - name: Change fill alpha and set fill opacity
    text: '```csharp // Create an empty graphics state dictionary CosPdfDictionary
      newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);'
  - name: Add the new graphics state to the ExtGState dictionary
    text: '```csharp // Register the new state under the name "GS0" extGStateDict.Add("GS0",
      newGraphicsState); ```'
  - name: (Optional) Apply the graphics state in a content stream
    text: 'If you want to draw a rectangle using the new fill opacity, add the following
      after the previous steps:'
  - name: Save modified PDF
    text: '```csharp // Persist the changes to a new file pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
      ```'
  - name: Next steps
    text: '* Explore other blend modes (`Multiply`, `Screen`, etc.) by changing the
      `BM` entry. * Adjust stroke alpha (`CA`) to create semi‑transparent outlines.
      * Combine multiple graphics states to build a library of reusable visual effects.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- Transparency
title: Cómo establecer la transparencia en un PDF con Aspose.Pdf C#
url: /es/net/images-graphics/how-to-set-transparency-in-a-pdf-with-aspose-pdf-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo establecer transparencia en un PDF con Aspose.Pdf C#

Si necesita establecer transparencia en un PDF usando C#, este tutorial muestra los pasos exactos. También aprenderá cómo guardar archivos PDF modificados y cambiar la alfa de relleno sin salir del entorno de Aspose.Pdf.

La guía recorre la carga de un documento, la edición de recursos PDF, la creación de un estado gráfico que define la opacidad de relleno y la persistencia de los cambios. No se requieren herramientas externas; todo se ejecuta dentro de un proyecto .NET estándar.

## Requisitos previos

Antes de comenzar, asegúrese de tener:

* .NET 6.0 o posterior instalado  
* Una licencia válida de Aspose.Pdf para .NET (o una clave de evaluación gratuita)  
* Un archivo PDF de entrada ubicado en un directorio conocido  

Puede agregar el paquete Aspose.Pdf a través de NuGet:

```bash
dotnet add package Aspose.Pdf
```

## Cómo establecer transparencia en un PDF

Esta sección contiene la implementación principal. Cada paso explica **por qué** el código es necesario, no solo **qué** hace.

### Paso 1: Cargar el documento PDF

```csharp
using Aspose.Pdf;
using System.Collections.Generic;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*¿Por qué este paso?*  
`Document` representa el archivo PDF completo en memoria. Abrir el archivo le brinda acceso a páginas, recursos y objetos de bajo nivel que modificará.

### Paso 2: Editar recursos PDF para agregar un estado gráfico

```csharp
// Get the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];

// Create an editor for the page's resource dictionary
DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);

// Retrieve the ExtGState dictionary; it holds graphics state objects
CosPdfDictionary extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
```

*¿Por qué este paso?*  
Las páginas PDF almacenan objetos reutilizables — fuentes, imágenes y estados gráficos — en un diccionario de recursos. La entrada `ExtGState` contiene configuraciones de transparencia. Al editar este diccionario puede introducir un nuevo estado que la página pueda referenciar.

### Paso 3: Cambiar alfa de relleno y establecer opacidad de relleno

```csharp
// Create an empty graphics state dictionary
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the graphics state entries
var graphicsStateEntries = new[]
{
    // Stroke alpha (CA) – fully opaque
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    // Fill alpha (ca) – 50 % transparent
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // Blend mode (BM) – normal composition
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

// Populate the new graphics state
foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*¿Por qué este paso?*  
`ca` controla la **opacidad de relleno**, mientras que `CA` controla la **opacidad del trazo**. Establecer `ca` a `0.5` hace que las formas rellenas sean 50 % transparentes. La entrada `BM` selecciona el modo de fusión; `"Normal"` es la opción más común para transparencia estándar.

### Paso 4: Agregar el nuevo estado gráfico al diccionario ExtGState

```csharp
// Register the new state under the name "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

*¿Por qué este paso?*  
Nombrar el estado gráfico (`"GS0"`) permite que los flujos de contenido en la página lo referencien con el operador `gs`. Después de este registro, la página puede aplicar la transparencia que acaba de definir.

### Paso 5: (Opcional) Aplicar el estado gráfico en un flujo de contenido

Si desea dibujar un rectángulo usando la nueva opacidad de relleno, agregue lo siguiente después de los pasos anteriores:

```csharp
// Create a content stream that uses the new graphics state
string cs = @"
q               % Save graphics state
/GS0 gs         % Apply the graphics state defined earlier
0 0 200 100 re  % Define a rectangle (x, y, width, height)
0.2 0.6 0.8 rg  % Set fill color (RGB)
f               % Fill the rectangle using the current graphics state
Q               % Restore graphics state
";

firstPage.Contents.Add(new Aspose.Pdf.Operator.GsContent(cs));
```

*¿Por qué este paso?*  
Los operadores `q`/`Q` guardan y restauran el estado gráfico, asegurando que la transparencia afecte solo a los comandos de dibujo previstos. El operador `gs` cambia al estado gráfico llamado `"GS0"`.

### Paso 6: Guardar PDF modificado

```csharp
// Persist the changes to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*¿Por qué este paso?*  
Guardar escribe el diccionario de recursos actualizado y cualquier nuevo flujo de contenido en el disco. El archivo resultante (`output.pdf`) contiene el rectángulo transparente definido en el paso anterior.

## Ejemplo completo ejecutable

Uniendo las piezas, aquí hay un programa completo que puede compilar y ejecutar:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using System.Collections.Generic;

class SetTransparencyDemo
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Access the first page and its resources
        Page firstPage = pdfDocument.Pages[1];
        var resourceEditor = new DictionaryEditor(firstPage.Resources);
        var extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();

        // Create a new graphics state with 50 % fill opacity
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var graphicsStateEntries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke alpha
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill alpha
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var entry in graphicsStateEntries)
            newGraphicsState.Add(entry);

        // Register the graphics state as "GS0"
        extGStateDict.Add("GS0", newGraphicsState);

        // Optional: draw a rectangle using the new transparency
        string cs = @"
q
/GS0 gs
0 0 200 100 re
0.2 0.6 0.8 rg
f
Q
";
        firstPage.Contents.Add(new GsContent(cs));

        // Save the modified PDF
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

**Resultado esperado** – `output.pdf` muestra un rectángulo relleno con un color púrpura claro que es 50 % transparente, permitiendo que cualquier contenido de fondo sea parcialmente visible.

## Preguntas comunes y casos límite

* **¿Puedo cambiar la opacidad del trazo en lugar de la opacidad del relleno?**  
  Establezca el valor de `CA` (letras mayúsculas) a un número entre `0` (totalmente transparente) y `1` (totalmente opaco). El ejemplo ya establece `CA` en `1`, lo que significa que los trazos permanecen opacos.

* **¿Qué pasa si la página no tiene ya un diccionario ExtGState?**  
  `resourceEditor["ExtGState"]` creará automáticamente un diccionario vacío. Agregar `"GS0"` funciona de la misma manera.

* **¿El estado gráfico es reutilizable en varias páginas?**  
  Sí. Una vez que agrega la entrada al diccionario de recursos del documento, cualquier página que haga referencia a `"GS0"` heredará la misma configuración de transparencia.

* **¿En qué se diferencia este enfoque de usar la API de alto nivel `Graphics`?**  
  Editar el diccionario de recursos de bajo nivel le brinda un control preciso sobre los internos del PDF y produce archivos más pequeños porque evita incrustar objetos adicionales.

## Conclusión

Ahora sabe **cómo establecer transparencia en un PDF** con Aspose.Pdf para C#. El tutorial cubrió la edición de recursos PDF, el cambio de alfa de relleno, la configuración de opacidad de relleno y el guardado del PDF modificado. Con esta base puede experimentar con diferentes modos de fusión, aplicar transparencia al texto o crear estados gráficos reutilizables para documentos complejos.

### Próximos pasos

* Explore otros modos de fusión (`Multiply`, `Screen`, etc.) cambiando la entrada `BM`.  
* Ajuste la alfa del trazo (`CA`) para crear contornos semi‑transparentes.  
* Combine varios estados gráficos para crear una biblioteca de efectos visuales reutilizables.  

¡Siéntase libre de compartir sus resultados o hacer preguntas en los comentarios! ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarle a dominar características adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [How to Customize PDFs with Aspose.PDF for .NET&#58; Set Page Margins and Draw Lines](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [How to Set Image Size in a PDF Using Aspose-PDF for .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [How to Set PDF Permissions Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/security-permissions/set-pdf-privileges-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}