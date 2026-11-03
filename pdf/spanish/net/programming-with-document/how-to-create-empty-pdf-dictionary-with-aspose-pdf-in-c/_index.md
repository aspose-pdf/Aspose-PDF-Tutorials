---
category: general
date: 2026-09-18
description: Aprende a crear un diccionario PDF vacío en C# usando Aspose.PDF. Esta
  guía paso a paso cubre ExtGState, el estado gráfico y la manipulación de CosPdfDictionary.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.PDF
- ExtGState dictionary
- graphics state
- CosPdfDictionary
- PDF manipulation C#
language: es
lastmod: 2026-09-18
og_description: Crea un diccionario PDF vacío en C# con Aspose.PDF. Sigue este tutorial
  completo para editar los diccionarios ExtGState y de estado gráfico.
og_image_alt: Screenshot showing creation of an empty PDF dictionary in C#
og_title: Crear un diccionario PDF vacío en C# – guía completa de Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn to create empty PDF dictionary in C# using Aspose.PDF. This step‑by‑step
    guide covers ExtGState, graphics state, and CosPdfDictionary manipulation.
  headline: How to create empty PDF dictionary with Aspose.PDF in C#
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: Cómo crear un diccionario PDF vacío con Aspose.PDF en C#
url: /es/net/programming-with-document/how-to-create-empty-pdf-dictionary-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear un diccionario PDF vacío con Aspose.PDF en C#

Si necesitas **crear un diccionario PDF vacío** mientras procesas un archivo PDF, esta guía te muestra exactamente cómo hacerlo usando Aspose.PDF para .NET. Ya sea que estés ajustando la transparencia, los modos de fusión o cualquier estado gráfico personalizado, los pasos a continuación te permiten editar el diccionario `ExtGState` de forma segura y eficiente.

En este tutorial aprenderás a:

* Cargar un documento PDF con Aspose.PDF.
* Acceder a los recursos de la primera página y al diccionario `ExtGState` existente.
* Construir un nuevo `CosPdfDictionary` vacío y rellenarlo con entradas de estado gráfico.
* Guardar el PDF modificado sin perder ningún contenido original.

La solución funciona con cualquier PDF que contenga al menos una página y solo requiere la biblioteca Aspose.PDF (versión 23.10 o posterior).

## Requisitos previos

* .NET 6.0 o posterior (el código también se ejecuta en .NET Framework 4.8).
* Una referencia al paquete NuGet **Aspose.PDF**.
* Un archivo PDF de entrada ubicado en `YOUR_DIRECTORY/input.pdf`.
* Familiaridad básica con C# y conceptos de PDF como recursos y estado gráfico.

> **Consejo profesional:** Cuando trabajes con PDFs grandes, envuelve el objeto `Document` en un bloque `using` para garantizar que todos los manejadores de archivo se liberen rápidamente.

## Paso 1: Cargar el documento PDF

La primera operación abre el archivo fuente. Aspose.PDF lee todo el documento en memoria, lo que te permite editar los objetos internos.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

*Por qué es importante*: Cargar el documento crea un modelo de objetos mutable. Sin este paso no puedes acceder a los recursos de la página necesarios para manipular el diccionario.

## Paso 2: Recuperar los recursos de la primera página

Cada página almacena un diccionario `Resources` que contiene fuentes, imágenes y estados gráficos. Acceder a él te proporciona un `DictionaryEditor` que simplifica las operaciones de lectura/escritura.

```csharp
// Step 2: Get the resources of the first page
Page firstPage = pdfDocument.Pages[1];
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Por qué es importante*: El diccionario `ExtGState` se encuentra dentro de los recursos de la página. Editar el diccionario incorrecto no tendría efecto en el renderizado.

## Paso 3: Ubicar el diccionario ExtGState existente

La entrada `ExtGState` puede ya contener objetos de estado gráfico. La obtenemos como un `CosPdfDictionary` para poder añadir nuevas entradas.

```csharp
// Step 3: Access the existing ExtGState dictionary
CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

Si la entrada `ExtGState` no existe, Aspose.PDF crea automáticamente un diccionario vacío cuando asignas uno nuevo más adelante.

## Paso 4: **Crear diccionario PDF vacío** para un nuevo estado gráfico

Aquí construimos un `CosPdfDictionary` completamente nuevo—el núcleo de la operación **create empty PDF dictionary**. Luego lo rellenamos con claves estándar de estado gráfico:

* `CA` – opacidad del trazo.
* `ca` – opacidad del relleno.
* `BM` – modo de fusión.

```csharp
// Step 4: Create a new graphics state dictionary and define its entries
CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

KeyValuePair<string, ICosPdfPrimitive>[] graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),          // Stroke opacity
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),       // Fill opacity
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))    // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

*Por qué es importante*: Al definir explícitamente cada entrada, controlas cómo los objetos de la página se mezclan y renderizan. El diccionario está **vacío** hasta que añades estas claves, lo que satisface el requisito de **create empty PDF dictionary** antes de poblarlo.

## Paso 5: Añadir el nuevo estado gráfico al diccionario ExtGState

Cada estado gráfico debe tener un nombre único (p. ej., `GS0`). Insertamos el diccionario recién creado bajo ese nombre.

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary with a unique name
extGStateDict.Add("GS0", graphicsStateDict);
```

Si necesitas varios estados, sigue añadiendo entradas como `GS1`, `GS2`, etc., asegurándote de que cada nombre sea único dentro del diccionario `ExtGState`.

## Paso 6: Guardar el documento PDF actualizado

Finalmente, escribe los cambios en disco. El archivo original permanece intacto porque guardamos en una ruta nueva.

```csharp
// Step 6: Save the updated PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

El `output.pdf` resultante ahora contiene un estado gráfico adicional (`GS0`) que puedes referenciar desde cualquier flujo de contenido de página usando el operador `/GS0`.

## Ejemplo completo

Unir todos los pasos produce un programa autónomo que puedes ejecutar de inmediato.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources
            Page firstPage = pdfDocument.Pages[1];
            DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Get (or create) ExtGState dictionary
            CosPdfDictionary extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Build a new empty PDF dictionary for graphics state
            CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var entry in entries)
                graphicsStateDict.Add(entry);

            // Insert the new graphics state with a unique name
            extGStateDict.Add("GS0", graphicsStateDict);

            // Save the modified document
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

**Salida esperada**: Después de ejecutar el programa, `output.pdf` contiene el mismo contenido visual que `input.pdf`. Al inspeccionar el PDF con una herramienta como Adobe Acrobat o PDF‑Tron verás una nueva entrada `GS0` bajo el diccionario `ExtGState` de la primera página.

## Variaciones comunes y casos límite

| Situación | Qué ajustar |
|-----------|-------------|
| **No hay entrada ExtGState existente** | Reemplaza `resourcesEditor["ExtGState"]` por `new CosPdfDictionary(pdfDocument)` y asígnalo de nuevo a `firstPage.Resources["ExtGState"]`. |
| **Varias páginas necesitan el mismo estado** | Añade la misma entrada `GS0` al `ExtGState` de cada página, o referencia el diccionario desde un objeto de recursos compartido. |
| **Modo de fusión diferente** | Cambia el valor de `CosPdfName` de `"Normal"` a `"Multiply"`, `"Screen"`, etc., según el efecto deseado. |
| **Valores de opacidad más altos** | Usa `new CosPdfNumber(0.8)` para `ca` o `CA` para incrementar la opacidad de relleno o trazo. |
| **Uso de un operador de flujo** | En el flujo de contenido, escribe `"/GS0 gs"` antes de las operaciones de dibujo para aplicar el nuevo estado gráfico. |

## Consideraciones de rendimiento

* **Uso de memoria** – Cargar un PDF muy grande consume memoria proporcional al número de páginas. Si solo necesitas editar la primera página, considera usar `pdfDocument.Pages.Delete(pageNumber)` después del procesamiento para liberar recursos.
* **Seguridad en hilos** – Los objetos de Aspose.PDF no son seguros para acceso concurrente. Realiza las ediciones de diccionarios en un solo hilo o crea instancias `Document` separadas por hilo.

## Conclusión

Ahora sabes cómo **crear diccionario PDF vacío** con Aspose.PDF, rellenarlo con entradas de estado gráfico y adjuntarlo al diccionario `ExtGState` de una página. Esta técnica permite un control fino sobre la opacidad, el modo de fusión y otros parámetros de renderizado directamente desde C#.

A continuación, explora temas relacionados como **manipulación de PDF C#**, añadir entradas personalizadas al **diccionario ExtGState** para efectos avanzados de transparencia, o usar **CosPdfDictionary** para modificar otros tipos de recursos como fuentes o XObjects. Experimenta con múltiples estados gráficos para crear efectos visuales sofisticados en tus PDFs.

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Crear y rellenar rectángulos en PDFs usando Aspose.PDF para .NET: Guía paso a paso](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)
- [Cómo crear líneas discontinuas en PDFs usando Aspose.PDF para .NET: Guía paso a paso](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Cómo añadir una página vacía al final de un PDF usando Aspose.PDF para .NET | Guía paso a paso](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}