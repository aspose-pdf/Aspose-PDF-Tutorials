---
category: general
date: 2026-02-28
description: Crear documento PDF en C# con numeración Bates. Aprende cómo agregar
  numeración Bates al PDF, establecer prefijos y generar números PDF secuenciales
  en una única guía paso a paso.
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add document identification numbers
- add sequential pdf numbers
language: es
og_description: Crear documento PDF en C# con numeración Bates. Este tutorial muestra
  cómo agregar numeración Bates al PDF, establecer prefijos personalizados y generar
  números PDF secuenciales.
og_title: Crear documento PDF en C# – Añadir numeración Bates
tags:
- Aspose.PDF
- C#
- PDF automation
title: Crear documento PDF en C# – Guía para agregar numeración Bates
url: /es/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear documento PDF C# – Guía para agregar numeración Bates

¿Alguna vez te has preguntado cómo **crear documento PDF C#** que ya incluya un identificador único en cada página? Ese es un problema común cuando necesitas rastrear archivos legales, presentaciones judiciales o cualquier lote de PDFs que deben ser buscables por número. ¿La buena noticia? Con Aspose.PDF puedes agregar números Bates con solo unas pocas líneas de código, sin necesidad de edición manual.

En esta guía recorreremos todo el proceso: cargar un PDF existente, configurar **add bates numbering pdf**, aplicar los números y, finalmente, guardar el resultado. Al terminar podrás **add document identification numbers** e incluso **add sequential PDF numbers** automáticamente, todo desde C#.

## Prerrequisitos

- .NET 6.0 o posterior (la API también funciona con .NET Framework 4.5+)
- Una copia con licencia de **Aspose.PDF for .NET** (la versión de prueba gratuita sirve para pruebas)
- Un archivo PDF de entrada que deseas numerar (lo llamaremos `input.pdf`)
- Visual Studio 2022 (o cualquier IDE que prefieras)

No se requieren paquetes NuGet adicionales más allá de Aspose.PDF.

![Crear documento PDF C# con numeración Bates](https://example.com/image.png "Crear documento PDF C# ejemplo")

## Paso 1: Cargar el documento PDF de origen

Antes de poder **add bates numbering pdf**, necesitas un objeto `Document` que represente el archivo en disco.

```csharp
using Aspose.Pdf;

// Load the source PDF document
var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*Por qué es importante*: La clase `Document` es el punto de entrada para cada operación en Aspose.PDF. Abstrae el sistema de archivos, de modo que puedes trabajar con páginas, anotaciones y metadatos sin tocar los bytes crudos.

> **Consejo profesional:** Si procesas muchos archivos en un bucle, reutiliza la misma instancia de `Document` solo cuando la fuente sea idéntica; de lo contrario, crea un nuevo objeto para cada archivo para evitar fugas de memoria.

## Paso 2: Definir las opciones de numeración Bates

Aquí es donde la parte **how to add bates** se vuelve concreta. Configuras un objeto `BatesNumberingOptions` para indicarle a Aspose cuál debe ser el prefijo, dónde comenzar y qué tamaño de fuente debe usar.

```csharp
// Define Bates numbering options (prefix, start number, font size)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",   // You can change this to any string you need
    Start = 1000,      // Starting number – useful for continuous numbering across batches
    FontSize = 9       // Small enough to fit in the margin but still readable
};
```

*Por qué es importante*: El `Prefix` te permite incrustar un identificador de caso (p. ej., “ABC-”). La propiedad `Start` es esencial cuando estás **adding sequential PDF numbers** en varios documentos; simplemente sigue incrementándola. Y `FontSize` asegura que los números no obstruyan el contenido existente.

## Paso 3: Aplicar la numeración Bates a todo el documento

Ahora realmente estampamos los números en cada página. La clase `BatesNumbering` hace todo el trabajo pesado.

```csharp
// Apply Bates numbering to the entire document
var bates = new BatesNumbering();
bates.AddBatesNumbering(pdfDocument, batesOptions);
```

*Por qué es importante*: Internamente, Aspose recorre cada página, calcula el número apropiado (Prefijo + (Start + índice de página)) y lo dibuja en la esquina inferior‑derecha por defecto. Puedes personalizar la posición más adelante, pero el valor predeterminado funciona para la mayoría de documentos de estilo legal.

> **Pregunta frecuente:** *¿Qué pasa si solo necesito numerar un subconjunto de páginas?*  
> Usa la sobrecarga `AddBatesNumbering(Document, BatesNumberingOptions, int startPage, int endPage)` para limitar el rango.

## Paso 4: Guardar el PDF con los números Bates aplicados

El paso final es escribir el documento modificado de vuelta al disco.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*Por qué es importante*: El método `Save` respeta el formato de archivo original, de modo que terminas con un PDF estándar que cualquier visor puede abrir, completo con **add document identification numbers** en cada página.

## Ejemplo completo funcionando

Juntando todo, aquí tienes un programa autocontenido que puedes pegar en una nueva aplicación de consola y ejecutar de inmediato.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF document
            var inputPath = @"YOUR_DIRECTORY/input.pdf";
            var pdfDocument = new Document(inputPath);

            // 2️⃣ Define Bates numbering options (prefix, start number, font size)
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                FontSize = 9
            };

            // 3️⃣ Apply Bates numbering to the entire document
            var bates = new BatesNumbering();
            bates.AddBatesNumbering(pdfDocument, batesOptions);

            // 4️⃣ Save the PDF with Bates numbers applied
            var outputPath = @"YOUR_DIRECTORY/output.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbering added successfully. Output saved to {outputPath}");
        }
    }
}
```

**Resultado esperado:** Abre `output.pdf` en cualquier visor; verás “ABC‑1000”, “ABC‑1001”, … impresos en la esquina inferior‑derecha de cada página. Los números son texto seleccionable, por lo que son buscables y pueden copiarse, exactamente lo que esperas de una implementación adecuada de **add sequential PDF numbers**.

## Casos límite y variaciones

### Posicionamiento personalizado

Si la esquina predeterminada choca con pies de página existentes, puedes desplazar la ubicación:

```csharp
batesOptions.Position = new Position(10, 10); // X, Y from the bottom‑left
```

### Diferentes formatos de número

¿Quieres números con ceros a la izquierda (p. ej., 001000)? Usa `NumberFormat`:

```csharp
batesOptions.NumberFormat = "D6"; // Pads to 6 digits
```

### Varios archivos en lote

Al procesar muchos PDFs, mantén un contador continuo:

```csharp
int globalStart = 5000;
foreach (var file in Directory.GetFiles(@"YOUR_DIRECTORY\Batch", "*.pdf"))
{
    var doc = new Document(file);
    var opts = new BatesNumberingOptions
    {
        Prefix = "BATCH-",
        Start = globalStart,
        FontSize = 9
    };
    new BatesNumbering().AddBatesNumbering(doc, opts);
    doc.Save(Path.ChangeExtension(file, ".bated.pdf"));
    globalStart += doc.Pages.Count; // Increment for the next file
}
```

### Manejo de PDFs protegidos con contraseña

Si el PDF de origen está encriptado, pasa la contraseña al crear el `Document`:

```csharp
var pdfDocument = new Document("protected.pdf", new LoadOptions { Password = "mySecret" });
```

## Preguntas frecuentes

| Pregunta | Respuesta |
|----------|-----------|
| **¿Puedo usar una biblioteca diferente?** | Sí, bibliotecas como iTextSharp o PdfSharp también soportan la inserción de texto a nivel de página, pero Aspose.PDF ofrece la API más directa para la numeración Bates. |
| **¿Esto afecta el tamaño del archivo?** | Añadir unos pocos bytes de texto por página es insignificante; el tamaño de salida normalmente crece menos de 1 KB por página. |
| **¿Los números son buscables?** | Absolutamente. Aspose escribe los números como objetos de texto, no como imágenes, por lo que los lectores de PDF los indexan. |
| **¿Qué pasa si necesito una fuente diferente?** | Establece `batesOptions.Font` a un objeto `Font` (p. ej., `FontRepository.FindFont("Arial")`). |

## Conclusión

Acabamos de demostrar cómo **crear documento PDF C#** y agregar instantáneamente **add bates numbering pdf** usando Aspose.PDF. El proceso es simple, fiable y totalmente programable, perfecto para despachos legales, agencias gubernamentales o cualquier organización que deba **add document identification numbers** y **add sequential PDF numbers** a grandes lotes de archivos.

Toma esta base y experimenta: prueba diferentes prefijos para distintos departamentos, encadena la numeración a través de varios archivos o incrusta códigos QR junto a los números Bates para mayor trazabilidad. El cielo es el límite una vez que domines el flujo de trabajo central.

Si este tutorial te resultó útil, compártelo, deja un comentario o explora nuestras otras guías sobre manipulación de PDFs con C#. ¡Feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}