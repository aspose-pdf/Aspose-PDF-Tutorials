---
category: general
date: 2026-08-20
description: Crea un estado gráfico personalizado en PDF con Aspose.Pdf. Aprende cómo
  editar los recursos PDF y agregar transparencia al PDF en solo unos pocos pasos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom graphics state
- edit pdf resources
- add transparency pdf
- Aspose.Pdf graphics state
- PDF resource dictionary
language: es
lastmod: 2026-08-20
og_description: Cree un estado gráfico personalizado en PDF con Aspose.Pdf. Este tutorial
  muestra cómo editar recursos PDF y agregar transparencia PDF rápidamente.
og_image_alt: Screenshot of C# code that creates a custom graphics state in a PDF
og_title: Crear estado gráfico personalizado en PDF – Guía de Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create custom graphics state in PDF with Aspose.Pdf. Learn how to edit
    PDF resources and add transparency PDF in just a few steps.
  headline: Create custom graphics state in PDF using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- Aspose.Pdf
- C#
- Graphics state
title: Crear estado gráfico personalizado en PDF usando Aspose.Pdf
url: /es/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear estado gráfico personalizado en PDF usando Aspose.Pdf

Si necesitas **crear un estado gráfico personalizado** en un PDF, esta guía te muestra exactamente cómo hacerlo con Aspose.Pdf para .NET. Al final del tutorial podrás **editar recursos PDF**, inyectar un nuevo diccionario de estado gráfico y **añadir contenido PDF con transparencia** sin salir de tu proyecto C#.

Verás un ejemplo completo y ejecutable, una explicación de por qué cada línea es importante y consejos para manejar documentos de varias páginas o diferentes modos de fusión. No se requieren herramientas externas, solo la biblioteca Aspose.Pdf y un entorno básico de desarrollo .NET.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* .NET 6.0 o posterior (el código también funciona con .NET Framework 4.7+)
* Una copia con licencia de **Aspose.Pdf for .NET** (la versión de prueba gratuita sirve para pruebas)
* Un archivo PDF de entrada llamado `input.pdf` colocado en una carpeta que puedas referenciar desde el código
* Visual Studio 2022 o cualquier IDE que soporte desarrollo en C#

El tutorial asume que estás familiarizado con la sintaxis básica de C# y el concepto de páginas PDF.

## Paso 1: Cargar el PDF de origen y acceder a la primera página

La primera operación es abrir el archivo PDF y obtener la página cuyos recursos deseas modificar. Aspose.Pdf representa cada página como un objeto `Page`, y cada página contiene un **diccionario de recursos** que almacena estados gráficos, fuentes, XObjects y más.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

// Load the PDF you want to edit
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Get the first page (pages are 1‑based in Aspose.Pdf)
    Page firstPage = pdfDocument.Pages[1];
```

*Por qué es importante:* La clase `Document` carga el archivo en memoria, y `Pages[1]` te brinda acceso directo al diccionario de recursos de la primera página, que es donde reside un estado gráfico.

## Paso 2: Abrir el diccionario de recursos para editar

Aspose.Pdf proporciona un asistente `DictionaryEditor` que te permite tratar un diccionario de recursos como un `Dictionary` regular de .NET. Esto facilita leer, agregar o reemplazar entradas como `ExtGState`.

```csharp
    // Create an editor for the page’s resources
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Por qué es importante:* `DictionaryEditor` abstrae los objetos COS de bajo nivel, permitiéndote trabajar con pares clave/valor familiares mientras mantienes la conformidad del PDF.

## Paso 3: Recuperar (o crear) el diccionario ExtGState

La entrada **ExtGState** contiene todos los objetos de estado gráfico externo para la página. Si el diccionario no existe, Aspose.Pdf creará uno vacío por ti.

```csharp
    // Ensure the ExtGState dictionary exists
    var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
        ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
        : new CosPdfDictionary(pdfDocument);
```

*Por qué es importante:* Una entrada `ExtGState` ausente provocaría una `KeyNotFoundException` más adelante. Esta protección permite que el código funcione con PDFs que nunca han definido un estado gráfico personalizado antes, una parte esencial de la robustez al **editar recursos PDF**.

## Paso 4: Construir el diccionario de estado gráfico personalizado

Un estado gráfico describe cómo se renderizan las operaciones de dibujo. Para **añadir transparencia PDF**, necesitas establecer las entradas `ca` (opacidad de relleno) y `CA` (opacidad de trazo), y opcionalmente un modo de fusión (`BM`). El siguiente código construye un nuevo diccionario con esos parámetros.

```csharp
    // Create an empty dictionary that will become the new graphics state
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Define the parameters you want for the custom state
    var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
    {
        // Stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        // Fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        // Blend mode – "Normal" is the default, but you can use "Multiply", "Screen", etc.
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };

    // Populate the dictionary with the parameters
    foreach (var param in graphicsStateParams)
        newGraphicsState.Add(param);
```

*Por qué es importante:* Las entradas `ca` y `CA` controlan la transparencia para las operaciones de relleno y trazo, respectivamente. Configurar `BM` te permite experimentar con diferentes efectos de composición, lo cual es útil cuando más adelante **añades contenido PDF con transparencia** como formas o imágenes semitransparentes.

## Paso 5: Registrar el nuevo estado gráfico bajo un nombre único

Cada estado gráfico en el diccionario `ExtGState` debe tener un nombre único (p. ej., `GS0`, `GS1`). Puedes elegir cualquier nombre que no entre en conflicto con entradas existentes.

```csharp
    // Choose a name that is unlikely to collide with existing states
    const string graphicsStateName = "GS0";

    // Add the new graphics state to the ExtGState dictionary
    extGStateDict.Add(graphicsStateName, newGraphicsState);

    // If the ExtGState entry was missing, attach it back to the page resources
    if (!resourcesEditor.ContainsKey("ExtGState"))
        resourcesEditor["ExtGState"] = extGStateDict;
```

*Por qué es importante:* Al insertar el nuevo diccionario bajo `GS0`, haces que el estado sea direccionable desde los flujos de contenido de la página. El bloque condicional asegura que la entrada `ExtGState` esté presente incluso en PDFs que comenzaron sin ella, otra medida de seguridad al **editar recursos PDF**.

## Paso 6: Usar el estado gráfico personalizado en el contenido de la página (opcional)

Los pasos anteriores solo *definen* el estado gráfico. Para ver realmente el efecto, debes referenciarlo en el flujo de contenido de la página. A continuación hay un ejemplo rápido que dibuja un rectángulo semitransparente usando el estado que acabamos de crear.

```csharp
    // Get the page’s content stream (or create a new one if empty)
    var content = firstPage.Contents[1];
    var graphics = new ContentWriter(content);

    // Save current graphics state
    graphics.WriteOperator(OperatorName.SaveState);
    // Set the custom graphics state we just defined
    graphics.WriteOperand($"/{graphicsStateName}");
    graphics.WriteOperator(OperatorName.SetExtGState);
    // Draw a rectangle (coordinates are in points)
    graphics.WriteOperand(100);   // lower‑left x
    graphics.WriteOperand(500);   // lower‑left y
    graphics.WriteOperand(200);   // width
    graphics.WriteOperand(100);   // height
    graphics.WriteOperator(OperatorName.Rectangle);
    // Fill the rectangle using the current fill opacity (ca = 0.5)
    graphics.WriteOperator(OperatorName.Fill);
    // Restore the previous graphics state
    graphics.WriteOperator(OperatorName.RestoreState);
```

*Por qué es importante:* El operador `SetExtGState` (`gs`) indica al renderizador PDF que aplique los parámetros definidos en `GS0`. El rectángulo aparecerá con un 50 % de opacidad de relleno mientras su trazo permanece totalmente opaco.

## Paso 7: Guardar el PDF modificado

Finalmente, escribe los cambios de vuelta al disco. Puedes sobrescribir el archivo original o crear uno nuevo.

```csharp
    // Save the updated PDF
    pdfDocument.Save("YOUR_DIRECTORY/output_with_custom_gs.pdf");
}
```

Cuando abras `output_with_custom_gs.pdf` en un visor de PDF, deberías ver un rectángulo semitransparente en la primera página. Esto confirma que has creado correctamente un **estado gráfico personalizado**, **editado recursos PDF** y **añadido contenido PDF con transparencia**.

## Variaciones comunes y casos límite

| Situación | Qué ajustar |
|-----------|-------------|
| **Varias páginas necesitan el mismo estado** | Registrar el estado gráfico una sola vez (pasos 1‑5) y referenciar `GS0` en el flujo de contenido de cualquier página. |
| **Opacidad diferente por elemento** | Definir estados adicionales (`GS1`, `GS2`, …) con diferentes valores `ca`/`CA` y cambiar entre ellos usando `SetExtGState`. |
| **Modo de fusión distinto a Normal** | Reemplazar `"Normal"` por `"Multiply"`, `"Screen"` o cualquier modo de fusión estándar de PDF en la entrada `BM`. |
| **Colisión de nombres** | Antes de agregar, verifica `extGStateDict.ContainsKey(yourName)` y elige un sufijo único si es necesario. |
| **El PDF ya contiene un diccionario ExtGState** | El código en el Paso 3 ya reutiliza el diccionario existente, por lo que no se requiere manejo adicional. |

**Consejo profesional:** Cuando trabajes con PDFs grandes, envuelve el uso de `Document` en un bloque `using` (como se muestra) para liberar los recursos nativos rápidamente. Además, considera habilitar la propiedad `PdfCompliance` de Aspose.Pdf si necesitas garantizar la conformidad PDF/A o PDF/X después de editar los recursos.

## Ejemplo completo funcional

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Load the PDF you want to edit
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 1: Get the first page
            Page firstPage = pdfDocument.Pages[1];

            // Step 2: Open the page resources for editing
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 3: Retrieve or create the ExtGState dictionary
            var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
                ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
                : new CosPdfDictionary(pdfDocument);

            // Step 4: Build a custom graphics state (50 % fill opacity, 100 % stroke opacity)
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var param in graphicsStateParams)
                newGraphicsState.Add(param);

            // Step 5: Register the graphics state under the name GS0
            const string graphicsStateName = "GS0";
            extGStateDict.Add(graphicsStateName, newGraphics


## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo crear PDF con Aspose – Añadir campo de formulario y páginas](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Cómo crear tablas personalizadas en PDFs usando Aspose.PDF .NET](/pdf/english/net/tables-lists/create-custom-tables-in-pdfs-aspose-pdf-dot-net/)
- [Crear sellos PDF personalizados Aspose Pdf Net](/pdf/hongkong/net/images-graphics/create-custom-pdf-stamps-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}