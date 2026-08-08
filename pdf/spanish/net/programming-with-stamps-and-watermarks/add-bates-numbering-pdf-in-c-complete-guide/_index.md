---
category: general
date: 2026-05-27
description: Agregar numeración Bates a PDF usando Aspose.Pdf en C#. Aprende a agregar
  la numeración Bates rápidamente, personalizar el formato y automatizar el etiquetado
  de documentos legales.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbering
language: es
og_description: Agregar numeración Bates a PDF con Aspose.Pdf en C#. Esta guía muestra
  cómo agregar numeración Bates, configurar prefijos y guardar el resultado.
og_title: Agregar numeración Bates a PDF en C# – Tutorial paso a paso
schemas:
- author: Aspose
  dateModified: '2026-05-27'
  description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  headline: Add Bates Numbering PDF in C# – Complete Guide
  type: TechArticle
- description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  name: Add Bates Numbering PDF in C# – Complete Guide
  steps:
  - name: Expected Output
    text: 'When you run the program, the console prints:'
  - name: Can I position the Bates number elsewhere?
    text: Yes. Use the `BatesNumberingArtifact`’s `Location` property (e.g., `Location
      = new Position(10, 10)`) to place the number at custom X/Y coordinates. You
      can also set `HorizontalAlignment` and `VerticalAlignment` for more control.
  - name: What if my PDF has thousands of pages?
    text: Aspose.Pdf streams pages efficiently, but it’s still a good idea to process
      in batches if you hit memory limits. The `Document` class also supports `PdfConverter`
      for incremental saving.
  - name: How do I change the font or color?
    text: 'Wrap the artifact in a `TextState` object:'
  - name: Do I need a license for production use?
    text: A licensed version removes evaluation watermarks and unlocks full performance.
      The free trial works fine for testing and proof‑of‑concepts.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- Bates numbering
- PDF automation
title: Agregar numeración Bates a PDF en C# – Guía completa
url: /es/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Añadir numeración Bates a PDF en C# – Guía completa

¿Alguna vez te has preguntado **cómo añadir numeración Bates** a un PDF sin pasar horas jugando con herramientas manuales? No estás solo—los equipos legales, auditores y especialistas en e‑discovery necesitan una forma fiable de **añadir numeración Bates a archivos PDF** de forma programática.  

En este tutorial recorreremos una solución concisa, de extremo a extremo, usando Aspose.Pdf para .NET, para que puedas colocar números Bates en cualquier documento con solo unas pocas líneas de código C#.

## Lo que aprenderás

- Cómo abrir un PDF existente con Aspose.Pdf  
- Cómo crear un artefacto de numeración Bates y afinar su formato  
- Cómo adjuntar el artefacto a cada página (o solo a la primera)  
- Cómo guardar el archivo actualizado y verificar el resultado  

No se requiere experiencia previa con Aspose—solo una comprensión básica de C# y .NET. Al final, tendrás un fragmento reutilizable que puedes copiar y pegar en cualquier proyecto.

## Requisitos previos

- .NET 6.0 o superior (el código también funciona en .NET Framework 4.7+)
- Paquete NuGet Aspose.Pdf para .NET (`Install-Package Aspose.Pdf`)
- Un archivo PDF fuente que deseas etiquetar (colócalo en una carpeta a la que puedas referenciar)

> **Consejo profesional:** Si aún no tienes una licencia, Aspose ofrece una clave temporal gratuita que elimina las marcas de agua de evaluación.

## Paso 1 – Abrir el documento PDF fuente  

Primero necesitamos un objeto `Document` que represente el archivo en disco. Piensa en esto como cargar un lienzo en blanco al que luego pintaremos los números Bates.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Adjust the path to point at your source PDF
        string sourcePath = @"C:\Docs\source.pdf";

        // Load the PDF – this is where we start to add Bates numbering
        using (var pdfDocument = new Document(sourcePath))
        {
            // The rest of the logic lives inside this using block
        }
    }
}
```

**Por qué es importante:** Abrir el documento dentro de un bloque `using` asegura que todos los recursos no administrados se liberen rápidamente, lo cual es especialmente importante para PDFs grandes.

## Paso 2 – Crear un artefacto de numeración Bates  

Un *BatesNumberingArtifact* es la forma que Aspose tiene de describir cómo deben verse los números. Puedes establecer un prefijo, número inicial, incremento e incluso una cadena de formato personalizada.

```csharp
// Step 2: Define the Bates numbering artifact
var batesNumbering = new BatesNumberingArtifact
{
    Prefix = "ABC",            // Text that appears before each number
    StartNumber = 1000,        // First number in the sequence
    Increment = 1,             // Step between consecutive numbers
    Format = "{0:D5}"          // Zero‑padded 5‑digit number (e.g., 01000)
};
```

**Por qué podrías cambiar estos valores:**  
- **Prefix** es útil para IDs de casos (“CASE‑”, “DOC‑”).  
- **StartNumber** te permite continuar una serie anterior.  
- **Increment** puede establecerse en 2 si necesitas numeración impar/par.  
- **Format** soporta cualquier formato compuesto de .NET; `{0:D5}` garantiza cinco dígitos con ceros a la izquierda.

## Paso 3 – Adjuntar el artefacto a las páginas deseadas  

Puedes agregar el artefacto a una sola página, a un rango o a todo el documento. Para la mayoría de los flujos de trabajo legales lo adjuntamos a *cada* página, pero el ejemplo a continuación muestra el caso mínimo—agregándolo a la primera página.

```csharp
// Step 3: Attach the artifact to the first page (index is 1‑based)
pdfDocument.Pages[1].Artifacts.Add(batesNumbering);
```

Si necesitas cubrir todas las páginas, recorre un bucle por ellas:

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesNumbering);
}
```

**Por qué este paso es crucial:** Los artefactos se renderizan *después* del contenido de la página, por lo que los números aparecen sobre el texto existente sin alterar el diseño original.

## Paso 4 – Guardar el PDF modificado  

Finalmente, escribe los cambios de vuelta al disco. Puedes sobrescribir el original o crear un nuevo archivo—aquí generaremos una copia nueva llamada `bates.pdf`.

```csharp
// Step 4: Persist the changes
string outputPath = @"C:\Docs\bates.pdf";
pdfDocument.Save(outputPath);

Console.WriteLine($"Bates numbering added successfully. File saved to: {outputPath}");
```

Cuando abras `bates.pdf` verás “ABC01000” (o el formato que hayas elegido) estampado en la ubicación predeterminada—usualmente la esquina inferior derecha.

## Ejemplo completo en funcionamiento  

Juntándolo todo, aquí tienes el programa completo que puedes compilar y ejecutar:

```csharp
using Aspose.Pdf;
using System;

class AddBatesNumbering
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Open the source PDF
        // -----------------------------------------------------------------
        string sourcePath = @"C:\Docs\source.pdf";
        using (var pdfDocument = new Document(sourcePath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Create and configure the Bates numbering artifact
            // -----------------------------------------------------------------
            var batesNumbering = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                StartNumber = 1000,
                Increment = 1,
                Format = "{0:D5}"
            };

            // -----------------------------------------------------------------
            // 3️⃣ Attach the artifact to each page (or a specific page)
            // -----------------------------------------------------------------
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesNumbering);
            }

            // -----------------------------------------------------------------
            // 4️⃣ Save the new PDF
            // -----------------------------------------------------------------
            string outputPath = @"C:\Docs\bates.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbers added. Output: {outputPath}");
        }
    }
}
```

### Salida esperada

Cuando ejecutes el programa, la consola imprime:

```
Bates numbers added. Output: C:\Docs\bates.pdf
```

Al abrir `bates.pdf` se muestra el prefijo “ABC” seguido de una secuencia de cinco dígitos con ceros a la izquierda en cada página—exactamente lo que pediste al código.

## Preguntas comunes y casos límite

### ¿Puedo posicionar el número Bates en otro lugar?

Sí. Usa la propiedad `Location` del `BatesNumberingArtifact` (p. ej., `Location = new Position(10, 10)`) para colocar el número en coordenadas X/Y personalizadas. También puedes establecer `HorizontalAlignment` y `VerticalAlignment` para mayor control.

### ¿Qué pasa si mi PDF tiene miles de páginas?

Aspose.Pdf transmite páginas de manera eficiente, pero sigue siendo una buena idea procesar en lotes si alcanzas límites de memoria. La clase `Document` también soporta `PdfConverter` para guardado incremental.

### ¿Cómo cambio la fuente o el color?

Envuelve el artefacto en un objeto `TextState`:

```csharp
batesNumbering.TextState = new TextState
{
    FontSize = 12,
    Font = FontRepository.FindFont("Arial"),
    ForegroundColor = Color.FromRgb(255, 0, 0) // red
};
```

### ¿Necesito una licencia para uso en producción?

Una versión con licencia elimina las marcas de agua de evaluación y desbloquea el rendimiento completo. La prueba gratuita funciona bien para pruebas y pruebas de concepto.

## Verificación – Comprobación visual rápida  

Si prefieres una verificación automatizada, Aspose puede extraer el texto de una página y confirmar la presencia del prefijo:

```csharp
string pageText = pdfDocument.Pages[1].ExtractText();
bool hasBates = pageText.Contains("ABC01000");
Console.WriteLine(hasBates ? "Bates number verified." : "Number missing!");
```

Ejecutar esto después del paso de guardado imprimirá `Bates number verified.` si todo salió sin problemas.

## Conclusión  

Ahora sabes **cómo añadir numeración Bates a archivos PDF** usando Aspose.Pdf en C#. Desde abrir el documento hasta configurar el artefacto, adjuntarlo a las páginas y guardar el resultado, el proceso es sencillo y totalmente scriptable.  

¿Próximos pasos? Prueba a experimentar con:

- Diferentes valores de `Prefix` para múltiples lotes de casos  
- `Location` y `TextState` personalizados para branding  
- Añadir prefijos específicos por página (p. ej., “VOL‑1‑”, “VOL‑2‑”) ajustando `StartNumber` en cada iteración del bucle  

Estos ajustes te permiten adaptar la solución a casi cualquier flujo de trabajo legal o de archivo.  

¿Tienes más preguntas sobre **cómo añadir numeración Bates** para PDFs multilingües o archivos cifrados? Deja un comentario abajo, ¡y feliz codificación!

## Tutoriales relacionados

- [Cómo añadir y personalizar números de página en PDFs usando Aspose.PDF para .NET | Guía de manipulación de documentos](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Cómo añadir diferentes encabezados en PDF usando Aspose.PDF para .NET: Guía paso a paso](/pdf/english/net/document-manipulation/add-different-headers-aspose-pdf-net/)
- [Cómo añadir un pie de página con sello de texto en PDFs usando Aspose.PDF para .NET: Guía paso a paso](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}