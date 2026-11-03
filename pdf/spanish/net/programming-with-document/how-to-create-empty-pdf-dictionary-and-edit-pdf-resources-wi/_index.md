---
category: general
date: 2026-10-26
description: Aprende a crear un diccionario PDF vacío y editar los recursos PDF usando
  Aspose.PDF para C#. Guía paso a paso con un ejemplo de código completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- edit PDF resources
- Aspose.PDF C#
- PDF manipulation C#
- PDF graphics state
language: es
lastmod: 2026-10-26
og_description: Crea un diccionario PDF vacío y edita los recursos PDF con Aspose.PDF
  para C#. Sigue este tutorial completo para modificar los estados gráficos en los
  PDFs.
og_image_alt: Screenshot showing creation of empty PDF dictionary in Aspose.PDF
og_title: Crear diccionario PDF vacío y editar recursos PDF en C# – Guía de Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  headline: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  type: TechArticle
- description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  name: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  steps:
  - name: Populate the graphics state entries
    text: 'Add the standard keys:'
  - name: Register the new graphics state in the resource dictionary
    text: Give the state a name (`GS0`) and add it to the `ExtGState` dictionary that
      lives inside the page resources.
  - name: Expected output
    text: 'Running the program prints:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF
title: Cómo crear un diccionario PDF vacío y editar los recursos PDF con Aspose.PDF
  en C#
url: /es/net/programming-with-document/how-to-create-empty-pdf-dictionary-and-edit-pdf-resources-wi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear un diccionario PDF vacío y editar recursos PDF con Aspose.PDF en C#

Si necesita **create empty PDF dictionary** y luego **edit PDF resources** en una aplicación C#, esta guía le muestra los pasos exactos. Verá un ejemplo completo y ejecutable que agrega un estado gráfico personalizado a la primera página de un PDF existente.

Trabajar con objetos PDF de bajo nivel puede resultar intimidante, pero Aspose.PDF ofrece una API clara para la manipulación de diccionarios. Al final de este tutorial comprenderá por qué cada operación es importante y cómo adaptar el código para otros tipos de recursos.

## Requisitos previos

* .NET 6.0 (o posterior) instalado.
* Una copia con licencia de **Aspose.PDF for .NET** – la prueba gratuita funciona para pruebas.
* Un IDE como Visual Studio 2022.
* Un archivo PDF llamado `input.pdf` colocado en una carpeta a la que pueda referenciar desde el código.

No se requieren paquetes NuGet adicionales más allá de `Aspose.Pdf`.

## Paso 1: Configurar el proyecto e importar espacios de nombres

Cree un nuevo proyecto de consola y agregue el paquete Aspose.PDF:

```bash
dotnet new console -n PdfDictionaryDemo
cd PdfDictionaryDemo
dotnet add package Aspose.Pdf
```

En `Program.cs` importe los espacios de nombres que utilizará:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
```

Estas importaciones exponen las clases `Document`, `DictionaryEditor` y COS (Canonical Object Structure) que le permiten **create empty PDF dictionary** objetos y modificar diccionarios de recursos existentes.

## Paso 2: Definir la carpeta que contiene los archivos PDF

Especifique el directorio que contiene `input.pdf`. Usar una ruta absoluta evita ambigüedades cuando el programa se ejecuta desde un directorio de trabajo diferente.

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfDemo\";
```

Reemplace `C:\PdfDemo\` con la ruta en su máquina. Mantener la ruta en una variable facilita reutilizarla tanto para archivos de entrada como de salida.

## Paso 3: Abrir el documento PDF de origen

Cargue el PDF que desea modificar dentro de un bloque `using` para que el controlador del archivo se libere automáticamente.

```csharp
// Step 2: Open the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // The rest of the workflow lives inside this block
}
```

Abrir el documento le brinda acceso a su colección de páginas, diccionarios de recursos y objetos COS de bajo nivel.

## Paso 4: Acceder a la primera página y su diccionario de recursos

La primera página está indexada con `1` (las páginas PDF son basadas en 1). Recupere el diccionario `Resources` de la página y envuélvalo en un `DictionaryEditor` para habilitar la edición segura.

```csharp
// Step 3: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` abstrae la estructura COS subyacente, permitiéndole leer o crear entradas sin dañar el PDF.

## Paso 5: **Create empty PDF dictionary** para un nuevo estado gráfico

Un estado gráfico controla la transparencia, el modo de fusión y otros parámetros de dibujo. Para agregar un estado personalizado primero necesita un diccionario vacío, luego completarlo con las entradas requeridas.

```csharp
// Step 4: Retrieve the ExtGState dictionary and add a new graphics state
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

// Create an empty dictionary that will hold the graphics state parameters
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
```

La llamada a `CreateEmptyDictionary` es el núcleo de los objetos **creating empty PDF dictionary**. Devuelve un diccionario COS que pertenece al mismo documento, garantizando la integridad de las referencias cruzadas.

### Poblar las entradas del estado gráfico

Agregue las claves estándar:

* `CA` – constante alfa de trazo (rango 0 – 1).
* `ca` – constante alfa sin trazo.
* `BM` – nombre del modo de fusión.

```csharp
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

Cada entrada se agrega al diccionario vacío que acaba de crear. Al separar la definición del bucle de inserción mantiene el código legible y facilita la extensión con claves adicionales más adelante.

### Registrar el nuevo estado gráfico en el diccionario de recursos

Asigne al estado un nombre (`GS0`) y agréguelo al diccionario `ExtGState` que se encuentra dentro de los recursos de la página.

```csharp
// Name the new graphics state "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

Ahora el diccionario de recursos de la página contiene una referencia al estado gráfico personalizado, que podrá aplicar posteriormente a los flujos de contenido.

## Paso 6: Guardar el PDF actualizado

Finalmente, escriba el documento modificado en un archivo nuevo. Mantener el original intacto le ayuda a verificar los cambios.

```csharp
// Step 5: Save the updated PDF
pdfDocument.Save(dataDir + "output.pdf");
```

Cuando abra `output.pdf` en un visor que admita la inspección de estados gráficos (p. ej., Adobe Acrobat Pro), verá que el diccionario `ExtGState` contiene una entrada llamada `GS0` con los valores que definió.

## Código fuente completo

Unir todas las piezas produce un programa autónomo:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

class Program
{
    static void Main()
    {
        // Step 1: Define the folder that contains the PDF files
        string dataDir = @"C:\PdfDemo\"; // adjust to your environment

        // Step 2: Open the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Step 3: Access the first page and its resource dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 4: Retrieve the ExtGState dictionary and add a new graphics state
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // **Create empty PDF dictionary** for the new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateEntries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };

            foreach (var entry in graphicsStateEntries)
                newGraphicsState.Add(entry);

            // Register the new graphics state as "GS0"
            extGStateDict.Add("GS0", newGraphicsState);

            // Step 5: Save the updated PDF
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

### Salida esperada

Ejecutar el programa imprime:

```
PDF updated successfully.
```

y crea `output.pdf` en la misma carpeta. Al abrir el archivo se revela una nueva entrada bajo **Resources → ExtGState → GS0** con los parámetros que estableció.

## Variaciones comunes y casos límite

| Situation | How to adapt the code |
|-----------|-----------------------|
| **Multiple pages** necesitan el mismo estado gráfico | Cree el diccionario una vez, luego agregue la misma referencia `GS0` al diccionario `ExtGState` de cada página. |
| **Different blend mode** (p. ej., `Multiply`) | Cambie el valor `CosPdfName("Normal")` a `CosPdfName("Multiply")`. |
| **No existing ExtGState dictionary** | Antes de acceder a `resourcesEditor["ExtGState"]`, verifique `resourcesEditor.ContainsKey("ExtGState")`. Si falta, cree un nuevo diccionario vacío y agréguelo a `firstPage.Resources`. |
| **Large PDFs** causan presión de memoria | Utilice la sobrecarga de `PdfDocument.Load` que transmite páginas, o procese las páginas una a una dentro del bloque `using`. |
| **Need to edit other resources** (fuentes, XObjects) | Reemplace `"ExtGState"` por `"Font"` o `"XObject"` en la búsqueda `resourcesEditor`, luego siga el mismo patrón de crear un diccionario vacío y completarlo. |

Estas variaciones demuestran cómo el mismo patrón **create empty PDF dictionary** se aplica a cualquier tipo de recurso que desee **edit PDF resources**.

## Consejos profesionales

* **Validate the result** – después de guardar, abra el PDF en una herramienta que pueda mostrar el diccionario de recursos sin procesar (p. ej., `PDFDebugger` de PDF‑Box) para asegurarse de que la entrada exista.
* **Reuse dictionaries** – si agrega el mismo estado gráfico a muchas páginas, almacene el diccionario en una variable y haga referencia a él en lugar de recrearlo cada vez.
* **Version compatibility** – el código funciona con Aspose.PDF 23.12 y posteriores. Las versiones anteriores pueden requerir `CosDictionary` en lugar de `CosPdfDictionary`.

## Conclusión

Ahora sabe cómo **create empty PDF dictionary** objetos y **edit PDF resources** usando Aspose.PDF para C#. El tutorial cubrió abrir un documento, acceder al diccionario de recursos de la página, crear un estado gráfico personalizado, registrarlo y guardar el resultado. A partir de aquí puede experimentar con otros tipos de recursos, combinar varios estados gráficos o integrar la técnica en una canalización de procesamiento de PDF más grande.

---

*¿Listo para explorar más? Intente agregar un **ExtGState** personalizado a un flujo de contenido, o manipular el diccionario **Font** para incrustar nuevas fuentes. Ambos siguen el mismo patrón de crear un diccionario vacío y editar PDF resources.*

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarle a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Editar el diccionario de recursos PDF con Aspose.PDF – Guía C#](/pdf/english/net/programming-with-operators/edit-pdf-resource-dictionary-with-aspose-pdf-c-guide/)
- [Crear estado gráfico personalizado en PDF usando Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Cómo crear un estado gráfico vacío en un PDF con C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}