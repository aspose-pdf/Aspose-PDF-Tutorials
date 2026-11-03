---
category: general
date: 2026-10-07
description: Agregar estado gráfico PDF usando Aspose.Pdf en C# para modificar la
  transparencia del PDF. Sigue esta guía paso a paso para incrustar estados gráficos
  personalizados y controlar la opacidad.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- modify pdf transparency
language: es
lastmod: 2026-10-07
og_description: Agrega un estado gráfico PDF con Aspose.Pdf en C#. Aprende cómo modificar
  la transparencia de un PDF creando un diccionario de estado gráfico personalizado.
og_image_alt: Screenshot showing the add graphics state pdf code editor in Visual
  Studio
og_title: Añadir estado gráfico PDF con Aspose.Pdf – controlar la transparencia del
  PDF
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Add graphics state pdf using Aspose.Pdf in C# to modify PDF transparency.
    Follow this step‑by‑step guide to embed custom graphics states and control opacity.
  headline: Add graphics state pdf with Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Añadir estado gráfico PDF con Aspose.Pdf en C#
url: /es/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Añadir estado gráfico pdf con Aspose.Pdf en C#

Si necesitas **añadir estado gráfico pdf** a un documento, este tutorial te muestra exactamente cómo hacerlo con Aspose.Pdf para .NET. Al final de la guía también sabrás cómo **modificar la transparencia de PDF**, lo que te permite establecer valores de opacidad personalizados en cualquier operación de dibujo.

Trabajar con estados gráficos de PDF te permite controlar parámetros como el ancho de línea, el modo de fusión y, lo más importante para este artículo, la transparencia del contenido. Los pasos a continuación están escritos para desarrolladores que se sienten cómodos con C# y desean una solución lista para ejecutar sin tener que profundizar en la documentación oficial del SDK.

## Lo que aprenderás

* Cómo crear un nuevo diccionario de estado gráfico y rellenarlo con las entradas `CA`, `ca` y `BM`.  
* Cómo insertar ese diccionario en el recurso `ExtGState` de la página para que el PDF lo reconozca.  
* Cómo los valores `ca` (trazo) y `CA` (relleno) afectan **modificar la transparencia de PDF** para los comandos de dibujo posteriores.  
* Problemas comunes como colisiones de nombres y compatibilidad de versiones, además de consejos profesionales para ampliar el estado gráfico más adelante.

## Requisitos previos

* .NET 6.0 o posterior (el código también funciona con .NET Framework 4.7+).  
* Una licencia válida de Aspose.Pdf para .NET (la evaluación gratuita funciona para pruebas).  
* Visual Studio 2022 o cualquier IDE de C# que prefieras.  

---

## Paso 1: Instalar Aspose.Pdf para .NET

Agrega el paquete NuGet a tu proyecto:

```bash
dotnet add package Aspose.Pdf
```

El paquete incluye el espacio de nombres `Aspose.Pdf` que proporciona las clases `Document`, `DictionaryEditor` y `CosPdfDictionary` utilizadas más adelante.

> **Consejo profesional:** Si planeas procesar muchos PDFs en lote, habilita la **License** temprano en `Program.cs` para evitar la marca de agua de evaluación.

```csharp
// Apply your license (optional for evaluation)
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Aspose.Pdf.lic");
```

## Paso 2: Definir rutas de entrada y salida

Debes indicar al SDK un PDF existente (`input.pdf`) y especificar dónde se guardará el archivo modificado (`output.pdf`).

```csharp
// Define input and output PDF file paths
string inputPath = @"C:\MyPdfs\input.pdf";
string outputPath = @"C:\MyPdfs\output.pdf";
```

> **Por qué es importante:** Usar rutas absolutas evita que el SDK busque en el directorio de trabajo incorrecto, lo cual es una fuente común de `FileNotFoundException`.

## Paso 3: Abrir el PDF y localizar los recursos de la primera página

El diccionario `ExtGState` se encuentra dentro del diccionario de recursos de cada página. Editaremos la primera página por simplicidad, pero el mismo enfoque funciona para cualquier índice de página.

```csharp
using (var pdfDocument = new Aspose.Pdf.Document(inputPath))
{
    // Get the first page (pages are 1‑based)
    var firstPage = pdfDocument.Pages[1];

    // Access the page’s resource dictionary via DictionaryEditor
    var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);

    // Retrieve (or create) the ExtGState entry
    var extGStateDict = resourcesEditor["ExtGState"]
        .ToCosPdfDictionary(); // Throws if ExtGState does not exist
```

**Caso extremo:** Si la página no tiene una entrada `ExtGState`, necesitas crearla:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
{
    var emptyDict = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", emptyDict);
    extGStateDict = emptyDict;
}
```

## Paso 4: Construir un nuevo diccionario de estado gráfico

Un estado gráfico es una colección de pares clave/valor que describen cómo se comportan las operaciones de dibujo. Para la transparencia necesitamos tres claves:

| Clave | Significado | Valor típico |
|-----|-------------|--------------|
| `CA` | Opacidad de relleno (0 = transparente, 1 = opaco) | `1` (totalmente opaco) |
| `ca` | Opacidad de trazo (misma escala) | `0.5` (50 % transparente) |
| `BM` | Modo de fusión (p.ej., `Normal`, `Multiply`) | `Normal` |

```csharp
    // Create an empty dictionary that will hold the graphics state
    var newGraphicsState = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Populate the dictionary with transparency and blend mode entries
    var graphicsStateEntries = new[]
    {
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "CA", new Aspose.Pdf.CosPdfNumber(1)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "ca", new Aspose.Pdf.CosPdfNumber(0.5)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "BM", new Aspose.Pdf.CosPdfName("Normal"))
    };

    foreach (var entry in graphicsStateEntries)
        newGraphicsState.Add(entry);
```

**¿Por qué estos valores?**  
`ca = 0.5` hace que cualquier ruta trazada (líneas, bordes) aparezca al 50 % de opacidad, mientras que `CA = 1` deja las formas rellenas totalmente opacas. Ajusta ambos números para lograr el efecto exacto de **modificar la transparencia de PDF** que necesitas.

## Paso 5: Insertar el estado gráfico en el diccionario ExtGState

Debes asignar al nuevo estado un nombre único (p.ej., `GS0`). Si el nombre ya existe, Aspose.Pdf sobrescribirá la entrada existente, lo que podría romper otro contenido que dependa de ella.

```csharp
    // Add the new graphics state under a custom name
    const string stateName = "GS0";

    // Ensure we don’t clash with an existing entry
    if (extGStateDict.ContainsKey(stateName))
        extGStateDict.Remove(stateName);

    extGStateDict.Add(stateName, newGraphicsState);
```

Ahora los recursos de la página conocen `GS0`. Para usarlo realmente, deberías referenciar el estado gráfico en un flujo de contenido mediante el operador `gs` (p.ej., `GS0 gs`). Aspose.Pdf te permite inyectar operadores PDF sin procesar si necesitas dibujar formas personalizadas.

## Paso 6: Guardar el PDF modificado

```csharp
    // Persist the changes to a new file
    pdfDocument.Save(outputPath);
}
```

El `output.pdf` resultante contiene el mismo contenido visual que el original, pero cualquier comando de dibujo posterior que seleccione `GS0` respetará la configuración de transparencia que definiste.

### Resultado esperado

Abre `output.pdf` en Adobe Acrobat o cualquier visor de PDF. Si añades una nueva línea trazada usando el estado gráfico `GS0` (p.ej., mediante `pdfDocument.Pages[1].Contents.Add(...)`), la línea aparecerá semitransparente mientras los rellenos permanecen opacos. Esto demuestra que has añadido correctamente **estado gráfico pdf** y **modificado la transparencia de PDF**.

---

## Ejemplo completo ejecutable

A continuación se muestra el programa completo que puedes copiar y pegar en una aplicación de consola. Incluye la carga de la licencia, manejo de errores y comentarios que explican cada paso no obvio.

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣  Apply license (optional for evaluation)
        // -------------------------------------------------
        try
        {
            var license = new License();
            license.SetLicense("Aspose.Pdf.lic");
        }
        catch (Exception) { /* License not found – continue in evaluation mode */ }

        // -------------------------------------------------
        // 2️⃣  Define file locations
        // -------------------------------------------------
        string inputPath = @"C:\MyPdfs\input.pdf";
        string outputPath = @"C:\MyPdfs\output.pdf";

        // -------------------------------------------------
        // 3️⃣  Open document and prepare resources
        // -------------------------------------------------
        using (var pdfDocument = new Document(inputPath))
        {
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            if (!resourcesEditor.ContainsKey("ExtGState"))
            {
                var emptyExtGState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
                resourcesEditor.Add("ExtGState", emptyExtGState);
            }

            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // -------------------------------------------------
            // 4️⃣  Create custom graphics state (transparency)
            // -------------------------------------------------
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            newGraphicsState.Add("CA", new CosPdfNumber(1));   // Fill opacity
            newGraphicsState.Add("ca", new CosPdfNumber(0.5)); // Stroke opacity
            newGraphicsState.Add("BM", new CosPdf


## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Añadir transparencia a PDF con Aspose PDF en C# – Guía paso a paso](/pdf/english/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Añadir transparencia a PDF usando Aspose – Guía completa en C#](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [Cómo añadir una marca de imagen a un PDF usando Aspose.PDF para .NET: Guía completa](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}