---
category: general
date: 2026-09-27
description: Agregar numeración Bates a PDF usando Aspose.PDF en C#. Aprende cómo
  cargar un documento PDF, establecer las opciones de numeración Bates y guardar el
  archivo actualizado.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- load pdf document
- how to add bates numbering
- Aspose.PDF C#
- PDF Bates numbering example
language: es
lastmod: 2026-09-27
og_description: Agrega numeración Bates a PDF usando Aspose.PDF en C#. Este tutorial
  te muestra cómo cargar un documento PDF, configurar la numeración Bates y guardar
  el resultado.
og_image_alt: Screenshot of a PDF page displaying Bates numbers in the footer
og_title: Agregar numeración Bates a PDF con Aspose.PDF – Guía de C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Add bates numbering to PDF using Aspose.PDF in C#. Learn how to load
    a PDF document, set Bates numbering options, and save the updated file.
  headline: Add bates numbering to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF processing
title: Agregar numeración Bates a PDF usando Aspose.PDF en C#
url: /es/net/programming-with-text/add-bates-numbering-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Añadir numeración Bates a PDF usando Aspose.PDF en C#

Si necesitas **añadir numeración Bates** a un archivo PDF, esta guía te muestra una solución completa y lista para ejecutar. Verás cómo **cargar un documento PDF**, configurar las opciones de numeración Bates y escribir el archivo numerado de vuelta al disco, todo con Aspose.PDF para .NET.

Aplicar números Bates es común en flujos de trabajo legales, de aplicación de la ley y de archivo. Al final de este tutorial podrás incrustar un identificador secuencial en cada página, personalizar el prefijo y comenzar la cuenta en cualquier número que elijas.

## Lo que aprenderás

* Cómo **cargar el contenido del documento PDF** en un objeto `Aspose.Pdf.Document`.  
* Los pasos exactos **para añadir numeración Bates** con `BatesNumberingOptions`.  
* Cómo guardar el archivo modificado preservando el diseño y la calidad originales.  

No se requieren herramientas externas, solo el paquete NuGet Aspose.PDF y un entorno de desarrollo .NET (Visual Studio, VS Code o Rider).  

---

## Paso 1: Instalar Aspose.PDF para .NET

Abre la carpeta de tu proyecto en una terminal y ejecuta:

```bash
dotnet add package Aspose.PDF
```

El paquete incluye el espacio de nombres `Aspose.Pdf`, que proporciona todas las clases usadas en este tutorial. Después de la instalación, recarga el proyecto para que el IDE detecte la nueva referencia.

## Paso 2: Cargar el documento PDF

Cargar el archivo fuente es la primera operación porque el motor de numeración Bates funciona sobre una instancia `Document` existente.

```csharp
using Aspose.Pdf;

// ...

// Replace with the path to your input PDF
string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Load the PDF document into memory
Document doc = new Document(inputPath);
```

**Por qué es importante:** La clase `Document` analiza la estructura del PDF, dándote acceso a páginas, anotaciones y metadatos. Sin cargar el archivo primero, no puedes aplicar ninguna numeración.

## Paso 3: Configurar las opciones de numeración Bates

Crea un objeto `BatesNumberingOptions` y establece el prefijo deseado, el número inicial y los parámetros de formato opcionales.

```csharp
using Aspose.Pdf;

// ...

BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Text that appears before the numeric part
    Prefix = "CASE01",

    // First number to use (1 means the first page gets CASE01-1)
    StartNumber = 1,

    // Optional: customize the appearance
    // The default places the number in the footer, centered.
    // You can change Font, FontSize, Color, and Position if needed.
    // Example:
    // Font = FontRepository.FindFont("Arial"),
    // FontSize = 10,
    // Color = Color.Black,
    // Margin = new Margin(0, 0, 0, 20)
};
```

**Por qué es importante:** `BatesNumberingOptions` indica a Aspose.PDF cómo generar la etiqueta para cada página. El `Prefix` te ayuda a agrupar casos relacionados, mientras que `StartNumber` te permite continuar una secuencia desde un lote anterior.

## Paso 4: Guardar el PDF con la numeración Bates aplicada

Pasa el objeto de opciones al método `Save`. Aspose.PDF escribe los números directamente sobre cada página.

```csharp
// Replace with the desired output path
string outputPath = @"YOUR_DIRECTORY\output.pdf";

// Save the document, applying the Bates numbering
doc.Save(outputPath, batesOptions);
```

**Por qué es importante:** La sobrecarga `Save(string, BatesNumberingOptions)` combina el paso de renderizado con el proceso de numeración, asegurando que el archivo de salida contenga los identificadores visibles.

## Ejemplo completo – todo junto

A continuación tienes un programa único y autocontenido que puedes copiar, pegar y ejecutar. Demuestra **cómo añadir numeración Bates** de principio a fin.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the PDF document
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Set up Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                Prefix = "CASE01",
                StartNumber = 1,
                // Optional appearance tweaks:
                // Font = FontRepository.FindFont("Times New Roman"),
                // FontSize = 9,
                // Color = Color.DarkBlue,
                // Margin = new Margin(0, 0, 0, 15)
            };

            // 3️⃣ Save the document with Bates numbers
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath, batesOptions);

            Console.WriteLine($"Bates numbering added. Output saved to: {outputPath}");
        }
    }
}
```

### Resultado esperado

Al ejecutar el programa se genera `output.pdf` donde cada página muestra una etiqueta similar a:

```
CASE01-1
CASE01-2
CASE01-3
...
```

Los números aparecen en el pie de página por defecto, pero puedes moverlos ajustando la propiedad `Margin` en `BatesNumberingOptions`.

## Casos límite y variaciones comunes

| Situación | Qué ajustar |
|-----------|-------------|
| **Prefijo diferente por lote** | Cambia `Prefix` antes de llamar a `Save`. Puedes iterar sobre varios documentos con prefijos distintos. |
| **Continuar la numeración desde un archivo anterior** | Establece `StartNumber` al último número usado + 1. |
| **Colocar los números en el encabezado** | Usa `batesOptions.Margin = new Margin(20, 0, 0, 0);` (margen superior) o personaliza `batesOptions.Position`. |
| **Fuente o color personalizados** | Asigna las propiedades `Font`, `FontSize` y `Color` como se muestra en la sección comentada. |
| **PDFs grandes (1000+ páginas)** | La operación es eficiente en memoria; sin embargo, podrías habilitar `doc.OptimizeResources()` antes de guardar para reducir el tamaño del archivo. |

**Consejo profesional:** Si tu flujo de trabajo requiere esquemas de numeración diferentes por documento, encapsula la lógica en un método auxiliar:

```csharp
static void ApplyBatesNumbering(string src, string dst, string prefix, int start)
{
    var doc = new Document(src);
    var opts = new BatesNumberingOptions { Prefix = prefix, StartNumber = start };
    doc.Save(dst, opts);
}
```

## Conclusión

Ahora sabes **cómo añadir numeración Bates** a cualquier PDF usando Aspose.PDF en C#. El tutorial cubrió la carga del documento PDF, la configuración de las opciones de numeración y el guardado del archivo final, todo en un solo programa ejecutable.  

A partir de aquí puedes explorar temas relacionados como **añadir marcas de agua**, **combinar varios PDFs** o **extraer texto** con Aspose.PDF. Experimenta con diferentes fuentes, colores y posiciones para que coincidan con los estándares de formato de tu organización.

¿Listo para automatizar tu flujo de trabajo de documentos legales? Añade el código a tu pipeline de compilación, ejecútalo contra lotes de archivos y deja que Aspose.PDF haga el trabajo pesado. ¡Feliz codificación!


## ¿Qué deberías aprender a continuación?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Create PDF Document C# – Add Bates Numbering](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/)
- [Add Bates Numbering PDF – Step‑by‑Step Guide to Number PDF Pages](/pdf/english/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/)
- [Aspose PDF Tutorial – Insert a Blank Page and Update Bates Numbering](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}