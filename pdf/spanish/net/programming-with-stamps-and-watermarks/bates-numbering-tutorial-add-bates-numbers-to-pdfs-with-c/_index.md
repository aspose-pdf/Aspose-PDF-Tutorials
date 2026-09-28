---
category: general
date: 2026-02-25
description: tutorial de numeración Bates – aprende cómo agregar números de página
  PDF y aplicar numeración Bates personalizada usando Aspose.Pdf en C#. Guía paso
  a paso con código completo.
draft: false
keywords:
- bates numbering tutorial
- add page numbers pdf
- how to add bates
- add bates numbering
language: es
og_description: El tutorial de numeración Bates te muestra cómo agregar números de
  página PDF y numeración Bates personalizada en C#. Código completo, explicaciones
  y consejos.
og_title: Tutorial de numeración Bates – Añadir números Bates a PDFs con C#
tags:
- PDF
- C#
- Aspose.Pdf
title: 'Tutorial de numeración Bates: Añadir números Bates a PDFs con C#'
url: /es/net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-bates-numbers-to-pdfs-with-c/
---

.

Now produce final output with all translated content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutorial de numeración Bates – Añadiendo Números Bates a PDFs en C#

¿Alguna vez te has preguntado cómo añadir números de página pdf mientras también incrustas un número Bates de estilo legal? No estás solo. En este **bates numbering tutorial** repasaremos todo lo que necesitas saber para estampar cada página de un PDF con un prefijo personalizado, ceros a la izquierda y una posición precisa—usando Aspose.Pdf para .NET.

¿La buena noticia? Es bastante sencillo una vez que comprendes los conceptos básicos. Al final de esta guía tendrás un programa ejecutable que toma *input.pdf* y genera *bates_out.pdf* con una etiqueta de estilo “ABC‑01000” en cada página. Vamos a sumergirnos.

## Lo que necesitarás

- **Aspose.Pdf for .NET** (versión 23.10 o posterior). La biblioteca es comercial, pero una prueba gratuita funciona perfectamente para aprender.
- SDK .NET 6+ (cualquier versión reciente servirá).
- Un entorno básico de desarrollo C#—Visual Studio, VS Code o Rider.
- Un PDF de entrada para experimentar (cualquier documento de varias páginas ilustrará el efecto).

No se requieren paquetes NuGet adicionales más allá de Aspose.Pdf, y el código se ejecuta en Windows, Linux o macOS sin modificaciones.

## Paso 1: Cargar el documento PDF de origen (bates numbering tutorial – inicialización)

Primero creamos un objeto `Document` que representa el PDF que queremos modificar. Piensa en ello como cargar un lienzo en blanco sobre el que puedes dibujar.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF – replace the path with your actual file location
Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// Quick sanity check – make sure the document actually has pages
if (pdfDocument.Pages.Count == 0)
{
    throw new InvalidOperationException("The PDF you provided contains no pages.");
}
```

**Por qué es importante:** Sin cargar el archivo, no hay nada que anotar. La verificación de validez evita un fallo silencioso más adelante cuando intentas añadir artefactos a una colección de páginas inexistente.

## Paso 2: Definir el artefacto de numeración Bates (cómo añadir bates)

Un *BatesNumberingArtifact* indica a Aspose dónde y cómo dibujar el identificador. Puedes controlar el prefijo, número inicial, relleno de ceros, tamaño de fuente y coordenadas X/Y exactas.

```csharp
// Configure the Bates numbering artifact
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
{
    Prefix = "ABC",          // Text that appears before the number
    Start = 1000,            // First number in the sequence
    LeadingZeros = 5,        // Pad the number with zeros (e.g., 01000)
    FontSize = 9,            // Small enough to sit in the margin
    Position = new Position   // Position measured from the lower‑left corner
    {
        X = 50,               // Horizontal offset (points)
        Y = 30                // Vertical offset (points)
    }
};
```

**Por qué es importante:** La propiedad `LeadingZeros` asegura que cada etiqueta tenga la misma longitud, lo cual es crucial para documentos legales donde la alineación importa. Ajusta `X` y `Y` para mover el sello a la esquina superior derecha, inferior izquierda, o donde tu flujo de trabajo lo requiera.

## Paso 3: Adjuntar el artefacto a cada página (añadir números de página pdf)

Ahora iteramos sobre cada página y adjuntamos el mismo artefacto. Aquí es donde se cumple el requisito de *add page numbers pdf*: cada página recibe automáticamente su propia etiqueta secuencial.

```csharp
// Iterate over each page and add the Bates artifact
foreach (Page page in pdfDocument.Pages)
{
    // The artifact is added to the page's Artifacts collection.
    // Aspose will handle the incrementing of the number for us.
    page.Artifacts.Add(batesArtifact);
}
```

**Por qué es importante:** Al añadir el artefacto a la colección `Artifacts` en lugar de dibujar texto manualmente, dejamos que Aspose gestione la lógica de numeración, los ceros a la izquierda y el renderizado. Esto reduce errores y mantiene el código conciso.

## Paso 4: Guardar el PDF modificado (añadir numeración Bates)

Finalmente, guardamos los cambios en un nuevo archivo. Es una buena práctica escribir con un nombre de archivo diferente para mantener el original intacto.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");

// Optional: let the user know we succeeded
Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
```

**Por qué es importante:** El método `Save` escribe todo el PDF, incrustando los artefactos como parte del flujo de contenido de la página. El archivo resultante puede abrirse en cualquier visor de PDF y mostrará los números Bates exactamente como se especificó.

## Ejemplo completo funcional (Todos los pasos combinados)

A continuación se muestra el programa completo, listo para ejecutarse. Copia‑y‑pega en un proyecto de aplicación de consola, reemplaza las rutas de marcador de posición y pulsa **F5**.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            Document pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
            if (pdfDocument.Pages.Count == 0)
                throw new InvalidOperationException("The PDF you provided contains no pages.");

            // 2️⃣ Configure the Bates numbering artifact
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                Start = 1000,
                LeadingZeros = 5,
                FontSize = 9,
                Position = new Position { X = 50, Y = 30 }
            };

            // 3️⃣ Attach the artifact to every page
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesArtifact);
            }

            // 4️⃣ Save the modified PDF
            pdfDocument.Save("YOUR_DIRECTORY/bates_out.pdf");
            Console.WriteLine("Bates numbering applied successfully! Output saved to bates_out.pdf");
        }
    }
}
```

### Resultado esperado

Abre *bates_out.pdf* en Adobe Reader, Foxit o cualquier visor. Deberías ver una etiqueta como **ABC‑01000** en la primera página, **ABC‑01001** en la segunda, y así sucesivamente, posicionada a 50 pts del borde izquierdo y 30 pts del borde inferior. Los números están alineados a la derecha gracias a los ceros a la izquierda, lo que brinda al documento un aspecto limpio y profesional.

## Variaciones comunes y casos límite

| Escenario | Cómo ajustar |
|----------|---------------|
| **Prefijo diferente** | Cambia `Prefix = "XYZ"` en la definición del artefacto. |
| **Comenzar en un número personalizado** | Establece `Start = 5000` (o cualquier entero). |
| **Colocar el número en la esquina superior derecha** | Usa `Position = new Position { X = pdfDocument.PageInfo.Width - 50, Y = pdfDocument.PageInfo.Height - 30 }`. |
| **Cambiar el tamaño de fuente para documentos más grandes** | Modifica `FontSize = 12` (o cualquier tamaño). |
| **Agregar un rectángulo de fondo** | Crea un `RectangleArtifact` y añádelo antes del `BatesNumberingArtifact`. |
| **Omitir ciertas páginas** | Dentro del bucle `foreach`, agrega un `if (page.Number % 2 == 0) continue;` para omitir páginas pares. |

**Consejo profesional:** Siempre prueba primero con un PDF corto. Es más rápido verificar la posición antes de ejecutar el script en un archivo de caso de 200 páginas.

## Preguntas frecuentes

- **¿Esto funciona con PDFs encriptados?**  
  Aspose.Pdf puede abrir archivos protegidos con contraseña si proporcionas la contraseña mediante `Document(string, string)`. El artefacto Bates seguirá aplicándose después de la desencriptación.

- **¿Puedo añadir tanto números Bates como números de página regulares?**  
  Sí. Añade un `PageNumberArtifact` junto al `BatesNumberingArtifact`. Cada artefacto mantiene su propio contador.

- **¿Qué pasa si mi PDF tiene diferentes tamaños de página?**  
  Los valores de `Position` son puntos absolutos. Para documentos de tamaños mixtos, calcula la posición por página dentro del bucle usando `page.PageInfo.Width` y `page.PageInfo.Height`.

## Próximos pasos y temas relacionados

Ahora que dominas el **bates numbering tutorial**, podrías querer explorar:

- **Añadir marcas de agua** – enfoque de artefacto similar con `TextArtifact`.
- **Combinar varios PDFs** – usa `Document.AppendDocument`.
- **Extraer texto para indexación de búsqueda** – clase `TextAbsorber`.
- **Automatizar procesamiento por lotes** – iterar sobre una carpeta de PDFs y aplicar el mismo artefacto.

Todos estos temas se basan en los mismos conceptos que acabas de aprender, por lo que estás bien posicionado para ampliar tu conjunto de herramientas de automatización de PDFs.

---

*¡Feliz codificación! Si encuentras algún problema o tienes ideas para personalizaciones adicionales, no dudes en dejar un comentario abajo. El mundo de la manipulación de PDFs es amplio, pero con un sólido **bates numbering tutorial** bajo el brazo, ya estás un paso adelante.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}