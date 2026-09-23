---
category: general
date: 2026-03-24
description: Cómo agregar un sello a un PDF usando Aspose.Pdf en C#. Aprende a colocar
  un sello en PDF y añadir un sello de texto con ajuste automático de tamaño en unos
  pocos pasos fáciles.
draft: false
keywords:
- how to add stamp
- place stamp pdf
- add text stamp pdf
- Aspose.Pdf stamp example
- C# PDF annotation
language: es
og_description: ¿Cómo agregar una marca de agua a un PDF en C#? Esta guía le muestra
  cómo colocar una marca de agua en PDF y agregar una marca de texto en PDF con ajuste
  automático del tamaño de fuente usando Aspose.Pdf.
og_title: Cómo agregar un sello a PDF con Aspose.Pdf – Guía rápida
tags:
- pdf
- csharp
- aspose
- stamping
title: Cómo agregar un sello a PDF con Aspose.Pdf – Guía paso a paso
url: /es/net/programming-with-stamps-and-watermarks/how-to-add-stamp-to-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo agregar una marca de agua a PDF con Aspose.Pdf – Guía paso a paso

**Cómo agregar una marca de agua** a un PDF es una necesidad frecuente cuando deseas identificar, certificar o simplemente anotar un documento. ¿Alguna vez te has preguntado la forma más fácil de colocar una marca de agua PDF sin lidiar con gráficos de bajo nivel? En este tutorial recorreremos una solución completa, lista para ejecutar, que no solo muestra **cómo agregar una marca de agua**, sino que también explica *por qué* cada línea es importante.

Aprenderás cómo **colocar una marca de agua PDF** en cualquier página, cómo **agregar una marca de texto PDF** que se reduce automáticamente para ajustarse a su rectángulo, y qué trampas evitar cuando el texto es demasiado largo. Al final tendrás un único archivo C# que podrás insertar en tu proyecto y comenzar a marcar PDFs de inmediato.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* .NET 6.0 o posterior (el código funciona también con .NET Core y .NET Framework).
* El paquete NuGet Aspose.Pdf for .NET (`Aspose.Pdf`) instalado.
* Un archivo PDF llamado `input.pdf` en una carpeta a la que puedas referenciar (cualquier PDF simple de una página servirá).

No se requiere configuración adicional: Aspose.Pdf se encarga de todo el trabajo pesado.

## Paso 1: Configurar el proyecto y cargar el PDF de origen

Lo primero que necesitamos es un objeto `Document` que represente el PDF que queremos anotar. Piensa en ello como cargar un lienzo en blanco sobre el que luego pintaremos una marca de agua.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the source PDF document
// The using statement ensures the file is closed automatically.
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Por qué es importante:** `Document` es el punto de entrada para cualquier manipulación de PDF en Aspose.Pdf. Al usar el patrón `using` garantizamos que el manejador del archivo se libere, lo que evita problemas de bloqueo al intentar guardar el PDF modificado más adelante.

## Paso 2: Crear una marca de texto con ajuste automático del tamaño de fuente

Ahora creamos un `TextStamp`. El truco que hace que este ejemplo destaque es la bandera `AutoAdjustFontSizeToFitStampRectangle`: le indica a Aspose que reduzca el texto hasta que quepa dentro del rectángulo que definimos.

```csharp
// Create a text stamp that will automatically resize to fit its rectangle
var textStamp = new TextStamp("Long text that must fit")
{
    // Let Aspose shrink the text if it overflows
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Precision of the auto‑adjust algorithm (lower = more accurate)
    AutoAdjustFontSizePrecision = 0.01f,
    // Define the stamp's bounding box (in points)
    Width = 300,
    Height = 100,
    // Word‑wrap by whole words so we don’t split in the middle of a word
    WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
    // Optional: set background color or opacity if you want a visible box
    Background = new Background()
    {
        Color = Color.LightGray,
        Opacity = 0.5
    }
};
```

> **Consejo profesional:** Si necesitas un logotipo o una imagen en lugar de texto, usa `ImageStamp`; la misma lógica de ajuste automático existe para el escalado de imágenes.

## Paso 3: Elegir dónde **colocar la marca de agua PDF** – Primera página, última página o índice personalizado

Aspose.Pdf almacena las páginas en una colección basada en 1 (`pdfDocument.Pages[1]` es la primera página). Puedes **colocar la marca de agua PDF** en cualquier página cambiando el índice.

```csharp
// Place the stamp on the first page (index 1)
// To stamp the last page use pdfDocument.Pages[pdfDocument.Pages.Count]
pdfDocument.Pages[1].AddStamp(textStamp);
```

> **Por qué es flexible:** Como la colección `Pages` es mutable, puedes recorrer todas las páginas y añadir la misma marca de agua a cada una, o dirigirte a una página específica según la lógica de negocio (por ejemplo, solo la portada).

## Paso 4: Guardar el documento modificado

Después de marcar, necesitas escribir los cambios en disco. Puedes sobrescribir el archivo original o crear uno nuevo, como prefieras.

```csharp
// Save the stamped PDF – change the path if you don’t want to overwrite
pdfDocument.Save("YOUR_DIRECTORY/output-stamped.pdf");
```

Al abrir `output-stamped.pdf` verás un rectángulo gris claro en la primera página que contiene el texto “Long text that must fit”. Si el texto fuera más largo, Aspose lo reduciría automáticamente hasta que encaje perfectamente dentro del rectángulo de 300 × 100 pt.

## Ejemplo completo funcional

A continuación tienes el programa completo que puedes copiar y pegar en una aplicación de consola (`Program.cs`). Incluye todas las piezas que discutimos, más un pequeño ayudante para verificar que la marca de agua aparece.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;   // Needed for Background and Color

namespace PdfStampDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the source PDF
            using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

            // 2️⃣ Create a text stamp with auto‑adjusting font size
            var textStamp = new TextStamp("Long text that must fit")
            {
                AutoAdjustFontSizeToFitStampRectangle = true,
                AutoAdjustFontSizePrecision = 0.01f,
                Width = 300,
                Height = 100,
                WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
                Background = new Background()
                {
                    Color = Color.LightGray,
                    Opacity = 0.5
                }
            };

            // 3️⃣ Place the stamp on the first page (you can change the index)
            pdfDocument.Pages[1].AddStamp(textStamp);

            // 4️⃣ Save the result
            string outputPath = "YOUR_DIRECTORY/output-stamped.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Stamp added successfully! Check the file at: {outputPath}");
        }
    }
}
```

### Resultado esperado

* El PDF se abre con un cuadro gris semitransparente en la primera página.
* Dentro del cuadro el texto suministrado encaja perfectamente, incluso si lo reemplazas por una frase más larga.
* No se requieren cálculos manuales del tamaño de fuente; Aspose realiza el trabajo pesado.

## Problemas comunes al **colocar una marca de agua PDF**

| Síntoma | Causa probable | Solución |
|---------|----------------|----------|
| El texto se corta | `AutoAdjustFontSizeToFitStampRectangle` está **false** o el rectángulo es demasiado pequeño. | Habilita la bandera y aumenta `Width`/`Height` o reduce la longitud del texto. |
| La marca de agua aparece descentrada | Los valores predeterminados de `HorizontalAlignment`/`VerticalAlignment` son `Left`/`Top`. | Establece `HorizontalAlignment = HorizontalAlignment.Center` y `VerticalAlignment = VerticalAlignment.Center`. |
| La marca de agua no se ve en algunos visores | Opacidad de fondo establecida en 0 o el color de la marca coincide con el fondo de la página. | Usa un `Background.Color` contrastante o establece `Opacity` > 0.3. |
| Varias marcas de agua se superponen | Añadir marcas en un bucle sin ajustar coordenadas. | Utiliza `textStamp.XIndent` y `textStamp.YIndent` para desplazar cada marca. |

Abordar estos problemas desde el principio te ahorrará mucho tiempo de depuración más adelante.

## Extender el ejemplo: agregar una marca de imagen

Si necesitas **agregar una marca de texto PDF** *y* una imagen (por ejemplo, el logotipo de la empresa), puedes combinar ambas:

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    Width = 100,
    Height = 50,
    XIndent = 400,          // Position to the right of the text stamp
    YIndent = 20,
    Background = new Background()
    {
        Color = Color.Transparent
    }
};

pdfDocument.Pages[1].AddStamp(imageStamp);
```

Ahora la página muestra tanto una marca de texto dinámica como una marca de imagen estática una al lado de la otra.

## Probar tu implementación

1. Ejecuta la aplicación de consola.  
2. Abre `output-stamped.pdf` en Adobe Reader, Edge o cualquier visor de PDF.  
3. Verifica que el rectángulo de la marca de agua está presente y que el texto es totalmente visible.  
4. Cambia el texto a una frase más larga, vuelve a ejecutar y confirma que la fuente se reduce automáticamente.

Si algo no se ve bien, revisa las dimensiones del rectángulo y la configuración `AutoAdjustFontSizePrecision`.

## Conclusión

Ahora sabes **cómo agregar una marca de agua** a un PDF usando Aspose.Pdf, cómo **colocar una marca de agua PDF** en una página específica, y cómo **agregar una marca de texto PDF** que ajusta automáticamente su tamaño de fuente. El ejemplo completo y ejecutable anterior elimina la conjetura y te brinda una base sólida para escenarios de marcado más avanzados, como el procesamiento por lotes de docenas de archivos o la adición condicional de marcas de agua.

¿Listo para el siguiente paso? Prueba a marcar cada página en un bucle, experimenta con diferentes fuentes, o combina marcas de imagen y texto para crear un sello de aspecto profesional. El cielo es el límite, y con Aspose.Pdf tienes un motor confiable bajo el capó.

Si encontraste algún obstáculo, deja un comentario o consulta la documentación de Aspose.Pdf para opciones de personalización más profundas. ¡Feliz marcado!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}