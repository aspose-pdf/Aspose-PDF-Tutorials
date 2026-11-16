---
category: general
date: 2026-11-16
description: Aprende cómo crear el estado gráfico de PDF en C# usando Aspose.Pdf.
  Esta guía cubre la opacidad, el modo de fusión y un ejemplo completo de código.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf graphics state
- Aspose.Pdf ExtGState
- PDF opacity
- C# PDF manipulation
- PDF blend mode
- Aspose.Pdf graphics state
language: es
lastmod: 2026-11-16
og_description: Crea el estado gráfico de PDF en C# con Aspose.Pdf. Sigue este tutorial
  completo para establecer la opacidad y el modo de fusión programáticamente.
og_image_alt: Illustration of how to create PDF graphics state with Aspose.Pdf in
  C#
og_title: Crear estado gráfico de PDF en C# – guía paso a paso de Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to create PDF graphics state in C# using Aspose.Pdf. This
    guide covers opacity, blend mode, and full code example.
  headline: How to create PDF graphics state in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF
title: Cómo crear el estado gráfico de PDF en C# con Aspose.Pdf
url: /es/net/images-graphics/how-to-create-pdf-graphics-state-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear un estado gráfico PDF en C# con Aspose.Pdf

Si necesitas **crear un estado gráfico PDF** en un proyecto .NET, este tutorial te muestra exactamente cómo hacerlo con Aspose.Pdf. Ya sea que quieras controlar la opacidad, cambiar el modo de fusión o reutilizar un estado gráfico personalizado en varias páginas, los pasos a continuación te ofrecen una solución completa y lista para ejecutar.

En esta guía aprenderás a acceder a los recursos de la página, añadir una entrada **ExtGState** y guardar los cambios en un nuevo archivo. El ejemplo funciona con Aspose.Pdf 23.12 (o posterior) y está dirigido a .NET 6+, aunque los conceptos también se aplican a versiones anteriores.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* Visual Studio 2022 (o cualquier IDE de C#) con el SDK de .NET 6 instalado.  
* Una licencia de Aspose.Pdf para .NET o una clave de evaluación temporal.  
* Un archivo PDF llamado `input.pdf` ubicado en una carpeta a la que puedas referenciar desde el código.  

No se requieren paquetes NuGet adicionales más allá de `Aspose.Pdf`.

## Qué cubre el tutorial

* Cargar un documento PDF existente.  
* Navegar al diccionario de recursos de la primera página.  
* Crear un nuevo diccionario de estado gráfico que define la opacidad del trazo (`CA`), la opacidad del relleno (`ca`) y el modo de fusión (`BM`).  
* Añadir el nuevo estado gráfico a la colección **ExtGState** con un nombre personalizado (`GS0`).  
* Guardar el PDF actualizado para que los comandos de dibujo posteriores puedan referenciar el nuevo estado.

Al final del tutorial podrás **crear objetos de estado gráfico PDF** de forma programática y reutilizarlos en cualquier operación de dibujo.

## Paso 1: Configurar el proyecto e importar espacios de nombres

Crea una nueva aplicación de consola (o integra el código en un proyecto existente). Añade la referencia a Aspose.Pdf e incluye los espacios de nombres necesarios:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Generator;
```

> **Consejo profesional:** Si utilizas la versión de evaluación gratuita, agrega `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` antes de cargar el documento para evitar mensajes de marca de agua.

## Paso 2: Cargar el documento PDF

Abrir el archivo es sencillo. La clase `Document` representa todo el PDF y te brinda acceso a sus páginas y recursos.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";

using (var document = new Document(inputPath))
{
    // All subsequent steps run inside this using block
```

Colocar el código dentro de un bloque `using` garantiza que el manejador del archivo se libere después de la operación, lo cual es esencial para la **manipulación de PDF en C#** en entornos de producción.

## Paso 3: Recuperar el diccionario de recursos de la primera página

Cada página PDF tiene un diccionario *Resources* que almacena fuentes, imágenes y estados gráficos. Necesitamos un `DictionaryEditor` para editar esa estructura.

```csharp
    // Step 3: Get the first page and its resources dictionary
    var page = document.Pages[1];
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

Si el PDF ya contiene una entrada `ExtGState`, `resourcesEditor["ExtGState"]` la devolverá; de lo contrario, Aspose.Pdf crea un diccionario vacío para nosotros cuando añadimos la primera entrada.

## Paso 4: Acceder o crear el diccionario ExtGState

El diccionario **ExtGState** contiene objetos de estado gráfico con nombre. Obtendremos uno existente o crearemos un nuevo contenedor.

```csharp
    // Step 4: Access (or create) the ExtGState dictionary within the resources
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

Cuando `ExtGState` no existe, `resourcesEditor["ExtGState"]` devuelve automáticamente un nuevo diccionario vacío, asegurando que el código funcione con cualquier PDF.

## Paso 5: Construir el nuevo diccionario de estado gráfico

Un estado gráfico es un `CosPdfDictionary` con claves específicas:

* `CA` – opacidad del trazo (0‑1)  
* `ca` – opacidad del relleno (0‑1)  
* `BM` – modo de fusión (`Normal`, `Multiply`, etc.)

Creamos un diccionario vacío, lo rellenamos y luego lo añadimos a `ExtGState`.

```csharp
    // Step 5: Create a new graphics state dictionary with desired parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (50% transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };

    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

Puedes cambiar `0.5` por cualquier valor entre `0` y `1` para ajustar la opacidad del relleno, o reemplazar `"Normal"` por `"Multiply"` para usar un **modo de fusión PDF** diferente. Esta flexibilidad es la razón por la que crear un estado gráfico personalizado es una técnica poderosa en la gestión de **estados gráficos en Aspose.Pdf**.

## Paso 6: Registrar el estado gráfico con un nombre

Los flujos de contenido PDF hacen referencia a los estados gráficos por nombre. Aquí usamos `GS0`, pero cualquier nombre único funciona.

```csharp
    // Step 6: Add the new graphics state to the ExtGState dictionary with a name (e.g., GS0)
    extGState.Add("GS0", newGraphicsState);
```

Si necesitas varios estados, repite el paso de creación con diferentes parámetros y añádelos como `GS1`, `GS2`, etc. Este patrón escala bien para documentos complejos que requieren distintas configuraciones de opacidad o fusión en diferentes capas.

## Paso 7: Guardar el PDF modificado

Finalmente, escribe el documento actualizado en un nuevo archivo. Mantener el original intacto facilita la depuración.

```csharp
    // Step 7: Save the updated PDF document
    string outputPath = @"YOUR_DIRECTORY\output.pdf";
    document.Save(outputPath);
}
```

Tras la ejecución, `output.pdf` contiene una entrada `ExtGState` llamada `GS0`. Cualquier operador de dibujo posterior puede referenciarla usando el operador `gs` (p. ej., `GS0 gs` en un flujo de contenido).  

> **Por qué es importante:** Al crear un estado gráfico reutilizable evitas repetir configuraciones de opacidad y fusión en cada comando de dibujo, lo que mejora tanto el rendimiento como la mantenibilidad.

## Usar el nuevo estado gráfico en un flujo de contenido (opcional)

Si deseas ver el efecto de inmediato, puedes añadir un rectángulo simple que utilice el estado que acabamos de crear:

```csharp
using (var document = new Document(outputPath))
{
    var page = document.Pages[1];
    var content = page.Contents[1]; // Get the first content stream

    // Insert graphics state selection and a semi‑transparent rectangle
    var operators = new List<Operator>
    {
        new Operator("GS0", "gs"),                     // Select our custom graphics state
        new Operator("0.5", "w"),                      // Set line width (optional)
        new Operator("100", "100", "200", "150", "re"), // Rectangle (x, y, width, height)
        new Operator("B")                              // Stroke the rectangle
    };

    foreach (var op in operators)
        content.Operators.Add(op);

    document.Save(@"YOUR_DIRECTORY\final_output.pdf");
}
```

El rectángulo se dibujará con un 50 % de opacidad de relleno mientras que el trazo permanecerá totalmente opaco, tal como se definió en el diccionario **create PDF graphics state**.

## Problemas comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| Entrada `ExtGState` no encontrada | Algunos PDFs omiten el diccionario por completo. | El `DictionaryEditor` lo crea automáticamente al añadir la primera entrada, por lo que no se necesita una verificación adicional. |
| Valores de opacidad > 1 o < 0 | La especificación PDF limita la opacidad al rango `[0,1]`. | Limita los valores antes de crear `CosPdfNumber`. |
| Error tipográfico en el modo de fusión | Los nombres de los modos de fusión son sensibles a mayúsculas y minúsculas. | Usa nombres exactos como `"Normal"`, `"Multiply"`, `"Screen"`. |
| Marca de agua de licencia | La versión de evaluación añade una marca de agua en la primera página. | Aplica un archivo de licencia válido antes de abrir el documento. |

Abordar estos casos límite garantiza que tu implementación de **create PDF graphics state** funcione de manera fiable con diferentes fuentes PDF.

## Ejemplo completo y ejecutable

A continuación tienes un programa autónomo que puedes copiar, pegar y ejecutar. Sustituye `YOUR_DIRECTORY` por la ruta real de una carpeta en tu máquina.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;

class Program
{
    static void Main()
    {
        // Opcional: aplicar licencia para eliminar la marca de agua de evaluación
        // var license = new Aspose.Pdf.License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        using (var document = new Document(inputPath))
        {
            // 1️⃣ Obtener la primera página y sus recursos
            var page = document.Pages[1];
            var resourcesEditor = new DictionaryEditor(page.Resources);

            // 2️⃣ Acceder (o crear) al diccionario ExtGState
            var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // 3️⃣ Construir nuevo estado gráfico
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Opacidad del trazo
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Opacidad del relleno
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Modo de fusión
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // 4️⃣ Registrar el estado con un nombre (GS0)
            extGState.Add("


## ¿Qué deberías aprender a continuación?


Los tutoriales siguientes cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funcionalidades adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Create custom graphics state in PDF using Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Add graphics state to PDF using Aspose.PDF for .NET (C#)](/pdf/english/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/)
- [How to create empty graphics state in a PDF with C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}