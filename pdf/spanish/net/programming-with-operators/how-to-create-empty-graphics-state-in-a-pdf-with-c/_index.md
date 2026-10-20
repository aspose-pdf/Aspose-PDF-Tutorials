---
category: general
date: 2026-08-17
description: Crea un estado gráfico vacío en un PDF usando C# y Aspose.Pdf. Sigue
  esta guía paso a paso para editar los recursos ExtGState de forma segura.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty graphics state
- Aspose PDF graphics state
- C# modify PDF resources
- add ExtGState dictionary
- PDF page resources editing
language: es
lastmod: 2026-08-17
og_description: Crear un estado gráfico vacío en un PDF usando C#. Este tutorial muestra
  cómo editar los recursos ExtGState con Aspose.Pdf para realizar modificaciones de
  PDF fiables.
og_image_alt: Screenshot of C# code that adds an empty graphics state to a PDF document
og_title: Crear un estado gráfico vacío en PDF con C# – guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Create empty graphics state in a PDF using C# and Aspose.Pdf. Follow
    this step‑by‑step guide to edit ExtGState resources safely.
  headline: How to create empty graphics state in a PDF with C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Cómo crear un estado gráfico vacío en un PDF con C#
url: /es/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear un estado gráfico vacío en un PDF con C#

Si necesitas **crear un estado gráfico vacío** en un PDF, esta guía te muestra exactamente cómo hacerlo con C# y Aspose.Pdf. Verás un ejemplo completo y ejecutable que añade una nueva entrada al diccionario ExtGState de la página sin afectar el contenido existente.

Trabajar con estados gráficos de PDF es un requisito común cuando deseas controlar la transparencia, los modos de fusión u otros parámetros de renderizado por objeto. El código a continuación demuestra el enfoque recomendado, explica por qué cada paso es importante y cubre variaciones típicas que podrías encontrar.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* .NET 6.0 o posterior (el ejemplo también compila con .NET Core).
* Una licencia de Aspose.Pdf para .NET (o una clave de evaluación temporal).
* Una carpeta que contenga un archivo `input.pdf` que quieras modificar.
* Familiaridad básica con la sintaxis de C# y conceptos de PDF como los diccionarios de recursos.

## Paso 1: Configurar el proyecto e importar espacios de nombres

Crea una nueva aplicación de consola o integra el código en un proyecto existente. Añade el paquete NuGet Aspose.Pdf:

```bash
dotnet add package Aspose.Pdf
```

Luego importa los espacios de nombres requeridos:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
```

Estas importaciones te dan acceso a las clases `Document`, `DictionaryEditor` y a los primitivos PDF necesarios para **crear un estado gráfico vacío**.

## Paso 2: Definir la carpeta que contiene los archivos PDF

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfSamples\";
```

Reemplaza la ruta con la ubicación de tus propios archivos PDF. Mantener el directorio en una variable hace que el código sea reutilizable y más fácil de probar.

## Paso 3: Cargar el documento PDF de origen

```csharp
// Step 2: Load the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // All subsequent operations happen inside this using block
```

Abrir el documento dentro de una sentencia `using` garantiza que el manejador del archivo se libere automáticamente después de guardar los cambios.

## Paso 4: Acceder a la primera página y a su diccionario Resources

```csharp
    // Step 3: Get the first page and its Resources dictionary
    var firstPage = pdfDocument.Pages[1];
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
    var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

* `Pages[1]` recupera la primera página (los números de página en PDF empiezan en 1).
* `DictionaryEditor` proporciona una forma cómoda de leer y modificar diccionarios PDF.
* La entrada `ExtGState` contiene todos los objetos de estado gráfico de la página. Si la clave no existe, Aspose.Pdf crea automáticamente un diccionario vacío.

## Paso 5: Construir un nuevo diccionario de estado gráfico vacío

El estado gráfico que añadas puede estar vacío o pre‑poblado con parámetros como opacidad (`CA`, `ca`) o modo de fusión (`BM`). En este tutorial creamos un **estado gráfico vacío** y luego establecemos algunos valores típicos para ilustrar cómo funciona el diccionario.

```csharp
    // Step 4: Create a new empty graphics‑state dictionary and set its parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // Stroke opacity
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };
    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

* `CosPdfDictionary.CreateEmptyDictionary` crea un contenedor limpio que puedes rellenar con cualquier clave de estado gráfico.
* Añadir `CA`, `ca` y `BM` es opcional; puedes omitirlos si realmente necesitas un estado vacío. El código muestra cómo agregar entradas cuando luego decidas controlar el renderizado.

## Paso 6: Insertar el nuevo estado gráfico en el diccionario ExtGState

```csharp
    // Step 5: Add the new graphics state to the page's ExtGState dictionary (e.g., name it "GS0")
    extGStateDict.Add("GS0", newGraphicsState);
```

Nombrar la entrada `"GS0"` sigue la convención común de prefijar los nombres de estado gráfico con “GS”. Puedes elegir cualquier nombre PDF válido que no choque con claves existentes.

## Paso 7: Guardar el documento PDF modificado

```csharp
    // Step 6: Save the modified PDF document
    pdfDocument.Save(dataDir + "output.pdf");
}
```

La llamada `Save` escribe el archivo actualizado en `output.pdf`. Abrir este archivo en un visor de PDF confirma que el nuevo estado gráfico existe; podrás referenciarlo más adelante con el operador `gs` en los flujos de contenido.

### Listado completo del código fuente

Uniendo todo, el programa completo se ve así:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;

class Program
{
    static void Main()
    {
        // Define the folder that contains the PDF files
        string dataDir = @"C:\PdfSamples\";

        // Load the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Get the first page and its Resources dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create a new empty graphics‑state dictionary and set its parameters
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters)
                newGraphicsState.Add(p);

            // Add the new graphics state to the page's ExtGState dictionary (name it "GS0")
            extGStateDict.Add("GS0", newGraphicsState);

            // Save the modified PDF document
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("Empty graphics state created and saved to output.pdf");
    }
}
```

Ejecutar el programa muestra una línea de confirmación y genera `output.pdf` con el estado gráfico recién añadido.

## Por qué este enfoque funciona mejor

* **Edición directa de diccionarios** – Usar `DictionaryEditor` evita la necesidad de analizar todo el flujo de contenido. Modificas solo los recursos que te interesan.
* **Primitivos PDF tipados** – `CosPdfNumber`, `CosPdfName` y `CosPdfDictionary` garantizan que el PDF generado cumpla con la especificación PDF 1.7.
* **Seguridad** – El bloque `using` dispone del objeto `Document`, evitando bloqueos de archivo que podrían corromper compilaciones posteriores.
* **Extensibilidad** – Una vez que el estado gráfico vacío existe, puedes referenciarlo desde cualquier operador de contenido (`gs`) para cambiar la opacidad, el modo de fusión u otros parámetros de los comandos de dibujo seleccionados.

## Variaciones comunes y casos límite

| Situación | Ajuste recomendado |
|-----------|-------------------|
| **Múltiples páginas** | Recorre `pdfDocument.Pages` y repite la inserción del diccionario para cada página que necesites modificar. |
| **No hay entrada ExtGState existente** | `resourcesEditor["ExtGState"]` crea automáticamente un diccionario vacío si no existe. No se requiere código adicional. |
| **Nombre de estado gráfico diferente** | Reemplaza `"GS0"` por un nombre que coincida con tu convención, por ejemplo, `"MyTransparentState"`. |
| **Agregar solo un estado vacío** | Omite el arreglo `parameters` y el bucle `foreach`; el diccionario permanecerá vacío. |
| **Trabajar con PDFs encriptados** | Proporciona la contraseña al construir `new Document(path, password)` antes de editar los recursos. |

## Verificando el resultado

Puedes comprobar que el estado gráfico se añadió inspeccionando el PDF con un visor de bajo nivel como **PDF‑Tron** o **iText Sharp**. Busca una entrada similar a:

```
/ExtGState << /GS0 << /CA 1 /ca 0.5 /BM /Normal >> >>
```

Si la entrada aparece, la operación **crear un estado gráfico vacío** se realizó con éxito.

## Conclusión

Ahora sabes cómo **crear un estado gráfico vacío** en un PDF usando C# y Aspose.Pdf. El tutorial cubrió cada paso—desde cargar el documento hasta editar el diccionario `ExtGState` y guardar el resultado—explicando la lógica detrás de cada acción.  

A partir de aquí puedes:

* Usar el nuevo estado gráfico en flujos de contenido (`gs /GS0`).
* Experimentar con claves adicionales como `/SM` (ajuste de trazo) o `/OPM` (modo de sobreimpresión).
* Aplicar la misma técnica a otros tipos de recursos como `/XObject` o `/ColorSpace`.

¡Feliz manipulación de PDFs, y siéntete libre de explorar otros escenarios de **estado gráfico de Aspose PDF** como cambios dinámicos de opacidad o modos de fusión personalizados!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo crear líneas discontinuas en PDFs usando Aspose.PDF para .NET: Guía paso a paso](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Cómo eliminar gráficos de PDFs usando Aspose.PDF .NET: Guía completa](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Crear y rellenar rectángulos en PDFs usando Aspose.PDF para .NET: Guía paso a paso](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}